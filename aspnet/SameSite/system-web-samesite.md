---
title: ASP.NET で SameSite cookie を使用する
author: rick-anderson
description: を使用して ASP.NET でクッキーを SameSite する方法について説明します。
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: d2160bd9aeb93398b49b3a0e5e7a8a4404a5bc63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519194"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET で SameSite cookie を使用する

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフトです。 [SameSite 2019 のドラフト](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* クッキーを既定で `SameSite=Lax` として扱います。
* クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie の状態を `Secure`としてマークする必要があります。

`Lax` は、ほとんどのアプリ cookie で機能します。 [OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。 POST ベースのリダイレクトによって SameSite ブラウザーの保護がトリガーされるため、これらのコンポーネントの SameSite は無効になります。 ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。

`None` パラメーターを指定すると、以前の[2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)(iOS 12 など) を実装したクライアントとの互換性の問題が発生します。 このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。

Cookie を生成する各 ASP.NET コンポーネントは、SameSite が適切かどうかを判断する必要があります。

## <a name="api-usage-with-samesite"></a>SameSite を使用した API の使用

[SameSite プロパティを](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)参照してください HttpCookie

## <a name="history-and-changes"></a>履歴と変更

SameSite のサポートは、 [2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)を使用して最初に .net 4.7.2 に実装されました。

Windows の2019年11月19日の更新プログラムで、.NET 4.7.2 + が2016標準から2019標準に更新されました。 その他のバージョンの Windows では、追加の更新が予定されています。 詳細については、「 <xref:samesite/kbs-samesite>」を参照してください。

 SameSite 仕様の2019ドラフト:

* は、2016ドラフトとの下位互換性が**ありません**。 詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。
* Cookie を既定で `SameSite=Lax` として扱うことを指定します。
* クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie を `Secure`としてマークする必要があることを指定します。 `None` は、オプトアウトする新しいエントリです。
* は、上記の KB に記載されているように発行された修正プログラムによってサポートされています。
* [2 月 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)日に既定で[Chrome](https://chromestatus.com/feature/5088147346030592)によって有効になるようにスケジュールされています。 ブラウザーは2019でこの標準への移行を開始しました。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite cookie 処理

詳細については[、「Azure App Service — SameSite cookie 処理」と「.NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 」を参照してください。

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

## <a name="additional-resources"></a>その他の技術情報

* [Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie の説明](https://web.dev/samesite-cookies-explained/)
