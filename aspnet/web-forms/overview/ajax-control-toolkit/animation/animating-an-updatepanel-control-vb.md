---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel コントロールのアニメーション化 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 ... の内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607072"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="3b8fb-104">UpdatePanel コントロールをアニメーションにする (VB)</span><span class="sxs-lookup"><span data-stu-id="3b8fb-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="3b8fb-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="3b8fb-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3b8fb-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3b8fb-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="3b8fb-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3b8fb-108">UpdatePanel の内容については、animation framework: Updateパネルアニメーションに大きく依存する特別な extender が存在します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="3b8fb-109">このチュートリアルでは、このようなアニメーションを UpdatePanel に設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="3b8fb-110">の概要</span><span class="sxs-lookup"><span data-stu-id="3b8fb-110">Overview</span></span>

<span data-ttu-id="3b8fb-111">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="3b8fb-112">`UpdatePanel`の内容については、`UpdatePanelAnimation`のアニメーションフレームワークに大きく依存する特別な extender が存在します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="3b8fb-113">このチュートリアルでは、このようなアニメーションを `UpdatePanel`に設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="3b8fb-114">手順</span><span class="sxs-lookup"><span data-stu-id="3b8fb-114">Steps</span></span>

<span data-ttu-id="3b8fb-115">最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="3b8fb-116">このシナリオのアニメーションは、`UpdatePanel`に存在する ASP.NET `Wizard` web コントロールに適用されます。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="3b8fb-117">ポストバックをトリガーするためのオプションは、3つ (任意) の手順で指定します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="3b8fb-118">`UpdatePanelAnimationExtender` コントロールに必要なマークアップは、`AnimationExtender`に使用されるマークアップと非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="3b8fb-119">`TargetControlID` 属性では、アニメーション化する `UpdatePanel` の `ID` を指定します。`UpdatePanelAnimationExtender` コントロール内では、`<Animations>` 要素は、アニメーションの XML マークアップを保持します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="3b8fb-120">ただし、1つの違いがあります。 `AnimationExtender`と比較すると、イベントとイベントハンドラーの量が制限されます。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="3b8fb-121">`UpdatePanels`には、次の2つのみが存在します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="3b8fb-122">UpdatePanel が更新されたときの `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="3b8fb-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="3b8fb-123">UpdatePanel が更新を開始するときに `<OnUpdating>` します。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="3b8fb-124">このシナリオでは、(ポストバック後に) `UpdatePanel` の新しい内容がフェードインされます。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="3b8fb-125">これは、そのために必要なマークアップです。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="3b8fb-126">これで、UpdatePanel 内でポストバックが発生するたびに、パネルの新しいコンテンツがスムーズにフェードインされます。</span><span class="sxs-lookup"><span data-stu-id="3b8fb-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="3b8fb-127">[次のウィザードのステップがフェードイン ![](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3b8fb-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="3b8fb-128">次のウィザードステップはフェードインします ([クリックすると、フルサイズの画像が表示](animating-an-updatepanel-control-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="3b8fb-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3b8fb-129">[前へ](changing-an-animation-using-client-side-code-vb.md)
> [次へ](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3b8fb-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
