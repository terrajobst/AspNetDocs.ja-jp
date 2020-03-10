---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: はじめに | Microsoft Docs
author: Rick-Anderson
description: WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。 Visual Studio または Visual Studio Code を使用します。 このガイドの内容...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: bb863f8605e6f8faca3b285607b63a3e88e83012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440242"
---
# <a name="getting-started"></a><span data-ttu-id="7a034-105">作業の開始</span><span class="sxs-lookup"><span data-stu-id="7a034-105">Getting Started</span></span>

<span data-ttu-id="7a034-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7a034-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="7a034-107">WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="7a034-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="7a034-108">[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="7a034-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="7a034-109">このガイダンスとアプリケーションでは、動的 web サイトを作成するための軽量フレームワークである ASP.NET Web ページ (バージョン2以降) と Razor 構文の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="7a034-110">また、ページやサイトを作成するためのツールである WebMatrix も導入されています。</span><span class="sxs-lookup"><span data-stu-id="7a034-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="7a034-111">**Level**: ASP.NET Web ページが新しくなります。</span><span class="sxs-lookup"><span data-stu-id="7a034-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="7a034-112">**想定**されるスキルは、HTML、基本的なカスケードスタイルシート (CSS) です。</span><span class="sxs-lookup"><span data-stu-id="7a034-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="7a034-113">このセットの最初のチュートリアルで学習する内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7a034-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="7a034-114">ASP.NET Web ページテクノロジとは何ですか。</span><span class="sxs-lookup"><span data-stu-id="7a034-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="7a034-115">WebMatrix とは</span><span class="sxs-lookup"><span data-stu-id="7a034-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="7a034-116">すべてをインストールする方法。</span><span class="sxs-lookup"><span data-stu-id="7a034-116">How to install everything.</span></span>
> - <span data-ttu-id="7a034-117">WebMatrix を使用して web サイトを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="7a034-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="7a034-118">説明する機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="7a034-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="7a034-119">Microsoft Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="7a034-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="7a034-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7a034-120">WebMatrix.</span></span>
> - <span data-ttu-id="7a034-121">*cshtml*ページ</span><span class="sxs-lookup"><span data-stu-id="7a034-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="7a034-122">Mike Pope はこのチュートリアルを最初に記述しました。</span><span class="sxs-lookup"><span data-stu-id="7a034-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="7a034-123">Tom FitzMacken は Microsoft WebMatrix 3 用に更新されました。</span><span class="sxs-lookup"><span data-stu-id="7a034-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7a034-124">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7a034-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7a034-125">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="7a034-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="7a034-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7a034-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="7a034-127">何を知る必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="7a034-127">What Should You Know?</span></span>

<span data-ttu-id="7a034-128">次のことを理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="7a034-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="7a034-129">**HTML**。</span><span class="sxs-lookup"><span data-stu-id="7a034-129">**HTML**.</span></span> <span data-ttu-id="7a034-130">詳細な専門知識は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="7a034-130">No in-depth expertise is required.</span></span> <span data-ttu-id="7a034-131">HTML については説明しませんが、複雑なものは使用しません。</span><span class="sxs-lookup"><span data-stu-id="7a034-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="7a034-132">HTML チュートリアルへのリンクが用意されているので、それが役に立つと思います。</span><span class="sxs-lookup"><span data-stu-id="7a034-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="7a034-133">**カスケードスタイルシート (CSS)** 。</span><span class="sxs-lookup"><span data-stu-id="7a034-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="7a034-134">HTML の場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="7a034-134">Same as with HTML.</span></span>
- <span data-ttu-id="7a034-135">**基本的なデータベースアイデア**。</span><span class="sxs-lookup"><span data-stu-id="7a034-135">**Basic database ideas**.</span></span> <span data-ttu-id="7a034-136">データにスプレッドシートを使用し、データの並べ替えとフィルター処理を行った経験があれば、このチュートリアルセットでは一般的に想定しています。</span><span class="sxs-lookup"><span data-stu-id="7a034-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="7a034-137">また、基本的なプログラミングの学習に関心があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="7a034-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="7a034-138">ASP.NET Web ページは、C# と呼ばれるプログラミング言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="7a034-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="7a034-139">プログラミングの背景を必要とすることはありません。</span><span class="sxs-lookup"><span data-stu-id="7a034-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="7a034-140">以前に web ページで JavaScript を記述したことがある場合は、背景が十分にあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="7a034-141">プログラミングに習熟している場合は、このチュートリアルの初期段階では、新しいプログラマが速度を向上させるため、このチュートリアルの設定が遅くなる可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="7a034-142">ただし、最初のいくつかのチュートリアルでは説明しませんが、基本的なプログラミングについては説明しません。</span><span class="sxs-lookup"><span data-stu-id="7a034-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="7a034-143">必要なものは何ですか?</span><span class="sxs-lookup"><span data-stu-id="7a034-143">What Do You Need?</span></span>

<span data-ttu-id="7a034-144">次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="7a034-144">Here's what you'll need:</span></span>

- <span data-ttu-id="7a034-145">Windows 8、Windows 7、Windows Server 2008、または Windows Server 2012 を実行しているコンピューター。</span><span class="sxs-lookup"><span data-stu-id="7a034-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="7a034-146">ライブインターネット接続。</span><span class="sxs-lookup"><span data-stu-id="7a034-146">A live internet connection.</span></span>
- <span data-ttu-id="7a034-147">管理者特権 (インストールプロセスに必要)。</span><span class="sxs-lookup"><span data-stu-id="7a034-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="7a034-148">ASP.NET Web ページとは</span><span class="sxs-lookup"><span data-stu-id="7a034-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="7a034-149">ASP.NET Web ページは、動的な Web ページを作成するために使用できるフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="7a034-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="7a034-150">単純な HTML web ページは静的です。その内容は、ページ内の固定 HTML マークアップによって決定されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="7a034-151">ASP.NET Web ページで作成したような動的ページでは、コードを使用して、その場でページコンテンツを作成できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="7a034-152">動的ページを使用すると、あらゆる種類の操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="7a034-153">フォームを使用してユーザーに入力を要求してから、ページに表示される内容や外観を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="7a034-154">ユーザーから情報を取得してデータベースに保存し、後で一覧表示することができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="7a034-155">サイトから電子メールを送信できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-155">You can send email from your site.</span></span> <span data-ttu-id="7a034-156">Web 上の他のサービス (たとえば、マッピングサービス) と対話し、それらのソースの情報を統合するページを生成することができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="7a034-157">WebMatrix とは</span><span class="sxs-lookup"><span data-stu-id="7a034-157">What is WebMatrix?</span></span>

<span data-ttu-id="7a034-158">WebMatrix は、web ページエディター、データベースユーティリティ、ページをテストするための web サーバー、および web サイトをインターネットに公開する機能を統合するツールです。</span><span class="sxs-lookup"><span data-stu-id="7a034-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="7a034-159">WebMatrix は無料で、簡単にインストールでき、簡単に使用できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="7a034-160">(これは、単純な HTML ページだけでなく、PHP などの他のテクノロジにも使用できます)。</span><span class="sxs-lookup"><span data-stu-id="7a034-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="7a034-161">実際には、WebMatrix を使用して ASP.NET Web ページを操作する*必要はあり*ません。</span><span class="sxs-lookup"><span data-stu-id="7a034-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="7a034-162">たとえば、アクセス権のある web サーバーを使用して、テキストエディターやテストページを使用してページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="7a034-163">ただし、WebMatrix を使用すると非常に簡単になります。そのため、これらのチュートリアルでは、全体を通じて WebMatrix を使用します。</span><span class="sxs-lookup"><span data-stu-id="7a034-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="7a034-164">これらのチュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="7a034-164">About These Tutorials</span></span>

<span data-ttu-id="7a034-165">このチュートリアルセットでは、ASP.NET Web ページの使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="7a034-166">この入門用チュートリアルでは、合計9つのチュートリアルがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="7a034-167">これは、初心者向けの web サイトを作成するために ASP.NET Web ページ初心者からの一連のチュートリアルの一部です。</span><span class="sxs-lookup"><span data-stu-id="7a034-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="7a034-168">この最初のチュートリアルでは、ASP.NET Web ページを操作する方法の基本を示します。</span><span class="sxs-lookup"><span data-stu-id="7a034-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="7a034-169">完了したら、このチュートリアルの終了位置を確認し、Web ページをより詳細に調べるための追加のチュートリアルセットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="7a034-170">詳細については、簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="7a034-171">また、このチュートリアルでは、理解しやすい方法を常に選択します。</span><span class="sxs-lookup"><span data-stu-id="7a034-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="7a034-172">後のチュートリアルでは、より詳細な説明を設定し、より効率的で柔軟なアプローチを示します (さらに楽しい)。</span><span class="sxs-lookup"><span data-stu-id="7a034-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="7a034-173">ただし、これらのチュートリアルでは、まず基本を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a034-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="7a034-174">先ほど開始したチュートリアルでは、次の ASP.NET Web ページの機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="7a034-175">すべてのインストールについて説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="7a034-176">(これは、お読みのチュートリアルに含まれています)。</span><span class="sxs-lookup"><span data-stu-id="7a034-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="7a034-177">ASP.NET Web ページプログラミングの基本。</span><span class="sxs-lookup"><span data-stu-id="7a034-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="7a034-178">データベースを作成する。</span><span class="sxs-lookup"><span data-stu-id="7a034-178">Creating a database.</span></span>
- <span data-ttu-id="7a034-179">ユーザー入力フォームの作成と処理。</span><span class="sxs-lookup"><span data-stu-id="7a034-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="7a034-180">データベース内のデータの追加、更新、および削除。</span><span class="sxs-lookup"><span data-stu-id="7a034-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="7a034-181">何を作成しますか?</span><span class="sxs-lookup"><span data-stu-id="7a034-181">What Will You Create?</span></span>

<span data-ttu-id="7a034-182">このチュートリアルでは、次のチュートリアルを設定し、必要な映画を一覧表示できる web サイトを中心にしています。</span><span class="sxs-lookup"><span data-stu-id="7a034-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="7a034-183">映画を入力して編集し、一覧表示することができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="7a034-184">このチュートリアルセットで作成するページのいくつかを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7a034-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="7a034-185">最初の例では、作成するムービーリストページを示しています。</span><span class="sxs-lookup"><span data-stu-id="7a034-185">The first one shows the movie listing page that you'll create:</span></span>

![ムービーの一覧を表示しているムービーアプリ](getting-started/_static/image1.png)

<span data-ttu-id="7a034-187">次のページで、サイトに新しい映画情報を追加できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-187">And here's the page that lets you add new movie information to your site:</span></span>

![[ムービーの追加] ページを表示したムービーアプリが完成しました](getting-started/_static/image2.png)

<span data-ttu-id="7a034-189">以降のチュートリアルでは、このセットにビルドを設定し、画像のアップロード、個人のログイン、電子メールの送信、ソーシャルメディアとの統合などの機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="7a034-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="7a034-190">このアプリが Azure で実行されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="7a034-190">See this App Running on Azure</span></span>

<span data-ttu-id="7a034-191">完成したサイトがライブ web アプリとして実行されていることを確認しますか?</span><span class="sxs-lookup"><span data-stu-id="7a034-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="7a034-192">次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="7a034-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="7a034-193">このソリューションを Azure にデプロイするには、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="7a034-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="7a034-194">まだアカウントを持っていない場合は、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="7a034-195">[無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="7a034-196">[Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="7a034-197">すべてをインストールする</span><span class="sxs-lookup"><span data-stu-id="7a034-197">Installing Everything</span></span>

<span data-ttu-id="7a034-198">Microsoft の Web Platform Installer を使用して、すべてをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="7a034-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="7a034-199">実際には、インストーラーをインストールし、それを使用して他のすべてをインストールします。</span><span class="sxs-lookup"><span data-stu-id="7a034-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="7a034-200">Web ページを使用するには、Windows XP SP3 以降、または Windows Server 2008 以降がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a034-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="7a034-201">ASP.NET web サイトの [ [Web ページ] ページ](../../../index.md)で、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET Web サイトを表示 &quot;WebMatrix&quot; ボタンをインストールする](getting-started/_static/image3.png)

<span data-ttu-id="7a034-203">WebMatrix をインストールする前に、ライセンス条項およびプライバシーに関する声明に同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="7a034-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![条項に同意してインストールを開始する](getting-started/_static/image4.png)

<span data-ttu-id="7a034-205">**[実行]** をクリックしてインストールを開始します。</span><span class="sxs-lookup"><span data-stu-id="7a034-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="7a034-206">(インストーラーを保存する場合は、 **[保存]** をクリックし、保存したフォルダーからインストーラーを実行します)。</span><span class="sxs-lookup"><span data-stu-id="7a034-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="7a034-207">Web Platform Installer が表示され、WebMatrix をインストールできるようになります。</span><span class="sxs-lookup"><span data-stu-id="7a034-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="7a034-208">**[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="7a034-209">インストールプロセスでは、コンピューターにインストールする必要があることが確認され、プロセスが開始されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="7a034-210">インストールが必要な内容によっては、処理に数分から数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="7a034-211">[**同意**する] を選択して、ライセンス条項に同意します。</span><span class="sxs-lookup"><span data-stu-id="7a034-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="7a034-212">Hello, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="7a034-212">Hello, WebMatrix</span></span>

<span data-ttu-id="7a034-213">完了すると、インストールプロセスによって WebMatrix が自動的に起動されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="7a034-214">そうでない場合は、Windows の **[スタート]** メニューから**Microsoft WebMatrix**を起動します。</span><span class="sxs-lookup"><span data-stu-id="7a034-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="7a034-215">WebMatrix を初めて起動すると、Microsoft アカウントで Microsoft Azure にサインインする機会が与えられます。</span><span class="sxs-lookup"><span data-stu-id="7a034-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="7a034-216">サインインすると、Azure を通じて10個の無料 web アプリを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="7a034-217">これらの無料の web アプリは、アプリをテストするための便利な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="7a034-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="7a034-218">まだ Azure アカウントを持っていないが、MSDN サブスクリプションをお持ちの場合は、 [msdn サブスクリプションの特典を有効](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にすることができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="7a034-219">それ以外の場合は、無料試用版アカウントを数分で作成できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7a034-220">詳細については、「[Azure の無料試用版サイト](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="7a034-221">このチュートリアルを続行するには、すぐにサインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="7a034-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="7a034-222">サインインしていない場合でも、後でサインインすることができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="7a034-223">このチュートリアルシリーズの最後の[トピック](publishing.md)では、web サイトを Azure にデプロイする方法について説明します。そのため、このトピックを完了するにはサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a034-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="7a034-224">この時点で、Microsoft アカウントを使用してサインインするか、右下隅にある [いいえ]**を選択し**ます。</span><span class="sxs-lookup"><span data-stu-id="7a034-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![Sign In (Azure: サインイン)](getting-started/_static/image7.png)

<span data-ttu-id="7a034-226">まず、空の web サイトを作成し、ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="7a034-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="7a034-227">このセットの後のチュートリアルでは、組み込みの web サイトテンプレートの1つを使用します。</span><span class="sxs-lookup"><span data-stu-id="7a034-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="7a034-228">開始 ウィンドウで、**新規** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-228">In the start window, click **New**.</span></span>

![WebMatrix の起動画面](getting-started/_static/image8.png)

<span data-ttu-id="7a034-230">テンプレートは、さまざまな種類の web サイトの事前に構築されたファイルとページです。</span><span class="sxs-lookup"><span data-stu-id="7a034-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="7a034-231">既定で使用できるすべてのテンプレートを表示するには、[テンプレートギャラリー] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="7a034-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![テンプレートギャラリーの選択](getting-started/_static/image9.png)

<span data-ttu-id="7a034-233">**[クイックスタート]** ウィンドウで、 **ASP.NET**グループの **[空のサイト]** を選択し、新しいサイトに "web 映画" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="7a034-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![空のサイトテンプレートが選択されている WebMatrix クイックスタートウィンドウ](getting-started/_static/image10.png)

<span data-ttu-id="7a034-235">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-235">Click **Next**.</span></span>

<span data-ttu-id="7a034-236">Microsoft アカウントにサインインしている場合は、Azure にサイトを作成する機会が与えられます。</span><span class="sxs-lookup"><span data-stu-id="7a034-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="7a034-237">サイトの名前に基づいて、 **WebPagesMovies.azurewebsites.net**の既定の名前が推奨されます。ただし、感嘆符は、この名前が Windows Azure で使用できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="7a034-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="7a034-238">わかりやすくするために、 **[スキップ]** を選択して、今すぐ Azure での web サイトの作成をバイパスします。</span><span class="sxs-lookup"><span data-stu-id="7a034-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="7a034-239">このシリーズの後半では、このサイトを Azure に発行します。</span><span class="sxs-lookup"><span data-stu-id="7a034-239">Later in this series, we will publish the site to Azure.</span></span>

![azure サイトの作成](getting-started/_static/image11.png)

<span data-ttu-id="7a034-241">WebMatrix は、サイトを作成して開きます。</span><span class="sxs-lookup"><span data-stu-id="7a034-241">WebMatrix creates and opens the site:</span></span>

![WebMatrix で開かれる新しい Webweb ムービーサイト](getting-started/_static/image12.png)

<span data-ttu-id="7a034-243">上部には、クイックアクセスツールバーとリボンがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="7a034-244">左下には、タスク (**サイト**、**ファイル**、**データベース**、**レポート**) を切り替えるワークスペースセレクターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="7a034-245">右側には、エディターのコンテンツウィンドウとレポートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="7a034-246">下部には、メッセージの通知バーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="7a034-247">WebMatrix とその機能の詳細については、これらのチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="7a034-248">Web ページの作成</span><span class="sxs-lookup"><span data-stu-id="7a034-248">Creating a Web Page</span></span>

<span data-ttu-id="7a034-249">WebMatrix と ASP.NET Web ページについて理解を深めるには、簡単なページを作成します。</span><span class="sxs-lookup"><span data-stu-id="7a034-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="7a034-250">ワークスペースセレクターで、 **[ファイル]** ワークスペースを選択します。</span><span class="sxs-lookup"><span data-stu-id="7a034-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="7a034-251">このワークスペースを使用すると、ファイルとフォルダーを操作できます。</span><span class="sxs-lookup"><span data-stu-id="7a034-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="7a034-252">左側のウィンドウには、サイトのファイル構造が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="7a034-253">リボンが変更され、ファイル関連のタスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix のファイルワークスペース](getting-started/_static/image13.png)

<span data-ttu-id="7a034-255">リボンで、 **[新規]** の下の矢印をクリックし、 **[新しいファイル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![リボンの [新しい&quot; の &quot;] コマンドを使用して新しいファイルを作成する](getting-started/_static/image14.png)

<span data-ttu-id="7a034-257">WebMatrix では、ファイルの種類の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="7a034-258">**[CSHTML]** を選択し、 **[名前]** ボックスに「HelloWorld」と入力します。</span><span class="sxs-lookup"><span data-stu-id="7a034-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="7a034-259">CSHTML ページは ASP.NET Web ページページです。</span><span class="sxs-lookup"><span data-stu-id="7a034-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![HelloWorld という名前の新しい CSHTML ページを作成します。](getting-started/_static/image15.png)

<span data-ttu-id="7a034-261">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-261">Click **OK**.</span></span>

<span data-ttu-id="7a034-262">WebMatrix によってページが作成され、エディターで開かれます。</span><span class="sxs-lookup"><span data-stu-id="7a034-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix エディターの新しい HelloWorld ページ](getting-started/_static/image16.png)

<span data-ttu-id="7a034-264">ご覧のように、このページにはほとんどの通常の HTML マークアップが含まれています。ただし、上部には次のようなブロックがあります。</span><span class="sxs-lookup"><span data-stu-id="7a034-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="7a034-265">これはコードを追加するためのものです。後で説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="7a034-266">ページのさまざまな部分には、要素名、属性、テキスト、および上部にあるブロック &mdash;、すべて異なる色が付いていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="7a034-267">これを*構文の強調表示*と呼びます。これにより、すべてを明確に保つことができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="7a034-268">これは、WebMatrix で web ページを簡単に操作できるようにする機能の1つです。</span><span class="sxs-lookup"><span data-stu-id="7a034-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="7a034-269">次の例のように、`<head>` と `<body>` の要素の内容を追加します。</span><span class="sxs-lookup"><span data-stu-id="7a034-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="7a034-270">(必要に応じて、次のブロックをコピーし、既存のページ全体をこのコードで置き換えることができます)。</span><span class="sxs-lookup"><span data-stu-id="7a034-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="7a034-271">クイックアクセスツールバーまたは **[ファイル]** メニューの **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix クイックアクセスツールバーの [保存] ボタン](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="7a034-273">ページのテスト</span><span class="sxs-lookup"><span data-stu-id="7a034-273">Testing the Page</span></span>

<span data-ttu-id="7a034-274">**[ファイル]** ワークスペースで、 *HelloWorld*ページを右クリックし、 **[ブラウザーで起動]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7a034-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix リボンの [実行] ボタンを使用したページの実行](getting-started/_static/image18.png)

<span data-ttu-id="7a034-276">WebMatrix では、コンピューター上のページをテストするために使用できる、組み込みの web サーバー (IIS Express) を起動します。</span><span class="sxs-lookup"><span data-stu-id="7a034-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="7a034-277">(WebMatrix で IIS Express を使用しない場合は、テストする前に、web サーバーにページを発行する必要があります)。ページが既定のブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![ブラウザーで実行されている Hello World&quot; ページの &quot;](getting-started/_static/image19.png)

<span data-ttu-id="7a034-279">WebMatrix でページをテストすると、ブラウザーの URL は、 *localhost*がローカルサーバーを参照する `http://localhost:33651/HelloWorld.cshtml.` のようになります。つまり、ページは自分のコンピューター上の web サーバーによって処理されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="7a034-280">前述のように、WebMatrix には、ページの起動時に実行される IIS Express という名前の web サーバープログラムが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7a034-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="7a034-281">*Localhost*の後の番号 ( *localhost: 33651*など) は、コンピューター上の*ポート番号*を参照します。</span><span class="sxs-lookup"><span data-stu-id="7a034-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="7a034-282">これは、この特定の web サイトに IIS Express が使用する "チャネル" の番号です。</span><span class="sxs-lookup"><span data-stu-id="7a034-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="7a034-283">ポート番号は、サイトの作成時に 1024 ~ 65536 の範囲でランダムに選択されます。これは、作成するサイトごとに異なります。</span><span class="sxs-lookup"><span data-stu-id="7a034-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="7a034-284">(独自のサイトをテストする場合、ポート番号は、ほぼ確実に33561とは異なる数値になります)。Web サイトごとに異なるポートを使用することにより、IIS Express は、通信先のサイトを直接保つことができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="7a034-285">後でパブリック web サーバーにサイトを発行すると、URL に*localhost*が表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="7a034-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="7a034-286">その時点で、`http://myhostingsite/mywebsite/HelloWorld.cshtml` などの一般的な URL やページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="7a034-287">サイトの発行の詳細については、このチュートリアルシリーズの後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="7a034-288">サーバー側コードの追加</span><span class="sxs-lookup"><span data-stu-id="7a034-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="7a034-289">ブラウザーを閉じて、WebMatrix のページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="7a034-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="7a034-290">コードブロックに行を追加して、次のコードのようにします。</span><span class="sxs-lookup"><span data-stu-id="7a034-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="7a034-291">これは、いくつかの Razor コードです。</span><span class="sxs-lookup"><span data-stu-id="7a034-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="7a034-292">現在の日付と時刻が取得され、その値が `currentDateTime`という名前の*変数*に格納されていることは明らかです。</span><span class="sxs-lookup"><span data-stu-id="7a034-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="7a034-293">Razor 構文の詳細については、次のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="7a034-294">ページの本文で、`<p>Hello World!</p>` 要素の後に次を追加します。</span><span class="sxs-lookup"><span data-stu-id="7a034-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="7a034-295">このコードは、`currentDateTime` 変数に格納した値を上部に取得し、その値をページのマークアップに挿入します。</span><span class="sxs-lookup"><span data-stu-id="7a034-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="7a034-296">`@` 文字は、ページ内の ASP.NET Web ページコードをマークします。</span><span class="sxs-lookup"><span data-stu-id="7a034-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="7a034-297">ページをもう一度実行します (WebMatrix はページを実行する前に変更を保存します)。</span><span class="sxs-lookup"><span data-stu-id="7a034-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="7a034-298">今度は、ページに日付と時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-298">This time you see the date and time in the page.</span></span>

![動的に生成された時間表示でブラウザーで実行されている Hello World&quot; ページを &quot;](getting-started/_static/image20.png)

<span data-ttu-id="7a034-300">しばらく待ってから、ブラウザーでページを更新してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="7a034-301">日付と時刻の表示が更新されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-301">The date and time display is updated.</span></span>

<span data-ttu-id="7a034-302">ブラウザーでページソースを確認します。</span><span class="sxs-lookup"><span data-stu-id="7a034-302">In the browser, look at the page source.</span></span> <span data-ttu-id="7a034-303">次のマークアップに似ています。</span><span class="sxs-lookup"><span data-stu-id="7a034-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="7a034-304">上部に `@{ }` ブロックがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7a034-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="7a034-305">また、日付と時刻`1/18/2012 2:49:50 PM` 表示に `@currentDateTime` は、 *..........................................*</span><span class="sxs-lookup"><span data-stu-id="7a034-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="7a034-306">ここでの変更点は、ページを実行したときに、`@`でマークされたすべてのコード (この場合はごくわずか) が ASP.NET によって処理されたことです。</span><span class="sxs-lookup"><span data-stu-id="7a034-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="7a034-307">コードによって出力が生成され、その出力がページに挿入されました。</span><span class="sxs-lookup"><span data-stu-id="7a034-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="7a034-308">ASP.NET Web ページは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7a034-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="7a034-309">ここでは、動的な Web コンテンツを作成 ASP.NET Web ページについて説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="7a034-310">先ほど作成したページには、前に見たものと同じ HTML マークアップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7a034-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="7a034-311">また、あらゆる種類のタスクを実行できるコードを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="7a034-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="7a034-312">この例では、現在の日付と時刻を取得するという単純なタスクを実行しました。</span><span class="sxs-lookup"><span data-stu-id="7a034-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="7a034-313">ご覧のとおり、HTML を使用してコードを intersperse し、ページに出力を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="7a034-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="7a034-314">他の*ユーザーがブラウザーで ASP.NET ページを*要求すると、web サーバーの途中でページが処理されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="7a034-315">ASP.NET は、コード (存在する場合) の出力を HTML としてページに挿入します。</span><span class="sxs-lookup"><span data-stu-id="7a034-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="7a034-316">コード処理が完了すると、ASP.NET によって、結果のページがブラウザーに送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a034-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="7a034-317">すべてのブラウザーは HTML です。</span><span class="sxs-lookup"><span data-stu-id="7a034-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="7a034-318">次に図を示します。</span><span class="sxs-lookup"><span data-stu-id="7a034-318">Here's a diagram:</span></span>

![ASP.NET が HTML を動的に生成する方法の概念フロー](getting-started/_static/image21.png)

<span data-ttu-id="7a034-320">この考え方は単純ですが、コードが実行できる多くの興味深いタスクがあります。また、HTML コンテンツをページに動的に追加するための多くの興味深い方法があります。</span><span class="sxs-lookup"><span data-stu-id="7a034-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="7a034-321">また、HTML ページと同様に *、ASP.NET ページ*には、ブラウザー自体 (JavaScript および jQuery コード) で実行されるコードを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="7a034-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="7a034-322">ここでは、このチュートリアルセットとそれ以降の手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="7a034-323">次へ</span><span class="sxs-lookup"><span data-stu-id="7a034-323">Coming Up Next</span></span>

<span data-ttu-id="7a034-324">このシリーズの次のチュートリアルでは、ASP.NET Web ページプログラミングについてもう少し詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a034-325">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="7a034-325">Additional Resources</span></span>

<span data-ttu-id="7a034-326">[ASP.NET web サイトを最初から作成](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)します。</span><span class="sxs-lookup"><span data-stu-id="7a034-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="7a034-327">これは、(ASP.NET Web ページではなく) WebMatrix の使用について具体的に説明したチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="7a034-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="7a034-328">このチュートリアルでは説明しませんが、WebMatrix の追加機能のいくつかについてもう少し詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="7a034-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7a034-329">Next</span><span class="sxs-lookup"><span data-stu-id="7a034-329">Next</span></span>](intro-to-web-pages-programming.md)
