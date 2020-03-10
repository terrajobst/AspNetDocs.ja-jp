---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: ASP.NET Web API 2.2 | を使用した OData v4 のエンティティの関係Microsoft Docs
author: MikeWasson
description: ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 クライアントは、OData を使用して移動できます...
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484462"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="3ac33-104">ASP.NET Web API 2.2 を使用した OData v4 のエンティティの関係</span><span class="sxs-lookup"><span data-stu-id="3ac33-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="3ac33-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3ac33-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="3ac33-106">ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。</span><span class="sxs-lookup"><span data-stu-id="3ac33-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="3ac33-107">OData を使用すると、クライアントはエンティティの関係を移動できます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="3ac33-108">製品を指定すると、業者を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="3ac33-109">リレーションシップを作成または削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-109">You can also create or remove relationships.</span></span> <span data-ttu-id="3ac33-110">たとえば、製品の仕入先を設定できます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="3ac33-111">このチュートリアルでは、ASP.NET Web API を使用して OData v4 でこれらの操作をサポートする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="3ac33-112">このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。</span><span class="sxs-lookup"><span data-stu-id="3ac33-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3ac33-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="3ac33-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="3ac33-114">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="3ac33-114">Web API 2.1</span></span>
> - <span data-ttu-id="3ac33-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="3ac33-115">OData v4</span></span>
> - <span data-ttu-id="3ac33-116">Visual Studio 2013 (こちらから Visual Studio 2017 をダウンロードして[ください](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="3ac33-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="3ac33-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="3ac33-117">Entity Framework 6</span></span>
> - <span data-ttu-id="3ac33-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3ac33-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="3ac33-119">チュートリアルのバージョン</span><span class="sxs-lookup"><span data-stu-id="3ac33-119">Tutorial versions</span></span>
>
> <span data-ttu-id="3ac33-120">OData バージョン3については、「 [odata v3 でのエンティティリレーションのサポート](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3ac33-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="3ac33-121">Supplier エンティティを追加する</span><span class="sxs-lookup"><span data-stu-id="3ac33-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="3ac33-122">このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。</span><span class="sxs-lookup"><span data-stu-id="3ac33-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="3ac33-123">まず、関連エンティティが必要です。</span><span class="sxs-lookup"><span data-stu-id="3ac33-123">First, we need a related entity.</span></span> <span data-ttu-id="3ac33-124">`Supplier` という名前のクラスを [モデル] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="3ac33-125">`Product` クラスにナビゲーションプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="3ac33-126">新しい**Dbset**を `ProductsContext` クラスに追加して、Entity Framework に Supplier テーブルをデータベースに含めます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="3ac33-127">WebApiConfig.cs で、エンティティデータモデルに &quot;のサプライヤー&quot; エンティティセットを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="3ac33-128">サプライヤーコントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="3ac33-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="3ac33-129">Controllers フォルダーに `SuppliersController` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="3ac33-130">このコントローラーに対して CRUD 操作を追加する方法については説明しません。</span><span class="sxs-lookup"><span data-stu-id="3ac33-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="3ac33-131">これらの手順は、Products コントローラーの場合と同じです (「 [OData V4 エンドポイントを作成する](create-an-odata-v4-endpoint.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="3ac33-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="3ac33-132">関連エンティティの取得</span><span class="sxs-lookup"><span data-stu-id="3ac33-132">Getting Related Entities</span></span>

<span data-ttu-id="3ac33-133">製品の供給業者を取得するために、クライアントは GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="3ac33-134">この要求をサポートするには、次のメソッドを `ProductsController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="3ac33-135">このメソッドは、既定の名前付け規則を使用します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="3ac33-136">メソッド名: GetX。ここで、X はナビゲーションプロパティです。</span><span class="sxs-lookup"><span data-stu-id="3ac33-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="3ac33-137">パラメーター名:*キー*</span><span class="sxs-lookup"><span data-stu-id="3ac33-137">Parameter name: *key*</span></span>

<span data-ttu-id="3ac33-138">この名前付け規則に従うと、Web API によって HTTP 要求がコントローラーメソッドに自動的にマップされます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="3ac33-139">HTTP 要求の例:</span><span class="sxs-lookup"><span data-stu-id="3ac33-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="3ac33-140">HTTP 応答の例:</span><span class="sxs-lookup"><span data-stu-id="3ac33-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="3ac33-141">関連コレクションの取得</span><span class="sxs-lookup"><span data-stu-id="3ac33-141">Getting a related collection</span></span>

<span data-ttu-id="3ac33-142">前の例では、製品に1つの仕入先があります。</span><span class="sxs-lookup"><span data-stu-id="3ac33-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="3ac33-143">ナビゲーションプロパティは、コレクションを返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="3ac33-144">次のコードは、業者の製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="3ac33-145">この場合、メソッドは、 **SingleResult&lt;t**ではなく**IQueryable**を返し&gt;</span><span class="sxs-lookup"><span data-stu-id="3ac33-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="3ac33-146">HTTP 要求の例:</span><span class="sxs-lookup"><span data-stu-id="3ac33-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="3ac33-147">HTTP 応答の例:</span><span class="sxs-lookup"><span data-stu-id="3ac33-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="3ac33-148">エンティティ間のリレーションシップの作成</span><span class="sxs-lookup"><span data-stu-id="3ac33-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="3ac33-149">OData は、既存の2つのエンティティ間のリレーションシップの作成または削除をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3ac33-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="3ac33-150">OData v4 の用語では、リレーションシップは &quot;参照&quot;です。</span><span class="sxs-lookup"><span data-stu-id="3ac33-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="3ac33-151">(OData v3 では、リレーションシップは*リンク*と呼ばれていました。</span><span class="sxs-lookup"><span data-stu-id="3ac33-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="3ac33-152">このチュートリアルでは、プロトコルの違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="3ac33-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="3ac33-153">参照には、`/Entity/NavigationProperty/$ref`という形式の独自の URI があります。</span><span class="sxs-lookup"><span data-stu-id="3ac33-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="3ac33-154">たとえば、製品とその業者との間の参照に対応する URI を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="3ac33-155">リレーションシップを追加するために、クライアントはこのアドレスに POST または PUT 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="3ac33-156">ナビゲーションプロパティが `Product.Supplier`などの単一のエンティティである場合は、を配置します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="3ac33-157">ナビゲーションプロパティが `Supplier.Products`などのコレクションである場合は POST。</span><span class="sxs-lookup"><span data-stu-id="3ac33-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="3ac33-158">要求の本文には、リレーションシップ内の他のエンティティの URI が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="3ac33-159">要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="3ac33-160">この例では、クライアントが PUT 要求を `/Products(6)/Supplier/$ref`に送信します。これは、ID = 6 の製品の `Supplier` の $ref URI です。</span><span class="sxs-lookup"><span data-stu-id="3ac33-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="3ac33-161">要求が成功した場合、サーバーは 204 (コンテンツなし) の応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="3ac33-162">`Product`にリレーションシップを追加するコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="3ac33-163">*NavigationProperty*パラメーターは、設定するリレーションシップを指定します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="3ac33-164">(エンティティに複数のナビゲーションプロパティがある場合は、さらに `case` ステートメントを追加できます)。</span><span class="sxs-lookup"><span data-stu-id="3ac33-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="3ac33-165">*Link*パラメーターには、業者の URI が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3ac33-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="3ac33-166">Web API は、要求本文を自動的に解析して、このパラメーターの値を取得します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="3ac33-167">業者を検索するには、*リンク*パラメーターの一部である ID (またはキー) が必要です。</span><span class="sxs-lookup"><span data-stu-id="3ac33-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="3ac33-168">これを行うには、次のヘルパーメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="3ac33-169">基本的に、このメソッドは、OData ライブラリを使用して URI パスをセグメントに分割し、キーを含むセグメントを見つけて、キーを正しい型に変換します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="3ac33-170">エンティティ間のリレーションシップの削除</span><span class="sxs-lookup"><span data-stu-id="3ac33-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="3ac33-171">リレーションシップを削除するために、クライアントは HTTP DELETE 要求を $ref URI に送信します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="3ac33-172">製品と業者の関係を削除するコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="3ac33-173">この場合、`Product.Supplier` は1対多の関係の &quot;1&quot; 終了であるため、`Product.Supplier` を `null`に設定するだけでリレーションシップを削除できます。</span><span class="sxs-lookup"><span data-stu-id="3ac33-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="3ac33-174">リレーションシップの多くの&quot; end &quot;、クライアントは、削除する関連エンティティを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ac33-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="3ac33-175">これを行うために、クライアントは、要求のクエリ文字列内に関連エンティティの URI を送信します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="3ac33-176">たとえば、"Supplier 1" から "Product 1" を削除するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="3ac33-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="3ac33-177">Web API でこれをサポートするには、`DeleteRef` メソッドに追加のパラメーターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ac33-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="3ac33-178">`Supplier.Products` 関係から製品を削除するコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ac33-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="3ac33-179">*キー*パラメーターは業者のキーであり、関連*キー*パラメーターは、`Products` リレーションシップから削除する製品のキーです。</span><span class="sxs-lookup"><span data-stu-id="3ac33-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="3ac33-180">Web API は、クエリ文字列からキーを自動的に取得することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3ac33-180">Note that Web API automatically gets the key from the query string.</span></span>
