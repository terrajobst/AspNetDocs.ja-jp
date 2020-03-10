---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC ビューの概要C#() |Microsoft Docs
author: StephenWalther
description: ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。 このチュートリアルでは、Stephen Walther がビューを紹介し、その方法を示します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: b3f44aa9654a2a718381eaf9c856ca3e15ed1e27
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485854"
---
# <a name="aspnet-mvc-views-overview-c"></a><span data-ttu-id="9483e-104">ASP.NET MVC ビュー概要 (C#)</span><span class="sxs-lookup"><span data-stu-id="9483e-104">ASP.NET MVC Views Overview (C#)</span></span>

<span data-ttu-id="9483e-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9483e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9483e-106">ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。</span><span class="sxs-lookup"><span data-stu-id="9483e-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="9483e-107">このチュートリアルでは、Stephen Walther を使用してビューを作成し、ビュー内でビューデータと HTML ヘルパーを活用する方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="9483e-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="9483e-108">このチュートリアルの目的は、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーの概要を説明することです。</span><span class="sxs-lookup"><span data-stu-id="9483e-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="9483e-109">このチュートリアルの最後に、新しいビューを作成する方法、コントローラーからビューにデータを渡す方法、HTML ヘルパーを使用してビューのコンテンツを生成する方法について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="9483e-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="9483e-110">ビューについて</span><span class="sxs-lookup"><span data-stu-id="9483e-110">Understanding Views</span></span>

<span data-ttu-id="9483e-111">ASP.NET ページまたは Active Server ページの場合、ASP.NET MVC には、ページに直接対応するものは含まれません。</span><span class="sxs-lookup"><span data-stu-id="9483e-111">For ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="9483e-112">ASP.NET MVC アプリケーションでは、ブラウザーのアドレスバーに入力する URL 内のパスに対応するページがディスク上にありません。</span><span class="sxs-lookup"><span data-stu-id="9483e-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="9483e-113">ASP.NET MVC アプリケーションのページに最も近いのは、*ビュー*と呼ばれるものです。</span><span class="sxs-lookup"><span data-stu-id="9483e-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="9483e-114">ASP.NET MVC アプリケーションでは、入力方向のブラウザー要求がコントローラーアクションにマップされます。</span><span class="sxs-lookup"><span data-stu-id="9483e-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="9483e-115">コントローラーアクションはビューを返すことがあります。</span><span class="sxs-lookup"><span data-stu-id="9483e-115">A controller action might return a view.</span></span> <span data-ttu-id="9483e-116">ただし、コントローラーアクションでは、他の種類のアクション (別のコントローラーアクションへのリダイレクトなど) が実行される場合があります。</span><span class="sxs-lookup"><span data-stu-id="9483e-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="9483e-117">リスト1には、HomeController という名前のシンプルなコントローラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9483e-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="9483e-118">HomeController は、Index () と Details () という2つのコントローラーアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="9483e-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="9483e-119">**リスト 1-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="9483e-119">**Listing 1 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

<span data-ttu-id="9483e-120">ブラウザーのアドレスバーに次の URL を入力して、最初のアクション (Index () アクション) を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="9483e-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="9483e-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="9483e-121">/Home/Index</span></span>

<span data-ttu-id="9483e-122">このアドレスをブラウザーに入力することで、2番目のアクションである Details () アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="9483e-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="9483e-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="9483e-123">/Home/Details</span></span>

<span data-ttu-id="9483e-124">Index () アクションを実行すると、ビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-124">The Index() action returns a view.</span></span> <span data-ttu-id="9483e-125">作成するほとんどの操作では、ビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-125">Most actions that you create will return views.</span></span> <span data-ttu-id="9483e-126">ただし、アクションは他の種類のアクション結果を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="9483e-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="9483e-127">たとえば、Details () アクションは、着信要求を Index () アクションにリダイレクトする RedirectToActionResult を返します。</span><span class="sxs-lookup"><span data-stu-id="9483e-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="9483e-128">Index () アクションには、次の1行のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9483e-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="9483e-129">View();</span><span class="sxs-lookup"><span data-stu-id="9483e-129">View();</span></span>

<span data-ttu-id="9483e-130">次のコード行では、web サーバー上の次のパスにあるビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="9483e-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="9483e-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="9483e-132">ビューへのパスは、コントローラーの名前とコントローラーアクションの名前から推測されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="9483e-133">必要に応じて、ビューを明示的に指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="9483e-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="9483e-134">次のコード行では、Fred という名前のビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="9483e-135">View( Fred );</span><span class="sxs-lookup"><span data-stu-id="9483e-135">View( Fred );</span></span>

<span data-ttu-id="9483e-136">このコード行を実行すると、次のパスからビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="9483e-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="9483e-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9483e-138">ASP.NET MVC アプリケーションの単体テストを作成する予定の場合は、ビュー名について明示することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9483e-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="9483e-139">これにより、単体テストを作成して、必要なビューがコントローラーアクションによって返されたことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="9483e-140">ビューへのコンテンツの追加</span><span class="sxs-lookup"><span data-stu-id="9483e-140">Adding Content to a View</span></span>

<span data-ttu-id="9483e-141">ビューは、スクリプトを含めることができる標準 (X) の HTML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="9483e-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="9483e-142">スクリプトを使用して、動的なコンテンツをビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="9483e-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="9483e-143">たとえば、リスト2のビューには、現在の日付と時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="9483e-144">**リスト 2-\Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="9483e-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

<span data-ttu-id="9483e-145">リスト2の HTML ページの本文には、次のスクリプトが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9483e-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="9483e-146">&lt;% Response. 書き込み (DateTime. Now);%&gt;</span><span class="sxs-lookup"><span data-stu-id="9483e-146">&lt;% Response.Write(DateTime.Now);%&gt;</span></span>

<span data-ttu-id="9483e-147">スクリプトの区切り記号 &lt;% および%&gt; を使用して、スクリプトの先頭と末尾にマークを付けます。</span><span class="sxs-lookup"><span data-stu-id="9483e-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="9483e-148">このスクリプトは、「 C#」で記述されています。</span><span class="sxs-lookup"><span data-stu-id="9483e-148">This script is written in C#.</span></span> <span data-ttu-id="9483e-149">ブラウザーにコンテンツを表示するために、Write () メソッドを呼び出して現在の日付と時刻を表示します。</span><span class="sxs-lookup"><span data-stu-id="9483e-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="9483e-150">スクリプトの区切り記号 &lt;% および%&gt; を使用して、1つまたは複数のステートメントを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="9483e-151">Response. Write () を呼び出すと、Microsoft から、Response () メソッドを呼び出すためのショートカットが提供されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="9483e-152">リスト3のビューでは、応答の呼び出し () のショートカットとして、区切り記号 &lt;% = および%&gt; を使用します。</span><span class="sxs-lookup"><span data-stu-id="9483e-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="9483e-153">**リスト 3-Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="9483e-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

<span data-ttu-id="9483e-154">任意の .NET 言語を使用して、動的なコンテンツをビューに生成できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="9483e-155">通常は、Visual Basic .NET またはC#を使用して、コントローラーとビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="9483e-155">Normally, you'll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="9483e-156">HTML ヘルパーを使用したビューコンテンツの生成</span><span class="sxs-lookup"><span data-stu-id="9483e-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="9483e-157">ビューにコンテンツを簡単に追加できるようにするために、 *HTML ヘルパー*と呼ばれるものを利用できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="9483e-158">通常、HTML ヘルパーは、文字列を生成するメソッドです。</span><span class="sxs-lookup"><span data-stu-id="9483e-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="9483e-159">HTML ヘルパーを使用すると、テキストボックス、リンク、ドロップダウンリスト、リストボックスなどの標準の HTML 要素を生成できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="9483e-160">たとえば、リスト4のビューでは、3つの HTML ヘルパー (BeginForm ()、TextBox ()、および Password () ヘルパー) を利用して、ログインフォームを生成します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="9483e-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="9483e-161">**リスト 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="9483e-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]

<span data-ttu-id="9483e-162">[[新しいプロジェクト] ダイアログボックスの ![](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9483e-162">[![The New Project dialog box](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="9483e-163">**図 01**: 標準のログインフォーム ([クリックすると、フルサイズの画像が表示](asp-net-mvc-views-overview-cs/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="9483e-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-cs/_static/image2.png))</span></span>

<span data-ttu-id="9483e-164">すべての HTML ヘルパーメソッドは、ビューの Html プロパティで呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="9483e-165">たとえば、TextBox () メソッドを呼び出すことによってテキストボックスをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="9483e-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="9483e-166">Html の TextBox () ヘルパーと .Html () ヘルパーの両方を呼び出すときは、スクリプトの区切り記号 &lt;% = および%&gt; を使用することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9483e-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="9483e-167">これらのヘルパーは単に文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="9483e-167">These helpers simply return a string.</span></span> <span data-ttu-id="9483e-168">文字列をブラウザーに表示するには、Response. Write () を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="9483e-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="9483e-169">HTML ヘルパーメソッドの使用は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="9483e-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="9483e-170">記述する必要のある HTML およびスクリプトの量を減らすことで、作業が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="9483e-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="9483e-171">リスト5のビューでは、HTML ヘルパーを使用せずに、リスト4のビューとまったく同じ形式がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="9483e-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="9483e-172">**リスト 5--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="9483e-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

<span data-ttu-id="9483e-173">独自の HTML ヘルパーを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="9483e-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="9483e-174">たとえば、データベースレコードのセットを HTML テーブルに自動的に表示する GridView () ヘルパーメソッドを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9483e-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="9483e-175">このトピックでは、**カスタム HTML ヘルパーの作成**について説明します。</span><span class="sxs-lookup"><span data-stu-id="9483e-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="9483e-176">ビューデータを使用してビューにデータを渡す</span><span class="sxs-lookup"><span data-stu-id="9483e-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="9483e-177">ビューデータを使用して、コントローラーからビューにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="9483e-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="9483e-178">メールを通じて送信するパッケージのようなデータを表示してみてください。</span><span class="sxs-lookup"><span data-stu-id="9483e-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="9483e-179">コントローラーからビューに渡されるすべてのデータは、このパッケージを使用して送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9483e-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="9483e-180">たとえば、リスト6のコントローラーは、データを表示するメッセージを追加します。</span><span class="sxs-lookup"><span data-stu-id="9483e-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="9483e-181">**リスト 6-ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="9483e-181">**Listing 6 - ProductController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

<span data-ttu-id="9483e-182">Controller ViewData プロパティは、名前と値のペアのコレクションを表します。</span><span class="sxs-lookup"><span data-stu-id="9483e-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="9483e-183">リスト6では、Index () メソッドは、Hello World! という値を持つメッセージという名前のビューデータコレクションに項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="9483e-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="9483e-184">Index () メソッドによってビューが返されると、ビューデータは自動的にビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="9483e-185">リスト7のビューでは、ビューデータからメッセージが取得され、ブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9483e-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="9483e-186">**リスト 7--\Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="9483e-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

<span data-ttu-id="9483e-187">このビューでは、メッセージを表示するときに html. Encode () HTML ヘルパーメソッドが利用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9483e-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="9483e-188">Html. Encode () HTML ヘルパーは、&lt; や &gt; などの特殊文字を、web ページに安全に表示できる文字にエンコードします。</span><span class="sxs-lookup"><span data-stu-id="9483e-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="9483e-189">ユーザーが web サイトに送信するコンテンツをレンダリングするときは常に、JavaScript インジェクション攻撃を防ぐためにコンテンツをエンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9483e-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="9483e-190">(ProductController に自分でメッセージを作成したので、実際にはメッセージをエンコードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9483e-190">(Because we created the message ourselves in the ProductController, we don't really need to encode the message.</span></span> <span data-ttu-id="9483e-191">ただし、ビュー内のビューデータから取得したコンテンツを表示するときは、常に Html の Encode () メソッドを呼び出すことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9483e-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="9483e-192">リスト7では、ビューデータを利用して、コントローラーからビューに単純な文字列メッセージを渡していました。</span><span class="sxs-lookup"><span data-stu-id="9483e-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="9483e-193">また、ビューデータを使用して、データベースレコードのコレクションなど、他の種類のデータをコントローラーからビューに渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="9483e-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="9483e-194">たとえば、Products データベーステーブルの内容をビューに表示する場合は、データベースレコードのコレクションをビューデータに渡すことになります。</span><span class="sxs-lookup"><span data-stu-id="9483e-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="9483e-195">また、厳密に型指定されたビューデータをコントローラーからビューに渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="9483e-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="9483e-196">このトピックでは、厳密に**型指定されたビューのデータとビューについ**て説明します。</span><span class="sxs-lookup"><span data-stu-id="9483e-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="9483e-197">まとめ</span><span class="sxs-lookup"><span data-stu-id="9483e-197">Summary</span></span>

<span data-ttu-id="9483e-198">このチュートリアルでは、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーについて簡単に説明しました。</span><span class="sxs-lookup"><span data-stu-id="9483e-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="9483e-199">最初のセクションでは、新しいビューをプロジェクトに追加する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9483e-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="9483e-200">特定のコントローラーからビューを呼び出すには、適切なフォルダーにビューを追加する必要があることを学びました。</span><span class="sxs-lookup"><span data-stu-id="9483e-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="9483e-201">次に、HTML ヘルパーのトピックについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="9483e-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="9483e-202">HTML ヘルパーを使用して、標準の HTML コンテンツを簡単に生成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9483e-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="9483e-203">最後に、ビューデータを利用して、コントローラーからビューにデータを渡す方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9483e-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9483e-204">Next</span><span class="sxs-lookup"><span data-stu-id="9483e-204">Next</span></span>](creating-custom-html-helpers-cs.md)
