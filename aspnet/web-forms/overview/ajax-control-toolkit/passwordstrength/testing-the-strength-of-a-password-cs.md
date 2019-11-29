---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: パスワードの強度をテストする (C#) |Microsoft Docs
author: wenz
description: パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。 ASP の PasswordStrength 制御。N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598849"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="3de18-104">パスワードの強度をテストする (C#)</span><span class="sxs-lookup"><span data-stu-id="3de18-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="3de18-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="3de18-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3de18-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3de18-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="3de18-107">パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。</span><span class="sxs-lookup"><span data-stu-id="3de18-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="3de18-108">ASP.NET AJAX Control Toolkit の PasswordStrength 制御では、パスワードがどれだけ良好かを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3de18-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="3de18-109">の概要</span><span class="sxs-lookup"><span data-stu-id="3de18-109">Overview</span></span>

<span data-ttu-id="3de18-110">パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。</span><span class="sxs-lookup"><span data-stu-id="3de18-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="3de18-111">ASP.NET AJAX Control Toolkit の `PasswordStrength` コントロールは、パスワードがどれだけ良好かを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3de18-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="3de18-112">手順</span><span class="sxs-lookup"><span data-stu-id="3de18-112">Steps</span></span>

<span data-ttu-id="3de18-113">`PasswordStrength` コントロールによってテキストボックスが拡張され、パスワードが十分であるかどうかがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="3de18-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="3de18-114">属性を使用した豊富なオプションが用意されています。その一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3de18-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="3de18-115">パスワードに必要な数字の最小文字数を `MinimumNumericCharacters` します。</span><span class="sxs-lookup"><span data-stu-id="3de18-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="3de18-116">パスワードに必要な記号 (文字と数字以外) の最小数を `MinimumSymbolCharacters` します。</span><span class="sxs-lookup"><span data-stu-id="3de18-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="3de18-117">パスワードの最小 `PreferredPasswordLength` 長さ</span><span class="sxs-lookup"><span data-stu-id="3de18-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="3de18-118">パスワードが大文字と小文字の両方を使用する必要があるかどうかを `RequiresUpperAndLowerCaseCharacters` する</span><span class="sxs-lookup"><span data-stu-id="3de18-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="3de18-119">`StrengthIndicatorType` には、パスワードの強度をテキスト (値 `"Text"`)、または進行状況バーの種類 (値 `"BarIndicator"`) として表示する方法が記載されています。</span><span class="sxs-lookup"><span data-stu-id="3de18-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="3de18-120">`DisplayPosition` 属性では、情報が表示される場所を構成します。</span><span class="sxs-lookup"><span data-stu-id="3de18-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="3de18-121">ここでは、ASP.NET AJAX `ScriptManager` コントロール、`PasswordStrength` 制御、ユーザーがパスワードを入力するテキストボックスなど、完全な例を示します。</span><span class="sxs-lookup"><span data-stu-id="3de18-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="3de18-122">このデモでは、後者のフォームフィールドは通常のテキストフィールドであり、パスワードフィールドではなく、開発中に入力した内容を確認できるようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="3de18-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="3de18-123">ページを実行して入力し直します: 小文字、大文字、数字、および記号を入力した後にのみ、パスワードは分割されていないと見なされます。</span><span class="sxs-lookup"><span data-stu-id="3de18-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="3de18-124">[現在、パスワードは (非常に) 良い ![](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3de18-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="3de18-125">これで、パスワードが (かなり) 良好になりました ([クリックすると、フルサイズの画像が表示](testing-the-strength-of-a-password-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="3de18-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3de18-126">次へ</span><span class="sxs-lookup"><span data-stu-id="3de18-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
