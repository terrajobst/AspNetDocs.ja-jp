---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434488"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="d4d3f-104">コントローラーからモデルのデータにアクセスする</span><span class="sxs-lookup"><span data-stu-id="d4d3f-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="d4d3f-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d4d3f-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="d4d3f-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="d4d3f-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="d4d3f-108">このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="d4d3f-109">次の手順に進む前に **、アプリケーションをビルドし**ます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="d4d3f-110">*Controllers*フォルダーを右クリックし、新しい `MoviesController` コントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="d4d3f-111">以下のオプションは、アプリケーションをビルドするまで表示されません。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="d4d3f-112">次のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-112">Select the following options:</span></span>

- <span data-ttu-id="d4d3f-113">コントローラー名: **moviescontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="d4d3f-114">(これが既定値です。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-114">(This is the default.</span></span> <span data-ttu-id="d4d3f-115">)</span><span class="sxs-lookup"><span data-stu-id="d4d3f-115">)</span></span>
- <span data-ttu-id="d4d3f-116">テンプレート: **Entity Framework を使用した、読み取り/書き込みアクションとビューがある MVC コントローラー**。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="d4d3f-117">モデルクラス: **Movie (MvcMovie. model)** 。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="d4d3f-118">データコンテキストクラス: **moの Dbcontext (MvcMovie. model)** 。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="d4d3f-119">Views: **Razor (CSHTML)** 。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="d4d3f-120">(既定値)。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="d4d3f-122">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-122">Click **Add**.</span></span> <span data-ttu-id="d4d3f-123">Visual Studio Express によって、次のファイルとフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="d4d3f-124">プロジェクトの*Controllers*フォルダー内の*MoviesController.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="d4d3f-125">プロジェクトの*Views*フォルダー内の*ムービー*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="d4d3f-126">新しい*Views\Movies*フォルダーに、cshtml、Cshtml、 *Details、Edit.* cshtml、および*Index*を作成します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="d4d3f-127">ASP.NET MVC 4 では、CRUD (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されました (CRUD アクションメソッドとビューの自動作成はスキャフォールディングと呼ばれています)。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="d4d3f-128">これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="d4d3f-129">アプリケーションを実行し、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="d4d3f-130">アプリケーションは既定のルーティング ( *global.asax*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、`Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="d4d3f-131">つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="d4d3f-132">まだ追加していないため、結果はムービーの空の一覧になります。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="d4d3f-133">ムービーの作成</span><span class="sxs-lookup"><span data-stu-id="d4d3f-133">Creating a Movie</span></span>

<span data-ttu-id="d4d3f-134">**[Create New]\(新規作成\)** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-134">Select the **Create New** link.</span></span> <span data-ttu-id="d4d3f-135">ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="d4d3f-136">**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="d4d3f-137">次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="d4d3f-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="d4d3f-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="d4d3f-139">いくつかのムービー エントリを作成します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-139">Create a couple more movie entries.</span></span> <span data-ttu-id="d4d3f-140">**[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="d4d3f-141">生成されたコードの調査</span><span class="sxs-lookup"><span data-stu-id="d4d3f-141">Examining the Generated Code</span></span>

<span data-ttu-id="d4d3f-142">*Controllers\MoviesController.cs*ファイルを開き、生成された `Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="d4d3f-143">`Index` メソッドを使用したムービーコントローラーの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="d4d3f-144">前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="d4d3f-145">ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="d4d3f-146">`Movies` コントローラーに対する要求では、ムービーデータベースの `Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="d4d3f-147">厳密に型指定されたモデルと @model キーワード</span><span class="sxs-lookup"><span data-stu-id="d4d3f-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="d4d3f-148">このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="d4d3f-149">`ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="d4d3f-150">また、ASP.NET MVC では、厳密に型指定されたデータまたはオブジェクトをビューテンプレートに渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="d4d3f-151">この厳密に型指定されたアプローチによって、Visual Studio エディターでのコードのコンパイル時のチェックと、より高度な IntelliSense が有効になります。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="d4d3f-152">Visual Studio のスキャフォールディングメカニズムでは、メソッドとビューを作成するときに、`MoviesController` クラスとビューテンプレートでこの方法を使用しました。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="d4d3f-153">*Controllers\MoviesController.cs*ファイルで、生成された `Details` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="d4d3f-154">`Details` メソッドを使用したムービーコントローラーの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="d4d3f-155">`Movie` が見つかった場合は、`Movie` モデルのインスタンスが詳細ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="d4d3f-156">*Views\Movies\Details.cshtml*ファイルの内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="d4d3f-157">ビューテンプレートファイルの先頭に `@model` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="d4d3f-158">ムービー コントローラーを作成したとき、Visual Studio によって `@model`Details.cshtml*ファイルの先頭に* ステートメントが自動的に追加されています。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="d4d3f-159">この `@model` ディレクティブにより、厳密に型指定された `Model` オブジェクトを使って、コントローラーがビューに渡したムービーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="d4d3f-160">たとえば、 *Details. cshtml*テンプレートでは、コードは各ムービーフィールドを `DisplayNameFor` に渡し、厳密に型指定された `Model` オブジェクトを使用して HTML ヘルパー[を](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)表示します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="d4d3f-161">Create メソッドと Edit メソッドとビューテンプレートも、ムービーモデルオブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="d4d3f-162">*MoviesController.cs*ファイルで、*インデックスの cshtml*ビューテンプレートと `Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="d4d3f-163">`Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="d4d3f-164">次に、コードはこの `Movies` リストをコントローラーからビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="d4d3f-165">ムービーコントローラーを作成すると、Visual Studio Express によって、次の `@model` ステートメントが*Index. cshtml*ファイルの先頭に自動的に含まれます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="d4d3f-166">この `@model` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="d4d3f-167">たとえば、 *Index. cshtml*テンプレートでは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="d4d3f-168">`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="d4d3f-169">その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="d4d3f-171">SQL Server LocalDB の使用</span><span class="sxs-lookup"><span data-stu-id="d4d3f-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="d4d3f-172">Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="d4d3f-173">これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="d4d3f-174">*ムービーの .mdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、最新の情報に **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="d4d3f-175">[ *.Mdf* ] をダブルクリックして**データベースエクスプローラー**を開き、 **[テーブル]** フォルダーを展開して、ムービーテーブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="d4d3f-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="d4d3f-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="d4d3f-177">データベースエクスプローラーが表示されない場合は、 **[ツール]** メニューの **[データベースへの接続]** をクリックし、 **[データソースの選択]** ダイアログをキャンセルします。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="d4d3f-178">これにより、データベースエクスプローラーが強制的に開きます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="d4d3f-179">VWD または Visual Studio 2010 を使用していて、次のようなエラーが表示される場合:</span><span class="sxs-lookup"><span data-stu-id="d4d3f-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="d4d3f-180">データベース ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF ' はバージョン706であるため、開くことができません。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="d4d3f-181">このサーバーでは、バージョン655以前がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="d4d3f-182">このダウングレード パスはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="d4d3f-183">指定された SqlConnection が初期カタログを指定していない&quot;、&quot;InvalidOperation Exception がユーザーコードによって処理されませんでした。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="d4d3f-184">[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)と[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="d4d3f-185">前のページで指定した `MovieDBContext` 接続文字列を確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="d4d3f-186">`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="d4d3f-187">`Movies` テーブルを右クリックし、 **[テーブル定義を開く]** を選択して、Entity Framework 作成 Code First テーブルの構造を確認します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="d4d3f-188">`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="d4d3f-189">このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="d4d3f-190">操作が完了したら、 *Mo? Dbcontext*を右クリックし、 **[接続を閉じる]** を選択して接続を閉じます。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="d4d3f-191">(接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="d4d3f-192">これで、データベースと、そのコンテンツを表示する単純なリストページが作成されました。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="d4d3f-193">次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="d4d3f-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d4d3f-194">[前へ](adding-a-model.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="d4d3f-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
