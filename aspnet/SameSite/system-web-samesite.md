---
title: ASP.NET で SameSite cookie を使用する
author: rick-anderson
description: を使用して ASP.NET でクッキーを SameSite する方法について説明します。
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455707"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET で SameSite cookie を使用する

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフト標準です。 最初は[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)でドラフトされていましたが、draft standard は[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)で更新されました。 更新された標準は以前の標準との下位互換性はありませんが、次のように最も顕著な違いがあります。

* SameSite ヘッダーのない cookie は、既定では `SameSite=Lax` として扱われます。
* クロスサイトクッキーの使用を許可するには、`SameSite=None` を使用する必要があります。
* `SameSite=None` をアサートする cookie も `Secure`としてマークする必要があります。
* [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe)を使用するアプリケーションでは、`<iframe>` はクロスサイトのシナリオとして扱われるため、`sameSite=Lax` または `sameSite=Strict` cookie に関する問題が発生する可能性があります。
* 値 `SameSite=None` は[2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)では許可されていないため、一部の実装では、このような cookie を `SameSite=Strict`として扱います。 このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

`SameSite=Lax` 設定は、ほとんどのアプリケーション cookie に対して機能します。 [OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。 POST ベースのリダイレクトによって SameSite ブラウザーの保護がトリガーされるため、これらのコンポーネントの SameSite は無効になります。 ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。

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

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>.NET アプリの再ターゲット

.NET 4.7.2 以降をターゲットにするには:

* Web.config に次のもの*が含まれていること*を確認します。  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  詳細については、「 [.Net 移行ガイド」](/dotnet/framework/migration-guide/)を参照してください。

* プロジェクトの NuGet パッケージが、正しいバージョンのフレームワークを対象としていることを確認します。 次の例のように、*パッケージの .config*ファイルを調べることで、正しいフレームワークのバージョンを確認できます。

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  上記の*パッケージ .config*ファイルの `Microsoft.ApplicationInsights` パッケージは次のとおりです。
    * は .NET 4.5.1 を対象としています。
    * フレームワークターゲットをターゲットとする更新されたパッケージが存在する場合は、`targetFramework` 属性を `net472` に更新する必要があります。

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>4\.7.2 より前の .NET バージョン

Microsoft では、同じサイトの cookie 属性の書き込みを4.7.2 する .NET バージョンよりもサポートされていません。 次のような信頼性の高い方法が見つかりませんでした。

* ブラウザーのバージョンに基づいて、属性が正しく記述されていることを確認します。
* 以前のバージョンの framework で認証とセッション cookie をインターセプトして調整します。

### <a name="december-patch-behavior-changes"></a>12月のパッチ動作の変更

.NET Framework の特定の動作変更は、`SameSite` プロパティが `None` の値を解釈する方法です。

* パッチの適用前は、次のような `None` の値になります。
  * 属性をまったく生成しません。
* 修正プログラムの適用後:
  * `None`値は、"`None`の値を持つ属性を生成する" ことを意味します。
  * `(SameSiteMode)(-1)` の `SameSite` 値を指定すると、属性は出力されません。

フォーム認証およびセッション状態 cookie の既定の SameSite 値は、`None` から `Lax`に変更されました。

### <a name="summary-of-change-impact-on-browsers"></a>ブラウザーへの変更の影響の概要

修正プログラムをインストールし、`SameSite.None`でクッキーを発行すると、次の2つのいずれかが発生します。
* Chrome v80 は、この cookie を新しい実装に従って扱い、cookie に同じサイト制限を適用しません。
* 新しい実装をサポートするように更新されていないブラウザーは、前の実装に従います。 以前の実装では、次のようになります。
  * 理解していない値が表示された場合は無視し、厳密に同じサイト制限に切り替えます。

そのため、アプリが Chrome で破損しているか、他のさまざまな場所で中断しています。

## <a name="history-and-changes"></a>履歴と変更

SameSite のサポートは、 [2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)を使用して最初に .net 4.7.2 に実装されました。

Windows の2019年11月19日の更新プログラムで、.NET 4.7.2 + が2016標準から2019標準に更新されました。 その他のバージョンの Windows では、追加の更新が予定されています。 詳細については、<xref:samesite/kbs-samesite> を参照してください。

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

2016 SameSite 標準では、不明な値を `SameSite=Strict` 値として処理する必要があることが義務付けられています。 2016 SameSite 標準をサポートする古いブラウザーからアクセスされるアプリは、値が `None`の SameSite プロパティを取得すると壊れます。 Web apps が古いブラウザーをサポートする予定の場合は、ブラウザーの検出を実装する必要があります。 ASP.NET は、ユーザーエージェントの値が変動し頻繁に変更されるため、ブラウザーの検出を実装しません。

Microsoft がこの問題を解決するには、ブラウザーがサポートしていないことがわかっている場合に、ブラウザー検出コンポーネントを実装して cookie から `sameSite=None` 属性を取り除くことができます。 Google のアドバイスは、2つのクッキーを発行することでした。1つは新しい属性で、もう1つは属性なしです。 ただし、Google のアドバイスは限定されています。 一部のブラウザー (特にモバイルブラウザー) では、サイトの cookie の数に関する制限が非常に小さいか、またはドメイン名が送信できます。 複数の cookie を送信すると、特に認証 cookie などの大規模な cookie はモバイルブラウザーの制限に達する可能性があり、その結果、診断や修正が困難なアプリの障害が発生します。 さらに、フレームワークとして、サードパーティのコードとコンポーネントの大規模なエコシステムがあり、二重 cookie のアプローチを使用するように更新することはできません。

[この GitHub リポジトリ]()のサンプルプロジェクトで使用されているブラウザー検出コードは、2つのファイルに含まれています。

* [C#SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

これらの検出は、2016標準をサポートし、属性を完全に削除する必要がある、最も一般的なブラウザーエージェントです。 完全な実装とは言えません。

* テストサイトではないブラウザーがアプリに表示されることがあります。
* 必要に応じて環境に検出を追加できるように準備する必要があります。

検出を接続する方法は、使用している .NET のバージョンと web フレームワークによって異なります。 <xref:HTTP.HttpCookie> 呼び出しサイトで、次のコードを呼び出すことができます。

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

次の ASP.NET 4.7.2 SameSite cookie のトピックを参照してください。

* [C#MVC](xref:samesite/csMVC)
* [C#WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>サイトが HTTPS にリダイレクトされるようにする

ASP.NET 4.x、WebForms、および MVC では、 [IIS の URL 書き換え](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)機能を使用して、すべての要求を HTTPS にリダイレクトすることができます。 次の XML は、ルールの例を示しています。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

[IIS URL 書き換え](https://www.iis.net/downloads/microsoft/url-rewrite)のオンプレミスインストールでは、のインストールが必要になる可能性があるオプションの機能です。

## <a name="test-apps-for-samesite-problems"></a>SameSite 問題のアプリをテストする

サポートされているブラウザーを使用してアプリをテストし、cookie を含むシナリオを確認する必要があります。 Cookie のシナリオには通常、

* ログインフォーム
* Facebook、Azure AD、OAuth、OIDC などの外部ログインメカニズム
* 他のサイトからの要求を受け入れるページ
* Iframe に埋め込まれるように設計されたアプリのページ

アプリで cookie が作成、保存、および削除されたことを確認する必要があります。

サードパーティのログインによってなどのリモートサイトと対話するアプリでは、次の操作を行う必要があります。

* 複数のブラウザーで相互作用をテストします。
* このドキュメントで説明され[ているブラウザーの検出と軽減策](#sob)を適用します。

新しい SameSite 動作にオプトインできるクライアントバージョンを使用して、web アプリをテストします。 Chrome、Firefox、Chromium Edge には、テストに使用できる新しいオプトイン機能フラグがあります。 アプリが SameSite パッチを適用したら、古いクライアントバージョン (特に Safari) を使用してテストします。 詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

### <a name="test-with-chrome"></a>Chrome を使用したテスト

Chrome 78 + には一時的な軽減策があるため、誤解を招く結果になります。 Chrome 78 + 一時的な軽減策では、2分前よりも少ない cookie を使用できます。 適切なテストフラグが有効になっている Chrome 76 または77では、より正確な結果が得られます。 新しい SameSite の動作をテストするには、`chrome://flags/#same-site-by-default-cookies` を**有効**に切り替えます。 新しい `None` 設定で失敗するように、Chrome の旧バージョン (75 以降) が報告されます。 このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

Google では、以前のバージョンの chrome は使用できません。 「 [Chromium のダウンロード](https://www.chromium.org/getting-involved/download-chromium)」の手順に従って、Chrome の旧バージョンをテストします。 以前のバージョンの chrome を検索することによって提供されるリンクから Chrome**をダウンロードしないでください**。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* Windows の64ビット版を使用していない場合は、 [Omahaproxy ビューアー](https://omahaproxy.appspot.com/)を使用して、 [Chromium の指示](https://www.chromium.org/getting-involved/download-chromium)に従って、Chrome 74 (v 74.0.3729.108) に対応する Chromium 分岐を調べることができます。

#### <a name="test-with-chrome-80"></a>Chrome 80 + を使用したテスト

新しい属性をサポートするバージョンの Chrome を[ダウンロード](https://www.google.com/chrome/)します。 このドキュメントの執筆時点では、現在のバージョンは Chrome 80 です。 Chrome 80 では、新しい動作を使用するためにフラグ `chrome://flags/#same-site-by-default-cookies` 有効にする必要があります。 また、sameSite 属性が有効になっていない cookie の今後の動作をテストするには、(`chrome://flags/#cookies-without-same-site-must-be-secure`) を有効にする必要があります。 Chrome 80 はターゲット上にあります。これは、特定の要求に対して一定の猶予期間がある場合でも、`SameSite=Lax`のように属性を持たない cookie をスイッチが処理するようにするためのものです。 時間指定の猶予期間を無効にするには、次のコマンドライン引数を使用して Chrome 80 を起動します。

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 では、不足している sameSite 属性について、ブラウザーコンソールに警告メッセージがあります。 F12 キーを使用してブラウザーコンソールを開きます。

### <a name="test-with-safari"></a>Safari を使用したテスト

Safari 12 では以前のドラフトが厳密に実装されており、新しい `None` 値が cookie に含まれていると失敗します。 このドキュメントでは、[古いブラウザーをサポート](#sob)するブラウザーの検出コードを使用して `None` を回避します。 MSAL、ADAL、使用している任意のライブラリを使用して、Safari 12、Safari 13、WebKit ベースの OS スタイルのログインをテストします。 この問題は、基盤の OS バージョンによって変わります。 OSX Mojave (10.14) と iOS 12 には、新しい SameSite の動作に互換性の問題があることがわかっています。 OS を OSX Catalina.properties (10.15) または iOS 13 にアップグレードすると、問題が解決されます。 Safari には、現在、新しい仕様動作をテストするオプトインフラグがありません。

### <a name="test-with-firefox"></a>Firefox でのテスト

新しい標準の Firefox サポートは、バージョン68以降で、[`about:config`] ページで機能フラグ `network.cookie.sameSite.laxByDefault`をオンにしてテストできます。 以前のバージョンの Firefox との互換性に関する問題は報告されていません。

### <a name="test-with-edge-legacy-browser"></a>Microsoft Edge (レガシ) ブラウザーを使用したテスト

Edge では、古い SameSite 標準がサポートされています。 Edge バージョン44以降では、新しい標準との互換性に関する既知の問題はありません。

### <a name="test-with-edge-chromium"></a>Edge でテストする (Chromium)

SameSite フラグは `edge://flags/#same-site-by-default-cookies` ページで設定されます。 Edge Chromium で互換性の問題は検出されませんでした。

### <a name="test-with-electron"></a>電子を使用したテスト

Electron の複数のバージョンには、Chromium の古いバージョンが含まれています。 たとえば、チームによって使用されている電子 66 Chromium のバージョンは、以前の動作を示しています。 製品で使用されている電子版を使用して、独自の互換性テストを実行する必要があります。 「[古いブラウザーのサポート](#sob)」を参照してください。

## <a name="reverting-samesite-patches"></a>SameSite パッチの復元

.NET Framework アプリで更新された sameSite の動作を、`None`の値に対して sameSite 属性が出力されない以前の動作に戻すことができます。また、認証とセッション cookie を元に戻して値を出力しないようにします。 Chrome の変更によって、標準への変更をサポートするブラウザーを使用しているユーザーの外部 POST 要求または認証が中断されるため、これは*非常に一時的な修正*として表示されます。

### <a name="reverting-net-472-behavior"></a>.NET 4.7.2 の動作を元に戻す

Web.config*を更新*して、次の構成設定を含めます。

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>その他のリソース

* [ASP.NET と ASP.NET Core での今後の SameSite Cookie の変更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie の説明](https://web.dev/samesite-cookies-explained/)
* [Chrome の更新](https://www.chromium.org/updates/same-site)
* [.NET SameSite パッチ](/aspnet/samesite/kbs-samesite)
* [Azure Web アプリケーションと同じサイト情報](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure Active Directory のサイト情報](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
