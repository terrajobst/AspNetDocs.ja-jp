---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Web API 2 を使用した OData v3 でのエンティティリレーションのサポート |Microsoft Docs
author: MikeWasson
description: ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 クライアントは、OData を使用して移動できます...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484504"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="f3779-104">OData v3 での Web API 2 を使用したエンティティリレーションのサポート</span><span class="sxs-lookup"><span data-stu-id="f3779-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="f3779-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f3779-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f3779-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="f3779-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="f3779-107">ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="f3779-108">OData を使用すると、クライアントはエンティティの関係を移動できます。</span><span class="sxs-lookup"><span data-stu-id="f3779-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="f3779-109">製品を指定すると、業者を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="f3779-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="f3779-110">リレーションシップを作成または削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="f3779-110">You can also create or remove relationships.</span></span> <span data-ttu-id="f3779-111">たとえば、製品の仕入先を設定できます。</span><span class="sxs-lookup"><span data-stu-id="f3779-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="f3779-112">このチュートリアルでは、ASP.NET Web API でこれらの操作をサポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f3779-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="f3779-113">このチュートリアルは、 [WEB API 2 で OData V3 エンドポイントを作成する](creating-an-odata-endpoint.md)チュートリアルに基づいています。</span><span class="sxs-lookup"><span data-stu-id="f3779-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f3779-114">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="f3779-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f3779-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="f3779-115">Web API 2</span></span>
> - <span data-ttu-id="f3779-116">OData バージョン3</span><span class="sxs-lookup"><span data-stu-id="f3779-116">OData Version 3</span></span>
> - <span data-ttu-id="f3779-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="f3779-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="f3779-118">Supplier エンティティを追加する</span><span class="sxs-lookup"><span data-stu-id="f3779-118">Add a Supplier Entity</span></span>

<span data-ttu-id="f3779-119">まず、OData フィードに新しいエンティティ型を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="f3779-120">`Supplier` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="f3779-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="f3779-121">このクラスは、エンティティキーに文字列を使用します。</span><span class="sxs-lookup"><span data-stu-id="f3779-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="f3779-122">実際には、整数キーを使用するよりも、あまり一般的ではない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="f3779-123">ただし、OData が整数以外のキーの種類を処理する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="f3779-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="f3779-124">次に、`Product` クラスに `Supplier` プロパティを追加して、リレーションシップを作成します。</span><span class="sxs-lookup"><span data-stu-id="f3779-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="f3779-125">新しい**Dbset**を `ProductServiceContext` クラスに追加して、Entity Framework に `Supplier` テーブルをデータベースに含めます。</span><span class="sxs-lookup"><span data-stu-id="f3779-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="f3779-126">WebApiConfig.cs で、EDM モデルに "仕入先" エンティティを追加します。</span><span class="sxs-lookup"><span data-stu-id="f3779-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="f3779-127">ナビゲーション プロパティ</span><span class="sxs-lookup"><span data-stu-id="f3779-127">Navigation Properties</span></span>

<span data-ttu-id="f3779-128">製品の供給業者を取得するために、クライアントは GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="f3779-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="f3779-129">ここで、"Supplier" は `Product` 型のナビゲーションプロパティです。</span><span class="sxs-lookup"><span data-stu-id="f3779-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="f3779-130">この場合、`Supplier` は1つの項目を参照しますが、ナビゲーションプロパティはコレクション (一対多または多対多の関係) を返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="f3779-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="f3779-131">この要求をサポートするには、次のメソッドを `ProductsController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f3779-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="f3779-132">*キー*パラメーターは製品のキーです。</span><span class="sxs-lookup"><span data-stu-id="f3779-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="f3779-133">このメソッドは、関連エンティティ&#8212;(この場合は `Supplier` インスタンス) を返します。</span><span class="sxs-lookup"><span data-stu-id="f3779-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="f3779-134">メソッド名とパラメーター名はどちらも重要です。</span><span class="sxs-lookup"><span data-stu-id="f3779-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="f3779-135">一般に、ナビゲーションプロパティの名前が "X" の場合は、"GetX" という名前のメソッドを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="f3779-136">メソッドは、親のキーのデータ型と一致する "*key*" という名前のパラメーターを受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="f3779-137">*キー*パラメーターに **[Fromodatauri]** 属性を含めることも重要です。</span><span class="sxs-lookup"><span data-stu-id="f3779-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="f3779-138">この属性は、要求 URI からキーを解析するときに、OData 構文規則を使用するように Web API に指示します。</span><span class="sxs-lookup"><span data-stu-id="f3779-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="f3779-139">リンクの作成と削除</span><span class="sxs-lookup"><span data-stu-id="f3779-139">Creating and Deleting Links</span></span>

<span data-ttu-id="f3779-140">OData は、2つのエンティティ間のリレーションシップの作成または削除をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f3779-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="f3779-141">OData 用語では、リレーションシップは "リンク" です。</span><span class="sxs-lookup"><span data-stu-id="f3779-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="f3779-142">各リンクには、*エンティティ*/$links/*エンティティ*という形式の URI があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="f3779-143">たとえば、product から supplier へのリンクは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f3779-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="f3779-144">新しいリンクを作成するために、クライアントは、リンク URI に POST 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="f3779-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="f3779-145">要求の本文は、ターゲットエンティティの URI です。</span><span class="sxs-lookup"><span data-stu-id="f3779-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="f3779-146">たとえば、"CTSO" というキーを持つ業者があるとします。</span><span class="sxs-lookup"><span data-stu-id="f3779-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="f3779-147">"Product (1)" から "Supplier (' CTSO ')" へのリンクを作成するために、クライアントは次のような要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="f3779-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="f3779-148">リンクを削除するには、クライアントがリンク URI に DELETE 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="f3779-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="f3779-149">**リンクの作成**</span><span class="sxs-lookup"><span data-stu-id="f3779-149">**Creating Links**</span></span>

<span data-ttu-id="f3779-150">クライアントが製品供給業者のリンクを作成できるようにするには、次のコードを `ProductsController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f3779-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="f3779-151">このメソッドには、次の 3 つのパラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="f3779-151">This method takes three parameters:</span></span>

- <span data-ttu-id="f3779-152">*キー*: 親エンティティ (製品) へのキー</span><span class="sxs-lookup"><span data-stu-id="f3779-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="f3779-153">*navigationProperty*: ナビゲーションプロパティの名前。</span><span class="sxs-lookup"><span data-stu-id="f3779-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="f3779-154">この例では、有効なナビゲーションプロパティは "Supplier" だけです。</span><span class="sxs-lookup"><span data-stu-id="f3779-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="f3779-155">*リンク*: 関連エンティティの OData URI。</span><span class="sxs-lookup"><span data-stu-id="f3779-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="f3779-156">この値は、要求本文から取得されます。</span><span class="sxs-lookup"><span data-stu-id="f3779-156">This value is taken from the request body.</span></span> <span data-ttu-id="f3779-157">たとえば、リンク URI は "`http://localhost/odata/Suppliers('CTSO')`、つまり、ID が ' CTSO ' の業者を意味します。</span><span class="sxs-lookup"><span data-stu-id="f3779-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="f3779-158">このメソッドは、リンクを使用して業者を検索します。</span><span class="sxs-lookup"><span data-stu-id="f3779-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="f3779-159">一致する業者が見つかった場合、メソッドは `Product.Supplier` プロパティを設定し、結果をデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="f3779-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="f3779-160">最も難しい部分は、リンク URI の解析です。</span><span class="sxs-lookup"><span data-stu-id="f3779-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="f3779-161">基本的には、その URI に GET 要求を送信した結果をシミュレートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="f3779-162">次のヘルパーメソッドは、この方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f3779-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="f3779-163">メソッドは、Web API ルーティングプロセスを呼び出し、解析された OData パスを表す**ODataPath**インスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="f3779-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="f3779-164">リンク URI の場合、セグメントの1つをエンティティキーにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="f3779-165">(存在しない場合、クライアントは無効な URI を送信しました)。</span><span class="sxs-lookup"><span data-stu-id="f3779-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="f3779-166">**リンクの削除**</span><span class="sxs-lookup"><span data-stu-id="f3779-166">**Deleting Links**</span></span>

<span data-ttu-id="f3779-167">リンクを削除するには、`ProductsController` クラスに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f3779-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="f3779-168">この例では、ナビゲーションプロパティは単一の `Supplier` エンティティです。</span><span class="sxs-lookup"><span data-stu-id="f3779-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="f3779-169">ナビゲーションプロパティがコレクションの場合、リンクを削除するための URI には、関連エンティティのキーが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="f3779-170">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f3779-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="f3779-171">この要求により、顧客1の注文1が削除されます。</span><span class="sxs-lookup"><span data-stu-id="f3779-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="f3779-172">この場合、DeleteLink メソッドのシグネチャは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f3779-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="f3779-173">関連付けられた*キー*パラメーターは、関連エンティティのキーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f3779-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="f3779-174">したがって、`DeleteLink` メソッドでは、 *key*パラメーターでプライマリエンティティを検索し、関連するエンティティを関連する*キー*パラメーターで検索してから、関連付けを削除します。</span><span class="sxs-lookup"><span data-stu-id="f3779-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="f3779-175">データモデルによっては、`DeleteLink`の両方のバージョンを実装することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f3779-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="f3779-176">Web API は、要求 URI に基づいて正しいバージョンを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f3779-176">Web API will call the correct version based on the request URI.</span></span>
