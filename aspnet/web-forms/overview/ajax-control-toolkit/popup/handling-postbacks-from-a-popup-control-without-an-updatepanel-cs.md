---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel を使用せずに Popup コントロールからポストC#バックを処理する () |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 Su でポストバックが発生したとき...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496504"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="28653-104">ポップアップ コントロールからポストバックを処理する (UpdatePanel なし) (C#)</span><span class="sxs-lookup"><span data-stu-id="28653-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>

<span data-ttu-id="28653-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="28653-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="28653-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="28653-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="28653-107">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="28653-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="28653-108">このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="28653-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="28653-109">概要</span><span class="sxs-lookup"><span data-stu-id="28653-109">Overview</span></span>

<span data-ttu-id="28653-110">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="28653-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="28653-111">このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="28653-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="28653-112">手順</span><span class="sxs-lookup"><span data-stu-id="28653-112">Steps</span></span>

<span data-ttu-id="28653-113">ポストバックで `PopupControl` を使用するときに、ページに `UpdatePanel` を設定していない場合、コントロールツールキットでは、ポストバックの原因となったポップアップをトリガーしたクライアント要素を特定する方法は提供されません。</span><span class="sxs-lookup"><span data-stu-id="28653-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="28653-114">ただし、このシナリオの回避策としては小さなトリックがあります。</span><span class="sxs-lookup"><span data-stu-id="28653-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="28653-115">まず、基本的なセットアップは次のようになります。2つのテキストボックスで同じポップアップ (予定表) がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="28653-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="28653-116">2つの `PopupControlExtenders` テキストボックスとポップアップをまとめて表示します。</span><span class="sxs-lookup"><span data-stu-id="28653-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="28653-117">基本的な考え方は、ポップアップを起動したテキストボックスを保持する &lt;`form`&gt; 要素に非表示のフォームフィールドを追加することです。</span><span class="sxs-lookup"><span data-stu-id="28653-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="28653-118">ページが読み込まれると、JavaScript コードによって、イベントハンドラーが両方のテキストボックスに追加されます。ユーザーがテキストボックスをクリックするたびに、その名前が隠しフォームフィールドに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="28653-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="28653-119">サーバー側のコードでは、隠しフィールドの値を読み取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="28653-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="28653-120">非表示のフォームフィールドは簡単に操作できるため、非表示の値を検証するホワイトリストアプローチが必要です。</span><span class="sxs-lookup"><span data-stu-id="28653-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="28653-121">正しいテキストボックスが識別されると、カレンダーの日付が書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="28653-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

<span data-ttu-id="28653-122">[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28653-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="28653-123">ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="28653-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="28653-124">[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="28653-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="28653-125">日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="28653-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="28653-126">[前へ](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [次へ](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="28653-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
