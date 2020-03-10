---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API | でのルーティングMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449248"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="da0d4-102">ASP.NET Web API でのルーティング</span><span class="sxs-lookup"><span data-stu-id="da0d4-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="da0d4-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="da0d4-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="da0d4-104">この記事では、ASP.NET Web API が HTTP 要求をコントローラーにルーティングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="da0d4-105">ASP.NET MVC を使い慣れている場合、Web API ルーティングは MVC ルーティングとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="da0d4-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="da0d4-106">主な違いは、Web API は URI パスではなく HTTP 動詞を使用してアクションを選択することです。</span><span class="sxs-lookup"><span data-stu-id="da0d4-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="da0d4-107">Web API で MVC スタイルのルーティングを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="da0d4-108">この記事では、ASP.NET MVC に関する知識を前提としていません。</span><span class="sxs-lookup"><span data-stu-id="da0d4-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="da0d4-109">ルーティングテーブル</span><span class="sxs-lookup"><span data-stu-id="da0d4-109">Routing Tables</span></span>

<span data-ttu-id="da0d4-110">ASP.NET Web API では、*コントローラー*は HTTP 要求を処理するクラスです。</span><span class="sxs-lookup"><span data-stu-id="da0d4-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="da0d4-111">コントローラーのパブリックメソッドは、*アクションメソッド*または単なる*アクション*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="da0d4-112">Web API フレームワークは、要求を受信すると、要求をアクションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="da0d4-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="da0d4-113">呼び出すアクションを決定するために、フレームワークは*ルーティングテーブル*を使用します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="da0d4-114">Web API 用の Visual Studio プロジェクトテンプレートでは、既定のルートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="da0d4-115">このルートは*WebApiConfig.cs*ファイルで定義されています。このファイルは、*アプリ\_の開始*ディレクトリに配置されます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="da0d4-116">`WebApiConfig` クラスの詳細については、「 [ASP.NET Web API の構成](../advanced/configuring-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da0d4-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="da0d4-117">Web API を自己ホストする場合は、`HttpSelfHostConfiguration` オブジェクトでルーティングテーブルを直接設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da0d4-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="da0d4-118">詳細については、「 [WEB API をセルフホストする](../older-versions/self-host-a-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da0d4-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="da0d4-119">ルーティングテーブルの各エントリには、*ルートテンプレート*が含まれています。</span><span class="sxs-lookup"><span data-stu-id="da0d4-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="da0d4-120">Web API の既定のルートテンプレートは &quot;api/{controller}/{id}&quot;です。</span><span class="sxs-lookup"><span data-stu-id="da0d4-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="da0d4-121">このテンプレートでは、&quot;api&quot; はリテラルパスセグメントで、{controller} と {id} はプレースホルダー変数です。</span><span class="sxs-lookup"><span data-stu-id="da0d4-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="da0d4-122">Web API フレームワークは HTTP 要求を受信すると、URI とルーティングテーブル内のいずれかのルートテンプレートとの照合を試みます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="da0d4-123">一致するルートがない場合、クライアントは404エラーを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="da0d4-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="da0d4-124">たとえば、次の Uri は既定のルートと一致します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="da0d4-125">/api/contacts</span><span class="sxs-lookup"><span data-stu-id="da0d4-125">/api/contacts</span></span>
- <span data-ttu-id="da0d4-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="da0d4-126">/api/contacts/1</span></span>
- <span data-ttu-id="da0d4-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="da0d4-127">/api/products/gizmo1</span></span>

<span data-ttu-id="da0d4-128">ただし、次の URI は一致しません。これは、&quot;api&quot; セグメントがないためです。</span><span class="sxs-lookup"><span data-stu-id="da0d4-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="da0d4-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="da0d4-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="da0d4-130">ルートで "api" を使用する理由は、ASP.NET MVC ルーティングとの競合を避けるためです。</span><span class="sxs-lookup"><span data-stu-id="da0d4-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="da0d4-131">このようにして、&quot;/連絡先&quot; MVC コントローラーにアクセスできます。また、Web API コントローラーにアクセス&quot; に &quot;/連絡先を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="da0d4-132">もちろん、この規則に満足できない場合は、既定のルートテーブルを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="da0d4-133">一致するルートが見つかると、Web API はコントローラーとアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="da0d4-134">コントローラーを検索するために、Web API は &quot;コントローラーの&quot; を *{controller}* 変数の値に追加します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="da0d4-135">アクションを検索するために、Web API は HTTP 動詞を参照し、その HTTP 動詞名で始まる名前を持つアクションを検索します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="da0d4-136">たとえば、GET 要求では、Web API は &quot;GetContact&quot; や &quot;GetAllContacts&quot;などの &quot;Get&quot;で始まるアクションを検索します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="da0d4-137">この規則は、GET、POST、PUT、DELETE、HEAD、OPTIONS、PATCH 動詞にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="da0d4-138">他の HTTP 動詞は、コントローラーの属性を使用して有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="da0d4-139">その例については後で説明します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="da0d4-140">*{Id}* など、ルートテンプレート内のその他のプレースホルダー変数は、アクションパラメーターにマップされます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="da0d4-141">1 つ例を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="da0d4-141">Let's look at an example.</span></span> <span data-ttu-id="da0d4-142">次のコントローラーを定義するとします。</span><span class="sxs-lookup"><span data-stu-id="da0d4-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="da0d4-143">次に、使用可能な HTTP 要求と、それぞれに対して呼び出されるアクションを示します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="da0d4-144">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="da0d4-144">HTTP Verb</span></span> | <span data-ttu-id="da0d4-145">URI パス</span><span class="sxs-lookup"><span data-stu-id="da0d4-145">URI Path</span></span> | <span data-ttu-id="da0d4-146">アクション</span><span class="sxs-lookup"><span data-stu-id="da0d4-146">Action</span></span> | <span data-ttu-id="da0d4-147">パラメーター</span><span class="sxs-lookup"><span data-stu-id="da0d4-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da0d4-148">GET</span><span class="sxs-lookup"><span data-stu-id="da0d4-148">GET</span></span> | <span data-ttu-id="da0d4-149">api/製品</span><span class="sxs-lookup"><span data-stu-id="da0d4-149">api/products</span></span> | <span data-ttu-id="da0d4-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="da0d4-150">GetAllProducts</span></span> | <span data-ttu-id="da0d4-151">*存在*</span><span class="sxs-lookup"><span data-stu-id="da0d4-151">*(none)*</span></span> |
| <span data-ttu-id="da0d4-152">GET</span><span class="sxs-lookup"><span data-stu-id="da0d4-152">GET</span></span> | <span data-ttu-id="da0d4-153">api/製品/4</span><span class="sxs-lookup"><span data-stu-id="da0d4-153">api/products/4</span></span> | <span data-ttu-id="da0d4-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="da0d4-154">GetProductById</span></span> | <span data-ttu-id="da0d4-155">4</span><span class="sxs-lookup"><span data-stu-id="da0d4-155">4</span></span> |
| <span data-ttu-id="da0d4-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="da0d4-156">DELETE</span></span> | <span data-ttu-id="da0d4-157">api/製品/4</span><span class="sxs-lookup"><span data-stu-id="da0d4-157">api/products/4</span></span> | <span data-ttu-id="da0d4-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="da0d4-158">DeleteProduct</span></span> | <span data-ttu-id="da0d4-159">4</span><span class="sxs-lookup"><span data-stu-id="da0d4-159">4</span></span> |
| <span data-ttu-id="da0d4-160">POST</span><span class="sxs-lookup"><span data-stu-id="da0d4-160">POST</span></span> | <span data-ttu-id="da0d4-161">api/製品</span><span class="sxs-lookup"><span data-stu-id="da0d4-161">api/products</span></span> | <span data-ttu-id="da0d4-162">*(一致なし)*</span><span class="sxs-lookup"><span data-stu-id="da0d4-162">*(no match)*</span></span> |  |

<span data-ttu-id="da0d4-163">URI の *{id}* セグメント (存在する場合) がアクションの*id*パラメーターにマップされていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="da0d4-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="da0d4-164">この例では、コントローラーは2つの GET メソッドを定義します。1つは*id*パラメーターを持ち、もう1つはパラメーターを指定しません。</span><span class="sxs-lookup"><span data-stu-id="da0d4-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="da0d4-165">また、コントローラーでは &quot;Post...&quot; メソッドが定義されていないため、POST 要求は失敗します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="da0d4-166">ルーティングのバリエーション</span><span class="sxs-lookup"><span data-stu-id="da0d4-166">Routing Variations</span></span>

<span data-ttu-id="da0d4-167">前のセクションでは、ASP.NET Web API の基本的なルーティングメカニズムについて説明しています。</span><span class="sxs-lookup"><span data-stu-id="da0d4-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="da0d4-168">ここでは、いくつかのバリエーションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="da0d4-169">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="da0d4-169">HTTP verbs</span></span>

<span data-ttu-id="da0d4-170">HTTP 動詞の名前付け規則を使用する代わりに、次のいずれかの属性を使用してアクションメソッドを装飾することで、アクションの HTTP 動詞を明示的に指定できます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="da0d4-171">次の例では、`FindProduct` メソッドが GET 要求にマップされます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="da0d4-172">アクションに対して複数の HTTP 動詞を許可したり、GET、PUT、POST、DELETE、HEAD、OPTIONS、PATCH 以外の HTTP 動詞を許可したりするには、`[AcceptVerbs]` 属性を使用します。この属性は、HTTP 動詞の一覧を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="da0d4-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="da0d4-173">アクション名によるルーティング</span><span class="sxs-lookup"><span data-stu-id="da0d4-173">Routing by Action Name</span></span>

<span data-ttu-id="da0d4-174">既定のルーティングテンプレートでは、Web API は HTTP 動詞を使用してアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="da0d4-175">ただし、URI にアクション名が含まれているルートを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="da0d4-176">このルートテンプレートでは、 *{action}* パラメーターはコントローラーのアクションメソッドに名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="da0d4-177">このスタイルのルーティングでは、属性を使用して、許可される HTTP 動詞を指定します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="da0d4-178">たとえば、コントローラーに次のメソッドがあるとします。</span><span class="sxs-lookup"><span data-stu-id="da0d4-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="da0d4-179">この場合、"api/products/details/1" の GET 要求が `Details` メソッドにマップされます。</span><span class="sxs-lookup"><span data-stu-id="da0d4-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="da0d4-180">このスタイルのルーティングは ASP.NET MVC に似ており、RPC スタイルの API に適している場合があります。</span><span class="sxs-lookup"><span data-stu-id="da0d4-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="da0d4-181">アクション名をオーバーライドするには、`[ActionName]` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="da0d4-182">次の例では、&quot;api/製品/サムネイル/*id*にマップされる2つのアクションがあります。GET をサポートし、もう1つは POST をサポートします。</span><span class="sxs-lookup"><span data-stu-id="da0d4-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="da0d4-183">非アクション</span><span class="sxs-lookup"><span data-stu-id="da0d4-183">Non-Actions</span></span>

<span data-ttu-id="da0d4-184">メソッドがアクションとして呼び出されないようにするには、`[NonAction]` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="da0d4-185">これは、メソッドがルーティング規則と一致する場合でも、メソッドがアクションではないことをフレームワークに通知します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="da0d4-186">参考資料</span><span class="sxs-lookup"><span data-stu-id="da0d4-186">Further Reading</span></span>

<span data-ttu-id="da0d4-187">このトピックでは、ルーティングの概要について説明しました。</span><span class="sxs-lookup"><span data-stu-id="da0d4-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="da0d4-188">詳細については、「[ルーティングとアクションの選択](routing-and-action-selection.md)」を参照してください。これは、フレームワークがルートと URI を照合する方法を正確に説明し、コントローラーを選択して、呼び出すアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="da0d4-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
