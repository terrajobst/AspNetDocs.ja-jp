---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET Web ページ (Razor) サイトのトラッキング訪問者情報 (Analytics)Microsoft Docs
author: Rick-Anderson
description: Web サイトのアクセスが完了したら、web サイトのトラフィックを分析することができます。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421456"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="62158-103">ASP.NET Web ページ (Razor) サイトのトラッキング訪問者情報 (Analytics)</span><span class="sxs-lookup"><span data-stu-id="62158-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="62158-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="62158-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="62158-105">この記事では、ヘルパーを使用して、ASP.NET Web ページ (Razor) web サイトのページに web サイトの分析を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="62158-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="62158-106">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="62158-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="62158-107">Web サイトのトラフィックに関する情報を分析プロバイダーに送信する方法。</span><span class="sxs-lookup"><span data-stu-id="62158-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="62158-108">この記事で紹介する ASP.NET プログラミング機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="62158-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="62158-109">`Analytics` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="62158-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="62158-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="62158-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="62158-111">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="62158-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="62158-112">ASP.NET Web ヘルパーライブラリ (NuGet パッケージ)</span><span class="sxs-lookup"><span data-stu-id="62158-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="62158-113">Analytics は、ユーザーがサイトをどのように使用しているかを理解できるように、web サイトのトラフィックを測定するテクノロジの一般的な用語です。</span><span class="sxs-lookup"><span data-stu-id="62158-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="62158-114">Google、Yahoo、StatCounter などのサービスを含む多くの分析サービスを利用できます。</span><span class="sxs-lookup"><span data-stu-id="62158-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="62158-115">Analytics の機能として、分析プロバイダーを使用してアカウントにサインアップし、追跡するサイトを登録するという方法があります。プロバイダーは、お客様のアカウントの ID または追跡コードを含む JavaScript コードのスニペットを送信します。</span><span class="sxs-lookup"><span data-stu-id="62158-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="62158-116">JavaScript スニペットは、追跡するサイトの web ページに追加します。(通常、分析スニペットは、サイト内のすべてのページに表示されるフッターまたはレイアウトページやその他の HTML マークアップに追加します)。これらの JavaScript スニペットの1つが含まれているページをユーザーが要求すると、スニペットは現在のページに関する情報を分析プロバイダーに送信し、そのページに関するさまざまな詳細情報を記録します。</span><span class="sxs-lookup"><span data-stu-id="62158-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="62158-117">サイトの統計情報を確認するには、analytics プロバイダーの web サイトにログインします。</span><span class="sxs-lookup"><span data-stu-id="62158-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="62158-118">次のように、サイトに関するすべての種類のレポートを表示できます。</span><span class="sxs-lookup"><span data-stu-id="62158-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="62158-119">個々のページのページビューの数。</span><span class="sxs-lookup"><span data-stu-id="62158-119">The number of page views for individual pages.</span></span> <span data-ttu-id="62158-120">これにより、サイトにアクセスしているユーザーの数と、最も人気のあるサイトのページがわかります。</span><span class="sxs-lookup"><span data-stu-id="62158-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="62158-121">特定のページに対して、どのくらいの時間がかかっているか。</span><span class="sxs-lookup"><span data-stu-id="62158-121">How long people spend on specific pages.</span></span> <span data-ttu-id="62158-122">これにより、ホームページがユーザーの関心を持っているかどうかがわかります。</span><span class="sxs-lookup"><span data-stu-id="62158-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="62158-123">サイトにアクセスする前に、どのサイトを使用していたか。</span><span class="sxs-lookup"><span data-stu-id="62158-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="62158-124">これにより、トラフィックがリンクから送信されるか、検索から送信されるかなどを把握できます。</span><span class="sxs-lookup"><span data-stu-id="62158-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="62158-125">ユーザーがサイトにアクセスするときと、その期間の長さ。</span><span class="sxs-lookup"><span data-stu-id="62158-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="62158-126">訪問者の国を示します。</span><span class="sxs-lookup"><span data-stu-id="62158-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="62158-127">訪問者が使用しているブラウザーとオペレーティングシステム</span><span class="sxs-lookup"><span data-stu-id="62158-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="62158-129">ヘルパーを使用してページに Analytics を追加する</span><span class="sxs-lookup"><span data-stu-id="62158-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="62158-130">ASP.NET Web ページには、分析に使用される JavaScript スニペットを簡単に管理できるようにする分析ヘルパー (`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`、および `Analytics.GetStatCounterHtml`) がいくつか含まれています。</span><span class="sxs-lookup"><span data-stu-id="62158-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="62158-131">JavaScript コードを配置する方法と場所を確認するのではなく、ヘルパーをページに追加するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="62158-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="62158-132">指定する必要がある情報は、アカウント名、ID、または追跡コードだけです。</span><span class="sxs-lookup"><span data-stu-id="62158-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="62158-133">(StatCounter の場合は、いくつかの追加の値も指定する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="62158-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="62158-134">この手順では、`GetGoogleHtml` ヘルパーを使用するレイアウトページを作成します。</span><span class="sxs-lookup"><span data-stu-id="62158-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="62158-135">他のいずれかの分析プロバイダーを持つアカウントが既にある場合は、代わりにそのアカウントを使用し、必要に応じて微調整を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="62158-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="62158-136">Analytics アカウントを作成するときに、追跡対象のサイトの URL を登録します。</span><span class="sxs-lookup"><span data-stu-id="62158-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="62158-137">ローカルコンピューター上のすべてをテストする場合は、実際のトラフィック (唯一のトラフィック) を追跡することはありません。そのため、サイトの統計情報を記録して表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="62158-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="62158-138">ただし、この手順では、分析ヘルパーをページに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="62158-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="62158-139">サイトを発行すると、ライブサイトから分析プロバイダーに情報が送信されます。</span><span class="sxs-lookup"><span data-stu-id="62158-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="62158-140">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。</span><span class="sxs-lookup"><span data-stu-id="62158-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="62158-141">Google アナリティクスでアカウントを作成し、アカウント名を記録します。</span><span class="sxs-lookup"><span data-stu-id="62158-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="62158-142">*Analytics*という名前のレイアウトページを作成し、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="62158-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="62158-143">`Analytics` ヘルパーへの呼び出しは、(`</body>` タグの前に) web ページの本文に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="62158-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="62158-144">そうしないと、ブラウザーでスクリプトが実行されません。</span><span class="sxs-lookup"><span data-stu-id="62158-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="62158-145">別の分析プロバイダーを使用している場合は、代わりに次のいずれかのヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="62158-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="62158-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="62158-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="62158-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="62158-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="62158-148">`myaccount` は、手順 1. で作成したアカウントの名前、ID、または追跡コードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="62158-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="62158-149">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="62158-149">Run the page in the browser.</span></span> <span data-ttu-id="62158-150">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="62158-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="62158-151">ブラウザーでページソースを表示します。</span><span class="sxs-lookup"><span data-stu-id="62158-151">In the browser, view the page source.</span></span> <span data-ttu-id="62158-152">表示される分析コードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="62158-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="62158-153">Google アナリティクスサイトにログオンし、サイトの統計情報を確認します。</span><span class="sxs-lookup"><span data-stu-id="62158-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="62158-154">ライブサイトでページを実行している場合は、アクセスをページに記録するエントリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="62158-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="62158-155">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="62158-155">Additional Resources</span></span>

- [<span data-ttu-id="62158-156">Google アナリティクスサイト</span><span class="sxs-lookup"><span data-stu-id="62158-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="62158-157">Yahoo! Web Analytics サイト</span><span class="sxs-lookup"><span data-stu-id="62158-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="62158-158">StatCounter サイト</span><span class="sxs-lookup"><span data-stu-id="62158-158">StatCounter site</span></span>](http://statcounter.com/)
