---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: ModalPopup (C#) を配置するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、コントロールは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496918"
---
# <a name="positioning-a-modalpopup-c"></a><span data-ttu-id="a7adb-104">ModalPopup の位置を決める (C#)</span><span class="sxs-lookup"><span data-stu-id="a7adb-104">Positioning a ModalPopup (C#)</span></span>

<span data-ttu-id="a7adb-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="a7adb-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a7adb-106">[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7adb-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="a7adb-107">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="a7adb-108">ただし、このコントロールにはポップアップを配置するための組み込みの機能は用意されていません。</span><span class="sxs-lookup"><span data-stu-id="a7adb-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="a7adb-109">概要</span><span class="sxs-lookup"><span data-stu-id="a7adb-109">Overview</span></span>

<span data-ttu-id="a7adb-110">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="a7adb-111">ただし、このコントロールにはポップアップを配置するための組み込みの機能は用意されていません。</span><span class="sxs-lookup"><span data-stu-id="a7adb-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="a7adb-112">手順</span><span class="sxs-lookup"><span data-stu-id="a7adb-112">Steps</span></span>

<span data-ttu-id="a7adb-113">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するために、`ScriptManager`ます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="a7adb-114">コントロールは、ページの任意の場所に配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="a7adb-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="a7adb-115">次に、モーダルポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="a7adb-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="a7adb-116">ポップアップを閉じるには、ボタンを使用します。</span><span class="sxs-lookup"><span data-stu-id="a7adb-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="a7adb-117">ポップアップが表示されるたびに、ページ内の特定の場所に配置されます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="a7adb-118">このタスクでは、クライアント側の JavaScript 関数が作成されます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="a7adb-119">まず、パネルにアクセスしようとします。</span><span class="sxs-lookup"><span data-stu-id="a7adb-119">It first tries to access the panel.</span></span> <span data-ttu-id="a7adb-120">成功した場合、パネルの位置は CSS と JavaScript を使用して設定されます (ポップアップの位置を変更します)。</span><span class="sxs-lookup"><span data-stu-id="a7adb-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="a7adb-121">ただし、`ModalPopupExtender` コントロールでもポップアップの配置が試行されます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="a7adb-122">したがって、JavaScript コードでは、ポップアップが1秒ごとに繰り返し配置されます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="a7adb-123">ご覧のように、`setTimeout()` JavaScript メソッドの戻り値はグローバル変数に保存されます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="a7adb-124">これにより、`clearTimeout()` メソッドを使用して、オンデマンドでポップアップの繰り返し位置を停止できます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="a7adb-125">ここでは、必要に応じて、ブラウザーがこれらの関数を呼び出すようにします。</span><span class="sxs-lookup"><span data-stu-id="a7adb-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="a7adb-126">パネルをトリガーするボタンをクリックしたときに `movePanel()` JavaScript 関数を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7adb-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="a7adb-127">また、`stopMoving()` 関数は、ポップアップが閉じられたときに再生されます。これは、`ModalPopupExtender` コントロールでトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="a7adb-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

<span data-ttu-id="a7adb-128">[指定した位置にモーダルポップアップが表示さ ![](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a7adb-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="a7adb-129">モーダルポップアップが指定した位置に表示されます ([クリックすると、フルサイズの画像が表示](positioning-a-modalpopup-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="a7adb-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a7adb-130">[前へ](handling-postbacks-from-a-modalpopup-cs.md)
> [次へ](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a7adb-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
