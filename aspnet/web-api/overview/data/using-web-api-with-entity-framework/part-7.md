---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: ビューを作成する (UI) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448984"
---
# <a name="create-the-view-ui"></a><span data-ttu-id="3d50f-102">ビューの作成 (UI)</span><span class="sxs-lookup"><span data-stu-id="3d50f-102">Create the View (UI)</span></span>

<span data-ttu-id="3d50f-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3d50f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3d50f-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="3d50f-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="3d50f-105">このセクションでは、アプリの HTML の定義を開始し、HTML とビューモデルの間にデータバインディングを追加します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="3d50f-106">Views/Home/Index. cshtml というファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3d50f-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="3d50f-107">そのファイルの内容全体を次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3d50f-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="3d50f-108">`div` の要素のほとんどは、[ブートストラップ](http://getbootstrap.com/)のスタイルを設定するために用意されています。</span><span class="sxs-lookup"><span data-stu-id="3d50f-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="3d50f-109">重要な要素は、`data-bind` 属性を持つ要素です。</span><span class="sxs-lookup"><span data-stu-id="3d50f-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="3d50f-110">この属性は、HTML をビューモデルにリンクします。</span><span class="sxs-lookup"><span data-stu-id="3d50f-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="3d50f-111">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="3d50f-112">この例では、&quot;`text`&quot; のバインドによって、`<p>` 要素によって、ビューモデルからの `error` プロパティの値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3d50f-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="3d50f-113">`error` が `ko.observable`として宣言されていることを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="3d50f-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="3d50f-114">新しい値が `error`に割り当てられるたびに、`<p>` 要素内のテキストがノックアウトによって更新されます。</span><span class="sxs-lookup"><span data-stu-id="3d50f-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="3d50f-115">`foreach` binding は、`books` 配列の内容をループするようにノックアウトに指示します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="3d50f-116">ノックアウトは、配列内の各項目に対して新しい &lt;li&gt; 要素を作成します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="3d50f-117">`foreach` のコンテキスト内のバインディングは、配列項目のプロパティを参照します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="3d50f-118">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="3d50f-119">ここでは、`text` バインドは各書籍の Author プロパティを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="3d50f-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="3d50f-120">ここでアプリケーションを実行すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3d50f-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="3d50f-121">ページが読み込まれた後、ブックの一覧が非同期に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="3d50f-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="3d50f-122">現時点では、&quot;の詳細&quot; リンクは機能していません。</span><span class="sxs-lookup"><span data-stu-id="3d50f-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="3d50f-123">次のセクションでは、この機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="3d50f-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3d50f-124">[前へ](part-6.md)
> [次へ](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="3d50f-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
