---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel を使用せずに Popup コントロールからポストバックを処理する (VB) |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 Su でポストバックが発生したとき...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446140"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="5999b-104">ポップアップ コントロールからポストバックを処理する (UpdatePanel なし) (VB)</span><span class="sxs-lookup"><span data-stu-id="5999b-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="5999b-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="5999b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5999b-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5999b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="5999b-107">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="5999b-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5999b-108">このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="5999b-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="5999b-109">概要</span><span class="sxs-lookup"><span data-stu-id="5999b-109">Overview</span></span>

<span data-ttu-id="5999b-110">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="5999b-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5999b-111">このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="5999b-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="5999b-112">手順</span><span class="sxs-lookup"><span data-stu-id="5999b-112">Steps</span></span>

<span data-ttu-id="5999b-113">ポストバックで `PopupControl` を使用するときに、ページに `UpdatePanel` を設定していない場合、コントロールツールキットでは、ポストバックの原因となったポップアップをトリガーしたクライアント要素を特定する方法は提供されません。</span><span class="sxs-lookup"><span data-stu-id="5999b-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="5999b-114">ただし、このシナリオの回避策としては小さなトリックがあります。</span><span class="sxs-lookup"><span data-stu-id="5999b-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="5999b-115">まず、基本的なセットアップは次のようになります。2つのテキストボックスで同じポップアップ (予定表) がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="5999b-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="5999b-116">2つの `PopupControlExtenders` テキストボックスとポップアップをまとめて表示します。</span><span class="sxs-lookup"><span data-stu-id="5999b-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="5999b-117">基本的な考え方は、ポップアップを起動したテキストボックスを保持する &lt;`form`&gt; 要素に非表示のフォームフィールドを追加することです。</span><span class="sxs-lookup"><span data-stu-id="5999b-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="5999b-118">ページが読み込まれると、JavaScript コードによって、イベントハンドラーが両方のテキストボックスに追加されます。ユーザーがテキストボックスをクリックするたびに、その名前が隠しフォームフィールドに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="5999b-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="5999b-119">サーバー側のコードでは、隠しフィールドの値を読み取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="5999b-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="5999b-120">非表示のフォームフィールドは簡単に操作できるため、非表示の値を検証するホワイトリストアプローチが必要です。</span><span class="sxs-lookup"><span data-stu-id="5999b-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="5999b-121">正しいテキストボックスが識別されると、カレンダーの日付が書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="5999b-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="5999b-122">[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5999b-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="5999b-123">ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="5999b-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="5999b-124">[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5999b-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="5999b-125">日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="5999b-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5999b-126">[[戻る]](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5999b-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
