---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 条件に応じたアニメーション (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの有無
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484168"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="6ad19-104">条件に基づくアニメーション (C#)</span><span class="sxs-lookup"><span data-stu-id="6ad19-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="6ad19-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="6ad19-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6ad19-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6ad19-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="6ad19-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="6ad19-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6ad19-108">アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="6ad19-109">概要</span><span class="sxs-lookup"><span data-stu-id="6ad19-109">Overview</span></span>

<span data-ttu-id="6ad19-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="6ad19-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6ad19-111">アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="6ad19-112">手順</span><span class="sxs-lookup"><span data-stu-id="6ad19-112">Steps</span></span>

<span data-ttu-id="6ad19-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="6ad19-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="6ad19-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="6ad19-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="6ad19-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="6ad19-116">次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="6ad19-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="6ad19-117">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="6ad19-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="6ad19-118">通常のアニメーションのいずれかではなく、`<Condition>` 要素が再生されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="6ad19-119">`ConditionScript` 属性の値として指定された JavaScript コードは、実行時に実行されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="6ad19-120">True と評価された場合、アニメーションは実行されます。それ以外の場合は実行されません。</span><span class="sxs-lookup"><span data-stu-id="6ad19-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="6ad19-121">次のマークアップは、2つのアニメーションを提供します。それぞれのアニメーションは、ランダムに50% のケースで実行されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="6ad19-122">`<OnLoad>`内には1つのアニメーションしか存在しないため、2つの `<Condition>` アニメーションは `<Sequence>` 要素を使用して結合されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="6ad19-123">`ConditionScript` 属性の不等号 (`<`) をエスケープする () 必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6ad19-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="6ad19-124">このスクリプトを実行すると、アニメーションは実行されず、どちらか一方または両方が実行されます。</span><span class="sxs-lookup"><span data-stu-id="6ad19-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="6ad19-125">[パネルのサイズを変更せずにフェードアウトする ![、2番目のアニメーションが実行されます。最初のアニメーションは実行されませんでした。](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6ad19-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="6ad19-126">パネルはサイズ変更せずにフェードアウトします。そのため、2番目のアニメーションを実行します ([クリックすると、フルサイズの画像が表示](animation-depending-on-a-condition-cs/_static/image3.png)されます)。</span><span class="sxs-lookup"><span data-stu-id="6ad19-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6ad19-127">[前へ](executing-several-animations-after-each-other-cs.md)
> [次へ](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6ad19-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
