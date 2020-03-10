---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: ユーザーの操作に応答してアニメーション化する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは星型にすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497926"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="b45ca-104">ユーザー操作に対してアニメーションを返す (VB)</span><span class="sxs-lookup"><span data-stu-id="b45ca-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="b45ca-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="b45ca-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b45ca-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b45ca-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="b45ca-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b45ca-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b45ca-108">アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b45ca-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="b45ca-109">概要</span><span class="sxs-lookup"><span data-stu-id="b45ca-109">Overview</span></span>

<span data-ttu-id="b45ca-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b45ca-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b45ca-111">アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b45ca-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="b45ca-112">手順</span><span class="sxs-lookup"><span data-stu-id="b45ca-112">Steps</span></span>

<span data-ttu-id="b45ca-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b45ca-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="b45ca-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b45ca-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="b45ca-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="b45ca-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="b45ca-116">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="b45ca-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="b45ca-117">[`<Animations>`] ノードには、ユーザーの操作によってアニメーションを開始する5つの方法があります (missing 要素は、ページ全体が完全に読み込まれた後に実行される `<OnLoad>`)。</span><span class="sxs-lookup"><span data-stu-id="b45ca-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="b45ca-118">`<OnClick>` (コントロール上でマウスをクリック)</span><span class="sxs-lookup"><span data-stu-id="b45ca-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="b45ca-119">`<OnHoverOut>` (マウスをコントロールから離す)</span><span class="sxs-lookup"><span data-stu-id="b45ca-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="b45ca-120">`<OnHoverOver>` (マウスポインターをコントロールの上に置くと、`<OnHoverOut>` アニメーションが停止します)</span><span class="sxs-lookup"><span data-stu-id="b45ca-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="b45ca-121">`<OnMouseOut>` (マウスをコントロールから離す)</span><span class="sxs-lookup"><span data-stu-id="b45ca-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="b45ca-122">`<OnMouseOver>` (マウスポインターをコントロールの上に置くと、`<OnMouseOut>` アニメーションは停止しません)</span><span class="sxs-lookup"><span data-stu-id="b45ca-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="b45ca-123">このシナリオでは、`<OnClick>` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b45ca-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="b45ca-124">ユーザーがパネルをクリックすると、サイズが変更され、同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="b45ca-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="b45ca-125">[マウスクリックによってアニメーションが開始 ![](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b45ca-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="b45ca-126">マウスクリックでアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](animating-in-response-to-user-interaction-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b45ca-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b45ca-127">[前へ](picking-one-animation-out-of-a-list-vb.md)
> [次へ](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b45ca-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
