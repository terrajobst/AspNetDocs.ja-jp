---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 'パート 6: 製品および注文のコントローラーの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421288"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="3cd79-102">パート 6: 製品および注文コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="3cd79-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="3cd79-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3cd79-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3cd79-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="3cd79-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="3cd79-105">製品コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="3cd79-105">Add a Products Controller</span></span>

<span data-ttu-id="3cd79-106">管理コントローラーは、管理者特権を持つユーザーのためのものです。</span><span class="sxs-lookup"><span data-stu-id="3cd79-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="3cd79-107">一方、顧客は製品を表示できますが、作成、更新、または削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="3cd79-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="3cd79-108">Get メソッドを開いたままにして、Post、Put、Delete の各メソッドへのアクセスを簡単に制限することができます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="3cd79-109">しかし、製品に関して返されるデータを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="3cd79-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="3cd79-110">`ActualCost` のプロパティは、お客様に表示されません。</span><span class="sxs-lookup"><span data-stu-id="3cd79-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="3cd79-111">この問題を解決するには、ユーザーに表示する必要があるプロパティのサブセットを含む*データ転送オブジェクト*(DTO) を定義します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="3cd79-112">ここでは、LINQ を使用してインスタンスを `ProductDTO` `Product` インスタンスを射影します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="3cd79-113">`ProductDTO` という名前のクラスを [モデル] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="3cd79-114">次に、コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-114">Now add the controller.</span></span> <span data-ttu-id="3cd79-115">ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="3cd79-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="3cd79-116">**[追加]** を選択し、 **[コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="3cd79-117">**[コントローラーの追加]** ダイアログボックスで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="3cd79-118">**[テンプレート]** で **[空の API コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="3cd79-119">ソースファイル内のすべてのものを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="3cd79-120">コントローラーは引き続き `OrdersContext` を使用してデータベースを照会します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="3cd79-121">ただし、`Product` インスタンスを直接返すのではなく、`MapProducts` を呼び出して `ProductDTO` インスタンスに射影します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="3cd79-122">`MapProducts` メソッドは**IQueryable**を返します。そのため、他のクエリパラメーターを使用して結果を構成できます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="3cd79-123">これは、 **where**句をクエリに追加する `GetProduct` メソッドで確認できます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="3cd79-124">Orders コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="3cd79-124">Add an Orders Controller</span></span>

<span data-ttu-id="3cd79-125">次に、ユーザーが注文を作成および表示できるようにするコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="3cd79-126">まず、別の DTO を使用します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-126">We'll start with another DTO.</span></span> <span data-ttu-id="3cd79-127">ソリューションエクスプローラーで、[モデル] フォルダーを右クリックし、次の実装を使用して `OrderDTO` という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="3cd79-128">次に、コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-128">Now add the controller.</span></span> <span data-ttu-id="3cd79-129">ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="3cd79-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="3cd79-130">**[追加]** を選択し、 **[コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="3cd79-131">**[コントローラーの追加]** ダイアログで、次のオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="3cd79-132">**[コントローラー名]** に「OrdersController」と入力します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="3cd79-133">**テンプレート** で、Entity Framework を使用した、読み取り/書き込みアクションがある API コントローラー を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="3cd79-134">**モデルクラス** で、&quot;の順序 (Productstore. モデル)&quot;を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="3cd79-135">**[データコンテキストクラス]** で、[&quot;OrdersContext (Productstore. モデル)&quot;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="3cd79-136">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3cd79-136">Click **Add**.</span></span> <span data-ttu-id="3cd79-137">これにより、OrdersController.cs という名前のファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="3cd79-138">次に、コントローラーの既定の実装を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3cd79-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="3cd79-139">最初に、`PutOrder` および `DeleteOrder` メソッドを削除します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="3cd79-140">このサンプルでは、顧客が既存の注文を変更または削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="3cd79-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="3cd79-141">実際のアプリケーションでは、これらのケースを処理するために多くのバックエンドロジックが必要になります。</span><span class="sxs-lookup"><span data-stu-id="3cd79-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="3cd79-142">(たとえば、注文は既に発送されていますか)。</span><span class="sxs-lookup"><span data-stu-id="3cd79-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="3cd79-143">ユーザーに属する注文だけを返すように `GetOrders` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="3cd79-144">`GetOrder` メソッドを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="3cd79-145">メソッドに加えられた変更を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="3cd79-146">戻り値は、`Order`ではなく、`OrderDTO` インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="3cd79-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="3cd79-147">データベースに対して注文のクエリを実行する場合は、 [Dbquery. Include](https://msdn.microsoft.com/library/gg696395)メソッドを使用して、関連する `OrderDetail` および `Product` エンティティをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="3cd79-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="3cd79-148">射影を使用して結果を平坦化します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="3cd79-149">HTTP 応答には、数量を含む製品の配列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="3cd79-150">この形式は、クライアントが、入れ子になったエンティティ (順序、詳細、および製品) を含む元のオブジェクトグラフよりも簡単に使用できます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="3cd79-151">`PostOrder`を考慮する最後のメソッド。</span><span class="sxs-lookup"><span data-stu-id="3cd79-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="3cd79-152">現時点では、このメソッドは `Order` インスタンスを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3cd79-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="3cd79-153">しかし、クライアントが次のような要求本文を送信した場合はどうなるかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="3cd79-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="3cd79-154">これは適切に構成された順序であり、Entity Framework によってデータベースに挿入されます。</span><span class="sxs-lookup"><span data-stu-id="3cd79-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="3cd79-155">ただし、これには以前に存在していなかった製品エンティティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3cd79-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="3cd79-156">クライアントは、データベースに新しい製品を作成しました。</span><span class="sxs-lookup"><span data-stu-id="3cd79-156">The client just created a new product in our database!</span></span> <span data-ttu-id="3cd79-157">これは、注文調達部門に対して、お客様が注文を受けたときに驚くようになります。</span><span class="sxs-lookup"><span data-stu-id="3cd79-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="3cd79-158">教訓は、POST または PUT 要求で受け入れられるデータについて慎重に検討することです。</span><span class="sxs-lookup"><span data-stu-id="3cd79-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="3cd79-159">この問題を回避するには、`OrderDTO` インスタンスを取得するように `PostOrder` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="3cd79-160">`Order`を作成するには、`OrderDTO` を使用します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="3cd79-161">`ProductID` と `Quantity` のプロパティを使用し、クライアントが製品名または価格に対して送信した値は無視されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3cd79-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="3cd79-162">製品 ID が有効でない場合は、データベース内の foreign key 制約に違反するため、挿入は失敗します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="3cd79-163">`PostOrder` の完全な方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="3cd79-164">最後に、**承認**属性をコントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="3cd79-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="3cd79-165">登録済みのユーザーのみが注文を作成または表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3cd79-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3cd79-166">[前へ](using-web-api-with-entity-framework-part-5.md)
> [次へ](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="3cd79-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
