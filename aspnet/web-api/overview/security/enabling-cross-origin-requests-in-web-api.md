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
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="d234a-103">ASP.NET Web API 2 でのクロスオリジン要求を有効にする</span><span class="sxs-lookup"><span data-stu-id="d234a-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="d234a-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d234a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="d234a-105">ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="d234a-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="d234a-106">この制限は、*同一オリジン ポリシー*と呼ばれ、悪意のあるサイトが、別のサイトから機密データを読み取れないようにします。</span><span class="sxs-lookup"><span data-stu-id="d234a-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="d234a-107">ただし、他のサイトから Web API を呼び出したほうが良い場合もあります。</span><span class="sxs-lookup"><span data-stu-id="d234a-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="d234a-108">[クロスオリジンリソース共有](http://www.w3.org/TR/cors/)(CORS) は、サーバーが同じオリジンポリシーを緩めることを可能にする W3C 標準です。</span><span class="sxs-lookup"><span data-stu-id="d234a-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="d234a-109">CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="d234a-110">CORS は、 [JSONP](http://en.wikipedia.org/wiki/JSONP)など、以前の手法よりも安全で柔軟性に優れています。</span><span class="sxs-lookup"><span data-stu-id="d234a-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="d234a-111">このチュートリアルでは、Web API アプリケーションで CORS を有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d234a-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="d234a-112">チュートリアルで使用するソフトウェア</span><span class="sxs-lookup"><span data-stu-id="d234a-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="d234a-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d234a-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="d234a-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="d234a-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="d234a-115">はじめに</span><span class="sxs-lookup"><span data-stu-id="d234a-115">Introduction</span></span>

<span data-ttu-id="d234a-116">このチュートリアルでは、ASP.NET Web API での CORS のサポートについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d234a-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="d234a-117">まず、2つの ASP.NET プロジェクトを作成します。1つは Web API コントローラーをホストする "WebService" と呼ばれ、もう1つは WebService を呼び出す "WebClient" です。</span><span class="sxs-lookup"><span data-stu-id="d234a-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="d234a-118">2つのアプリケーションは異なるドメインでホストされているため、WebClient から WebService への AJAX 要求はクロスオリジン要求です。</span><span class="sxs-lookup"><span data-stu-id="d234a-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="d234a-119">「同一生成元」とは</span><span class="sxs-lookup"><span data-stu-id="d234a-119">What is "same origin"?</span></span>

<span data-ttu-id="d234a-120">2 つの URL のスキーム、ホスト、ポートが同じである場合、その URL は同一生成元となります。</span><span class="sxs-lookup"><span data-stu-id="d234a-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="d234a-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="d234a-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="d234a-122">次の 2 つの URL は生成元が同じです。</span><span class="sxs-lookup"><span data-stu-id="d234a-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="d234a-123">次の URL は、上の URL とは生成元が異なります。</span><span class="sxs-lookup"><span data-stu-id="d234a-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="d234a-124">`http://example.net`-別のドメイン</span><span class="sxs-lookup"><span data-stu-id="d234a-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="d234a-125">`http://example.com:9000/foo.html`-別のポート</span><span class="sxs-lookup"><span data-stu-id="d234a-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="d234a-126">`https://example.com/foo.html`-異なるスキーム</span><span class="sxs-lookup"><span data-stu-id="d234a-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="d234a-127">`http://www.example.com/foo.html`-異なるサブドメイン</span><span class="sxs-lookup"><span data-stu-id="d234a-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="d234a-128">Internet Explorer では、オリジンを比較するときにポートは考慮されません。</span><span class="sxs-lookup"><span data-stu-id="d234a-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="d234a-129">WebService プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d234a-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="d234a-130">このセクションでは、Web API プロジェクトを作成する方法を既に理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="d234a-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="d234a-131">それ以外の場合は、「[はじめに ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d234a-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="d234a-132">Visual Studio を起動し、新しい**ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d234a-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="d234a-133">**[New ASP.NET Web アプリケーション]** ダイアログボックスで、**空**のプロジェクトテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="d234a-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="d234a-134">**[のフォルダーとコア参照の追加]** で、 **[Web API]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="d234a-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio の [新しい ASP.NET プロジェクト] ダイアログ](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="d234a-136">次のコードを使用して、`TestController` という名前の Web API コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="d234a-137">アプリケーションをローカルで実行するか、Azure にデプロイすることができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="d234a-138">(このチュートリアルのスクリーンショットでは、アプリが Azure App Service Web Apps にデプロイされます)。Web API が動作していることを確認するには、`http://hostname/api/test/`に移動します。 *hostname*は、アプリケーションを配置したドメインです。</span><span class="sxs-lookup"><span data-stu-id="d234a-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="d234a-139">応答テキスト、&quot;GET: Test Message&quot;が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![テストメッセージを表示している Web ブラウザー](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="d234a-141">WebClient プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d234a-141">Create the WebClient project</span></span>

1. <span data-ttu-id="d234a-142">別の**ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成し、 **MVC**プロジェクトテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="d234a-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="d234a-143">必要に応じて、[認証の**変更** > 認証**なし**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d234a-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="d234a-144">このチュートリアルでは、認証は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="d234a-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio の [New ASP.NET Project] ダイアログの MVC テンプレート](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="d234a-146">**ソリューションエクスプローラー**で、 *Views/Home/Index. cshtml*というファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="d234a-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="d234a-147">このファイルのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d234a-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="d234a-148">*Serviceurl*変数には、WebService アプリの URI を使用します。</span><span class="sxs-lookup"><span data-stu-id="d234a-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="d234a-149">WebClient アプリをローカルで実行するか、別の web サイトに発行します。</span><span class="sxs-lookup"><span data-stu-id="d234a-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="d234a-150">[試してみる] ボタンをクリックすると、ドロップダウンボックスに表示されている HTTP メソッド (GET、POST、または PUT) を使用して、AJAX 要求が WebService アプリに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="d234a-151">これにより、さまざまなクロスオリジン要求を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="d234a-152">現在、WebService アプリでは CORS がサポートされていないため、ボタンをクリックするとエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="d234a-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![ブラウザーで ' Try it ' エラーが発生しています](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="d234a-154">[Fiddler](https://www.telerik.com/fiddler)のようなツールで HTTP トラフィックを監視すると、ブラウザーが GET 要求を送信したことがわかりますが、要求は成功しますが、AJAX 呼び出しではエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="d234a-155">同じ配信元ポリシーでは、ブラウザーが要求を*送信*できないようにする必要があることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="d234a-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="d234a-156">代わりに、アプリケーションで*応答*が表示されないようにします。</span><span class="sxs-lookup"><span data-stu-id="d234a-156">Instead, it prevents the application from seeing the *response*.</span></span>

![Web 要求を表示している Fiddler web デバッガー](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="d234a-158">CORS を有効にする</span><span class="sxs-lookup"><span data-stu-id="d234a-158">Enable CORS</span></span>

<span data-ttu-id="d234a-159">次に、WebService アプリで CORS を有効にしましょう。</span><span class="sxs-lookup"><span data-stu-id="d234a-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="d234a-160">まず、CORS NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="d234a-161">Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d234a-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d234a-162">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="d234a-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="d234a-163">このコマンドを実行すると、最新のパッケージがインストールされ、コア Web API ライブラリを含むすべての依存関係が更新されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="d234a-164">特定のバージョンを対象にするには、`-Version` フラグを使用します。</span><span class="sxs-lookup"><span data-stu-id="d234a-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="d234a-165">CORS パッケージには、Web API 2.0 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="d234a-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="d234a-166">File *App\_Start/webapiconfig.cs*を開きます。</span><span class="sxs-lookup"><span data-stu-id="d234a-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="d234a-167">**Webapiconfig.cs**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="d234a-168">次に、 **[Enablecors]** 属性を `TestController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="d234a-169">*オリジン*パラメーターには、WebClient アプリケーションを配置した URI を使用します。</span><span class="sxs-lookup"><span data-stu-id="d234a-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="d234a-170">これにより、WebClient からのクロスオリジン要求が可能になりますが、他のすべてのドメイン間要求は引き続き許可されません。</span><span class="sxs-lookup"><span data-stu-id="d234a-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="d234a-171">後で、 **[Enablecors]** のパラメーターについてさらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="d234a-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="d234a-172">*オリジン*の URL の末尾にスラッシュを含めないでください。</span><span class="sxs-lookup"><span data-stu-id="d234a-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="d234a-173">更新された WebService アプリケーションを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="d234a-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="d234a-174">WebClient を更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d234a-174">You don't need to update WebClient.</span></span> <span data-ttu-id="d234a-175">これで、WebClient からの AJAX 要求が成功するはずです。</span><span class="sxs-lookup"><span data-stu-id="d234a-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="d234a-176">GET、PUT、および POST メソッドはすべて許可されています。</span><span class="sxs-lookup"><span data-stu-id="d234a-176">The GET, PUT, and POST methods are all allowed.</span></span>

![成功したテストメッセージを示す Web ブラウザー](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="d234a-178">CORS のしくみ</span><span class="sxs-lookup"><span data-stu-id="d234a-178">How CORS Works</span></span>

<span data-ttu-id="d234a-179">このセクションでは、HTTP メッセージのレベルでの CORS 要求の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="d234a-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="d234a-180">CORS がどのように機能するかを理解しておくことが重要です。これにより、 **[Enablecors]** 属性を適切に構成し、予期したとおりに動作しない場合にトラブルシューティングを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="d234a-181">CORS 仕様には、クロスオリジン要求を有効にするための新しい HTTP ヘッダーがいくつか導入されています。</span><span class="sxs-lookup"><span data-stu-id="d234a-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="d234a-182">ブラウザーが CORS をサポートしている場合、クロスオリジン要求に対してこれらのヘッダーが自動的に設定されます。JavaScript コードで特別な操作を行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d234a-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="d234a-183">クロスオリジン要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="d234a-184">"Origin" ヘッダーは、要求を行っているサイトのドメインを示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="d234a-185">サーバーが要求を許可している場合は、アクセス制御-許可元ヘッダーが設定されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="d234a-186">このヘッダーの値は Origin ヘッダーに一致します。または、ワイルドカード値 "\*" であり、すべてのオリジンが許可されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d234a-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="d234a-187">応答にアクセス制御-許可元ヘッダーが含まれていない場合、AJAX 要求は失敗します。</span><span class="sxs-lookup"><span data-stu-id="d234a-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="d234a-188">具体的には、ブラウザーは要求を許可しません。</span><span class="sxs-lookup"><span data-stu-id="d234a-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="d234a-189">サーバーが応答を正常に返す場合でも、ブラウザーはクライアントアプリケーションで応答を使用できません。</span><span class="sxs-lookup"><span data-stu-id="d234a-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="d234a-190">**プレフライト要求**</span><span class="sxs-lookup"><span data-stu-id="d234a-190">**Preflight Requests**</span></span>

<span data-ttu-id="d234a-191">一部の CORS 要求については、ブラウザーは "プレフライト要求" と呼ばれる追加の要求を送信してから、リソースに対する実際の要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="d234a-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="d234a-192">次の条件に該当する場合、ブラウザーはプレフライト要求をスキップできます。</span><span class="sxs-lookup"><span data-stu-id="d234a-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="d234a-193">要求メソッドは*GET、HEAD* 、または POST です。</span><span class="sxs-lookup"><span data-stu-id="d234a-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="d234a-194">アプリケーションで*は、accept* 、Accept-Language、Content-type、content-type、または LAST イベント ID 以外の要求ヘッダーは設定されません。</span><span class="sxs-lookup"><span data-stu-id="d234a-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="d234a-195">Content-type ヘッダー (設定されている場合) は、次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="d234a-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="d234a-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="d234a-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="d234a-197">マルチパート/フォーム-データ</span><span class="sxs-lookup"><span data-stu-id="d234a-197">multipart/form-data</span></span>
    - <span data-ttu-id="d234a-198">text/plain</span><span class="sxs-lookup"><span data-stu-id="d234a-198">text/plain</span></span>

<span data-ttu-id="d234a-199">要求ヘッダーに関する規則は、 **XMLHttpRequest**オブジェクトで**setRequestHeader**を呼び出すことによって、アプリケーションが設定するヘッダーに適用されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="d234a-200">(CORS 仕様は、これらの "author 要求ヘッダー" を呼び出します)。この規則は、*ブラウザー*が設定できるヘッダー (ユーザーエージェント、ホスト、コンテンツの長さなど) には適用されません。</span><span class="sxs-lookup"><span data-stu-id="d234a-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="d234a-201">プレフライト要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="d234a-202">事前フライト要求では、HTTP OPTIONS メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="d234a-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="d234a-203">次の2つの特殊なヘッダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d234a-203">It includes two special headers:</span></span>

- <span data-ttu-id="d234a-204">アクセス制御要求メソッド: 実際の要求に使用される HTTP メソッド。</span><span class="sxs-lookup"><span data-stu-id="d234a-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="d234a-205">アクセス制御要求ヘッダー:*アプリケーション*が実際の要求に設定した要求ヘッダーのリスト。</span><span class="sxs-lookup"><span data-stu-id="d234a-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="d234a-206">(この場合も、ブラウザーによって設定されるヘッダーは含まれません)。</span><span class="sxs-lookup"><span data-stu-id="d234a-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="d234a-207">サーバーが要求を許可していると仮定した場合の応答例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="d234a-208">応答には、許可されたメソッドの一覧を示すアクセス制御許可のヘッダーと、必要に応じて、許可されるヘッダーの一覧を示すアクセス制御-許可ヘッダーヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d234a-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="d234a-209">プレフライト要求が成功した場合、前に説明したように、ブラウザーは実際の要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="d234a-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="d234a-210">プレフライトオプション要求 (たとえば、 [Fiddler](https://www.telerik.com/fiddler)や[Postman](https://www.getpostman.com/)) を使用してエンドポイントをテストするために一般的に使用されるツールは、既定で必要なオプションヘッダーを送信しません。</span><span class="sxs-lookup"><span data-stu-id="d234a-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="d234a-211">`Access-Control-Request-Method` ヘッダーと `Access-Control-Request-Headers` ヘッダーが要求と共に送信されること、およびそのオプションヘッダーが IIS を介してアプリに渡されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d234a-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="d234a-212">ASP.NET アプリがオプション要求を受信して処理できるように IIS を構成するには、次の構成を `<system.webServer><handlers>` セクションのアプリの*web.config*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="d234a-213">`OPTIONSVerbHandler` を削除すると、IIS がオプションの要求を処理できなくなります。</span><span class="sxs-lookup"><span data-stu-id="d234a-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="d234a-214">既定のモジュールの登録では、拡張子の Url を使用した GET、HEAD、POST、および DEBUG 要求のみが許可されるため、`ExtensionlessUrlHandler-Integrated-4.0` を置き換えることで、オプションの要求がアプリに到達できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d234a-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="d234a-215">[EnableCors] のスコープルール</span><span class="sxs-lookup"><span data-stu-id="d234a-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="d234a-216">CORS は、アプリケーション内のすべての Web API コントローラーに対して、アクションごと、コントローラー単位、またはグローバルに有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="d234a-217">**アクションごと**</span><span class="sxs-lookup"><span data-stu-id="d234a-217">**Per Action**</span></span>

<span data-ttu-id="d234a-218">単一のアクションに対して CORS を有効にするには、アクションメソッドで **[Enablecors]** 属性を設定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="d234a-219">次の例では、`GetItem` メソッドに対してのみ CORS を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d234a-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="d234a-220">**コントローラーごと**</span><span class="sxs-lookup"><span data-stu-id="d234a-220">**Per Controller**</span></span>

<span data-ttu-id="d234a-221">コントローラークラスで **[Enablecors]** を設定すると、コントローラー上のすべてのアクションに適用されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="d234a-222">アクションに対して CORS を無効にするには、アクションに **[Disablecors]** 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="d234a-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="d234a-223">次の例では、`PutItem`を除くすべてのメソッドに対して CORS を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d234a-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="d234a-224">**規模**</span><span class="sxs-lookup"><span data-stu-id="d234a-224">**Globally**</span></span>

<span data-ttu-id="d234a-225">アプリケーション内のすべての Web API コントローラーに対して CORS を有効にするには、 **EnableCorsAttribute**インスタンスを**enablecors**メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="d234a-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="d234a-226">複数のスコープで属性を設定した場合、優先順位は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d234a-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="d234a-227">アクション</span><span class="sxs-lookup"><span data-stu-id="d234a-227">Action</span></span>
2. <span data-ttu-id="d234a-228">コントローラー</span><span class="sxs-lookup"><span data-stu-id="d234a-228">Controller</span></span>
3. <span data-ttu-id="d234a-229">グローバル</span><span class="sxs-lookup"><span data-stu-id="d234a-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="d234a-230">許可されるオリジンの設定</span><span class="sxs-lookup"><span data-stu-id="d234a-230">Set the allowed origins</span></span>

<span data-ttu-id="d234a-231">**[Enablecors]** 属性の*オリジン*パラメーターは、リソースへのアクセスが許可されているオリジンを指定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="d234a-232">値は、許可されたオリジンのコンマ区切りのリストです。</span><span class="sxs-lookup"><span data-stu-id="d234a-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="d234a-233">また、任意のオリジンからの要求を許可するために、ワイルドカード値 "\*" を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="d234a-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="d234a-234">配信元からの要求を許可する前に、慎重に検討してください。</span><span class="sxs-lookup"><span data-stu-id="d234a-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="d234a-235">これは、文字どおりの web サイトが web API に対して AJAX 呼び出しを行うことができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d234a-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="d234a-236">許可される HTTP メソッドを設定する</span><span class="sxs-lookup"><span data-stu-id="d234a-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="d234a-237">**[Enablecors]** 属性の*メソッド*パラメーターでは、リソースへのアクセスを許可する HTTP メソッドを指定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="d234a-238">すべてのメソッドを許可するには、ワイルドカード値として "\*" を使用します。</span><span class="sxs-lookup"><span data-stu-id="d234a-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="d234a-239">次の例では、GET および POST 要求のみが許可されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="d234a-240">許可された要求ヘッダーを設定する</span><span class="sxs-lookup"><span data-stu-id="d234a-240">Set the allowed request headers</span></span>

<span data-ttu-id="d234a-241">この記事では、前に説明したプレフライト要求に、アプリケーションによって設定された HTTP ヘッダー (いわゆる "author 要求ヘッダー") を一覧表示するための、アクセス制御要求ヘッダーヘッダーが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="d234a-242">**[Enablecors]** 属性の*headers*パラメーターでは、許可される作成者要求ヘッダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="d234a-243">ヘッダーを許可するには、*ヘッダー*を "\*" に設定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="d234a-244">特定のヘッダーをホワイトリストに登録するには、*ヘッダー*を、許可されているヘッダーのコンマ区切りの一覧に設定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="d234a-245">ただし、ブラウザーでは、アクセス制御要求ヘッダーの設定方法が完全に一致しているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="d234a-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="d234a-246">たとえば、Chrome には現在 "origin" が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d234a-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="d234a-247">FireFox には、アプリケーションでスクリプトに設定されている場合でも、"Accept" などの標準ヘッダーは含まれません。</span><span class="sxs-lookup"><span data-stu-id="d234a-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="d234a-248">*ヘッダー*を "\*" 以外に設定する場合は、少なくとも "accept"、"content-type"、および "origin" と、サポートするカスタムヘッダーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="d234a-249">許可される応答ヘッダーを設定する</span><span class="sxs-lookup"><span data-stu-id="d234a-249">Set the allowed response headers</span></span>

<span data-ttu-id="d234a-250">既定では、ブラウザーはアプリケーションに応答ヘッダーをすべて公開しません。</span><span class="sxs-lookup"><span data-stu-id="d234a-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="d234a-251">既定で使用できる応答ヘッダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d234a-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="d234a-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="d234a-252">Cache-Control</span></span>
- <span data-ttu-id="d234a-253">Content-Language</span><span class="sxs-lookup"><span data-stu-id="d234a-253">Content-Language</span></span>
- <span data-ttu-id="d234a-254">Content-Type</span><span class="sxs-lookup"><span data-stu-id="d234a-254">Content-Type</span></span>
- <span data-ttu-id="d234a-255">Expires</span><span class="sxs-lookup"><span data-stu-id="d234a-255">Expires</span></span>
- <span data-ttu-id="d234a-256">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="d234a-256">Last-Modified</span></span>
- <span data-ttu-id="d234a-257">Pragma</span><span class="sxs-lookup"><span data-stu-id="d234a-257">Pragma</span></span>

<span data-ttu-id="d234a-258">CORS 仕様は、これらの[単純な応答ヘッダー](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="d234a-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="d234a-259">アプリケーションで他のヘッダーを使用できるようにするには、 **[enablecors]** のパラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="d234a-260">次の例では、コントローラーの `Get` メソッドによって、' X-Custom ヘッダー ' という名前のカスタムヘッダーが設定されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="d234a-261">既定では、ブラウザーは、このヘッダーをクロスオリジン要求で公開しません。</span><span class="sxs-lookup"><span data-stu-id="d234a-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="d234a-262">ヘッダーを使用できるようにするには、 *exposedHeaders*に ' X-Custom ヘッダー ' を含めます。</span><span class="sxs-lookup"><span data-stu-id="d234a-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="d234a-263">クロスオリジン要求で資格情報を渡す</span><span class="sxs-lookup"><span data-stu-id="d234a-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="d234a-264">資格情報では、CORS 要求で特別な処理を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="d234a-265">既定では、ブラウザーは、クロスオリジン要求で資格情報を送信しません。</span><span class="sxs-lookup"><span data-stu-id="d234a-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="d234a-266">資格情報には、cookie と HTTP 認証スキームが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d234a-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="d234a-267">クロスオリジン要求で資格情報を送信するには、クライアントで**XMLHttpRequest. withCredentials**を true に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="d234a-268">**XMLHttpRequest**の直接使用:</span><span class="sxs-lookup"><span data-stu-id="d234a-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="d234a-269">JQuery の場合:</span><span class="sxs-lookup"><span data-stu-id="d234a-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="d234a-270">また、サーバーは資格情報を許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="d234a-271">Web API でのクロスオリジンの資格情報を許可するには、 **[Enablecors]** 属性の [ ] プロパティを true に設定します。</span><span class="sxs-lookup"><span data-stu-id="d234a-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="d234a-272">このプロパティが true の場合、HTTP 応答には、アクセス制御-許可-資格情報ヘッダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d234a-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="d234a-273">このヘッダーは、サーバーがクロスオリジン要求に対して資格情報を許可することをブラウザーに指示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="d234a-274">ブラウザーが資格情報を送信しても、応答に有効なアクセス制御-資格情報のヘッダーが含まれていない場合、ブラウザーはアプリケーションへの応答を公開せず、AJAX 要求は失敗します。</span><span class="sxs-lookup"><span data-stu-id="d234a-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="d234a-275">**SupportsCredentials**を true に設定することに注意してください。これは、別のドメインの web サイトがユーザーの代わりに、ログインしているユーザーの資格情報をユーザーの代わりに web API に送信できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d234a-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="d234a-276">また、CORS 仕様では、 **SupportsCredentials**が true の場合、&quot; \*&quot;*の設定が無効になっ*ていることも示されます。</span><span class="sxs-lookup"><span data-stu-id="d234a-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="d234a-277">カスタム CORS ポリシープロバイダー</span><span class="sxs-lookup"><span data-stu-id="d234a-277">Custom CORS policy providers</span></span>

<span data-ttu-id="d234a-278">**[Enablecors]** 属性は、 **ICorsPolicyProvider**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="d234a-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="d234a-279">**属性**から派生するクラスを作成し、 **ICorsPolicyProvider**を実装することで、独自の実装を提供できます。</span><span class="sxs-lookup"><span data-stu-id="d234a-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="d234a-280">ここで、 **[Enablecors]** として指定する任意の場所に属性を適用できます。</span><span class="sxs-lookup"><span data-stu-id="d234a-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="d234a-281">たとえば、カスタム CORS ポリシープロバイダーは、構成ファイルから設定を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="d234a-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="d234a-282">属性を使用する代わりに、 **ICorsPolicyProvider**オブジェクトを作成する**ICorsPolicyProviderFactory**オブジェクトを登録できます。</span><span class="sxs-lookup"><span data-stu-id="d234a-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="d234a-283">**ICorsPolicyProviderFactory**を設定するには、スタートアップ時に**Setcorspolicyproviderfactory**拡張メソッドを呼び出します。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="d234a-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="d234a-284">ブラウザーのサポート</span><span class="sxs-lookup"><span data-stu-id="d234a-284">Browser support</span></span>

<span data-ttu-id="d234a-285">Web API CORS パッケージは、サーバー側のテクノロジです。</span><span class="sxs-lookup"><span data-stu-id="d234a-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="d234a-286">ユーザーのブラウザーも CORS をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d234a-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="d234a-287">幸い、すべての主要なブラウザーの現在のバージョンには[CORS のサポート](http://caniuse.com/cors)が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d234a-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
