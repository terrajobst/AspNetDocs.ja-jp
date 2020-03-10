---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2-ASP.NET 4.x の構成
author: MikeWasson
description: 'ASP.NET 4.x 用に ASP.NET Web API 2 を構成する: 設定、ASP.NET 4.x ホスト、OWIN 自己ホスト、グローバルサービス、およびコントローラーの事前構成を構成します。'
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449344"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="c2eee-103">ASP.NET Web API 2 の構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="c2eee-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c2eee-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c2eee-105">このトピックでは、ASP.NET Web API を構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="c2eee-106">構成設定</span><span class="sxs-lookup"><span data-stu-id="c2eee-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="c2eee-107">ASP.NET ホスティングを使用した Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="c2eee-108">OWIN 自己ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="c2eee-109">グローバル Web API サービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="c2eee-110">コントローラーごとの構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="c2eee-111">構成設定</span><span class="sxs-lookup"><span data-stu-id="c2eee-111">Configuration Settings</span></span>

<span data-ttu-id="c2eee-112">Web API の構成設定は、 [httpconfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)クラスで定義されています。</span><span class="sxs-lookup"><span data-stu-id="c2eee-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="c2eee-113">メンバー</span><span class="sxs-lookup"><span data-stu-id="c2eee-113">Member</span></span> | <span data-ttu-id="c2eee-114">Description</span><span class="sxs-lookup"><span data-stu-id="c2eee-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2eee-115">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="c2eee-115">**DependencyResolver**</span></span> | <span data-ttu-id="c2eee-116">コントローラーの依存関係の挿入を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c2eee-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="c2eee-117">「 [WEB API 依存関係競合回避モジュールの使用」を](dependency-injection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="c2eee-118">**フィルター**</span><span class="sxs-lookup"><span data-stu-id="c2eee-118">**Filters**</span></span> | <span data-ttu-id="c2eee-119">アクション フィルター。</span><span class="sxs-lookup"><span data-stu-id="c2eee-119">Action filters.</span></span> |
| <span data-ttu-id="c2eee-120">**逆**</span><span class="sxs-lookup"><span data-stu-id="c2eee-120">**Formatters**</span></span> | <span data-ttu-id="c2eee-121">[メディアの種類のフォーマッタ](../formats-and-model-binding/media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="c2eee-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="c2eee-122">**Includeerrorのポリシー**</span><span class="sxs-lookup"><span data-stu-id="c2eee-122">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="c2eee-123">サーバーが HTTP 応答メッセージに例外メッセージやスタックトレースなどのエラーの詳細を含める必要があるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="c2eee-124">「 [Includeerror詳細ポリシー](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="c2eee-125">**初期化**</span><span class="sxs-lookup"><span data-stu-id="c2eee-125">**Initializer**</span></span> | <span data-ttu-id="c2eee-126">**Httpconfiguration**の最終的な初期化を実行する関数。</span><span class="sxs-lookup"><span data-stu-id="c2eee-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="c2eee-127">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="c2eee-127">**MessageHandlers**</span></span> | <span data-ttu-id="c2eee-128">[HTTP メッセージハンドラー](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="c2eee-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="c2eee-129">**ParameterBindingRules もの**</span><span class="sxs-lookup"><span data-stu-id="c2eee-129">**ParameterBindingRules**</span></span> | <span data-ttu-id="c2eee-130">コントローラーアクションのパラメーターをバインドするための規則のコレクション。</span><span class="sxs-lookup"><span data-stu-id="c2eee-130">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="c2eee-131">**Properties**</span><span class="sxs-lookup"><span data-stu-id="c2eee-131">**Properties**</span></span> | <span data-ttu-id="c2eee-132">汎用プロパティバッグ。</span><span class="sxs-lookup"><span data-stu-id="c2eee-132">A generic property bag.</span></span> |
| <span data-ttu-id="c2eee-133">**ルート**</span><span class="sxs-lookup"><span data-stu-id="c2eee-133">**Routes**</span></span> | <span data-ttu-id="c2eee-134">ルートのコレクション。</span><span class="sxs-lookup"><span data-stu-id="c2eee-134">The collection of routes.</span></span> <span data-ttu-id="c2eee-135">「 [ASP.NET Web API でのルーティング」を](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c2eee-136">**サービス**</span><span class="sxs-lookup"><span data-stu-id="c2eee-136">**Services**</span></span> | <span data-ttu-id="c2eee-137">サービスのコレクション。</span><span class="sxs-lookup"><span data-stu-id="c2eee-137">The collection of services.</span></span> <span data-ttu-id="c2eee-138">「[サービス](#services)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-138">See [Services](#services).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="c2eee-139">前提条件</span><span class="sxs-lookup"><span data-stu-id="c2eee-139">Prerequisites</span></span>

<span data-ttu-id="c2eee-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional、または Enterprise エディション。</span><span class="sxs-lookup"><span data-stu-id="c2eee-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="c2eee-141">ASP.NET ホスティングを使用した Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="c2eee-142">ASP.NET アプリケーションで、Globalconfiguration を呼び出して Web API を構成[します。](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) **application\_Start**メソッドを構成します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="c2eee-143">**Configure**メソッドは、 **httpconfiguration**型の1つのパラメーターを持つデリゲートを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c2eee-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="c2eee-144">デリゲート内ですべての構成を実行します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="c2eee-145">匿名デリゲートを使用した例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c2eee-146">Visual Studio 2017 では、**新しい ASP.NET プロジェクト** ダイアログボックスで web API を選択した場合、"ASP.NET Web Application" プロジェクトテンプレートによって構成コードが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="c2eee-147">プロジェクトテンプレートによって、WebApiConfig.cs という名前のファイルがアプリ\_の [開始] フォルダー内に作成されます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="c2eee-148">このコードファイルは、Web API 構成コードを配置する必要があるデリゲートを定義します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="c2eee-149">また、プロジェクトテンプレートによって、アプリケーションからデリゲートを呼び出すコード **\_開始**します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="c2eee-150">OWIN 自己ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="c2eee-151">OWIN を使用して自己ホストしている場合は、新しい**Httpconfiguration**インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="c2eee-152">このインスタンスで構成を実行し、インスタンスを**UseWebApi**拡張メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="c2eee-153">このチュートリアルでは、 [OWIN を自己ホスト ASP.NET Web API 2 に使用](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)して、完全な手順を示します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="c2eee-154">グローバル Web API サービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-154">Global Web API Services</span></span>

<span data-ttu-id="c2eee-155">**Httpconfiguration. Services**コレクションには、コントローラーの選択やコンテンツネゴシエーションなどのさまざまなタスクを実行するために Web API で使用される一連のグローバルサービスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c2eee-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="c2eee-156">サービス**コレクションは**、サービスの検出または依存関係の挿入のための汎用的なメカニズムではありません。</span><span class="sxs-lookup"><span data-stu-id="c2eee-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="c2eee-157">Web API フレームワークに認識されているサービスの種類のみを格納します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-157">It only stores service types that are known to the Web API framework.</span></span>

<span data-ttu-id="c2eee-158">**サービス**コレクションは、既定のサービスのセットを使用して初期化され、独自のカスタム実装を提供できます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="c2eee-159">一部のサービスでは複数のインスタンスがサポートされていますが、インスタンスは1つしか持つことができません。</span><span class="sxs-lookup"><span data-stu-id="c2eee-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="c2eee-160">(ただし、コントローラーレベルでサービスを提供することもできます。「[コントローラーごとの構成](#percontrollerconfig)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="c2eee-161">単一インスタンスサービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-161">Single-Instance Services</span></span>

| <span data-ttu-id="c2eee-162">サービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-162">Service</span></span> | <span data-ttu-id="c2eee-163">Description</span><span class="sxs-lookup"><span data-stu-id="c2eee-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2eee-164">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="c2eee-164">**IActionValueBinder**</span></span> | <span data-ttu-id="c2eee-165">パラメーターのバインディングを取得します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-165">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="c2eee-166">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="c2eee-166">**IApiExplorer**</span></span> | <span data-ttu-id="c2eee-167">アプリケーションによって公開されている Api の説明を取得します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="c2eee-168">「 [WEB API のヘルプページを作成](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="c2eee-169">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="c2eee-169">**IAssembliesResolver**</span></span> | <span data-ttu-id="c2eee-170">アプリケーションのアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="c2eee-171">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-172">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="c2eee-172">**IBodyModelValidator**</span></span> | <span data-ttu-id="c2eee-173">メディアタイプフォーマッタによって要求本文から読み取られるモデルを検証します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="c2eee-174">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="c2eee-174">**IContentNegotiator**</span></span> | <span data-ttu-id="c2eee-175">コンテンツ ネゴシエーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-175">Performs content negotiation.</span></span> |
| <span data-ttu-id="c2eee-176">**Idocumentation プロバイダー**</span><span class="sxs-lookup"><span data-stu-id="c2eee-176">**IDocumentationProvider**</span></span> | <span data-ttu-id="c2eee-177">Api のドキュメントを提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-177">Provides documentation for APIs.</span></span> <span data-ttu-id="c2eee-178">既定値は **null**です。</span><span class="sxs-lookup"><span data-stu-id="c2eee-178">The default is **null**.</span></span> <span data-ttu-id="c2eee-179">「 [WEB API のヘルプページを作成](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="c2eee-180">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="c2eee-180">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="c2eee-181">ホストが HTTP メッセージエンティティ本体をバッファーする必要があるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="c2eee-182">**IHttpActionInvoker 元**</span><span class="sxs-lookup"><span data-stu-id="c2eee-182">**IHttpActionInvoker**</span></span> | <span data-ttu-id="c2eee-183">コントローラーアクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-183">Invokes a controller action.</span></span> <span data-ttu-id="c2eee-184">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-185">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="c2eee-185">**IHttpActionSelector**</span></span> | <span data-ttu-id="c2eee-186">コントローラーアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-186">Selects a controller action.</span></span> <span data-ttu-id="c2eee-187">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-188">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="c2eee-188">**IHttpControllerActivator**</span></span> | <span data-ttu-id="c2eee-189">コントローラーをアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="c2eee-189">Activates a controller.</span></span> <span data-ttu-id="c2eee-190">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-191">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="c2eee-191">**IHttpControllerSelector**</span></span> | <span data-ttu-id="c2eee-192">コントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-192">Selects a controller.</span></span> <span data-ttu-id="c2eee-193">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-194">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="c2eee-194">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="c2eee-195">アプリケーションの Web API コントローラーの種類の一覧を提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="c2eee-196">「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c2eee-197">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="c2eee-197">**ITraceManager**</span></span> | <span data-ttu-id="c2eee-198">トレースフレームワークを初期化します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-198">Initializes the tracing framework.</span></span> <span data-ttu-id="c2eee-199">「 [ASP.NET Web API でのトレース」を](../testing-and-debugging/tracing-in-aspnet-web-api.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c2eee-200">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="c2eee-200">**ITraceWriter**</span></span> | <span data-ttu-id="c2eee-201">トレースライターを提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-201">Provides a trace writer.</span></span> <span data-ttu-id="c2eee-202">既定値は "no op" トレースライターです。</span><span class="sxs-lookup"><span data-stu-id="c2eee-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="c2eee-203">「 [ASP.NET Web API でのトレース」を](../testing-and-debugging/tracing-in-aspnet-web-api.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c2eee-204">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="c2eee-204">**IModelValidatorCache**</span></span> | <span data-ttu-id="c2eee-205">モデルの検証コントロールのキャッシュを提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="c2eee-206">複数インスタンスサービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-206">Multiple-Instance Services</span></span>

|                 <span data-ttu-id="c2eee-207">サービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="c2eee-208">Description</span><span class="sxs-lookup"><span data-stu-id="c2eee-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="c2eee-209"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c2eee-209"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="c2eee-210">コントローラーアクションのフィルターの一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="c2eee-211"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c2eee-211"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="c2eee-212">指定された型のモデルバインダーを返します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="c2eee-213"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c2eee-213"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="c2eee-214">モデルのメタデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-214">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="c2eee-215"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c2eee-215"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="c2eee-216">モデルの検証コントロールを提供します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="c2eee-217"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="c2eee-217"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="c2eee-218">値プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-218">Creates a value provider.</span></span> <span data-ttu-id="c2eee-219">詳細については、「 [WebAPI でカスタム値プロバイダーを作成する方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2eee-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="c2eee-220">カスタム実装をマルチインスタンスサービスに追加するには、**サービス**コレクションで**Add**または**Insert**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c2eee-221">単一インスタンスサービスをカスタム実装に置き換えるには、**サービス**コレクションで**replace**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="c2eee-222">コントローラーごとの構成</span><span class="sxs-lookup"><span data-stu-id="c2eee-222">Per-Controller Configuration</span></span>

<span data-ttu-id="c2eee-223">次の設定は、コントローラーごとにオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="c2eee-224">メディアの種類のフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="c2eee-224">Media-type formatters</span></span>
- <span data-ttu-id="c2eee-225">パラメーターのバインド規則</span><span class="sxs-lookup"><span data-stu-id="c2eee-225">Parameter binding rules</span></span>
- <span data-ttu-id="c2eee-226">サービス</span><span class="sxs-lookup"><span data-stu-id="c2eee-226">Services</span></span>

<span data-ttu-id="c2eee-227">これを行うには、 **IControllerConfiguration**インターフェイスを実装するカスタム属性を定義します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="c2eee-228">次に、コントローラーに属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="c2eee-229">既定のメディアタイプフォーマッタをカスタムフォーマッタに置き換える例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="c2eee-230">**IControllerConfiguration**メソッドは、次の2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c2eee-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="c2eee-231">**Httpコントローラー設定**オブジェクト</span><span class="sxs-lookup"><span data-stu-id="c2eee-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="c2eee-232">**Httpコントローラー記述子**オブジェクト</span><span class="sxs-lookup"><span data-stu-id="c2eee-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="c2eee-233">**Httpcontroller 記述子**には、コントローラーの説明が含まれています。これは、2つのコントローラーを区別するために、情報を調べるために使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="c2eee-234">**Httpcontroller 設定**オブジェクトを使用してコントローラーを構成します。</span><span class="sxs-lookup"><span data-stu-id="c2eee-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="c2eee-235">このオブジェクトには、コントローラーごとにオーバーライドできる構成パラメーターのサブセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c2eee-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="c2eee-236">変更しない設定は、既定でグローバル**Httpconfiguration**オブジェクトに設定されます。</span><span class="sxs-lookup"><span data-stu-id="c2eee-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
