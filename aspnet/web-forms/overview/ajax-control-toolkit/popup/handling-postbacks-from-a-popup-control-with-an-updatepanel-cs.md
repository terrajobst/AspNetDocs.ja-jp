---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: ポップアップコントロールからのポストバックを UpdatePanel (C#) で処理するMicrosoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 特別な注意が必要です...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606317"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a><span data-ttu-id="117dd-104">ポップアップ コントロールからポストバックを処理する (UpdatePanel あり) (C#)</span><span class="sxs-lookup"><span data-stu-id="117dd-104">Handling Postbacks from A Popup Control With an UpdatePanel (C#)</span></span>

<span data-ttu-id="117dd-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="117dd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="117dd-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="117dd-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span></span>

> <span data-ttu-id="117dd-107">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="117dd-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="117dd-108">このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="117dd-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="117dd-109">の概要</span><span class="sxs-lookup"><span data-stu-id="117dd-109">Overview</span></span>

<span data-ttu-id="117dd-110">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="117dd-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="117dd-111">このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="117dd-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="117dd-112">手順</span><span class="sxs-lookup"><span data-stu-id="117dd-112">Steps</span></span>

<span data-ttu-id="117dd-113">ポストバックで `PopupControl` を使用すると、ポストバックによるページの更新が `UpdatePanel` によって妨げられる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="117dd-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="117dd-114">次のマークアップは、いくつかの重要な要素を定義します。</span><span class="sxs-lookup"><span data-stu-id="117dd-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="117dd-115">ASP.NET AJAX Control Toolkit が動作するように `ScriptManager` コントロール</span><span class="sxs-lookup"><span data-stu-id="117dd-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="117dd-116">ポップアップをトリガーする2つの `TextBox` コントロール</span><span class="sxs-lookup"><span data-stu-id="117dd-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="117dd-117">ポップアップとして機能する `Panel` コントロール</span><span class="sxs-lookup"><span data-stu-id="117dd-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="117dd-118">パネル内では、`Calendar` コントロールが `UpdatePanel` コントロール内に埋め込まれます。</span><span class="sxs-lookup"><span data-stu-id="117dd-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="117dd-119">パネルをテキストボックスに割り当てる2つの `PopupControlExtender` コントロール</span><span class="sxs-lookup"><span data-stu-id="117dd-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="117dd-120">`Calendar` コントロールの `OnSelectionChanged` 属性が設定されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="117dd-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="117dd-121">そのため、ユーザーがカレンダー内の日付を選択すると、ポストバックが発生し、サーバー側のメソッド `c1_SelectionChanged()` が実行されます。</span><span class="sxs-lookup"><span data-stu-id="117dd-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="117dd-122">そのメソッド内で、現在の日付を取得し、テキストボックスに書き戻す必要があります。</span><span class="sxs-lookup"><span data-stu-id="117dd-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="117dd-123">の構文は次のとおりです。最初に、ページの `PopupControlExtender` のプロキシオブジェクトを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="117dd-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="117dd-124">ASP.NET AJAX Control Toolkit には、`GetProxyForCurrentPopup()` メソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="117dd-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="117dd-125">このメソッドが返すオブジェクトは、`Commit()` メソッドをサポートしています。このメソッドは、ポップアップをトリガーしたコントロール (メソッド呼び出しをトリガーしたコントロールではない) に値を返します。</span><span class="sxs-lookup"><span data-stu-id="117dd-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="117dd-126">次のコードでは、`Commit()` メソッドの引数として選択された日付を提供しています。これにより、コードは、選択した日付をテキストボックスに書き戻します。</span><span class="sxs-lookup"><span data-stu-id="117dd-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="117dd-127">これで、カレンダーの日付をクリックするたびに、選択した日付が関連するテキストボックスに表示され、多くの web サイトで現在検出できる日付の選択コントロールが作成されます。</span><span class="sxs-lookup"><span data-stu-id="117dd-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="117dd-128">[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="117dd-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="117dd-129">ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="117dd-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="117dd-130">[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="117dd-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="117dd-131">日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="117dd-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="117dd-132">[前へ](using-multiple-popup-controls-cs.md)
> [次へ](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span><span class="sxs-lookup"><span data-stu-id="117dd-132">[Previous](using-multiple-popup-controls-cs.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span></span>
