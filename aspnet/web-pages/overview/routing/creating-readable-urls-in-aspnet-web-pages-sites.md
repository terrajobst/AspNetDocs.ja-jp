---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET Web ページ (Razor) サイトで読み取り可能な Url を作成する |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトでのルーティングについて説明します。また、これにより、SEO により読みやすく、より優れた Url を使用する方法についても説明します。 作業内容
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509908"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="f8ffc-104">ASP.NET Web ページ (Razor) サイトでの読み取り可能な Url の作成</span><span class="sxs-lookup"><span data-stu-id="f8ffc-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="f8ffc-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f8ffc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f8ffc-106">この記事では、ASP.NET Web ページ (Razor) web サイトでのルーティングについて説明します。また、これにより、SEO により読みやすく、より優れた Url を使用する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="f8ffc-107">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f8ffc-108">ASP.NET がルーティングを使用して、より読みやすく検索可能な Url を使用できるようにする方法。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f8ffc-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="f8ffc-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f8ffc-110">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="f8ffc-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="f8ffc-111">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="f8ffc-112">ルーティングについて</span><span class="sxs-lookup"><span data-stu-id="f8ffc-112">About Routing</span></span>

<span data-ttu-id="f8ffc-113">サイト内のページの Url は、サイトの動作に影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="f8ffc-114">&quot; &quot;やすい URL を使用すると、簡単にサイトを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="f8ffc-115">また、サイトの検索エンジン最適化 (SEO) にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="f8ffc-116">ASP.NET websites には、フレンドリな Url を自動的に使用する機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="f8ffc-117">ASP.NET を使用すると、サーバー上のファイルを指すのではなく、ユーザーの操作を記述する意味のある Url を作成できます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="f8ffc-118">架空のブログについては、次の Url を検討してください。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="f8ffc-119">これらの Url を次の Url と比較します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="f8ffc-120">最初のペアで*は、blog ページを*使用してブログが表示されていることをユーザーが認識する必要があり、その後、適切なカテゴリまたは日付範囲を取得するクエリ文字列を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="f8ffc-121">2番目の例のセットは、理解しやすく作成するのがはるかに簡単です。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="f8ffc-122">最初の例の Url も、特定のファイル (*blog*) を直接指しています。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="f8ffc-123">何らかの理由でブログがサーバー上の別のフォルダーに移動された場合、または別のページを使用するようにブログが書き換えられた場合、リンクは間違っています。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="f8ffc-124">2番目の Url のセットは特定のページを指していないので、ブログの実装や場所が変更された場合でも、Url は引き続き有効になります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="f8ffc-125">ASP.NET Web ページでは、ASP.NET が*ルーティング*を使用するため、上記の例のようなわかりやすい url を作成できます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="f8ffc-126">ルーティングにより、URL から要求を満たすことができるページ (またはページ) への論理マッピングが作成されます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="f8ffc-127">マッピングは論理的なものであり (物理的ではなく、特定のファイルに対するものではありません)、ルーティングによって、サイトの Url を定義する方法が非常に柔軟になります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="f8ffc-128">ルーティングのしくみ</span><span class="sxs-lookup"><span data-stu-id="f8ffc-128">How Routing Works</span></span>

<span data-ttu-id="f8ffc-129">ASP.NET が要求を処理するときに、URL を読み取り、その要求をルーティングする方法を決定します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="f8ffc-130">ASP.NET は、URL の個々のセグメントを、左から右に、ディスク上のファイルに一致させようとします。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="f8ffc-131">一致するものがある場合、URL に残っているものは*パス情報*としてページに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="f8ffc-132">この URL を使用してだれかが要求を行うとします。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="f8ffc-133">検索は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-133">The search goes like this:</span></span>

1. <span data-ttu-id="f8ffc-134">*/A/b/c.cshtml*のパスと名前を持つファイルはありますか。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="f8ffc-135">その場合は、そのページを実行し、情報を渡しません。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="f8ffc-136">それ以外の場合:</span><span class="sxs-lookup"><span data-stu-id="f8ffc-136">Otherwise ...</span></span>
2. <span data-ttu-id="f8ffc-137">*/A/b.cshtml*のパスと名前を持つファイルはありますか。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="f8ffc-138">その場合は、そのページを実行し、`c` の値を渡します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="f8ffc-139">それ以外の場合...</span><span class="sxs-lookup"><span data-stu-id="f8ffc-139">Otherwise …</span></span>
3. <span data-ttu-id="f8ffc-140">*/A.cshtml*のパスと名前を持つファイルはありますか。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="f8ffc-141">その場合は、そのページを実行し、`b/c` の値を渡します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="f8ffc-142">指定されたフォルダー内のファイル*の完全*一致が検索で見つからなかった場合、ASP.NET は引き続きこれらのファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="f8ffc-143">*/a/b/c/default.cshtml* (パス情報なし)。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="f8ffc-144">*/a/b/c/index.cshtml* (パス情報なし)。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="f8ffc-145">明確にするために、特定のページ (つまり、ファイル名拡張子が*cshtml*の要求) の要求は、期待したとおりに動作します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="f8ffc-146">`http://www.contoso.com/a/b.cshtml` のような要求では、ページ*b.* を正常に実行します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="f8ffc-147">ページ内では、ページの `UrlData` プロパティ (ディクショナリ) を使用してパス情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="f8ffc-148">*Viewcustomers. cshtml*という名前のファイルがあり、サイトが次の要求を取得しているとします。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="f8ffc-149">上記のルールで説明したように、要求はページに送られます。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="f8ffc-150">ページ内で、次のようなコードを使用して、パス情報を取得して表示できます (この場合は、1000&quot;&quot;値)。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="f8ffc-151">ルーティングには完全なファイル名が含まれないため、同じ名前でファイル名拡張子が異なるページ ( *MyPage*や*MyPage*など) がある場合は、あいまいになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="f8ffc-152">ルーティングに関する問題を回避するために、サイト内のページの名前が拡張子だけで異なることを確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f8ffc-153">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="f8ffc-153">Additional Resources</span></span>

<span data-ttu-id="f8ffc-154">[WebMatrix-SEO の url、UrlData、および Routing](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="f8ffc-155">Mike Brind によるこのブログエントリでは、ASP.NET Web ページでのルーティングのしくみについてさらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="f8ffc-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
