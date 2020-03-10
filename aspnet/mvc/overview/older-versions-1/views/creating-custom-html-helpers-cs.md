---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: カスタム HTML ヘルパーの作成C#() |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。 HTML ヘルパーを利用することで...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485788"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="f7359-104">カスタム HTML ヘルパーの作成 (C#)</span><span class="sxs-lookup"><span data-stu-id="f7359-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="f7359-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f7359-105">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="f7359-106">[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f7359-106">[Download PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)</span></span>

> <span data-ttu-id="f7359-107">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。</span><span class="sxs-lookup"><span data-stu-id="f7359-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f7359-108">HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="f7359-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="f7359-109">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。</span><span class="sxs-lookup"><span data-stu-id="f7359-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f7359-110">HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="f7359-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="f7359-111">このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれる既存の HTML ヘルパーのいくつかについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f7359-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="f7359-112">次に、カスタム HTML ヘルパーを作成する2つの方法について説明します。ここでは、静的メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7359-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="f7359-113">HTML ヘルパーについて</span><span class="sxs-lookup"><span data-stu-id="f7359-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="f7359-114">HTML ヘルパーは、文字列を返すメソッドにすぎません。</span><span class="sxs-lookup"><span data-stu-id="f7359-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="f7359-115">文字列は、必要な任意の種類のコンテンツを表すことができます。</span><span class="sxs-lookup"><span data-stu-id="f7359-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="f7359-116">たとえば、html ヘルパーを使用して、HTML `<input>` や `<img>` タグなどの標準の HTML タグを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f7359-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="f7359-117">また、HTML ヘルパーを使用して、タブストリップやデータベースデータの HTML テーブルなど、より複雑なコンテンツを表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="f7359-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="f7359-118">ASP.NET MVC フレームワークには、次の一連の標準 HTML ヘルパーが含まれています (これは完全な一覧ではありません)。</span><span class="sxs-lookup"><span data-stu-id="f7359-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="f7359-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="f7359-119">Html.ActionLink()</span></span>
- <span data-ttu-id="f7359-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="f7359-120">Html.BeginForm()</span></span>
- <span data-ttu-id="f7359-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="f7359-121">Html.CheckBox()</span></span>
- <span data-ttu-id="f7359-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="f7359-122">Html.DropDownList()</span></span>
- <span data-ttu-id="f7359-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="f7359-123">Html.EndForm()</span></span>
- <span data-ttu-id="f7359-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="f7359-124">Html.Hidden()</span></span>
- <span data-ttu-id="f7359-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="f7359-125">Html.ListBox()</span></span>
- <span data-ttu-id="f7359-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="f7359-126">Html.Password()</span></span>
- <span data-ttu-id="f7359-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="f7359-127">Html.RadioButton()</span></span>
- <span data-ttu-id="f7359-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="f7359-128">Html.TextArea()</span></span>
- <span data-ttu-id="f7359-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="f7359-129">Html.TextBox()</span></span>

<span data-ttu-id="f7359-130">たとえば、リスト1のフォームについて考えてみます。</span><span class="sxs-lookup"><span data-stu-id="f7359-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="f7359-131">このフォームは、標準の HTML ヘルパーの2つのヘルプを使用してレンダリングされます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="f7359-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="f7359-132">このフォームでは、`Html.BeginForm()` と `Html.TextBox()` のヘルパーメソッドを使用して、単純な HTML フォームをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f7359-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="f7359-133">[HTML ヘルパーで表示される ![ページ](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f7359-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="f7359-134">**図 01**: HTML ヘルパーでレンダリングされるページ ([クリックすると、フルサイズの画像が表示](creating-custom-html-helpers-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="f7359-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="f7359-135">**リスト1– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f7359-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="f7359-136">Html. BeginForm () ヘルパーメソッドは、HTML `<form>` の開始タグと終了タグを作成するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="f7359-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="f7359-137">`Html.BeginForm()` メソッドは、using ステートメント内で呼び出されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="f7359-138">Using ステートメントを使用すると、`<form>` タグが using ブロックの末尾で閉じられるようになります。</span><span class="sxs-lookup"><span data-stu-id="f7359-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="f7359-139">必要に応じて、using ブロックを作成するのではなく、Html の EndForm () ヘルパーメソッドを呼び出して、`<form>` タグを閉じることができます。</span><span class="sxs-lookup"><span data-stu-id="f7359-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="f7359-140">どちらの方法を使用しても、直感的にわかりやすい `<form>` タグを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f7359-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="f7359-141">リスト1で HTML `<input>` タグを表示するには、`Html.TextBox()` ヘルパーメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="f7359-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="f7359-142">ブラウザーで [ソースの表示] を選択すると、リスト2に HTML ソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7359-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="f7359-143">ソースに標準の HTML タグが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7359-144">`Html.TextBox()`HTML ヘルパーは `<% %>` タグではなく `<%= %>` タグでレンダリングされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="f7359-145">等号を含めない場合は、ブラウザーに何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="f7359-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="f7359-146">ASP.NET MVC フレームワークには、少数のヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f7359-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="f7359-147">多くの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7359-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="f7359-148">このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する2つの方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f7359-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="f7359-149">**リスト2– `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="f7359-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="f7359-150">静的メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="f7359-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="f7359-151">新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す静的メソッドを作成することです。</span><span class="sxs-lookup"><span data-stu-id="f7359-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="f7359-152">たとえば、HTML `<label>` タグをレンダリングする新しい HTML ヘルパーを作成する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="f7359-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="f7359-153">リスト2のクラスを使用して、`<label>` を表示できます。</span><span class="sxs-lookup"><span data-stu-id="f7359-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="f7359-154">**リスト2– `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="f7359-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="f7359-155">リスト2のクラスについては特別なことはありません。</span><span class="sxs-lookup"><span data-stu-id="f7359-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="f7359-156">`Label()` メソッドは、単に文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="f7359-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="f7359-157">リスト3の変更されたインデックスビューでは、`LabelHelper` を使用して HTML `<label>` タグを表示します。</span><span class="sxs-lookup"><span data-stu-id="f7359-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="f7359-158">ビューには、`Application1.Helpers` 名前空間をインポートする `<%@ imports %>` ディレクティブが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="f7359-159">**リスト2– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f7359-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="f7359-160">拡張メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="f7359-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="f7359-161">ASP.NET MVC フレームワークに含まれている標準の HTML ヘルパーと同様に機能する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7359-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="f7359-162">拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f7359-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="f7359-163">HTML ヘルパーメソッドを作成する場合は、ビューの Html プロパティによって表される HtmlHelper クラスに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f7359-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="f7359-164">リスト3のクラスは、`Label()`という名前の `HtmlHelper` クラスに拡張メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f7359-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="f7359-165">このクラスについては、いくつかの点に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7359-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="f7359-166">まず、クラスが静的クラスであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="f7359-167">静的クラスを使用して拡張メソッドを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7359-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="f7359-168">次に、`Label()` メソッドの最初のパラメーターの前に `this`キーワードが付いていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="f7359-169">拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。</span><span class="sxs-lookup"><span data-stu-id="f7359-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="f7359-170">**リスト3– `Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="f7359-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="f7359-171">拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、Visual Studio の Intellisense に拡張メソッドが表示されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="f7359-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="f7359-172">唯一の違いは、拡張メソッドには、その横に特殊記号 (下向きの矢印のアイコン) が表示される点です。</span><span class="sxs-lookup"><span data-stu-id="f7359-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="f7359-173">[Html. Label () 拡張メソッドを使用して ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f7359-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="f7359-174">**図 02**: Html. Label () 拡張メソッドの使用 ([クリックしてフルサイズのイメージを表示する](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f7359-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="f7359-175">リスト4の変更されたインデックスビューでは、Html. Label () 拡張メソッドを使用して、すべての `<label>` タグをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f7359-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="f7359-176">**リスト4– `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f7359-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="f7359-177">まとめ</span><span class="sxs-lookup"><span data-stu-id="f7359-177">Summary</span></span>

<span data-ttu-id="f7359-178">このチュートリアルでは、カスタム HTML ヘルパーを作成する2つの方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="f7359-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="f7359-179">まず、文字列を返す静的メソッドを作成して、カスタム `Label()` HTML ヘルパーを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="f7359-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="f7359-180">次に、`HtmlHelper` クラスに拡張メソッドを作成して、カスタム `Label()` HTML ヘルパーメソッドを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="f7359-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="f7359-181">このチュートリアルでは、非常に単純な HTML ヘルパーメソッドを構築することに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="f7359-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="f7359-182">HTML ヘルパーは必要に応じて複雑になる可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7359-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="f7359-183">ツリービュー、メニュー、データベースデータのテーブルなどのリッチコンテンツを表示する HTML ヘルパーを構築できます。</span><span class="sxs-lookup"><span data-stu-id="f7359-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7359-184">[前へ](asp-net-mvc-views-overview-cs.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f7359-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
