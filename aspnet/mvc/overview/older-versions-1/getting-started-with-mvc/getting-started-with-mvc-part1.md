---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC の概要 |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469798"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="b8d1f-104">ASP.NET MVC 入門</span><span class="sxs-lookup"><span data-stu-id="b8d1f-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="b8d1f-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="b8d1f-106">このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="b8d1f-107">このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="b8d1f-108">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="b8d1f-109">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="b8d1f-110">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="b8d1f-111">[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)を使用して最初の ASP.NET MVC Web アプリケーションを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="b8d1f-112">ムービーの作成と一覧表示を行うための小さなムービーリストアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="b8d1f-113">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-113">What You'll Build</span></span>

<span data-ttu-id="b8d1f-114">ここでは、作成するアプリケーションの2つのスクリーンショットを示します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="b8d1f-115">さまざまな列を含む単純な映画のテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="b8d1f-116">[![ムービーの一覧-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="b8d1f-117">また、ムービーをリストに追加できるように、フォームが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="b8d1f-118">[![ムービーを作成する-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="b8d1f-119">学習内容</span><span class="sxs-lookup"><span data-stu-id="b8d1f-119">Skills You'll Learn</span></span>

<span data-ttu-id="b8d1f-120">このチュートリアルでは、Visual Studio を使用して ASP.NET MVC Web アプリケーションを構築する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="b8d1f-121">学習内容:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-121">You'll learn:</span></span>

- <span data-ttu-id="b8d1f-122">新しい ASP.NET MVC プロジェクトを作成する方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="b8d1f-123">SQL Server を使用して新しいデータベースを作成する方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="b8d1f-124">ASP.NET MVC コントローラーとビューを作成する方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="b8d1f-125">データを取得して表示する方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-125">How to retrieve and display data</span></span>
- <span data-ttu-id="b8d1f-126">データを編集し、データの検証を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="b8d1f-127">データベーススキーマを更新する方法</span><span class="sxs-lookup"><span data-stu-id="b8d1f-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="b8d1f-128">開始するには</span><span class="sxs-lookup"><span data-stu-id="b8d1f-128">Get Started</span></span>

<span data-ttu-id="b8d1f-129">まず、Visual Web Developer 2010 Express を実行します (ここでは "VWD" と呼ばれます)。スタート画面から [新しいプロジェクト] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="b8d1f-130">Visual Web Developer は、IDE または統合開発環境です。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="b8d1f-131">Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="b8d1f-132">上部には、使用可能なさまざまなオプションが表示されているツールバーがあります。また、[ファイル] を選択するために使用できるメニューもあります。新しいプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="b8d1f-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="b8d1f-134">最初のアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="b8d1f-134">Creating Your First Application</span></span>

<span data-ttu-id="b8d1f-135">Visual Basic または Visual C# を使用してアプリケーションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="b8d1f-136">ここで、選択 Visual C#、左側の「ASP.NET MVC 2 Web アプリケーション」を選択し、</span><span class="sxs-lookup"><span data-stu-id="b8d1f-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="b8d1f-137">プロジェクトに"Movies"という名前し、[ok] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="b8d1f-138">[新しいプロジェクトの ![](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="b8d1f-139">右側には、アプリケーション内のすべてのファイルとフォルダーが表示されるソリューションエクスプローラーます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="b8d1f-140">中央の大きなウィンドウでは、コードを編集し、ほとんどの時間を費やすことができます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="b8d1f-141">Visual Studio では、先ほど作成した ASP.NET MVC プロジェクトの既定のテンプレートが使用されているため、何もしなくても、すぐに動作するアプリケーションがあります。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="b8d1f-142">これは単純な "Hello World です。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-142">This is a simple "Hello World!</span></span> <span data-ttu-id="b8d1f-143">プロジェクトは、アプリケーションを開始するのに最適な場所です。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="b8d1f-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="b8d1f-145">ツールバーの [再生] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-145">Select the "play" button to the toolbar.</span></span>

![[デバッグ]](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="b8d1f-147">これは、プログラムをコンパイルし、web ブラウザーでアプリケーションを起動する、右側を指す緑色の矢印です。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="b8d1f-148">*注: 代わりに、キーボードの F5 キーを押すか、[デバッグ] メニューの [デバッグ] を選択して [デバッグ] を&gt;ます。*</span><span class="sxs-lookup"><span data-stu-id="b8d1f-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="b8d1f-149">これにより、Visual Web Developer は開発 web サーバーを起動し、web アプリケーションを実行します (これを有効にするために必要な構成や手動の手順はありません)。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="b8d1f-150">その後、ブラウザーが起動し、アプリケーションのホームページを参照するように構成されます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="b8d1f-151">以下のように、ブラウザーのアドレスバーには "localhost" と表示されており、example.com のようなものではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="b8d1f-152">これは、localhost は常に独自のローカルコンピューターを指しているためです。この場合、この例では、先ほど作成したアプリケーションが実行されています。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="b8d1f-153">[![ホームページ](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="b8d1f-154">すぐに使用できる既定のテンプレートでは、2つのページにアクセスでき、基本的なログインページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="b8d1f-155">このアプリケーションの動作を変更し、プロセスでの ASP.NET MVC について少し説明しましょう。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="b8d1f-156">ブラウザーを閉じ、コードを変更します。</span><span class="sxs-lookup"><span data-stu-id="b8d1f-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b8d1f-157">Next</span><span class="sxs-lookup"><span data-stu-id="b8d1f-157">Next</span></span>](getting-started-with-mvc-part2.md)
