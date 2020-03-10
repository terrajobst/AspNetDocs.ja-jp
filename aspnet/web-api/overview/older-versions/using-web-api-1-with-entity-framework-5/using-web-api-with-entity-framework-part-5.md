---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 'パート 5: ノックアウトを使用した動的 UI の作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447862"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="f8041-102">パート 5: ノックアウトを使用した動的 UI の作成</span><span class="sxs-lookup"><span data-stu-id="f8041-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="f8041-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f8041-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f8041-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="f8041-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="f8041-105">Knockout.js で動的 UI を作成する</span><span class="sxs-lookup"><span data-stu-id="f8041-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="f8041-106">このセクションでは、ノックアウトを使用して管理ビューに機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="f8041-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="f8041-107">[ノックアウト](http://knockoutjs.com/)は、HTML コントロールを簡単にデータにバインドできる Javascript ライブラリです。</span><span class="sxs-lookup"><span data-stu-id="f8041-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="f8041-108">ノックアウトは、モデルビュービューモデル (MVVM) パターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="f8041-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="f8041-109">この*モデル*は、ビジネスドメイン内のデータ (ここでは、製品と注文) のサーバー側表現です。</span><span class="sxs-lookup"><span data-stu-id="f8041-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="f8041-110">*ビュー*はプレゼンテーション層 (HTML) です。</span><span class="sxs-lookup"><span data-stu-id="f8041-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="f8041-111">*ビューモデル*は、モデルデータを保持する Javascript オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="f8041-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="f8041-112">ビューモデルは、UI のコード抽象化です。</span><span class="sxs-lookup"><span data-stu-id="f8041-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="f8041-113">HTML 表現に関する情報はありません。</span><span class="sxs-lookup"><span data-stu-id="f8041-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="f8041-114">代わりに、"項目のリスト" など、ビューの抽象的な機能を表します。</span><span class="sxs-lookup"><span data-stu-id="f8041-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="f8041-115">ビューは、ビューモデルにデータバインドされています。</span><span class="sxs-lookup"><span data-stu-id="f8041-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="f8041-116">ビューモデルに対する更新は、自動的にビューに反映されます。</span><span class="sxs-lookup"><span data-stu-id="f8041-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="f8041-117">ビューモデルでは、ボタンのクリックなど、ビューからイベントを取得したり、注文の作成など、モデルに対する操作を実行したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f8041-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="f8041-118">まず、ビューモデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="f8041-118">First we'll define the view-model.</span></span> <span data-ttu-id="f8041-119">その後、HTML マークアップをビューモデルにバインドします。</span><span class="sxs-lookup"><span data-stu-id="f8041-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="f8041-120">次の Razor セクションを Admin. cshtml に追加します。</span><span class="sxs-lookup"><span data-stu-id="f8041-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="f8041-121">このセクションは、ファイルの任意の場所に追加できます。</span><span class="sxs-lookup"><span data-stu-id="f8041-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="f8041-122">ビューが表示されると、HTML ページの下部に、終了 &lt;/本文&gt; タグの直前に、セクションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8041-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="f8041-123">このページのすべてのスクリプトは、コメントで示されているスクリプトタグ内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8041-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="f8041-124">まず、ビューモデルクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="f8041-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="f8041-125">**ko**は、"*観測*可能" と呼ばれる、ノックアウトの特殊なオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="f8041-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="f8041-126">[ノックアウトドキュメント](http://knockoutjs.com/documentation/observables.html)から: 観測可能なは、変更についてサブスクライバーに通知できる "JavaScript オブジェクト" です。</span><span class="sxs-lookup"><span data-stu-id="f8041-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="f8041-127">監視可能な変更の内容が一致するように、ビューが自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="f8041-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="f8041-128">`products` 配列にデータを設定するには、web API に対して AJAX 要求を行います。</span><span class="sxs-lookup"><span data-stu-id="f8041-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="f8041-129">API のベース URI がビューバッグに格納されていることを思い出してください (チュートリアルの[パート 4](using-web-api-with-entity-framework-part-4.md)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f8041-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="f8041-130">次に、ビューモデルに関数を追加して、製品を作成、更新、および削除します。</span><span class="sxs-lookup"><span data-stu-id="f8041-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="f8041-131">これらの関数は、AJAX 呼び出しを web API に送信し、結果を使用してビューモデルを更新します。</span><span class="sxs-lookup"><span data-stu-id="f8041-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="f8041-132">ここで最も重要なのは、DOM が非常に読み込まれるときに、 **ko**関数を呼び出し、`ProductsViewModel`の新しいインスタンスを渡すことです。</span><span class="sxs-lookup"><span data-stu-id="f8041-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="f8041-133">**Ko**メソッドは、ノックアウトをアクティブにし、ビューモデルをビューに配線します。</span><span class="sxs-lookup"><span data-stu-id="f8041-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="f8041-134">ビューモデルが用意できたので、次にバインドを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8041-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="f8041-135">これを行うには、`data-bind` 属性を HTML 要素に追加します。</span><span class="sxs-lookup"><span data-stu-id="f8041-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="f8041-136">たとえば、HTML リストを配列にバインドするには、`foreach` バインドを使用します。</span><span class="sxs-lookup"><span data-stu-id="f8041-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="f8041-137">`foreach` バインディングは配列を反復処理し、配列内の各オブジェクトに対して子要素を作成します。</span><span class="sxs-lookup"><span data-stu-id="f8041-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="f8041-138">子要素のバインドは、配列オブジェクトのプロパティを参照できます。</span><span class="sxs-lookup"><span data-stu-id="f8041-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="f8041-139">次のバインドを "更新-製品" リストに追加します。</span><span class="sxs-lookup"><span data-stu-id="f8041-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="f8041-140">`<li>` 要素は、 **foreach**バインドのスコープ内で発生します。</span><span class="sxs-lookup"><span data-stu-id="f8041-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="f8041-141">つまり、抜き合わせは、`products` 配列内の製品ごとに1回要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f8041-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="f8041-142">`<li>` 要素内のすべてのバインドは、その製品インスタンスを参照します。</span><span class="sxs-lookup"><span data-stu-id="f8041-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="f8041-143">たとえば、`$data.Name` は、製品の `Name` プロパティを参照します。</span><span class="sxs-lookup"><span data-stu-id="f8041-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="f8041-144">テキスト入力の値を設定するには、`value` バインドを使用します。</span><span class="sxs-lookup"><span data-stu-id="f8041-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="f8041-145">これらのボタンは、`click` バインディングを使用して、モデルビューの関数にバインドされます。</span><span class="sxs-lookup"><span data-stu-id="f8041-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="f8041-146">製品インスタンスは、各関数にパラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8041-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="f8041-147">詳細については、さまざまなバインドについての適切な説明を[ノックアウトドキュメント](http://knockoutjs.com/documentation/observables.html)に記載しています。</span><span class="sxs-lookup"><span data-stu-id="f8041-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="f8041-148">次に、[製品の追加] フォームで**submit**イベントのバインドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f8041-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="f8041-149">このバインディングは、ビューモデルの `create` 関数を呼び出して、新しい製品を作成します。</span><span class="sxs-lookup"><span data-stu-id="f8041-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="f8041-150">管理ビューの完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="f8041-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="f8041-151">アプリケーションを実行し、管理者アカウントでログインして、[Admin] \ (管理者 \) リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f8041-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="f8041-152">製品の一覧が表示され、製品を作成、更新、または削除できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f8041-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f8041-153">[前へ](using-web-api-with-entity-framework-part-4.md)
> [次へ](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="f8041-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
