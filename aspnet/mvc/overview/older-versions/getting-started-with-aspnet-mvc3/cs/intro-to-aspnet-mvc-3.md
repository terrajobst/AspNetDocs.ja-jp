---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) の概要 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434728"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="eb422-103">ASP.NET MVC 3 (C#) の概要</span><span class="sxs-lookup"><span data-stu-id="eb422-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="eb422-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="eb422-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="eb422-105">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="eb422-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="eb422-106">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="eb422-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="eb422-107">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="eb422-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="eb422-108">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="eb422-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="eb422-109">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="eb422-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="eb422-110">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="eb422-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="eb422-111">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="eb422-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="eb422-112">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="eb422-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="eb422-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="eb422-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="eb422-114">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="eb422-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="eb422-115">このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="eb422-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="eb422-116">[バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="eb422-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="eb422-117">Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。</span><span class="sxs-lookup"><span data-stu-id="eb422-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="eb422-118">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="eb422-118">What You'll Build</span></span>

<span data-ttu-id="eb422-119">データベースからのムービーの作成、編集、および一覧表示をサポートする単純なムービーリスティングアプリケーションを実装します。</span><span class="sxs-lookup"><span data-stu-id="eb422-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="eb422-120">ビルドするアプリケーションの2つのスクリーンショットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="eb422-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="eb422-121">これには、データベースからムービーの一覧を表示するページが含まれています。</span><span class="sxs-lookup"><span data-stu-id="eb422-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="eb422-123">また、このアプリケーションでは、ムービーの追加、編集、削除を行うことができます。また、個々のムービーの詳細も確認できます。</span><span class="sxs-lookup"><span data-stu-id="eb422-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="eb422-124">すべてのデータ入力シナリオには、データベースに格納されているデータが正しいことを確認するための検証が含まれます。</span><span class="sxs-lookup"><span data-stu-id="eb422-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="eb422-125">学習内容</span><span class="sxs-lookup"><span data-stu-id="eb422-125">Skills You'll Learn</span></span>

<span data-ttu-id="eb422-126">ここでは次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="eb422-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="eb422-127">新しい ASP.NET MVC プロジェクトを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="eb422-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="eb422-128">ASP.NET MVC コントローラーとビューを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="eb422-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="eb422-129">Entity Framework Code First パラダイムを使用して新しいデータベースを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="eb422-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="eb422-130">データを取得および表示する方法。</span><span class="sxs-lookup"><span data-stu-id="eb422-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="eb422-131">データを編集し、データの検証を有効にする方法。</span><span class="sxs-lookup"><span data-stu-id="eb422-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eb422-132">作業の開始</span><span class="sxs-lookup"><span data-stu-id="eb422-132">Getting Started</span></span>

<span data-ttu-id="eb422-133">まず、Visual Web Developer 2010 Express ("Visual Web Developer" for short) を実行し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb422-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="eb422-134">Visual Web Developer は、IDE または統合開発環境です。</span><span class="sxs-lookup"><span data-stu-id="eb422-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="eb422-135">Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="eb422-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="eb422-136">Visual Web Developer には、さまざまなオプションが表示されているツールバーが上部にあります。</span><span class="sxs-lookup"><span data-stu-id="eb422-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="eb422-137">IDE でタスクを実行する別の方法を提供するメニューもあります。</span><span class="sxs-lookup"><span data-stu-id="eb422-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="eb422-138">(たとえば、**スタート**ページで **[新しいプロジェクト]** を選択する代わりに、メニューを使用して [**ファイル**&gt;**新しいプロジェクト**] を選択できます)。</span><span class="sxs-lookup"><span data-stu-id="eb422-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="eb422-139">最初のアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="eb422-139">Creating Your First Application</span></span>

<span data-ttu-id="eb422-140">プログラミング言語として Visual Basic または Visual C# を使用してアプリケーションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="eb422-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="eb422-141">左側にC#ある ビジュアル を選択し、 **ASP.NET MVC 3 Web アプリケーション** を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb422-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="eb422-142">プロジェクトに "MvcMovie" という名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eb422-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="eb422-143">(Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。)</span><span class="sxs-lookup"><span data-stu-id="eb422-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="eb422-144">**[New ASP.NET MVC 3 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb422-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="eb422-145">**[HTML5 マークアップを使用する]** チェックボックスをオンにして、既定のビューエンジンとして**Razor**を残します。</span><span class="sxs-lookup"><span data-stu-id="eb422-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="eb422-146">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eb422-146">Click **OK**.</span></span> <span data-ttu-id="eb422-147">Visual Web Developer では、作成した ASP.NET MVC プロジェクトの既定のテンプレートを使用しています。これにより、何も実行することなく、すぐに動作するアプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="eb422-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="eb422-148">これは単純な "Hello World!" です。</span><span class="sxs-lookup"><span data-stu-id="eb422-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="eb422-149">プロジェクトは、アプリケーションを起動するのに適した場所です。</span><span class="sxs-lookup"><span data-stu-id="eb422-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="eb422-150">**[デバッグ]** メニューの **[デバッグの開始]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eb422-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="eb422-151">デバッグを開始するためのキーボードショートカットが F5 キーになっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eb422-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="eb422-152">F5 キーを押すと、Visual Web Developer によって開発 web サーバーが起動され、web アプリケーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="eb422-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="eb422-153">その後、Visual Web Developer がブラウザーを起動し、アプリケーションのホームページを開きます。</span><span class="sxs-lookup"><span data-stu-id="eb422-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="eb422-154">ブラウザーのアドレスバーには `localhost` が表示され、`example.com`のようなものではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eb422-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="eb422-155">これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。</span><span class="sxs-lookup"><span data-stu-id="eb422-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="eb422-156">Visual Web Developer で web プロジェクトを実行する場合、web サーバーにはランダムなポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="eb422-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="eb422-157">次の図では、ランダムポート番号は43246です。</span><span class="sxs-lookup"><span data-stu-id="eb422-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="eb422-158">アプリケーションを実行すると、別のポート番号が表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="eb422-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="eb422-159">すぐに使用できる既定のテンプレートでは、2つのページにアクセスでき、基本ログインページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="eb422-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="eb422-160">次の手順では、このアプリケーションの動作を変更し、プロセスでの ASP.NET MVC について少し説明します。</span><span class="sxs-lookup"><span data-stu-id="eb422-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="eb422-161">ブラウザーを閉じて、コードを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="eb422-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="eb422-162">Next</span><span class="sxs-lookup"><span data-stu-id="eb422-162">Next</span></span>](adding-a-controller.md)
