---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 構文を使用した ASP.NET Web プログラミングの概要 (Visual Basic) |Microsoft Docs
author: Rick-Anderson
description: この付録概要 ASP.NET Web ページを使用したプログラミングの Visual Basic で Razor 構文を使用します。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422662"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="4c6ea-103">Razor 構文 (Visual Basic) を使用した ASP.NET Web プログラミングの概要 (英語)</span><span class="sxs-lookup"><span data-stu-id="4c6ea-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="4c6ea-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4c6ea-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4c6ea-105">この記事では、Razor 構文と Visual Basic を使用した ASP.NET Web ページによるプログラミングの概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="4c6ea-106">ASP.NETは、Webサーバーで動的な Web ページを運用するためのマイクロソフトの技術です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="4c6ea-107">**学習内容**:</span><span class="sxs-lookup"><span data-stu-id="4c6ea-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="4c6ea-108">Razor構文を使ったASP.NET Webページのプログラミングをはじめるための上位8つのプログラミング Tips</span><span class="sxs-lookup"><span data-stu-id="4c6ea-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="4c6ea-109">必要とする基本的なプログラミング概念</span><span class="sxs-lookup"><span data-stu-id="4c6ea-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="4c6ea-110">ASP.NETサーバーコードとRazor構文に関する全体像</span><span class="sxs-lookup"><span data-stu-id="4c6ea-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="4c6ea-111">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="4c6ea-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="4c6ea-112">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="4c6ea-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="4c6ea-113">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="4c6ea-114">Razor 構文を使用する ASP.NET Web ページを使用するほとんどの例は C# を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="4c6ea-115">ただし、Razor 構文も Visual Basic をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="4c6ea-116">Visual Basic で ASP.NET web ページをプログラミングするには、拡張子が*vbhtml*の web ページを作成し、Visual Basic コードを追加します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="4c6ea-117">この記事では、ASP.NET の Web ページを作成するための Visual Basic 言語と構文の使用方法の概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="4c6ea-118">Microsoft WebMatrix の既定の web サイトテンプレート (**ケーキ屋さん**、**フォトギャラリー**、および**スターターサイト**など) は、および Visual Basic C#バージョンで使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="4c6ea-119">Visual Basic テンプレートを NuGet パッケージとしてインストールできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="4c6ea-120">Web サイトテンプレートは、サイトのルートフォルダーに*Microsoft templates*という名前のフォルダーにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="4c6ea-121">8 つのプログラミング Tips</span><span class="sxs-lookup"><span data-stu-id="4c6ea-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="4c6ea-122">このセクションでは、Razor 構文を使用して ASP.NET サーバーコードの記述を開始するときに理解しておく必要があるいくつかのヒントを示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="4c6ea-123">1. @ 文字を使用してコードをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="4c6ea-124">`@` 文字は、インライン式、単一ステートメントブロック、および複数ステートメントブロックを開始します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="4c6ea-125">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="4c6ea-127">**HTML エンコード**</span><span class="sxs-lookup"><span data-stu-id="4c6ea-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="4c6ea-128">前の例のように `@` 文字を使用してページにコンテンツを表示すると、ASP.NET は出力を HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="4c6ea-129">これにより、予約された HTML 文字 (`<`、`>` や `&`など) が、HTML タグまたはエンティティとして解釈されるのではなく、web ページに文字として表示されるようにするコードに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="4c6ea-130">HTML エンコードを使用しないと、サーバーコードからの出力が正しく表示されず、ページがセキュリティ上のリスクにさらされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="4c6ea-131">タグをマークアップとしてレンダリングする HTML マークアップを出力することが目的である場合 (たとえば、段落や `<em></em>` テキストを強調するための `<p></p>`)、この記事で後述する「[コードブロック内のテキスト、マークアップ、およびコードの結合](#BM_CombiningTextMarkupAndCode)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="4c6ea-132">Html エンコードの詳細については、 [ASP.NET Web ページサイトでの Html フォームの操作](https://go.microsoft.com/fwlink/?LinkId=202892)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="4c6ea-133">2. コードブロックをコードで囲みます...終了コード</span><span class="sxs-lookup"><span data-stu-id="4c6ea-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="4c6ea-134">コードブロックには1つ以上のコードステートメントが含まれており、キーワード `Code` と `End Code`で囲まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="4c6ea-135">開始 `Code` キーワードは、`@` 文字&#8212;の直後に配置することはできません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="4c6ea-136">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="4c6ea-138">3. ブロック内では、各コードステートメントを改行で終了します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="4c6ea-139">Visual Basic コードブロックでは、各ステートメントは改行で終了します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="4c6ea-140">(この記事の後半では、必要に応じて長いコードステートメントを複数の行にラップする方法を説明しています)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="4c6ea-141">4. 変数を使用して値を格納する</span><span class="sxs-lookup"><span data-stu-id="4c6ea-141">4. You use variables to store values</span></span>

<span data-ttu-id="4c6ea-142">文字列、数値、日付など、*変数*に値を格納することができます。新しい変数を作成するには、`Dim` キーワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="4c6ea-143">`@`を使用して、変数の値をページに直接挿入できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="4c6ea-144">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="4c6ea-146">5. リテラル文字列値を二重引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="4c6ea-147">*文字列*は、テキストとして扱われる文字のシーケンスです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="4c6ea-148">文字列を指定するには、ダブル クォーテーション記号で囲みます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="4c6ea-149">文字列値の中に二重引用符を埋め込むには、2つの二重引用符文字を挿入します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="4c6ea-150">ページ出力に二重引用符文字を1回だけ表示する場合は、引用符で囲まれた文字列内の `""` として入力します。2回表示する場合は、引用符で囲まれた文字列内の `""""` として入力します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="4c6ea-151">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="4c6ea-153">6. Visual Basic コードでは大文字と小文字が区別されない</span><span class="sxs-lookup"><span data-stu-id="4c6ea-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="4c6ea-154">Visual Basic 言語では大文字と小文字が区別されません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="4c6ea-155">プログラミングキーワード (`Dim`、`If`、`True`など) と変数名 (`myString`、`subTotal`など) は、どのような場合でも記述できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="4c6ea-156">次のコード行では、小文字の名前を使用して `lastname` 変数に値を代入し、大文字の名前を使用して変数の値をページに出力します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="4c6ea-157">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="4c6ea-159">7. コーディングの多くは、オブジェクトの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="4c6ea-160">オブジェクトは、ページ、テキストボックス、ファイル、 &#8212;画像、web 要求、電子メールメッセージ、顧客レコード (データベース行) などを使用してプログラミングできることを表します。オブジェクトにはプロパティ&#8212;があり、テキストボックスオブジェクトには `Text` プロパティがあり、要求オブジェクトにはプロパティが `Url`、電子メールメッセージには `From` プロパティがあり、customer オブジェクトには `FirstName` プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="4c6ea-161">オブジェクトには、実行できる&quot; &quot;動詞であるメソッドもあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="4c6ea-162">例としては、ファイルオブジェクトの `Save` メソッド、イメージオブジェクトの `Rotate` メソッド、電子メールオブジェクトの `Send` メソッドなどがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="4c6ea-163">多くの場合、`Request` オブジェクトを使用します。これにより、ページ上のフォームフィールドの値 (テキストボックスなど)、要求を行ったブラウザーの種類、ページの URL、ユーザー id などの情報が得られます。この例では、`Request` オブジェクトのプロパティにアクセスする方法と、`Request` オブジェクトの `MapPath` メソッドを呼び出す方法を示します。これにより、サーバー上のページの絶対パスが得られます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="4c6ea-164">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="4c6ea-166">8. 決定を行うコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="4c6ea-167">動的 web ページの重要な機能は、条件に基づいて何を行うかを決定できることです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="4c6ea-168">これを行う最も一般的な方法は、`If` ステートメント (および省略可能な `Else` ステートメント) を使用することです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="4c6ea-169">ステートメント `If IsPost` は、`If IsPost = True`を簡単に記述する方法です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="4c6ea-170">`If` ステートメントと共に、条件のテスト、コードブロックの繰り返しなど、さまざまな方法があります。これについては、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="4c6ea-171">ブラウザーに表示される結果 ( **[送信]** をクリックした後):</span><span class="sxs-lookup"><span data-stu-id="4c6ea-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="4c6ea-173">**HTTP GET メソッドと POST メソッド、および IsPost プロパティ**</span><span class="sxs-lookup"><span data-stu-id="4c6ea-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="4c6ea-174">Web ページ (HTTP) に使用されるプロトコルでは、サーバーへの要求を行うために使用されるメソッド (&quot;動詞&quot;) の数が制限されています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="4c6ea-175">最も一般的な2つの方法は、ページの読み取りに使用される GET と、ページの送信に使用される POST です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="4c6ea-176">一般に、ユーザーが初めてページを要求したときは、GET を使用してページが要求されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="4c6ea-177">ユーザーがフォームに入力して **[送信]** をクリックすると、ブラウザーはサーバーに POST 要求を行います。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="4c6ea-178">Web プログラミングでは、ページの処理方法を把握できるように、ページが GET として要求されているのか、または投稿として要求されているのかを知ることが役に立つことがよくあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="4c6ea-179">ASP.NET Web ページでは、`IsPost` プロパティを使用して、要求が GET または POST のどちらであるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="4c6ea-180">要求が POST の場合、`IsPost` プロパティは true を返し、フォームのテキストボックスの値を読み取るなどの操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="4c6ea-181">多くの例では、`IsPost`の値に応じて、ページを異なる方法で処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="4c6ea-182">単純なコード例</span><span class="sxs-lookup"><span data-stu-id="4c6ea-182">A Simple Code Example</span></span>

<span data-ttu-id="4c6ea-183">この手順では、基本的なプログラミング手法を示すページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="4c6ea-184">この例では、ユーザーが2つの数値を入力できるページを作成し、それらを追加して結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="4c6ea-185">エディターで、新しいファイルを作成し、「 *Addnumbers. vbhtml*」という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="4c6ea-186">次のコードとマークアップをページにコピーして、ページに既に存在するものを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="4c6ea-187">ここでは、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="4c6ea-188">`@` 文字は、ページ内の最初のコードブロックを開始し、最後の近くに埋め込まれた `totalMessage` 変数の前に置かれます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="4c6ea-189">ページの上部にあるブロックは `Code...End Code`で囲まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="4c6ea-190">変数 `total`、`num1`、`num2`、および `totalMessage` には、いくつかの数値と文字列が格納されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="4c6ea-191">`totalMessage` 変数に代入されたリテラル文字列値は、二重引用符で囲まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="4c6ea-192">Visual Basic コードでは大文字と小文字が区別されないため、ページの下部付近で `totalMessage` 変数が使用されている場合、その名前はページの先頭にある変数宣言のスペルと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="4c6ea-193">大文字と小文字は区別されません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="4c6ea-194">式 `num1.AsInt()` + `num2.AsInt()` オブジェクトとメソッドの操作方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="4c6ea-195">各変数の `AsInt` メソッドは、ユーザーが入力した文字列を、追加できる整数 (整数) に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="4c6ea-196">`<form>` タグには、`method="post"` 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="4c6ea-197">これにより、ユーザーが **[追加]** をクリックしたときに、HTTP POST メソッドを使用してページがサーバーに送信されることを指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="4c6ea-198">ページが送信されると、コード `If IsPost` が true に評価され、条件コードが実行されて、数値を加算した結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="4c6ea-199">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="4c6ea-200">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。2つの整数を入力し、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="4c6ea-202">Visual Basic 言語と構文</span><span class="sxs-lookup"><span data-stu-id="4c6ea-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="4c6ea-203">前に、ASP.NET web ページを作成する方法の基本的な例と、HTML マークアップにサーバーコードを追加する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="4c6ea-204">ここでは、Visual Basic を使用して、プログラミング言語の規則である Razor 構文&#8212;を使用して ASP.NET サーバーコードを記述する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="4c6ea-205">(特に C、C++、C#、Visual Basic、または JavaScript を使用した) 場合のプログラミング経験豊富な場合は、ここで読んだの多くが使い慣れたになります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="4c6ea-206">場合によっては、WebMatrix コードを*vbhtml*ファイルのマークアップに追加する方法についてのみ理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="4c6ea-207">コードブロック内のテキスト、マークアップ、およびコードの結合</span><span class="sxs-lookup"><span data-stu-id="4c6ea-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="4c6ea-208">サーバーコードブロックでは、多くの場合、テキストとマークアップをページに出力します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="4c6ea-209">サーバーコードブロックにコード以外のテキストが含まれていて、そのテキストをそのように表示する必要がある場合、ASP.NET はそのテキストをコードから区別できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="4c6ea-210">これにはいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-210">There are several ways to do this.</span></span>

- <span data-ttu-id="4c6ea-211">テキストは、`<p></p>` や `<em></em>`などの HTML ブロック要素で囲みます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="4c6ea-212">HTML 要素には、テキスト、追加の HTML 要素、およびサーバーコード式を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="4c6ea-213">ASP.NET が HTML の開始タグ (`<p>`など) を認識すると、要素とその内容をすべてブラウザーに表示します (サーバーコード式を解決します)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="4c6ea-214">`@:` 演算子または `<text>` 要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="4c6ea-215">`@:` は、プレーンテキストまたは一致しない HTML タグを含む1行のコンテンツを出力します。`<text>` 要素は、出力に複数の行を囲みます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="4c6ea-216">これらのオプションは、HTML 要素を出力の一部としてレンダリングしない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="4c6ea-217">次の例では、前の例を繰り返しますが、1組の `<text>` タグを使用して、表示するテキストを囲みます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="4c6ea-218">次の例では、`<text>` タグと `</text>` タグによって3つの行が囲まれています。これらの行には、非包含テキストと一致しない HTML タグ (`<br />`) と、サーバーコードおよび一致した HTML タグがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="4c6ea-219">繰り返しになりますが、各行の前に `@:` 演算子を使用することもできます。どちらの方法でも動作します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="4c6ea-220">HTML 要素を使用して、このセクション&#8212;に示すようにテキストを出力する場合、`@:` 演算子、 &#8212;または `<text>` 要素 ASP.NET は、出力を html エンコードしません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="4c6ea-221">(前述のように、ASP.NET は、このセクションに記載されている特殊なケースを除き、`@`の前にあるサーバーコード式とサーバーコードブロックの出力をエンコードします)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="4c6ea-222">空白文字</span><span class="sxs-lookup"><span data-stu-id="4c6ea-222">Whitespace</span></span>

<span data-ttu-id="4c6ea-223">ステートメント内の余分なスペース (および文字列リテラルの外部) は、ステートメントに影響しません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="4c6ea-224">長いステートメントを複数行に分割する</span><span class="sxs-lookup"><span data-stu-id="4c6ea-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="4c6ea-225">長いコードステートメントを複数の行に分割するには、各コード行の後にアンダースコア文字 `_` (Visual Basic は*継続文字*と呼ばれます) を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="4c6ea-226">ステートメントを次の行に分割するには、行の末尾でスペースと継続文字を追加します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="4c6ea-227">次の行でステートメントを続行します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-227">Continue the statement on the next line.</span></span> <span data-ttu-id="4c6ea-228">ステートメントは、読みやすさを向上させるために必要な数の行にラップすることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="4c6ea-229">次の 2 つのステートメントでは同じ結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="4c6ea-230">ただし、文字列リテラルの途中では、行をラップすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="4c6ea-231">次の例は機能しません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="4c6ea-232">上のコードのように、折り返される長い文字列を複数の行に結合するには、*連結演算子*(`&`) を使用する必要があります。これについては、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="4c6ea-233">コードコメント</span><span class="sxs-lookup"><span data-stu-id="4c6ea-233">Code comments</span></span>

<span data-ttu-id="4c6ea-234">コメントを使用すると、自分や他のユーザーにメモを残すことができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="4c6ea-235">Razor 構文のコメントの先頭には `@*` が付き、`*@`で終わります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="4c6ea-236">コードブロック内では、Razor 構文コメントを使用することも、通常の Visual Basic コメント文字を使用することもできます。これは、各行の先頭に単一引用符 (`'`) を付けたものです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="4c6ea-237">変数:</span><span class="sxs-lookup"><span data-stu-id="4c6ea-237">Variables</span></span>

<span data-ttu-id="4c6ea-238">変数は、データを格納するために使用する名前付きオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="4c6ea-239">変数には任意の名前を指定できますが、名前の先頭には英字を使用する必要があり、空白や予約文字を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="4c6ea-240">Visual Basic で、前に説明したように、変数名の文字の大文字と小文字は関係ありません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="4c6ea-241">変数とデータ型</span><span class="sxs-lookup"><span data-stu-id="4c6ea-241">Variables and data types</span></span>

<span data-ttu-id="4c6ea-242">変数には、変数に格納されているデータの種類を示す特定のデータ型を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="4c6ea-243">文字列値 (&quot;Hello world&quot;など) を格納する文字列変数、整数値 (3 や79など) を格納する整数変数、および日付値をさまざまな形式で格納する日付変数 (4/12/2012 や2009など) を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="4c6ea-244">他にもさまざまなデータ型を使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="4c6ea-245">ただし、変数の型を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="4c6ea-246">ほとんどの場合、ASP.NET は変数のデータがどのように使用されているかに基づいて型を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="4c6ea-247">(場合によっては、型を指定する必要があります。これが当てはまる例があります)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="4c6ea-248">型を指定せずに変数を宣言するには、`Dim` と変数名 (たとえば、`Dim myVar`) を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="4c6ea-249">型の変数を宣言するには、`Dim` を使用し、変数名の後に `As` を指定してから、型名 (たとえば、`Dim myVar As String`) を指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="4c6ea-250">次の例は、web ページの変数を使用するインライン式を示しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="4c6ea-251">結果がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="4c6ea-253">データ型の変換とテスト</span><span class="sxs-lookup"><span data-stu-id="4c6ea-253">Converting and testing data types</span></span>

<span data-ttu-id="4c6ea-254">ASP.NET は通常、データ型を自動的に判断することができますが、できないことがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="4c6ea-255">そのため、明示的な変換を実行して ASP.NET を解決することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="4c6ea-256">型を変換する必要がない場合でも、使用している可能性のあるデータの種類を確認するためにテストすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="4c6ea-257">最も一般的なケースは、文字列を別の型 (整数や日付など) に変換する必要がある場合です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="4c6ea-258">次の例は、文字列を数値に変換する必要がある一般的なケースを示しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="4c6ea-259">規則として、ユーザーの入力は文字列として取得されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="4c6ea-260">数値を入力するように求められていても、数字を入力した場合でも、ユーザー入力が送信され、コードで読み取られた場合でも、データは文字列形式になります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="4c6ea-261">したがって、文字列を数値に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="4c6ea-262">この例では、変換せずに値に対して算術演算を実行しようとすると、ASP.NET は2つの文字列を追加できないため、次のエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="4c6ea-263">値を整数に変換するには、`AsInt` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="4c6ea-264">変換が成功した場合は、数値を追加できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="4c6ea-265">次の表に、変数の一般的な変換メソッドとテストメソッドの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="4c6ea-266"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-267"><strong>説明</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-268"><strong>例</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-269">整数 (&quot;593&quot;など) を表す文字列を整数に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-270">&quot;true&quot; のような文字列または false&quot; &quot;ブール型に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-271">&quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を浮動小数点数に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-272">&quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を10進数に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="4c6ea-273">(ASP.NET では、10進数は浮動小数点数よりも正確です)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-274">日付と時刻の値を表す文字列を ASP.NET `DateTime` 型に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-275">その他のデータ型を文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="4c6ea-276">オペレーター</span><span class="sxs-lookup"><span data-stu-id="4c6ea-276">Operators</span></span>

<span data-ttu-id="4c6ea-277">演算子は、式で実行するコマンドの種類を ASP.NET に指示するキーワードまたは文字です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="4c6ea-278">Visual Basic は多くの演算子をサポートしていますが、ASP.NET web ページの開発を開始するには、いくつかのことを理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="4c6ea-279">次の表は、最も一般的な演算子をまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="4c6ea-280"><strong>[オペレーター]</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-281"><strong>説明</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-282"><strong>使用例</strong></span><span class="sxs-lookup"><span data-stu-id="4c6ea-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-283">数値式で使用される算術演算子。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-283">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-284">代入と等値。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-284">Assignment and equality.</span></span> <span data-ttu-id="4c6ea-285">コンテキストによっては、ステートメントの右側の値が左側のオブジェクトに割り当てられるか、値が等しいかどうかがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-286">非等値。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-286">Inequality.</span></span> <span data-ttu-id="4c6ea-287">値が等しくない場合は `True` を返します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-287">Returns `True` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-288">より小さい、より大きい、より小さい、または等しい。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-289">連結。文字列を結合するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-289">Concatenation, which is used to join strings.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-290">インクリメント演算子とデクリメント演算子。変数から 1 (それぞれ) を加算して減算します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-291">.Dot.</span><span class="sxs-lookup"><span data-stu-id="4c6ea-291">Dot.</span></span> <span data-ttu-id="4c6ea-292">オブジェクトとそのプロパティおよびメソッドを区別するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-292">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-293">内側.</span><span class="sxs-lookup"><span data-stu-id="4c6ea-293">Parentheses.</span></span> <span data-ttu-id="4c6ea-294">式をグループ化したり、メソッドにパラメーターを渡したり、配列やコレクションのメンバーにアクセスしたりするために使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-295">じゃない。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-295">Not.</span></span> <span data-ttu-id="4c6ea-296">True の値を false に、またはその逆を反転します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="4c6ea-297">通常、`False` をテストするための簡単な方法として使用されます (つまり、`True`ではありません)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        <span data-ttu-id="4c6ea-298">論理 AND および OR。条件を相互にリンクするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="4c6ea-299">コードでのファイルとフォルダーのパスの操作</span><span class="sxs-lookup"><span data-stu-id="4c6ea-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="4c6ea-300">多くの場合、コードでファイルとフォルダーのパスを操作します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="4c6ea-301">開発用コンピューターに表示される web サイトの物理フォルダー構造の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="4c6ea-302">Url とパスに関する重要な詳細情報を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="4c6ea-303">URL は、ドメイン名 (`http://www.example.com`) またはサーバー名 (`http://localhost`、`http://mycomputer`) のいずれかで始まります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="4c6ea-304">URL は、ホストコンピューターの物理パスに対応します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="4c6ea-305">たとえば、`http://myserver` は、サーバー上の*C:\websites\mywebsite*フォルダーに対応している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="4c6ea-306">仮想パスは、完全パスを指定しなくてもコード内のパスを表す短縮形です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="4c6ea-307">これには、ドメイン名またはサーバー名の後の URL の部分が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="4c6ea-308">仮想パスを使用すると、パスを更新しなくてもコードを別のドメインまたはサーバーに移動できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="4c6ea-309">相違点を理解するための例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="4c6ea-310">完全な URL</span><span class="sxs-lookup"><span data-stu-id="4c6ea-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="4c6ea-311">サーバー名</span><span class="sxs-lookup"><span data-stu-id="4c6ea-311">Server name</span></span> | <span data-ttu-id="4c6ea-312">*my企業サーバー*</span><span class="sxs-lookup"><span data-stu-id="4c6ea-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="4c6ea-313">[仮想パス]</span><span class="sxs-lookup"><span data-stu-id="4c6ea-313">Virtual path</span></span> | <span data-ttu-id="4c6ea-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="4c6ea-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="4c6ea-315">物理パス</span><span class="sxs-lookup"><span data-stu-id="4c6ea-315">Physical path</span></span> | <span data-ttu-id="4c6ea-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="4c6ea-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="4c6ea-317">仮想ルートは/です。 C: ドライブのルートと同じです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="4c6ea-318">(仮想フォルダーパスは常にスラッシュを使用します)。フォルダーの仮想パスは、物理フォルダーと同じ名前である必要はありません。エイリアスにすることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="4c6ea-319">(実稼働サーバーでは、仮想パスが正確な物理パスと一致することはほとんどありません)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="4c6ea-320">コード内でファイルやフォルダーを操作するときに、使用しているオブジェクトに応じて、物理パスと仮想パスを参照することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="4c6ea-321">ASP.NET には、コード内のファイルとフォルダーのパスを操作するためのツールが用意されています。 `Server.MapPath` メソッド、`~` 演算子、および `Href` メソッドです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="4c6ea-322">仮想パスから物理パスへの変換: サーバーの MapPath メソッド</span><span class="sxs-lookup"><span data-stu-id="4c6ea-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="4c6ea-323">`Server.MapPath` メソッドは、仮想パス (C:\WebSites\MyWebSiteFolder\default.cshtml など *)* を絶対物理パス (たとえば、) に変換します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="4c6ea-324">この方法は、完全な物理パスが必要な場合にいつでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="4c6ea-325">一般的な例として、web サーバー上のテキストファイルまたはイメージファイルを読み取ったり書き込んだりする場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="4c6ea-326">通常、ホストサイトのサーバー上にあるサイトの絶対物理パスがわからないため、この方法では、既知のパス (仮想パス) をサーバー上の対応するパスに変換できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="4c6ea-327">ファイルまたはフォルダーへの仮想パスをメソッドに渡し、物理パスを返します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="4c6ea-328">仮想ルートの参照: ~ 演算子と Href メソッド</span><span class="sxs-lookup"><span data-stu-id="4c6ea-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="4c6ea-329">*Cshtml*ファイルまたは*vbhtml*ファイルでは、`~` 演算子を使用して仮想ルートパスを参照できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="4c6ea-330">これは、サイト内でページを移動することができ、他のページに含まれているすべてのリンクが破損しないため、非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="4c6ea-331">また、web サイトを別の場所に移動した場合にも便利です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="4c6ea-332">次に例をいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="4c6ea-333">Web サイトが `http://myserver/myapp`場合は、ページの実行時に ASP.NET がこれらのパスを処理する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="4c6ea-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="4c6ea-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="4c6ea-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="4c6ea-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="4c6ea-336">(実際には、これらのパスは変数の値としては表示されませんが、ASP.NET はそのようなパスを扱います)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="4c6ea-337">次のように、サーバーコード (上記) とマークアップの両方で `~` 演算子を使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="4c6ea-338">マークアップでは、`~` 演算子を使用して、イメージファイル、その他の web ページ、CSS ファイルなどのリソースへのパスを作成します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="4c6ea-339">ページが実行されると、ASP.NET はページ (コードとマークアップの両方) を参照し、適切なパスへのすべての `~` 参照を解決します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="4c6ea-340">条件付きロジックとループ</span><span class="sxs-lookup"><span data-stu-id="4c6ea-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="4c6ea-341">ASP.NET server code を使用すると、条件に基づいてタスクを実行し、特定の回数 (ループを実行するコード) でステートメントを繰り返すコードを記述することができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="4c6ea-342">テスト条件</span><span class="sxs-lookup"><span data-stu-id="4c6ea-342">Testing conditions</span></span>

<span data-ttu-id="4c6ea-343">単純な条件をテストするには、`If...Then` ステートメントを使用します。これにより、指定したテストに基づいて `True` または `False` が返されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="4c6ea-344">`If` キーワードはブロックを開始します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="4c6ea-345">実際のテスト (条件) は `If` キーワードに従い、true または false を返します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="4c6ea-346">`If` ステートメントが `Then`で終了します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="4c6ea-347">テストが true の場合に実行されるステートメントは、`If` と `End If`で囲まれます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="4c6ea-348">`If` ステートメントには、条件が false の場合に実行するステートメントを指定する `Else` ブロックを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="4c6ea-349">`If` ステートメントでコードブロックが開始された場合、通常の `Code...End Code` ステートメントを使用してブロックを含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="4c6ea-350">ブロックに `@` を追加するだけで、それが機能します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="4c6ea-351">この方法は、`If` と、`For`、`For Each`、`Do While`などのコードブロックが後に続く他の Visual Basic プログラミングキーワードにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="4c6ea-352">1つ以上の `ElseIf` ブロックを使用して、複数の条件を追加できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="4c6ea-353">この例では、`If` ブロックの最初の条件が true でない場合、`ElseIf` 条件がチェックされます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="4c6ea-354">この条件が満たされると、`ElseIf` ブロック内のステートメントが実行されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="4c6ea-355">条件が満たされていない場合は、`Else` ブロック内のステートメントが実行されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="4c6ea-356">任意の数の `ElseIf` ブロックを追加して、他のすべての条件を&quot; &quot;として、`Else` ブロックで閉じることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="4c6ea-357">多数の条件をテストするには、`Select Case` ブロックを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="4c6ea-358">テストする値はかっこで囲まれています (例では、曜日変数)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="4c6ea-359">個々のテストでは、値を一覧表示する `Case` ステートメントが使用されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="4c6ea-360">`Case` ステートメントの値がテスト値と一致する場合は、その `Case` ブロック内のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="4c6ea-361">ブラウザーに表示された最後の2つの条件ブロックの結果:</span><span class="sxs-lookup"><span data-stu-id="4c6ea-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="4c6ea-363">ループコード</span><span class="sxs-lookup"><span data-stu-id="4c6ea-363">Looping code</span></span>

<span data-ttu-id="4c6ea-364">多くの場合、同じステートメントを繰り返し実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="4c6ea-365">これを行うには、ループを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-365">You do this by looping.</span></span> <span data-ttu-id="4c6ea-366">たとえば、多くの場合、データのコレクション内の各項目に対して同じステートメントを実行します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="4c6ea-367">ループする回数が正確にわかっている場合は、`For` ループを使用できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="4c6ea-368">この種類のループは、カウントアップまたはカウントする場合に特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="4c6ea-369">ループは `For` キーワードで始まり、その後に3つの要素が続きます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="4c6ea-370">`For` ステートメントの直後に、カウンター変数を宣言し (`Dim`を使用する必要はありません)、`i = 10 to 20`のように範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="4c6ea-371">これは、変数 `i` が10にカウントされ、20 (を含む) に達するまで続行されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="4c6ea-372">`For` と `Next` ステートメントの間には、ブロックの内容があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="4c6ea-373">これには、各ループで実行される1つ以上のコードステートメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="4c6ea-374">`Next i` ステートメントは、ループを終了します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="4c6ea-375">カウンターをインクリメントし、ループの次の反復処理を開始します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="4c6ea-376">`For` と `Next` の行の間のコード行には、ループの各反復処理で実行されるコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="4c6ea-377">マークアップは、毎回新しい段落 (`<p>` 要素) を作成し、出力に行を追加して i (カウンター) の値を表示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="4c6ea-378">このページを実行すると、この例では、出力を表示する11行を作成し、アイテム番号を示す各行にテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="4c6ea-380">コレクションまたは配列を使用して作業している場合は、多くの場合、`For Each` ループを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="4c6ea-381">コレクションは、類似したオブジェクトのグループであり、`For Each` ループを使用すると、コレクション内の各項目に対してタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="4c6ea-382">この種類のループは、`For` ループとは異なり、カウンターをインクリメントしたり制限を設定したりする必要がないため、コレクションに便利です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="4c6ea-383">代わりに、`For Each` ループコードは、完了するまでコレクションを処理します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="4c6ea-384">この例では、`Request.ServerVariables` コレクション内の項目 (web サーバーに関する情報を含む) が返されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="4c6ea-385">`For Each` ループを使用して、HTML の箇条書きに新しい `<li>` 要素を作成することによって各項目の名前を表示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="4c6ea-386">`For Each` キーワードの後に、コレクション内の単一の項目 (例では `myItem`) を表す変数が続き、その後に `In` キーワードが続き、その後にループするコレクションが続きます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="4c6ea-387">`For Each` ループの本体では、前に宣言した変数を使用して現在の項目にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="4c6ea-389">より汎用的なループを作成するには、`Do While` ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="4c6ea-390">このループは `Do While` キーワードで始まり、その後に条件が続き、その後に繰り返しブロックが続きます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="4c6ea-391">ループは通常、カウントに使用される変数またはオブジェクトをインクリメント (加算) またはデクリメント (減算) します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="4c6ea-392">この例では、`+=` 演算子は、ループが実行されるたびに変数の値に1を加算します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="4c6ea-393">(カウントダウンするループ内で変数をデクリメントするには、デクリメント演算子 `-=`を使用します)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="4c6ea-394">オブジェクトとコレクション</span><span class="sxs-lookup"><span data-stu-id="4c6ea-394">Objects and Collections</span></span>

<span data-ttu-id="4c6ea-395">ASP.NET web サイトのほぼすべてのものは、web ページ自体を含むオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="4c6ea-396">このセクションでは、コード内で頻繁に使用するいくつかの重要なオブジェクトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="4c6ea-397">Page オブジェクト</span><span class="sxs-lookup"><span data-stu-id="4c6ea-397">Page objects</span></span>

<span data-ttu-id="4c6ea-398">ASP.NET の最も基本的なオブジェクトはページです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="4c6ea-399">ページオブジェクトのプロパティには、修飾されたオブジェクトを使用せずに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="4c6ea-400">次のコードは、ページの `Request` オブジェクトを使用して、ページのファイルパスを取得します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="4c6ea-401">`Page` オブジェクトのプロパティを使用して、次のような大量の情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="4c6ea-402">[https://login.microsoftonline.com/consumers/](`Request`)</span><span class="sxs-lookup"><span data-stu-id="4c6ea-402">`Request`.</span></span> <span data-ttu-id="4c6ea-403">既に説明したように、これは現在の要求に関する情報のコレクションです。要求を行ったブラウザーの種類、ページの URL、ユーザー id などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="4c6ea-404">[https://login.microsoftonline.com/consumers/](`Response`)</span><span class="sxs-lookup"><span data-stu-id="4c6ea-404">`Response`.</span></span> <span data-ttu-id="4c6ea-405">これは、サーバーコードの実行が終了したときにブラウザーに送信される応答 (ページ) に関する情報のコレクションです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="4c6ea-406">たとえば、このプロパティを使用して、応答に情報を書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="4c6ea-407">コレクションオブジェクト (配列とディクショナリ)</span><span class="sxs-lookup"><span data-stu-id="4c6ea-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="4c6ea-408">コレクションは、データベースの `Customer` オブジェクトのコレクションなど、同じ種類のオブジェクトのグループです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="4c6ea-409">ASP.NET には、`Request.Files` コレクションのような多くの組み込みコレクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="4c6ea-410">多くの場合、コレクション内のデータを操作します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-410">You'll often work with data in collections.</span></span> <span data-ttu-id="4c6ea-411">2つの一般的なコレクション型は、*配列*と*ディクショナリ*です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="4c6ea-412">配列は、類似した項目のコレクションを格納するが、各項目を保持するための個別の変数を作成しない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="4c6ea-413">配列を使用して、`String`、`Integer`、`DateTime`などの特定のデータ型を宣言します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="4c6ea-414">変数に配列を含めることができることを示すには、宣言の変数名にかっこを追加します (`Dim myVar() As String`など)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="4c6ea-415">配列内の項目には、その位置 (インデックス) を使用するか、`For Each` ステートメントを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="4c6ea-416">配列インデックスは 0 &#8212;から始まります。つまり、最初の項目の位置は0、2番目の項目は1の位置にあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="4c6ea-417">配列内の項目の数を確認するには、その `Length` プロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="4c6ea-418">配列内の特定の項目の位置を取得する (つまり、配列を検索する) には、`Array.IndexOf` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="4c6ea-419">また、配列の内容 (`Array.Reverse` メソッド) の反転やコンテンツ (`Array.Sort` メソッド) の並べ替えなどを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="4c6ea-420">ブラウザーに表示される文字列配列コードの出力を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="4c6ea-422">ディクショナリはキーと値のペアのコレクションであり、キー (または名前) を指定して、対応する値を設定または取得します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="4c6ea-423">ディクショナリを作成するには、`New` キーワードを使用して、新しい `Dictionary` オブジェクトを作成していることを示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="4c6ea-424">`Dim` キーワードを使用して、変数に辞書を割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="4c6ea-425">ディクショナリ内の項目のデータ型を示すには、かっこ (`( )`) を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="4c6ea-426">宣言の最後に、別のかっこのペアを追加する必要があります。これは、実際には新しいディクショナリを作成するメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="4c6ea-427">ディクショナリに項目を追加するには、ディクショナリ変数 (この場合は`myScores`) の `Add` メソッドを呼び出して、キーと値を指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="4c6ea-428">また、次の例のように、かっこを使用してキーを指定し、単純な割り当てを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="4c6ea-429">ディクショナリから値を取得するには、キーをかっこで囲んで指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="4c6ea-430">パラメーターを使用したメソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="4c6ea-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="4c6ea-431">この記事で既に説明したように、プログラムで使用するオブジェクトにはメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="4c6ea-432">たとえば、`Database` オブジェクトには、`Database.Connect` メソッドがある場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="4c6ea-433">多くのメソッドには、1つまたは複数のパラメーターもあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="4c6ea-434">*パラメーター*は、メソッドがタスクを完了できるようにメソッドに渡す値です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="4c6ea-435">たとえば、`Request.MapPath` メソッドの宣言を見て、次の3つのパラメーターを取得します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="4c6ea-436">このメソッドは、指定された仮想パスに対応するサーバー上の物理パスを返します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="4c6ea-437">メソッドの3つのパラメーターは、`virtualPath`、`baseVirtualDir`、および `allowCrossAppMapping`です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="4c6ea-438">(宣言では、パラメーターが、受け入れられるデータのデータ型と共に一覧表示されていることに注意してください)。このメソッドを呼び出す場合は、3つのすべてのパラメーターの値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="4c6ea-439">Razor 構文で Visual Basic を使用する場合、メソッドにパラメーターを渡す方法として、*位置指定*パラメーターと*名前付きパラメーター*の2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="4c6ea-440">位置指定パラメーターを使用してメソッドを呼び出すには、メソッド宣言で指定された厳密な順序でパラメーターを渡します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="4c6ea-441">(通常、この順序については、メソッドのドキュメントを参照してください)。順序に従う必要があります。また、必要に応じて&#8212;パラメーターを省略することはできません。値のない位置指定パラメーターには、空の文字列 (`""`) または null を渡します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="4c6ea-442">次の例では、web サイトに*scripts*という名前のフォルダーがあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="4c6ea-443">このコードは `Request.MapPath` メソッドを呼び出し、3つのパラメーターの値を正しい順序で渡します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="4c6ea-444">次に、結果としてマップされたパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="4c6ea-445">メソッドに多くのパラメーターがある場合は、名前付きパラメーターを使用して、コードをすっきりさせて読みやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="4c6ea-446">名前付きパラメーターを使用してメソッドを呼び出すには、パラメーター名の後に `:=` を指定し、値を指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="4c6ea-447">名前付きパラメーターの利点は、必要な順序で追加できることです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="4c6ea-448">(欠点は、メソッドの呼び出しがコンパクトではないことです)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="4c6ea-449">次の例では、上記と同じメソッドを呼び出しますが、名前付きパラメーターを使用して値を指定します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="4c6ea-450">ご覧のように、パラメーターは異なる順序で渡されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="4c6ea-451">ただし、前の例とこの例を実行すると、同じ値が返されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="4c6ea-452">エラーの処理</span><span class="sxs-lookup"><span data-stu-id="4c6ea-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="4c6ea-453">Try-catch ステートメント</span><span class="sxs-lookup"><span data-stu-id="4c6ea-453">Try-Catch statements</span></span>

<span data-ttu-id="4c6ea-454">多くの場合、コントロール以外の理由で失敗する可能性のあるステートメントがコードに含まれています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="4c6ea-455">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-455">For example:</span></span>

- <span data-ttu-id="4c6ea-456">コードでファイルのオープン、作成、読み取り、または書き込みを行おうとすると、すべてのエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="4c6ea-457">必要なファイルが存在しない可能性があります。ロックされているか、コードにアクセス許可がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="4c6ea-458">同様に、コードがデータベース内のレコードを更新しようとすると、アクセス許可の問題が発生し、データベースへの接続が切断され、保存するデータが無効になっている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="4c6ea-459">プログラミング用語では、これらの状況は*例外*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="4c6ea-460">コードで例外が発生した場合は、ユーザーにとって非常に面倒なエラーメッセージが生成 (スロー) されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="4c6ea-462">コードで例外が発生する可能性があり、この種類のエラーメッセージが表示されないようにするには、`Try/Catch` ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="4c6ea-463">`Try` ステートメントでは、チェックしているコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="4c6ea-464">1つ以上の `Catch` ステートメントでは、発生した可能性のある特定のエラー (特定の種類の例外) を検索できます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="4c6ea-465">予測しているエラーを検索するために必要な数の `Catch` ステートメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="4c6ea-466">`Try/Catch` ステートメントでは `Response.Redirect` メソッドを使用しないことをお勧めします。これは、ページで例外が発生する可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="4c6ea-467">次の例は、最初の要求でテキストファイルを作成し、ユーザーがファイルを開くためのボタンを表示するページを示しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="4c6ea-468">この例では、例外が発生するように、不適切なファイル名を意図的に使用しています。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="4c6ea-469">このコードには `Catch` 2 つの例外のステートメントが含まれています。 `FileNotFoundException`は、ファイル名が正しくない場合に発生します。また、ASP.NET がフォルダーを検索できない場合に発生する `DirectoryNotFoundException`です。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="4c6ea-470">(例では、すべてが正常に動作するときに実行方法を確認するために、ステートメントのコメントを解除できます)。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="4c6ea-471">コードで例外が処理されなかった場合は、前のスクリーンショットのようなエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="4c6ea-472">ただし、`Try/Catch` セクションは、ユーザーがこれらの種類のエラーを表示できないようにするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="4c6ea-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="4c6ea-473">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="4c6ea-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="4c6ea-474">リファレンス ドキュメント</span><span class="sxs-lookup"><span data-stu-id="4c6ea-474">Reference Documentation</span></span>

- [<span data-ttu-id="4c6ea-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4c6ea-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="4c6ea-476">Visual Basic 言語</span><span class="sxs-lookup"><span data-stu-id="4c6ea-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
