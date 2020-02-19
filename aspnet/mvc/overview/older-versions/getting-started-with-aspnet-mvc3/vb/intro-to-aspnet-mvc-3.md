---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 の概要 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456330"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="4af88-103">ASP.NET MVC 3 入門 (VB)</span><span class="sxs-lookup"><span data-stu-id="4af88-103">Intro to ASP.NET MVC 3 (VB)</span></span>

<span data-ttu-id="4af88-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4af88-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="4af88-105">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="4af88-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="4af88-106">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="4af88-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="4af88-107">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4af88-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="4af88-108">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="4af88-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="4af88-109">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="4af88-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="4af88-110">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="4af88-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="4af88-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="4af88-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="4af88-112">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="4af88-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="4af88-113">このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="4af88-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="4af88-114">[VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="4af88-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="4af88-115">必要に応じC#て[ C# ](../cs/intro-to-aspnet-mvc-3.md) 、このチュートリアルのバージョンに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="4af88-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="4af88-116">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="4af88-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="4af88-117">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="4af88-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="4af88-118">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4af88-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="4af88-119">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="4af88-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="4af88-120">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="4af88-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="4af88-121">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="4af88-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="4af88-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="4af88-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="4af88-123">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="4af88-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="4af88-124">このトピックには、VB ソースコードを含む Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="4af88-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="4af88-125">[VB バージョンをこちらからダウンロードして](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)ください。</span><span class="sxs-lookup"><span data-stu-id="4af88-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="4af88-126">CSharp を使用する場合は、このチュートリアルの[csharp バージョン](../cs/intro-to-aspnet-mvc-3.md)に切り替えてください。</span><span class="sxs-lookup"><span data-stu-id="4af88-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="4af88-127">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="4af88-127">What You'll Build</span></span>

<span data-ttu-id="4af88-128">データベースからのムービーの作成、編集、および一覧表示をサポートする単純なムービーリスティングアプリケーションを実装します。</span><span class="sxs-lookup"><span data-stu-id="4af88-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="4af88-129">ビルドするアプリケーションの2つのスクリーンショットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4af88-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="4af88-130">これには、データベースからムービーの一覧を表示するページが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4af88-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="4af88-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4af88-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="4af88-132">また、このアプリケーションでは、ムービーの追加、編集、削除を行うことができます。また、個々のムービーの詳細も確認できます。</span><span class="sxs-lookup"><span data-stu-id="4af88-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="4af88-133">すべてのデータ入力シナリオには、データベースに格納されているデータが正しいことを確認するための検証が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4af88-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="4af88-134">[CreateFormSo の ![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4af88-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="4af88-135">学習内容</span><span class="sxs-lookup"><span data-stu-id="4af88-135">Skills You'll Learn</span></span>

<span data-ttu-id="4af88-136">ここでは次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="4af88-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="4af88-137">新しい ASP.NET MVC プロジェクトを作成する方法</span><span class="sxs-lookup"><span data-stu-id="4af88-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="4af88-138">Entity Framework code first を使用して新しいデータベースを作成する方法</span><span class="sxs-lookup"><span data-stu-id="4af88-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="4af88-139">ASP.NET MVC コントローラーとビューを作成する方法</span><span class="sxs-lookup"><span data-stu-id="4af88-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="4af88-140">データを取得して表示する方法</span><span class="sxs-lookup"><span data-stu-id="4af88-140">How to retrieve and display data</span></span>
- <span data-ttu-id="4af88-141">データを編集し、データの検証を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="4af88-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="4af88-142">作業の開始</span><span class="sxs-lookup"><span data-stu-id="4af88-142">Getting Started</span></span>

<span data-ttu-id="4af88-143">Visual Web Developer 2010 Express (短い場合は "VWD") を実行し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4af88-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="4af88-144">Visual Web Developer は、IDE または統合開発環境です。</span><span class="sxs-lookup"><span data-stu-id="4af88-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="4af88-145">Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4af88-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="4af88-146">Visual Web Developer には、さまざまなオプションが表示されているツールバーが上部にあります。</span><span class="sxs-lookup"><span data-stu-id="4af88-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="4af88-147">IDE でタスクを実行する別の方法を提供するメニューもあります。</span><span class="sxs-lookup"><span data-stu-id="4af88-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="4af88-148">(たとえば、**スタート**ページで **[新しいプロジェクト]** を選択する代わりに、メニューを使用して [**ファイル**&gt;**新しいプロジェクト**] を選択できます)。</span><span class="sxs-lookup"><span data-stu-id="4af88-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="4af88-149">最初のアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="4af88-149">Creating Your First Application</span></span>

<span data-ttu-id="4af88-150">プログラミング言語として Visual Basic またはビジュアルC#のいずれかを選択して、アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4af88-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="4af88-151">このチュートリアルでは、左側の Visual Basic を選択し、 **ASP.NET MVC 3 Web アプリケーション** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4af88-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="4af88-152">プロジェクトに "MvcMovie" という名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4af88-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="4af88-154">**[New ASP.NET MVC 3 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4af88-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="4af88-155">既定のビューエンジンとして**Razor**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="4af88-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="4af88-157">**[OK]** をクリックすると、</span><span class="sxs-lookup"><span data-stu-id="4af88-157">Click **OK**.</span></span> <span data-ttu-id="4af88-158">Visual Web Developer では、作成した ASP.NET MVC プロジェクトの既定のテンプレートを使用しています。これにより、何も実行することなく、すぐに動作するアプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="4af88-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="4af88-159">これは単純な "Hello World!" です。</span><span class="sxs-lookup"><span data-stu-id="4af88-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="4af88-160">プロジェクトは、アプリケーションを起動するのに適した場所です。</span><span class="sxs-lookup"><span data-stu-id="4af88-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="4af88-161">**[デバッグ]** メニューの **[デバッグの開始]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4af88-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="4af88-162">デバッグを開始するためのキーボードショートカットが F5 キーになっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4af88-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="4af88-163">F5 キーを押すと、Visual Web Developer によって開発 web サーバーが起動され、web アプリケーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="4af88-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="4af88-164">その後、VWD はブラウザーを起動し、アプリケーションのホームページを開きます。</span><span class="sxs-lookup"><span data-stu-id="4af88-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="4af88-165">ブラウザーのアドレスバーには `localhost` が表示され、`example.com`のようなものではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4af88-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="4af88-166">これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。</span><span class="sxs-lookup"><span data-stu-id="4af88-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="4af88-167">VWD で web プロジェクトを実行する場合、プロジェクトにはランダムなポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="4af88-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="4af88-168">次の図では、ランダムポート番号は43246です。</span><span class="sxs-lookup"><span data-stu-id="4af88-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="4af88-169">プロジェクトでは、別のポート番号を使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="4af88-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="4af88-170">すぐに使用できる既定のテンプレートでは、2つのページにアクセスでき、基本的なログインページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4af88-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="4af88-171">このアプリケーションの動作を変更し、プロセスでの ASP.NET MVC について少し説明しましょう。</span><span class="sxs-lookup"><span data-stu-id="4af88-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="4af88-172">ブラウザーを閉じて、コードを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4af88-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4af88-173">Next</span><span class="sxs-lookup"><span data-stu-id="4af88-173">Next</span></span>](adding-a-controller.md)
