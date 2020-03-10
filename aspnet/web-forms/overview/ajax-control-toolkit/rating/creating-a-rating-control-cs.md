---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 評価コントロールを作成するC#() |Microsoft Docs
author: wenz
description: E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、いくつかのコーディング作業が必要ですが、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496162"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="65dd6-104">評価コントロールを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="65dd6-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="65dd6-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="65dd6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="65dd6-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="65dd6-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="65dd6-107">E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="65dd6-108">これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。</span><span class="sxs-lookup"><span data-stu-id="65dd6-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="65dd6-109">概要</span><span class="sxs-lookup"><span data-stu-id="65dd6-109">Overview</span></span>

<span data-ttu-id="65dd6-110">E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="65dd6-111">これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。</span><span class="sxs-lookup"><span data-stu-id="65dd6-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="65dd6-112">手順</span><span class="sxs-lookup"><span data-stu-id="65dd6-112">Steps</span></span>

<span data-ttu-id="65dd6-113">まず、2種類のイメージ (少なくとも) が必要です。1つは、入力された評価項目用で、もう1つは空の評価項目用です。</span><span class="sxs-lookup"><span data-stu-id="65dd6-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="65dd6-114">通常、評価項目は星またはスマイルです。</span><span class="sxs-lookup"><span data-stu-id="65dd6-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="65dd6-115">このシナリオでは、このチュートリアルのソースコードのダウンロードの一部として、3つのファイル、smiley-done、および空の .png とを見つけます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="65dd6-116">次に、新しい ASP.NET ファイルを作成し、`ScriptManager` コントロールの追加を開始します。</span><span class="sxs-lookup"><span data-stu-id="65dd6-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="65dd6-117">次に、ASP.NET AJAX Control Toolkit から `Rating` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="65dd6-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="65dd6-118">この例では、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="65dd6-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="65dd6-119">使用する初期評価を `CurrentRating` します</span><span class="sxs-lookup"><span data-stu-id="65dd6-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="65dd6-120">最大評価の `MaxRating`</span><span class="sxs-lookup"><span data-stu-id="65dd6-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="65dd6-121">評価項目 (星) が空のときに使用する CSS クラスを `EmptyStarCssClass` します</span><span class="sxs-lookup"><span data-stu-id="65dd6-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="65dd6-122">評価項目 (星) が入力されたときに使用する CSS クラスを `FilledStarCssClass` します</span><span class="sxs-lookup"><span data-stu-id="65dd6-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="65dd6-123">表示される stat に使用する CSS クラスを `StarCssClass` します</span><span class="sxs-lookup"><span data-stu-id="65dd6-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="65dd6-124">星評価がサーバーに送り返されるときに使用する CSS クラスを `WaitingStarCssClass` します</span><span class="sxs-lookup"><span data-stu-id="65dd6-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="65dd6-125">次に示すのは、5つの項目 (smileys) を持つ評価コントロールを作成するマークアップです。この場合、最初は何も入力されません。</span><span class="sxs-lookup"><span data-stu-id="65dd6-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="65dd6-126">参照される3つの CSS クラスは、CSS を使用して簡単に実行できる適切なイメージファイルを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="65dd6-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="65dd6-127">3つのイメージの幅と高さを指定していることを確認してください。そうしないと、表示が少し失敗に見えます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="65dd6-128">最後に、評価の結果がユーザーに表示される (少なくともデータベースに保存されている) 必要があります。</span><span class="sxs-lookup"><span data-stu-id="65dd6-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="65dd6-129">そのため、テキストメッセージの出力のラベルと、評価フォームをサーバーにポストバックするための [送信] ボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="65dd6-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="65dd6-130">サーバー側コードで、`ID` を使用して評価コントロールにアクセスし、選択した評価項目の番号である `CurrentRating` プロパティにアクセスします。この例では、0 ~ 5 の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="65dd6-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="65dd6-131">ページを保存し、ブラウザーに読み込みます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="65dd6-132">(最初に空になっている) 評価項目をポイントすると、JavaScript の効果が発生します。評価が変更されます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="65dd6-133">星のセットをクリックすると、現在の評価が保持されます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="65dd6-134">最後に、フォームを送信すると、サーバー側のコードによって、選択した評価が出力されます。</span><span class="sxs-lookup"><span data-stu-id="65dd6-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="65dd6-135">[最小限のコードで評価システムを作成 ![には](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="65dd6-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="65dd6-136">最小限のコードで評価システムを作成[する (クリックすると、フルサイズの画像が表示](creating-a-rating-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="65dd6-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="65dd6-137">Next</span><span class="sxs-lookup"><span data-stu-id="65dd6-137">Next</span></span>](creating-a-rating-control-vb.md)
