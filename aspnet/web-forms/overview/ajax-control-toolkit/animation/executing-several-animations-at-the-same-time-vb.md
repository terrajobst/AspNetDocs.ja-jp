---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 複数のアニメーションを同時に実行する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497800"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="5a4fa-104">複数のアニメーションを同時に実行する (VB)</span><span class="sxs-lookup"><span data-stu-id="5a4fa-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="5a4fa-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="5a4fa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5a4fa-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5a4fa-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="5a4fa-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5a4fa-108">を使用すると、複数のアニメーションを並行して実行できます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="5a4fa-109">概要</span><span class="sxs-lookup"><span data-stu-id="5a4fa-109">Overview</span></span>

<span data-ttu-id="5a4fa-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5a4fa-111">を使用すると、複数のアニメーションを並行して実行できます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="5a4fa-112">手順</span><span class="sxs-lookup"><span data-stu-id="5a4fa-112">Steps</span></span>

<span data-ttu-id="5a4fa-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="5a4fa-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="5a4fa-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="5a4fa-116">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="5a4fa-117">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="5a4fa-118">通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="5a4fa-119">Animation framework では、`<Parallel>` 要素を使用して複数のアニメーションを1つに結合できます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="5a4fa-120">`<Parallel>` 内のすべてのアニメーションが同時に実行されます。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="5a4fa-121">`AnimationExtender` コントロールのマークアップを次に示します。同時にパネルをフェードアウトし、サイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="5a4fa-122">実際には、このスクリプトを実行すると、パネルが表示され、サイズが変更され (幅が tripling、高さが半分に)、同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="5a4fa-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="5a4fa-123">[ブラウザーのレンダリングエンジンにより、パネルのフェードアウトとサイズ変更 (コンテンツを含む) ![](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a4fa-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="5a4fa-124">パネルのフェードアウトとサイズ変更 (ブラウザーのレンダリングエンジンにより、コンテンツを含む) が表示されます ([クリックすると、フルサイズの画像が表示](executing-several-animations-at-the-same-time-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="5a4fa-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5a4fa-125">[前へ](adding-animation-to-a-control-vb.md)
> [次へ](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5a4fa-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
