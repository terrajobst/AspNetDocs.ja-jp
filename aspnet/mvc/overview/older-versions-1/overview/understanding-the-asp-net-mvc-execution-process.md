---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 実行プロセスについて |Microsoft Docs
author: microsoft
description: ASP.NET MVC フレームワークがブラウザーの要求を処理する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435454"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="1d16a-103">ASP.NET MVC 実行プロセスを理解する</span><span class="sxs-lookup"><span data-stu-id="1d16a-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="1d16a-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1d16a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1d16a-105">ASP.NET MVC フレームワークがブラウザーの要求を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="1d16a-106">ASP.NET MVC ベースの Web アプリケーションに対する要求は、まず、HTTP モジュールである**Urlroutingmodule**オブジェクトをパススルーします。</span><span class="sxs-lookup"><span data-stu-id="1d16a-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="1d16a-107">このモジュールは、要求を解析してルートの選択を行います。</span><span class="sxs-lookup"><span data-stu-id="1d16a-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="1d16a-108">**Urlroutingmodule**オブジェクトは、現在の要求に一致する最初のルートオブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="1d16a-109">ルートオブジェクトは**Routebase**を実装するクラスであり、通常は**route**クラスのインスタンスです。一致するルートがない場合、 **Urlroutingmodule**オブジェクトは何も行いません。これにより、要求は通常の ASP.NET または IIS 要求の処理に戻されます。</span><span class="sxs-lookup"><span data-stu-id="1d16a-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="1d16a-110">選択された**ルート**オブジェクトから、 **urlroutingmodule**オブジェクトは、**ルート**オブジェクトに関連付けられている**iroutehandler**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="1d16a-111">通常、MVC アプリケーションでは、これは**Mvcroutehandler**のインスタンスになります。</span><span class="sxs-lookup"><span data-stu-id="1d16a-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="1d16a-112">**Iroutehandler**インスタンスは、 **IHttpHandler**オブジェクトを作成し、それに**ihttpcontext**オブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="1d16a-113">既定では、MVC の**IHttpHandler**インスタンスは**MvcHandler**オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1d16a-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="1d16a-114">次に、 **MvcHandler**オブジェクトは、最終的に要求を処理するコントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="1d16a-115">ASP.NET MVC Web アプリケーションを IIS 7.0 で実行する場合、MVC プロジェクトにファイル名の拡張子は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="1d16a-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="1d16a-116">IIS 6.0 で実行する場合は、ファイル名の拡張子 .mvc を ASP.NET ISAPI DLL に関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d16a-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="1d16a-117">モジュールとハンドラーは、ASP.NET MVC フレームワークへのエントリポイントです。</span><span class="sxs-lookup"><span data-stu-id="1d16a-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="1d16a-118">これらは次のアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-118">They perform the following actions:</span></span>

- <span data-ttu-id="1d16a-119">MVC Web アプリケーションの適切なコントローラーを選択する。</span><span class="sxs-lookup"><span data-stu-id="1d16a-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="1d16a-120">特定のコントローラー インスタンスを取得する。</span><span class="sxs-lookup"><span data-stu-id="1d16a-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="1d16a-121">コントローラーの**Execute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="1d16a-122">MVC Web プロジェクトの実行段階を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="1d16a-123">アプリケーションへの最初の要求を受け取る</span><span class="sxs-lookup"><span data-stu-id="1d16a-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="1d16a-124">Global.asax ファイルで、 **route**オブジェクトが**routetable**オブジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="1d16a-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="1d16a-125">ルーティングを実行する</span><span class="sxs-lookup"><span data-stu-id="1d16a-125">Perform routing</span></span> 

    - <span data-ttu-id="1d16a-126">**Urlroutingmodule**モジュールは、 **routetable**コレクション内の最初に一致する**ルート**オブジェクトを使用して、 **routetable**オブジェクトを作成します。このオブジェクトは、このオブジェクトを使用して**RequestContext** (**ihttpcontext**) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="1d16a-127">MVC 要求ハンドラーを作成する</span><span class="sxs-lookup"><span data-stu-id="1d16a-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="1d16a-128">**Mvcroutehandler**オブジェクトは、 **MvcHandler**クラスのインスタンスを作成し、そのインスタンスを**RequestContext**インスタンスに渡します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="1d16a-129">コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="1d16a-129">Create controller</span></span> 

    - <span data-ttu-id="1d16a-130">**MvcHandler**オブジェクトは、 **RequestContext**インスタンスを使用して、コントローラーインスタンスを作成するための**IControllerFactory**オブジェクト (通常は**defaultcontroller ファクトリ**クラスのインスタンス) を識別します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="1d16a-131">コントローラーの実行- **MvcHandler**インスタンスは、コントローラーの**execute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="1d16a-132">アクションを呼び出す</span><span class="sxs-lookup"><span data-stu-id="1d16a-132">Invoke action</span></span> 

    - <span data-ttu-id="1d16a-133">ほとんどのコントローラーは、**コントローラー**の基本クラスを継承します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="1d16a-134">コントローラーの場合、コントローラーに関連付けられているコントローラーのコントローラークラスのアクションメソッドを決定**し、その**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1d16a-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="1d16a-135">結果を実行する</span><span class="sxs-lookup"><span data-stu-id="1d16a-135">Execute result</span></span> 

    - <span data-ttu-id="1d16a-136">一般的なアクションメソッドでは、ユーザー入力を受け取り、適切な応答データを準備してから、結果の型を返すことによって結果を実行できます。</span><span class="sxs-lookup"><span data-stu-id="1d16a-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="1d16a-137">実行できる組み込みの結果型には、 **viewresult** (ビューをレンダリングし、最も頻繁に使用される結果型)、 **RedirectToRouteResult**、 **redirectresult**、 **Contentresult**、 **jsonresult**、および**emptyresult**があります。</span><span class="sxs-lookup"><span data-stu-id="1d16a-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
