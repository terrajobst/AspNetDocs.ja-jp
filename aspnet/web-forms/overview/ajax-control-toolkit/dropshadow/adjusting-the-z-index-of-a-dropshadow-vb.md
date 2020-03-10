---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: DropShadow の Z インデックスの調整 (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 ただし、この影は、他のコントロールと競合することがあります。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497512"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="ccddd-104">DropShadow の Z インデックスを調整する (VB)</span><span class="sxs-lookup"><span data-stu-id="ccddd-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>

<span data-ttu-id="ccddd-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="ccddd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ccddd-106">[コードのダウンロード](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ccddd-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="ccddd-107">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="ccddd-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="ccddd-108">ただし、この影は、ASP.NET Menu コントロールなど、他のコントロールと競合することがあります。</span><span class="sxs-lookup"><span data-stu-id="ccddd-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="ccddd-109">メニューエントリがポップアップ表示されると、ドロップシャドウの背後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ccddd-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="ccddd-110">概要</span><span class="sxs-lookup"><span data-stu-id="ccddd-110">Overview</span></span>

<span data-ttu-id="ccddd-111">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="ccddd-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="ccddd-112">ただし、この影は、ASP.NET Menu コントロールなど、他のコントロールと競合することがあります。</span><span class="sxs-lookup"><span data-stu-id="ccddd-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="ccddd-113">メニューエントリがポップアップ表示されると、ドロップシャドウの背後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ccddd-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="ccddd-114">手順</span><span class="sxs-lookup"><span data-stu-id="ccddd-114">Steps</span></span>

<span data-ttu-id="ccddd-115">コードはパネル自体で開始されます。これにより、パネルには、効果を表示するのに十分なテキストが含まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="ccddd-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="ccddd-116">`panelShadow` パネルの直前に別のパネルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="ccddd-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="ccddd-117">メニュー項目が [`dropShadow`] パネルの上 (または下) に表示されるように、横方向のメニューが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccddd-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="ccddd-118">次に、`DropShadowExtender` を追加して、ドロップシャドウ効果を持つ `panelShadow` パネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="ccddd-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="ccddd-119">最後に、ASP.NET AJAX `ScriptManager` コントロールを使用して、コントロールツールキットを機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="ccddd-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="ccddd-120">このスクリプトを実行すると、メニューエントリがパネルの下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ccddd-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="ccddd-121">ただし、メニューでは CSS クラス `panel` を使用します。ここでは、要素を他のパネルの前面に表示するために、次の2つの項目を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccddd-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="ccddd-122">相対配置</span><span class="sxs-lookup"><span data-stu-id="ccddd-122">Relative positioning</span></span>
- <span data-ttu-id="ccddd-123">正の z インデックス</span><span class="sxs-lookup"><span data-stu-id="ccddd-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="ccddd-124">その後、`DropShadowExtender` コントロールがメニューコントロールと競合しないようになります。</span><span class="sxs-lookup"><span data-stu-id="ccddd-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="ccddd-125">[![の前: メニューエントリは表示されません](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ccddd-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span></span>

<span data-ttu-id="ccddd-126">[前]: メニューエントリは表示されません ([クリックすると、フルサイズの画像が表示](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ccddd-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>

<span data-ttu-id="ccddd-127">[![後: メニュー項目が表示されます。](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ccddd-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span></span>

<span data-ttu-id="ccddd-128">[完了]: メニューエントリが表示されます ([クリックすると、フルサイズの画像が表示](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ccddd-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ccddd-129">[前へ](manipulating-dropshadow-properties-from-client-code-cs.md)
> [次へ](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ccddd-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
