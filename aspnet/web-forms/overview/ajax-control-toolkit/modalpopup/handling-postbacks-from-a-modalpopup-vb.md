---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: ModalPopup からポストバックを処理する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 Pos を使用する場合は、特別な注意が必要です。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606619"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="7f5a2-104">ModalPopup からポストバックを処理する (VB)</span><span class="sxs-lookup"><span data-stu-id="7f5a2-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="7f5a2-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="7f5a2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7f5a2-106">[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7f5a2-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="7f5a2-107">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7f5a2-108">ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="7f5a2-109">の概要</span><span class="sxs-lookup"><span data-stu-id="7f5a2-109">Overview</span></span>

<span data-ttu-id="7f5a2-110">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7f5a2-111">ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="7f5a2-112">手順</span><span class="sxs-lookup"><span data-stu-id="7f5a2-112">Steps</span></span>

<span data-ttu-id="7f5a2-113">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="7f5a2-114">次に、モーダルポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="7f5a2-115">ここで、ユーザーは名前と電子メールアドレスを入力できます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="7f5a2-116">ボタンを使用してポップアップを閉じ、情報を保存します。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="7f5a2-117">このボタンがクリックされたときにポストバックが発生するように、`OnClick` 属性が設定されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="7f5a2-118">ページ自体は、名前と電子メールアドレスというまったく同じ情報の2つのラベルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="7f5a2-119">モーダルポップアップをトリガーするには、ボタンを使用します。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="7f5a2-120">ポップアップが表示されるようにするには、`ModalPopupExtender` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="7f5a2-121">`PopupControlID` 属性をパネルの ID に設定し、ボタンの ID に `TargetControlID` します。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="7f5a2-122">モーダルポップアップ内の [`Save`] ボタンがクリックされるたびに、サーバー側の `SaveData()` メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="7f5a2-123">ここでは、入力したデータをデータストアに保存できます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="7f5a2-124">わかりやすくするために、新しいデータは次のようにラベルに出力されます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="7f5a2-125">また、モーダルポップアップ内のテキストボックスコントロールに、現在の名前と電子メールアドレスが入力されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="7f5a2-126">ただし、これはポストバックが発生しない場合にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="7f5a2-127">ポストバックがある場合は、ASP.NET viewstate 機能によって、テキストボックスに適切な値が自動的に入力されます。</span><span class="sxs-lookup"><span data-stu-id="7f5a2-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="7f5a2-128">[モーダルポップアップによってポストバックが発生 ![](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7f5a2-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="7f5a2-129">モーダルポップアップによってポストバックが発生します ([クリックすると、フルサイズのイメージが表示](handling-postbacks-from-a-modalpopup-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7f5a2-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7f5a2-130">[前へ](using-modalpopup-with-a-repeater-control-vb.md)
> [次へ](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7f5a2-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
