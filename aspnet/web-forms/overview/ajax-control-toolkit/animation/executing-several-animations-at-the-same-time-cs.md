---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 複数のアニメーションを同時に実行するC#() |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483970"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="a76e5-104">複数のアニメーションを同時に実行するC#()</span><span class="sxs-lookup"><span data-stu-id="a76e5-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="a76e5-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="a76e5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a76e5-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a76e5-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="a76e5-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="a76e5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a76e5-108">を使用すると、複数のアニメーションを並行して実行できます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="a76e5-109">概要</span><span class="sxs-lookup"><span data-stu-id="a76e5-109">Overview</span></span>

<span data-ttu-id="a76e5-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="a76e5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a76e5-111">を使用すると、複数のアニメーションを並行して実行できます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="a76e5-112">手順</span><span class="sxs-lookup"><span data-stu-id="a76e5-112">Steps</span></span>

<span data-ttu-id="a76e5-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a76e5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="a76e5-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="a76e5-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="a76e5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="a76e5-116">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="a76e5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="a76e5-117">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="a76e5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="a76e5-118">通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="a76e5-119">Animation framework では、`<Parallel>` 要素を使用して複数のアニメーションを1つに結合できます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="a76e5-120">`<Parallel>` 内のすべてのアニメーションが同時に実行されます。</span><span class="sxs-lookup"><span data-stu-id="a76e5-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="a76e5-121">`AnimationExtender` コントロールのマークアップを次に示します。同時にパネルをフェードアウトし、サイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="a76e5-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="a76e5-122">実際には、このスクリプトを実行すると、パネルが表示され、サイズが変更され (幅が tripling、高さが半分に)、同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="a76e5-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="a76e5-123">[ブラウザーのレンダリングエンジンにより、パネルのフェードアウトとサイズ変更 (コンテンツを含む) ![](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a76e5-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="a76e5-124">パネルのフェードアウトとサイズ変更 (ブラウザーのレンダリングエンジンにより、コンテンツを含む) が表示されます ([クリックすると、フルサイズの画像が表示](executing-several-animations-at-the-same-time-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="a76e5-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a76e5-125">[前へ](adding-animation-to-a-control-cs.md)
> [次へ](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a76e5-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
