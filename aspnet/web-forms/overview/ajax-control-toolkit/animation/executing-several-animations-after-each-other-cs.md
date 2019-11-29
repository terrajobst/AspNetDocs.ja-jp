---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 複数のアニメーションを相互に実行C#する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575425"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="8ad41-104">複数のアニメーションを順番に実行する (C#)</span><span class="sxs-lookup"><span data-stu-id="8ad41-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="8ad41-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="8ad41-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8ad41-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8ad41-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="8ad41-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="8ad41-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8ad41-108">複数のアニメーションを1つずつ実行できます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-108">It allows to run several animations one after the other.</span></span>

<span data-ttu-id="8ad41-109">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="8ad41-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8ad41-110">複数のアニメーションを1つずつ実行できます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="8ad41-111">手順</span><span class="sxs-lookup"><span data-stu-id="8ad41-111">Steps</span></span>

<span data-ttu-id="8ad41-112">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="8ad41-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="8ad41-113">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="8ad41-114">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="8ad41-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="8ad41-115">次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="8ad41-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="8ad41-116">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8ad41-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="8ad41-117">通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="8ad41-118">Animation framework では、`<Sequence>` 要素を使用して複数のアニメーションを1つに結合できます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="8ad41-119">`<Sequence>` 内のすべてのアニメーションが1つずつ実行されます。</span><span class="sxs-lookup"><span data-stu-id="8ad41-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="8ad41-120">`AnimationExtender` コントロールのマークアップを次に示します。まず、パネルの幅を広げ、その高さを小さくします。</span><span class="sxs-lookup"><span data-stu-id="8ad41-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="8ad41-121">このスクリプトを実行すると、最初にパネルの幅が広くなり、小さくなります。</span><span class="sxs-lookup"><span data-stu-id="8ad41-121">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="8ad41-122">[最初 ![幅が増加しています](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8ad41-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="8ad41-123">最初に幅が増加します ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="8ad41-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>

<span data-ttu-id="8ad41-124">[![高さを下げる](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8ad41-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="8ad41-125">次に、高さを下げます ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="8ad41-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8ad41-126">[前へ](executing-several-animations-at-the-same-time-cs.md)
> [次へ](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8ad41-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
