---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 複数のアニメーションの実行 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606850"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="b7013-104">複数のアニメーションを順番に実行する (VB)</span><span class="sxs-lookup"><span data-stu-id="b7013-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="b7013-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="b7013-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b7013-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b7013-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="b7013-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b7013-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b7013-108">複数のアニメーションを1つずつ実行できます。</span><span class="sxs-lookup"><span data-stu-id="b7013-108">It allows to run several animations one after the other.</span></span>

## <a name="overview"></a><span data-ttu-id="b7013-109">の概要</span><span class="sxs-lookup"><span data-stu-id="b7013-109">Overview</span></span>

<span data-ttu-id="b7013-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b7013-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b7013-111">複数のアニメーションを1つずつ実行できます。</span><span class="sxs-lookup"><span data-stu-id="b7013-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="b7013-112">手順</span><span class="sxs-lookup"><span data-stu-id="b7013-112">Steps</span></span>

<span data-ttu-id="b7013-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b7013-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="b7013-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b7013-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="b7013-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="b7013-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="b7013-116">次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="b7013-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="b7013-117">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="b7013-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="b7013-118">通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="b7013-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="b7013-119">Animation framework では、`<Sequence>` 要素を使用して複数のアニメーションを1つに結合できます。</span><span class="sxs-lookup"><span data-stu-id="b7013-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="b7013-120">`<Sequence>` 内のすべてのアニメーションが1つずつ実行されます。</span><span class="sxs-lookup"><span data-stu-id="b7013-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="b7013-121">`AnimationExtender` コントロールのマークアップを次に示します。まず、パネルの幅を広げ、その高さを小さくします。</span><span class="sxs-lookup"><span data-stu-id="b7013-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="b7013-122">このスクリプトを実行すると、最初にパネルの幅が広くなり、小さくなります。</span><span class="sxs-lookup"><span data-stu-id="b7013-122">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="b7013-123">[最初 ![幅が増加しています](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b7013-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="b7013-124">最初に幅が増加します ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b7013-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>

<span data-ttu-id="b7013-125">[![高さを下げる](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b7013-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="b7013-126">次に、高さを下げます ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b7013-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b7013-127">[前へ](executing-several-animations-at-the-same-time-vb.md)
> [次へ](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b7013-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
