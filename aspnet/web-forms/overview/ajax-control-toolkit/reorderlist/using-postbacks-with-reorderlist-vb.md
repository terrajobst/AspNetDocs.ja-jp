---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: ReorderList でポストバックを使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。 リストが並べ替えられるたびに、po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445930"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="f3655-104">ReorderList でポストバックを使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="f3655-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="f3655-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="f3655-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f3655-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f3655-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="f3655-107">AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。</span><span class="sxs-lookup"><span data-stu-id="f3655-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f3655-108">リストが並べ替えられるたびに、ポストバックはサーバーに変更を通知します。</span><span class="sxs-lookup"><span data-stu-id="f3655-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="f3655-109">概要</span><span class="sxs-lookup"><span data-stu-id="f3655-109">Overview</span></span>

<span data-ttu-id="f3655-110">AJAX コントロールツールキットの `ReorderList` コントロールには、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストが用意されています。</span><span class="sxs-lookup"><span data-stu-id="f3655-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f3655-111">リストが並べ替えられるたびに、ポストバックはサーバーに変更を通知します。</span><span class="sxs-lookup"><span data-stu-id="f3655-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="f3655-112">手順</span><span class="sxs-lookup"><span data-stu-id="f3655-112">Steps</span></span>

<span data-ttu-id="f3655-113">`ReorderList` コントロールには、いくつかのデータソースが考えられます。</span><span class="sxs-lookup"><span data-stu-id="f3655-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="f3655-114">1つは、`XmlDataSource` コントロールを使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="f3655-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="f3655-115">この XML を `ReorderList` コントロールにバインドし、ポストバックを有効にするには、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3655-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="f3655-116">`DataSourceID`: データソースの ID</span><span class="sxs-lookup"><span data-stu-id="f3655-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="f3655-117">`SortOrderField`: 並べ替えの基準となるプロパティ</span><span class="sxs-lookup"><span data-stu-id="f3655-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="f3655-118">`AllowReorder`: ユーザーがリスト要素の順序を変更できるようにするかどうか</span><span class="sxs-lookup"><span data-stu-id="f3655-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="f3655-119">`PostBackOnReorder`: リストを再配置するたびにポストバックを作成するかどうか</span><span class="sxs-lookup"><span data-stu-id="f3655-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="f3655-120">次に、コントロールの適切なマークアップを示します。</span><span class="sxs-lookup"><span data-stu-id="f3655-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="f3655-121">`ReorderList` コントロール内では、`Eval()` メソッドを使用してデータソースの特定のデータをバインドできます。</span><span class="sxs-lookup"><span data-stu-id="f3655-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="f3655-122">ページ上の任意の位置で、最後の並べ替えが行われたときにラベルに情報が保持されます。</span><span class="sxs-lookup"><span data-stu-id="f3655-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="f3655-123">このラベルには、ポストバックを処理するサーバー側コードのテキストが格納されます。</span><span class="sxs-lookup"><span data-stu-id="f3655-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="f3655-124">最後に、ASP.NET AJAX と Control `ScriptManager` Toolkit の機能をアクティブ化するために、ページにコントロールを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3655-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

<span data-ttu-id="f3655-125">[各並べ替えの ![ポストバックをトリガーする](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f3655-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="f3655-126">各並べ替え順序によってポストバックがトリガーされる ([クリックすると、フルサイズの画像が表示](using-postbacks-with-reorderlist-vb/_static/image3.png)される)</span><span class="sxs-lookup"><span data-stu-id="f3655-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3655-127">[前へ](drag-and-drop-via-reorderlist-cs.md)
> [次へ](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f3655-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
