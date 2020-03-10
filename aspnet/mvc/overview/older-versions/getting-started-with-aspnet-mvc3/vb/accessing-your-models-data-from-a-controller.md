---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498658"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="70032-103">コントローラーからモデルのデータにアクセスする (VB)</span><span class="sxs-lookup"><span data-stu-id="70032-103">Accessing your Model's Data from a Controller (VB)</span></span>

<span data-ttu-id="70032-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="70032-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="70032-105">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="70032-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="70032-106">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="70032-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="70032-107">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="70032-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="70032-108">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="70032-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="70032-109">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="70032-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="70032-110">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="70032-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="70032-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="70032-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="70032-112">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="70032-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="70032-113">このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="70032-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="70032-114">[VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="70032-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="70032-115">必要に応じC#て[ C# ](../cs/accessing-your-models-data-from-a-controller.md) 、このチュートリアルのバージョンに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="70032-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="70032-116">このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="70032-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="70032-117">続行する前に、アプリケーションをビルドしてください。</span><span class="sxs-lookup"><span data-stu-id="70032-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="70032-118">*Controllers*フォルダーを右クリックし、新しい `MoviesController` コントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="70032-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="70032-119">次のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="70032-119">Select the following options:</span></span>

- <span data-ttu-id="70032-120">コントローラー名: **moviescontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="70032-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="70032-121">(これが既定値です)。</span><span class="sxs-lookup"><span data-stu-id="70032-121">(This is the default.)</span></span>
- <span data-ttu-id="70032-122">テンプレート: **Entity Framework を使用した、読み取り/書き込みアクションとビューを備えたコントローラー**。</span><span class="sxs-lookup"><span data-stu-id="70032-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="70032-123">モデルクラス: **Movie (MvcMovie. model)** 。</span><span class="sxs-lookup"><span data-stu-id="70032-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="70032-124">データコンテキストクラス: **moの Dbcontext (MvcMovie. model)** 。</span><span class="sxs-lookup"><span data-stu-id="70032-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="70032-125">Views: **Razor (CSHTML)** 。</span><span class="sxs-lookup"><span data-stu-id="70032-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="70032-126">(既定値)。</span><span class="sxs-lookup"><span data-stu-id="70032-126">(The default.)</span></span>

<span data-ttu-id="70032-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="70032-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="70032-128">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="70032-128">Click **Add**.</span></span> <span data-ttu-id="70032-129">Visual Web Developer では、次のファイルとフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="70032-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="70032-130">プロジェクトの*Controllers*フォルダー内の*moviescontroller.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="70032-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="70032-131">プロジェクトの*Views*フォルダー内の*ムービー*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="70032-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="70032-132">新しい*Views\Movies*フォルダーで、Vbhtml を作成し、 *vbhtml、Details*、Vbhtml、および*を削除します*。</span><span class="sxs-lookup"><span data-stu-id="70032-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="70032-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="70032-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="70032-134">ASP.NET MVC 3 スキャフォールディング機構により、CRUD (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="70032-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="70032-135">これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="70032-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="70032-136">アプリケーションを実行し、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します。</span><span class="sxs-lookup"><span data-stu-id="70032-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="70032-137">アプリケーションは既定のルーティング ( *global.asax*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、`Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="70032-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="70032-138">つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。</span><span class="sxs-lookup"><span data-stu-id="70032-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="70032-139">まだ追加していないため、結果はムービーの空の一覧になります。</span><span class="sxs-lookup"><span data-stu-id="70032-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="70032-140">ムービーの作成</span><span class="sxs-lookup"><span data-stu-id="70032-140">Creating a Movie</span></span>

<span data-ttu-id="70032-141">**[Create New]\(新規作成\)** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="70032-141">Select the **Create New** link.</span></span> <span data-ttu-id="70032-142">ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="70032-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="70032-143">**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="70032-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="70032-144">次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。</span><span class="sxs-lookup"><span data-stu-id="70032-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="70032-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="70032-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="70032-146">いくつかのムービー エントリを作成します。</span><span class="sxs-lookup"><span data-stu-id="70032-146">Create a couple more movie entries.</span></span> <span data-ttu-id="70032-147">**[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。</span><span class="sxs-lookup"><span data-stu-id="70032-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="70032-148">生成されたコードの調査</span><span class="sxs-lookup"><span data-stu-id="70032-148">Examining the Generated Code</span></span>

<span data-ttu-id="70032-149">*Controllers\MoviesController.vb*ファイルを開き、生成された `Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="70032-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="70032-150">`Index` メソッドを使用したムービーコントローラーの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="70032-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="70032-151">前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="70032-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="70032-152">ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="70032-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="70032-153">`Movies` コントローラーに対する要求では、ムービーデータベースの `Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="70032-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="70032-154">厳密に型指定されたモデルと @model キーワード</span><span class="sxs-lookup"><span data-stu-id="70032-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="70032-155">このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="70032-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="70032-156">`ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="70032-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="70032-157">また、ASP.NET MVC では、厳密に型指定されたデータまたはオブジェクトをビューテンプレートに渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="70032-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="70032-158">この厳密に型指定されたアプローチによって、Visual Web Developer エディターでのコードのコンパイル時チェックと IntelliSense の強化が可能になります。</span><span class="sxs-lookup"><span data-stu-id="70032-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="70032-159">ここでは、`MoviesController` クラスと*インデックスの vbhtml*ビューテンプレートでこの方法を使用しています。</span><span class="sxs-lookup"><span data-stu-id="70032-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="70032-160">`Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="70032-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="70032-161">次に、コードはこの `Movies` リストをコントローラーからビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="70032-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="70032-162">ビューテンプレートファイルの先頭に `@ModelType` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。</span><span class="sxs-lookup"><span data-stu-id="70032-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="70032-163">ムービーコントローラーを作成したときに、Visual Web Developer によって、次の `@model` ステートメントが*インデックスの vbhtml*ファイルの先頭に自動的に追加されました。</span><span class="sxs-lookup"><span data-stu-id="70032-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="70032-164">この `@ModelType` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="70032-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="70032-165">たとえば、*インデックスの vbhtml*テンプレートでは、コードは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。</span><span class="sxs-lookup"><span data-stu-id="70032-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="70032-166">`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。</span><span class="sxs-lookup"><span data-stu-id="70032-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="70032-167">その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="70032-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="70032-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="70032-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="70032-169">SQL Server Compact の操作</span><span class="sxs-lookup"><span data-stu-id="70032-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="70032-170">Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="70032-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="70032-171">これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="70032-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="70032-172">*ムービーの .sdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、 **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="70032-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="70032-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="70032-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="70032-174">[*ムービー. .sdf* ] をダブルクリックして、**サーバーエクスプローラー**を開きます。</span><span class="sxs-lookup"><span data-stu-id="70032-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="70032-175">次に、 **[テーブル]** フォルダーを展開して、データベースに作成されたテーブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="70032-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="70032-176">[ *.Sdf*] をダブルクリックしたときにエラーが表示された場合は、 **SQL Server Compact 4.0 用の VISUAL Studio 2010 SP1 ツール**がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="70032-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="70032-177">(本ソフトウェアのリンクについては、このチュートリアルシリーズのパート1の前提条件の一覧を参照してください)。今すぐリリースをインストールする場合は、Visual Web Developer を閉じてから再度開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="70032-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>

<span data-ttu-id="70032-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="70032-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="70032-179">2つのテーブルがあります。1つは `Movie` エンティティセット用、もう1つは `EdmMetadata` テーブルです。</span><span class="sxs-lookup"><span data-stu-id="70032-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="70032-180">`EdmMetadata` テーブルは、モデルとデータベースが同期されていないことを判断するために Entity Framework によって使用されます。</span><span class="sxs-lookup"><span data-stu-id="70032-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="70032-181">`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="70032-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="70032-182">[![Moの安定](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="70032-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="70032-183">`Movies` テーブルを右クリックし、 **[テーブルスキーマの編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="70032-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="70032-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="70032-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="70032-186">`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。</span><span class="sxs-lookup"><span data-stu-id="70032-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="70032-187">このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。</span><span class="sxs-lookup"><span data-stu-id="70032-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="70032-188">終了したら、接続を閉じます。</span><span class="sxs-lookup"><span data-stu-id="70032-188">When you're finished, close the connection.</span></span> <span data-ttu-id="70032-189">(接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。</span><span class="sxs-lookup"><span data-stu-id="70032-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="70032-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="70032-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="70032-191">これで、データベースと、そのコンテンツを表示する単純なリストページが作成されました。</span><span class="sxs-lookup"><span data-stu-id="70032-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="70032-192">次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="70032-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="70032-193">[前へ](adding-a-model.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="70032-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
