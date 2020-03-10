---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトでのヘルパーの作成と使用 |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーを作成する方法について説明します。 ヘルパーは再利用可能なコンポーネントであり、コードと、パフォーマンスに対するマークアップを含んでいます...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454306"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="5766e-104">ASP.NET Web ページ (Razor) サイトでのヘルパーの作成と使用</span><span class="sxs-lookup"><span data-stu-id="5766e-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="5766e-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5766e-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5766e-106">この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5766e-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="5766e-107">*ヘルパー*は、煩雑または複雑なタスクを実行するためのコードとマークアップを含む再利用可能なコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="5766e-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="5766e-108">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="5766e-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="5766e-109">単純なヘルパーを作成して使用する方法。</span><span class="sxs-lookup"><span data-stu-id="5766e-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="5766e-110">この記事で導入された ASP.NET 機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5766e-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="5766e-111">`@helper` 構文。</span><span class="sxs-lookup"><span data-stu-id="5766e-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5766e-112">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="5766e-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5766e-113">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="5766e-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="5766e-114">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="5766e-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="5766e-115">ヘルパーの概要</span><span class="sxs-lookup"><span data-stu-id="5766e-115">Overview of Helpers</span></span>

<span data-ttu-id="5766e-116">サイト内の異なるページで同じタスクを実行する必要がある場合は、ヘルパーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5766e-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="5766e-117">ASP.NET Web ページには多くのヘルパーが含まれており、ダウンロードしてインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="5766e-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="5766e-118">(ASP.NET Web ページの組み込みヘルパーの一覧については、「 [ASP.NET API クイックリファレンス](https://go.microsoft.com/fwlink/?LinkId=202907)」を参照してください)。既存のヘルパーがニーズに合わない場合は、独自のヘルパーを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="5766e-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="5766e-119">ヘルパーを使用すると、複数のページで共通のコードブロックを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5766e-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="5766e-120">ページ内で通常の段落とは別に設定されたノート項目を作成することがよくあるとします。</span><span class="sxs-lookup"><span data-stu-id="5766e-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="5766e-121">メモは、境界線を持つボックスとしてスタイルを作成する `<div>` 要素として作成される場合があります。</span><span class="sxs-lookup"><span data-stu-id="5766e-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="5766e-122">メモを表示するたびに、この同じマークアップをページに追加するのではなく、マークアップをヘルパーとしてパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="5766e-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="5766e-123">その後、必要な場所に1行のコードでメモを挿入できます。</span><span class="sxs-lookup"><span data-stu-id="5766e-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="5766e-124">このようなヘルパーを使用すると、各ページのコードがより簡単に読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="5766e-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="5766e-125">また、ノートの外観を変更する必要がある場合は、マークアップを1か所で変更できるので、サイトの保守が容易になります。</span><span class="sxs-lookup"><span data-stu-id="5766e-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="5766e-126">ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="5766e-126">Creating a Helper</span></span>

<span data-ttu-id="5766e-127">この手順では、説明したように、メモを作成するヘルパーを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="5766e-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="5766e-128">これは簡単な例ですが、カスタムヘルパーには、必要なマークアップと ASP.NET のコードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="5766e-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="5766e-129">Web サイトのルートフォルダーで、 *App\_Code*という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5766e-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="5766e-130">これは ASP.NET で予約されているフォルダー名であり、ヘルパーなどのコンポーネントのコードを配置できます。</span><span class="sxs-lookup"><span data-stu-id="5766e-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="5766e-131">*アプリ\_コード*フォルダーで、新しい*cshtml*ファイルを作成し、 *myhelpers. cshtml*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5766e-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="5766e-132">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5766e-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="5766e-133">このコードでは、`@helper` 構文を使用して `MakeNote`という名前の新しいヘルパーを宣言します。</span><span class="sxs-lookup"><span data-stu-id="5766e-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="5766e-134">この特定のヘルパーを使用すると、テキストとマークアップの組み合わせを含むことができる `content` という名前のパラメーターを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="5766e-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="5766e-135">ヘルパーは、`@content` 変数を使用して、ノート本体に文字列を挿入します。</span><span class="sxs-lookup"><span data-stu-id="5766e-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="5766e-136">このファイルは*myhelpers. cshtml*という名前であることに注意してください。ヘルパーには `MakeNote`という名前が付けられています。</span><span class="sxs-lookup"><span data-stu-id="5766e-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="5766e-137">複数のカスタムヘルパーを1つのファイルに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="5766e-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="5766e-138">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5766e-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="5766e-139">ページでのヘルパーの使用</span><span class="sxs-lookup"><span data-stu-id="5766e-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="5766e-140">ルートフォルダーに、 *TestHelper*という名前の新しい空のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="5766e-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="5766e-141">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="5766e-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="5766e-142">作成したヘルパーを呼び出すには、`@` を使用し、その後にヘルパーがあるファイル名、ドット、ヘルパー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="5766e-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="5766e-143">(*アプリ\_コード*フォルダーに複数のフォルダーがある場合は、`@FolderName.FileName.HelperName` 構文を使用して、入れ子になったフォルダーレベルでヘルパーを呼び出すことができます)。</span><span class="sxs-lookup"><span data-stu-id="5766e-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="5766e-144">かっこ内に引用符で囲んだテキストは、ヘルパーが web ページのノートの一部として表示されるテキストです。</span><span class="sxs-lookup"><span data-stu-id="5766e-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="5766e-145">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="5766e-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="5766e-146">ヘルパーは、2つの段落の間でヘルパーを呼び出したときに、ノート項目の右側を生成します。</span><span class="sxs-lookup"><span data-stu-id="5766e-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![ブラウザー内のページを示すスクリーンショットと、指定したテキストをボックスに配置するためのマークアップをヘルパーが生成した方法を示します。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="5766e-148">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="5766e-148">Additional Resources</span></span>

<span data-ttu-id="5766e-149">[Razor ヘルパーとしての水平メニュー](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。</span><span class="sxs-lookup"><span data-stu-id="5766e-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="5766e-150">Mike Pope によるこのブログエントリは、マークアップ、CSS、およびコードを使用して、水平メニューをヘルパーとして作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5766e-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="5766e-151">[WebMatrix と ASP.NET MVC3 の ASP.NET Web ページヘルパーでの HTML5 の活用](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5766e-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="5766e-152">Sam Abraham によるこのブログエントリは、HTML5 `Canvas` 要素をレンダリングするヘルパーを示しています。</span><span class="sxs-lookup"><span data-stu-id="5766e-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="5766e-153">[WebMatrix での @Helpers と @Functions の違い](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。</span><span class="sxs-lookup"><span data-stu-id="5766e-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="5766e-154">Mike Brind によるこのブログエントリでは、`@helper` 構文と `@function` 構文、およびそれぞれを使用するタイミングについて説明します。</span><span class="sxs-lookup"><span data-stu-id="5766e-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
