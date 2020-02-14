---
title: ASP.NET で SameSite cookie を使用する
author: rick-anderson
description: を使用して ASP.NET でクッキーを SameSite する方法について説明します。
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c262e300361f33621e8bd126a34b251c23f56e1a
ms.sourcegitcommit: 6bd0d7581ec36dc32cb85d0d5fc0e51068dd4423
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2020
ms.locfileid: "77234763"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET で SameSite cookie を使用する

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフト標準です。 最初は[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)でドラフトされていましたが、draft standard は[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)で更新されました。 更新された標準は以前の標準との下位互換性はありませんが、次のように最も顕著な違いがあります。

* SameSite ヘッダーのない cookie は、既定では `SameSite=Lax` として扱われます。
* クロスサイトクッキーの使用を許可するには、`SameSite=None` を使用する必要があります。
* `SameSite=None` をアサートする cookie も `Secure`としてマークする必要があります。
* 値 SameSite = None は[2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)では許可されていません。また、一部の実装では、このような Cookie を SameSite = Strict として扱います。 このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

`SameSite=Lax` 設定は、ほとんどのアプリケーション cookie に対して機能します。 [OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。 POST ベースのリダイレクトによって SameSite ブラウザーの保護がトリガーされるため、これらのコンポーネントの SameSite は無効になります。 ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。

`iframe` を使用するアプリケーションでは、iframe はクロスサイトシナリオとして扱われるため、`SameSite=Lax` または `SameSite=Strict` cookie に関する問題が発生する可能性があります。

Cookie を生成する各 ASP.NET コンポーネントは、SameSite が適切かどうかを判断する必要があります。

2019 .Net SameSite の更新プログラムをインストールした後のアプリケーションの問題に関する[既知の問題](#known)を参照してください。

## <a name="using-samesite-in-aspnet-472-and-48"></a>ASP.NET 4.7.2 と4.8 での SameSite の使用

.Net 4.7.2 と4.8 では、年 12 2019 月に更新プログラムがリリースされてから、SameSite の[2019 ドラフト標準](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)がサポートされています。 開発者は、 [HttpCookie プロパティ](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)を使用して、SameSite ヘッダーの値をプログラムで制御できます。 `SameSite` プロパティを `Strict`、`Lax`、または `None` に設定すると、これらの値が cookie を使用してネットワーク上に書き込まれます。 これを `(SameSiteMode)(-1)` に設定すると、cookie を使用してネットワークに SameSite ヘッダーを含める必要がなくなります。 構成ファイルの[HttpCookie プロパティ](/dotnet/api/system.web.httpcookie.secure)または ' requireSSL ' を使用して、cookie を `Secure` としてマークできます。

新しい `HttpCookie` インスタンスは、既定で `SameSite=(SameSiteMode)(-1)` と `Secure=false`になります。 これらの既定値は、`system.web/httpCookies` 構成セクションでオーバーライドできます。この場合、文字列 `"Unspecified"` は `(SameSiteMode)(-1)`のわかりやすい構成のみの構文です。

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

また、ASP.Net は、匿名認証、フォーム認証、セッション状態、ロール管理といった機能について、独自の4つの cookie を発行します。 ランタイムで取得したこれらのクッキーのインスタンスは、他の HttpCookie インスタンスと同様に、`SameSite` と `Secure` のプロパティを使用して操作できます。 ただし、SameSite 標準の寄せ集めが発生しているため、これらの4つの機能の構成オプションには一貫性がありません。 関連する構成セクションと属性 (既定値) を以下に示します。 フィーチャーに `SameSite` または `Secure` 関連属性がない場合、この機能は、前述の `system.web/httpCookies` セクションで構成されている既定値にフォールバックします。

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**注**: ' 未指定 ' は、現時点では `system.web/httpCookies@sameSite` にのみ使用できます。 今後の更新で、以前に表示されていた cookieSameSite 属性に同様の構文を追加することを願っています。 コード内の `(SameSiteMode)(-1)` の設定は、これらの cookie のインスタンスでも機能します。 *

## <a name="history-and-changes"></a>履歴と変更

SameSite のサポートは、 [2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)を使用して最初に .net 4.7.2 に実装されました。

Windows の2019年11月19日の更新プログラムで、.NET 4.7.2 + が2016標準から2019標準に更新されました。 その他のバージョンの Windows では、追加の更新が予定されています。 詳細については、「 <xref:samesite/kbs-samesite>」を参照してください。

 SameSite 仕様の2019ドラフト:

* は、2016ドラフトとの下位互換性が**ありません**。 詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。
* Cookie を既定で `SameSite=Lax` として扱うことを指定します。
* クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie も `Secure`としてマークするように指定します。
* は、上記の KB に記載されているように発行された修正プログラムによってサポートされています。
* [2 月 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)日に既定で[Chrome](https://chromestatus.com/feature/5088147346030592)によって有効になるようにスケジュールされています。 ブラウザーは2019でこの標準への移行を開始しました。

<a name="known"><a/>

## <a name="known-issues"></a>既知の問題

2016と2019のドラフト仕様には互換性がないため、11 2019 月の .Net Framework の更新プログラムでは、いくつかの変更が行われている可能性があります。

* セッション状態とフォーム認証 cookie が、未指定ではなく `Lax` としてネットワークに書き込まれるようになりました。
  * ほとんどのアプリは `SameSite=Lax` cookie で動作しますが、`iframe` を使用するサイトまたはアプリケーションに投稿するアプリでは、セッション状態またはフォーム認証 cookie が想定どおりに使用されていないことがわかります。 これを解決するには、前述のように、適切な構成セクションの `cookieSameSite` 値を変更します。
* コードまたは構成で明示的に `SameSite=None` を設定する HttpCookies では、以前は省略されていましたが、この値は cookie で記述されています。 これにより、2016ドラフト標準のみをサポートする古いブラウザーで問題が発生する可能性があります。
  * `SameSite=None` cookie を使用して2019ドラフト標準をサポートするブラウザーを対象としている場合は、`Secure` にマークしたり、認識されなかったりすることを忘れないでください。
  * `SameSite=None`を書き込まない場合の2016の動作に戻すには、アプリ設定 `aspnet:SupressSameSiteNone=true`を使用します。 これは、アプリ内のすべての HttpCookies に適用されることに注意してください。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite cookie 処理

.Net 4.7.2 アプリで SameSite の動作を構成 Azure App Service する方法の詳細については[、「Azure App Service — SameSite cookie 処理」と「.NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 」を参照してください。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>古いブラウザーのサポート

2016 SameSite 標準では、不明な値を `SameSite=Strict` 値として処理する必要があることが義務付けられています。 2016 SameSite 標準をサポートする古いブラウザーからアクセスされるアプリは、値が `None`の SameSite プロパティを取得すると壊れます。 Web apps が古いブラウザーをサポートする予定の場合は、ブラウザーの検出を実装する必要があります。 ASP.NET は、ユーザーエージェントの値が変動し頻繁に変更されるため、ブラウザーの検出を実装しません。 <xref:HTTP.HttpCookie> 呼び出しサイトで、次のコードを呼び出すことができます。

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

前のサンプルの `MyUserAgentDetectionLib.DisallowsSameSiteNone` は、ユーザーエージェントが SameSite `None`をサポートしていないかどうかを検出するユーザー指定のライブラリです。 次のコードは、`DisallowsSameSiteNone` メソッドの例を示しています。

> [!WARNING]
> 次のコードは、デモンストレーションのみを対象としています。
> * 完全であるとは限りません。
> * 管理されていないか、サポートされていません。

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>SameSite 問題のアプリをテストする

サードパーティのログインによってなどのリモートサイトと対話するアプリでは、次の操作を行う必要があります。

* 複数のブラウザーで相互作用をテストします。
* このドキュメントで説明され[ているブラウザーの検出と軽減策](#sob)を適用します。

新しい SameSite 動作にオプトインできるクライアントバージョンを使用して、web アプリをテストします。 Chrome、Firefox、Chromium Edge には、テストに使用できる新しいオプトイン機能フラグがあります。 アプリが SameSite パッチを適用したら、古いクライアントバージョン (特に Safari) を使用してテストします。 詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

### <a name="test-with-chrome"></a>Chrome を使用したテスト

Chrome 78 + には一時的な軽減策があるため、誤解を招く結果になります。 Chrome 78 + 一時的な軽減策では、2分前よりも少ない cookie を使用できます。 適切なテストフラグが有効になっている Chrome 76 または77では、より正確な結果が得られます。 新しい SameSite の動作をテストするには、`chrome://flags/#same-site-by-default-cookies` を**有効**に切り替えます。 新しい `None` 設定で失敗するように、Chrome の旧バージョン (75 以降) が報告されます。 このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

Google では、以前のバージョンの chrome は使用できません。 「 [Chromium のダウンロード](https://www.chromium.org/getting-involved/download-chromium)」の手順に従って、Chrome の旧バージョンをテストします。 以前のバージョンの chrome を検索することによって提供されるリンクから Chrome**をダウンロードしないでください**。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Safari を使用したテスト

Safari 12 では以前のドラフトが厳密に実装されており、新しい `None` 値が cookie に含まれていると失敗します。 このドキュメントでは、[古いブラウザーをサポート](#sob)するブラウザーの検出コードを使用して `None` を回避します。 MSAL、ADAL、使用している任意のライブラリを使用して、Safari 12、Safari 13、WebKit ベースの OS スタイルのログインをテストします。 この問題は、基盤の OS バージョンによって変わります。 OSX Mojave (10.14) と iOS 12 には、新しい SameSite の動作に互換性の問題があることがわかっています。 OS を OSX Catalina.properties (10.15) または iOS 13 にアップグレードすると、問題が解決されます。 Safari には、現在、新しい仕様動作をテストするオプトインフラグがありません。

### <a name="test-with-firefox"></a>Firefox でのテスト

新しい標準の Firefox サポートは、バージョン68以降で、[`about:config`] ページで機能フラグ `network.cookie.sameSite.laxByDefault`をオンにしてテストできます。 以前のバージョンの Firefox との互換性に関する問題は報告されていません。

### <a name="test-with-edge-browser"></a>Edge ブラウザーを使用したテスト

Edge では、古い SameSite 標準がサポートされています。 Edge バージョン44には、新しい標準との互換性に関する既知の問題はありません。

### <a name="test-with-edge-chromium"></a>Edge でテストする (Chromium)

SameSite フラグは `edge://flags/#same-site-by-default-cookies` ページで設定されます。 Edge Chromium で互換性の問題は検出されませんでした。

### <a name="test-with-electron"></a>電子を使用したテスト

Electron の複数のバージョンには、Chromium の古いバージョンが含まれています。 たとえば、チームによって使用されている電子 66 Chromium のバージョンは、以前の動作を示しています。 製品で使用されている電子版を使用して、独自の互換性テストを実行する必要があります。 次のセクションの「[古いブラウザーのサポート](#sob)」を参照してください。

## <a name="additional-resources"></a>その他のリソース

* [ASP.NET と ASP.NET Core での今後の SameSite Cookie の変更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie の説明](https://web.dev/samesite-cookies-explained/)
