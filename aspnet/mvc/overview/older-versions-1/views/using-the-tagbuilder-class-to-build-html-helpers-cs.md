---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: TagBuilder クラスを使用して HTML ヘルパーをC#構築する () |Microsoft Docs
author: StephenWalther
description: Stephen Walther には、TagBuilder クラスという名前の ASP.NET MVC フレームワークの便利なユーティリティクラスが導入されています。 TagBuilder クラスは簡単に使用できます。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485608"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="f6226-104">TagBuilder クラスを使用した HTML ヘルパーのC#構築 ()</span><span class="sxs-lookup"><span data-stu-id="f6226-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>

<span data-ttu-id="f6226-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="f6226-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="f6226-106">Stephen Walther には、TagBuilder クラスという名前の ASP.NET MVC フレームワークの便利なユーティリティクラスが導入されています。</span><span class="sxs-lookup"><span data-stu-id="f6226-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="f6226-107">TagBuilder クラスを使用すると、HTML タグを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="f6226-108">ASP.NET MVC フレームワークには、HTML ヘルパーを構築するときに使用できる TagBuilder クラスという便利なユーティリティクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f6226-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="f6226-109">TagBuilder クラスは、クラスの名前として、HTML タグを簡単に作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f6226-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="f6226-110">この簡単なチュートリアルでは、TagBuilder クラスの概要を説明し、HTML &lt;img&gt; タグをレンダリングする単純な HTML ヘルパーを構築するときに、このクラスを使用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f6226-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="f6226-111">TagBuilder クラスの概要</span><span class="sxs-lookup"><span data-stu-id="f6226-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="f6226-112">TagBuilder クラスは、System.web 名前空間に含まれています。</span><span class="sxs-lookup"><span data-stu-id="f6226-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="f6226-113">次の5つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="f6226-113">It has five methods:</span></span>

- <span data-ttu-id="f6226-114">AddCssClass ()-新しい*class = ""* 属性をタグに追加できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="f6226-115">GenerateId ()-タグに id 属性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="f6226-116">このメソッドは、自動的に id の期間を置き換えます (既定では、ピリオドはアンダースコアに置き換えられます)</span><span class="sxs-lookup"><span data-stu-id="f6226-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="f6226-117">MergeAttribute ()-タグに属性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="f6226-118">このメソッドには複数のオーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="f6226-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="f6226-119">SetInnerText ()-タグの内部テキストを設定できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="f6226-120">内部テキストは、自動的に HTML エンコードされます。</span><span class="sxs-lookup"><span data-stu-id="f6226-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="f6226-121">ToString ()-タグを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="f6226-122">通常のタグ、開始タグ、終了タグ、または自己終了タグを作成するかどうかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="f6226-123">TagBuilder クラスには、次の4つの重要なプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="f6226-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="f6226-124">Attributes-タグのすべての属性を表します。</span><span class="sxs-lookup"><span data-stu-id="f6226-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="f6226-125">IdAttributeDotReplacement-GenerateId () メソッドがピリオドを置き換えるために使用する文字を表します (既定値はアンダースコアです)。</span><span class="sxs-lookup"><span data-stu-id="f6226-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="f6226-126">InnerHTML-タグの内部コンテンツを表します。</span><span class="sxs-lookup"><span data-stu-id="f6226-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="f6226-127">このプロパティに文字列を割り当てると、文字列は HTML エンコード*されません*。</span><span class="sxs-lookup"><span data-stu-id="f6226-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="f6226-128">TagName-タグの名前を表します。</span><span class="sxs-lookup"><span data-stu-id="f6226-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="f6226-129">これらのメソッドとプロパティは、HTML タグを構築するために必要なすべての基本メソッドとプロパティを提供します。</span><span class="sxs-lookup"><span data-stu-id="f6226-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="f6226-130">実際に TagBuilder クラスを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f6226-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="f6226-131">代わりに StringBuilder クラスを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f6226-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="f6226-132">しかし、TagBuilder クラスを使用すると、作業が楽になります。</span><span class="sxs-lookup"><span data-stu-id="f6226-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="f6226-133">イメージ HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="f6226-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="f6226-134">TagBuilder クラスのインスタンスを作成するときに、TagBuilder コンストラクターにビルドするタグの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="f6226-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="f6226-135">次に、AddCssClass メソッドや MergeAttribute () メソッドなどのメソッドを呼び出して、タグの属性を変更できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="f6226-136">最後に、ToString () メソッドを呼び出してタグを表示します。</span><span class="sxs-lookup"><span data-stu-id="f6226-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="f6226-137">たとえば、リスト1には、イメージ HTML ヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f6226-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="f6226-138">イメージヘルパーは、HTML &lt;img&gt; タグを表す TagBuilder を使用して内部的に実装されます。</span><span class="sxs-lookup"><span data-stu-id="f6226-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="f6226-139">**リスト 1-イメージの一覧表示**</span><span class="sxs-lookup"><span data-stu-id="f6226-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="f6226-140">リスト1のクラスには、Image という名前の静的オーバーロードメソッドが2つ含まれています。</span><span class="sxs-lookup"><span data-stu-id="f6226-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="f6226-141">Image () メソッドを呼び出すと、HTML 属性のセットを表すオブジェクトを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="f6226-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="f6226-142">Tagbuilder. MergeAttribute () メソッドを使用して、src 属性などの個々の属性を TagBuilder に追加する方法に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f6226-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="f6226-143">さらに、tagbuilder に属性のコレクションを追加する方法についても説明しています。</span><span class="sxs-lookup"><span data-stu-id="f6226-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="f6226-144">MergeAttributes () メソッドは、ディクショナリ&lt;string、object&gt; パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f6226-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="f6226-145">RouteValueDictionary クラスは、属性のコレクションを表すオブジェクトを、文字列、オブジェクト&gt;&lt;ディクショナリに変換するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6226-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="f6226-146">イメージヘルパーを作成した後は、他の標準 HTML ヘルパーと同様に、ASP.NET MVC ビューでヘルパーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f6226-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="f6226-147">リスト2のビューでは、イメージヘルパーを使用して Xbox の同じイメージが2回表示されます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="f6226-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="f6226-148">Image () ヘルパーは、HTML 属性コレクションの有無にかかわらず呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="f6226-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="f6226-149">**リスト 2-ホーム \ aspx**</span><span class="sxs-lookup"><span data-stu-id="f6226-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

<span data-ttu-id="f6226-150">[[新しいプロジェクト] ダイアログボックスの ![](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f6226-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="f6226-151">**図 01**: イメージヘルパーを使用[する (クリックすると、フルサイズの画像が表示](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="f6226-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>

<span data-ttu-id="f6226-152">イメージヘルパーに関連付けられている名前空間を、インデックス .aspx ビューの先頭にインポートする必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f6226-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="f6226-153">ヘルパーは、次のディレクティブを使用してインポートされます。</span><span class="sxs-lookup"><span data-stu-id="f6226-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="f6226-154">[前へ](creating-custom-html-helpers-cs.md)
> [次へ](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f6226-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>
