---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: ユーザーの操作に応答してC#アニメーション化する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは星型にすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497902"
---
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="84801-104">ユーザー操作に対してアニメーションを返す (C#)</span><span class="sxs-lookup"><span data-stu-id="84801-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="84801-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="84801-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="84801-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="84801-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="84801-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="84801-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84801-108">アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。</span><span class="sxs-lookup"><span data-stu-id="84801-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="84801-109">概要</span><span class="sxs-lookup"><span data-stu-id="84801-109">Overview</span></span>

<span data-ttu-id="84801-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="84801-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84801-111">アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。</span><span class="sxs-lookup"><span data-stu-id="84801-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="84801-112">手順</span><span class="sxs-lookup"><span data-stu-id="84801-112">Steps</span></span>

<span data-ttu-id="84801-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="84801-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="84801-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="84801-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="84801-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="84801-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="84801-116">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="84801-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="84801-117">[`<Animations>`] ノードには、ユーザーの操作によってアニメーションを開始する5つの方法があります (missing 要素は、ページ全体が完全に読み込まれた後に実行される `<OnLoad>`)。</span><span class="sxs-lookup"><span data-stu-id="84801-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="84801-118">`<OnClick>` (コントロール上でマウスをクリック)</span><span class="sxs-lookup"><span data-stu-id="84801-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="84801-119">`<OnHoverOut>` (マウスをコントロールから離す)</span><span class="sxs-lookup"><span data-stu-id="84801-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="84801-120">`<OnHoverOver>` (マウスポインターをコントロールの上に置くと、`<OnHoverOut>` アニメーションが停止します)</span><span class="sxs-lookup"><span data-stu-id="84801-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="84801-121">`<OnMouseOut>` (マウスをコントロールから離す)</span><span class="sxs-lookup"><span data-stu-id="84801-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="84801-122">`<OnMouseOver>` (マウスポインターをコントロールの上に置くと、`<OnMouseOut>` アニメーションは停止しません)</span><span class="sxs-lookup"><span data-stu-id="84801-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="84801-123">このシナリオでは、`<OnClick>` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="84801-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="84801-124">ユーザーがパネルをクリックすると、サイズが変更され、同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="84801-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="84801-125">[マウスクリックによってアニメーションが開始 ![](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="84801-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="84801-126">マウスクリックでアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](animating-in-response-to-user-interaction-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="84801-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84801-127">[前へ](picking-one-animation-out-of-a-list-cs.md)
> [次へ](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="84801-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
