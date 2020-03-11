---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012 での Page Inspector の使用 |Microsoft Docs
author: rick-anderson
description: このハンズオンラボでは、Visual Studio での web ページの問題を見つけて修正するための新しいツールを紹介します (Page Inspector)。 Page Inspector は新しいツールです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473800"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="a5a46-104">Visual Studio 2012 で Page Inspector を使用する</span><span class="sxs-lookup"><span data-stu-id="a5a46-104">Using Page Inspector in Visual Studio 2012</span></span>

<span data-ttu-id="a5a46-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="a5a46-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="a5a46-106">このハンズオンラボでは、Visual Studio での web ページの問題を見つけて修正するための新しいツールを紹介します (Page Inspector)。</span><span class="sxs-lookup"><span data-stu-id="a5a46-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="a5a46-107">Page Inspector は、ブラウザー診断ツールを Visual Studio に導入し、ブラウザー、ASP.NET、ソースコードの間で統合されたエクスペリエンスを提供する新しいツールです。</span><span class="sxs-lookup"><span data-stu-id="a5a46-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="a5a46-108">Web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) を Visual Studio IDE 内で直接レンダリングし、ソースコードと結果の出力の両方を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="a5a46-109">Page Inspector を使用すると、web サイトを簡単に分解したり、ページをすぐにすばやく構築したり、問題を迅速に診断したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="a5a46-110">今日では、ASP.NET MVC や WebForms など、柔軟でスケーラブルな web サイトをタイムリーに作成できる Web フレームワークが数多く用意されています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="a5a46-111">一方、IDE では、テンプレートベースのページと動的コンテンツのデザイナービューがサポートされていないため、ページの問題を見つけるのが困難になります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="a5a46-112">そのため、これらの web サイトをユーザーに表示するには、ブラウザーで開いている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="a5a46-113">Web 開発者は、外部ツールを使用して、ブラウザーで定期的に実行される問題を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="a5a46-114">次に、IDE に戻り、修正を開始します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="a5a46-115">これにより、IDE、ブラウザー、およびプロファイリングツールが非効率的になり、問題を再現するたびに、新しい配置とキャッシュのクリーニングが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="a5a46-116">Page Inspector は、結合された一連の機能を使用して、両方の長所を組み合わせて、クライアント (ブラウザーツール) とサーバー (ASP.NET とソースコード) の間の Web 開発のギャップを橋渡しします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="a5a46-117">Page Inspector を使用すると、ブラウザーに表示される HTML マークアップを生成したソースファイル内の要素 (サーバー側コードを含む) を確認できます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="a5a46-118">また Page Inspector を使用すると、CSS のプロパティや DOM 要素の属性を変更して、変更がブラウザーに直ちに反映されるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="a5a46-119">このハンズオンラボでは、Page Inspector 機能について説明し、Web アプリケーションの問題を解決するためにそれらを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="a5a46-120">**このラボには、似たフローを使用する2つの演習が含まれていますが、さまざまなテクノロジが対象ASP.NET MVC Developer の場合は、練習1を実行します。WebForms の開発者の場合は、練習2を実行**します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="a5a46-121">このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="a5a46-122">すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="a5a46-123">目標</span><span class="sxs-lookup"><span data-stu-id="a5a46-123">Objectives</span></span>

<span data-ttu-id="a5a46-124">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="a5a46-125">Page Inspector を使用して Web サイトを分解する</span><span class="sxs-lookup"><span data-stu-id="a5a46-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="a5a46-126">Page Inspector を使用した CSS スタイルの変更の検査とプレビュー</span><span class="sxs-lookup"><span data-stu-id="a5a46-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="a5a46-127">Page Inspector を使用して web ページの問題を検出して修正する</span><span class="sxs-lookup"><span data-stu-id="a5a46-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="a5a46-128">前提条件</span><span class="sxs-lookup"><span data-stu-id="a5a46-128">Prerequisites</span></span>

<span data-ttu-id="a5a46-129">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="a5a46-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="a5a46-130">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="a5a46-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="a5a46-131">Internet Explorer 9 以降</span><span class="sxs-lookup"><span data-stu-id="a5a46-131">Internet Explorer 9 or higher</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="a5a46-132">手順</span><span class="sxs-lookup"><span data-stu-id="a5a46-132">Exercises</span></span>

<span data-ttu-id="a5a46-133">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="a5a46-134">演習 1: ASP.NET MVC プロジェクトでの Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="a5a46-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="a5a46-135">演習 2: WebForms プロジェクトでの Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="a5a46-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="a5a46-136">各演習には、演習の Begin フォルダーにある開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行できます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="a5a46-137">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む終了フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="a5a46-138">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

<span data-ttu-id="a5a46-139">このラボの推定所要時間: **30 分**。</span><span class="sxs-lookup"><span data-stu-id="a5a46-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="a5a46-140">演習 1: ASP.NET MVC プロジェクトでの Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="a5a46-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="a5a46-141">この演習では、 **Page Inspector**を使用して**ASP.NET MVC 4**ソリューションをプレビューし、デバッグする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="a5a46-142">まず、ツールについて簡単に説明して、Web デバッグプロセスを容易にする機能について学習します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="a5a46-143">次に、スタイルの問題を含む web ページで作業を行います。</span><span class="sxs-lookup"><span data-stu-id="a5a46-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="a5a46-144">Page Inspector を使用して、問題を生成して修正するソースコードを見つける方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="a5a46-145">タスク 1-Page Inspector の調査</span><span class="sxs-lookup"><span data-stu-id="a5a46-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="a5a46-146">このタスクでは、フォトギャラリーを表示する ASP.NET MVC 4 プロジェクトのコンテキストで Page Inspector を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="a5a46-147">**Source/Ex1-MVC4/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="a5a46-148">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="a5a46-149">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="a5a46-150">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="a5a46-151">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a5a46-152">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="a5a46-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="a5a46-153">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="a5a46-154">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="a5a46-155">ソリューションエクスプローラーで、 **[/]** ビュー プロジェクトフォルダーの下にある **[インデックス]** を見つけて右クリックし、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="a5a46-156">![プレビューするファイルを選択 Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "プレビューするファイルを選択 Page Inspector")</span><span class="sxs-lookup"><span data-stu-id="a5a46-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="a5a46-157">*プレビューするファイルを選択 Page Inspector*</span><span class="sxs-lookup"><span data-stu-id="a5a46-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="a5a46-158">[Page Inspector] ウィンドウに、選択したソースビューにマップされている */Home/Index* URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![PageInspector を使用した最初の連絡先](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="a5a46-160">*の最初の連絡先 Page Inspector*</span><span class="sxs-lookup"><span data-stu-id="a5a46-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="a5a46-161">Page Inspector ツールは、Visual Studio 環境に統合されています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="a5a46-162">インスペクターには、強力な HTML プロファイラーと共に、埋め込みブラウザーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="a5a46-163">ソリューションを実行して、ページの外観を確認する必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-164">Page Inspector ブラウザーの幅が、開いているページの幅よりも小さい場合、ページは正しく表示されません。</span><span class="sxs-lookup"><span data-stu-id="a5a46-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="a5a46-165">そのような場合は、Page Inspector の幅を調整します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="a5a46-166">Page Inspector の **[ファイル]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="a5a46-167">インデックスページを作成しているすべてのソースファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="a5a46-168">この機能は、すべての要素を一目で特定するのに役立ちます。特に、部分的なビューとテンプレートを操作する場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="a5a46-169">リンクをクリックすると、各ファイルを開くこともできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="a5a46-171">*[ファイル] タブ*</span><span class="sxs-lookup"><span data-stu-id="a5a46-171">*The Files tab*</span></span>
5. <span data-ttu-id="a5a46-172">タブの左側にある **[トグル検査モード]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="a5a46-173">このツールを使用すると、ページの任意の要素を選択し、HTML および Razor コードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![トグル/検査-モード-ボタン](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="a5a46-175">*検査モードボタンの切り替え*</span><span class="sxs-lookup"><span data-stu-id="a5a46-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="a5a46-176">Page Inspector ブラウザーで、ページ要素の上にマウスポインターを移動します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="a5a46-177">表示されるページの任意の部分にマウスポインターを移動すると、要素の種類が表示され、対応するソースマークアップまたはコードが Visual Studio エディターで強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![検査モードが動作しています](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="a5a46-179">*検査モードが動作しています*</span><span class="sxs-lookup"><span data-stu-id="a5a46-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-180">[Page Inspector] ウィンドウを最大化しないでください。または、ソースコードが表示されている [プレビュー] タブを表示できなくなります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="a5a46-181">Page Inspector の要素をクリックすると、その要素が最大化されると、選択したソースコードが表示されますが、Page Inspector ウィンドウは非表示になります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="a5a46-182">**インデックスの cshtml**ファイルに注意を払うと、選択した要素を生成するソースコードの部分が強調表示されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="a5a46-183">この機能により、長いソースファイルの編集が容易になり、コードに直接アクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![検査 (要素を)](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="a5a46-185">*検査 (要素を)*</span><span class="sxs-lookup"><span data-stu-id="a5a46-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="a5a46-186">**[検査モードの切り替え]** ボタンをクリックします ([![html] タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。](using-page-inspector-in-visual-studio-2012/_static/image7.png "[HTML] タブを選択すると、Page Inspector ブラウザーに表示される HTML コードが表示されます。")</span><span class="sxs-lookup"><span data-stu-id="a5a46-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="a5a46-187">) 、カーソルを無効にします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="a5a46-188">**[Html]** タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="a5a46-189">HTML マークアップで、[オブジェクト] リンクがあるリスト項目を見つけて選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="a5a46-190">コードを選択すると、対応する出力がブラウザーで自動的に強調表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="a5a46-191">この機能は、HTML ブロックがページにどのように表示されるかを確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="a5a46-192">![ページ内の HTML 要素の選択](using-page-inspector-in-visual-studio-2012/_static/image8.png "ページ内の HTML 要素の選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="a5a46-193">*ページ内の HTML 要素の選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="a5a46-194">**[検査モードの切り替え]** ボタンをクリックして*検査モード*を有効にし、ナビゲーションバーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="a5a46-195">HTML コードの右側にある [スタイル] ペインに、選択した要素に CSS スタイルが適用された一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-196">ヘッダーはサイトレイアウトの一部であるため、Page Inspector は \_Layout ファイルも開き、影響を受けるコードのセグメントを強調表示します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![スタイルの検出](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="a5a46-198">*選択した要素のスタイルとソースファイルの検出*</span><span class="sxs-lookup"><span data-stu-id="a5a46-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="a5a46-199">トグルインスペクションポインターが有効になっている状態で、マウスポインターを青いおすすめバーの下に移動し、半円をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="a5a46-200">![要素の選択](using-page-inspector-in-visual-studio-2012/_static/image10.png "要素の選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="a5a46-201">*要素の選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-201">*Selecting an element*</span></span>
12. <span data-ttu-id="a5a46-202">スタイルペインで、 **[...]** グループの下にある**背景画像**項目を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="a5a46-203">**背景イメージ**を**オフ**にして、何が起こるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="a5a46-204">ブラウザーに変更がすぐに反映され、円が非表示になっていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-205">[Page Inspector スタイル] タブで適用した変更は、元のスタイルシートには影響しません。</span><span class="sxs-lookup"><span data-stu-id="a5a46-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="a5a46-206">スタイルの選択を解除したり、必要な数だけ値を変更したりできますが、ページを更新した後に復元されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="a5a46-207">![CSS スタイルの有効化と無効化](using-page-inspector-in-visual-studio-2012/_static/image11.png "CSS スタイルの有効化と無効化")</span><span class="sxs-lookup"><span data-stu-id="a5a46-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="a5a46-208">*CSS スタイルの有効化と無効化*</span><span class="sxs-lookup"><span data-stu-id="a5a46-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="a5a46-209">次に、検査モードを使用して、ヘッダーの "your**logo here**" テキストをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="a5a46-210">**[スタイル]** タブで、 **[サイト-タイトル]** グループの下の **[フォントサイズ]** CSS 属性を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="a5a46-211">属性値をダブルクリックし、2.3 em 値を**3 em**に**置き換えて、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="a5a46-212">タイトルが大きくなっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="a5a46-213">![Page Inspector での CSS 値の変更](using-page-inspector-in-visual-studio-2012/_static/image12.png "Page Inspector での CSS 値の変更")</span><span class="sxs-lookup"><span data-stu-id="a5a46-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="a5a46-214">*Page Inspector での CSS 値の変更*</span><span class="sxs-lookup"><span data-stu-id="a5a46-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="a5a46-215">Page Inspector の右ペインにある **[トレーススタイル]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="a5a46-216">これは、選択に適用されているすべてのスタイルを属性名順に表示するための別の方法です。</span><span class="sxs-lookup"><span data-stu-id="a5a46-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSS スタイルのトレース](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="a5a46-218">*選択された要素の CSS スタイルのトレース*</span><span class="sxs-lookup"><span data-stu-id="a5a46-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="a5a46-219">Page Inspector のもう1つの機能は、レイアウトペインです。</span><span class="sxs-lookup"><span data-stu-id="a5a46-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="a5a46-220">検査モードを使用して、ナビゲーションバーを選択し、右側のウィンドウの **[レイアウト]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="a5a46-221">選択した要素の正確なサイズに加え、オフセット、余白、余白、および境界線のサイズが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="a5a46-222">このビューから値を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="a5a46-223">![Page Inspector での要素のレイアウト](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector での要素のレイアウト")</span><span class="sxs-lookup"><span data-stu-id="a5a46-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="a5a46-224">*Page Inspector での要素のレイアウト*</span><span class="sxs-lookup"><span data-stu-id="a5a46-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="a5a46-225">タスク 2-フォトギャラリーでのスタイルの問題の検出と修正</span><span class="sxs-lookup"><span data-stu-id="a5a46-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="a5a46-226">以前のバージョンの Visual Studio で Web ページの問題を診断するにはどうすればよいですか。</span><span class="sxs-lookup"><span data-stu-id="a5a46-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="a5a46-227">Internet Explorer 開発者ツールや焼討バグなど、Visual Studio IDE の外部で実行される web デバッグツールに慣れている場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="a5a46-228">ブラウザーは HTML、スクリプト、およびスタイルを理解するだけで、基になるフレームワークはレンダリングされる HTML を生成します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="a5a46-229">そのため、多くの場合、サイト全体を展開して、web ページの外観を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="a5a46-230">Web サイトの問題を検出して修正する場合は、次の手順に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="a5a46-231">Visual Studio からソリューションを実行するか、web サーバーにページを配置します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="a5a46-232">ブラウザーで、使用する開発者ツールを開くか、ソースコードとスタイルを開いて問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="a5a46-233">関連するファイルを見つけるには、&quot;検索&quot; を使用するか、スタイルクラスの名前を使用してファイル&quot; 機能を検索 &quot;ます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="a5a46-234">エラーが検出されたら、Web ブラウザーとサーバーを停止します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="a5a46-235">ブラウザーのキャッシュをクリアします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="a5a46-236">修正プログラムを適用するには、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="a5a46-237">テストするすべての手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="a5a46-238">ASP.NET MVC 4 には実際の WYSIWYG は存在しないため、web アプリケーションを実行またはデプロイした後で、スタイルの問題のほとんどが後の段階で検出されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="a5a46-239">現在、Page Inspector では、ソリューションを実行せずに任意のページをプレビューすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="a5a46-240">このタスクでは、Page inspector を使用して、フォトギャラリーアプリケーションのいくつかの問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="a5a46-241">Page Inspector を使用して、ヘッダーの左側にある**レジスタ**と**ログイン**リンクを見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="a5a46-242">リンクは右側に期待される場所に表示されず、箇条書きリストのように表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="a5a46-243">次に、リンクを右揃えにして、適切にスタイルを調整します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="a5a46-244">![登録とログインのリンクの検索](using-page-inspector-in-visual-studio-2012/_static/image15.png "登録とログインのリンクの検索")</span><span class="sxs-lookup"><span data-stu-id="a5a46-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="a5a46-245">*登録とログインのリンクの検索*</span><span class="sxs-lookup"><span data-stu-id="a5a46-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="a5a46-246">トグル検査モードを選択した状態で、[登録] リンクをクリックしてコードを開きます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="a5a46-247">リンクのソースコードは **\_LoginPartial**ファイルにあります。これは、最初に見られる場所である、インデックス番号と \_の形式ではありません。</span><span class="sxs-lookup"><span data-stu-id="a5a46-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="a5a46-248">正しいソースファイルに直接配置されています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="a5a46-249">**[スタイル]** タブで、[ **\<] セクション**を見つけてクリックします。これは、これらのリンクの HTML コンテナーである #login 項目 > ます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-249">In the **Styles** tab, locate and click the **\<section> #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="a5a46-250">クリックすると、 **[#login]** スタイルが **[.css]** に自動的に配置されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="a5a46-251">さらに、コードが強調表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="a5a46-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="a5a46-252">![CSS スタイルの選択](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS スタイルの選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="a5a46-253">*CSS スタイルの選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="a5a46-254">強調表示されたコード内の**テキストの整列**属性のコメントを解除します。そのためには、開始文字と終了文字を削除して、**サイトの .css**ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="a5a46-255">Page Inspector は、現在のページを構成するすべての異なるファイルを認識し、これらのファイルのいずれかが変更されたときに検出することができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="a5a46-256">ブラウザーの現在のページがソースファイルと同期されていない場合は、いつでもアラートが生成されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="a5a46-257">Page Inspector ブラウザーで、アドレスバーの下にあるバーをクリックして、ページを再度読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![ページの再読み込み](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="a5a46-259">*ページの再読み込み*</span><span class="sxs-lookup"><span data-stu-id="a5a46-259">*Reloading the page*</span></span>

    <span data-ttu-id="a5a46-260">リンクは右側に表示されていますが、箇条書きのように見えます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="a5a46-261">ここで、箇条書きを削除して、リンクを水平方向に揃えます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![更新されたページ](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="a5a46-263">*更新されたページ*</span><span class="sxs-lookup"><span data-stu-id="a5a46-263">*Updated page*</span></span>
6. <span data-ttu-id="a5a46-264">検査モードを使用して、&quot;レジスタ&quot; を含む任意の **&lt;li&gt;** 項目を選択し &quot;リンクを&quot; します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="a5a46-265">次に、[ **&lt;] セクション&gt; #login**項目をクリックして、**スタイルの .css**コードにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="a5a46-266">![スタイルの検索](using-page-inspector-in-visual-studio-2012/_static/image19.png "スタイルの検索")</span><span class="sxs-lookup"><span data-stu-id="a5a46-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="a5a46-267">*スタイルの検索*</span><span class="sxs-lookup"><span data-stu-id="a5a46-267">*Finding the style*</span></span>
7. <span data-ttu-id="a5a46-268">**.Css**で **#login li**項目のコードをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="a5a46-269">追加するスタイルによって、行頭文字が非表示になり、項目が横方向に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="a5a46-270">![ログインリンクのスタイルを再設定する](using-page-inspector-in-visual-studio-2012/_static/image20.png "ログインリンクのスタイルを再設定する")</span><span class="sxs-lookup"><span data-stu-id="a5a46-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="a5a46-271">*ログインリンクのスタイルを再設定する*</span><span class="sxs-lookup"><span data-stu-id="a5a46-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="a5a46-272">**スタイルの .css**ファイルを保存し、アドレスの下にあるバーで [1 回] をクリックして、ページを再度読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="a5a46-273">リンクが正しく表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="a5a46-274">![右側に合わせたリンク](using-page-inspector-in-visual-studio-2012/_static/image21.png "右側に合わせたリンク")</span><span class="sxs-lookup"><span data-stu-id="a5a46-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="a5a46-275">*右側に合わせたリンク*</span><span class="sxs-lookup"><span data-stu-id="a5a46-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="a5a46-276">最後に、ヘッダーのタイトルを変更します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-276">Finally, you will change the header title.</span></span> <span data-ttu-id="a5a46-277">検査モードを使用して、**ここでロゴ**をクリックすると、そのテキストを生成するソースコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="a5a46-278">これで、 **Layout\_** になりました。 '**logo**' のテキストを '**フォトギャラリー**' で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="a5a46-279">Page Inspector ブラウザーを保存して更新します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="a5a46-280">![新しいタイトルの割り当て](using-page-inspector-in-visual-studio-2012/_static/image22.png "新しいタイトルの割り当て")</span><span class="sxs-lookup"><span data-stu-id="a5a46-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="a5a46-281">*新しいタイトルの割り当て*</span><span class="sxs-lookup"><span data-stu-id="a5a46-281">*Assigning a new title*</span></span>

    ![フォトギャラリーページ](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="a5a46-283">*フォトギャラリーページが更新されました*</span><span class="sxs-lookup"><span data-stu-id="a5a46-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="a5a46-284">最後に、 **Photogallery**プロジェクトを選択し、 **F5**キーを押してアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-284">Finally, select the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="a5a46-285">すべての変更が期待どおりに動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-285">Check out all the changes work as expected.</span></span>

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="a5a46-286">演習 2: WebForms プロジェクトでの Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="a5a46-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="a5a46-287">この演習では、Page Inspector を使用して WebForms ソリューションをプレビューおよびデバッグする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="a5a46-288">まず、ツールについて簡単に説明して、Web デバッグプロセスを容易にする Page Inspector 機能について学習します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="a5a46-289">次に、スタイルの問題を含む web ページで作業を行います。</span><span class="sxs-lookup"><span data-stu-id="a5a46-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="a5a46-290">Page Inspector を使用して、問題を生成して修正するソースコードを見つける方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="a5a46-291">タスク 1-Page Inspector の調査</span><span class="sxs-lookup"><span data-stu-id="a5a46-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="a5a46-292">このタスクでは、フォトギャラリーを表示する WebForms プロジェクトのコンテキストで Page Inspector 機能を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="a5a46-293">**Source/Ex2-WebForms/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="a5a46-294">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="a5a46-295">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="a5a46-296">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="a5a46-297">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a5a46-298">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="a5a46-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="a5a46-299">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="a5a46-300">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="a5a46-301">ソリューションエクスプローラーで**default.aspx**ページを検索し、右クリックして、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="a5a46-302">![Page Inspector で default.aspx を開く](using-page-inspector-in-visual-studio-2012/_static/image24.png "Page Inspector で default.aspx を開く")</span><span class="sxs-lookup"><span data-stu-id="a5a46-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="a5a46-303">*Page Inspector で default.aspx を開く*</span><span class="sxs-lookup"><span data-stu-id="a5a46-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="a5a46-304">Page Inspector ウィンドウに default.aspx が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="a5a46-305">![Page Inspector で default.aspx を表示する](using-page-inspector-in-visual-studio-2012/_static/image25.png "Page Inspector で default.aspx を表示する")</span><span class="sxs-lookup"><span data-stu-id="a5a46-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="a5a46-306">*Page Inspector で default.aspx を表示する*</span><span class="sxs-lookup"><span data-stu-id="a5a46-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="a5a46-307">Page Inspector ツールは、Visual Studio 環境に統合されています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="a5a46-308">インスペクターには、選択したコードを表示する強力な HTML プロファイラーと共に、埋め込みブラウザーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="a5a46-309">ソリューションを実行して、ページの外観を確認する必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-310">Page Inspector ブラウザーの幅が、開いているページの幅よりも小さい場合、ページは正しく表示されません。</span><span class="sxs-lookup"><span data-stu-id="a5a46-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="a5a46-311">そのような場合は、Page Inspector の幅を調整します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="a5a46-312">Page Inspector の **[ファイル]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="a5a46-313">レンダリングされた既定のページを作成しているすべてのソースファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="a5a46-314">これは、特にユーザーコントロールやマスターページを操作しているときに、すべての要素を一目で確認するのに便利な機能です。</span><span class="sxs-lookup"><span data-stu-id="a5a46-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="a5a46-315">各ファイルに移動することもできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="a5a46-316">![[ファイル] タブ](using-page-inspector-in-visual-studio-2012/_static/image26.png "[ファイル] タブ")</span><span class="sxs-lookup"><span data-stu-id="a5a46-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="a5a46-317">*[ファイル] タブ*</span><span class="sxs-lookup"><span data-stu-id="a5a46-317">*The Files tab*</span></span>
5. <span data-ttu-id="a5a46-318">タブの左側にある **[トグル検査モード]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="a5a46-319">このツールを使用すると、ページの任意の要素を選択し、その HTML コードと .aspx ソースを表示できます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="a5a46-320">![検査モードボタンの切り替え](using-page-inspector-in-visual-studio-2012/_static/image27.png "検査モードボタンの切り替え")</span><span class="sxs-lookup"><span data-stu-id="a5a46-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="a5a46-321">*検査モードボタンの切り替え*</span><span class="sxs-lookup"><span data-stu-id="a5a46-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="a5a46-322">Page Inspector ブラウザーで、ページ要素の上にマウスポインターを移動します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="a5a46-323">表示されるページの任意の部分にマウスポインターを移動すると、要素の種類が表示され、対応するソースマークアップまたはコードが Visual Studio エディターで強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="a5a46-324">![検査モードが動作しています](using-page-inspector-in-visual-studio-2012/_static/image28.png "検査モードが動作しています")</span><span class="sxs-lookup"><span data-stu-id="a5a46-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="a5a46-325">*検査モードが動作しています*</span><span class="sxs-lookup"><span data-stu-id="a5a46-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-326">[Page Inspector] ウィンドウを最大化しないでください。または、ソースコードが表示されている [プレビュー] タブを表示できなくなります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="a5a46-327">Page Inspector の要素をクリックすると、その要素が最大化されると、選択したソースコードが表示されますが、Page Inspector ウィンドウは非表示になります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="a5a46-328">**Default.aspx**ファイルに注意を払う場合は、選択した要素を生成するソースコードの部分が強調表示されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="a5a46-329">この機能により、長いソースファイルのエディションが容易になり、コードに直接アクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="a5a46-330">![検査 (要素を)](using-page-inspector-in-visual-studio-2012/_static/image29.png "検査 (要素を)")</span><span class="sxs-lookup"><span data-stu-id="a5a46-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="a5a46-331">*検査 (要素を)*</span><span class="sxs-lookup"><span data-stu-id="a5a46-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="a5a46-332">**[検査モードの切り替え]** ボタンをクリックします (![-HTML--html-tab](using-page-inspector-in-visual-studio-2012/_static/image30.png "[-HTML]-[-HTML-html----------------------]-[ブラウザー] を選択します。") ---------------)-ブラウザーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="a5a46-333">) 、カーソルを無効にする、Page Inspector のタブにあります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="a5a46-334">**[Html]** タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="a5a46-335">HTML コードで、[] リンクをクリックしてリスト項目を探し、それを選択します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="a5a46-336">コードを選択すると、対応する出力が自動的に強調表示されたブラウザーになります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="a5a46-337">この機能は、HTML ブロックがページにどのように表示されるかを確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="a5a46-338">![ページ内の HTML 要素の選択](using-page-inspector-in-visual-studio-2012/_static/image31.png "ページ内の HTML 要素の選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="a5a46-339">*ページ内の HTML 要素の選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="a5a46-340">**[検査モードの切り替え]** ボタンをクリックして*検査モード*を有効にし、ナビゲーションバーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="a5a46-341">HTML コードの右側にある [スタイル] ペインに、選択した要素に CSS スタイルが適用された一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-342">ヘッダーはサイトレイアウトの一部であるため、Page Inspector によって、サイトのマスターファイルも開き、影響を受けるコードのセグメントが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="a5a46-343">![スタイルの検出 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "選択した要素のスタイルとソースファイルの検出")</span><span class="sxs-lookup"><span data-stu-id="a5a46-343">![Discovering styles WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="a5a46-344">*選択した要素のスタイルとソースファイルの検出*</span><span class="sxs-lookup"><span data-stu-id="a5a46-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="a5a46-345">トグルインスペクションポインターが有効になっている状態で、マウスポインターをメニューバーの下に移動し、空白の円をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="a5a46-346">![要素の選択](using-page-inspector-in-visual-studio-2012/_static/image33.png "要素の選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="a5a46-347">*要素の選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-347">*Selecting an element*</span></span>
12. <span data-ttu-id="a5a46-348">スタイルペインで、 **[...]** グループの下にある**背景画像**項目を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="a5a46-349">**背景イメージ**を**オフ**にして、何が起こるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="a5a46-350">ブラウザーに変更がすぐに反映され、円が非表示になっていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a46-351">[Page Inspector スタイル] タブで適用した変更は、元のスタイルシートには影響しません。</span><span class="sxs-lookup"><span data-stu-id="a5a46-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="a5a46-352">スタイルの選択を解除したり、必要な数だけ値を変更したりできますが、ページを更新した後に復元されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="a5a46-353">![CSS styles2 を有効または無効にする](using-page-inspector-in-visual-studio-2012/_static/image34.png "CSS スタイルの有効化と無効化")</span><span class="sxs-lookup"><span data-stu-id="a5a46-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="a5a46-354">*CSS スタイルの有効化と無効化*</span><span class="sxs-lookup"><span data-stu-id="a5a46-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="a5a46-355">次に、検査モードを使用**して、ヘッダーの "your** **logo here"** テキストをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="a5a46-356">**[スタイル]** タブで、 **[サイト-タイトル]** グループの下の **[フォントサイズ]** CSS 属性を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="a5a46-357">属性の値を編集するには、属性を1回ダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="a5a46-358">2\.3 em 値を**3em**に置き換え、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="a5a46-359">タイトルが大きくなっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="a5a46-360">![ページ Inspector2 の CSS 値の変更](using-page-inspector-in-visual-studio-2012/_static/image35.png "Page Inspector での CSS 値の変更")</span><span class="sxs-lookup"><span data-stu-id="a5a46-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="a5a46-361">*Page Inspector での CSS 値の変更*</span><span class="sxs-lookup"><span data-stu-id="a5a46-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="a5a46-362">Page Inspector の右ペインにある **[トレーススタイル]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="a5a46-363">これは、選択に適用されているすべてのスタイルを属性名順に表示するための別の方法です。</span><span class="sxs-lookup"><span data-stu-id="a5a46-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="a5a46-364">![選択された要素の CSS スタイルのトレース](using-page-inspector-in-visual-studio-2012/_static/image36.png "選択された要素の CSS スタイルのトレース")</span><span class="sxs-lookup"><span data-stu-id="a5a46-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="a5a46-365">*選択された要素の CSS スタイルのトレース*</span><span class="sxs-lookup"><span data-stu-id="a5a46-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="a5a46-366">Page Inspector のもう1つの機能は、レイアウトペインです。</span><span class="sxs-lookup"><span data-stu-id="a5a46-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="a5a46-367">検査モードを使用して、ナビゲーションバーを選択し、右側のウィンドウの **[レイアウト]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="a5a46-368">選択した要素の正確なサイズに加え、オフセット、余白、余白、および境界線のサイズが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="a5a46-369">このビューから値を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="a5a46-370">![Page Inspector での要素のレイアウト](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector での要素のレイアウト")</span><span class="sxs-lookup"><span data-stu-id="a5a46-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="a5a46-371">*Page Inspector での要素のレイアウト*</span><span class="sxs-lookup"><span data-stu-id="a5a46-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="a5a46-372">タスク 2-フォトギャラリーでのスタイルの問題の検出と修正</span><span class="sxs-lookup"><span data-stu-id="a5a46-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="a5a46-373">以前のバージョンの Visual Studio で Web ページの問題を診断するにはどうすればよいですか。</span><span class="sxs-lookup"><span data-stu-id="a5a46-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="a5a46-374">Internet Explorer 開発者ツールや焼討バグなど、Visual Studio IDE の外部で実行される web デバッグツールに慣れている場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="a5a46-375">ブラウザーは HTML、スクリプト、およびスタイルを理解するだけで、基になるフレームワークはレンダリングされる HTML を生成します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="a5a46-376">そのため、多くの場合、サイト全体を展開して、web ページの外観を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="a5a46-377">Web サイトの問題を検出して修正する場合は、次の手順に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="a5a46-378">Visual Studio からソリューションを実行するか、web サーバーにページを配置します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="a5a46-379">ブラウザーで、使用する開発者ツールを開くか、ソースコードとスタイルを開いて問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="a5a46-380">関連するファイルを見つけるには、&quot;検索&quot; を使用するか、スタイルクラスの名前を使用してファイル&quot; 機能を検索 &quot;ます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="a5a46-381">エラーが検出されたら、Web ブラウザーとサーバーを停止します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="a5a46-382">ブラウザーのキャッシュをクリアします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="a5a46-383">修正プログラムを適用するには、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="a5a46-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="a5a46-384">テストするすべての手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="a5a46-385">ASP.NET WebForms に実際の WYSIWYG は存在しないため、いくつかのスタイルの問題は、実行中または配置後に、後の段階で検出されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="a5a46-386">現在、Page Inspector では、ソリューションを実行せずに任意のページをプレビューすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="a5a46-387">このタスクでは、Page inspector を使用して、フォトギャラリーアプリケーションのいくつかの問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="a5a46-388">次の手順では、ヘッダーのいくつかの簡単なスタイルの問題を検出して迅速に修正します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="a5a46-389">ページ検査を使用して、ヘッダーの左側にある**レジスタ**と**ログイン**リンクを探します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="a5a46-390">右側の適切な場所にリンクが表示されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5a46-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="a5a46-391">次に、リンクを右揃えにして、それに応じてスタイルを調整します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="a5a46-392">![左側に配置されているログインリンク](using-page-inspector-in-visual-studio-2012/_static/image38.png "左側に配置されているログインリンク")</span><span class="sxs-lookup"><span data-stu-id="a5a46-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="a5a46-393">*左側に配置されているログインリンク*</span><span class="sxs-lookup"><span data-stu-id="a5a46-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="a5a46-394">トグル検査モードを選択した状態で、[ログイン] リンクを選択してコードを開きます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="a5a46-395">リンクのソースコードは、default.aspx ページではなく、最初に表示される場所である、default.aspx ファイルにあることに注意し**てください。** 正しいソースファイルに直接配置されています。</span><span class="sxs-lookup"><span data-stu-id="a5a46-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="a5a46-396">**[スタイル]** タブで、[ **&lt;] セクション**を見つけてクリックします。これは、これらのリンクの HTML コンテナーである #login 項目&gt; ます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="a5a46-397">クリックすると、 **[#login]** スタイルが **[.css]** に自動的に配置されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="a5a46-398">さらに、コードが強調表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="a5a46-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="a5a46-399">![CSS スタイルの選択](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS スタイルの選択")</span><span class="sxs-lookup"><span data-stu-id="a5a46-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="a5a46-400">*CSS スタイルの選択*</span><span class="sxs-lookup"><span data-stu-id="a5a46-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="a5a46-401">強調表示されたコード内の**テキストの整列**属性のコメントを解除します。そのためには、開始文字と終了文字を削除して、**サイトの .css**ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="a5a46-402">Page Inspector は、現在のページを構成するすべての異なるファイルを認識し、これらのファイルのいずれかが変更されたときに検出することができます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="a5a46-403">ブラウザーの現在のページがソースファイルと同期されていない場合は、いつでもアラートが生成されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="a5a46-404">Page Inspector ブラウザーで、アドレスバーの下にあるバーをクリックして変更を保存し、ページを再度読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![ページの再読み込み](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="a5a46-406">*ページの再読み込み*</span><span class="sxs-lookup"><span data-stu-id="a5a46-406">*Reloading the page*</span></span>

    <span data-ttu-id="a5a46-407">リンクは右側に表示されていますが、箇条書きのように見えます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="a5a46-408">ここで、箇条書きを削除して、リンクを水平方向に揃えます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![更新されたページ](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="a5a46-410">*更新されたページ*</span><span class="sxs-lookup"><span data-stu-id="a5a46-410">*Updated page*</span></span>
6. <span data-ttu-id="a5a46-411">検査モードを使用して、&quot;レジスタ&quot; を含む任意の **&lt;li&gt;** 項目を選択し &quot;リンクを&quot; します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="a5a46-412">次に、[ **&lt;] セクション&gt; #login**項目をクリックして、**スタイルの .css**コードにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="a5a46-413">![スタイルの検索](using-page-inspector-in-visual-studio-2012/_static/image42.png "スタイルの検索")</span><span class="sxs-lookup"><span data-stu-id="a5a46-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="a5a46-414">*スタイルの検索*</span><span class="sxs-lookup"><span data-stu-id="a5a46-414">*Finding the style*</span></span>
7. <span data-ttu-id="a5a46-415">**.Css**で **#login li**項目のコードをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="a5a46-416">追加するスタイルによって、行頭文字が非表示になり、項目が横方向に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="a5a46-417">![ログインリンクのスタイルを再設定する](using-page-inspector-in-visual-studio-2012/_static/image43.png "ログインリンクのスタイルを再設定する")</span><span class="sxs-lookup"><span data-stu-id="a5a46-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="a5a46-418">*ログインリンクのスタイルを再設定する*</span><span class="sxs-lookup"><span data-stu-id="a5a46-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="a5a46-419">**スタイルの .css**ファイルを保存し、アドレスの下にあるバーで [1 回] をクリックして、ページを再度読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="a5a46-420">リンクが正しく表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="a5a46-421">![右側に合わせたリンク](using-page-inspector-in-visual-studio-2012/_static/image44.png "右側に合わせたリンク")</span><span class="sxs-lookup"><span data-stu-id="a5a46-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="a5a46-422">*右側に合わせたリンク*</span><span class="sxs-lookup"><span data-stu-id="a5a46-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="a5a46-423">最後に、ヘッダーのタイトルを変更します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-423">Finally, you will change the header title.</span></span> <span data-ttu-id="a5a46-424">すべてのファイルで ' your**logo here '** テキストを検索するのではなく、検査モードを使用してテキストをクリックし、それを生成するソースコードにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="a5a46-425">![サイトのタイトルの検索](using-page-inspector-in-visual-studio-2012/_static/image45.png "サイトのタイトルの検索")</span><span class="sxs-lookup"><span data-stu-id="a5a46-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="a5a46-426">*サイトのタイトルの検索*</span><span class="sxs-lookup"><span data-stu-id="a5a46-426">*Finding the site title*</span></span>
10. <span data-ttu-id="a5a46-427">これで、"your**logo here**" というテキストを '**フォトギャラリー**' で置き換えることができ**ます。**</span><span class="sxs-lookup"><span data-stu-id="a5a46-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="a5a46-428">Page Inspector ブラウザーを保存して更新します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="a5a46-429">![フォトギャラリーページが更新されました](using-page-inspector-in-visual-studio-2012/_static/image46.png "フォトギャラリーページが更新されました")</span><span class="sxs-lookup"><span data-stu-id="a5a46-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="a5a46-430">*フォトギャラリーページが更新されました*</span><span class="sxs-lookup"><span data-stu-id="a5a46-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="a5a46-431">最後に、 **F5**キーを押してアプリを実行し、すべての変更が期待どおりに動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="a5a46-432">まとめ</span><span class="sxs-lookup"><span data-stu-id="a5a46-432">Summary</span></span>

<span data-ttu-id="a5a46-433">このハンズオンラボでは、ブラウザーで Web サイトをリビルドして実行しなくても、Page Inspector を使用して Web アプリケーションをプレビューする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="a5a46-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="a5a46-434">また、レンダリングされた出力からソースコードに直接アクセスして、バグをすばやく見つけて修正する方法を習得しました。</span><span class="sxs-lookup"><span data-stu-id="a5a46-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="a5a46-435">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="a5a46-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="a5a46-436">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="a5a46-437">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="a5a46-438">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="a5a46-439">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="a5a46-440">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-440">Click on **Install Now**.</span></span> <span data-ttu-id="a5a46-441">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="a5a46-442">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="a5a46-443">![Visual Studio Express のインストール](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="a5a46-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="a5a46-444">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="a5a46-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="a5a46-445">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="a5a46-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="a5a46-447">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="a5a46-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="a5a46-448">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-448">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="a5a46-450">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="a5a46-450">*Installation progress*</span></span>
6. <span data-ttu-id="a5a46-451">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-451">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="a5a46-453">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="a5a46-453">*Installation completed*</span></span>
7. <span data-ttu-id="a5a46-454">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="a5a46-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="a5a46-455">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a5a46-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="a5a46-457">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="a5a46-457">*VS Express for Web tile*</span></span>
