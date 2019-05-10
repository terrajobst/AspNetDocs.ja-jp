---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: スライダー コントロールを使用する (VB) の自動ポストバックあり |Microsoft Docs
author: wenz
description: スライダー コントロール、AJAX Control Toolkit では、マウスを使用して制御できるグラフィカルなスライダーを提供します。 スライダー自動転記を作成することはしています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: c4ee6642726b4209d09907f615ee3286ca00caa3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124620"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="ae1ab-104">スライダー コントロールを使用する (VB) の自動ポストバックあり</span><span class="sxs-lookup"><span data-stu-id="ae1ab-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="ae1ab-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ae1ab-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ae1ab-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ae1ab-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="ae1ab-107">スライダー コントロール、AJAX Control Toolkit では、マウスを使用して制御できるグラフィカルなスライダーを提供します。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="ae1ab-108">ようにスライダー autopostback 1 回、値が変化することになります。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="ae1ab-109">概要</span><span class="sxs-lookup"><span data-stu-id="ae1ab-109">Overview</span></span>

<span data-ttu-id="ae1ab-110">スライダー コントロール、AJAX Control Toolkit では、マウスを使用して制御できるグラフィカルなスライダーを提供します。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="ae1ab-111">ようにスライダー autopostback 1 回、値が変化することになります。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="ae1ab-112">手順</span><span class="sxs-lookup"><span data-stu-id="ae1ab-112">Steps</span></span>

<span data-ttu-id="ae1ab-113">両方のテキスト ボックス、スライダーを変更すると自動的にポストバックするには、するには、属性が必要な`AutoPostBack="true"`:テキスト ボックス自体には、スライダーになると、テキスト ボックス、スライダーの位置を保持します。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="ae1ab-114">そのための必要なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="ae1ab-115">`SliderExtender` ASP.NET AJAX Control toolkit コントロールが 2 つのテキスト ボックスに、スライダーの機能を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="ae1ab-116">追加のラベル要素が、ポストバックのユーザーに通知するために後で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="ae1ab-117">最後に、 `ScriptManager` ASP.NET AJAX のコントロールが動作する Control Toolkit の必要な JavaScript を読み込みます。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="ae1ab-118">これで、スライダーがポスト バック;サーバー側で、このイベントをキャッチして処理して可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="ae1ab-119">[![ポストバックをトリガーするスライダーの移動](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ae1ab-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="ae1ab-120">ポストバックをトリガーするスライダーの移動 ([フルサイズの画像を表示する をクリックします](using-the-slider-control-with-auto-postback-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="ae1ab-121">[![その後、この変更の日付は、ラベルに書き込まれます](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ae1ab-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="ae1ab-122">その後、この変更の日付は、ラベルに書き込まれます ([フルサイズの画像を表示する をクリックします](using-the-slider-control-with-auto-postback-vb/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="ae1ab-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ae1ab-123">[前へ](databinding-the-slider-control-cs.md)
> [次へ](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ae1ab-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
