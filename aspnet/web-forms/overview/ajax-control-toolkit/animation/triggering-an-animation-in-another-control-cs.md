---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: 別のコントロールでアニメーションをトリガーC#する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 一般に、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599634"
---
# <a name="triggering-an-animation-in-another-control-c"></a><span data-ttu-id="13c9b-104">別のコントロールでアニメーションをトリガーする (C#)</span><span class="sxs-lookup"><span data-stu-id="13c9b-104">Triggering an Animation in another Control (C#)</span></span>

<span data-ttu-id="13c9b-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="13c9b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="13c9b-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="13c9b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span></span>

> <span data-ttu-id="13c9b-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="13c9b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="13c9b-108">通常、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="13c9b-109">ただし、1つのコントロールと対話し、別のコントロールをアニメーションすることもできます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="13c9b-110">の概要</span><span class="sxs-lookup"><span data-stu-id="13c9b-110">Overview</span></span>

<span data-ttu-id="13c9b-111">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="13c9b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="13c9b-112">通常、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="13c9b-113">ただし、1つのコントロールと対話し、別のコントロールをアニメーションすることもできます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="13c9b-114">手順</span><span class="sxs-lookup"><span data-stu-id="13c9b-114">Steps</span></span>

<span data-ttu-id="13c9b-115">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="13c9b-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

<span data-ttu-id="13c9b-116">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

<span data-ttu-id="13c9b-117">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="13c9b-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

<span data-ttu-id="13c9b-118">パネルのアニメーション化を開始するために、HTML ボタンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="13c9b-119">`<input type="button" />` は、ユーザーがボタンをクリックしたときにポストバックが不要になるため、`<asp:Button />` で favoured されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="13c9b-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

<span data-ttu-id="13c9b-120">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="13c9b-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="13c9b-121">`TargetControlID` を、パネルの ID (アニメーション化する要素) ではなく、ボタンの ID (アニメーションをトリガーする要素) に設定することが重要です。</span><span class="sxs-lookup"><span data-stu-id="13c9b-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

<span data-ttu-id="13c9b-122">[`<Animations>`] ノード内で、アニメーションを通常どおりに配置します。</span><span class="sxs-lookup"><span data-stu-id="13c9b-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="13c9b-123">ボタンではなくパネルを変更するには、`AnimationExtender`内のすべてのアニメーション要素の `AnimationTarget` 属性を設定します。</span><span class="sxs-lookup"><span data-stu-id="13c9b-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="13c9b-124">`AnimationTarget` の値は、もちろん、パネルの ID です。</span><span class="sxs-lookup"><span data-stu-id="13c9b-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="13c9b-125">これにより、アニメーションは、[トリガー] ボタンではなく、パネルで行われます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="13c9b-126">このシナリオの `AnimationExtender` マークアップは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="13c9b-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

<span data-ttu-id="13c9b-127">個々のアニメーションが表示される特別な順序に注意してください。</span><span class="sxs-lookup"><span data-stu-id="13c9b-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="13c9b-128">まず、アニメーションを実行すると、ボタンが非アクティブになります。</span><span class="sxs-lookup"><span data-stu-id="13c9b-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="13c9b-129">`<EnableAction>` 要素には `AnimationTarget` 属性がないため、このアニメーションは元のコントロール (ボタン) に適用されます。</span><span class="sxs-lookup"><span data-stu-id="13c9b-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="13c9b-130">次の2つのアニメーションの手順は、並列 (`<Parallel>` 要素) で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="13c9b-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="13c9b-131">どちらの `AnimationTarget` 属性も `"Panel1"`に設定されているので、ボタンではなくパネルをアニメーション化します。</span><span class="sxs-lookup"><span data-stu-id="13c9b-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="13c9b-132">[ボタンをクリックする ![、パネルアニメーションが開始されます。](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="13c9b-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="13c9b-133">ボタンをクリックするとパネルアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](triggering-an-animation-in-another-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="13c9b-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="13c9b-134">[前へ](disabling-actions-during-animation-cs.md)
> [次へ](modifying-animations-from-the-server-side-cs.md)</span><span class="sxs-lookup"><span data-stu-id="13c9b-134">[Previous](disabling-actions-during-animation-cs.md)
[Next](modifying-animations-from-the-server-side-cs.md)</span></span>
