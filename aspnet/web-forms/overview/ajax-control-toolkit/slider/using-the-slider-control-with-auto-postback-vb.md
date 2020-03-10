---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 自動ポストバックと共にスライダーコントロールを使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーを自動投稿することができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445780"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="52633-104">スライダーコントロールを自動ポストバックと共に使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="52633-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="52633-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="52633-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="52633-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="52633-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="52633-107">AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="52633-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="52633-108">スライダーの値が変更されたときに、そのスライダーを autopostback にすることができます。</span><span class="sxs-lookup"><span data-stu-id="52633-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="52633-109">概要</span><span class="sxs-lookup"><span data-stu-id="52633-109">Overview</span></span>

<span data-ttu-id="52633-110">AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="52633-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="52633-111">スライダーの値が変更されたときに、そのスライダーを autopostback にすることができます。</span><span class="sxs-lookup"><span data-stu-id="52633-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="52633-112">手順</span><span class="sxs-lookup"><span data-stu-id="52633-112">Steps</span></span>

<span data-ttu-id="52633-113">スライダーが変化したときに自動的にポストバックされるようにするには、両方のテキストボックスに属性 `AutoPostBack="true"`が必要です。これは、スライダー自体になるテキストボックスと、スライダーの位置を保持するテキストボックスです。</span><span class="sxs-lookup"><span data-stu-id="52633-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="52633-114">そのために必要なマークアップは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="52633-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="52633-115">ASP.NET AJAX Control Toolkit の `SliderExtender` コントロールでは、次の2つのテキストボックスにスライダーの機能が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="52633-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="52633-116">後で追加の label 要素を使用して、ユーザーにポストバックを通知します。</span><span class="sxs-lookup"><span data-stu-id="52633-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="52633-117">最後に、ASP.NET AJAX の `ScriptManager` 制御によって、コントロールツールキットが動作するために必要な JavaScript が読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="52633-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="52633-118">これで、スライダーがポストバックされます。サーバー側では、このイベントがキャッチされ、次のように処理されることがあります。</span><span class="sxs-lookup"><span data-stu-id="52633-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="52633-119">[スライダーを移動 ![とポストバックがトリガーされる](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="52633-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="52633-120">スライダーを移動するとポストバックがトリガーされます ([クリックすると、フルサイズのイメージが表示](using-the-slider-control-with-auto-postback-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="52633-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="52633-121">[![後、この変更の日付はラベルに書き込まれます。](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="52633-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="52633-122">その後、この変更の日付がラベルに書き込まれます ([クリックすると、フルサイズの画像が表示](using-the-slider-control-with-auto-postback-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="52633-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52633-123">[前へ](databinding-the-slider-control-cs.md)
> [次へ](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="52633-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
