---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: スライダーコントロールのデータバインドC#() |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 現在の positio をバインドすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ef547573f17f3265ad72717d3d3bbc622fd6894e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598607"
---
# <a name="databinding-the-slider-control-c"></a><span data-ttu-id="6f401-104">スライダー コントロールをデータバインドする (C#)</span><span class="sxs-lookup"><span data-stu-id="6f401-104">Databinding the Slider Control (C#)</span></span>

<span data-ttu-id="6f401-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="6f401-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6f401-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6f401-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="6f401-107">AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="6f401-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6f401-108">スライダーの現在位置を別の ASP.NET コントロールにバインドすることができます。</span><span class="sxs-lookup"><span data-stu-id="6f401-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="6f401-109">の概要</span><span class="sxs-lookup"><span data-stu-id="6f401-109">Overview</span></span>

<span data-ttu-id="6f401-110">AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="6f401-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6f401-111">スライダーの現在位置を別の ASP.NET コントロールにバインドすることができます。</span><span class="sxs-lookup"><span data-stu-id="6f401-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="6f401-112">手順</span><span class="sxs-lookup"><span data-stu-id="6f401-112">Steps</span></span>

<span data-ttu-id="6f401-113">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="6f401-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="6f401-114">次に、2つの `TextBox` コントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="6f401-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="6f401-115">一方はグラフィカルなスライダーに変換され、もう一方はスライダーの位置を保持します。</span><span class="sxs-lookup"><span data-stu-id="6f401-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="6f401-116">次の手順は、既に最後の手順です。</span><span class="sxs-lookup"><span data-stu-id="6f401-116">The next step is already the final step.</span></span> <span data-ttu-id="6f401-117">ASP.NET AJAX Control Toolkit の `SliderExtender` コントロールによって、最初のテキストボックスの下にスライダーが表示され、スライダーの位置が変更されると、2つ目のテキストボックスが自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f401-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="6f401-118">これが機能するためには、`SliderExtender`の `TargetControlID` 属性が最初のテキストボックスの ID に設定されている必要があります。`BoundControlID` 属性は、2番目のテキストボックスの ID に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f401-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="6f401-119">ブラウザーで見るとわかるように、データバインディングは双方向で動作します。テキストボックスに新しい値を入力すると、スライダーの位置が更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f401-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="6f401-120">2番目のテキストボックスを読み取り専用にする場合は、ユーザーが手動で値を更新するのが難しいように、テキストフィールドに弱い保護を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="6f401-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="6f401-121">[![スライダーとテキストボックスが同期されています](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f401-121">[![Slider and text box are in sync](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f401-122">スライダーとテキストボックスが同期されています ([クリックすると、フルサイズの画像が表示](databinding-the-slider-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="6f401-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f401-123">[前へ](using-the-slider-control-with-auto-postback-cs.md)
> [次へ](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6f401-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>
