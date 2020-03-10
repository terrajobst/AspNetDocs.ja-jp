---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2 | でのクロスオリジン要求を有効にするMicrosoft Docs
author: MikeWasson
description: ASP.NET Web API でクロスオリジンリソース共有 (CORS) をサポートする方法を示します。
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447616"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>ASP.NET Web API 2 でのクロスオリジン要求を有効にする

[Mike Wasson](https://github.com/MikeWasson)

> ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。 この制限は、*同一オリジン ポリシー*と呼ばれ、悪意のあるサイトが、別のサイトから機密データを読み取れないようにします。 ただし、他のサイトから Web API を呼び出したほうが良い場合もあります。
>
> [クロスオリジンリソース共有](http://www.w3.org/TR/cors/)(CORS) は、サーバーが同じオリジンポリシーを緩めることを可能にする W3C 標準です。 CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。 CORS は、 [JSONP](http://en.wikipedia.org/wiki/JSONP)など、以前の手法よりも安全で柔軟性に優れています。 このチュートリアルでは、Web API アプリケーションで CORS を有効にする方法について説明します。
>
> ## <a name="software-used-in-the-tutorial"></a>チュートリアルで使用するソフトウェア
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2.2

## <a name="introduction"></a>はじめに

このチュートリアルでは、ASP.NET Web API での CORS のサポートについて説明します。 まず、2つの ASP.NET プロジェクトを作成します。1つは Web API コントローラーをホストする "WebService" と呼ばれ、もう1つは WebService を呼び出す "WebClient" です。 2つのアプリケーションは異なるドメインでホストされているため、WebClient から WebService への AJAX 要求はクロスオリジン要求です。

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>「同一生成元」とは

2 つの URL のスキーム、ホスト、ポートが同じである場合、その URL は同一生成元となります。 ([RFC 6454](http://tools.ietf.org/html/rfc6454))

次の 2 つの URL は生成元が同じです。

- `http://example.com/foo.html`
- `http://example.com/bar.html`

次の URL は、上の URL とは生成元が異なります。

- `http://example.net`-別のドメイン
- `http://example.com:9000/foo.html`-別のポート
- `https://example.com/foo.html`-異なるスキーム
- `http://www.example.com/foo.html`-異なるサブドメイン

> [!NOTE]
> Internet Explorer では、オリジンを比較するときにポートは考慮されません。

## <a name="create-the-webservice-project"></a>WebService プロジェクトを作成する

> [!NOTE]
> このセクションでは、Web API プロジェクトを作成する方法を既に理解していることを前提としています。 それ以外の場合は、「[はじめに ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。

1. Visual Studio を起動し、新しい**ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成します。
2. **[New ASP.NET Web アプリケーション]** ダイアログボックスで、**空**のプロジェクトテンプレートを選択します。 **[のフォルダーとコア参照の追加]** で、 **[Web API]** チェックボックスをオンにします。

   ![Visual Studio の [新しい ASP.NET プロジェクト] ダイアログ](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. 次のコードを使用して、`TestController` という名前の Web API コントローラーを追加します。

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. アプリケーションをローカルで実行するか、Azure にデプロイすることができます。 (このチュートリアルのスクリーンショットでは、アプリが Azure App Service Web Apps にデプロイされます)。Web API が動作していることを確認するには、`http://hostname/api/test/`に移動します。 *hostname*は、アプリケーションを配置したドメインです。 応答テキスト、&quot;GET: Test Message&quot;が表示されます。

   ![テストメッセージを表示している Web ブラウザー](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>WebClient プロジェクトを作成する

1. 別の**ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成し、 **MVC**プロジェクトテンプレートを選択します。 必要に応じて、[認証の**変更** > 認証**なし**] を選択します。 このチュートリアルでは、認証は必要ありません。

   ![Visual Studio の [New ASP.NET Project] ダイアログの MVC テンプレート](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. **ソリューションエクスプローラー**で、 *Views/Home/Index. cshtml*というファイルを開きます。 このファイルのコードを次のコードに置き換えます。

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   *Serviceurl*変数には、WebService アプリの URI を使用します。

3. WebClient アプリをローカルで実行するか、別の web サイトに発行します。

[試してみる] ボタンをクリックすると、ドロップダウンボックスに表示されている HTTP メソッド (GET、POST、または PUT) を使用して、AJAX 要求が WebService アプリに送信されます。 これにより、さまざまなクロスオリジン要求を調べることができます。 現在、WebService アプリでは CORS がサポートされていないため、ボタンをクリックするとエラーが発生します。

![ブラウザーで ' Try it ' エラーが発生しています](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> [Fiddler](https://www.telerik.com/fiddler)のようなツールで HTTP トラフィックを監視すると、ブラウザーが GET 要求を送信したことがわかりますが、要求は成功しますが、AJAX 呼び出しではエラーが返されます。 同じ配信元ポリシーでは、ブラウザーが要求を*送信*できないようにする必要があることを理解しておくことが重要です。 代わりに、アプリケーションで*応答*が表示されないようにします。

![Web 要求を表示している Fiddler web デバッガー](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>CORS を有効にする

次に、WebService アプリで CORS を有効にしましょう。 まず、CORS NuGet パッケージを追加します。 Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

このコマンドを実行すると、最新のパッケージがインストールされ、コア Web API ライブラリを含むすべての依存関係が更新されます。 特定のバージョンを対象にするには、`-Version` フラグを使用します。 CORS パッケージには、Web API 2.0 以降が必要です。

File *App\_Start/webapiconfig.cs*を開きます。 **Webapiconfig.cs**メソッドに次のコードを追加します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

次に、 **[Enablecors]** 属性を `TestController` クラスに追加します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

*オリジン*パラメーターには、WebClient アプリケーションを配置した URI を使用します。 これにより、WebClient からのクロスオリジン要求が可能になりますが、他のすべてのドメイン間要求は引き続き許可されません。 後で、 **[Enablecors]** のパラメーターについてさらに詳しく説明します。

*オリジン*の URL の末尾にスラッシュを含めないでください。

更新された WebService アプリケーションを再デプロイします。 WebClient を更新する必要はありません。 これで、WebClient からの AJAX 要求が成功するはずです。 GET、PUT、および POST メソッドはすべて許可されています。

![成功したテストメッセージを示す Web ブラウザー](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>CORS のしくみ

このセクションでは、HTTP メッセージのレベルでの CORS 要求の動作について説明します。 CORS がどのように機能するかを理解しておくことが重要です。これにより、 **[Enablecors]** 属性を適切に構成し、予期したとおりに動作しない場合にトラブルシューティングを行うことができます。

CORS 仕様には、クロスオリジン要求を有効にするための新しい HTTP ヘッダーがいくつか導入されています。 ブラウザーが CORS をサポートしている場合、クロスオリジン要求に対してこれらのヘッダーが自動的に設定されます。JavaScript コードで特別な操作を行う必要はありません。

クロスオリジン要求の例を次に示します。 "Origin" ヘッダーは、要求を行っているサイトのドメインを示します。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

サーバーが要求を許可している場合は、アクセス制御-許可元ヘッダーが設定されます。 このヘッダーの値は Origin ヘッダーに一致します。または、ワイルドカード値 "\*" であり、すべてのオリジンが許可されることを意味します。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

応答にアクセス制御-許可元ヘッダーが含まれていない場合、AJAX 要求は失敗します。 具体的には、ブラウザーは要求を許可しません。 サーバーが応答を正常に返す場合でも、ブラウザーはクライアントアプリケーションで応答を使用できません。

**プレフライト要求**

一部の CORS 要求については、ブラウザーは "プレフライト要求" と呼ばれる追加の要求を送信してから、リソースに対する実際の要求を送信します。

次の条件に該当する場合、ブラウザーはプレフライト要求をスキップできます。

- 要求メソッドは*GET、HEAD* 、または POST です。
- アプリケーションで*は、accept* 、Accept-Language、Content-type、content-type、または LAST イベント ID 以外の要求ヘッダーは設定されません。
- Content-type ヘッダー (設定されている場合) は、次のいずれかになります。

    - application/x-www-form-urlencoded
    - マルチパート/フォーム-データ
    - text/plain

要求ヘッダーに関する規則は、 **XMLHttpRequest**オブジェクトで**setRequestHeader**を呼び出すことによって、アプリケーションが設定するヘッダーに適用されます。 (CORS 仕様は、これらの "author 要求ヘッダー" を呼び出します)。この規則は、*ブラウザー*が設定できるヘッダー (ユーザーエージェント、ホスト、コンテンツの長さなど) には適用されません。

プレフライト要求の例を次に示します。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

事前フライト要求では、HTTP OPTIONS メソッドを使用します。 次の2つの特殊なヘッダーが含まれます。

- アクセス制御要求メソッド: 実際の要求に使用される HTTP メソッド。
- アクセス制御要求ヘッダー:*アプリケーション*が実際の要求に設定した要求ヘッダーのリスト。 (この場合も、ブラウザーによって設定されるヘッダーは含まれません)。

サーバーが要求を許可していると仮定した場合の応答例を次に示します。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

応答には、許可されたメソッドの一覧を示すアクセス制御許可のヘッダーと、必要に応じて、許可されるヘッダーの一覧を示すアクセス制御-許可ヘッダーヘッダーが含まれています。 プレフライト要求が成功した場合、前に説明したように、ブラウザーは実際の要求を送信します。

プレフライトオプション要求 (たとえば、 [Fiddler](https://www.telerik.com/fiddler)や[Postman](https://www.getpostman.com/)) を使用してエンドポイントをテストするために一般的に使用されるツールは、既定で必要なオプションヘッダーを送信しません。 `Access-Control-Request-Method` ヘッダーと `Access-Control-Request-Headers` ヘッダーが要求と共に送信されること、およびそのオプションヘッダーが IIS を介してアプリに渡されることを確認します。

ASP.NET アプリがオプション要求を受信して処理できるように IIS を構成するには、次の構成を `<system.webServer><handlers>` セクションのアプリの*web.config*ファイルに追加します。

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

`OPTIONSVerbHandler` を削除すると、IIS がオプションの要求を処理できなくなります。 既定のモジュールの登録では、拡張子の Url を使用した GET、HEAD、POST、および DEBUG 要求のみが許可されるため、`ExtensionlessUrlHandler-Integrated-4.0` を置き換えることで、オプションの要求がアプリに到達できるようになります。

## <a name="scope-rules-for-enablecors"></a>[EnableCors] のスコープルール

CORS は、アプリケーション内のすべての Web API コントローラーに対して、アクションごと、コントローラー単位、またはグローバルに有効にすることができます。

**アクションごと**

単一のアクションに対して CORS を有効にするには、アクションメソッドで **[Enablecors]** 属性を設定します。 次の例では、`GetItem` メソッドに対してのみ CORS を有効にします。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**コントローラーごと**

コントローラークラスで **[Enablecors]** を設定すると、コントローラー上のすべてのアクションに適用されます。 アクションに対して CORS を無効にするには、アクションに **[Disablecors]** 属性を追加します。 次の例では、`PutItem`を除くすべてのメソッドに対して CORS を有効にします。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**規模**

アプリケーション内のすべての Web API コントローラーに対して CORS を有効にするには、 **EnableCorsAttribute**インスタンスを**enablecors**メソッドに渡します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

複数のスコープで属性を設定した場合、優先順位は次のようになります。

1. アクション
2. コントローラー
3. グローバル

## <a name="set-the-allowed-origins"></a>許可されるオリジンの設定

**[Enablecors]** 属性の*オリジン*パラメーターは、リソースへのアクセスが許可されているオリジンを指定します。 値は、許可されたオリジンのコンマ区切りのリストです。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

また、任意のオリジンからの要求を許可するために、ワイルドカード値 "\*" を使用することもできます。

配信元からの要求を許可する前に、慎重に検討してください。 これは、文字どおりの web サイトが web API に対して AJAX 呼び出しを行うことができることを意味します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>許可される HTTP メソッドを設定する

**[Enablecors]** 属性の*メソッド*パラメーターでは、リソースへのアクセスを許可する HTTP メソッドを指定します。 すべてのメソッドを許可するには、ワイルドカード値として "\*" を使用します。 次の例では、GET および POST 要求のみが許可されます。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>許可された要求ヘッダーを設定する

この記事では、前に説明したプレフライト要求に、アプリケーションによって設定された HTTP ヘッダー (いわゆる "author 要求ヘッダー") を一覧表示するための、アクセス制御要求ヘッダーヘッダーが含まれている可能性があります。 **[Enablecors]** 属性の*headers*パラメーターでは、許可される作成者要求ヘッダーを指定します。 ヘッダーを許可するには、*ヘッダー*を "\*" に設定します。 特定のヘッダーをホワイトリストに登録するには、*ヘッダー*を、許可されているヘッダーのコンマ区切りの一覧に設定します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

ただし、ブラウザーでは、アクセス制御要求ヘッダーの設定方法が完全に一致しているわけではありません。 たとえば、Chrome には現在 "origin" が含まれています。 FireFox には、アプリケーションでスクリプトに設定されている場合でも、"Accept" などの標準ヘッダーは含まれません。

*ヘッダー*を "\*" 以外に設定する場合は、少なくとも "accept"、"content-type"、および "origin" と、サポートするカスタムヘッダーを含める必要があります。

## <a name="set-the-allowed-response-headers"></a>許可される応答ヘッダーを設定する

既定では、ブラウザーはアプリケーションに応答ヘッダーをすべて公開しません。 既定で使用できる応答ヘッダーは次のとおりです。

- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

CORS 仕様は、これらの[単純な応答ヘッダー](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)を呼び出します。 アプリケーションで他のヘッダーを使用できるようにするには、 **[enablecors]** のパラメーターを設定します。

次の例では、コントローラーの `Get` メソッドによって、' X-Custom ヘッダー ' という名前のカスタムヘッダーが設定されます。 既定では、ブラウザーは、このヘッダーをクロスオリジン要求で公開しません。 ヘッダーを使用できるようにするには、 *exposedHeaders*に ' X-Custom ヘッダー ' を含めます。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>クロスオリジン要求で資格情報を渡す

資格情報では、CORS 要求で特別な処理を行う必要があります。 既定では、ブラウザーは、クロスオリジン要求で資格情報を送信しません。 資格情報には、cookie と HTTP 認証スキームが含まれます。 クロスオリジン要求で資格情報を送信するには、クライアントで**XMLHttpRequest. withCredentials**を true に設定する必要があります。

**XMLHttpRequest**の直接使用:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

JQuery の場合:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

また、サーバーは資格情報を許可する必要があります。 Web API でのクロスオリジンの資格情報を許可するには、 **[Enablecors]** 属性の [ ] プロパティを true に設定します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

このプロパティが true の場合、HTTP 応答には、アクセス制御-許可-資格情報ヘッダーが含まれます。 このヘッダーは、サーバーがクロスオリジン要求に対して資格情報を許可することをブラウザーに指示します。

ブラウザーが資格情報を送信しても、応答に有効なアクセス制御-資格情報のヘッダーが含まれていない場合、ブラウザーはアプリケーションへの応答を公開せず、AJAX 要求は失敗します。

**SupportsCredentials**を true に設定することに注意してください。これは、別のドメインの web サイトがユーザーの代わりに、ログインしているユーザーの資格情報をユーザーの代わりに web API に送信できることを意味します。 また、CORS 仕様では、 **SupportsCredentials**が true の場合、&quot; \*&quot;*の設定が無効になっ*ていることも示されます。

## <a name="custom-cors-policy-providers"></a>カスタム CORS ポリシープロバイダー

**[Enablecors]** 属性は、 **ICorsPolicyProvider**インターフェイスを実装します。 **属性**から派生するクラスを作成し、 **ICorsPolicyProvider**を実装することで、独自の実装を提供できます。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

ここで、 **[Enablecors]** として指定する任意の場所に属性を適用できます。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

たとえば、カスタム CORS ポリシープロバイダーは、構成ファイルから設定を読み取ることができます。

属性を使用する代わりに、 **ICorsPolicyProvider**オブジェクトを作成する**ICorsPolicyProviderFactory**オブジェクトを登録できます。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

**ICorsPolicyProviderFactory**を設定するには、スタートアップ時に**Setcorspolicyproviderfactory**拡張メソッドを呼び出します。次に例を示します。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>ブラウザーのサポート

Web API CORS パッケージは、サーバー側のテクノロジです。 ユーザーのブラウザーも CORS をサポートする必要があります。 幸い、すべての主要なブラウザーの現在のバージョンには[CORS のサポート](http://caniuse.com/cors)が含まれています。
