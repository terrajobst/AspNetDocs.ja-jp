---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: テキストボックス内の特定の文字のみを許可する (VB) |Microsoft Docs
author: wenz
description: ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。 ただし、これによって、ユーザーが無効な型を入力するのを防ぐことはできません...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497164"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="01530-104">テキスト ボックスで特定の文字だけを許可する (VB)</span><span class="sxs-lookup"><span data-stu-id="01530-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="01530-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="01530-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="01530-106">[コードのダウンロード](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="01530-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="01530-107">ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="01530-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="01530-108">ただし、これによって、ユーザーが無効な文字を入力したり、フォームを送信したりするのを防ぐことはできません。</span><span class="sxs-lookup"><span data-stu-id="01530-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="01530-109">概要</span><span class="sxs-lookup"><span data-stu-id="01530-109">Overview</span></span>

<span data-ttu-id="01530-110">ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="01530-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="01530-111">ただし、これによって、ユーザーが無効な文字を入力したり、フォームを送信したりするのを防ぐことはできません。</span><span class="sxs-lookup"><span data-stu-id="01530-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="01530-112">手順</span><span class="sxs-lookup"><span data-stu-id="01530-112">Steps</span></span>

<span data-ttu-id="01530-113">ASP.NET AJAX Control Toolkit には、テキストボックスを拡張する `FilteredTextBox` コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="01530-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="01530-114">アクティブ化されると、特定の文字セットのみがフィールドに入力される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01530-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="01530-115">これを機能させるには、まず、ASP.NET AJAX Control Toolkit でも使用されている JavaScript ライブラリを読み込む ASP.NET AJAX `ScriptManager` が必要です。</span><span class="sxs-lookup"><span data-stu-id="01530-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="01530-116">次に、テキストボックスが必要です。</span><span class="sxs-lookup"><span data-stu-id="01530-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="01530-117">最後に、`FilteredTextBoxExtender` コントロールは、ユーザーが入力できる文字を制限します。</span><span class="sxs-lookup"><span data-stu-id="01530-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="01530-118">最初に、`TargetControlID` 属性を `TextBox` コントロールの `ID` に設定します。</span><span class="sxs-lookup"><span data-stu-id="01530-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="01530-119">次に、使用可能な `FilterType` の値のいずれかを選択します。</span><span class="sxs-lookup"><span data-stu-id="01530-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="01530-120">`Custom` 既定値です。有効な文字の一覧を指定する必要があります</span><span class="sxs-lookup"><span data-stu-id="01530-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="01530-121">小文字のみを `LowercaseLetters`</span><span class="sxs-lookup"><span data-stu-id="01530-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="01530-122">`Numbers` 数字のみ</span><span class="sxs-lookup"><span data-stu-id="01530-122">`Numbers` digits only</span></span>
- <span data-ttu-id="01530-123">`UppercaseLetters` 大文字のみ</span><span class="sxs-lookup"><span data-stu-id="01530-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="01530-124">`Custom FilterType` を使用する場合は、`ValidChars` プロパティを設定し、入力可能な文字の一覧を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01530-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="01530-125">方法: テキストボックスにテキストを貼り付けようとすると、無効な文字がすべて削除されます。</span><span class="sxs-lookup"><span data-stu-id="01530-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="01530-126">数字のみを許可する `FilteredTextBoxExtender` コントロールのマークアップを次に示します (`FilterType="Numbers"`でも可能なもの)。</span><span class="sxs-lookup"><span data-stu-id="01530-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="01530-127">ページを実行し、JavaScript が有効になっている場合は文字を入力しようとすると機能しません。ただし、このページには数字が表示されます。</span><span class="sxs-lookup"><span data-stu-id="01530-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="01530-128">ただし、で提供される保護 `FilteredTextBox` では、"箇条書き" ではないことに注意してください。 JavaScript が有効になっている場合、テキストボックスにデータが入力される可能性があるため、追加の検証方法 (つまり、ASP) を使用する必要があります。NET の検証コントロール。</span><span class="sxs-lookup"><span data-stu-id="01530-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="01530-129">[![数字のみを入力できます](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="01530-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="01530-130">数字のみを入力できます ([クリックすると、フルサイズの画像が表示](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="01530-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="01530-131">[[戻る]](allowing-only-certain-characters-in-a-text-box-cs.md)</span><span class="sxs-lookup"><span data-stu-id="01530-131">[Previous](allowing-only-certain-characters-in-a-text-box-cs.md)</span></span>
