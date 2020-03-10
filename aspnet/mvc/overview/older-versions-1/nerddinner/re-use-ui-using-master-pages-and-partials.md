---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: マスターページとパーシャルを使用して UI を再利用する |Microsoft Docs
author: microsoft
description: 手順7では、ビューテンプレート内に "ドライ原理" を適用して、部分ビューテンプレートとマスターページを使用してコードの重複を排除する方法を見ていきます。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468724"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="73596-103">マスター ページと部分を利用して UI を再使用する</span><span class="sxs-lookup"><span data-stu-id="73596-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="73596-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="73596-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="73596-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="73596-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="73596-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順7です。</span><span class="sxs-lookup"><span data-stu-id="73596-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="73596-107">手順7では、ビューテンプレート内で "ドライ原理" を適用して、部分ビューテンプレートとマスターページを使用してコードの重複を排除する方法を見ていきます。</span><span class="sxs-lookup"><span data-stu-id="73596-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="73596-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="73596-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="73596-109">手順 7: パーシャルとマスターページを操作する</span><span class="sxs-lookup"><span data-stu-id="73596-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="73596-110">ASP.NET MVC の開発理念の1つは、"何も繰り返さない" という原則 (一般に "ドライ" と呼ばれます) です。</span><span class="sxs-lookup"><span data-stu-id="73596-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="73596-111">ドライデザインは、コードとロジックの重複を排除するのに役立ちます。これにより、最終的にアプリケーションのビルドが高速化され、保守が容易になります。</span><span class="sxs-lookup"><span data-stu-id="73596-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="73596-112">私たちは、私たちのいくつかの例において、既にドライの原則が適用されています。</span><span class="sxs-lookup"><span data-stu-id="73596-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="73596-113">いくつかの例を次に示します。検証ロジックは、モデルレイヤー内に実装されています。これにより、コントローラーの編集シナリオと作成シナリオの両方で適用できます。Edit、Details、Delete アクションの各メソッドで "NotFound" ビューテンプレートを再利用しています。ここでは、ビューテンプレートで規則の命名パターンを使用しています。これにより、View () ヘルパーメソッドを呼び出すときに名前を明示的に指定する必要がなくなります。さらに、編集と作成アクションの両方のシナリオで Dinを再利用しています。</span><span class="sxs-lookup"><span data-stu-id="73596-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="73596-114">ここで、ビューテンプレート内に "ドライ原理" を適用して、コードの重複を排除する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="73596-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="73596-115">編集および作成ビューのテンプレートを再度閲覧する</span><span class="sxs-lookup"><span data-stu-id="73596-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="73596-116">現在、2つの異なるビューテンプレート ("Edit .aspx" と "default.aspx") を使用して、ディナーフォーム UI を表示しています。</span><span class="sxs-lookup"><span data-stu-id="73596-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="73596-117">視覚的な比較では、これらの類似点が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="73596-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="73596-118">作成フォームは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="73596-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="73596-119">"Edit" フォームは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="73596-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="73596-120">違いはほとんどありませんか。</span><span class="sxs-lookup"><span data-stu-id="73596-120">Not much of a difference is there?</span></span> <span data-ttu-id="73596-121">タイトルとヘッダーのテキスト以外のフォームレイアウトと入力コントロールは同じです。</span><span class="sxs-lookup"><span data-stu-id="73596-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="73596-122">"Edit .aspx" ビューと ".aspx" ビューテンプレートを開くと、同一のフォームレイアウトと入力制御コードが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="73596-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="73596-123">この重複は、新しいディナープロパティを導入または変更するたびに、変更を2回行う必要があることを意味します (これは適切ではありません)。</span><span class="sxs-lookup"><span data-stu-id="73596-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="73596-124">部分ビューテンプレートの使用</span><span class="sxs-lookup"><span data-stu-id="73596-124">Using Partial View Templates</span></span>

<span data-ttu-id="73596-125">ASP.NET MVC では、ページのサブ部分のビューレンダリングロジックをカプセル化するために使用できる "部分ビュー" テンプレートを定義する機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="73596-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="73596-126">"パーシャル" を使用すると、表示ロジックを1回だけ定義し、アプリケーションの複数の場所で再利用するための便利な方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="73596-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="73596-127">編集用の .aspx を "乾か" し、.aspx ビューテンプレートの複製を作成するには、両方に共通するフォームレイアウトと入力要素をカプセル化する "Din" という名前の部分ビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="73596-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="73596-128">この操作を行うには、/Views/Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="73596-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="73596-129">[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="73596-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="73596-130">"Dinフォーム" を作成する新しいビューに名前を指定し、ダイアログ内の [部分ビューを作成します] チェックボックスをオンにして、これを Dinに渡すことを示します。</span><span class="sxs-lookup"><span data-stu-id="73596-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="73596-131">[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Din" ビューテンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="73596-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="73596-132">次に、Edit .aspx/Create .aspx ビューテンプレートから、複製されたフォームレイアウト/入力制御コードをコピーして、新しい "Din. .ascx" 部分ビューテンプレートに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="73596-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="73596-133">次に、Edit および Create view テンプレートを更新して、Dinフォーム部分テンプレートを呼び出し、フォームの重複を除去します。</span><span class="sxs-lookup"><span data-stu-id="73596-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="73596-134">これを行うには、ビューテンプレート内で Html の RenderPartial ("Dinの形式") を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="73596-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="73596-135">Create.aspx</span><span class="sxs-lookup"><span data-stu-id="73596-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="73596-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="73596-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="73596-137">.Html 部分を呼び出すときに、必要な部分テンプレートのパスを明示的に修飾できます (例: ~ Views/ディナー/Din)。</span><span class="sxs-lookup"><span data-stu-id="73596-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="73596-138">上記のコードでは、ASP.NET MVC 内で規約ベースの命名パターンを利用しています。また、レンダリングする部分の名前として "Dinare Form" を指定するだけです。</span><span class="sxs-lookup"><span data-stu-id="73596-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="73596-139">この操作を行うと、規則ベースの views ディレクトリで ASP.NET MVC が最初に表示されます (/Views/Dinners)。</span><span class="sxs-lookup"><span data-stu-id="73596-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="73596-140">部分的なテンプレートが見つからない場合は、[/]/[共有] ディレクトリで検索します。</span><span class="sxs-lookup"><span data-stu-id="73596-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="73596-141">部分ビューの名前だけを使用して Html の RenderPartial () が呼び出されると、ASP.NET MVC は、呼び出し元のビューテンプレートによって使用されるのと同じモデルおよび ViewData dictionary オブジェクトを部分ビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="73596-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="73596-142">または、Html. RenderPartial () のオーバーロードされたバージョンがあります。これにより、部分ビューで使用する代替モデルオブジェクトまたは ViewData dictionary を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="73596-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="73596-143">これは、完全なモデル/ビューモデルのサブセットのみを渡す必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="73596-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="73596-144">**サイドトピック: &lt;%&gt;ではなく%%&gt; を &lt;理由**</span><span class="sxs-lookup"><span data-stu-id="73596-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="73596-145">上記のコードでは、Html の RenderPartial () を呼び出すときに &lt;% =%&gt; ブロックではなく &lt;%%&gt; ブロックを使用していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="73596-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="73596-146">&lt;% =%&gt; ASP.NET のブロックは、開発者が指定された値を表示しようとしていることを示します (例: &lt;% = "Hello"%&gt; は "Hello" を表示します)。</span><span class="sxs-lookup"><span data-stu-id="73596-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="73596-147">&lt;%%&gt; ブロックは、開発者がコードを実行しようとしていること、およびその中のレンダリングされた出力を明示的に実行する必要があることを示しています (例: &lt;% Response. 書き込み ("Hello")%&gt;。</span><span class="sxs-lookup"><span data-stu-id="73596-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="73596-148">ここでは、&lt;%%&gt; ブロックを Html. RenderPartial コードで使用しています。これは、Html. RenderPartial () メソッドが文字列を返さず、代わりに、呼び出し元ビューテンプレートの出力ストリームに直接コンテンツを出力するためです。</span><span class="sxs-lookup"><span data-stu-id="73596-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="73596-149">これは、パフォーマンスの効率を向上させるために行われます。これにより、(非常に大きな可能性がある) 一時文字列オブジェクトを作成する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="73596-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="73596-150">これにより、メモリ使用量が減り、アプリケーション全体のスループットが向上します。</span><span class="sxs-lookup"><span data-stu-id="73596-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="73596-151">.Html 部分 () を使用する場合の一般的な間違いの1つは、呼び出しの末尾にセミコロンを追加することです。これは、&lt;%%&gt; ブロック内にあるときに忘れられます。</span><span class="sxs-lookup"><span data-stu-id="73596-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="73596-152">たとえば、次のコードではコンパイラエラーが発生します。% Html. RenderPartial ("din&lt;Form")%&gt; は、次のように記述する必要があります: &lt;% .Html ("Din)")。%&gt; これは、&lt;%%&gt; ブロックが自己完結型のコードステートメントであるためC#です。また、コードステートメントを使用する場合は、セミコロンで終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="73596-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="73596-153">部分ビューテンプレートを使用してコードを明確にする</span><span class="sxs-lookup"><span data-stu-id="73596-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="73596-154">ビューレンダリングロジックが複数の場所に複製されないように、"Dinform" 部分ビューテンプレートを作成しました。</span><span class="sxs-lookup"><span data-stu-id="73596-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="73596-155">これは、部分ビューテンプレートを作成する最も一般的な理由です。</span><span class="sxs-lookup"><span data-stu-id="73596-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="73596-156">場合によっては、1つの場所でのみ呼び出される場合でも、部分ビューを作成するのが理にかなっていることもあります。</span><span class="sxs-lookup"><span data-stu-id="73596-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="73596-157">ビューのレンダリングロジックを抽出し、1つまたは複数の適切な名前付き部分テンプレートにパーティション分割すると、非常に複雑なビューテンプレートが読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="73596-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="73596-158">たとえば、次のコードスニペットは、プロジェクトのサイトの .master ファイルからのものであるとします (これについては後で説明します)。</span><span class="sxs-lookup"><span data-stu-id="73596-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="73596-159">画面の右上にログイン/ログアウトリンクを表示するロジックは、"LogOnUserControl" 部分にカプセル化されているため、このコードは比較的簡単に読むことができます。</span><span class="sxs-lookup"><span data-stu-id="73596-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="73596-160">ビューテンプレート内の html/コードマークアップを解釈しようとすると混乱が見られる場合は、その一部を抽出して、適切な名前の部分ビューにリファクタリングしたかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="73596-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="73596-161">マスター ページ</span><span class="sxs-lookup"><span data-stu-id="73596-161">Master Pages</span></span>

<span data-ttu-id="73596-162">ASP.NET MVC では、部分ビューをサポートするだけでなく、サイトの共通レイアウトとトップレベル html を定義するために使用できる "マスターページ" テンプレートを作成する機能もサポートされています。</span><span class="sxs-lookup"><span data-stu-id="73596-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="73596-163">次に、コンテンツプレースホルダーコントロールをマスターページに追加して、上書きまたはビューによる "塗りつぶし" が可能な置換可能な領域を識別できます。</span><span class="sxs-lookup"><span data-stu-id="73596-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="73596-164">これにより、アプリケーション全体に共通のレイアウトを適用するための、非常に効果的な (ドライ) 方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="73596-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="73596-165">既定では、新しい ASP.NET MVC プロジェクトには、自動的に追加されたマスターページテンプレートがあります。</span><span class="sxs-lookup"><span data-stu-id="73596-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="73596-166">このマスターページは、"\Views\Shared\" という名前で、次のフォルダー内に存在します。</span><span class="sxs-lookup"><span data-stu-id="73596-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="73596-167">既定のサイトのマスターファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="73596-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="73596-168">ここでは、サイトの外部 html と、上部のナビゲーションのメニューを定義します。</span><span class="sxs-lookup"><span data-stu-id="73596-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="73596-169">これには、2つの置き換え可能なコンテンツのプレースホルダーコントロールが含まれています。タイトルの場合は、もう1つはページのプライマリコンテンツを置き換える必要がある場合はです。</span><span class="sxs-lookup"><span data-stu-id="73596-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="73596-170">これまでに作成したすべてのビューテンプレート ("リスト"、"詳細"、"編集"、"作成"、"NotFound" など) は、このサイトのマスターテンプレートに基づいています。</span><span class="sxs-lookup"><span data-stu-id="73596-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="73596-171">これは、[ビューの追加] ダイアログボックスを使用してビューを作成したときに、既定で top &lt;% @ Page%&gt; ディレクティブに追加された "MasterPageFile" 属性によって示されます。</span><span class="sxs-lookup"><span data-stu-id="73596-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="73596-172">これは、サイトのマスターコンテンツを変更し、ビューテンプレートをレンダリングするときに、変更が自動的に適用されて使用されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="73596-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="73596-173">ここでは、アプリケーションのヘッダーが "My MVC Application" ではなく "" である "というように、Site. マスターのヘッダーセクションを更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="73596-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="73596-174">また、ナビゲーションメニューを更新して、最初のタブが "Find a ディナー" (HomeController の Index () アクションメソッドによって処理されます) になるようにします。次に、"Host a ディナー" という名前の新しいタブを追加します (Dinの Scontroller の Create () アクションメソッドによって処理されます)。</span><span class="sxs-lookup"><span data-stu-id="73596-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="73596-175">サイトのマスターファイルを保存してブラウザーを更新すると、アプリケーション内のすべてのビューでヘッダーの変更が表示されます。</span><span class="sxs-lookup"><span data-stu-id="73596-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="73596-176">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="73596-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="73596-177">また、/// */[id]* URL を使用すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="73596-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="73596-178">次の手順</span><span class="sxs-lookup"><span data-stu-id="73596-178">Next Step</span></span>

<span data-ttu-id="73596-179">パーシャルおよびマスターページでは、ビューをクリーンに整理するための非常に柔軟なオプションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="73596-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="73596-180">ビューのコンテンツやコードを複製して、ビューテンプレートを読みやすくし、管理しやすくするために役立つことがわかります。</span><span class="sxs-lookup"><span data-stu-id="73596-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="73596-181">先ほど作成したリストシナリオにもう一度目を通して、スケーラブルなページングサポートを有効にしましょう。</span><span class="sxs-lookup"><span data-stu-id="73596-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="73596-182">[前へ](use-viewdata-and-implement-viewmodel-classes.md)
> [次へ](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="73596-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
