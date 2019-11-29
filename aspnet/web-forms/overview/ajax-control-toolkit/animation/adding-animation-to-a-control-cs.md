---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: コントロールへのアニメーションの追加C#() |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 このチュートリアルでは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607110"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="e80ab-104">コントロールにアニメーションを追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="e80ab-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="e80ab-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="e80ab-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e80ab-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e80ab-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="e80ab-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="e80ab-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e80ab-108">このチュートリアルでは、このようなアニメーションを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e80ab-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="e80ab-109">の概要</span><span class="sxs-lookup"><span data-stu-id="e80ab-109">Overview</span></span>

<span data-ttu-id="e80ab-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="e80ab-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e80ab-111">このチュートリアルでは、このようなアニメーションを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e80ab-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="e80ab-112">手順</span><span class="sxs-lookup"><span data-stu-id="e80ab-112">Steps</span></span>

<span data-ttu-id="e80ab-113">最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。</span><span class="sxs-lookup"><span data-stu-id="e80ab-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="e80ab-114">このシナリオのアニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="e80ab-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="e80ab-115">パネルに関連付けられている CSS クラスは、背景色と幅を定義します。</span><span class="sxs-lookup"><span data-stu-id="e80ab-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="e80ab-116">次に、`AnimationExtender`が必要です。</span><span class="sxs-lookup"><span data-stu-id="e80ab-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="e80ab-117">`ID` と通常の `runat="server"`を指定した後、`TargetControlID` 属性をコントロールに設定して、アニメーション化するには、パネルで次のようにします。</span><span class="sxs-lookup"><span data-stu-id="e80ab-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="e80ab-118">アニメーション全体は XML 構文を使用して宣言によって適用されますが、現時点では Visual Studio の IntelliSense で完全にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="e80ab-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="e80ab-119">ルートノードがこのノード内に `<Animations>;`、次のようないくつかのイベントが許可されます。これにより、アニメーションの実行時間が決まります。</span><span class="sxs-lookup"><span data-stu-id="e80ab-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="e80ab-120">`OnClick` (マウスクリック)</span><span class="sxs-lookup"><span data-stu-id="e80ab-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="e80ab-121">`OnHoverOut` (マウスをコントロールから離したとき)</span><span class="sxs-lookup"><span data-stu-id="e80ab-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="e80ab-122">`OnHoverOver` (マウスポインターをコントロールの上に置くと、`OnHoverOut` アニメーションが停止します)</span><span class="sxs-lookup"><span data-stu-id="e80ab-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="e80ab-123">`OnLoad` (ページが読み込まれたとき)</span><span class="sxs-lookup"><span data-stu-id="e80ab-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="e80ab-124">`OnMouseOut` (マウスをコントロールから離したとき)</span><span class="sxs-lookup"><span data-stu-id="e80ab-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="e80ab-125">`OnMouseOver` (マウスポインターをコントロールの上に置くと、`OnMouseOut` アニメーションは停止しません)</span><span class="sxs-lookup"><span data-stu-id="e80ab-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="e80ab-126">フレームワークには一連のアニメーションが用意されており、それぞれが独自の XML 要素で表されます。</span><span class="sxs-lookup"><span data-stu-id="e80ab-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="e80ab-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="e80ab-127">Here is a selection:</span></span>

- <span data-ttu-id="e80ab-128">`<Color>` (色の変更)</span><span class="sxs-lookup"><span data-stu-id="e80ab-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="e80ab-129">`<FadeIn>` (フェードイン)</span><span class="sxs-lookup"><span data-stu-id="e80ab-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="e80ab-130">`<FadeOut>` (フェードアウト)</span><span class="sxs-lookup"><span data-stu-id="e80ab-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="e80ab-131">`<Property>` (コントロールのプロパティを変更する)</span><span class="sxs-lookup"><span data-stu-id="e80ab-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="e80ab-132">`<Pulse>` (アウト)</span><span class="sxs-lookup"><span data-stu-id="e80ab-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="e80ab-133">`<Resize>` (サイズの変更)</span><span class="sxs-lookup"><span data-stu-id="e80ab-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="e80ab-134">`<Scale>` (サイズの変更に比例)</span><span class="sxs-lookup"><span data-stu-id="e80ab-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="e80ab-135">この例では、パネルはフェードアウトします。アニメーションには1.5 秒 (`Duration` 属性) が必要で、1秒あたり24フレーム (アニメーションステップ) が表示されます (`Fps` 属性)。</span><span class="sxs-lookup"><span data-stu-id="e80ab-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="e80ab-136">`AnimationExtender` コントロールの完全なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e80ab-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="e80ab-137">このスクリプトを実行すると、パネルが表示され、1秒と30秒でフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="e80ab-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="e80ab-138">[パネルがフェードアウト ![](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e80ab-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="e80ab-139">パネルがフェードアウトします ([クリックすると、フルサイズの画像が表示](adding-animation-to-a-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="e80ab-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e80ab-140">次へ</span><span class="sxs-lookup"><span data-stu-id="e80ab-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
