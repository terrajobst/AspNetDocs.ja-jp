---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 項目の詳細を表示する |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449002"
---
# <a name="display-item-details"></a><span data-ttu-id="e6a9a-102">作業項目の表示</span><span class="sxs-lookup"><span data-stu-id="e6a9a-102">Display Item Details</span></span>

<span data-ttu-id="e6a9a-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e6a9a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e6a9a-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="e6a9a-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="e6a9a-105">このセクションでは、各ブックの詳細を表示する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="e6a9a-106">App.config で、ビューモデルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="e6a9a-107">Views/Home/Index. cshtml で、データバインド要素を Details リンクに追加します。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="e6a9a-108">これにより、&gt; 要素 &lt;のクリックハンドラーがビューモデルの `getBookDetail` 関数にバインドされます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="e6a9a-109">同じファイルで、次のマークアップを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="e6a9a-110">以下に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="e6a9a-111">このマークアップは、ビューモデルで監視可能な `detail` のプロパティにデータバインドされたテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="e6a9a-112">"&lt;!--ko--&gt;&quot; 構文では、DOM 要素の外側にあるノックアウトバインドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="e6a9a-113">この場合、`if` バインドを使用すると、`details` が null 以外の場合にのみ、マークアップのこのセクションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="e6a9a-114">アプリを実行して &quot;詳細&quot; リンクのいずれかをクリックすると、アプリにブックの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e6a9a-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="e6a9a-115">[前へ](part-7.md)
> [次へ](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="e6a9a-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
