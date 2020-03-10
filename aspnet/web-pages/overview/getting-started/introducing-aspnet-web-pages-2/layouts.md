---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET Web ページの概要-一貫したレイアウトの作成 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、レイアウトを使用して、ASP.NET Web ページを使用するサイト上のページの一貫性のある検索を作成する方法について説明します。 完了したことを前提としています...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422746"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="3ec79-104">ASP.NET Web ページの概要-一貫したレイアウトの作成</span><span class="sxs-lookup"><span data-stu-id="3ec79-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="3ec79-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ec79-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3ec79-106">このチュートリアルでは、*レイアウト*を使用して、ASP.NET Web ページを使用するサイト上のページの一貫性のある検索を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="3ec79-107">[ASP.NET Web ページでデータベースデータを削除](https://go.microsoft.com/fwlink/?LinkId=251584)して、シリーズを完了していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="3ec79-108">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3ec79-109">レイアウトページとは何ですか。</span><span class="sxs-lookup"><span data-stu-id="3ec79-109">What a layout page is.</span></span>
> - <span data-ttu-id="3ec79-110">レイアウトページと動的なコンテンツを結合する方法。</span><span class="sxs-lookup"><span data-stu-id="3ec79-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="3ec79-111">レイアウトページに値を渡す方法。</span><span class="sxs-lookup"><span data-stu-id="3ec79-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="3ec79-112">レイアウトについて</span><span class="sxs-lookup"><span data-stu-id="3ec79-112">About Layouts</span></span>

<span data-ttu-id="3ec79-113">これまでに作成したページはすべて完成し、スタンドアロンページです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="3ec79-114">これらはすべて同じサイトに属していますが、共通の要素や標準的な外観を持っていません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="3ec79-115">ほとんどのサイトには、一貫した外観とレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="3ec79-116">たとえば、 [Microsoft.com/web](https://www.microsoft.com/web/)サイトに移動して、すべてのページがレイアウト全体と視覚テーマに準拠していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![ヘッダー、ナビゲーション領域、コンテンツ領域、およびフッターのレイアウトを表示する Microsoft.com/web サイトページ](layouts/_static/image1.png)

<span data-ttu-id="3ec79-118">このレイアウトを*効率的*に作成する方法としては、各ページで個別にヘッダー、ナビゲーションバー、およびフッターを定義する方法があります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="3ec79-119">毎回同じマークアップを複製します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="3ec79-120">何かを変更する (たとえば、フッターを更新する) 場合は、各ページを個別に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="3ec79-121">ここで*レイアウトページ*が登場します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="3ec79-122">ASP.NET Web ページでは、サイト上のページのコンテナー全体を提供するレイアウトページを定義できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="3ec79-123">たとえば、[レイアウト] ページには、ヘッダー、ナビゲーション領域、およびフッターを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="3ec79-124">レイアウトページには、メインコンテンツが配置されるプレースホルダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="3ec79-125">その後、マークアップを含む個々のコンテンツページと、そのページのみのコードを定義できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="3ec79-126">コンテンツページは HTML ページ全体である必要はありません。`<body>` 要素を持つ必要もありません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="3ec79-127">また、コンテンツを表示するレイアウトページを ASP.NET に伝えるコード行もあります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="3ec79-128">このリレーションシップのしくみを次の図に示します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-128">Here's a picture that shows roughly how this relationship works:</span></span>

![2つのコンテンツページと、それらが適合するレイアウトページを示す概念図](layouts/_static/image2.png)

<span data-ttu-id="3ec79-130">この相互作用は、実際に動作していることを確認するとわかりやすくなります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="3ec79-131">このチュートリアルでは、レイアウトを使用するようにムービーページを変更します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="3ec79-132">レイアウトページの追加</span><span class="sxs-lookup"><span data-stu-id="3ec79-132">Adding a Layout Page</span></span>

<span data-ttu-id="3ec79-133">まず、ヘッダー、フッター、およびメインコンテンツ用の領域を含む一般的なページレイアウトを定義するレイアウトページを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="3ec79-134">Webweb ムービーサイトで、 *\_Layout. cshtml*という名前の cshtml ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="3ec79-135">先頭のアンダースコア (`_`) 文字は重要です。</span><span class="sxs-lookup"><span data-stu-id="3ec79-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="3ec79-136">ページの名前がアンダースコアで始まる場合、ASP.NET はそのページをブラウザーに直接送信しません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="3ec79-137">この規則を使用すると、サイトに必要なページを定義できますが、ユーザーが直接要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="3ec79-138">ページのコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="3ec79-139">ご覧のように、このマークアップは `<div>` 要素を使用してページ内の3つのセクションを定義し、3つのセクションを保持するもう1つの `<div>` 要素を使用する HTML にすぎません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="3ec79-140">フッターには、ページ内の現在の年を表示する Razor コードの `@DateTime.Now.Year`が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="3ec79-141">「 *.Css*」という名前のスタイルシートへのリンクが表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3ec79-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="3ec79-142">スタイルシートには、要素の物理的なレイアウトの詳細が定義されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="3ec79-143">これは、すぐに作成します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-143">You'll create that in a moment.</span></span>

<span data-ttu-id="3ec79-144">この *\_Layout*ページの通常とは異なる機能は、`@Render.Body()` 行です。</span><span class="sxs-lookup"><span data-stu-id="3ec79-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="3ec79-145">これは、このレイアウトが別のページにマージされたときにコンテンツが移動するプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="3ec79-146">.Css ファイルの追加</span><span class="sxs-lookup"><span data-stu-id="3ec79-146">Adding a .css File</span></span>

<span data-ttu-id="3ec79-147">ページ上の要素の実際の配置 (外観) を定義するには、カスケードスタイルシート (CSS) 規則を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3ec79-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="3ec79-148">そのため、新しいレイアウトのルールを含む *.css*ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="3ec79-149">WebMatrix で、サイトのルートを選択します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="3ec79-150">次に、リボンの **[ファイル]** タブで、 **[新規]** ボタンの下の矢印をクリックし、 **[新しいフォルダー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3ec79-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![リボンの [新規] の下にある [新しいフォルダー] オプション。](layouts/_static/image3.png)

<span data-ttu-id="3ec79-152">新しいフォルダーの*スタイル*の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-152">Name the new folder *Styles*.</span></span>

![新しいフォルダーに ' Styles ' という名前を付ける](layouts/_static/image4.png)

<span data-ttu-id="3ec79-154">[新しい*スタイル*] フォルダー内に、「 *.css*」という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![新しいムービーの .css ファイルを作成する](layouts/_static/image5.png)

<span data-ttu-id="3ec79-156">新しい *.css*ファイルの内容を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="3ec79-157">これらの CSS 規則についてはあまり詳しく説明しませんが、2つの点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="3ec79-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="3ec79-158">1つの方法として、フォントとサイズの設定に加えて、ルールでは、ヘッダー、フッター、およびメインコンテンツ領域の位置を設定するための絶対配置が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="3ec79-159">CSS での配置を初めて使用する場合は、W3Schools サイトの[css の配置](http://www.w3schools.com/css/css_positioning.asp)に関するチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3ec79-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="3ec79-160">もう1つ注意すべき点は、一番下には、最初に*ムービーの cshtml*ファイルで定義されたスタイルルールがコピーされていることです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="3ec79-161">これらのルールは、 [ASP.NET Web ページチュートリアルを使用してデータを表示する方法の概要](https://go.microsoft.com/fwlink/?LinkId=251580)で、`WebGrid` ヘルパーが、テーブルにストライプを追加したマークアップを表示するようにするために使用されていました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="3ec79-162">(スタイル定義に *.css*ファイルを使用する場合は、サイト全体のスタイルルールを配置することもできます)。</span><span class="sxs-lookup"><span data-stu-id="3ec79-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="3ec79-163">レイアウトを使用するようにムービーファイルを更新する</span><span class="sxs-lookup"><span data-stu-id="3ec79-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="3ec79-164">これで、サイト内の既存のファイルを更新して、新しいレイアウトを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="3ec79-165">ムービーの*cshtml*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="3ec79-166">先頭に、コードの最初の行として、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="3ec79-167">これで、このページは次のように開始されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="3ec79-168">この1行のコードでは、*ムービー*ページが実行されたときに、 *\_* ASP.NET ファイルにマージする必要があることがわかります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="3ec79-169">現在、この*ムービー*ファイルではレイアウトページが使用されているため、 *\_layout*ファイルによって処理される、*ムービーの cshtml*ページからマークアップを削除できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="3ec79-170">`<!DOCTYPE>`、`<html>`、および `<body>` の開始タグと終了タグを取得します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="3ec79-171">`<head>` の要素とその内容をすべて取得し*ます。* これには、グリッドのスタイルルールが含まれています。これは、これらのルールが .css ファイルに格納されているためです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="3ec79-172">この時点で、既存の `<h1>` 要素を `<h2>` 要素に変更します。レイアウトページに `<h1>` 要素が既に存在します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="3ec79-173">`<h2>` テキストを「ムービーの一覧表示」に変更します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="3ec79-174">通常、このような変更をコンテンツページで行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="3ec79-175">レイアウトページを使用してサイトを開始するときに、これらすべての要素を開始せずにコンテンツページを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="3ec79-176">ただし、この場合は、スタンドアロンページをレイアウトを使用するものに変換するので、クリーンアップが少しあります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="3ec79-177">完了すると、次のような*ムービー*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="3ec79-178">レイアウトのテスト</span><span class="sxs-lookup"><span data-stu-id="3ec79-178">Testing the Layout</span></span>

<span data-ttu-id="3ec79-179">これで、レイアウトがどのように見えるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="3ec79-180">WebMatrix で、[*ムービー* ] ページを右クリックし、 **[ブラウザーで起動]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="3ec79-181">ブラウザーがページを表示すると、次のようなページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-181">When the browser displays the page, it looks like this page:</span></span>

![レイアウトを使用してレンダリングされたムービーページ](layouts/_static/image6.png)

<span data-ttu-id="3ec79-183">ASP.NET は、ページの内容を、`RenderBody` メソッドがである *\_のレイアウト*にマージしました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="3ec79-184">もちろん、\_の*レイアウトの cshtml*ページでは、ページの外観を定義する *.css*ファイルが参照されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="3ec79-185">レイアウトを使用するように AddMovie ページを更新する</span><span class="sxs-lookup"><span data-stu-id="3ec79-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="3ec79-186">レイアウトの実際の利点は、サイト内のすべてのページに使用できることです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="3ec79-187">*Addmovie. cshtml*ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="3ec79-188">最初に、 *Addmovie. cshtml*ページには、検証エラーメッセージの外観を定義する CSS ルールがいくつかありました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="3ec79-189">ここでは、サイトの *.css*ファイルがあるため、これらのルールを *.css*ファイルに移動できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="3ec79-190">これらのファイルを、もう一度*Addmovie*ファイルから削除し、*ムービーの .css*ファイルの一番下に追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="3ec79-191">次のルールを移動しています:</span><span class="sxs-lookup"><span data-stu-id="3ec79-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="3ec79-192">次に、[ *Addmovie. cshtml* ] で同じ種類の変更を加え*ます。* ここでは、`Layout="~/_Layout.cshtml;` を追加し、余分な HTML マークアップを削除します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="3ec79-193">`<h1>` 要素を `<h2>` に変更します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="3ec79-194">完了すると、ページは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="3ec79-195">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-195">Run the page.</span></span> <span data-ttu-id="3ec79-196">次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-196">Now it looks like this illustration:</span></span>

![レイアウトを使用してレンダリングされた ' ムービーの追加 ' ページ](layouts/_static/image7.png)

<span data-ttu-id="3ec79-198">サイト内のページ ( *Editmovie. cshtml*と*DeleteMovie*) に同様の変更を行う場合。</span><span class="sxs-lookup"><span data-stu-id="3ec79-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="3ec79-199">ただし、これを行う前に、レイアウトに別の変更を加えて、もう少し柔軟にすることができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="3ec79-200">タイトル情報をレイアウトページに渡す</span><span class="sxs-lookup"><span data-stu-id="3ec79-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="3ec79-201">作成した *\_の Layout*ページには、"マイムービーサイト" に設定されている `<title>` 要素があります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="3ec79-202">ほとんどのブラウザーでは、この要素の内容がタブ上のテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-202">Most browsers display the content of this element as the text on a tab:</span></span>

![ブラウザータブに表示されるページの &lt;タイトル&gt; 要素](layouts/_static/image8.png)

<span data-ttu-id="3ec79-204">このタイトル情報は汎用的なものです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-204">This title information is generic.</span></span> <span data-ttu-id="3ec79-205">タイトルのテキストを現在のページにより具体的に指定するとします。</span><span class="sxs-lookup"><span data-stu-id="3ec79-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="3ec79-206">(タイトルのテキストは、検索エンジンによって、ページの内容を判別するためにも使用されます)。Movie *. cshtml*や*addmovie. cshtml*などのコンテンツページの情報をレイアウトページに渡し、その情報を使用してレイアウトページの表示内容をカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="3ec79-207">もう一度、[*ムービー* ] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="3ec79-208">上部にあるコードで、次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="3ec79-209">`Page` オブジェクトは、すべての*cshtml*ページで使用でき、この目的のために、ページとそのレイアウトの間で情報を共有します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="3ec79-210">*\_Layout*ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="3ec79-211">次のマークアップのように `<title>` 要素を変更します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="3ec79-212">このコードは、`Page.Title` プロパティ内の任意のものを、ページ内のその位置にある任意の場所にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="3ec79-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="3ec79-213">[*ムービー* ] ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="3ec79-214">今度は、[ブラウザー] タブに `Page.Title`の値として渡された内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![タイトルが動的に作成されたブラウザータブ](layouts/_static/image9.png)

<span data-ttu-id="3ec79-216">必要に応じて、ブラウザーでページソースを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="3ec79-217">`<title>` 要素が `<title>List Movies</title>`としてレンダリングされていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="3ec79-218">**Page オブジェクト**</span><span class="sxs-lookup"><span data-stu-id="3ec79-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="3ec79-219">`Page` の便利な機能は、動的なオブジェクトであり、`Title` プロパティは固定または予約された名前ではないということです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="3ec79-220">`Page` オブジェクトの値には *、任意*の名前を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="3ec79-221">たとえば、`Page.CurrentName` または `Page.MyPage`という名前のプロパティを使用して、タイトルを簡単に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="3ec79-222">唯一の制限は、名前を付けることができるプロパティの通常の規則に従う必要があることです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="3ec79-223">(たとえば、名前にスペースを含めることはできません)。</span><span class="sxs-lookup"><span data-stu-id="3ec79-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="3ec79-224">`Page` オブジェクトを使用して、任意の数の値を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="3ec79-225">ムービー情報をレイアウトページに渡す必要がある場合は、`Page.MovieTitle`、`Page.Genre` と `Page.MovieYear`などを使用して値を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="3ec79-226">(または、情報を格納するために開発したその他のすべての名前)。唯一の要件として、[コンテンツ] ページと [レイアウト] ページで同じ名前を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ec79-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="3ec79-227">`Page` オブジェクトを使用して渡す情報は、レイアウトページに表示されるテキストのみに制限されていません。</span><span class="sxs-lookup"><span data-stu-id="3ec79-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="3ec79-228">レイアウトページに値を渡すことができます。次に、レイアウトページ内のコードで値を使用して、ページのセクション、使用する *.css*ファイルなどを表示するかどうかを決定できます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="3ec79-229">`Page` オブジェクトで渡す値は、コードで使用する他の値と同じです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="3ec79-230">値がコンテンツページに由来し、レイアウトページに渡されるだけです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="3ec79-231">*Addmovie. cshtml*ページを開き、 *addmovie. cshtml*ページのタイトルを提供するコードの先頭に行を追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="3ec79-232">*Addmovie. cshtml*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="3ec79-233">新しいタイトルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-233">You see the new title there:</span></span>

![[ムービーの追加] タイトルが動的に作成されたブラウザータブ](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="3ec79-235">レイアウトを使用するために残りのページを更新する</span><span class="sxs-lookup"><span data-stu-id="3ec79-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="3ec79-236">これで、サイト内の残りのページを完了して、新しいレイアウトを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="3ec79-237">*Editmovie. cshtml*と*DeleteMovie*をもう一度開き、それぞれに同じ変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="3ec79-238">レイアウトページにリンクするコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="3ec79-239">ページのタイトルを設定する行を追加します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="3ec79-240">または</span><span class="sxs-lookup"><span data-stu-id="3ec79-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="3ec79-241">余分な HTML マークアップをすべて削除します。基本的には、`<body>` 要素の内側にあるビットだけを残します (上部にあるコードブロックを使用します)。</span><span class="sxs-lookup"><span data-stu-id="3ec79-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="3ec79-242">`<h1>` 要素を `<h2>` 要素に変更します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="3ec79-243">これらの変更を行ったら、それぞれをテストし、正しく表示されていること、およびタイトルが正しいことを確認します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="3ec79-244">レイアウトページについての分離の考え</span><span class="sxs-lookup"><span data-stu-id="3ec79-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="3ec79-245">このチュートリアルでは、 *\_の Layout*ページを作成し、`RenderBody` メソッドを使用して別のページのコンテンツをマージしました。</span><span class="sxs-lookup"><span data-stu-id="3ec79-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="3ec79-246">これは、Web ページでレイアウトを使用するための基本的なパターンです。</span><span class="sxs-lookup"><span data-stu-id="3ec79-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="3ec79-247">レイアウトページには、ここでは説明しなかった機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="3ec79-248">たとえば、レイアウトページを入れ子にすることができ、1つのレイアウトページで別のレイアウトページを参照することができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="3ec79-249">入れ子になったレイアウトは、異なるレイアウトを必要とするサイトのサブセクションを操作する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="3ec79-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="3ec79-250">また、追加のメソッド (`RenderSection`など) を使用して、レイアウトページで名前付きセクションを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="3ec79-251">レイアウトページと *.css*ファイルの組み合わせは強力です。</span><span class="sxs-lookup"><span data-stu-id="3ec79-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="3ec79-252">次のチュートリアルシリーズで説明するように、WebMatrix では、*テンプレート*に基づいてサイトを作成できます。これにより、作成済みの機能を持つサイトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="3ec79-253">テンプレートでは、レイアウトページと CSS を使用して、見栄えの良いサイトや、メニューのような機能を持つサイトを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="3ec79-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="3ec79-254">次に示すのは、テンプレートに基づいたサイトのホームページのスクリーンショットです。レイアウトページと CSS を使用する機能が表示されています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![WebMatrix サイトテンプレートによって作成されたレイアウトで、ヘッダー、ナビゲーション領域、コンテンツエリア、オプションのセクション、およびログインリンクが表示されます。](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="3ec79-256">[ムービーの完全な一覧表示] ページ (レイアウトページを使用するように更新)</span><span class="sxs-lookup"><span data-stu-id="3ec79-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="3ec79-257">[ムービーの追加] ページのページの完全な一覧 (レイアウト用に更新)</span><span class="sxs-lookup"><span data-stu-id="3ec79-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="3ec79-258">[ムービーの削除] ページのページの完全な一覧 (レイアウト用に更新)</span><span class="sxs-lookup"><span data-stu-id="3ec79-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="3ec79-259">[ムービーの編集] ページの完全なページリスト (レイアウト用に更新)</span><span class="sxs-lookup"><span data-stu-id="3ec79-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="3ec79-260">次へ</span><span class="sxs-lookup"><span data-stu-id="3ec79-260">Coming Up Next</span></span>

<span data-ttu-id="3ec79-261">次のチュートリアルでは、すべてのユーザーが閲覧できるように、サイトをインターネットに発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ec79-262">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="3ec79-262">Additional Resources</span></span>

- <span data-ttu-id="3ec79-263">[一貫性のある外観の作成](https://go.microsoft.com/fwlink/?LinkID=202891): レイアウトの操作に関する詳細情報を提供する記事です。</span><span class="sxs-lookup"><span data-stu-id="3ec79-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="3ec79-264">また、コンテンツの一部を表示または非表示にするレイアウトページに値を渡す方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="3ec79-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="3ec79-265">[Razor を使用した入れ子になったレイアウトページ](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor): Mike brind ブログでは、レイアウトページを入れ子にする方法の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3ec79-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="3ec79-266">(ページのダウンロードも含まれています)。</span><span class="sxs-lookup"><span data-stu-id="3ec79-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ec79-267">[前へ](deleting-data.md)
> [次へ](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="3ec79-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
