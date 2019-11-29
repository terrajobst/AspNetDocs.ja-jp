---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 複数のポップアップコントロールをC#使用する () |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 また、m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611640"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="05ff5-104">複数のポップアップ コントロールを使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="05ff5-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="05ff5-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="05ff5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="05ff5-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="05ff5-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="05ff5-107">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="05ff5-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="05ff5-108">1つのページで複数のポップアップコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="05ff5-109">の概要</span><span class="sxs-lookup"><span data-stu-id="05ff5-109">Overview</span></span>

<span data-ttu-id="05ff5-110">AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="05ff5-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="05ff5-111">1つのページで複数のポップアップコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="05ff5-112">手順</span><span class="sxs-lookup"><span data-stu-id="05ff5-112">Steps</span></span>

<span data-ttu-id="05ff5-113">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="05ff5-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="05ff5-114">次に、ポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="05ff5-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="05ff5-115">現在のシナリオでは、パネルには `Calendar` コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="05ff5-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="05ff5-116">カレンダーのポストバックによるページの更新を回避するために、パネルは `UpdatePanel` コントロール内に配置されます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="05ff5-117">このページには、2つのテキストボックスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="05ff5-117">The page also contains two text boxes.</span></span> <span data-ttu-id="05ff5-118">各テキストボックスでは、テキストボックスがアクティブになるとカレンダーのポップアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="05ff5-119">ここで、2つのテキストボックスをそれぞれ `PopupControlExtender`に拡張します。</span><span class="sxs-lookup"><span data-stu-id="05ff5-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="05ff5-120">`TargetControlID` 属性は、エクステンダーに関連付けられているコントロールの ID を提供します。</span><span class="sxs-lookup"><span data-stu-id="05ff5-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="05ff5-121">`PopupControlID` 属性には、ポップアップパネルの ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="05ff5-122">この場合、どちらのエクステンダーも同じパネルを表示しますが、異なるパネルを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="05ff5-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="05ff5-123">テキストフィールド内をクリックするたびに、フィールドの下にカレンダーが表示され、日付を選択できるようになります。</span><span class="sxs-lookup"><span data-stu-id="05ff5-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="05ff5-124">(選択した日付をテキストボックスに戻すと、別のチュートリアルで説明されています)。</span><span class="sxs-lookup"><span data-stu-id="05ff5-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="05ff5-125">[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05ff5-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="05ff5-126">ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](using-multiple-popup-controls-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="05ff5-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="05ff5-127">次へ</span><span class="sxs-lookup"><span data-stu-id="05ff5-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
