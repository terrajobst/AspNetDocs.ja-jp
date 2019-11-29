---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: リストから1つのアニメーションを選択する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 フレームワークも許可する (...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606735"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="e71e5-104">一覧からアニメーションを 1 つ選択する (VB)</span><span class="sxs-lookup"><span data-stu-id="e71e5-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="e71e5-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="e71e5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e71e5-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e71e5-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="e71e5-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="e71e5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e71e5-108">また、一部の JavaScript コードの評価に応じて、アニメーションの一覧から1つのアニメーションを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="e71e5-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="e71e5-109">の概要</span><span class="sxs-lookup"><span data-stu-id="e71e5-109">Overview</span></span>

<span data-ttu-id="e71e5-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="e71e5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e71e5-111">また、一部の JavaScript コードの評価に応じて、アニメーションの一覧から1つのアニメーションを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="e71e5-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="e71e5-112">手順</span><span class="sxs-lookup"><span data-stu-id="e71e5-112">Steps</span></span>

<span data-ttu-id="e71e5-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="e71e5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="e71e5-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="e71e5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="e71e5-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="e71e5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="e71e5-116">次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="e71e5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="e71e5-117">ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="e71e5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="e71e5-118">通常のアニメーションのいずれかではなく、`<Case>` 要素が再生されます。</span><span class="sxs-lookup"><span data-stu-id="e71e5-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="e71e5-119">SelectScript 属性の値が評価されます。戻り値は数値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e71e5-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="e71e5-120">この数値に応じて、&lt;Case&gt; 内のいずれかのサブアニメーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="e71e5-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="e71e5-121">たとえば、SelectScript が2に評価される場合、Control Toolkit は &lt;ケース&gt; 内で3番目のアニメーションを実行します (カウントは0から始まります)。</span><span class="sxs-lookup"><span data-stu-id="e71e5-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="e71e5-122">次のマークアップは、3つのサブアニメーションを定義します。幅の変更、高さのサイズ変更、およびフェードアウトです。次に、JavaScript コード (`Math.floor(3 * Math.random())`) が 0 ~ 2 の範囲の数値を選択して、3つのアニメーションのいずれかが実行されるようにします。</span><span class="sxs-lookup"><span data-stu-id="e71e5-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

<span data-ttu-id="e71e5-123">[使用可能な3つのアニメーションのいずれかを ![します。パネルの幅が広くなります。](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e71e5-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="e71e5-124">使用可能な3つのアニメーションのいずれか: パネルの幅が広くなります ([クリックすると、フルサイズの画像が表示](picking-one-animation-out-of-a-list-vb/_static/image3.png)されます)。</span><span class="sxs-lookup"><span data-stu-id="e71e5-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e71e5-125">[前へ](animation-depending-on-a-condition-vb.md)
> [次へ](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e71e5-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
