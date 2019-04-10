---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: $Select を使用して、$ の展開、および ASP.NET Web API 2 odata - ASP.NET $value 4.x
author: MikeWasson
description: $ の概要およびコード サンプルを展開し、$select と ASP.NET の場合、この $value は OData Web API 2 でオプション 4.x です。
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400699"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="d7e93-103">ASP.NET Web API 2 OData で $select, $expand, および $value を使用する</span><span class="sxs-lookup"><span data-stu-id="d7e93-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="d7e93-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d7e93-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d7e93-105">$ の概要およびコード サンプルを展開し、$select と ASP.NET の場合、この $value は OData Web API 2 でオプション 4.x です。</span><span class="sxs-lookup"><span data-stu-id="d7e93-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="d7e93-106">これらのオプションは、サーバーから返された形式を制御することをクライアントに許可します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="d7e93-107">**$expand** は、応答にインラインで含まれる関連するエンティティを発生させます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="d7e93-108">**$select**は、応答に含めるプロパティのサブセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="d7e93-109">**$value**は、プロパティの未加工の値を取得します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="d7e93-110">スキーマの例</span><span class="sxs-lookup"><span data-stu-id="d7e93-110">Example Schema</span></span>

<span data-ttu-id="d7e93-111">この記事では、3 つのエンティティを定義する OData サービスを使用します。製品、仕入先、およびカテゴリ。</span><span class="sxs-lookup"><span data-stu-id="d7e93-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="d7e93-112">各製品には、1 つのカテゴリと仕入先の 1 つがあります。</span><span class="sxs-lookup"><span data-stu-id="d7e93-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="d7e93-113">エンティティ モデルを定義する c# クラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="d7e93-114">注意、`Product`クラスのナビゲーション プロパティを定義、`Supplier`と`Category`します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="d7e93-115">`Category`クラスは、各カテゴリの製品のナビゲーション プロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="d7e93-116">このスキーマの OData エンドポイントを作成するには、Visual Studio 2013 のスキャフォールディングを」の説明に従って使用[で ASP.NET Web API OData エンドポイントを作成する](odata-v3/creating-an-odata-endpoint.md)します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="d7e93-117">製品、カテゴリ、および仕入先の別のコント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="d7e93-118">$ の有効化を展開し、$select</span><span class="sxs-lookup"><span data-stu-id="d7e93-118">Enabling $expand and $select</span></span>

<span data-ttu-id="d7e93-119">Visual Studio 2013 では、Web API OData のスキャフォールディングは、その $ の展開を自動的にサポートおよび $select にコント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="d7e93-120">リファレンスについては、ここでは $ をサポートするための要件を展開し、コント ローラーの $select します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="d7e93-121">コレクションの場合、コント ローラーの`Get`メソッドが返す必要があります、 **IQueryable**します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="d7e93-122">単一のエンティティを返す、 **SingleResult&lt;T&gt;**、T は、 **IQueryable** 0 または 1 つのエンティティを格納しています。</span><span class="sxs-lookup"><span data-stu-id="d7e93-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="d7e93-123">また、装飾、`Get`メソッド、 **[Queryable]** 属性は、前のコード スニペットで示すように。</span><span class="sxs-lookup"><span data-stu-id="d7e93-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="d7e93-124">代わりに、呼び出す**EnableQuerySupport**上、 **HttpConfiguration**スタートアップ時のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="d7e93-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="d7e93-125">(詳細については、次を参照してください[OData クエリ オプションを有効にする](supporting-odata-query-options.md#enable)。)。</span><span class="sxs-lookup"><span data-stu-id="d7e93-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="d7e93-126">$ を使用して展開</span><span class="sxs-lookup"><span data-stu-id="d7e93-126">Using $expand</span></span>

<span data-ttu-id="d7e93-127">OData エンティティまたはコレクションを照会するときに、既定の応答に関連するエンティティは含まれません。</span><span class="sxs-lookup"><span data-stu-id="d7e93-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="d7e93-128">たとえば、カテゴリ エンティティ セットの既定の応答を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="d7e93-129">ご覧のように、応答は含まれません任意の製品では、Category エンティティは製品のナビゲーション リンク。</span><span class="sxs-lookup"><span data-stu-id="d7e93-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="d7e93-130">ただし、クライアントは $ を使用できる展開すると、各カテゴリの製品の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="d7e93-131">$Expand オプションを展開し、要求のクエリ文字列には。</span><span class="sxs-lookup"><span data-stu-id="d7e93-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="d7e93-132">これで、サーバー カテゴリごとに、インラインで、カテゴリの製品が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="d7e93-133">応答ペイロードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="d7e93-134">"Value"配列内の各エントリに製品一覧が含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="d7e93-135">$ では、展開するナビゲーション プロパティのオプションはコンマ区切りの一覧を展開します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="d7e93-136">次の要求は、カテゴリと製品の仕入先の両方を展開します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="d7e93-137">応答本文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="d7e93-138">ナビゲーション プロパティの 1 つ以上のレベルを展開することができます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="d7e93-139">次の例には、カテゴリのすべての製品と各製品の仕入先が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="d7e93-140">応答本文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="d7e93-141">既定では、Web API は、2、最大の深さを制限します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="d7e93-142">ような複雑な要求を送信することから、クライアントを妨げる`$expand=Orders/OrderDetails/Product/Supplier/Region`、効率的にクエリを実行し、大規模な応答を作成するがあります。</span><span class="sxs-lookup"><span data-stu-id="d7e93-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="d7e93-143">既定値を上書きするには、設定、 **MaxExpansionDepth**プロパティを **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="d7e93-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="d7e93-144">$ の詳細については、オプションを展開するを参照してください。 [Expand システム クエリ オプション ($ の展開)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) 、公式の OData ドキュメント。</span><span class="sxs-lookup"><span data-stu-id="d7e93-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="d7e93-145">$Select を使用します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-145">Using $select</span></span>

<span data-ttu-id="d7e93-146">$Select オプションでは、応答本文に含めるプロパティのサブセットを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="d7e93-147">たとえば、名前と各製品の価格を取得するには、次のクエリを使用します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="d7e93-148">応答本文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="d7e93-149">$Select を組み合わせることができ、$ が同じクエリ内で展開します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="d7e93-150">$Select オプションに展開されたプロパティを含めるに確認します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="d7e93-151">たとえば、次の要求は、業者と製品の名前を取得します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="d7e93-152">応答本文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="d7e93-153">展開のプロパティ内のプロパティを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="d7e93-154">次の要求では、製品を展開し、カテゴリ名と製品名を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="d7e93-155">応答本文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="d7e93-156">$Select オプションの詳細については、次を参照してください。 [Select システム クエリ オプション ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) 、公式の OData ドキュメント。</span><span class="sxs-lookup"><span data-stu-id="d7e93-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="d7e93-157">エンティティ ($value) の個々 のプロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="d7e93-158">エンティティから個々 のプロパティを取得する OData クライアントの 2 つの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="d7e93-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="d7e93-159">クライアントでは、OData の形式で値を取得することまたは、プロパティの生の値を取得できます。</span><span class="sxs-lookup"><span data-stu-id="d7e93-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="d7e93-160">次の要求は、OData 形式でプロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="d7e93-161">JSON 形式で応答の例を示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="d7e93-162">プロパティの生の値を取得するには、URI に $value を追加します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="d7e93-163">応答を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-163">Here is the response.</span></span> <span data-ttu-id="d7e93-164">コンテンツの種類が"text/plain"、JSON に注意してください。</span><span class="sxs-lookup"><span data-stu-id="d7e93-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="d7e93-165">という名前のメソッドを追加すると、OData コント ローラーでこれらのクエリをサポートするために`GetProperty`ここで、`Property`プロパティの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="d7e93-166">たとえば、Name プロパティを取得するメソッドを名前は`GetName`します。</span><span class="sxs-lookup"><span data-stu-id="d7e93-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="d7e93-167">メソッドは、そのプロパティの値を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7e93-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
