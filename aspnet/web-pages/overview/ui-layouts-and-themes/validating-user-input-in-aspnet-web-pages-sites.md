---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET Web ページ (Razor) サイトでのユーザー入力の検証Microsoft Docs
author: Rick-Anderson
description: この記事では、ユーザーから取得した情報を検証する方法について説明します。これは、ユーザーがという形式で HTML フォームの有効な情報を入力することを確認するために &mdash; ます。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454300"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="7459f-103">ASP.NET Web ページ (Razor) サイトでのユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="7459f-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="7459f-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7459f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7459f-105">この記事では、ユーザー &mdash; から取得した情報を検証する方法について説明します。つまり、ユーザーが ASP.NET Web ページ (Razor) サイトの HTML フォームに有効な情報を入力していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7459f-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="7459f-106">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="7459f-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7459f-107">ユーザーの入力が定義した検証条件に一致するかどうかを確認する方法。</span><span class="sxs-lookup"><span data-stu-id="7459f-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="7459f-108">すべての検証テストが成功したかどうかを確認する方法。</span><span class="sxs-lookup"><span data-stu-id="7459f-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="7459f-109">検証エラーを表示する方法 (および書式設定方法)。</span><span class="sxs-lookup"><span data-stu-id="7459f-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="7459f-110">ユーザーから直接取得されないデータを検証する方法。</span><span class="sxs-lookup"><span data-stu-id="7459f-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="7459f-111">この記事で紹介する ASP.NET プログラミングの概念は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7459f-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="7459f-112">`Validation` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="7459f-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="7459f-113">`Html.ValidationSummary` メソッドと `Html.ValidationMessage` メソッド。</span><span class="sxs-lookup"><span data-stu-id="7459f-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7459f-114">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7459f-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7459f-115">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="7459f-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="7459f-116">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="7459f-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="7459f-117">このトピックの内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7459f-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="7459f-118">ユーザー入力の検証の概要</span><span class="sxs-lookup"><span data-stu-id="7459f-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="7459f-119">ユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="7459f-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="7459f-120">クライアント側の検証の追加</span><span class="sxs-lookup"><span data-stu-id="7459f-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="7459f-121">検証エラーの書式設定</span><span class="sxs-lookup"><span data-stu-id="7459f-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="7459f-122">ユーザーから直接取得されていないデータの検証</span><span class="sxs-lookup"><span data-stu-id="7459f-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="7459f-123">ユーザー入力の検証の概要</span><span class="sxs-lookup"><span data-stu-id="7459f-123">Overview of User Input Validation</span></span>

<span data-ttu-id="7459f-124">たとえば、フォームに情報を入力するようユーザーに求める場合は、入力した値が有効であることを確認することが重要です。</span><span class="sxs-lookup"><span data-stu-id="7459f-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="7459f-125">たとえば、重要な情報が欠落しているフォームを処理する必要がないとします。</span><span class="sxs-lookup"><span data-stu-id="7459f-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="7459f-126">ユーザーが HTML フォームに値を入力すると、入力した値は文字列になります。</span><span class="sxs-lookup"><span data-stu-id="7459f-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="7459f-127">多くの場合、必要な値は、整数や日付などの他のデータ型です。</span><span class="sxs-lookup"><span data-stu-id="7459f-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="7459f-128">そのため、ユーザーが入力する値を適切なデータ型に正しく変換できることも確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="7459f-129">また、値に特定の制限がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="7459f-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="7459f-130">たとえば、ユーザーが適切に整数を入力したとしても、値が特定の範囲内に収まるようにする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![CSS スタイルクラスを使用する検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="7459f-132">**重要**ユーザー入力の検証は、セキュリティのためにも重要です。</span><span class="sxs-lookup"><span data-stu-id="7459f-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="7459f-133">ユーザーがフォームに入力できる値を制限すると、サイトのセキュリティを損なう可能性のある値をユーザーが入力できる可能性が低くなります。</span><span class="sxs-lookup"><span data-stu-id="7459f-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="7459f-134">ユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="7459f-134">Validating User Input</span></span>

<span data-ttu-id="7459f-135">ASP.NET Web ページ2では、`Validator` ヘルパーを使用してユーザー入力をテストできます。</span><span class="sxs-lookup"><span data-stu-id="7459f-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="7459f-136">基本的な方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7459f-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="7459f-137">検証する入力要素 (フィールド) を決定します。</span><span class="sxs-lookup"><span data-stu-id="7459f-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="7459f-138">通常、フォーム内の `<input>` 要素の値を検証します。</span><span class="sxs-lookup"><span data-stu-id="7459f-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="7459f-139">ただし、`<select>` リストのような制約された要素からの入力も含め、すべての入力を検証することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7459f-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="7459f-140">これにより、ユーザーがページ上のコントロールをバイパスしてフォームを送信しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="7459f-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="7459f-141">ページコードで、`Validation` ヘルパーのメソッドを使用して、各入力要素に対して個別の検証チェックを追加します。</span><span class="sxs-lookup"><span data-stu-id="7459f-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="7459f-142">必須フィールドを確認するには、`Validation.RequireField(field, [error message])` (個々のフィールド) または `Validation.RequireFields(field1, field2, ...))` (フィールドの一覧) を使用します。</span><span class="sxs-lookup"><span data-stu-id="7459f-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="7459f-143">その他の種類の検証については、`Validation.Add(field, ValidationType)`を使用します。</span><span class="sxs-lookup"><span data-stu-id="7459f-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="7459f-144">`ValidationType`には、次のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="7459f-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="7459f-145">ページが送信されたら、`Validation.IsValid`を確認して、検証が成功したかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="7459f-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="7459f-146">検証エラーが発生した場合は、通常のページ処理をスキップします。</span><span class="sxs-lookup"><span data-stu-id="7459f-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="7459f-147">たとえば、ページの目的がデータベースを更新する必要がある場合、すべての検証エラーが修正されるまで、そのような処理は行われません。</span><span class="sxs-lookup"><span data-stu-id="7459f-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="7459f-148">検証エラーが発生した場合は、`Html.ValidationSummary` または `Html.ValidationMessage`、またはその両方を使用して、ページのマークアップにエラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="7459f-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="7459f-149">次の例は、これらの手順を示すページを示しています。</span><span class="sxs-lookup"><span data-stu-id="7459f-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="7459f-150">検証のしくみを確認するには、このページを実行し、意図的に間違いを犯してください。</span><span class="sxs-lookup"><span data-stu-id="7459f-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="7459f-151">たとえば、コース名を入力し忘れた場合に、「」と入力したときに、無効な日付を入力すると、次のようなページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![レンダリングされたページでの検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="7459f-153">クライアント側の検証の追加</span><span class="sxs-lookup"><span data-stu-id="7459f-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="7459f-154">既定では、ユーザーの入力は、ユーザーがページを送信した後に検証されます。つまり、検証はサーバーコードで実行されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="7459f-155">この方法の欠点は、ユーザーがページを送信するまでエラーが発生したことをユーザーが認識していないことです。</span><span class="sxs-lookup"><span data-stu-id="7459f-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="7459f-156">フォームが長い場合や複雑な場合は、ページが送信された後にのみエラーを報告すると、ユーザーにとって不便な場合があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="7459f-157">クライアントスクリプトで検証を実行するためのサポートを追加できます。</span><span class="sxs-lookup"><span data-stu-id="7459f-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="7459f-158">この場合、ユーザーがブラウザーで作業するときに検証が実行されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="7459f-159">たとえば、値が整数であることを指定したとします。</span><span class="sxs-lookup"><span data-stu-id="7459f-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="7459f-160">ユーザーが整数以外の値を入力した場合、ユーザーが入力フィールドを離れるとすぐにエラーが報告されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="7459f-161">ユーザーはすぐにフィードバックを受け取ります。これは便利です。</span><span class="sxs-lookup"><span data-stu-id="7459f-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="7459f-162">クライアントベースの検証では、複数のエラーを修正するために、ユーザーがフォームを送信する必要がある回数を減らすこともできます。</span><span class="sxs-lookup"><span data-stu-id="7459f-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="7459f-163">クライアント側の検証を使用する場合でも、検証はサーバーコードで常に実行されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="7459f-164">サーバーコードでの検証の実行は、ユーザーがクライアントベースの検証を省略した場合のセキュリティ対策です。</span><span class="sxs-lookup"><span data-stu-id="7459f-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="7459f-165">ページに次の JavaScript ライブラリを登録します。</span><span class="sxs-lookup"><span data-stu-id="7459f-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="7459f-166">2つのライブラリは、コンテンツ配信ネットワーク (CDN) から読み込むことができるため、コンピューターまたはサーバーに必ずしも必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="7459f-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="7459f-167">ただし、 *jquery*のローカルコピーを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="7459f-168">ライブラリを含む WebMatrix テンプレート (**スターターサイト**など) をまだ使用していない場合は、 **starter サイト**に基づいた Web ページサイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="7459f-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="7459f-169">次に、 *.js*ファイルを現在のサイトにコピーします。</span><span class="sxs-lookup"><span data-stu-id="7459f-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="7459f-170">マークアップで、検証する要素ごとに `Validation.For(field)`の呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="7459f-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="7459f-171">このメソッドは、クライアント側の検証で使用される属性を出力します。</span><span class="sxs-lookup"><span data-stu-id="7459f-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="7459f-172">(実際の JavaScript コードを出力するのではなく、メソッドは `data-val-...`のような属性を出力します。</span><span class="sxs-lookup"><span data-stu-id="7459f-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="7459f-173">これらの属性は、jQuery を使用して作業を行う控えめなクライアント検証をサポートしています)。</span><span class="sxs-lookup"><span data-stu-id="7459f-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="7459f-174">次のページは、前に示した例にクライアント検証機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7459f-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="7459f-175">すべての検証チェックがクライアントで実行されるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="7459f-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="7459f-176">特に、データ型の検証 (整数、日付など) は、クライアントでは実行されません。</span><span class="sxs-lookup"><span data-stu-id="7459f-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="7459f-177">次のチェックは、クライアントとサーバーの両方で機能します。</span><span class="sxs-lookup"><span data-stu-id="7459f-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="7459f-178">この例では、有効な日付のテストがクライアントコードで機能しません。</span><span class="sxs-lookup"><span data-stu-id="7459f-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="7459f-179">ただし、テストはサーバーコードで実行されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="7459f-180">検証エラーの書式設定</span><span class="sxs-lookup"><span data-stu-id="7459f-180">Formatting Validation Errors</span></span>

<span data-ttu-id="7459f-181">次の予約名を持つ CSS クラスを定義することで、検証エラーを表示する方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="7459f-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="7459f-182">[https://login.microsoftonline.com/consumers/](`field-validation-error`)</span><span class="sxs-lookup"><span data-stu-id="7459f-182">`field-validation-error`.</span></span> <span data-ttu-id="7459f-183">エラーを表示しているときの `Html.ValidationMessage` メソッドの出力を定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="7459f-184">[https://login.microsoftonline.com/consumers/](`field-validation-valid`)</span><span class="sxs-lookup"><span data-stu-id="7459f-184">`field-validation-valid`.</span></span> <span data-ttu-id="7459f-185">エラーがない場合に `Html.ValidationMessage` メソッドの出力を定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="7459f-186">[https://login.microsoftonline.com/consumers/](`input-validation-error`)</span><span class="sxs-lookup"><span data-stu-id="7459f-186">`input-validation-error`.</span></span> <span data-ttu-id="7459f-187">エラーが発生した場合に `<input>` 要素をどのようにレンダリングするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="7459f-188">(たとえば、このクラスを使用すると、&lt;入力&gt; 要素の背景色を、値が無効である場合に別の色に設定できます)。この CSS クラスは、クライアント検証中にのみ使用されます (ASP.NET Web ページ 2)。</span><span class="sxs-lookup"><span data-stu-id="7459f-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="7459f-189">[https://login.microsoftonline.com/consumers/](`input-validation-valid`)</span><span class="sxs-lookup"><span data-stu-id="7459f-189">`input-validation-valid`.</span></span> <span data-ttu-id="7459f-190">エラーがない場合の `<input>` 要素の外観を定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="7459f-191">[https://login.microsoftonline.com/consumers/](`validation-summary-errors`)</span><span class="sxs-lookup"><span data-stu-id="7459f-191">`validation-summary-errors`.</span></span> <span data-ttu-id="7459f-192">エラーの一覧を表示している `Html.ValidationSummary` メソッドの出力を定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="7459f-193">[https://login.microsoftonline.com/consumers/](`validation-summary-valid`)</span><span class="sxs-lookup"><span data-stu-id="7459f-193">`validation-summary-valid`.</span></span> <span data-ttu-id="7459f-194">エラーがない場合に `Html.ValidationSummary` メソッドの出力を定義します。</span><span class="sxs-lookup"><span data-stu-id="7459f-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="7459f-195">次の `<style>` ブロックは、エラー条件のルールを示しています。</span><span class="sxs-lookup"><span data-stu-id="7459f-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="7459f-196">前の記事の例のページにこのスタイルブロックを含めると、エラー表示は次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="7459f-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![CSS スタイルクラスを使用する検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="7459f-198">ASP.NET Web ページ2でクライアント検証を使用していない場合、`<input>` 要素 (`input-validation-error` および `input-validation-valid` の CSS クラスには何の効果もありません。</span><span class="sxs-lookup"><span data-stu-id="7459f-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="7459f-199">静的および動的なエラー表示</span><span class="sxs-lookup"><span data-stu-id="7459f-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="7459f-200">CSS ルールは、`validation-summary-errors` や `validation-summary-valid`など、ペアで提供されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="7459f-201">これらのペアを使用すると、エラー条件と "通常の" (非エラー) 条件の両方の条件に対してルールを定義できます。</span><span class="sxs-lookup"><span data-stu-id="7459f-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="7459f-202">エラーがない場合でも、エラー表示のマークアップは常に表示されることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="7459f-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="7459f-203">たとえば、ページにマークアップに `Html.ValidationSummary` メソッドがある場合、ページが初めて要求されたときでも、ページソースには次のマークアップが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7459f-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="7459f-204">つまり、`Html.ValidationSummary` メソッドは、エラー一覧が空の場合でも、常に `<div>` 要素とリストをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="7459f-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="7459f-205">同様に、`Html.ValidationMessage` メソッドは、エラーがない場合でも、個々のフィールドエラーのプレースホルダーとして `<span>` 要素を常にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="7459f-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="7459f-206">場合によっては、エラーメッセージを表示すると、ページの折り返しが発生し、ページ上の要素が移動する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="7459f-207">`-valid` で終わる CSS 規則を使用すると、この問題を回避するためのレイアウトを定義できます。</span><span class="sxs-lookup"><span data-stu-id="7459f-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="7459f-208">たとえば、`field-validation-error` を定義し、`field-validation-valid` を同じ固定サイズにすることができます。</span><span class="sxs-lookup"><span data-stu-id="7459f-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="7459f-209">このようにして、フィールドの表示領域は静的であり、エラーメッセージが表示されている場合はページフローが変更されません。</span><span class="sxs-lookup"><span data-stu-id="7459f-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="7459f-210">ユーザーから直接取得されていないデータの検証</span><span class="sxs-lookup"><span data-stu-id="7459f-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="7459f-211">場合によっては、HTML フォームから直接取得されない情報を検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="7459f-212">一般的な例としては、次の例のように、クエリ文字列に値が渡されるページがあります。</span><span class="sxs-lookup"><span data-stu-id="7459f-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="7459f-213">この場合、ページに渡された値 (`classid`の値の 1022) が有効であることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="7459f-214">この検証を実行するために `Validation` ヘルパーを直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="7459f-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="7459f-215">ただし、検証エラーメッセージを表示する機能のように、検証システムの他の機能を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="7459f-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7459f-216">**重要**フォームフィールドの値、クエリ文字列の値、cookie の値など、*任意*のソースから取得した値を常に検証します。</span><span class="sxs-lookup"><span data-stu-id="7459f-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="7459f-217">これらの値を簡単に変更できます (悪意のある目的の場合など)。</span><span class="sxs-lookup"><span data-stu-id="7459f-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="7459f-218">アプリケーションを保護するために、これらの値を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7459f-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="7459f-219">次の例は、クエリ文字列で渡される値を検証する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7459f-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="7459f-220">このコードは、値が空ではなく、整数であることをテストします。</span><span class="sxs-lookup"><span data-stu-id="7459f-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="7459f-221">要求がフォーム送信 (`if(!IsPost)`) でない場合は、テストが実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7459f-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="7459f-222">このテストは、ページが初めて要求されたときに合格しますが、要求がフォーム送信の場合は成功しません。</span><span class="sxs-lookup"><span data-stu-id="7459f-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="7459f-223">このエラーを表示するには、`Validation.AddFormError("message")`を呼び出して、エラーを検証エラーの一覧に追加します。</span><span class="sxs-lookup"><span data-stu-id="7459f-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="7459f-224">ページに `Html.ValidationSummary` メソッドの呼び出しが含まれている場合は、ユーザー入力の検証エラーと同様にエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7459f-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="7459f-225">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="7459f-225">Additional Resources</span></span>

[<span data-ttu-id="7459f-226">ASP.NET Web ページサイトでの HTML フォームの操作</span><span class="sxs-lookup"><span data-stu-id="7459f-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
