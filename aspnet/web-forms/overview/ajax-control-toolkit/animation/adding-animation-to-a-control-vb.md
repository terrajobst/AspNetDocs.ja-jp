---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: コントロールへのアニメーションの追加 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 このチュートリアルでは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484126"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="7abd2-104">コントロールにアニメーションを追加する (VB)</span><span class="sxs-lookup"><span data-stu-id="7abd2-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="7abd2-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="7abd2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7abd2-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7abd2-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="7abd2-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="7abd2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7abd2-108">このチュートリアルでは、このようなアニメーションを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7abd2-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="7abd2-109">概要</span><span class="sxs-lookup"><span data-stu-id="7abd2-109">Overview</span></span>

<span data-ttu-id="7abd2-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="7abd2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7abd2-111">このチュートリアルでは、このようなアニメーションを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7abd2-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="7abd2-112">手順</span><span class="sxs-lookup"><span data-stu-id="7abd2-112">Steps</span></span>

<span data-ttu-id="7abd2-113">最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。</span><span class="sxs-lookup"><span data-stu-id="7abd2-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="7abd2-114">このシナリオのアニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="7abd2-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="7abd2-115">パネルに関連付けられている CSS クラスは、背景色と幅を定義します。</span><span class="sxs-lookup"><span data-stu-id="7abd2-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="7abd2-116">次に、`AnimationExtender`が必要です。</span><span class="sxs-lookup"><span data-stu-id="7abd2-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="7abd2-117">`ID` と通常の `runat="server"`を指定した後、`TargetControlID` 属性をコントロールに設定して、アニメーション化するには、パネルで次のようにします。</span><span class="sxs-lookup"><span data-stu-id="7abd2-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="7abd2-118">アニメーション全体は XML 構文を使用して宣言によって適用されますが、現時点では Visual Studio の IntelliSense で完全にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="7abd2-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="7abd2-119">ルートノードがこのノード内に `<Animations>;`、次のようないくつかのイベントが許可されます。これにより、アニメーションの実行時間が決まります。</span><span class="sxs-lookup"><span data-stu-id="7abd2-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="7abd2-120">`OnClick` (マウスクリック)</span><span class="sxs-lookup"><span data-stu-id="7abd2-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="7abd2-121">`OnHoverOut` (マウスをコントロールから離したとき)</span><span class="sxs-lookup"><span data-stu-id="7abd2-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="7abd2-122">`OnHoverOver` (マウスポインターをコントロールの上に置くと、`OnHoverOut` アニメーションが停止します)</span><span class="sxs-lookup"><span data-stu-id="7abd2-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="7abd2-123">`OnLoad` (ページが読み込まれたとき)</span><span class="sxs-lookup"><span data-stu-id="7abd2-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="7abd2-124">`OnMouseOut` (マウスをコントロールから離したとき)</span><span class="sxs-lookup"><span data-stu-id="7abd2-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="7abd2-125">`OnMouseOver` (マウスポインターをコントロールの上に置くと、`OnMouseOut` アニメーションは停止しません)</span><span class="sxs-lookup"><span data-stu-id="7abd2-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="7abd2-126">フレームワークには一連のアニメーションが用意されており、それぞれが独自の XML 要素で表されます。</span><span class="sxs-lookup"><span data-stu-id="7abd2-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="7abd2-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7abd2-127">Here is a selection:</span></span>

- <span data-ttu-id="7abd2-128">`<Color>` (色の変更)</span><span class="sxs-lookup"><span data-stu-id="7abd2-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="7abd2-129">`<FadeIn>` (フェードイン)</span><span class="sxs-lookup"><span data-stu-id="7abd2-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="7abd2-130">`<FadeOut>` (フェードアウト)</span><span class="sxs-lookup"><span data-stu-id="7abd2-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="7abd2-131">`<Property>` (コントロールのプロパティを変更する)</span><span class="sxs-lookup"><span data-stu-id="7abd2-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="7abd2-132">`<Pulse>` (アウト)</span><span class="sxs-lookup"><span data-stu-id="7abd2-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="7abd2-133">`<Resize>` (サイズの変更)</span><span class="sxs-lookup"><span data-stu-id="7abd2-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="7abd2-134">`<Scale>` (サイズの変更に比例)</span><span class="sxs-lookup"><span data-stu-id="7abd2-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="7abd2-135">この例では、パネルはフェードアウトします。アニメーションには1.5 秒 (`Duration` 属性) が必要で、1秒あたり24フレーム (アニメーションステップ) が表示されます (`Fps` 属性)。</span><span class="sxs-lookup"><span data-stu-id="7abd2-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="7abd2-136">`AnimationExtender` コントロールの完全なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7abd2-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="7abd2-137">このスクリプトを実行すると、パネルが表示され、1秒と30秒でフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="7abd2-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="7abd2-138">[パネルがフェードアウト ![](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7abd2-138">[![The panel is fading out](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="7abd2-139">パネルがフェードアウトします ([クリックすると、フルサイズの画像が表示](adding-animation-to-a-control-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7abd2-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7abd2-140">[前へ](dynamically-controlling-updatepanel-animations-cs.md)
> [次へ](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7abd2-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
