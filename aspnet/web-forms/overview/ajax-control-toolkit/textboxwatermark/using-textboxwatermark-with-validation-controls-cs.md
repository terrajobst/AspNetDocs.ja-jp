---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 検証コントロールでの TextBoxWatermark のC#使用 () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466588"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="a98ac-104">検証コントロールと共に TextBoxWatermark を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="a98ac-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="a98ac-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="a98ac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a98ac-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a98ac-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="a98ac-107">AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="a98ac-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="a98ac-108">ユーザーがボックスをクリックすると、そのボックスは空になります。</span><span class="sxs-lookup"><span data-stu-id="a98ac-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="a98ac-109">ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="a98ac-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="a98ac-110">これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a98ac-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="a98ac-111">概要</span><span class="sxs-lookup"><span data-stu-id="a98ac-111">Overview</span></span>

<span data-ttu-id="a98ac-112">AJAX コントロールツールキットの `TextBoxWatermark` コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="a98ac-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="a98ac-113">ユーザーがボックスをクリックすると、そのボックスは空になります。</span><span class="sxs-lookup"><span data-stu-id="a98ac-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="a98ac-114">ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="a98ac-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="a98ac-115">これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a98ac-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="a98ac-116">手順</span><span class="sxs-lookup"><span data-stu-id="a98ac-116">Steps</span></span>

<span data-ttu-id="a98ac-117">このサンプルの基本的な設定は次のとおりです。 `TextBox` コントロールは、`TextBoxWatermarkExtender` コントロールを使用して目標ます。</span><span class="sxs-lookup"><span data-stu-id="a98ac-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="a98ac-118">ボタンはポストバックをトリガーし、後でページの検証コントロールをトリガーするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a98ac-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="a98ac-119">また、ASP.NET AJAX を初期化するには、`ScriptManager` コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="a98ac-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="a98ac-120">次に、フォームが送信されたときにフィールドにテキストがあるかどうかを確認する `RequiredFieldValidator` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="a98ac-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="a98ac-121">バリデーターの `InitialValue` プロパティは、`TextBoxWatermarkExtender` コントロールで使用されているのと同じ値に設定する必要があります。フォームが送信されると、変更されていないテキストボックスの値は、その中の基準値になります。</span><span class="sxs-lookup"><span data-stu-id="a98ac-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="a98ac-122">ただし、この方法には1つの問題があります。クライアントが JavaScript を無効にした場合は、テキストフィールドがウォーターマークテキストに事前されないため、`RequiredFieldValidator` はエラーメッセージをトリガーしません。</span><span class="sxs-lookup"><span data-stu-id="a98ac-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="a98ac-123">そのため、2番目の `RequiredFieldValidator` コントロールが必要です。このコントロールでは、空のテキストボックスを確認します (`InitialValue` 属性を省略します)。</span><span class="sxs-lookup"><span data-stu-id="a98ac-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="a98ac-124">両方の検証コントロールで `Display`=`"Dynamic"`が使用されるため、エンドユーザーは2つの検証コントロールのどちらを起動したかを視覚的に区別することはできません。そのうちの1つだけがあるようです。</span><span class="sxs-lookup"><span data-stu-id="a98ac-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="a98ac-125">最後に、検証コントロールによってエラーメッセージが発行されなかった場合に、フィールドにテキストを出力するサーバー側コードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a98ac-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="a98ac-126">[検証コントロールの ![、フィールドにテキストがないことを示しています。](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a98ac-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="a98ac-127">検証コントロールは、フィールドにテキストがないことを示しています ([クリックすると、フルサイズの画像が表示](using-textboxwatermark-with-validation-controls-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="a98ac-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a98ac-128">[前へ](using-textboxwatermark-in-a-formview-cs.md)
> [次へ](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a98ac-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
