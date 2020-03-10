---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API でのルーティングとアクションの選択 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446914"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="2397e-102">ASP.NET Web API でのルーティングとアクションの選択</span><span class="sxs-lookup"><span data-stu-id="2397e-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="2397e-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2397e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2397e-104">この記事では、ASP.NET Web API して、コントローラー上の特定のアクションに HTTP 要求をルーティングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2397e-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="2397e-105">ルーティングの概要については、「 [ASP.NET Web API でのルーティング](routing-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2397e-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="2397e-106">この記事では、ルーティングプロセスの詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="2397e-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="2397e-107">Web API プロジェクトを作成し、一部の要求が意図したとおりにルーティングされないことを確認した場合、この記事は役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="2397e-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="2397e-108">ルーティングには、次の3つの主要なフェーズがあります。</span><span class="sxs-lookup"><span data-stu-id="2397e-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="2397e-109">URI をルートテンプレートと照合します。</span><span class="sxs-lookup"><span data-stu-id="2397e-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="2397e-110">コントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-110">Selecting a controller.</span></span>
3. <span data-ttu-id="2397e-111">アクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-111">Selecting an action.</span></span>

<span data-ttu-id="2397e-112">プロセスの一部の部分は、独自のカスタム動作に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="2397e-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="2397e-113">この記事では、既定の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="2397e-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="2397e-114">最後に、動作をカスタマイズできる場所に注意してください。</span><span class="sxs-lookup"><span data-stu-id="2397e-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="2397e-115">ルートテンプレート</span><span class="sxs-lookup"><span data-stu-id="2397e-115">Route Templates</span></span>

<span data-ttu-id="2397e-116">ルートテンプレートは、URI パスに似ていますが、プレースホルダー値を含むことができます (中かっこで囲まれています)。</span><span class="sxs-lookup"><span data-stu-id="2397e-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="2397e-117">ルートを作成するときに、一部またはすべてのプレースホルダーに既定値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="2397e-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="2397e-118">また、URI セグメントがプレースホルダーと一致する方法を制限する制約を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="2397e-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="2397e-119">フレームワークは、URI パスのセグメントとテンプレートを一致させようとします。</span><span class="sxs-lookup"><span data-stu-id="2397e-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="2397e-120">テンプレート内のリテラルは正確に一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="2397e-121">制約を指定しない限り、プレースホルダーは任意の値と一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="2397e-122">フレームワークは、ホスト名やクエリパラメーターなど、URI のその他の部分と一致しません。</span><span class="sxs-lookup"><span data-stu-id="2397e-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="2397e-123">フレームワークは、ルートテーブル内で URI に一致する最初のルートを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="2397e-124">"{Controller}" と "{action}" という2つの特殊なプレースホルダーがあります。</span><span class="sxs-lookup"><span data-stu-id="2397e-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="2397e-125">"{controller}" には、コントローラーの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="2397e-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="2397e-126">"{action}" は、アクションの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="2397e-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="2397e-127">Web API では、通常、"{action}" を省略しています。</span><span class="sxs-lookup"><span data-stu-id="2397e-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="2397e-128">デフォルト</span><span class="sxs-lookup"><span data-stu-id="2397e-128">Defaults</span></span>

<span data-ttu-id="2397e-129">既定値を指定した場合、ルートはそれらのセグメントが欠落している URI と一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="2397e-130">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2397e-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="2397e-131">Uri `http://localhost/api/products/all` と `http://localhost/api/products` は、前のルートと一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="2397e-132">後者の URI では、不足している `{category}` セグメントに既定値 `all`が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="2397e-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="2397e-133">ルートディクショナリ</span><span class="sxs-lookup"><span data-stu-id="2397e-133">Route Dictionary</span></span>

<span data-ttu-id="2397e-134">URI に一致するものが見つかった場合は、各プレースホルダーの値を含むディクショナリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="2397e-135">キーはプレースホルダー名であり、中かっこは含まれません。</span><span class="sxs-lookup"><span data-stu-id="2397e-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="2397e-136">値は、URI パスまたは既定値から取得されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="2397e-137">ディクショナリは、 **IHttpRouteData**オブジェクトに格納されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="2397e-138">このルート照合フェーズでは、特別な "{controller}" プレースホルダーと "{action}" プレースホルダーが、他のプレースホルダーと同じように扱われます。</span><span class="sxs-lookup"><span data-stu-id="2397e-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="2397e-139">これらは、他の値と共にディクショナリに格納されるだけです。</span><span class="sxs-lookup"><span data-stu-id="2397e-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="2397e-140">既定値は、特別な値 Routeparameter を持つことができ**ます。省略可能**。</span><span class="sxs-lookup"><span data-stu-id="2397e-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="2397e-141">プレースホルダーにこの値が割り当てられている場合、その値はルートディクショナリに追加されません。</span><span class="sxs-lookup"><span data-stu-id="2397e-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="2397e-142">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2397e-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="2397e-143">URI パス "api/製品" の場合、ルートディクショナリには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2397e-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="2397e-144">コントローラー: "製品"</span><span class="sxs-lookup"><span data-stu-id="2397e-144">controller: "products"</span></span>
- <span data-ttu-id="2397e-145">カテゴリ: "all"</span><span class="sxs-lookup"><span data-stu-id="2397e-145">category: "all"</span></span>

<span data-ttu-id="2397e-146">ただし、"api/products/toys/123" の場合、ルートディクショナリには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2397e-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="2397e-147">コントローラー: "製品"</span><span class="sxs-lookup"><span data-stu-id="2397e-147">controller: "products"</span></span>
- <span data-ttu-id="2397e-148">category: "toys"</span><span class="sxs-lookup"><span data-stu-id="2397e-148">category: "toys"</span></span>
- <span data-ttu-id="2397e-149">id: "123"</span><span class="sxs-lookup"><span data-stu-id="2397e-149">id: "123"</span></span>

<span data-ttu-id="2397e-150">既定値には、ルートテンプレートのどこにも表示されない値を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="2397e-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="2397e-151">ルートがと一致する場合、その値はディクショナリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="2397e-152">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2397e-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="2397e-153">URI パスが "api/root/8" の場合、ディクショナリには次の2つの値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2397e-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="2397e-154">コントローラー: "customers"</span><span class="sxs-lookup"><span data-stu-id="2397e-154">controller: "customers"</span></span>
- <span data-ttu-id="2397e-155">id: "8"</span><span class="sxs-lookup"><span data-stu-id="2397e-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="2397e-156">コントローラーの選択</span><span class="sxs-lookup"><span data-stu-id="2397e-156">Selecting a Controller</span></span>

<span data-ttu-id="2397e-157">コントローラーの選択は、 **IHttpControllerSelector**メソッドによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="2397e-158">このメソッドは、 **HttpRequestMessage**インスタンスを受け取り、 **httpコントローラー記述子**を返します。</span><span class="sxs-lookup"><span data-stu-id="2397e-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="2397e-159">既定の実装は、 **DefaultHttpControllerSelector**クラスによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="2397e-160">このクラスは、単純なアルゴリズムを使用します。</span><span class="sxs-lookup"><span data-stu-id="2397e-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="2397e-161">ルートディクショナリでキー "controller" を探します。</span><span class="sxs-lookup"><span data-stu-id="2397e-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="2397e-162">このキーの値を取得し、"Controller" という文字列を追加して、コントローラーの種類の名前を取得します。</span><span class="sxs-lookup"><span data-stu-id="2397e-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="2397e-163">この型名の Web API コントローラーを探します。</span><span class="sxs-lookup"><span data-stu-id="2397e-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="2397e-164">たとえば、ルートディクショナリにキーと値のペア "controller" = "products" が含まれている場合、コントローラーの種類は "製品コントローラー" です。</span><span class="sxs-lookup"><span data-stu-id="2397e-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="2397e-165">一致する型がない場合、または複数の一致がある場合、フレームワークはクライアントにエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="2397e-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="2397e-166">手順3では、 **DefaultHttpControllerSelector**は**IHttpControllerTypeResolver**インターフェイスを使用して、Web API コントローラーの種類の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="2397e-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="2397e-167">**IHttpControllerTypeResolver**の既定の実装は、(a) が**IHttpController**を実装するすべてのパブリッククラスを返します。 (b) は abstract ではなく、(c) は "Controller" で終わる名前を持ちます。</span><span class="sxs-lookup"><span data-stu-id="2397e-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="2397e-168">アクションの選択</span><span class="sxs-lookup"><span data-stu-id="2397e-168">Action Selection</span></span>

<span data-ttu-id="2397e-169">コントローラーを選択した後、フレームワークは**Ihttpactionselector. selectaction**メソッドを呼び出してアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="2397e-170">このメソッドは**Httpコントローラーコンテキスト**を取得し、 **Httpactiondescriptor**を返します。</span><span class="sxs-lookup"><span data-stu-id="2397e-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="2397e-171">既定の実装は、 **ApiControllerActionSelector**クラスによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="2397e-172">アクションを選択するには、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="2397e-173">要求の HTTP メソッド。</span><span class="sxs-lookup"><span data-stu-id="2397e-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="2397e-174">ルートテンプレート内の "{action}" プレースホルダー (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="2397e-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="2397e-175">コントローラー上のアクションのパラメーター。</span><span class="sxs-lookup"><span data-stu-id="2397e-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="2397e-176">選択アルゴリズムを確認する前に、コントローラーアクションに関するいくつかの点を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="2397e-177">**コントローラーのどのメソッドが "アクション" と見なされますか。**</span><span class="sxs-lookup"><span data-stu-id="2397e-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="2397e-178">アクションを選択すると、フレームワークはコントローラーのパブリックインスタンスメソッドのみを参照します。</span><span class="sxs-lookup"><span data-stu-id="2397e-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="2397e-179">また、 ["特別な名前"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)メソッド (コンストラクター、イベント、演算子のオーバーロードなど)、および**ApiController**クラスから継承されたメソッドは除外されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="2397e-180">**HTTP メソッド。**</span><span class="sxs-lookup"><span data-stu-id="2397e-180">**HTTP Methods.**</span></span> <span data-ttu-id="2397e-181">フレームワークは、次のように決定された要求の HTTP メソッドに一致するアクションのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="2397e-182">HTTP メソッドには、 **Acceptverbs**、 **httpdelete**、 **HttpGet**、 **httpdelete**、 **HttpOptions**、 **httpdelete**、 **httpdelete**、または**httpdelete**の属性を指定できます。</span><span class="sxs-lookup"><span data-stu-id="2397e-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="2397e-183">それ以外の場合、コントローラーメソッドの名前が "Get"、"Post"、"Put"、"Delete"、"Head"、"Options"、または "Patch" で始まる場合、規則によって、アクションはその HTTP メソッドをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2397e-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="2397e-184">上記のいずれも当てはまらない場合、メソッドは POST をサポートします。</span><span class="sxs-lookup"><span data-stu-id="2397e-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="2397e-185">**パラメーターのバインド。**</span><span class="sxs-lookup"><span data-stu-id="2397e-185">**Parameter Bindings.**</span></span> <span data-ttu-id="2397e-186">パラメーターのバインドとは、Web API がパラメーターの値を作成する方法です。</span><span class="sxs-lookup"><span data-stu-id="2397e-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="2397e-187">パラメーターバインドの既定の規則を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2397e-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="2397e-188">単純型は URI から取得されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="2397e-189">複合型は、要求本文から取得されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="2397e-190">単純型には、すべての[.NET Framework プリミティブ型](https://msdn.microsoft.com/library/system.type.isprimitive)に加え、 **DateTime**、 **Decimal**、 **Guid**、 **String**、および**TimeSpan**が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2397e-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="2397e-191">アクションごとに、最大で1つのパラメーターで要求本文を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="2397e-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="2397e-192">既定のバインディング規則をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="2397e-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="2397e-193">詳細[については、「WebAPI Parameter binding」を](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="2397e-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="2397e-194">この背景を使用すると、アクションの選択アルゴリズムが次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2397e-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="2397e-195">HTTP 要求メソッドに一致するコントローラー上のすべてのアクションの一覧を作成します。</span><span class="sxs-lookup"><span data-stu-id="2397e-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="2397e-196">ルートディクショナリに "action" エントリがある場合は、名前がこの値と一致しないアクションを削除します。</span><span class="sxs-lookup"><span data-stu-id="2397e-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="2397e-197">次のように、アクションパラメーターを URI と照合します。</span><span class="sxs-lookup"><span data-stu-id="2397e-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="2397e-198">アクションごとに、単純型のパラメーターのリストを取得します。ここで、バインドは URI からパラメーターを取得します。</span><span class="sxs-lookup"><span data-stu-id="2397e-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="2397e-199">省略可能なパラメーターを除外します。</span><span class="sxs-lookup"><span data-stu-id="2397e-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="2397e-200">この一覧から、ルートディクショナリまたは URI クエリ文字列のいずれかで、各パラメーター名に一致するものを検索します。</span><span class="sxs-lookup"><span data-stu-id="2397e-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="2397e-201">一致では大文字と小文字が区別されず、パラメーターの順序に依存しません。</span><span class="sxs-lookup"><span data-stu-id="2397e-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="2397e-202">リスト内のすべてのパラメーターが URI で一致するアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="2397e-203">1つのアクションがこれらの条件を満たしている場合は、最も多くのパラメーターが一致するものを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="2397e-204">**[非アクション]** 属性を持つアクションは無視します。</span><span class="sxs-lookup"><span data-stu-id="2397e-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="2397e-205">手順 #3 は、おそらく最もわかりにくいものです。</span><span class="sxs-lookup"><span data-stu-id="2397e-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="2397e-206">基本的な考え方は、パラメーターが URI、要求本文、またはカスタムバインディングから値を取得できることです。</span><span class="sxs-lookup"><span data-stu-id="2397e-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="2397e-207">URI からのパラメーターの場合、URI に実際にそのパラメーターの値が含まれていることを確認する必要があります (ルートディクショナリ経由のパスまたはクエリ文字列内)。</span><span class="sxs-lookup"><span data-stu-id="2397e-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="2397e-208">たとえば、次のようなアクションを考えてみます。</span><span class="sxs-lookup"><span data-stu-id="2397e-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="2397e-209">*Id*パラメーターは URI にバインドされます。</span><span class="sxs-lookup"><span data-stu-id="2397e-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="2397e-210">このため、このアクションは、ルートディクショナリまたはクエリ文字列に "id" の値を含む URI にのみ一致できます。</span><span class="sxs-lookup"><span data-stu-id="2397e-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="2397e-211">省略可能なパラメーターは省略可能であるため、例外です。</span><span class="sxs-lookup"><span data-stu-id="2397e-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="2397e-212">省略可能なパラメーターの場合、バインドが URI から値を取得できない場合は問題ありません。</span><span class="sxs-lookup"><span data-stu-id="2397e-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="2397e-213">複合型は、さまざまな理由で例外となります。</span><span class="sxs-lookup"><span data-stu-id="2397e-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="2397e-214">複合型は、カスタムバインドを介して URI にのみバインドできます。</span><span class="sxs-lookup"><span data-stu-id="2397e-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="2397e-215">ただし、この場合、パラメーターが特定の URI にバインドされるかどうかを事前に確認することはできません。</span><span class="sxs-lookup"><span data-stu-id="2397e-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="2397e-216">これを確認するには、バインディングを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="2397e-217">選択アルゴリズムの目的は、バインドを呼び出す前に、静的な説明からアクションを選択することです。</span><span class="sxs-lookup"><span data-stu-id="2397e-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="2397e-218">したがって、複合型は照合アルゴリズムから除外されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="2397e-219">アクションを選択すると、すべてのパラメーターバインドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="2397e-220">概要:</span><span class="sxs-lookup"><span data-stu-id="2397e-220">Summary:</span></span>

- <span data-ttu-id="2397e-221">アクションは、要求の HTTP メソッドと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="2397e-222">アクション名がルートディクショナリの "action" エントリと一致している必要があります (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="2397e-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="2397e-223">アクションのすべてのパラメーターについて、パラメーターが URI から取得されている場合は、ルートディクショナリまたは URI クエリ文字列でパラメーター名を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="2397e-224">(省略可能なパラメーターと複合型のパラメーターは除外されます)。</span><span class="sxs-lookup"><span data-stu-id="2397e-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="2397e-225">最も多くのパラメーターを一致させてください。</span><span class="sxs-lookup"><span data-stu-id="2397e-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="2397e-226">最適な一致は、パラメーターのないメソッドである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2397e-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="2397e-227">拡張の例</span><span class="sxs-lookup"><span data-stu-id="2397e-227">Extended Example</span></span>

<span data-ttu-id="2397e-228">送る</span><span class="sxs-lookup"><span data-stu-id="2397e-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="2397e-229">コントローラー:</span><span class="sxs-lookup"><span data-stu-id="2397e-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="2397e-230">HTTP 要求:</span><span class="sxs-lookup"><span data-stu-id="2397e-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="2397e-231">ルート一致</span><span class="sxs-lookup"><span data-stu-id="2397e-231">Route Matching</span></span>

<span data-ttu-id="2397e-232">URI は "DefaultApi" という名前のルートと一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="2397e-233">ルートディクショナリには、次のエントリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2397e-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="2397e-234">コントローラー: "製品"</span><span class="sxs-lookup"><span data-stu-id="2397e-234">controller: "products"</span></span>
- <span data-ttu-id="2397e-235">id: "1"</span><span class="sxs-lookup"><span data-stu-id="2397e-235">id: "1"</span></span>

<span data-ttu-id="2397e-236">ルートディクショナリには、クエリ文字列パラメーター "version" と "details" は含まれませんが、アクションの選択時には引き続き考慮されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="2397e-237">コントローラーの選択</span><span class="sxs-lookup"><span data-stu-id="2397e-237">Controller Selection</span></span>

<span data-ttu-id="2397e-238">ルートディクショナリの "controller" エントリから、コントローラーの種類は `ProductsController`になります。</span><span class="sxs-lookup"><span data-stu-id="2397e-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="2397e-239">アクションの選択</span><span class="sxs-lookup"><span data-stu-id="2397e-239">Action Selection</span></span>

<span data-ttu-id="2397e-240">HTTP 要求は GET 要求です。</span><span class="sxs-lookup"><span data-stu-id="2397e-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="2397e-241">GET をサポートするコントローラーアクションは、`GetAll`、`GetById`、および `FindProductsByName`です。</span><span class="sxs-lookup"><span data-stu-id="2397e-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="2397e-242">ルートディクショナリに "action" のエントリが含まれていないため、アクション名と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="2397e-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="2397e-243">次に、アクションのパラメーター名を照合して、GET アクションだけを検索します。</span><span class="sxs-lookup"><span data-stu-id="2397e-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="2397e-244">アクション</span><span class="sxs-lookup"><span data-stu-id="2397e-244">Action</span></span> | <span data-ttu-id="2397e-245">一致するパラメーター</span><span class="sxs-lookup"><span data-stu-id="2397e-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="2397e-246">なし</span><span class="sxs-lookup"><span data-stu-id="2397e-246">none</span></span> |
| `GetById` | <span data-ttu-id="2397e-247">"ID"</span><span class="sxs-lookup"><span data-stu-id="2397e-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="2397e-248">指定</span><span class="sxs-lookup"><span data-stu-id="2397e-248">"name"</span></span> |

<span data-ttu-id="2397e-249">`GetById` の*バージョン*パラメーターは、省略可能なパラメーターであるため、考慮されません。</span><span class="sxs-lookup"><span data-stu-id="2397e-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="2397e-250">`GetAll` メソッドは普通に一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="2397e-251">ルートディクショナリに "id" が含まれているため、`GetById` メソッドも一致します。</span><span class="sxs-lookup"><span data-stu-id="2397e-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="2397e-252">`FindProductsByName` メソッドが一致しません。</span><span class="sxs-lookup"><span data-stu-id="2397e-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="2397e-253">`GetById` メソッドは、1つのパラメーターに一致するので、`GetAll`のパラメーターとは一致しないため、優先されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="2397e-254">次のパラメーター値を使用してメソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2397e-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="2397e-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="2397e-255">*id* = 1</span></span>
- <span data-ttu-id="2397e-256">*バージョン*= 1.5</span><span class="sxs-lookup"><span data-stu-id="2397e-256">*version* = 1.5</span></span>

<span data-ttu-id="2397e-257">選択アルゴリズムで*バージョン*が使用されていなくても、パラメーターの値は URI クエリ文字列から取得されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2397e-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="2397e-258">拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="2397e-258">Extension Points</span></span>

<span data-ttu-id="2397e-259">Web API には、ルーティングプロセスの一部の拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2397e-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="2397e-260">インターフェイス</span><span class="sxs-lookup"><span data-stu-id="2397e-260">Interface</span></span> | <span data-ttu-id="2397e-261">Description</span><span class="sxs-lookup"><span data-stu-id="2397e-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2397e-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="2397e-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="2397e-263">コントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-263">Selects the controller.</span></span> |
| <span data-ttu-id="2397e-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="2397e-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="2397e-265">コントローラーの種類の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="2397e-265">Gets the list of controller types.</span></span> <span data-ttu-id="2397e-266">**DefaultHttpControllerSelector**は、この一覧からコントローラーの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="2397e-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="2397e-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="2397e-268">プロジェクトアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="2397e-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="2397e-269">**IHttpControllerTypeResolver**インターフェイスは、このリストを使用してコントローラーの種類を検索します。</span><span class="sxs-lookup"><span data-stu-id="2397e-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="2397e-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="2397e-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="2397e-271">新しいコントローラーインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="2397e-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="2397e-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="2397e-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="2397e-273">アクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2397e-273">Selects the action.</span></span> |
| <span data-ttu-id="2397e-274">**IHttpActionInvoker 元**</span><span class="sxs-lookup"><span data-stu-id="2397e-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="2397e-275">アクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2397e-275">Invokes the action.</span></span> |

<span data-ttu-id="2397e-276">これらのインターフェイスのいずれかに独自の実装を提供するには、 **Httpconfiguration**オブジェクトの**Services**コレクションを使用します。</span><span class="sxs-lookup"><span data-stu-id="2397e-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
