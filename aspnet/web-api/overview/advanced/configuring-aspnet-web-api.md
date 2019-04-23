---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 構成の ASP.NET Web API 2 - ASP.NET 4.x
author: MikeWasson
description: ASP.NET 用の ASP.NET Web API 2 の構成 4.x:設定、ASP.NET 4.x をホストしている、OWIN 自己ホスト、グローバル サービスおよび前のコント ローラーの構成を構成します。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 39629ba404e536b29318db00bce8c4443a782497
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411944"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="c571f-103">ASP.NET Web API 2 の構成</span><span class="sxs-lookup"><span data-stu-id="c571f-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="c571f-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c571f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c571f-105">このトピックでは、ASP.NET Web API を構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c571f-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="c571f-106">構成設定</span><span class="sxs-lookup"><span data-stu-id="c571f-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="c571f-107">ASP.NET ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c571f-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="c571f-108">OWIN 自己ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c571f-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="c571f-109">グローバルな Web API サービス</span><span class="sxs-lookup"><span data-stu-id="c571f-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="c571f-110">コント ローラーごとの構成</span><span class="sxs-lookup"><span data-stu-id="c571f-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="c571f-111">構成設定</span><span class="sxs-lookup"><span data-stu-id="c571f-111">Configuration Settings</span></span>

<span data-ttu-id="c571f-112">Web API の構成設定が定義されている、 [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)クラス。</span><span class="sxs-lookup"><span data-stu-id="c571f-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="c571f-113">メンバー</span><span class="sxs-lookup"><span data-stu-id="c571f-113">Member</span></span> | <span data-ttu-id="c571f-114">説明</span><span class="sxs-lookup"><span data-stu-id="c571f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c571f-115">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="c571f-115">**DependencyResolver**</span></span> | <span data-ttu-id="c571f-116">コント ローラーの依存関係の挿入を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c571f-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="c571f-117">参照してください[、Web API の依存関係競合回避モジュールを使用して](dependency-injection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="c571f-118">**Filters**</span><span class="sxs-lookup"><span data-stu-id="c571f-118">**Filters**</span></span> | <span data-ttu-id="c571f-119">アクション フィルター。</span><span class="sxs-lookup"><span data-stu-id="c571f-119">Action filters.</span></span> |
| <span data-ttu-id="c571f-120">**Formatters**</span><span class="sxs-lookup"><span data-stu-id="c571f-120">**Formatters**</span></span> | <span data-ttu-id="c571f-121">[メディア タイプ フォーマッタ](../formats-and-model-binding/media-formatters.md)です。</span><span class="sxs-lookup"><span data-stu-id="c571f-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="c571f-122">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="c571f-122">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="c571f-123">サーバーが HTTP 応答メッセージで例外メッセージやスタック トレースなどのエラーの詳細を含めるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="c571f-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="c571f-124">参照してください[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))します。</span><span class="sxs-lookup"><span data-stu-id="c571f-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="c571f-125">**Initializer**</span><span class="sxs-lookup"><span data-stu-id="c571f-125">**Initializer**</span></span> | <span data-ttu-id="c571f-126">最終初期化を実行する関数、**HttpConfiguration**です。</span><span class="sxs-lookup"><span data-stu-id="c571f-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="c571f-127">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="c571f-127">**MessageHandlers**</span></span> | <span data-ttu-id="c571f-128">[HTTP メッセージ ハンドラー](http-message-handlers.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="c571f-129">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="c571f-129">**ParameterBindingRules**</span></span> | <span data-ttu-id="c571f-130">コント ローラー アクションのパラメーターをバインドするための規則のコレクション。</span><span class="sxs-lookup"><span data-stu-id="c571f-130">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="c571f-131">**Properties**</span><span class="sxs-lookup"><span data-stu-id="c571f-131">**Properties**</span></span> | <span data-ttu-id="c571f-132">汎用プロパティ バッグ。</span><span class="sxs-lookup"><span data-stu-id="c571f-132">A generic property bag.</span></span> |
| <span data-ttu-id="c571f-133">**Routes**</span><span class="sxs-lookup"><span data-stu-id="c571f-133">**Routes**</span></span> | <span data-ttu-id="c571f-134">ルートのコレクション。</span><span class="sxs-lookup"><span data-stu-id="c571f-134">The collection of routes.</span></span> <span data-ttu-id="c571f-135">参照してください[ASP.NET Web API でルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)です。</span><span class="sxs-lookup"><span data-stu-id="c571f-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c571f-136">**Services**</span><span class="sxs-lookup"><span data-stu-id="c571f-136">**Services**</span></span> | <span data-ttu-id="c571f-137">サービスのコレクション。</span><span class="sxs-lookup"><span data-stu-id="c571f-137">The collection of services.</span></span> <span data-ttu-id="c571f-138">参照してください[Services](#services)です。</span><span class="sxs-lookup"><span data-stu-id="c571f-138">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="c571f-139">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="c571f-139">Prerequisites</span></span>

<span data-ttu-id="c571f-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional、または Enterprise edition。</span><span class="sxs-lookup"><span data-stu-id="c571f-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="c571f-141">ASP.NET ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c571f-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="c571f-142">ASP.NET アプリケーションで、**Application\_Start** メソッドから [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) を呼び出して Web API を設定します。</span><span class="sxs-lookup"><span data-stu-id="c571f-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="c571f-143">**構成**メソッドは型の 1 つのパラメーターを持つデリゲートを受け取ります**HttpConfiguration**します。</span><span class="sxs-lookup"><span data-stu-id="c571f-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="c571f-144">デリゲート内で、構成のすべてを実行します。</span><span class="sxs-lookup"><span data-stu-id="c571f-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="c571f-145">匿名デリゲートの使用例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c571f-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c571f-146">Visual Studio 2017 では、「ASP.NET Web アプリケーション」プロジェクト テンプレートを自動的に設定、構成コードの"Web API"を選択した場合、**新しい ASP.NET プロジェクト**ダイアログ。</span><span class="sxs-lookup"><span data-stu-id="c571f-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="c571f-147">プロジェクト テンプレートは、アプリ内で WebApiConfig.cs という名前のファイルを作成します。\_開始フォルダー。</span><span class="sxs-lookup"><span data-stu-id="c571f-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="c571f-148">このコード ファイルは、Web API の構成コードを配置する必要があります、デリゲートを定義します。</span><span class="sxs-lookup"><span data-stu-id="c571f-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="c571f-149">プロジェクト テンプレートもからデリゲートを呼び出すコードを追加**Application\_Start**です。
</span><span class="sxs-lookup"><span data-stu-id="c571f-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="c571f-150">OWIN 自己ホストによる Web API の構成</span><span class="sxs-lookup"><span data-stu-id="c571f-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="c571f-151">OWIN 自己ホストする場合は、作成、新しい**HttpConfiguration**インスタンス。</span><span class="sxs-lookup"><span data-stu-id="c571f-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="c571f-152">このインスタンスで、任意の構成を実行し、インスタンスを渡す、 **Owin.UseWebApi**拡張メソッド。</span><span class="sxs-lookup"><span data-stu-id="c571f-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="c571f-153">このチュートリアル[Self-Host ASP.NET Web API 2 を使用して OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)は完全な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="c571f-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="c571f-154">グローバルな Web API サービス</span><span class="sxs-lookup"><span data-stu-id="c571f-154">Global Web API Services</span></span>

<span data-ttu-id="c571f-155">**HttpConfiguration.Services**コレクションには、Web API を使用してコント ローラーの選択とコンテンツ ネゴシエーションなどのさまざまなタスクを実行するグローバル サービスのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c571f-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="c571f-156">**サービス**コレクションは、サービスの検出または依存関係の挿入の汎用メカニズムではありません。</span><span class="sxs-lookup"><span data-stu-id="c571f-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="c571f-157">Web API フレームワークに認識されているサービスの種類のみ格納されます。</span><span class="sxs-lookup"><span data-stu-id="c571f-157">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="c571f-158">**サービス**コレクションは、サービスの既定のセットで初期化されており、独自のカスタム実装を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c571f-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="c571f-159">一部のサービスは、インスタンス 1 つだけを持つ他のユーザーに複数のインスタンスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c571f-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="c571f-160">(ただし、コント ローラー レベルでサービスを提供することもできます。 を参照してください[コント ローラーごとの構成](#percontrollerconfig)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="c571f-161">単一インスタンス サービス</span><span class="sxs-lookup"><span data-stu-id="c571f-161">Single-Instance Services</span></span>


| <span data-ttu-id="c571f-162">サービス</span><span class="sxs-lookup"><span data-stu-id="c571f-162">Service</span></span> | <span data-ttu-id="c571f-163">説明</span><span class="sxs-lookup"><span data-stu-id="c571f-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c571f-164">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="c571f-164">**IActionValueBinder**</span></span> | <span data-ttu-id="c571f-165">パラメーターのバインドを取得します。</span><span class="sxs-lookup"><span data-stu-id="c571f-165">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="c571f-166">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="c571f-166">**IApiExplorer**</span></span> | <span data-ttu-id="c571f-167">アプリケーションによって公開される Api の説明を取得します。</span><span class="sxs-lookup"><span data-stu-id="c571f-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="c571f-168">参照してください[Web API のヘルプ ページを作成する](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="c571f-169">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="c571f-169">**IAssembliesResolver**</span></span> | <span data-ttu-id="c571f-170">アプリケーションのアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="c571f-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="c571f-171">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-172">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="c571f-172">**IBodyModelValidator**</span></span> | <span data-ttu-id="c571f-173">要求本文からメディア タイプ フォーマッタによって読み取られるモデルを検証します。</span><span class="sxs-lookup"><span data-stu-id="c571f-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="c571f-174">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="c571f-174">**IContentNegotiator**</span></span> | <span data-ttu-id="c571f-175">コンテンツ ネゴシエーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c571f-175">Performs content negotiation.</span></span> |
| <span data-ttu-id="c571f-176">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="c571f-176">**IDocumentationProvider**</span></span> | <span data-ttu-id="c571f-177">Api のドキュメントを提供します。</span><span class="sxs-lookup"><span data-stu-id="c571f-177">Provides documentation for APIs.</span></span> <span data-ttu-id="c571f-178">既定値は **null**です。</span><span class="sxs-lookup"><span data-stu-id="c571f-178">The default is **null**.</span></span> <span data-ttu-id="c571f-179">参照してください[Web API のヘルプ ページを作成する](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="c571f-180">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="c571f-180">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="c571f-181">ホストで HTTP メッセージのエンティティ ボディをバッファーする必要があるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="c571f-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="c571f-182">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="c571f-182">**IHttpActionInvoker**</span></span> | <span data-ttu-id="c571f-183">コント ローラー アクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c571f-183">Invokes a controller action.</span></span> <span data-ttu-id="c571f-184">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-185">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="c571f-185">**IHttpActionSelector**</span></span> | <span data-ttu-id="c571f-186">コント ローラーのアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c571f-186">Selects a controller action.</span></span> <span data-ttu-id="c571f-187">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-188">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="c571f-188">**IHttpControllerActivator**</span></span> | <span data-ttu-id="c571f-189">コント ローラーがアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="c571f-189">Activates a controller.</span></span> <span data-ttu-id="c571f-190">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-191">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="c571f-191">**IHttpControllerSelector**</span></span> | <span data-ttu-id="c571f-192">コント ローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="c571f-192">Selects a controller.</span></span> <span data-ttu-id="c571f-193">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-194">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="c571f-194">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="c571f-195">アプリケーションで Web API コント ローラーの種類の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="c571f-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="c571f-196">参照してください[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="c571f-197">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="c571f-197">**ITraceManager**</span></span> | <span data-ttu-id="c571f-198">このトレース フレームワークを初期化します。</span><span class="sxs-lookup"><span data-stu-id="c571f-198">Initializes the tracing framework.</span></span> <span data-ttu-id="c571f-199">参照してください[ASP.NET Web API でのトレース](../testing-and-debugging/tracing-in-aspnet-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c571f-200">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="c571f-200">**ITraceWriter**</span></span> | <span data-ttu-id="c571f-201">トレース ライターを提供します。</span><span class="sxs-lookup"><span data-stu-id="c571f-201">Provides a trace writer.</span></span> <span data-ttu-id="c571f-202">既定では"no op"トレース ライターです。</span><span class="sxs-lookup"><span data-stu-id="c571f-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="c571f-203">参照してください[ASP.NET Web API でのトレース](../testing-and-debugging/tracing-in-aspnet-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="c571f-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="c571f-204">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="c571f-204">**IModelValidatorCache**</span></span> | <span data-ttu-id="c571f-205">モデル検証コントロールのキャッシュを提供します。</span><span class="sxs-lookup"><span data-stu-id="c571f-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="c571f-206">複数インスタンスのサービス</span><span class="sxs-lookup"><span data-stu-id="c571f-206">Multiple-Instance Services</span></span>


|                 <span data-ttu-id="c571f-207">サービス</span><span class="sxs-lookup"><span data-stu-id="c571f-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="c571f-208">説明</span><span class="sxs-lookup"><span data-stu-id="c571f-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="c571f-209"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c571f-209"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="c571f-210">コント ローラー アクションのフィルターの一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="c571f-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="c571f-211"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c571f-211"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="c571f-212">指定された型のモデル バインダーを返します。</span><span class="sxs-lookup"><span data-stu-id="c571f-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="c571f-213"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c571f-213"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="c571f-214">モデルのメタデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="c571f-214">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="c571f-215"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="c571f-215"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="c571f-216">モデルの検証コントロールを提供します。</span><span class="sxs-lookup"><span data-stu-id="c571f-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="c571f-217"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="c571f-217"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="c571f-218">値プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="c571f-218">Creates a value provider.</span></span> <span data-ttu-id="c571f-219">詳細については、Mike Stall のブログの投稿を参照してください[WebAPI でカスタム値プロバイダーを作成する方法。](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="c571f-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="c571f-220">マルチ インスタンスのサービスには、カスタム実装を追加するには、呼び出す**追加**または**挿入**上、**サービス**コレクション。</span><span class="sxs-lookup"><span data-stu-id="c571f-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c571f-221">単一インスタンスのサービスをカスタム実装で置き換えるには、呼び出す**置換**上、**サービス**コレクション。</span><span class="sxs-lookup"><span data-stu-id="c571f-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="c571f-222">コント ローラーごとの構成</span><span class="sxs-lookup"><span data-stu-id="c571f-222">Per-Controller Configuration</span></span>

<span data-ttu-id="c571f-223">コント ローラーごとに、次の設定をオーバーライドすることができます。</span><span class="sxs-lookup"><span data-stu-id="c571f-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="c571f-224">メディア タイプ フォーマッタ</span><span class="sxs-lookup"><span data-stu-id="c571f-224">Media-type formatters</span></span>
- <span data-ttu-id="c571f-225">パラメーター バインディング規則</span><span class="sxs-lookup"><span data-stu-id="c571f-225">Parameter binding rules</span></span>
- <span data-ttu-id="c571f-226">Services</span><span class="sxs-lookup"><span data-stu-id="c571f-226">Services</span></span>

<span data-ttu-id="c571f-227">これを行うには、実装するカスタム属性を定義、 **IControllerConfiguration**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="c571f-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="c571f-228">コント ローラーに、属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="c571f-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="c571f-229">次の例では、カスタム フォーマッタで既定のメディア タイプ フォーマッタを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c571f-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="c571f-230">**IControllerConfiguration.Initialize**メソッドは 2 つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c571f-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="c571f-231">**HttpControllerSettings**オブジェクト</span><span class="sxs-lookup"><span data-stu-id="c571f-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="c571f-232">**HttpControllerDescriptor**オブジェクト</span><span class="sxs-lookup"><span data-stu-id="c571f-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="c571f-233">**HttpControllerDescriptor**調べることができます (たとえば、2 つのコント ローラー間で区別するために) 情報提供を目的のコント ローラーの説明が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c571f-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="c571f-234">使用して、 **HttpControllerSettings**コント ローラーを構成するオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="c571f-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="c571f-235">このオブジェクトには、コント ローラーごとにオーバーライドできる構成パラメーターのサブセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c571f-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="c571f-236">すべての設定は変更しないことを既定のグローバル**HttpConfiguration**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="c571f-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
