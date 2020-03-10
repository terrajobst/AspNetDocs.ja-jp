---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'ハンズオンラボ: Visual Studio 2013 Web ツール |Microsoft Docs'
author: rick-anderson
description: Visual Studio は、の優れた開発環境です。NET ベースの Windows および web プロジェクト。 これには、簡単に使用できる強力なテキストエディターが含まれています。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505006"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="95afb-104">ハンズオンラボ: Visual Studio 2013 Web ツール</span><span class="sxs-lookup"><span data-stu-id="95afb-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="95afb-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="95afb-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="95afb-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="95afb-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="95afb-107">Visual Studio は、の優れた開発環境です。NET ベースの Windows および web プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="95afb-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="95afb-108">これには、プロジェクトなしでスタンドアロンファイルを編集するために簡単に使用できる強力なテキストエディターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="95afb-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="95afb-109">Visual Studio では、各ファイルを編集するときに、すべての機能を備えた解析ツリーが維持されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="95afb-110">これにより、Visual Studio は比類のないオートコンプリートとドキュメントベースのアクションを提供しながら、開発環境をはるかに高速かつ快適にすることができます。</span><span class="sxs-lookup"><span data-stu-id="95afb-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="95afb-111">これらの機能は、HTML および CSS ドキュメントで特に強力です。</span><span class="sxs-lookup"><span data-stu-id="95afb-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="95afb-112">また、拡張機能でもこの機能を利用できるため、必要に応じて強力な新機能を使用してエディターを簡単に拡張できます。</span><span class="sxs-lookup"><span data-stu-id="95afb-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="95afb-113">Web Essentials は、ほとんどの場合、Visual Studio の web 関連の拡張機能のコレクションです。</span><span class="sxs-lookup"><span data-stu-id="95afb-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="95afb-114">これには、多くの新しい IntelliSense 入力候補 (特に、CSS の場合)、新しいブラウザーリンク機能、JavaScript ファイルの自動 JSHint、HTML と CSS の新しい警告、および最新の web 開発に不可欠なその他多くの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="95afb-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="95afb-115">すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="95afb-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="95afb-116">概要</span><span class="sxs-lookup"><span data-stu-id="95afb-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="95afb-117">目標</span><span class="sxs-lookup"><span data-stu-id="95afb-117">Objectives</span></span>

<span data-ttu-id="95afb-118">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="95afb-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="95afb-119">豊富な HTML5 コードスニペットや Zen コーディングなど、Web Essentials に含まれる新しい HTML エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="95afb-120">カラーピッカーやブラウザーマトリックスのツールヒントなど、Web Essentials に含まれる新しい CSS エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="95afb-121">すべての HTML 要素のファイルや IntelliSense の抽出など、Web Essentials に含まれる新しい JavaScript エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="95afb-122">ブラウザーリンクを使用してブラウザーと Visual Studio の間でデータを交換する</span><span class="sxs-lookup"><span data-stu-id="95afb-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="95afb-123">前提条件</span><span class="sxs-lookup"><span data-stu-id="95afb-123">Prerequisites</span></span>

<span data-ttu-id="95afb-124">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="95afb-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="95afb-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)以上</span><span class="sxs-lookup"><span data-stu-id="95afb-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="95afb-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="95afb-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="95afb-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="95afb-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="95afb-128">セットアップ</span><span class="sxs-lookup"><span data-stu-id="95afb-128">Setup</span></span>

<span data-ttu-id="95afb-129">このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="95afb-130">Windows エクスプローラーウィンドウを開き、ラボの**ソース**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="95afb-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="95afb-131">**[Setup.exe]** を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="95afb-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="95afb-132">ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="95afb-133">セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="95afb-134">コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="95afb-134">Using the Code Snippets</span></span>

<span data-ttu-id="95afb-135">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="95afb-136">便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="95afb-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="95afb-137">各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。</span><span class="sxs-lookup"><span data-stu-id="95afb-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="95afb-138">演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="95afb-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="95afb-139">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="95afb-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="95afb-140">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="95afb-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="95afb-141">手順</span><span class="sxs-lookup"><span data-stu-id="95afb-141">Exercises</span></span>

<span data-ttu-id="95afb-142">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="95afb-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="95afb-143">ブラウザーリンクと Web Essentials の操作</span><span class="sxs-lookup"><span data-stu-id="95afb-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="95afb-144">コードスニペットと IntelliSense の活用</span><span class="sxs-lookup"><span data-stu-id="95afb-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="95afb-145">Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="95afb-146">定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。</span><span class="sxs-lookup"><span data-stu-id="95afb-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="95afb-147">このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="95afb-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="95afb-148">開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="95afb-149">演習 1: ブラウザーリンクと Web Essentials の操作</span><span class="sxs-lookup"><span data-stu-id="95afb-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="95afb-150">**Web Essentials**は、最新の web 開発に役立つさまざまな機能を追加する Visual Studio の拡張機能であり、ほとんどの場合、web 開発のエクスペリエンスをはるかに高速かつ快適にすることに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="95afb-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="95afb-151">Web Essentials は、Visual Studio の拡張機能ギャラリーからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="95afb-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="95afb-152">**ブラウザーリンク**は Visual Studio 2013 に含まれる新機能であり、VISUAL studio IDE と、web アプリケーションと visual studio の間でデータを交換するための任意のオープンブラウザーの間のチャネルを提供します。</span><span class="sxs-lookup"><span data-stu-id="95afb-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="95afb-153">Web Essentials は、ブラウザーリンクをツールと共に拡張し、DOM オブジェクトモデルと web ページの CSS スタイルをブラウザーから直接操作します。</span><span class="sxs-lookup"><span data-stu-id="95afb-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="95afb-154">この演習では、簡単なクイズページを強化するために、 **Web Essentials**と**ブラウザーリンク**でサポートされている機能をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="95afb-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="95afb-155">タスク 1-複数のブラウザーでプロジェクトを実行する</span><span class="sxs-lookup"><span data-stu-id="95afb-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="95afb-156">このタスクでは、複数のブラウザーで同時に実行されるように web アプリケーションを構成します。これは、ブラウザー間のテストに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="95afb-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="95afb-157">**Microsoft Visual Studio**を開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="95afb-158">**ファイル** メニューの 開く を選択します。 **プロジェクト/ソリューション...** ラボの**ソース**フォルダー (C:\WebCampsTK\HOL\VSWebTooling\Source) で**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin**を参照します。</span><span class="sxs-lookup"><span data-stu-id="95afb-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="95afb-159">**[開始]** を選択し、 **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="95afb-160">Visual Studio のツールバーで、ブラウザー メニューを展開し、**参照** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="95afb-161">![メニューオプションを使用して参照](visual-studio-2013-web-tools/_static/image1.png "参照...ブラウザーメニュー内")</span><span class="sxs-lookup"><span data-stu-id="95afb-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="95afb-162">*メニューオプションを使用して参照*</span><span class="sxs-lookup"><span data-stu-id="95afb-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="95afb-163">[**ブラウザー**の選択] ダイアログボックスで、 **CTRL**キーを押しながら [**既定と**して設定] をクリックして、 **Google Chrome**と**Internet Explorer**の両方を選択します。</span><span class="sxs-lookup"><span data-stu-id="95afb-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="95afb-164">![[参照] ダイアログボックス](visual-studio-2013-web-tools/_static/image2.png "[参照] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="95afb-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="95afb-165">*複数の既定のブラウザーの選択*</span><span class="sxs-lookup"><span data-stu-id="95afb-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="95afb-166">Google Chrome と Internet Explorer の両方が既定のブラウザーとして表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="95afb-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="95afb-167">**[キャンセル]** をクリックして、ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="95afb-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="95afb-168">![既定のブラウザーとしての Google Chrome および Internet Explorer](visual-studio-2013-web-tools/_static/image3.png "Google Chrome と Internet Explorer の既定のブラウザー")</span><span class="sxs-lookup"><span data-stu-id="95afb-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="95afb-169">*既定のブラウザーとしての Google Chrome および Internet Explorer*</span><span class="sxs-lookup"><span data-stu-id="95afb-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-170">既定のブラウザーを構成した後、ブラウザー メニューで **複数のブラウザー** オプションが選択されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="95afb-171">![複数のブラウザー](visual-studio-2013-web-tools/_static/image4.png "複数のブラウザー")</span><span class="sxs-lookup"><span data-stu-id="95afb-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="95afb-172">**CTRL** + **F5**キーを押して、デバッグなしでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="95afb-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="95afb-173">両方のブラウザーウィンドウを開いたときに、両方のブラウザーで同時に更新プログラムを表示するために、どちらか一方を配置します。</span><span class="sxs-lookup"><span data-stu-id="95afb-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="95afb-174">ブラウザーには、薄い青の四角形の付いた web ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="95afb-175">![1つのブラウザーを他のブラウザーの上に配置する](visual-studio-2013-web-tools/_static/image5.png "1つのブラウザーを他のブラウザーの上に配置する")</span><span class="sxs-lookup"><span data-stu-id="95afb-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="95afb-176">*1つのブラウザーを他のブラウザーの上に配置する*</span><span class="sxs-lookup"><span data-stu-id="95afb-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="95afb-177">ブラウザーを閉じないでください。</span><span class="sxs-lookup"><span data-stu-id="95afb-177">Do not close the browsers.</span></span> <span data-ttu-id="95afb-178">これらは、次のタスクで使用します。</span><span class="sxs-lookup"><span data-stu-id="95afb-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="95afb-179">タスク 2-Zen コーディングを使用して HTML 要素を作成する</span><span class="sxs-lookup"><span data-stu-id="95afb-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="95afb-180">**Zen コーディング**は、高速 HTML、XML、XSL (またはその他の構造化されたコード形式) のコーディングおよび編集用のエディタープラグインです。</span><span class="sxs-lookup"><span data-stu-id="95afb-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="95afb-181">このプラグインの中核となるのは、CSS セレクターに似た式を HTML コードに展開できる強力な省略形エンジンです。</span><span class="sxs-lookup"><span data-stu-id="95afb-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="95afb-182">Zen コーディングは、CSS スタイルセレクター構文を使用して HTML を記述する高速な方法です。</span><span class="sxs-lookup"><span data-stu-id="95afb-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="95afb-183">この演習では、Web Essentials によって提供される Zen コーディング機能を使用して、質問のオプションを表す HTML ボタンを生成します。</span><span class="sxs-lookup"><span data-stu-id="95afb-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="95afb-184">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="95afb-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="95afb-185">**Views** | **ホーム**フォルダーにある**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="95afb-186">**&lt;!--TODO: [オプションの追加]--&gt;** コメントを次のコードに置き換え、 **tab**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="95afb-187">コードは HTML に展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="95afb-188">![拡張 HTML](visual-studio-2013-web-tools/_static/image6.png "拡張 HTML")</span><span class="sxs-lookup"><span data-stu-id="95afb-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="95afb-189">*拡張 HTML*</span><span class="sxs-lookup"><span data-stu-id="95afb-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-190">Zen コーディング構文の詳細については、次の[記事](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="95afb-191">[リンクされた**ブラウザーの更新**] ボタンをクリックして、両方のブラウザーを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="95afb-192">![リンクされたブラウザーの更新](visual-studio-2013-web-tools/_static/image7.png "リンクされたブラウザーの更新")</span><span class="sxs-lookup"><span data-stu-id="95afb-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="95afb-193">*リンクされたブラウザーの更新*</span><span class="sxs-lookup"><span data-stu-id="95afb-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="95afb-194">![Internet Explorer-4 つのボタンで更新されたページ](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-4 つのボタンで更新されたページ")</span><span class="sxs-lookup"><span data-stu-id="95afb-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="95afb-195">*Internet Explorer-4 つのボタンで更新されたページ*</span><span class="sxs-lookup"><span data-stu-id="95afb-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="95afb-196">![Google Chrome-4 つのボタンで更新されたページ](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-4 つのボタンで更新されたページ")</span><span class="sxs-lookup"><span data-stu-id="95afb-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="95afb-197">*Google Chrome-4 つのボタンで更新されたページ*</span><span class="sxs-lookup"><span data-stu-id="95afb-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="95afb-198">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="95afb-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="95afb-199">ボタンをページに追加しましたが、それでもテンプレートの質問を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="95afb-200">これを行うには、 **Lorem Ipsum generator**と呼ばれる Web Essentials の新機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="95afb-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="95afb-201">**クラス**属性**front**の**div**要素を見つけます。</span><span class="sxs-lookup"><span data-stu-id="95afb-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="95afb-202">次のコードを**div**の最初の子要素として追加し、 **tab**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="95afb-203">コードは HTML に展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="95afb-204">![Lorem Ipsum 自動生成](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 自動生成")</span><span class="sxs-lookup"><span data-stu-id="95afb-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="95afb-205">*Lorem Ipsum 自動生成*</span><span class="sxs-lookup"><span data-stu-id="95afb-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-206">Zen コーディングの一部として、HTML エディターで直接 Lorem Ipsum コードを生成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="95afb-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="95afb-207">「 **Lorem** And Hit **TAB」** と入力するだけで、30ワード lorem Ipsum text が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="95afb-208">例:</span><span class="sxs-lookup"><span data-stu-id="95afb-208">E.g.</span></span> <span data-ttu-id="95afb-209">*lorem10*によって 10 Lorem Ipsum 単語が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="95afb-210">**Lorem Pixel generator**と呼ばれる Web Essentials の別の新機能を使用して、質問の一番上にロゴを追加します。</span><span class="sxs-lookup"><span data-stu-id="95afb-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="95afb-211">次のコードを**div**要素の最初の子要素として、**コンテナー**を**クラス**値として追加し、 **tab**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="95afb-212">コードは HTML に展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="95afb-213">![Lorem ピクセル自動生成](visual-studio-2013-web-tools/_static/image11.png "Lorem ピクセル自動生成")</span><span class="sxs-lookup"><span data-stu-id="95afb-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="95afb-214">*Lorem ピクセル自動生成*</span><span class="sxs-lookup"><span data-stu-id="95afb-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-215">Zen コーディングの一部として、HTML エディターで直接 Lorem ピクセルコードを生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="95afb-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="95afb-216">「 **Pix-200 x 200-** animal And Hit **TAB」** と入力するだけで、animal の 200 x 200 イメージを含む**img**タグが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="95afb-217">詳細については、「 [Lorem ピクセル](http://www.lorempixel.com)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="95afb-218">[リンクされた**ブラウザーの更新**] ボタンをクリックして、両方のブラウザーを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="95afb-219">![Internet Explorer で自動生成されたイメージとテキスト](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer で自動生成されたイメージとテキスト")</span><span class="sxs-lookup"><span data-stu-id="95afb-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="95afb-220">*Internet Explorer で自動生成されたイメージとテキスト*</span><span class="sxs-lookup"><span data-stu-id="95afb-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="95afb-221">![Google Chrome で自動生成されたイメージとテキスト](visual-studio-2013-web-tools/_static/image13.png "Google Chrome で自動生成されたイメージとテキスト")</span><span class="sxs-lookup"><span data-stu-id="95afb-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="95afb-222">*Google Chrome で自動生成されたイメージとテキスト*</span><span class="sxs-lookup"><span data-stu-id="95afb-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-223">コードスニペットを追加すると、イメージがランダムに選択されるため、ブラウザーに表示されるイメージが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="95afb-224">ブラウザーを閉じないでください。</span><span class="sxs-lookup"><span data-stu-id="95afb-224">Do not close the browsers.</span></span> <span data-ttu-id="95afb-225">これらは、次のタスクで使用します。</span><span class="sxs-lookup"><span data-stu-id="95afb-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="95afb-226">タスク 3-スタイルプロパティの更新</span><span class="sxs-lookup"><span data-stu-id="95afb-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="95afb-227">このタスクでは、ブラウザーリンクの**検査モード**機能を使用して、特定の DOM 要素が生成される場所を正確に検出し、Web Essentials によって提供されるカラーピッカーを使用してその要素の color プロパティを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="95afb-228">Internet Explorer ブラウザーで、 **CTRL** + **ALT** + **I**キーを押して、検査モードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="95afb-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="95afb-229">薄い青の境界線の上にポインターを移動し、[] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="95afb-230">![薄い青の境界線の上にポインターを移動する](visual-studio-2013-web-tools/_static/image14.png "薄い青の境界線の上にポインターを移動する")</span><span class="sxs-lookup"><span data-stu-id="95afb-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="95afb-231">*薄い青の境界線の上にポインターを移動する*</span><span class="sxs-lookup"><span data-stu-id="95afb-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="95afb-232">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="95afb-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="95afb-233">Visual Studio HTML エディターで、ブラウザーで選択した HTML 要素も選択されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="95afb-234">![Visual Studio HTML エディターで選択された HTML 要素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML エディターで選択された HTML 要素")</span><span class="sxs-lookup"><span data-stu-id="95afb-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="95afb-235">*Visual Studio HTML エディターで選択された HTML 要素*</span><span class="sxs-lookup"><span data-stu-id="95afb-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="95afb-236">次に、選択した要素のスタイルを変更するために、 **front** CSS クラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="95afb-237">これを行うには 、CTRL \*\* + キーを押し\*\*て、 **[移動]** 検索ボックスを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="95afb-238">「 **Site .Css** 」と入力し、 **enter**キーを押してファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="95afb-239">![ファイルサイト .css を開いています](visual-studio-2013-web-tools/_static/image16.png "ファイルサイト .css を開いています")</span><span class="sxs-lookup"><span data-stu-id="95afb-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="95afb-240">*ファイルサイト .css を開いています*</span><span class="sxs-lookup"><span data-stu-id="95afb-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="95afb-241">**CTRL** + **F**キーを押し、「」と入力**し**て CSS セレクターを検索します。</span><span class="sxs-lookup"><span data-stu-id="95afb-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="95afb-242">クラスの [border] プロパティで薄い青色の四角をクリックして、カラーピッカーを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="95afb-243">![カラーピッカーを開く](visual-studio-2013-web-tools/_static/image17.png "カラーピッカーを開く")</span><span class="sxs-lookup"><span data-stu-id="95afb-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="95afb-244">*カラーピッカーを開く*</span><span class="sxs-lookup"><span data-stu-id="95afb-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="95afb-245">シェブロンボタンをクリックしてカラーピッカーを展開し、新しい色を選択します。</span><span class="sxs-lookup"><span data-stu-id="95afb-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="95afb-246">![カラーピッカーを展開する](visual-studio-2013-web-tools/_static/image18.png "カラーピッカーを展開する")</span><span class="sxs-lookup"><span data-stu-id="95afb-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="95afb-247">*カラーピッカーを展開する*</span><span class="sxs-lookup"><span data-stu-id="95afb-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="95afb-248">**CTRL** + **ALT** \*\* + 押して、\*\* リンクされたブラウザーを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="95afb-249">Internet Explorer に切り替えて、境界線の色がどのように変化したかを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="95afb-250">![Internet Explorer-境界線の色が更新されました](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-境界線の色が更新されました")</span><span class="sxs-lookup"><span data-stu-id="95afb-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="95afb-251">*Internet Explorer-境界線の色が更新されました*</span><span class="sxs-lookup"><span data-stu-id="95afb-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="95afb-252">Google Chrome に切り替え、境界線の色がどのように変化したかを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="95afb-253">![Google Chrome-更新された境界線の色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-更新された境界線の色")</span><span class="sxs-lookup"><span data-stu-id="95afb-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="95afb-254">*Google Chrome-更新された境界線の色*</span><span class="sxs-lookup"><span data-stu-id="95afb-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="95afb-255">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="95afb-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="95afb-256">**Btn**セレクターを見つけるには、**サイトの .css**ファイルの末尾に移動し、 **CTRL** + **F**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="95afb-257">**-Webkit**プロパティが緑色で下線が引かれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="95afb-258">![-webkit-btn selector の radius プロパティ](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn selector の radius プロパティ")</span><span class="sxs-lookup"><span data-stu-id="95afb-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="95afb-259">*-webkit-btn selector の radius プロパティ*</span><span class="sxs-lookup"><span data-stu-id="95afb-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="95afb-260">**-Webkit-radius**プロパティにカレットを置きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="95afb-261">プロパティの最初の単語の最初の文字の下に青い線が表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="95afb-262">これは**スマートタグ**です。</span><span class="sxs-lookup"><span data-stu-id="95afb-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="95afb-263">**Ctrl** + キーを押し**ます。**</span><span class="sxs-lookup"><span data-stu-id="95afb-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="95afb-264">[候補] メニューを開き、[**存在しない標準プロパティの追加] (罫線-半径)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="95afb-265">![不足している標準プロパティの追加の提案](visual-studio-2013-web-tools/_static/image22.png "不足している標準プロパティの追加の提案")</span><span class="sxs-lookup"><span data-stu-id="95afb-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="95afb-266">*不足している標準プロパティの追加の提案*</span><span class="sxs-lookup"><span data-stu-id="95afb-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="95afb-267">**境界線**のプロパティが CSS 規則に自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="95afb-268">![欠落した標準プロパティが追加されました](visual-studio-2013-web-tools/_static/image23.png "欠落した標準プロパティが追加されました")</span><span class="sxs-lookup"><span data-stu-id="95afb-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="95afb-269">*欠落した標準プロパティが追加されました*</span><span class="sxs-lookup"><span data-stu-id="95afb-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="95afb-270">**境界半径**プロパティの上にポインターを移動すると、**ブラウザーのマトリックスのツールヒント**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="95afb-271">**ブラウザーのマトリックスのツールヒント**には、各ブラウザーでプロパティが利用可能かどうかが表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="95afb-272">![ブラウザーマトリックスのツールヒント](visual-studio-2013-web-tools/_static/image24.png "ブラウザーマトリックスのツールヒント")</span><span class="sxs-lookup"><span data-stu-id="95afb-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="95afb-273">*ブラウザーマトリックスのツールヒント*</span><span class="sxs-lookup"><span data-stu-id="95afb-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="95afb-274">**Border-radius**プロパティの値に下線が表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="95afb-275">値の上にポインターを移動すると、警告メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="95afb-276">![罫線-radius プロパティ値-警告](visual-studio-2013-web-tools/_static/image25.png "罫線-radius プロパティ値-警告")</span><span class="sxs-lookup"><span data-stu-id="95afb-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="95afb-277">*罫線-radius プロパティ値-警告*</span><span class="sxs-lookup"><span data-stu-id="95afb-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="95afb-278">ツールヒントで提案されているように、**境界半径**プロパティ値の単位を削除します。</span><span class="sxs-lookup"><span data-stu-id="95afb-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="95afb-279">**境界線**として、丸みのある境界線の角を定義するための標準プロパティとして、 **-webkit-radius**プロパティと値を CSS 規則から削除できます。</span><span class="sxs-lookup"><span data-stu-id="95afb-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="95afb-280">**"ワードラップ**" プロパティにカレットを置き、スマートタグも下に表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="95afb-281">メニューを開き、[**不足**しているベンダの詳細の追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="95afb-282">![不足しているベンダーの詳細の提案の追加](visual-studio-2013-web-tools/_static/image26.png "不足しているベンダーの詳細の提案の追加")</span><span class="sxs-lookup"><span data-stu-id="95afb-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="95afb-283">*不足しているベンダーの詳細の提案の追加*</span><span class="sxs-lookup"><span data-stu-id="95afb-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="95afb-284">**-Ms-ワードラップ**プロパティは、CSS 規則に自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="95afb-285">![仕入先固有のプロパティの追加](visual-studio-2013-web-tools/_static/image27.png "仕入先固有のプロパティの追加")</span><span class="sxs-lookup"><span data-stu-id="95afb-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="95afb-286">*仕入先固有のプロパティの追加*</span><span class="sxs-lookup"><span data-stu-id="95afb-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="95afb-287">タスク 4-ブラウザーから HTML コードを更新する</span><span class="sxs-lookup"><span data-stu-id="95afb-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="95afb-288">このタスクでは、ブラウザーリンクの**デザインモード**機能を使用して、ブラウザーから DOM オブジェクトを編集し、Visual STUDIO の HTML ソースファイルに変更を転送します。</span><span class="sxs-lookup"><span data-stu-id="95afb-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="95afb-289">Google Chrome で、 **CTRL** + **ALT** + **D**キーを押してデザインモードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="95afb-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="95afb-290">**Lorem Ipsum dolor 座っ amet**ラベルの上にポインターを移動し、[] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="95afb-291">![質問の編集](visual-studio-2013-web-tools/_static/image28.png "質問の編集")</span><span class="sxs-lookup"><span data-stu-id="95afb-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="95afb-292">*質問の編集*</span><span class="sxs-lookup"><span data-stu-id="95afb-292">*Editing the question*</span></span>
3. <span data-ttu-id="95afb-293">カーソルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-293">A cursor should appear.</span></span> <span data-ttu-id="95afb-294">元のテキストを、*長い質問を書いたときに表示される内容*に置き換え、 **ESC**キーを押してデザインモードを終了します。</span><span class="sxs-lookup"><span data-stu-id="95afb-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="95afb-295">![編集した質問](visual-studio-2013-web-tools/_static/image29.png "編集した質問")</span><span class="sxs-lookup"><span data-stu-id="95afb-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="95afb-296">*編集した質問*</span><span class="sxs-lookup"><span data-stu-id="95afb-296">*Question edited*</span></span>
4. <span data-ttu-id="95afb-297">Visual Studio に戻り、(まだ開いていない場合は) **cshtml**を開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="95afb-298">**&lt;p&gt;** 要素の内部テキストが更新されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="95afb-299">![HTML ページで更新された質問](visual-studio-2013-web-tools/_static/image30.png "HTML ページで更新された質問")</span><span class="sxs-lookup"><span data-stu-id="95afb-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="95afb-300">*HTML ページで更新された質問*</span><span class="sxs-lookup"><span data-stu-id="95afb-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="95afb-301">タスク 5 - 変更履歴の SEO に関連する警告</span><span class="sxs-lookup"><span data-stu-id="95afb-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="95afb-302">**検索エンジンの最適化**(SEO) は、検索エンジンの結果の一覧で web サイトの順位を高くするプロセスです。</span><span class="sxs-lookup"><span data-stu-id="95afb-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="95afb-303">サイトの順位が高く、より一貫して一覧表示されていれば、その検索エンジンからサイトが取得する訪問者の数が増えます。</span><span class="sxs-lookup"><span data-stu-id="95afb-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="95afb-304">Web Essentials には、HTML を検査して検出された問題を報告し、それらを修正するためのサポートを提供する分析ツールが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="95afb-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="95afb-305">**[表示]** メニューにアクセスし、 **[エラー一覧]** をクリックして **[エラー一覧]** ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="95afb-306">![[表示] メニューのエラー一覧](visual-studio-2013-web-tools/_static/image31.png "[表示] メニューのエラー一覧")</span><span class="sxs-lookup"><span data-stu-id="95afb-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="95afb-307">*[表示] メニューのエラー一覧*</span><span class="sxs-lookup"><span data-stu-id="95afb-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="95afb-308">**&lt;メタ&gt;** タグがページの説明に含まれていないことを通知する SEO 警告が表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="95afb-309">SEO 警告エントリをダブルクリックして修正します。</span><span class="sxs-lookup"><span data-stu-id="95afb-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="95afb-310">![[エラー一覧] ウィンドウ](visual-studio-2013-web-tools/_static/image32.png "[エラー一覧] ウィンドウ")</span><span class="sxs-lookup"><span data-stu-id="95afb-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="95afb-311">*[エラー一覧] ウィンドウ*</span><span class="sxs-lookup"><span data-stu-id="95afb-311">*Error List window*</span></span>
3. <span data-ttu-id="95afb-312">**[Web Essentials]** ダイアログボックスで、 **[はい]** をクリックして説明 &lt;meta&gt; タグに挿入します。</span><span class="sxs-lookup"><span data-stu-id="95afb-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="95afb-313">![[Web Essentials] ダイアログボックス](visual-studio-2013-web-tools/_static/image33.png "[Web Essentials] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="95afb-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="95afb-314">*[Web Essentials] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="95afb-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="95afb-315">**\_Layout**のエディターが開き、 **&lt;meta&gt;** タグが HTML ファイルの**head**セクションに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="95afb-316">![_Layout ページに自動的に追加された Meta タグ](visual-studio-2013-web-tools/_static/image34.png "_Layout ページに自動的に追加された Meta タグ")</span><span class="sxs-lookup"><span data-stu-id="95afb-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="95afb-317">*\_レイアウトページに自動的に追加された Meta タグ*</span><span class="sxs-lookup"><span data-stu-id="95afb-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="95afb-318">**Content**属性の値を*GeekQuiz*に変更し、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="95afb-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="95afb-319">演習 2: コードスニペットと IntelliSense の活用</span><span class="sxs-lookup"><span data-stu-id="95afb-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="95afb-320">Web Essentials では、HTML エディターは追加機能を使用して拡張されています。</span><span class="sxs-lookup"><span data-stu-id="95afb-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="95afb-321">この演習では、web アプリケーションを開発する際に役立ついくつかの新機能について紹介します。</span><span class="sxs-lookup"><span data-stu-id="95afb-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="95afb-322">タスク 1-HTML ドキュメントでの IntelliSense の使用</span><span class="sxs-lookup"><span data-stu-id="95afb-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="95afb-323">このタスクに表示される最初の新機能は、**動的 IntelliSense**と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="95afb-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="95afb-324">動的 IntelliSense では、他のタグや属性を読み取って、使用する可能性のある id を推測します。</span><span class="sxs-lookup"><span data-stu-id="95afb-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="95afb-325">このタスクでは、ラベルと入力フィールドを含む新しい HTML フォーム要素を作成します。</span><span class="sxs-lookup"><span data-stu-id="95afb-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="95afb-326">次に、の属性をラベルに追加して入力にバインドします。これにより、スコープ内の入力の id に基づいて IntelliSense**の**候補が表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="95afb-327">**Web 用 Visual Studio Express 2013**を開き、 **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/begin**フォルダーにある**ソリューションを開きます。**</span><span class="sxs-lookup"><span data-stu-id="95afb-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="95afb-328">または、前の演習で取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="95afb-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="95afb-329">**ソリューションエクスプローラー**で、 **Views** | **ホーム**フォルダーにある**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="95afb-330">**&lt;section&gt;** 要素内に次のフォームを追加します。</span><span class="sxs-lookup"><span data-stu-id="95afb-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="95afb-331">(コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *フォーム*)</span><span class="sxs-lookup"><span data-stu-id="95afb-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="95afb-332">入力タグの前には、フィールドの説明を含むラベルを付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="95afb-333">入力タグの前に次のラベルを追加します。</span><span class="sxs-lookup"><span data-stu-id="95afb-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="95afb-334">ラベル**のバインド**先のフォーム要素を指定 **&gt;&lt;ラベル**の属性。</span><span class="sxs-lookup"><span data-stu-id="95afb-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="95afb-335">属性の値は、関連する要素の id と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="95afb-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="95afb-336">**&lt;label&gt;** 要素に**for**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="95afb-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="95afb-337">次の図に示すように、同じスコープ (外側の **&lt;フォーム&gt;** ) 内の要素の id に基づいて、[IntelliSense] ボックスに &quot;名&quot; 値がポップアップ表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="95afb-338">![IntelliSense で id を表示する](visual-studio-2013-web-tools/_static/image35.png "IntelliSense で id を表示する")</span><span class="sxs-lookup"><span data-stu-id="95afb-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="95afb-339">*IntelliSense で id を表示する*</span><span class="sxs-lookup"><span data-stu-id="95afb-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="95afb-340">最近追加された **&lt;フォーム&gt;** 要素とその内容を削除します。</span><span class="sxs-lookup"><span data-stu-id="95afb-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="95afb-341">タスク 2-HTML コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="95afb-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="95afb-342">HTML5 では、25個を超える新しいセマンティックタグが導入されました。</span><span class="sxs-lookup"><span data-stu-id="95afb-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="95afb-343">Visual Studio には既にこれらのタグの IntelliSense がサポートされていましたが、Visual Studio 2013 新しいコードスニペットを追加することにより、マークアップの記述が高速で簡単になります。</span><span class="sxs-lookup"><span data-stu-id="95afb-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="95afb-344">これらのタグは複雑ではありませんが、*オーディオ*タグに適切なコーデックフォールバックを追加するなど、若干の微妙な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="95afb-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="95afb-345">このタスクでは、オーディオタグの HTML コードスニペットを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="95afb-346">**Index. cshtml**ファイルで、次の図に示すように、 **&lt;セクション&gt;** 要素内に **&lt;aud**と入力します。</span><span class="sxs-lookup"><span data-stu-id="95afb-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="95afb-347">![オーディオ要素の挿入](visual-studio-2013-web-tools/_static/image36.png "オーディオ要素の挿入")</span><span class="sxs-lookup"><span data-stu-id="95afb-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="95afb-348">*オーディオ要素の挿入*</span><span class="sxs-lookup"><span data-stu-id="95afb-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="95afb-349">**Tab**キーを2回押して、ページに次のコードが追加され、カーソルが最初のソースの**src**属性に配置されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="95afb-350">**Tab**キーを2回押すと、コードスニペットが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="95afb-351">オーディオスニペットは、サポートを強化するために2つのソースファイルを使用して、*オーディオ*タグの標準的な使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="95afb-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="95afb-352">2行目を削除し、最初の行のソースを更新します。次のリンクを使用して、Webキャンプ Stv Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)にします。</span><span class="sxs-lookup"><span data-stu-id="95afb-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="95afb-353">結果のコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="95afb-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="95afb-354">ソースファイル*KatanaProject*が例として使用されています。</span><span class="sxs-lookup"><span data-stu-id="95afb-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="95afb-355">必要に応じて、別のソースを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="95afb-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="95afb-356">**Ctrl** + **S**キーを押して、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="95afb-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="95afb-357">**CTRL** + **F5**キーを押してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="95afb-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="95afb-358">オーディオプレーヤーがアプリケーションに追加されたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="95afb-359">![Internet Explorer のオーディオプレーヤー](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer のオーディオプレーヤー")</span><span class="sxs-lookup"><span data-stu-id="95afb-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="95afb-360">*Internet Explorer のオーディオプレーヤー*</span><span class="sxs-lookup"><span data-stu-id="95afb-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="95afb-361">![Google Chrome のオーディオプレーヤー](visual-studio-2013-web-tools/_static/image38.png "Google Chrome のオーディオプレーヤー")</span><span class="sxs-lookup"><span data-stu-id="95afb-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="95afb-362">*Google Chrome のオーディオプレーヤー*</span><span class="sxs-lookup"><span data-stu-id="95afb-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="95afb-363">ブラウザーを閉じないでください。</span><span class="sxs-lookup"><span data-stu-id="95afb-363">Do not close the browsers.</span></span> <span data-ttu-id="95afb-364">これらは、次のタスクで使用します。</span><span class="sxs-lookup"><span data-stu-id="95afb-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="95afb-365">タスク 3-JavaScript ドキュメントでの IntelliSense の使用</span><span class="sxs-lookup"><span data-stu-id="95afb-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="95afb-366">Web Essentials 2013 では、スタイルシートと HTML ページによって、Id とクラス名の一覧が生成されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="95afb-367">このタスクでは、Web Essentials 2013 での JavaScript IntelliSense のサポートを向上させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="95afb-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="95afb-368">**Index. cshtml**ファイルに次のコードを追加して、JavaScript コードの**スクリプト**タグを定義します。</span><span class="sxs-lookup"><span data-stu-id="95afb-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="95afb-369">**スクリプト**タグ内に次のコードを追加して、準備完了のコールバック関数を定義します。</span><span class="sxs-lookup"><span data-stu-id="95afb-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="95afb-370">(コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span><span class="sxs-lookup"><span data-stu-id="95afb-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="95afb-371">**スクリプト**タグにカレットを置き、 **ctrl** + キーを押し**ます。**</span><span class="sxs-lookup"><span data-stu-id="95afb-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="95afb-372">を開き、[候補] メニューを開きます。</span><span class="sxs-lookup"><span data-stu-id="95afb-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="95afb-373">[ **Extract To File] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="95afb-374">![JavaScript によるファイルへの抽出の提案](visual-studio-2013-web-tools/_static/image39.png "JavaScript によるファイルへの抽出の提案")</span><span class="sxs-lookup"><span data-stu-id="95afb-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="95afb-375">*JavaScript によるファイルへの抽出の提案*</span><span class="sxs-lookup"><span data-stu-id="95afb-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="95afb-376">**[名前を付けて保存]** ウィンドウで**Scripts**フォルダーを選択し、ファイルに「 **init** 」という名前を付けて、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="95afb-377">![ウィンドウとして保存](visual-studio-2013-web-tools/_static/image40.png "ウィンドウとして保存")</span><span class="sxs-lookup"><span data-stu-id="95afb-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="95afb-378">*ウィンドウとして保存*</span><span class="sxs-lookup"><span data-stu-id="95afb-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-379">この場合、**初期化**ファイルが作成され、スクリプトの内容がファイルに移動されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="95afb-380">![含まれているコンテンツを使用して作成された初期化 .js ファイル](visual-studio-2013-web-tools/_static/image41.png "含まれているコンテンツを使用して作成された初期化 .js ファイル")</span><span class="sxs-lookup"><span data-stu-id="95afb-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="95afb-381">*含まれているコンテンツを使用して作成された初期化 .js ファイル*</span><span class="sxs-lookup"><span data-stu-id="95afb-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="95afb-382">インデックスの**cshtml**ファイルを開き、スクリプトタグが**初期化**ファイルへの参照に置き換えられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="95afb-383">![Js html リファレンス](visual-studio-2013-web-tools/_static/image42.png "Js html リファレンス")</span><span class="sxs-lookup"><span data-stu-id="95afb-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="95afb-384">*Js html リファレンス*</span><span class="sxs-lookup"><span data-stu-id="95afb-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="95afb-385">**ソリューションエクスプローラー**にアクセスして、ソリューションに**初期化**ファイルが自動的に含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="95afb-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="95afb-386">![ソリューションに含まれている初期 .js ファイル](visual-studio-2013-web-tools/_static/image43.png "ソリューションに含まれている初期 .js ファイル")</span><span class="sxs-lookup"><span data-stu-id="95afb-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="95afb-387">*ソリューションに含まれている初期 .js ファイル*</span><span class="sxs-lookup"><span data-stu-id="95afb-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="95afb-388">**Init**ファイルに戻り、**準備ができ**ている関数のコールバックを更新します。</span><span class="sxs-lookup"><span data-stu-id="95afb-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="95afb-389">*準備完了*に渡される関数コールバック定義内で、次のコードを追加して、特定のクラス属性によってすべての要素を取得します。</span><span class="sxs-lookup"><span data-stu-id="95afb-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="95afb-390">**GetElementsByClassName**関数呼び出し内の引用符の間に、 **ctrl** + **Space**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="95afb-391">![GetElementsByClassName 関数の IntelliSense を表示する](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName 関数の IntelliSense を表示する")</span><span class="sxs-lookup"><span data-stu-id="95afb-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="95afb-392">*GetElementsByClassName 関数の IntelliSense を表示する*</span><span class="sxs-lookup"><span data-stu-id="95afb-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-393">IntelliSense により、プロジェクトのスタイルシートで定義されているクラスが表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95afb-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="95afb-394">作成した行を次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="95afb-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="95afb-395">**GetElementsByTagName**関数の引用符内に、 **au**の後にカーソルを置き、 **ctrl** + **Space**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="95afb-396">![GetElementByTagName メソッドの IntelliSense を表示する](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName メソッドの IntelliSense を表示する")</span><span class="sxs-lookup"><span data-stu-id="95afb-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="95afb-397">*GetElementsByTagName メソッドの IntelliSense を表示する*</span><span class="sxs-lookup"><span data-stu-id="95afb-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="95afb-398">一覧から [ **&quot;audio&quot;** ] を選択し、 **enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="95afb-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="95afb-399">結果を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="95afb-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="95afb-400">![取得 (オーディオ要素を)](visual-studio-2013-web-tools/_static/image46.png "取得 (オーディオ要素を)")</span><span class="sxs-lookup"><span data-stu-id="95afb-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="95afb-401">*取得 (オーディオ要素を)*</span><span class="sxs-lookup"><span data-stu-id="95afb-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="95afb-402">**ソリューションエクスプローラー**で、 **Scripts**フォルダー内の**init**ファイルを右クリックして、 **[Web Essentials]** メニューの **[minify JavaScript ファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95afb-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="95afb-403">![JavaScript ファイルをミニする](visual-studio-2013-web-tools/_static/image47.png "JavaScript ファイルをミニにする")</span><span class="sxs-lookup"><span data-stu-id="95afb-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="95afb-404">*JavaScript ファイルをミニする*</span><span class="sxs-lookup"><span data-stu-id="95afb-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="95afb-405">ソースファイルの変更時に自動縮小を有効にするように求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="95afb-406">![自動縮小の警告を有効にする](visual-studio-2013-web-tools/_static/image48.png "自動縮小の警告を有効にする")</span><span class="sxs-lookup"><span data-stu-id="95afb-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="95afb-407">*自動縮小の警告を有効にする*</span><span class="sxs-lookup"><span data-stu-id="95afb-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="95afb-408">初期化された **.js** **ファイルの**依存関係として追加されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="95afb-409">![作成された、最小の .js ファイル](visual-studio-2013-web-tools/_static/image49.png "作成された、最小の .js ファイル")</span><span class="sxs-lookup"><span data-stu-id="95afb-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="95afb-410">*作成された、最小の .js ファイル*</span><span class="sxs-lookup"><span data-stu-id="95afb-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="95afb-411">ファイルが縮小されていることを確認**します。**</span><span class="sxs-lookup"><span data-stu-id="95afb-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="95afb-412">![.Js ファイルの内容を初期化します。](visual-studio-2013-web-tools/_static/image50.png ".Js ファイルの内容を初期化します。")</span><span class="sxs-lookup"><span data-stu-id="95afb-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="95afb-413">*.Js ファイルの内容を初期化します。*</span><span class="sxs-lookup"><span data-stu-id="95afb-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="95afb-414">**GetElementsByTagName**関数の呼び出しの下に次のコードを**追加して**、すべてのオーディオ要素を再生します。</span><span class="sxs-lookup"><span data-stu-id="95afb-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="95afb-415">(コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *playaudioelements*)</span><span class="sxs-lookup"><span data-stu-id="95afb-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="95afb-416">CTRL + **S** **キーを押し**て、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="95afb-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="95afb-417">縮小表示ファイルは既に開かれているため、ファイルがソースエディターの外部で変更されたことを示すダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="95afb-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="95afb-418">**[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-418">Click **Yes**.</span></span>

    <span data-ttu-id="95afb-419">![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="95afb-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="95afb-420">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="95afb-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="95afb-421">新しいコードでファイルが更新されたことを確認するために、**初期の .js**ファイルに戻ります。</span><span class="sxs-lookup"><span data-stu-id="95afb-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="95afb-422">![初期の .js ファイルの更新](visual-studio-2013-web-tools/_static/image52.png "初期の .js ファイルの更新")</span><span class="sxs-lookup"><span data-stu-id="95afb-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="95afb-423">*初期の .js ファイルの更新*</span><span class="sxs-lookup"><span data-stu-id="95afb-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="95afb-424">ブラウザーの**リンク**の [更新] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95afb-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="95afb-425">両方のブラウザーが更新されると、前のタスクで表示されたオーディオプレーヤーが自動的に再生を開始します。</span><span class="sxs-lookup"><span data-stu-id="95afb-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="95afb-426">![オーディオプレーヤーがビューに含まれる](visual-studio-2013-web-tools/_static/image53.png "オーディオプレーヤーがビューに含まれる")</span><span class="sxs-lookup"><span data-stu-id="95afb-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="95afb-427">*オーディオプレーヤーがビューに含まれる*</span><span class="sxs-lookup"><span data-stu-id="95afb-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="95afb-428">まとめ</span><span class="sxs-lookup"><span data-stu-id="95afb-428">Summary</span></span>

<span data-ttu-id="95afb-429">このハンズオンラボを完了することで、次の方法を学習できました。</span><span class="sxs-lookup"><span data-stu-id="95afb-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="95afb-430">豊富な HTML5 コードスニペットや Zen コーディングなど、Web Essentials に含まれる新しい HTML エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="95afb-431">カラーピッカーやブラウザーマトリックスのツールヒントなど、Web Essentials に含まれる新しい CSS エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="95afb-432">すべての HTML 要素のファイルや IntelliSense の抽出など、Web Essentials に含まれる新しい JavaScript エディター機能を使用する</span><span class="sxs-lookup"><span data-stu-id="95afb-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="95afb-433">ブラウザーリンクを使用してブラウザーと Visual Studio の間でデータを交換する</span><span class="sxs-lookup"><span data-stu-id="95afb-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
