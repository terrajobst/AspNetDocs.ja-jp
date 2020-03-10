---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 | の属性ルーティングMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446998"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="3796a-102">ASP.NET Web API 2 での属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="3796a-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="3796a-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3796a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3796a-104">*ルーティング*とは、Web API が URI とアクションを照合する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="3796a-105">Web API 2 では、*属性ルーティング*と呼ばれる新しい種類のルーティングがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3796a-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="3796a-106">名前が示すように、属性ルーティングでは、属性を使用してルートを定義します。</span><span class="sxs-lookup"><span data-stu-id="3796a-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="3796a-107">属性ルーティングを使用すると、web API の Uri をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="3796a-108">たとえば、リソースの階層を記述する Uri を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="3796a-109">規則ベースのルーティングと呼ばれる以前のスタイルのルーティングは、まだ完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3796a-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="3796a-110">実際には、両方の手法を同じプロジェクトで組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="3796a-111">このトピックでは、属性ルーティングを有効にする方法と、属性ルーティングのさまざまなオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3796a-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="3796a-112">属性ルーティングを使用するエンドツーエンドのチュートリアルについては、「 [WEB API 2 で属性ルーティングを使用して REST API を作成](create-a-rest-api-with-attribute-routing.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3796a-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="3796a-113">Prerequisites</span></span>

<span data-ttu-id="3796a-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)Community、Professional、または Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="3796a-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="3796a-115">または、NuGet パッケージマネージャーを使用して、必要なパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3796a-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="3796a-116">Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="3796a-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="3796a-117">パッケージマネージャーコンソールウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="3796a-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="3796a-118">属性ルーティングの理由</span><span class="sxs-lookup"><span data-stu-id="3796a-118">Why Attribute Routing?</span></span>

<span data-ttu-id="3796a-119">Web API の最初のリリースでは、*規約ベース*のルーティングが使用されていました。</span><span class="sxs-lookup"><span data-stu-id="3796a-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="3796a-120">この種類のルーティングでは、基本的にパラメーター化された文字列である1つ以上のルートテンプレートを定義します。</span><span class="sxs-lookup"><span data-stu-id="3796a-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="3796a-121">フレームワークは、要求を受信すると、ルートテンプレートに対して URI と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="3796a-122">(規則ベースのルーティングの詳細については、「 [ASP.NET Web API でのルーティング](routing-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="3796a-123">規則ベースのルーティングの利点の1つは、テンプレートが1つの場所で定義され、ルーティング規則がすべてのコントローラーで一貫して適用されることです。</span><span class="sxs-lookup"><span data-stu-id="3796a-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="3796a-124">残念ながら、規約ベースのルーティングでは、RESTful Api に共通する特定の URI パターンをサポートすることが難しくなります。</span><span class="sxs-lookup"><span data-stu-id="3796a-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="3796a-125">たとえば、多くの場合、リソースには子リソースが含まれています。顧客の注文、映画、出演者などがあります。</span><span class="sxs-lookup"><span data-stu-id="3796a-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="3796a-126">これらの関係を反映する Uri を作成するのは自然なことです。</span><span class="sxs-lookup"><span data-stu-id="3796a-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="3796a-127">この種類の URI は、規約ベースのルーティングを使用して作成することは困難です。</span><span class="sxs-lookup"><span data-stu-id="3796a-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="3796a-128">これを行うことはできますが、多くのコントローラーまたはリソースの種類がある場合は、結果が適切にスケールされません。</span><span class="sxs-lookup"><span data-stu-id="3796a-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="3796a-129">属性ルーティングでは、この URI のルートを定義するのは簡単ではありません。</span><span class="sxs-lookup"><span data-stu-id="3796a-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="3796a-130">コントローラーアクションに属性を追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="3796a-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="3796a-131">ここでは、属性ルーティングが簡単になる他のパターンをいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="3796a-132">**API のバージョン管理**</span><span class="sxs-lookup"><span data-stu-id="3796a-132">**API versioning**</span></span>

<span data-ttu-id="3796a-133">この例では、"/api/v1/products" は "/api/v2/products" とは別のコントローラーにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="3796a-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="3796a-134">**オーバーロードされた URI セグメント**</span><span class="sxs-lookup"><span data-stu-id="3796a-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="3796a-135">この例では、"1" は注文番号ですが、"pending" はコレクションにマップされます。</span><span class="sxs-lookup"><span data-stu-id="3796a-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="3796a-136">**複数のパラメーターの型**</span><span class="sxs-lookup"><span data-stu-id="3796a-136">**Multiple parameter types**</span></span>

<span data-ttu-id="3796a-137">この例では、"1" は注文番号ですが、"2013/06/16" は日付を指定します。</span><span class="sxs-lookup"><span data-stu-id="3796a-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="3796a-138">属性ルーティングの有効化</span><span class="sxs-lookup"><span data-stu-id="3796a-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="3796a-139">属性ルーティングを有効にするには、構成中に**MapHttpAttributeRoutes**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3796a-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="3796a-140">この拡張メソッドは、System.web. **Http. HttpConfigurationExtensions**クラスで定義されています。</span><span class="sxs-lookup"><span data-stu-id="3796a-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="3796a-141">属性ルーティングは[、規則ベース](routing-in-aspnet-web-api.md)のルーティングと組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="3796a-142">規則ベースのルートを定義するには、 **MapHttpRoute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3796a-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="3796a-143">Web API の構成の詳細については、「 [ASP.NET Web API 2 の構成](../advanced/configuring-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="3796a-144">注: Web API からの移行1</span><span class="sxs-lookup"><span data-stu-id="3796a-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="3796a-145">Web API 2 より前の Web API プロジェクトでは、次のようなコードが生成されました。</span><span class="sxs-lookup"><span data-stu-id="3796a-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="3796a-146">属性ルーティングが有効になっている場合、このコードは例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="3796a-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="3796a-147">属性ルーティングを使用するように既存の Web API プロジェクトをアップグレードする場合は、この構成コードを次のように更新してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="3796a-148">詳細については、「 [ASP.NET ホスティングを使用した WEB API の構成](../advanced/configuring-aspnet-web-api.md#webhost)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="3796a-149">ルート属性の追加</span><span class="sxs-lookup"><span data-stu-id="3796a-149">Adding Route Attributes</span></span>

<span data-ttu-id="3796a-150">属性を使用して定義されたルートの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="3796a-151">文字列 &quot;customers/{customerId}/orders&quot; は、ルートの URI テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="3796a-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="3796a-152">Web API は、要求 URI とテンプレートを一致させようとします。</span><span class="sxs-lookup"><span data-stu-id="3796a-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="3796a-153">この例では、"customers" と "orders" はリテラルセグメントで、"{customerId}" は変数パラメーターです。</span><span class="sxs-lookup"><span data-stu-id="3796a-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="3796a-154">次の Uri は、このテンプレートに一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="3796a-155">このトピックの後半で説明する[制約](#constraints)を使用して、照合を制限できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="3796a-156">ルートテンプレートの &quot;{customerId}&quot; パラメーターが、メソッドの*customerId*パラメーターの名前と一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="3796a-157">Web API がコントローラーアクションを呼び出すと、ルートパラメーターのバインドが試行されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="3796a-158">たとえば、URI が `http://example.com/customers/1/orders`場合、Web API は、アクションの*customerId*パラメーターに値 "1" をバインドしようとします。</span><span class="sxs-lookup"><span data-stu-id="3796a-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="3796a-159">URI テンプレートには、いくつかのパラメーターを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="3796a-160">ルート属性を持たないコントローラーメソッドでは、規約ベースのルーティングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="3796a-161">これにより、両方の種類のルーティングを同じプロジェクトで組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3796a-162">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="3796a-162">HTTP Methods</span></span>

<span data-ttu-id="3796a-163">また、Web API は、要求の HTTP メソッド (GET、POST など) に基づいてアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="3796a-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="3796a-164">既定では、Web API は、コントローラーメソッド名の先頭と大文字と小文字を区別しない一致を検索します。</span><span class="sxs-lookup"><span data-stu-id="3796a-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="3796a-165">たとえば、`PutCustomers` という名前のコントローラーメソッドは、HTTP PUT 要求と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="3796a-166">次の属性を使用してメソッドを修飾することで、この規則をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="3796a-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="3796a-167">**HttpDelete**</span><span class="sxs-lookup"><span data-stu-id="3796a-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="3796a-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="3796a-168">**[HttpGet]**</span></span>
- <span data-ttu-id="3796a-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="3796a-169">**[HttpHead]**</span></span>
- <span data-ttu-id="3796a-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="3796a-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="3796a-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="3796a-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="3796a-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="3796a-172">**[HttpPost]**</span></span>
- <span data-ttu-id="3796a-173">**HttpPut**</span><span class="sxs-lookup"><span data-stu-id="3796a-173">**[HttpPut]**</span></span>

<span data-ttu-id="3796a-174">次の例では、CreateBook メソッドを HTTP POST 要求にマップします。</span><span class="sxs-lookup"><span data-stu-id="3796a-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="3796a-175">標準以外のメソッドを含め、他のすべての HTTP メソッドについては、 **Acceptverbs**属性を使用します。この属性は、http メソッドの一覧を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3796a-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="3796a-176">ルートプレフィックス</span><span class="sxs-lookup"><span data-stu-id="3796a-176">Route Prefixes</span></span>

<span data-ttu-id="3796a-177">多くの場合、コントローラー内のルートはすべて同じプレフィックスで開始されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="3796a-178">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="3796a-179">**[Routeprefix]** 属性を使用して、コントローラー全体に共通のプレフィックスを設定できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="3796a-180">Route プレフィックスをオーバーライドするには、メソッド属性にティルダ (~) を使用します。</span><span class="sxs-lookup"><span data-stu-id="3796a-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="3796a-181">ルートプレフィックスには、次のパラメーターを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="3796a-182">ルート制約</span><span class="sxs-lookup"><span data-stu-id="3796a-182">Route Constraints</span></span>

<span data-ttu-id="3796a-183">ルート制約を使用すると、ルートテンプレートのパラメーターの照合方法を制限できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="3796a-184">一般的な構文は &quot;{parameter: constraint}&quot;です。</span><span class="sxs-lookup"><span data-stu-id="3796a-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="3796a-185">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="3796a-186">ここでは、URI の &quot;id&quot; セグメントが整数である場合にのみ、最初のルートが選択されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="3796a-187">それ以外の場合は、2番目のルートが選択されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="3796a-188">次の表に、サポートされている制約の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="3796a-189">制約</span><span class="sxs-lookup"><span data-stu-id="3796a-189">Constraint</span></span> | <span data-ttu-id="3796a-190">Description</span><span class="sxs-lookup"><span data-stu-id="3796a-190">Description</span></span> | <span data-ttu-id="3796a-191">例</span><span class="sxs-lookup"><span data-stu-id="3796a-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3796a-192">アルファ</span><span class="sxs-lookup"><span data-stu-id="3796a-192">alpha</span></span> | <span data-ttu-id="3796a-193">大文字と小文字の英字 (a-z、a-z) を検索します。</span><span class="sxs-lookup"><span data-stu-id="3796a-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="3796a-194">{x:alpha}</span><span class="sxs-lookup"><span data-stu-id="3796a-194">{x:alpha}</span></span> |
| <span data-ttu-id="3796a-195">[bool]</span><span class="sxs-lookup"><span data-stu-id="3796a-195">bool</span></span> | <span data-ttu-id="3796a-196">ブール値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-196">Matches a Boolean value.</span></span> | <span data-ttu-id="3796a-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="3796a-197">{x:bool}</span></span> |
| <span data-ttu-id="3796a-198">DATETIME</span><span class="sxs-lookup"><span data-stu-id="3796a-198">datetime</span></span> | <span data-ttu-id="3796a-199">**DateTime**値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="3796a-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="3796a-200">{x:datetime}</span></span> |
| <span data-ttu-id="3796a-201">decimal</span><span class="sxs-lookup"><span data-stu-id="3796a-201">decimal</span></span> | <span data-ttu-id="3796a-202">10進値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-202">Matches a decimal value.</span></span> | <span data-ttu-id="3796a-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="3796a-203">{x:decimal}</span></span> |
| <span data-ttu-id="3796a-204">double</span><span class="sxs-lookup"><span data-stu-id="3796a-204">double</span></span> | <span data-ttu-id="3796a-205">64ビットの浮動小数点値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="3796a-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="3796a-206">{x:double}</span></span> |
| <span data-ttu-id="3796a-207">float</span><span class="sxs-lookup"><span data-stu-id="3796a-207">float</span></span> | <span data-ttu-id="3796a-208">32ビットの浮動小数点値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="3796a-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="3796a-209">{x:float}</span></span> |
| <span data-ttu-id="3796a-210">guid</span><span class="sxs-lookup"><span data-stu-id="3796a-210">guid</span></span> | <span data-ttu-id="3796a-211">GUID 値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-211">Matches a GUID value.</span></span> | <span data-ttu-id="3796a-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="3796a-212">{x:guid}</span></span> |
| <span data-ttu-id="3796a-213">INT</span><span class="sxs-lookup"><span data-stu-id="3796a-213">int</span></span> | <span data-ttu-id="3796a-214">32ビットの整数値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="3796a-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="3796a-215">{x:int}</span></span> |
| <span data-ttu-id="3796a-216">length</span><span class="sxs-lookup"><span data-stu-id="3796a-216">length</span></span> | <span data-ttu-id="3796a-217">指定された長さの文字列、または指定された長さの範囲内にある文字列と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="3796a-218">{x:length (6)}{x:length (1, 20)}</span><span class="sxs-lookup"><span data-stu-id="3796a-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="3796a-219">long</span><span class="sxs-lookup"><span data-stu-id="3796a-219">long</span></span> | <span data-ttu-id="3796a-220">64ビットの整数値と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="3796a-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="3796a-221">{x:long}</span></span> |
| <span data-ttu-id="3796a-222">max</span><span class="sxs-lookup"><span data-stu-id="3796a-222">max</span></span> | <span data-ttu-id="3796a-223">最大値を持つ整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="3796a-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="3796a-224">{x:max(10)}</span></span> |
| <span data-ttu-id="3796a-225">maxlength</span><span class="sxs-lookup"><span data-stu-id="3796a-225">maxlength</span></span> | <span data-ttu-id="3796a-226">最大長の文字列と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="3796a-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="3796a-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="3796a-228">min</span><span class="sxs-lookup"><span data-stu-id="3796a-228">min</span></span> | <span data-ttu-id="3796a-229">最小値を持つ整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="3796a-230">{x:min (10)}</span><span class="sxs-lookup"><span data-stu-id="3796a-230">{x:min(10)}</span></span> |
| <span data-ttu-id="3796a-231">minlength</span><span class="sxs-lookup"><span data-stu-id="3796a-231">minlength</span></span> | <span data-ttu-id="3796a-232">最小長の文字列と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="3796a-233">{x:minlength (10)}</span><span class="sxs-lookup"><span data-stu-id="3796a-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="3796a-234">range</span><span class="sxs-lookup"><span data-stu-id="3796a-234">range</span></span> | <span data-ttu-id="3796a-235">値の範囲内の整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="3796a-236">{x:range(10,50)}</span><span class="sxs-lookup"><span data-stu-id="3796a-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="3796a-237">regex</span><span class="sxs-lookup"><span data-stu-id="3796a-237">regex</span></span> | <span data-ttu-id="3796a-238">正規表現と一致します。</span><span class="sxs-lookup"><span data-stu-id="3796a-238">Matches a regular expression.</span></span> | <span data-ttu-id="3796a-239">{x:regex (^ \d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="3796a-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="3796a-240">&quot;min&quot;などの一部の制約は、かっこで囲まれた引数を受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="3796a-241">パラメーターには、コロンで区切られた複数の制約を適用できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="3796a-242">カスタム ルート制約</span><span class="sxs-lookup"><span data-stu-id="3796a-242">Custom Route Constraints</span></span>

<span data-ttu-id="3796a-243">**IHttpRouteConstraint**インターフェイスを実装することによって、カスタムルート制約を作成できます。</span><span class="sxs-lookup"><span data-stu-id="3796a-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="3796a-244">たとえば、次の制約では、パラメーターを0以外の整数値に制限しています。</span><span class="sxs-lookup"><span data-stu-id="3796a-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="3796a-245">次のコードは、制約を登録する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3796a-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="3796a-246">これで、ルートに制約を適用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3796a-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="3796a-247">また、 **Iinlineconstr/** resolver インターフェイスを実装することによって、 **defaulの**完全な使用方法を置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="3796a-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="3796a-248">これを行うと、 **Iinlineconstrの**実装で明示的に追加されていない限り、組み込みの制約がすべて置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="3796a-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="3796a-249">省略可能な URI パラメーターと既定値</span><span class="sxs-lookup"><span data-stu-id="3796a-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="3796a-250">ルートパラメーターに疑問符を追加することで、URI パラメーターをオプションにすることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="3796a-251">ルートパラメーターが省略可能な場合は、メソッドパラメーターの既定値を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3796a-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="3796a-252">この例では、`/api/books/locale/1033` と `/api/books/locale` は同じリソースを返します。</span><span class="sxs-lookup"><span data-stu-id="3796a-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="3796a-253">または、ルートテンプレート内の既定値を次のように指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="3796a-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="3796a-254">これは前の例とほぼ同じですが、既定値が適用された場合の動作に若干の違いがあります。</span><span class="sxs-lookup"><span data-stu-id="3796a-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="3796a-255">最初の例 ("{lcid: int?}") では、既定値の1033がメソッドのパラメーターに直接割り当てられているため、パラメーターにはこの正確な値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3796a-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="3796a-256">2番目の例 ("{lcid: int = 1033}") では、既定値の "1033" がモデルバインドプロセスを通過します。</span><span class="sxs-lookup"><span data-stu-id="3796a-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="3796a-257">既定のモデルバインダーは、"1033" を数値1033に変換します。</span><span class="sxs-lookup"><span data-stu-id="3796a-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="3796a-258">ただし、カスタムモデルバインダーをプラグインすることもできますが、これは別の方法で実行される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3796a-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="3796a-259">(ほとんどの場合、パイプラインにカスタムモデルバインダーがある場合を除き、2つの形式は同じです)。</span><span class="sxs-lookup"><span data-stu-id="3796a-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="3796a-260">ルート名</span><span class="sxs-lookup"><span data-stu-id="3796a-260">Route Names</span></span>

<span data-ttu-id="3796a-261">Web API では、すべてのルートに名前が付いています。</span><span class="sxs-lookup"><span data-stu-id="3796a-261">In Web API, every route has a name.</span></span> <span data-ttu-id="3796a-262">ルート名はリンクを生成するのに役立ちます。これにより、HTTP 応答にリンクを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="3796a-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="3796a-263">ルート名を指定するには、属性の**name**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="3796a-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="3796a-264">次の例は、ルート名を設定する方法と、リンクの生成時にルート名を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3796a-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="3796a-265">ルートの順序</span><span class="sxs-lookup"><span data-stu-id="3796a-265">Route Order</span></span>

<span data-ttu-id="3796a-266">フレームワークが URI とルートを一致させようとすると、ルートは特定の順序で評価されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="3796a-267">順序を指定するには、route 属性の**order**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="3796a-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="3796a-268">下限値が最初に評価されます。</span><span class="sxs-lookup"><span data-stu-id="3796a-268">Lower values are evaluated first.</span></span> <span data-ttu-id="3796a-269">既定の順序の値は0です。</span><span class="sxs-lookup"><span data-stu-id="3796a-269">The default order value is zero.</span></span>

<span data-ttu-id="3796a-270">合計の順序を決定する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="3796a-271">Route 属性の**Order**プロパティを比較します。</span><span class="sxs-lookup"><span data-stu-id="3796a-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="3796a-272">ルートテンプレート内の各 URI セグメントを確認します。</span><span class="sxs-lookup"><span data-stu-id="3796a-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="3796a-273">各セグメントについて、次の順序で並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="3796a-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="3796a-274">リテラルセグメント。</span><span class="sxs-lookup"><span data-stu-id="3796a-274">Literal segments.</span></span>
    2. <span data-ttu-id="3796a-275">制約付きのパラメーターをルーティングします。</span><span class="sxs-lookup"><span data-stu-id="3796a-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="3796a-276">制約のないルートパラメーター。</span><span class="sxs-lookup"><span data-stu-id="3796a-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="3796a-277">制約のあるワイルドカードパラメーターセグメント。</span><span class="sxs-lookup"><span data-stu-id="3796a-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="3796a-278">制約のないワイルドカードパラメーターセグメント。</span><span class="sxs-lookup"><span data-stu-id="3796a-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="3796a-279">同一の場合、ルートは、ルートテンプレートの大文字と小文字を区別しない序数の文字列比較 ([stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) によって並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="3796a-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="3796a-280">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3796a-280">Here is an example.</span></span> <span data-ttu-id="3796a-281">次のコントローラーを定義するとします。</span><span class="sxs-lookup"><span data-stu-id="3796a-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="3796a-282">これらのルートは次の順序で並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="3796a-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="3796a-283">注文/詳細</span><span class="sxs-lookup"><span data-stu-id="3796a-283">orders/details</span></span>
2. <span data-ttu-id="3796a-284">注文/{id}</span><span class="sxs-lookup"><span data-stu-id="3796a-284">orders/{id}</span></span>
3. <span data-ttu-id="3796a-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="3796a-285">orders/{customerName}</span></span>
4. <span data-ttu-id="3796a-286">orders/{\*date}</span><span class="sxs-lookup"><span data-stu-id="3796a-286">orders/{\*date}</span></span>
5. <span data-ttu-id="3796a-287">注文/保留中</span><span class="sxs-lookup"><span data-stu-id="3796a-287">orders/pending</span></span>

<span data-ttu-id="3796a-288">"Details" はリテラルセグメントであり、"{id}" の前に表示されますが、 **Order**プロパティが1であるため、"pending" が最後に表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3796a-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="3796a-289">(この例では、"詳細" または "保留中" という名前の顧客がいないことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="3796a-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="3796a-290">一般に、あいまいなルートは避けてください。</span><span class="sxs-lookup"><span data-stu-id="3796a-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="3796a-291">この例では、`GetByCustomer` のより優れたルートテンプレートは "customers/{様}" です)</span><span class="sxs-lookup"><span data-stu-id="3796a-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
