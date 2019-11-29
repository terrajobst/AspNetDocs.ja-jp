---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: カスタム HTML ヘルパーの作成 (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。 HTML ヘルパーを利用することで...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593869"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="40c89-104">カスタム HTML ヘルパーの作成 (VB)</span><span class="sxs-lookup"><span data-stu-id="40c89-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="40c89-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="40c89-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="40c89-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="40c89-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="40c89-107">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。</span><span class="sxs-lookup"><span data-stu-id="40c89-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="40c89-108">HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="40c89-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="40c89-109">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。</span><span class="sxs-lookup"><span data-stu-id="40c89-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="40c89-110">HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="40c89-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="40c89-111">このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれる既存の HTML ヘルパーのいくつかについて説明します。</span><span class="sxs-lookup"><span data-stu-id="40c89-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="40c89-112">次に、カスタム HTML ヘルパーを作成する2つの方法について説明します。ここでは、共有メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40c89-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="40c89-113">HTML ヘルパーについて</span><span class="sxs-lookup"><span data-stu-id="40c89-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="40c89-114">HTML ヘルパーは、文字列を返すメソッドにすぎません。</span><span class="sxs-lookup"><span data-stu-id="40c89-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="40c89-115">文字列は、必要な任意の種類のコンテンツを表すことができます。</span><span class="sxs-lookup"><span data-stu-id="40c89-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="40c89-116">たとえば、html ヘルパーを使用して、HTML `<input>` や `<img>` タグなどの標準の HTML タグを表示できます。</span><span class="sxs-lookup"><span data-stu-id="40c89-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="40c89-117">また、HTML ヘルパーを使用して、タブストリップやデータベースデータの HTML テーブルなど、より複雑なコンテンツを表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="40c89-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="40c89-118">ASP.NET MVC フレームワークには、次の一連の標準 HTML ヘルパーが含まれています (これは完全な一覧ではありません)。</span><span class="sxs-lookup"><span data-stu-id="40c89-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="40c89-119">Html.actionlink ()</span><span class="sxs-lookup"><span data-stu-id="40c89-119">Html.ActionLink()</span></span>
- <span data-ttu-id="40c89-120">Html. BeginForm ()</span><span class="sxs-lookup"><span data-stu-id="40c89-120">Html.BeginForm()</span></span>
- <span data-ttu-id="40c89-121">Html. CheckBox ()</span><span class="sxs-lookup"><span data-stu-id="40c89-121">Html.CheckBox()</span></span>
- <span data-ttu-id="40c89-122">Html. DropDownList ()</span><span class="sxs-lookup"><span data-stu-id="40c89-122">Html.DropDownList()</span></span>
- <span data-ttu-id="40c89-123">Html. EndForm ()</span><span class="sxs-lookup"><span data-stu-id="40c89-123">Html.EndForm()</span></span>
- <span data-ttu-id="40c89-124">Html. Hidden ()</span><span class="sxs-lookup"><span data-stu-id="40c89-124">Html.Hidden()</span></span>
- <span data-ttu-id="40c89-125">Html. ListBox ()</span><span class="sxs-lookup"><span data-stu-id="40c89-125">Html.ListBox()</span></span>
- <span data-ttu-id="40c89-126">Html. Password ()</span><span class="sxs-lookup"><span data-stu-id="40c89-126">Html.Password()</span></span>
- <span data-ttu-id="40c89-127">Html. RadioButton ()</span><span class="sxs-lookup"><span data-stu-id="40c89-127">Html.RadioButton()</span></span>
- <span data-ttu-id="40c89-128">Html. TextArea ()</span><span class="sxs-lookup"><span data-stu-id="40c89-128">Html.TextArea()</span></span>
- <span data-ttu-id="40c89-129">Html. TextBox ()</span><span class="sxs-lookup"><span data-stu-id="40c89-129">Html.TextBox()</span></span>

<span data-ttu-id="40c89-130">たとえば、リスト1のフォームについて考えてみます。</span><span class="sxs-lookup"><span data-stu-id="40c89-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="40c89-131">このフォームは、標準の HTML ヘルパーの2つのヘルプを使用してレンダリングされます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="40c89-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="40c89-132">このフォームでは、`Html.BeginForm()` と `Html.TextBox()` のヘルパーメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="40c89-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="40c89-133">[HTML ヘルパーで表示される ![ページ](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="40c89-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="40c89-134">**図 01**: HTML ヘルパーでレンダリングされるページ ([クリックすると、フルサイズの画像が表示](creating-custom-html-helpers-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="40c89-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="40c89-135">**リスト1– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="40c89-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="40c89-136">`Html.BeginForm()` のヘルパーメソッドは、HTML `<form>` の開始タグと終了タグを作成するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="40c89-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="40c89-137">`Html.BeginForm()` メソッドは、using ステートメント内で呼び出されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="40c89-138">Using ステートメントを使用すると、`<form>` タグが using ブロックの末尾で閉じられるようになります。</span><span class="sxs-lookup"><span data-stu-id="40c89-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="40c89-139">必要に応じて、using ブロックを作成するのではなく、Html の EndForm () ヘルパーメソッドを呼び出して、`<form>` タグを閉じることができます。</span><span class="sxs-lookup"><span data-stu-id="40c89-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="40c89-140">どちらの方法を使用しても、直感的にわかりやすい `<form>` タグを作成できます。</span><span class="sxs-lookup"><span data-stu-id="40c89-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="40c89-141">リスト1で HTML `<input>` タグを表示するには、`Html.TextBox()` ヘルパーメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="40c89-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="40c89-142">ブラウザーで [ソースの表示] を選択すると、リスト2に HTML ソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="40c89-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="40c89-143">ソースに標準の HTML タグが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40c89-144">`Html.TextBox()`HTML ヘルパーは `<% %>` タグではなく `<%= %>` タグでレンダリングされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="40c89-145">等号を含めない場合は、ブラウザーに何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="40c89-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="40c89-146">ASP.NET MVC フレームワークには、少数のヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="40c89-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="40c89-147">多くの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40c89-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="40c89-148">このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する2つの方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="40c89-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="40c89-149">**リスト2– `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="40c89-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="40c89-150">共有メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="40c89-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="40c89-151">新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す共有メソッドを作成することです。</span><span class="sxs-lookup"><span data-stu-id="40c89-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="40c89-152">たとえば、HTML `<label>` タグをレンダリングする新しい HTML ヘルパーを作成する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="40c89-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="40c89-153">リスト2のクラスを使用して、`<label>`を表示できます。</span><span class="sxs-lookup"><span data-stu-id="40c89-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="40c89-154">**リスト2– `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="40c89-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="40c89-155">リスト2のクラスについては特別なことはありません。</span><span class="sxs-lookup"><span data-stu-id="40c89-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="40c89-156">`Label()` メソッドは、単に文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="40c89-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="40c89-157">リスト3の変更されたインデックスビューでは、`LabelHelper` を使用して HTML `<label>` タグを表示します。</span><span class="sxs-lookup"><span data-stu-id="40c89-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="40c89-158">ビューには、アプリケーション1名前空間をインポートする `<%@ imports %>` ディレクティブが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="40c89-159">**リスト2– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="40c89-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="40c89-160">拡張メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="40c89-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="40c89-161">ASP.NET MVC フレームワークに含まれている標準の HTML ヘルパーと同様に機能する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40c89-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="40c89-162">拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。</span><span class="sxs-lookup"><span data-stu-id="40c89-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="40c89-163">HTML ヘルパーメソッドを作成する場合は、ビューの Html プロパティによって表される `HtmlHelper` クラスに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="40c89-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="40c89-164">リスト3の Visual Basic モジュールは、`Label()` という名前の拡張メソッドを `HtmlHelper` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="40c89-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="40c89-165">このモジュールに関しては、いくつかの点に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40c89-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="40c89-166">最初に、モジュールが `<Extension()>` 属性で修飾されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="40c89-167">この属性を使用するには、`System.Runtime.CompilerServices` 名前空間をインポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="40c89-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="40c89-168">次に、`Label()` メソッドの最初のパラメーターが `HtmlHelper` クラスを表すことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="40c89-169">拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。</span><span class="sxs-lookup"><span data-stu-id="40c89-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="40c89-170">**リスト3– `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="40c89-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="40c89-171">拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、Visual Studio の Intellisense に拡張メソッドが表示されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="40c89-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="40c89-172">唯一の違いは、拡張メソッドには、その横に特殊記号 (下向きの矢印のアイコン) が表示される点です。</span><span class="sxs-lookup"><span data-stu-id="40c89-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="40c89-173">[Html. Label () 拡張メソッドを使用して ![](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="40c89-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="40c89-174">**図 02**: Html. Label () 拡張メソッドの使用 ([クリックしてフルサイズのイメージを表示する](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="40c89-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="40c89-175">リスト4の変更されたインデックスビューでは、Html. Label () 拡張メソッドを使用して、すべての &lt;ラベル&gt; タグをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="40c89-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="40c89-176">**リスト4– `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="40c89-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="40c89-177">要約</span><span class="sxs-lookup"><span data-stu-id="40c89-177">Summary</span></span>

<span data-ttu-id="40c89-178">このチュートリアルでは、カスタム HTML ヘルパーを作成する2つの方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="40c89-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="40c89-179">まず、文字列を返す共有メソッドを作成して、カスタム `Label()` HTML ヘルパーを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="40c89-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="40c89-180">次に、`HtmlHelper` クラスに拡張メソッドを作成して、カスタム `Label()` HTML ヘルパーメソッドを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="40c89-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="40c89-181">このチュートリアルでは、非常に単純な HTML ヘルパーメソッドを構築することに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="40c89-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="40c89-182">HTML ヘルパーは必要に応じて複雑になる可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40c89-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="40c89-183">ツリービュー、メニュー、データベースデータのテーブルなどのリッチコンテンツを表示する HTML ヘルパーを構築できます。</span><span class="sxs-lookup"><span data-stu-id="40c89-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="40c89-184">[前へ](asp-net-mvc-views-overview-vb.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="40c89-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
