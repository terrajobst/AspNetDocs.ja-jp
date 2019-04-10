---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 複数のポップアップ コントロール (c#) を使用して |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。 M を使用することもしています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 2d13fbfdb8d2fe66c5ff036060b9289017f79d14
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421538"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="4a92f-104">複数のポップアップ コントロールを使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="4a92f-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="4a92f-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4a92f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4a92f-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4a92f-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="4a92f-107">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4a92f-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4a92f-108">1 ページには、複数のポップアップ コントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="4a92f-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="4a92f-109">概要</span><span class="sxs-lookup"><span data-stu-id="4a92f-109">Overview</span></span>

<span data-ttu-id="4a92f-110">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4a92f-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4a92f-111">1 ページには、複数のポップアップ コントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="4a92f-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="4a92f-112">手順</span><span class="sxs-lookup"><span data-stu-id="4a92f-112">Steps</span></span>

<span data-ttu-id="4a92f-113">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、`<form>`要素)。</span><span class="sxs-lookup"><span data-stu-id="4a92f-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="4a92f-114">次に、ポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="4a92f-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="4a92f-115">パネルに含まれる現在のシナリオでは、`Calendar`コントロール。</span><span class="sxs-lookup"><span data-stu-id="4a92f-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="4a92f-116">内のパネルを配置するカレンダーのポストバックの原因となったページ更新を回避するために、`UpdatePanel`コントロール。</span><span class="sxs-lookup"><span data-stu-id="4a92f-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="4a92f-117">ページには、2 つのテキスト ボックスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="4a92f-117">The page also contains two text boxes.</span></span> <span data-ttu-id="4a92f-118">各テキスト ボックスのテキスト ボックスがアクティブ化される、カレンダーのポップアップは表示されます。</span><span class="sxs-lookup"><span data-stu-id="4a92f-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="4a92f-119">2 つのテキスト ボックスのそれぞれを拡張するようになりました、`PopupControlExtender`します。</span><span class="sxs-lookup"><span data-stu-id="4a92f-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="4a92f-120">`TargetControlID`属性は、extender に関連付けられているコントロールの ID を提供します。</span><span class="sxs-lookup"><span data-stu-id="4a92f-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="4a92f-121">`PopupControlID`属性には、ポップアップ パネルの ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4a92f-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="4a92f-122">この場合は、両方のエクステンダーが同じのパネルを表示するが、さまざまなパネルをも可能であれば、します。</span><span class="sxs-lookup"><span data-stu-id="4a92f-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="4a92f-123">テキスト フィールド内でクリックしたときに、カレンダーが表示されます、フィールドの下の日付を選択することができます。</span><span class="sxs-lookup"><span data-stu-id="4a92f-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="4a92f-124">(テキスト ボックスに、選択した日付は戻ってきてで取り上げる別のチュートリアルです。)</span><span class="sxs-lookup"><span data-stu-id="4a92f-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


[![T<span data-ttu-id="4a92f-125">彼の予定表は、テキスト ボックスに、ユーザーがクリックしたときに表示されます]</span><span class="sxs-lookup"><span data-stu-id="4a92f-125">he Calendar appears when the user clicks into the textbox]</span></span>(using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

<span data-ttu-id="4a92f-126">テキスト ボックスに、ユーザーがクリックしたときに、カレンダーが表示されます ([フルサイズの画像を表示する をクリックします](using-multiple-popup-controls-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="4a92f-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4a92f-127">次へ</span><span class="sxs-lookup"><span data-stu-id="4a92f-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
