---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET Web ページ (Razor) サイトでの HTML フォームの操作 |Microsoft Docs
author: Rick-Anderson
description: フォームは、テキストボックス、チェックボックス、オプションボタン、プルダウンリストなどのユーザー入力コントロールを配置する HTML ドキュメントのセクションです。 フォーム wh を使用します。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519604"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="18cb6-104">ASP.NET Web ページ (Razor) サイトでの HTML フォームの操作</span><span class="sxs-lookup"><span data-stu-id="18cb6-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="18cb6-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="18cb6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="18cb6-106">この記事では、ASP.NET Web ページ (Razor) web サイトで作業しているときに HTML フォーム (テキストボックスとボタン) を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="18cb6-107">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="18cb6-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="18cb6-108">HTML フォームを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="18cb6-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="18cb6-109">フォームからユーザー入力を読み取る方法。</span><span class="sxs-lookup"><span data-stu-id="18cb6-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="18cb6-110">ユーザー入力を検証する方法。</span><span class="sxs-lookup"><span data-stu-id="18cb6-110">How to validate user input.</span></span>
> - <span data-ttu-id="18cb6-111">ページの送信後にフォーム値を復元する方法。</span><span class="sxs-lookup"><span data-stu-id="18cb6-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="18cb6-112">この記事で紹介する ASP.NET プログラミングの概念は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="18cb6-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="18cb6-113">`Request` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="18cb6-113">The `Request` object.</span></span>
> - <span data-ttu-id="18cb6-114">入力の検証。</span><span class="sxs-lookup"><span data-stu-id="18cb6-114">Input validation.</span></span>
> - <span data-ttu-id="18cb6-115">HTML エンコード。</span><span class="sxs-lookup"><span data-stu-id="18cb6-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="18cb6-116">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="18cb6-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="18cb6-117">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="18cb6-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="18cb6-118">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="creating-a-simple-html-form"></a><span data-ttu-id="18cb6-119">単純な HTML フォームの作成</span><span class="sxs-lookup"><span data-stu-id="18cb6-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="18cb6-120">新しい web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-120">Create a new website.</span></span>
2. <span data-ttu-id="18cb6-121">ルートフォルダーで、*フォーム cshtml*という名前の web ページを作成し、次のマークアップを入力します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="18cb6-122">ブラウザーでページを起動します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-122">Launch the page in your browser.</span></span> <span data-ttu-id="18cb6-123">(WebMatrix の **[ファイル]** ワークスペースで、ファイルを右クリックし、 **[ブラウザーで起動]** を選択します)。3つの入力フィールドと **[送信]** ボタンを含む単純なフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![3つのテキストボックスがあるフォームのスクリーンショット。](4-working-with-forms/_static/image1.png)

    <span data-ttu-id="18cb6-125">この時点で、 **[送信]** ボタンをクリックしても何も起こりません。</span><span class="sxs-lookup"><span data-stu-id="18cb6-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="18cb6-126">フォームを使いやすくするには、サーバーで実行するコードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="18cb6-127">フォームからのユーザー入力の読み取り</span><span class="sxs-lookup"><span data-stu-id="18cb6-127">Reading User Input from the Form</span></span>

<span data-ttu-id="18cb6-128">フォームを処理するには、送信されたフィールド値を読み取り、それらの値を処理するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="18cb6-129">この手順では、フィールドを読み取り、ユーザー入力をページに表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="18cb6-130">(実稼働アプリケーションでは、通常、ユーザー入力を使用してより興味深いものを実行します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="18cb6-131">これは、データベースの操作に関する記事で説明されています。)</span><span class="sxs-lookup"><span data-stu-id="18cb6-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="18cb6-132">*フォームの cshtml*ファイルの先頭に、次のコードを入力します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="18cb6-133">ユーザーが最初にページを要求すると、空のフォームのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="18cb6-134">フォームにユーザーが入力し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="18cb6-135">これにより、ユーザー入力がサーバーに送信 (投稿) されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="18cb6-136">既定では、要求は同じページ (つまり、 *cshtml*) に送られます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="18cb6-137">この時点でページを送信すると、入力した値がフォームのすぐ上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![入力した値がページに表示されるスクリーンショット。](4-working-with-forms/_static/image2.png)

    <span data-ttu-id="18cb6-139">ページのコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-139">Look at the code for the page.</span></span> <span data-ttu-id="18cb6-140">まず、`IsPost` メソッドを使用して、ページがポスト&#8212;されているかどうかを確認します。これは、ユーザーが **[送信]** ボタンをクリックしたかどうかによって決まります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="18cb6-141">これが post の場合、`IsPost` は true を返します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="18cb6-142">これは、初期要求 (GET 要求) とポストバック (POST 要求) のどちらを使用しているかを判断するために ASP.NET Web ページでの標準的な方法です。</span><span class="sxs-lookup"><span data-stu-id="18cb6-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="18cb6-143">(GET と POST の詳細については、「 [Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)」の「HTTP GET and post」と「IsPost プロパティ」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="18cb6-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="18cb6-144">次に、ユーザーが `Request.Form` オブジェクトから入力した値を取得し、後で変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="18cb6-145">`Request.Form` オブジェクトには、ページで送信されたすべての値が含まれます。各値はキーによって識別されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="18cb6-146">キーは、読み取るフォームフィールドの `name` 属性に相当します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="18cb6-147">たとえば、`companyname` フィールド (テキストボックス) を読み取るには、`Request.Form["companyname"]`を使用します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="18cb6-148">フォーム値は、`Request.Form` オブジェクトに文字列として格納されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="18cb6-149">したがって、数値、日付、またはその他の型として値を操作する必要がある場合は、文字列からその型に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="18cb6-150">この例では、`Request.Form` の `AsInt` メソッドを使用して、employees フィールド (従業員数を含む) の値を整数に変換します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="18cb6-151">ブラウザーでページを起動し、フォームのフィールドに入力して、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="18cb6-152">このページには、入力した値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="18cb6-153">外観とセキュリティのための HTML エンコード</span><span class="sxs-lookup"><span data-stu-id="18cb6-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="18cb6-154">HTML には、`<`、`>`、`&`などの文字が特別に使用されています。</span><span class="sxs-lookup"><span data-stu-id="18cb6-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="18cb6-155">これらの特殊文字が想定されていない場所に出現すると、web ページの外観と機能が無駄になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="18cb6-156">たとえば、ブラウザーは、`<b>` または `<input ...>`のように、HTML 要素の先頭として `<` 文字 (後にスペースがある場合を除く) を解釈します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="18cb6-157">ブラウザーが要素を認識しない場合は、`<` で始まる文字列を破棄するだけで、再度認識されるようになります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="18cb6-158">当然ながら、これによってページに外観が変わってしまう可能性があります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="18cb6-159">HTML エンコーディングでは、これらの予約文字は、ブラウザーが正しいシンボルとして解釈するコードに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="18cb6-160">たとえば、`<` 文字は `&lt;` に置き換えられ、`>` 文字は `&gt;`に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="18cb6-161">ブラウザーでは、表示する文字としてこれらの置換文字列がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="18cb6-162">ユーザーから返された文字列 (入力) を表示するときは常に HTML エンコーディングを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="18cb6-163">そうしないと、ユーザーは、悪意のあるスクリプトを実行したり、サイトのセキュリティを侵害したり、意図したものではないものを実行したりするために web ページを取得しようとすることができます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="18cb6-164">(これは、ユーザーの入力を取得し、その場所を保存した後、ブログ&#8212;コメントやユーザーのレビューなどのように後で表示する場合に特に重要です)。</span><span class="sxs-lookup"><span data-stu-id="18cb6-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="18cb6-165">これらの問題を回避するために、ASP.NET Web ページは、コードから出力されたテキストコンテンツを自動的に HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="18cb6-166">たとえば、`@MyVar`などのコードを使用して変数または式の内容を表示すると、ASP.NET Web ページによって出力が自動的にエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>

## <a name="validating-user-input"></a><span data-ttu-id="18cb6-167">ユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="18cb6-167">Validating User Input</span></span>

<span data-ttu-id="18cb6-168">ユーザーは間違いを犯してしまいます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-168">Users make mistakes.</span></span> <span data-ttu-id="18cb6-169">フィールドに入力するように要求したときに、忘れた場合、または従業員の数を入力するように依頼した場合は、代わりに名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="18cb6-170">フォームを処理する前に正しく入力されていることを確認するには、ユーザーの入力を検証します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="18cb6-171">この手順では、3つのフォームフィールドをすべて検証して、ユーザーがそれらを空白のままにしていないことを確認する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="18cb6-172">また、employee count の値が数値であることも確認します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="18cb6-173">エラーが発生した場合は、検証に合格しなかった値をユーザーに通知するエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="18cb6-174">フォームの*cshtml*ファイルで、最初のコードブロックを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="18cb6-175">ユーザー入力を検証するには、`Validation` ヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="18cb6-176">`Validation.RequireField`を呼び出すことによって、必要なフィールドを登録します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="18cb6-177">`Validation.Add` を呼び出し、検証するフィールドと実行する検証の種類を指定することによって、他の種類の検証を登録します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="18cb6-178">ページを実行すると、ASP.NET によってすべての検証が行われます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="18cb6-179">結果を確認するには、`Validation.IsValid`を呼び出します。これにより、すべての値が渡された場合は true が返され、検証に失敗した場合は false が返されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="18cb6-180">通常は、ユーザー入力に対して処理を実行する前に `Validation.IsValid` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="18cb6-181">次のように、`Html.ValidationMessage` メソッドに3つの呼び出しを追加して、`<body>` 要素を更新します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="18cb6-182">検証エラーメッセージを表示するには、Html.`ValidationMessage` を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="18cb6-183">メッセージに必要なフィールドの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="18cb6-184">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-184">Run the page.</span></span> <span data-ttu-id="18cb6-185">フィールドを空白のままにして、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="18cb6-186">エラーメッセージが表示できます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-186">You see error messages.</span></span>

    ![ユーザー入力が検証に合格しない場合に表示されるエラーメッセージを示すスクリーンショット。](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="18cb6-188">"ABC" などの文字列を " **Employee Count** " フィールドに追加し、もう一度 **[Submit]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="18cb6-189">今回は、文字列が正しい形式ではないことを示すエラーが表示されます。つまり、整数です。</span><span class="sxs-lookup"><span data-stu-id="18cb6-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![ユーザーが従業員フィールドに文字列を入力した場合に表示されるエラーメッセージを示すスクリーンショット。](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="18cb6-191">ASP.NET Web ページには、ユーザーの入力を検証するためのオプションが多数用意されています。たとえば、クライアントスクリプトを使用して自動的に検証を実行し、ユーザーがブラウザーですぐにフィードバックを取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="18cb6-192">詳細については、後の「[その他のリソース](#Additional_Resources)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="18cb6-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="18cb6-193">ポストバック後のフォーム値の復元</span><span class="sxs-lookup"><span data-stu-id="18cb6-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="18cb6-194">前のセクションのページをテストしたときに、検証エラーが発生した場合は (無効なデータだけでなく) 入力したものがすべて削除され、すべてのフィールドの値を再入力する必要があることがわかります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="18cb6-195">これは重要な点を示しています。ページを送信し、処理した後、再度ページを表示すると、ページがゼロから再作成されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="18cb6-196">ご覧のとおり、これは、送信時にページ内にあったすべての値が失われることを意味します。</span><span class="sxs-lookup"><span data-stu-id="18cb6-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="18cb6-197">ただし、これは簡単に修正できます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-197">You can fix this easily, however.</span></span> <span data-ttu-id="18cb6-198">送信された値 (`Request.Form` オブジェクト内) にアクセスできるため、ページを表示するときにこれらの値をフォームフィールドに戻すことができます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="18cb6-199">フォームの*cshtml*ファイルで、`value` 属性を使用して、`<input>` 要素の `value` 属性を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="18cb6-200">`<input>` 要素の `value` 属性は、`Request.Form` オブジェクトからフィールド値を動的に読み取るように設定されています。</span><span class="sxs-lookup"><span data-stu-id="18cb6-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="18cb6-201">ページが初めて要求されたときは、`Request.Form` オブジェクトの値がすべて空になります。</span><span class="sxs-lookup"><span data-stu-id="18cb6-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="18cb6-202">これは、フォームが空白であるため、問題ありません。</span><span class="sxs-lookup"><span data-stu-id="18cb6-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="18cb6-203">ブラウザーでページを起動し、フォームフィールドに入力するか、空白のままにして、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="18cb6-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="18cb6-204">送信された値を表示するページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="18cb6-204">A page that shows the submitted values is displayed.</span></span>

    ![フォーム-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="18cb6-206">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="18cb6-206">Additional Resources</span></span>

- [<span data-ttu-id="18cb6-207">1001 Web ユーザーから入力を取得する方法</span><span class="sxs-lookup"><span data-stu-id="18cb6-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/library/ms971057.aspx)
- <span data-ttu-id="18cb6-208">[フォームを使用してユーザー入力を処理する](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="18cb6-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="18cb6-209">ASP.NET Web ページにおけるユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="18cb6-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="18cb6-210">[HTML フォームでのオートコンプリートの使用](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="18cb6-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span></span>
