---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: ASP.NET Web ページ (Razor) サイトでの一貫したレイアウトの作成 |Microsoft Docs
author: Rick-Anderson
description: サイトの web ページをより効率的に作成するために、web サイト用に再利用可能なコンテンツのブロック (ヘッダーやフッターなど) を作成することができます。
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509098"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="fb0f5-103">ASP.NET Web ページ (Razor) サイトでの一貫したレイアウトの作成</span><span class="sxs-lookup"><span data-stu-id="fb0f5-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="fb0f5-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fb0f5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fb0f5-105">この記事では、ASP.NET Web ページ (Razor) web サイトのレイアウトページを使用して、再利用可能なコンテンツのブロック (ヘッダーやフッターなど) を作成し、サイト内のすべてのページに一貫した外観を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="fb0f5-106">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="fb0f5-107">ヘッダーやフッターなどの再利用可能なコンテンツのブロックを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="fb0f5-108">レイアウトを使用して、サイト内のすべてのページに一貫した外観を作成する方法。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="fb0f5-109">実行時にレイアウトページにデータを渡す方法。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="fb0f5-110">この記事で導入された ASP.NET 機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="fb0f5-111">コンテンツブロックは、複数のページに挿入される HTML 形式のコンテンツを含むファイルです。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="fb0f5-112">レイアウトページ: web サイト上のページで共有できる HTML 形式のコンテンツが含まれているページです。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="fb0f5-113">`RenderPage`、`RenderBody`、および `RenderSection` メソッド。ページ要素を挿入する場所を ASP.NET に指示します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="fb0f5-114">コンテンツブロックとレイアウトページの間でデータを共有できるようにする `PageData` ディクショナリ。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fb0f5-115">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="fb0f5-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fb0f5-116">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="fb0f5-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="fb0f5-117">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-layout-pages"></a><span data-ttu-id="fb0f5-118">レイアウトページについて</span><span class="sxs-lookup"><span data-stu-id="fb0f5-118">About Layout Pages</span></span>

<span data-ttu-id="fb0f5-119">多くの web サイトには、ヘッダーやフッターなどのすべてのページに表示されるコンテンツや、ログインしていることをユーザーに通知するボックスがあります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="fb0f5-120">ASP.NET を使用すると、通常の web ページと同様に、テキスト、マークアップ、およびコードを含めることができるコンテンツブロックを含む別のファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="fb0f5-121">その後、情報を表示するサイトの他のページにコンテンツブロックを挿入できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="fb0f5-122">このようにして、すべてのページに同じコンテンツをコピーして貼り付ける必要はありません。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="fb0f5-123">このような共通コンテンツを作成すると、サイトの更新も容易になります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="fb0f5-124">コンテンツを変更する必要がある場合は、単に1つのファイルを更新するだけで、コンテンツが挿入されるすべての場所に変更が反映されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="fb0f5-125">次の図は、コンテンツブロックがどのように機能するかを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="fb0f5-126">ブラウザーが web サーバーからページを要求すると、ASP.NET は、メインページで `RenderPage` メソッドが呼び出される位置にコンテンツブロックを挿入します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="fb0f5-127">完成した (マージされた) ページがブラウザーに送信されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-127">The finished (merged) page is then sent to the browser.</span></span>

![RenderPage メソッドが参照されているページを現在のページに挿入する方法を示す概念図。](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="fb0f5-129">この手順では、別のファイルに配置されている2つのコンテンツブロック (ヘッダーとフッター) を参照するページを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="fb0f5-130">これらの同じコンテンツブロックは、サイト内のどのページでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="fb0f5-131">完了すると、次のようなページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-131">When you're done, you'll get a page like this:</span></span>

![RenderPage メソッドの呼び出しを含むページを実行した結果として得られるブラウザー内のページを示すスクリーンショット。](3-creating-a-consistent-look/_static/image2.png)

1. <span data-ttu-id="fb0f5-133">Web サイトのルートフォルダーに、" *Index. cshtml*" という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="fb0f5-134">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="fb0f5-135">ルートフォルダーに、 *Shared*という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fb0f5-136">Web ページ間で共有されるファイルは、*共有*という名前のフォルダーに格納するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="fb0f5-137">*共有*フォルダーに、 *\_Header*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="fb0f5-138">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="fb0f5-139">ファイル名は、プレフィックスとしてアンダースコア (\_) を使用して *\_ヘッダーです。*</span><span class="sxs-lookup"><span data-stu-id="fb0f5-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="fb0f5-140">ASP.NET の名前がアンダースコアで始まる場合、ページはブラウザーに送信されません。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="fb0f5-141">これにより、これらのページを直接 (誤って、またはそれ以外の方法で) 要求できなくなります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="fb0f5-142">アンダースコアを使用して、コンテンツブロックのあるページに名前を付けることをお勧めします。実際には、他のページに挿入さ&#8212;れることがあるページをユーザーに要求することはありません。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="fb0f5-143">*共有*フォルダーに、 *\_Footer. cshtml*という名前のファイルを作成し、内容を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="fb0f5-144">次に示すように、 *Index. cshtml*ページで、`RenderPage` メソッドに2つの呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="fb0f5-145">これは、web ページにコンテンツブロックを挿入する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="fb0f5-146">`RenderPage` メソッドを呼び出し、その時点で内容を挿入するファイルの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="fb0f5-147">ここでは、 *\_Header*ファイルと *\_フッター*ファイルの内容を、*インデックスの cshtml*ファイルに挿入しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="fb0f5-148">ブラウザーで、 *Index. cshtml*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="fb0f5-149">(WebMatrix の **[ファイル]** ワークスペースで、ファイルを右クリックし、 **[ブラウザーで起動]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="fb0f5-150">ブラウザーでページソースを表示します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-150">In the browser, view the page source.</span></span> <span data-ttu-id="fb0f5-151">(たとえば、Internet Explorer で、ページを右クリックし、[ソースの**表示**] をクリックします)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="fb0f5-152">これにより、ブラウザーに送信された web ページマークアップが表示されます。これにより、インデックスページマークアップがコンテンツブロックと結合されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="fb0f5-153">次の例は、 *Index. cshtml*に対してレンダリングされるページソースを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="fb0f5-154">*Index. cshtml*に挿入した `RenderPage` への呼び出しは、ヘッダーファイルとフッターファイルの実際の内容に置き換えられています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="fb0f5-155">レイアウトページを使用して一貫した外観を作成する</span><span class="sxs-lookup"><span data-stu-id="fb0f5-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="fb0f5-156">ここまでで、同じコンテンツを複数のページに簡単に含めることができました。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="fb0f5-157">サイトの一貫性のある外観を作成するためのより体系的な方法は、レイアウトページを使用することです。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="fb0f5-158">レイアウトページは web ページの構造を定義しますが、実際のコンテンツは含まれません。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="fb0f5-159">レイアウトページを作成したら、そのコンテンツを含む web ページを作成して、レイアウトページにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="fb0f5-160">これらのページを表示すると、レイアウトページに従って書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="fb0f5-161">(この意味では、レイアウトページは他のページで定義されているコンテンツの一種のテンプレートとして機能します)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="fb0f5-162">レイアウトページは HTML ページと同じですが、`RenderBody` メソッドの呼び出しが含まれている点が異なります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="fb0f5-163">[レイアウト] ページの `RenderBody` メソッドの位置によって、コンテンツページからの情報が含まれる場所が決まります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="fb0f5-164">次の図は、実行時にコンテンツページとレイアウトページがどのように組み合わされ、完成した web ページが生成されるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="fb0f5-165">ブラウザーはコンテンツページを要求します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-165">The browser requests a content page.</span></span> <span data-ttu-id="fb0f5-166">コンテンツページには、ページの構造に使用するレイアウトページを指定するコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="fb0f5-167">[レイアウト] ページでは、`RenderBody` メソッドが呼び出される位置にコンテンツが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="fb0f5-168">また、前のセクションで行ったように、`RenderPage` メソッドを呼び出すことによって、コンテンツブロックをレイアウトページに挿入することもできます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="fb0f5-169">Web ページが完成すると、ブラウザーに送信されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-169">When the web page is complete, it's sent to the browser.</span></span>

![RenderBody メソッドの呼び出しを含むページを実行した結果として得られるブラウザー内のページを示すスクリーンショット。](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="fb0f5-171">次の手順では、レイアウトページを作成し、そのページにコンテンツページをリンクする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="fb0f5-172">Web サイトの*共有*フォルダーに、 *\_Layout1*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="fb0f5-173">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="fb0f5-174">コンテンツブロックを挿入するには、レイアウトページで `RenderPage` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="fb0f5-175">レイアウトページには、`RenderBody` メソッドの呼び出しを1つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="fb0f5-176">*共有*フォルダーで、 *\_.header2*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="fb0f5-177">ルートフォルダーで、新しいフォルダーを作成し、その名前を「 *Styles*」にします。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="fb0f5-178">[*スタイル*] フォルダーで、「 *.css* 」という名前のファイルを作成し、次のスタイル定義を追加します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="fb0f5-179">ここでは、スタイルシートをレイアウトページで使用する方法についてのみ説明します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="fb0f5-180">必要に応じて、これらの要素に対して独自のスタイルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="fb0f5-181">ルートフォルダーに*Content1*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="fb0f5-182">これは、レイアウトページを使用するページです。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="fb0f5-183">ページの上部にあるコードブロックは、このコンテンツの書式設定に使用するレイアウトページを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="fb0f5-184">ブラウザーで*Content1*を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="fb0f5-185">レンダリング\_されたページは、 *Layout1*で定義されている形式とスタイルシートと、 *Content1*で定義されているテキスト (コンテンツ) を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[画像]](3-creating-a-consistent-look/_static/image4.png)

    <span data-ttu-id="fb0f5-187">手順 6. を繰り返して、同じレイアウトページを共有できる追加のコンテンツページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fb0f5-188">フォルダー内のすべてのコンテンツページに対して同じレイアウトページを自動的に使用できるようにサイトを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="fb0f5-189">詳細については、「 [ASP.NET Web ページのサイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="fb0f5-190">複数のコンテンツセクションを含むレイアウトページのデザイン</span><span class="sxs-lookup"><span data-stu-id="fb0f5-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="fb0f5-191">コンテンツページには複数のセクションを含めることができます。これは、置き換え可能なコンテンツを持つ複数の領域を持つレイアウトを使用する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="fb0f5-192">[コンテンツ] ページで、各セクションに一意の名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="fb0f5-193">(既定のセクションは無名のままです)。[レイアウト] ページで、`RenderBody` メソッドを追加して、名前のない (既定の) セクションを表示する場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="fb0f5-194">次に、名前付きセクションを個別に表示するために、個別の `RenderSection` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="fb0f5-195">次の図は、ASP.NET が複数のセクションに分割されたコンテンツを処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="fb0f5-196">各名前付きセクションは、コンテンツページのセクションブロックに含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="fb0f5-197">(例では `Header` と `List` という名前です)。フレームワークによって、`RenderSection` メソッドが呼び出される位置のレイアウトページにコンテンツセクションが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="fb0f5-198">前に見たように、名前のない (既定の) セクションが、`RenderBody` メソッドが呼び出される位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![RenderSection メソッドが参照セクションを現在のページに挿入する方法を示す概念図。](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="fb0f5-200">この手順では、複数のコンテンツセクションを含むコンテンツページを作成する方法と、複数のコンテンツセクションをサポートするレイアウトページを使用してコンテンツセクションを表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="fb0f5-201">*共有*フォルダーに、 *\_Layout2*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="fb0f5-202">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="fb0f5-203">ヘッダーセクションとリストセクションの両方を表示するには、`RenderSection` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="fb0f5-204">ルートフォルダーに*Content2*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="fb0f5-205">このコンテンツページには、ページの上部にコードブロックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="fb0f5-206">各名前付きセクションは、セクションブロックに含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="fb0f5-207">ページの残りの部分には、既定の (名前のない) コンテンツセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="fb0f5-208">ブラウザーで*Content2*を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-208">Run *Content2.cshtml* in a browser.</span></span>

    ![RenderSection メソッドの呼び出しを含むページを実行した結果として得られるブラウザー内のページを示すスクリーンショット。](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a><span data-ttu-id="fb0f5-210">コンテンツセクションをオプションにする</span><span class="sxs-lookup"><span data-stu-id="fb0f5-210">Making Content Sections Optional</span></span>

<span data-ttu-id="fb0f5-211">通常、コンテンツページで作成するセクションは、[レイアウト] ページで定義されているセクションと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="fb0f5-212">次のいずれかが発生すると、エラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="fb0f5-213">コンテンツページには、レイアウトページに対応するセクションがないセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="fb0f5-214">レイアウトページには、コンテンツがないセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="fb0f5-215">レイアウトページには、同じセクションを複数回表示しようとするメソッド呼び出しが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="fb0f5-216">ただし、レイアウトページでセクションをオプションとして宣言することで、名前付きセクションのこの動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="fb0f5-217">これにより、レイアウトページを共有できるコンテンツページを複数定義できますが、特定のセクションのコンテンツが含まれていない場合もあります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="fb0f5-218">*Content2*を開き、次のセクションを削除します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="fb0f5-219">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="fb0f5-220">コンテンツページでは、レイアウトページで定義されているセクション (ヘッダーセクション) のコンテンツが提供されないため、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![RenderSection メソッドを呼び出すページを実行しても、対応するセクションが指定されていない場合に発生するエラーを示すスクリーンショット。](3-creating-a-consistent-look/_static/image7.png)
3. <span data-ttu-id="fb0f5-222">*共有*フォルダーで、 *\_Layout2*ページを開き、次の行を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="fb0f5-223">を、以下のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="fb0f5-224">別の方法として、前のコード行を次のコードブロックに置き換えることもできます。これにより、同じ結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="fb0f5-225">ブラウザーで*Content2*ページをもう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="fb0f5-226">(ブラウザーでこのページを開いたままにしている場合は、更新するだけで済みます)。今回は、ヘッダーがない場合でも、ページにエラーが表示されません。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="fb0f5-227">レイアウトページにデータを渡す</span><span class="sxs-lookup"><span data-stu-id="fb0f5-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="fb0f5-228">コンテンツページで、レイアウトページで参照する必要があるデータが定義されている場合があります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="fb0f5-229">その場合は、コンテンツページからレイアウトページにデータを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="fb0f5-230">たとえば、ユーザーのログインステータスを表示したり、ユーザー入力に基づいてコンテンツ領域の表示と非表示を切り替えたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="fb0f5-231">コンテンツページからレイアウトページにデータを渡すには、コンテンツページの [`PageData`] プロパティに値を入力します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="fb0f5-232">`PageData` プロパティは、ページ間で渡されるデータを格納する名前と値のペアのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="fb0f5-233">[レイアウト] ページでは、`PageData` プロパティから値を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="fb0f5-234">もう1つの図を次に示します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-234">Here's another diagram.</span></span> <span data-ttu-id="fb0f5-235">ここでは、ASP.NET が `PageData` プロパティを使用して、コンテンツページからレイアウトページに値を渡す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="fb0f5-236">ASP.NET が web ページの構築を開始すると、`PageData` コレクションが作成されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="fb0f5-237">[コンテンツ] ページで、`PageData` コレクションにデータを格納するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="fb0f5-238">`PageData` コレクション内の値は、コンテンツページの他のセクション、または追加のコンテンツブロックによってアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![コンテンツページで PageData 辞書にデータを入力し、その情報をレイアウトページに渡す方法を示す概念図。](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="fb0f5-240">次の手順では、コンテンツページからレイアウトページにデータを渡す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="fb0f5-241">ページを実行すると、レイアウトページで定義されている一覧をユーザーが非表示にしたり表示したりできるボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="fb0f5-242">ユーザーがボタンをクリックすると、`PageData` プロパティに true/false (ブール値) 値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="fb0f5-243">レイアウトページはその値を読み取り、false の場合はリストを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="fb0f5-244">この値は、**リストの非表示** ボタンと **リストの表示** ボタンのどちらを表示するかを決定するために、コンテンツ ページでも使用されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[画像]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="fb0f5-246">ルートフォルダーに*Content3*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="fb0f5-247">このコードでは、`PageData` プロパティ&#8212;に2つのデータを格納し、web ページのタイトルと true または false を指定して、リストを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="fb0f5-248">ASP.NET を使用すると、コードブロックを使用して条件付きでページに HTML マークアップを配置できます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="fb0f5-249">たとえば、ページの本文の `if/else` ブロックは、`PageData["ShowList"]` が true に設定されているかどうかに応じてどのフォームを表示するかを決定します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="fb0f5-250">*共有*フォルダーで、 *\_Layout3*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="fb0f5-251">レイアウトページには、`PageData` プロパティからタイトル値を取得する `<title>` 要素の式が含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="fb0f5-252">また、`PageData` プロパティの `ShowList` 値を使用して、リストコンテンツブロックを表示するかどうかを決定します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="fb0f5-253">*共有*フォルダーで、 *\_List. cshtml*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="fb0f5-254">ブラウザーで*Content3*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="fb0f5-255">ページが表示され、ページの左側にリストが表示され、下部に **[リストの非表示]** ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![リストを含むページと、' Hide List ' というボタンを示すスクリーンショット。](3-creating-a-consistent-look/_static/image10.png)
5. <span data-ttu-id="fb0f5-257">**[一覧の非表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-257">Click **Hide List**.</span></span> <span data-ttu-id="fb0f5-258">一覧が表示されなくなり、ボタンが **[一覧の表示]** に変わります。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-258">The list disappears and the button changes to **Show List**.</span></span>

    ![リストを含まないページと、' Show List ' というボタンを示すスクリーンショット。](3-creating-a-consistent-look/_static/image11.png)
6. <span data-ttu-id="fb0f5-260">**[一覧の表示]** ボタンをクリックすると、一覧が再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb0f5-261">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="fb0f5-261">Additional Resources</span></span>

[<span data-ttu-id="fb0f5-262">ASP.NET Web ページのサイト全体の動作のカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="fb0f5-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
