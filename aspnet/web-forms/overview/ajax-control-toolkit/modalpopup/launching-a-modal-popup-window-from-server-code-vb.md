---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: サーバーコードからモーダルポップアップウィンドウを起動する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、一部のシナリオでは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496960"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a><span data-ttu-id="96140-104">サーバー コードからモーダル ポップアップ ウィンドウを起動する (VB)</span><span class="sxs-lookup"><span data-stu-id="96140-104">Launching a Modal Popup Window from Server Code (VB)</span></span>

<span data-ttu-id="96140-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="96140-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="96140-106">[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="96140-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span></span>

> <span data-ttu-id="96140-107">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="96140-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="96140-108">ただし、一部のシナリオでは、モーダルポップアップを開くことがサーバー側でトリガーされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="96140-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="96140-109">概要</span><span class="sxs-lookup"><span data-stu-id="96140-109">Overview</span></span>

<span data-ttu-id="96140-110">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="96140-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="96140-111">ただし、一部のシナリオでは、モーダルポップアップを開くことがサーバー側でトリガーされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="96140-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="96140-112">手順</span><span class="sxs-lookup"><span data-stu-id="96140-112">Steps</span></span>

<span data-ttu-id="96140-113">まず、ModalPopup コントロールがどのように動作するかを示すために、ASP.NET Button web コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="96140-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="96140-114">新しいページの &lt;フォーム&gt; 要素内にこのようなボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="96140-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

<span data-ttu-id="96140-115">次に、作成するポップアップのマークアップが必要です。</span><span class="sxs-lookup"><span data-stu-id="96140-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="96140-116">`<asp:Panel>` コントロールとして定義し、ボタンコントロールが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="96140-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="96140-117">ModalPopup コントロールは、このようなボタンをポップアップを閉じる機能を提供します。そうしないと、簡単に消えることができません。</span><span class="sxs-lookup"><span data-stu-id="96140-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

<span data-ttu-id="96140-118">次に、ASP.NET AJAX Toolkit から ModalPopup コントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="96140-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="96140-119">コントロールを読み込むボタンのプロパティ、非表示にするボタン、および実際のポップアップの ID を設定します。</span><span class="sxs-lookup"><span data-stu-id="96140-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

<span data-ttu-id="96140-120">ASP.NET AJAX に基づくすべての web ページと同様です。スクリプトマネージャーでは、さまざまなターゲットブラウザーに必要な JavaScript ライブラリを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="96140-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

<span data-ttu-id="96140-121">ブラウザーで例を実行します。</span><span class="sxs-lookup"><span data-stu-id="96140-121">Run the example in the browser.</span></span> <span data-ttu-id="96140-122">このボタンをクリックすると、モーダルポップアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="96140-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="96140-123">サーバー側コードを使用して同じ効果を得るために、新しいボタンが必要です。</span><span class="sxs-lookup"><span data-stu-id="96140-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

<span data-ttu-id="96140-124">ご覧のように、ボタンをクリックするとポストバックが生成され、サーバーで `ServerButton_Click()` メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="96140-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="96140-125">このメソッドでは、`launchModal()` という名前の JavaScript 関数が完全に実行され、ページが読み込まれると JavaScript 関数が実行されます。</span><span class="sxs-lookup"><span data-stu-id="96140-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

<span data-ttu-id="96140-126">`launchModal()` のジョブは、ModalPopup を表示することです。</span><span class="sxs-lookup"><span data-stu-id="96140-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="96140-127">`launchModal()` 関数は、HTML ページ全体が読み込まれた後に実行されます。</span><span class="sxs-lookup"><span data-stu-id="96140-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="96140-128">しかし、現時点では、ASP.NET AJAX フレームワークはまだ完全に読み込まれていません。</span><span class="sxs-lookup"><span data-stu-id="96140-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="96140-129">したがって、`launchModal()` 関数は、ModalPopup コントロールを後で表示する必要がある変数を設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="96140-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

<span data-ttu-id="96140-130">`pageLoad()` JavaScript 関数は、ASP.NET AJAX が完全に読み込まれた後に実行される特別な関数です。</span><span class="sxs-lookup"><span data-stu-id="96140-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="96140-131">したがって、ModalPopup コントロールを表示するコードをこの関数に追加しますが、の前に `launchModal()` が呼び出されている場合に限ります。</span><span class="sxs-lookup"><span data-stu-id="96140-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

<span data-ttu-id="96140-132">`$find()` 関数は、ページ上の名前付き要素を探し、サーバー側 ID をパラメーターとして想定しています。</span><span class="sxs-lookup"><span data-stu-id="96140-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="96140-133">したがって、`$find("mpe")` は ModalPopup コントロールのクライアント表現を返します。`show()` メソッドを使用すると、ポップアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="96140-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="96140-134">[いずれかのボタンをクリックしたときにモーダルポップアップが表示さ ![](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="96140-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="96140-135">いずれかのボタンがクリックされると、モーダルポップアップが表示されます ([クリックすると、フルサイズの画像が表示](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="96140-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96140-136">[前へ](positioning-a-modalpopup-cs.md)
> [次へ](using-modalpopup-with-a-repeater-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="96140-136">[Previous](positioning-a-modalpopup-cs.md)
[Next](using-modalpopup-with-a-repeater-control-vb.md)</span></span>
