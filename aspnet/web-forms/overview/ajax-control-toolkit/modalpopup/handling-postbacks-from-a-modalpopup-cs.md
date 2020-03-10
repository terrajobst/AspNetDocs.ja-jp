---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: ModalPopup からポストバックを処理C#する () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 Pos を使用する場合は、特別な注意が必要です。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446206"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="e9914-104">ModalPopup からポストバックを処理する (C#)</span><span class="sxs-lookup"><span data-stu-id="e9914-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="e9914-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="e9914-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e9914-106">[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e9914-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="e9914-107">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="e9914-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e9914-108">ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="e9914-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="e9914-109">概要</span><span class="sxs-lookup"><span data-stu-id="e9914-109">Overview</span></span>

<span data-ttu-id="e9914-110">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="e9914-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e9914-111">ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="e9914-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="e9914-112">手順</span><span class="sxs-lookup"><span data-stu-id="e9914-112">Steps</span></span>

<span data-ttu-id="e9914-113">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="e9914-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="e9914-114">次に、モーダルポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="e9914-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="e9914-115">ここで、ユーザーは名前と電子メールアドレスを入力できます。</span><span class="sxs-lookup"><span data-stu-id="e9914-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="e9914-116">ボタンを使用してポップアップを閉じ、情報を保存します。</span><span class="sxs-lookup"><span data-stu-id="e9914-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="e9914-117">このボタンがクリックされたときにポストバックが発生するように、`OnClick` 属性が設定されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e9914-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="e9914-118">ページ自体は、名前と電子メールアドレスというまったく同じ情報の2つのラベルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="e9914-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="e9914-119">モーダルポップアップをトリガーするには、ボタンを使用します。</span><span class="sxs-lookup"><span data-stu-id="e9914-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="e9914-120">ポップアップが表示されるようにするには、`ModalPopupExtender` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="e9914-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="e9914-121">`PopupControlID` 属性をパネルの ID に設定し、ボタンの ID に `TargetControlID` します。</span><span class="sxs-lookup"><span data-stu-id="e9914-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="e9914-122">モーダルポップアップ内の [`Save`] ボタンがクリックされるたびに、サーバー側の `SaveData()` メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="e9914-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="e9914-123">ここでは、入力したデータをデータストアに保存できます。</span><span class="sxs-lookup"><span data-stu-id="e9914-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="e9914-124">わかりやすくするために、新しいデータは次のようにラベルに出力されます。</span><span class="sxs-lookup"><span data-stu-id="e9914-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="e9914-125">また、モーダルポップアップ内のテキストボックスコントロールに、現在の名前と電子メールアドレスが入力されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9914-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="e9914-126">ただし、これはポストバックが発生しない場合にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="e9914-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="e9914-127">ポストバックがある場合は、ASP.NET viewstate 機能によって、テキストボックスに適切な値が自動的に入力されます。</span><span class="sxs-lookup"><span data-stu-id="e9914-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

<span data-ttu-id="e9914-128">[モーダルポップアップによってポストバックが発生 ![](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e9914-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="e9914-129">モーダルポップアップによってポストバックが発生します ([クリックすると、フルサイズのイメージが表示](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="e9914-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e9914-130">[前へ](using-modalpopup-with-a-repeater-control-cs.md)
> [次へ](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e9914-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
