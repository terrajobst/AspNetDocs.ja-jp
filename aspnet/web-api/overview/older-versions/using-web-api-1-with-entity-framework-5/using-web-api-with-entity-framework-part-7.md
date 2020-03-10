---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 'パート 7: メインページを作成する |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484450"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="c460f-102">パート 7: メインページの作成</span><span class="sxs-lookup"><span data-stu-id="c460f-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="c460f-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c460f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c460f-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="c460f-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="c460f-105">メイン ページの作成</span><span class="sxs-lookup"><span data-stu-id="c460f-105">Creating the Main Page</span></span>

<span data-ttu-id="c460f-106">このセクションでは、メインアプリケーションページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c460f-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="c460f-107">このページは管理者ページより複雑になるため、いくつかの手順でアプローチします。</span><span class="sxs-lookup"><span data-stu-id="c460f-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="c460f-108">その過程で、いくつかの高度なノックアウト手法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c460f-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="c460f-109">次に、ページの基本的なレイアウトを示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="c460f-110">"Products" は、製品の配列を保持します。</span><span class="sxs-lookup"><span data-stu-id="c460f-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="c460f-111">"カート" は、数量を持つ製品の配列を保持します。</span><span class="sxs-lookup"><span data-stu-id="c460f-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="c460f-112">[カートに追加] をクリックすると、カートが更新されます。</span><span class="sxs-lookup"><span data-stu-id="c460f-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="c460f-113">"Orders" は、注文 Id の配列を保持します。</span><span class="sxs-lookup"><span data-stu-id="c460f-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="c460f-114">"詳細" は、商品の配列である注文明細 (数量を含む製品) を保持します。</span><span class="sxs-lookup"><span data-stu-id="c460f-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="c460f-115">まず、データバインドまたはスクリプトを使用せずに、HTML でいくつかの基本的なレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="c460f-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="c460f-116">Views/Home/Index を開き、すべての内容を次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c460f-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="c460f-117">次に、Scripts セクションを追加し、空のビューモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c460f-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="c460f-118">前の設計に基づいて、ビューモデルでは、製品、カート、注文、および詳細の observable が必要です。</span><span class="sxs-lookup"><span data-stu-id="c460f-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="c460f-119">`AppViewModel` オブジェクトに次の変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="c460f-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="c460f-120">ユーザーは、製品リストからカートに商品を追加したり、カートから品目を削除したりできます。</span><span class="sxs-lookup"><span data-stu-id="c460f-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="c460f-121">これらの関数をカプセル化するには、製品を表すビューモデルクラスをもう1つ作成します。</span><span class="sxs-lookup"><span data-stu-id="c460f-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="c460f-122">`AppViewModel` に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c460f-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="c460f-123">`ProductViewModel` クラスには、カートに製品を移動するために使用する2つの関数が含まれています。 `addItemToCart` 製品の1つの単位をカートに追加し、`removeAllFromCart` 製品のすべての数量を削除します。</span><span class="sxs-lookup"><span data-stu-id="c460f-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="c460f-124">ユーザーは、既存の注文を選択して注文の詳細を取得できます。</span><span class="sxs-lookup"><span data-stu-id="c460f-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="c460f-125">この機能を別のビューモデルにカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="c460f-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="c460f-126">`OrderDetailsViewModel` は順序を使用して初期化され、サーバーに AJAX 要求を送信して注文の詳細をフェッチします。</span><span class="sxs-lookup"><span data-stu-id="c460f-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="c460f-127">また、`OrderDetailsViewModel`の `total` プロパティにも注目してください。</span><span class="sxs-lookup"><span data-stu-id="c460f-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="c460f-128">このプロパティは、計算された[観測](http://knockoutjs.com/documentation/computedObservables.html)可能なと呼ばれる特別な種類の観測可能なオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="c460f-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="c460f-129">この名前が示すように、計算された観測可能なデータを&#8212;使用して、この場合は、注文の合計コストを計算値にバインドします。</span><span class="sxs-lookup"><span data-stu-id="c460f-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="c460f-130">次に、次の関数を `AppViewModel`に追加します。</span><span class="sxs-lookup"><span data-stu-id="c460f-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="c460f-131">`resetCart` カートからすべての項目を削除します。</span><span class="sxs-lookup"><span data-stu-id="c460f-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="c460f-132">`getDetails` は、新しい `OrderDetailsViewModel` を `details` の一覧にプッシュすることによって、注文の詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="c460f-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="c460f-133">`createOrder` によって新しい注文が作成され、カートが空になります。</span><span class="sxs-lookup"><span data-stu-id="c460f-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="c460f-134">最後に、製品および注文に対して AJAX 要求を行うことで、ビューモデルを初期化します。</span><span class="sxs-lookup"><span data-stu-id="c460f-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="c460f-135">そうですね。コードは非常に簡単ですが、ステップバイステップで構築しましたので、設計は明確であることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c460f-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="c460f-136">これで、いくつかのノックアウトバインドを HTML に追加できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c460f-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="c460f-137">**成果物**</span><span class="sxs-lookup"><span data-stu-id="c460f-137">**Products**</span></span>

<span data-ttu-id="c460f-138">製品リストのバインドは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c460f-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="c460f-139">Products 配列に対して反復処理を行い、名前と価格を表示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="c460f-140">[順序の追加] ボタンは、ユーザーがログインしている場合にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="c460f-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="c460f-141">[順序の追加] ボタンをクリックすると、製品の `ProductViewModel` インスタンスで `addItemToCart` が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c460f-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="c460f-142">これは、ノックアウトの便利な機能を示しています。ビューモデルに他のビューモデルが含まれている場合は、そのバインドを内部モデルに適用できます。</span><span class="sxs-lookup"><span data-stu-id="c460f-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="c460f-143">この例では、`foreach` 内のバインドが `ProductViewModel` の各インスタンスに適用されます。</span><span class="sxs-lookup"><span data-stu-id="c460f-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="c460f-144">この方法は、すべての機能を1つのビューモデルに配置するよりも、はるかにすっきりしています。</span><span class="sxs-lookup"><span data-stu-id="c460f-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="c460f-145">**カート**</span><span class="sxs-lookup"><span data-stu-id="c460f-145">**Cart**</span></span>

<span data-ttu-id="c460f-146">カートのバインドは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c460f-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="c460f-147">これにより、カート配列を反復処理し、名前、価格、および数量を表示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="c460f-148">[削除] リンクと [注文の作成] ボタンがビューモデル関数にバインドされていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c460f-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="c460f-149">**Orders (注文)**</span><span class="sxs-lookup"><span data-stu-id="c460f-149">**Orders**</span></span>

<span data-ttu-id="c460f-150">Orders リストのバインドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="c460f-151">注文を反復処理し、注文 ID を表示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="c460f-152">リンク上の click イベントは、`getDetails` 関数にバインドされています。</span><span class="sxs-lookup"><span data-stu-id="c460f-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="c460f-153">**注文の詳細**</span><span class="sxs-lookup"><span data-stu-id="c460f-153">**Order Details**</span></span>

<span data-ttu-id="c460f-154">次に、注文の詳細のバインドを示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="c460f-155">これにより、注文の項目を反復処理し、製品、価格、および数量を表示します。</span><span class="sxs-lookup"><span data-stu-id="c460f-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="c460f-156">周囲の div は、details 配列に1つ以上の項目が含まれている場合にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="c460f-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c460f-157">まとめ</span><span class="sxs-lookup"><span data-stu-id="c460f-157">Conclusion</span></span>

<span data-ttu-id="c460f-158">このチュートリアルでは、Entity Framework を使用してデータベースと通信するアプリケーションを作成し、データ層の上に公開インターフェイスを提供するように ASP.NET Web API しました。</span><span class="sxs-lookup"><span data-stu-id="c460f-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="c460f-159">ASP.NET MVC 4 を使用して HTML ページをレンダリングします。また、ページを再読み込みせずに動的な対話を行うために、ノックアウトと jQuery を組み合わせて使用します。</span><span class="sxs-lookup"><span data-stu-id="c460f-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="c460f-160">その他のリソース:</span><span class="sxs-lookup"><span data-stu-id="c460f-160">Additional resources:</span></span>

- [<span data-ttu-id="c460f-161">ASP.NET データアクセスコンテンツマップ</span><span class="sxs-lookup"><span data-stu-id="c460f-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="c460f-162">Entity Framework デベロッパーセンター</span><span class="sxs-lookup"><span data-stu-id="c460f-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> <span data-ttu-id="c460f-163">[[戻る]](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="c460f-163">[Previous](using-web-api-with-entity-framework-part-6.md)</span></span>
