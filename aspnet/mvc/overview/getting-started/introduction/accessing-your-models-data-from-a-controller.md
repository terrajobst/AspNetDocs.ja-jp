---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5d882d765133d32d3acdba9ffb5d43b69119a273
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499228"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="465cd-102">コントローラーからモデルのデータにアクセスする</span><span class="sxs-lookup"><span data-stu-id="465cd-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="465cd-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="465cd-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="465cd-104">このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="465cd-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="465cd-105">次の手順に進む前に **、アプリケーションをビルドし**ます。</span><span class="sxs-lookup"><span data-stu-id="465cd-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="465cd-106">アプリケーションをビルドしないと、コントローラーを追加するときにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="465cd-107">ソリューションエクスプローラーで、 *Controllers*フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="465cd-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="465cd-108">**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 Controller with views]** をクリックし、Entity Framework をクリックして、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="465cd-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="465cd-109">モデルクラスの **[ムービー (MvcMovie)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="465cd-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="465cd-110">データコンテキストクラスの**Mo? Dbcontext (MvcMovie. model)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="465cd-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="465cd-111">コントローラー名として「 **moviescontroller.cs**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="465cd-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="465cd-112">次の図は、完成したダイアログを示しています。</span><span class="sxs-lookup"><span data-stu-id="465cd-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="465cd-113">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="465cd-113">Click **Add**.</span></span> <span data-ttu-id="465cd-114">(エラーが発生した場合は、コントローラーの追加を開始する前にアプリケーションをビルドしていないことがあります)。Visual Studio では、次のファイルとフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="465cd-115">*Controllers*フォルダー内の*MoviesController.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="465cd-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="465cd-116">*Views\Movies*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="465cd-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="465cd-117">新しい*Views\Movies*フォルダーに、cshtml、Cshtml、 *Details、Edit.* cshtml、および*Index*を作成します。</span><span class="sxs-lookup"><span data-stu-id="465cd-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="465cd-118">Visual Studio では、 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されます (crud アクションメソッドとビューの自動作成はスキャフォールディングと呼ばれます)。</span><span class="sxs-lookup"><span data-stu-id="465cd-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="465cd-119">これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="465cd-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="465cd-120">アプリケーションを実行し、 **[MVC ムービー]** リンクをクリックします (または、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します)。</span><span class="sxs-lookup"><span data-stu-id="465cd-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="465cd-121">アプリケーションは既定のルーティング (*アプリ\_Start\RouteConfig.cs*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は `Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="465cd-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="465cd-122">つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。</span><span class="sxs-lookup"><span data-stu-id="465cd-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="465cd-123">まだ追加していないため、結果はムービーの空の一覧になります。</span><span class="sxs-lookup"><span data-stu-id="465cd-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="465cd-124">ムービーの作成</span><span class="sxs-lookup"><span data-stu-id="465cd-124">Creating a Movie</span></span>

<span data-ttu-id="465cd-125">**[Create New]\(新規作成\)** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="465cd-125">Select the **Create New** link.</span></span> <span data-ttu-id="465cd-126">ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="465cd-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="465cd-127">価格フィールドに小数点またはコンマを入力することはできません。</span><span class="sxs-lookup"><span data-stu-id="465cd-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="465cd-128">小数点に対してコンマ (&quot;、&quot;) を使用する英語以外のロケール、および米国英語以外の日付形式に対して jQuery 検証をサポートするには、`Globalize.parseFloat`を使用するように、*グローバライズ*および特定の*カルチャ/グローバライズ*ファイル ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize)から)、および JavaScript を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="465cd-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="465cd-129">これを行う方法については、次のチュートリアルで説明します。</span><span class="sxs-lookup"><span data-stu-id="465cd-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="465cd-130">ここでは、単に 10 のような整数を入力します。</span><span class="sxs-lookup"><span data-stu-id="465cd-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="465cd-131">**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="465cd-132">次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。</span><span class="sxs-lookup"><span data-stu-id="465cd-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="465cd-133">いくつかのムービー エントリを作成します。</span><span class="sxs-lookup"><span data-stu-id="465cd-133">Create a couple more movie entries.</span></span> <span data-ttu-id="465cd-134">**[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。</span><span class="sxs-lookup"><span data-stu-id="465cd-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="465cd-135">生成されたコードの調査</span><span class="sxs-lookup"><span data-stu-id="465cd-135">Examining the Generated Code</span></span>

<span data-ttu-id="465cd-136">*Controllers\MoviesController.cs*ファイルを開き、生成された `Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="465cd-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="465cd-137">`Index` メソッドを使用したムービーコントローラーの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="465cd-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="465cd-138">`Movies` コントローラーに対する要求では、`Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="465cd-139">前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="465cd-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="465cd-140">ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="465cd-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="465cd-141">厳密に型指定されたモデルと @model キーワード</span><span class="sxs-lookup"><span data-stu-id="465cd-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="465cd-142">このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="465cd-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="465cd-143">`ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="465cd-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="465cd-144">MVC では、*厳密*に型指定されたオブジェクトをビューテンプレートに渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="465cd-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="465cd-145">この厳密に型指定されたアプローチによって、Visual Studio エディターでのコードのコンパイル時のチェックと、より高度な[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx)が有効になります。</span><span class="sxs-lookup"><span data-stu-id="465cd-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="465cd-146">Visual Studio のスキャフォールディング機構では、メソッドとビューを作成するときに、この方法 (*厳密*に型指定されたモデルを渡す) を `MoviesController` クラスおよびビューテンプレートと共に使用しました。</span><span class="sxs-lookup"><span data-stu-id="465cd-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="465cd-147">*Controllers\MoviesController.cs*ファイルで、生成された `Details` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="465cd-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="465cd-148">`Details` メソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="465cd-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="465cd-149">`id` パラメーターは通常、ルートデータとして渡されます。たとえば、`http://localhost:1234/movies/details/1` によってコントローラーがムービーコントローラーに設定され、アクションが `details`、`id` が1に設定されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="465cd-150">次のように、クエリ文字列を使用して id を渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="465cd-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="465cd-151">`Movie` が見つかった場合、`Movie` モデルのインスタンスが `Details` ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="465cd-152">*Views\Movies\Details.cshtml*ファイルの内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="465cd-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="465cd-153">ビューテンプレートファイルの先頭に `@model` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。</span><span class="sxs-lookup"><span data-stu-id="465cd-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="465cd-154">ムービー コントローラーを作成したとき、Visual Studio によって `@model`Details.cshtml*ファイルの先頭に* ステートメントが自動的に追加されています。</span><span class="sxs-lookup"><span data-stu-id="465cd-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="465cd-155">この `@model` ディレクティブにより、厳密に型指定された `Model` オブジェクトを使って、コントローラーがビューに渡したムービーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="465cd-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="465cd-156">たとえば、 *Details. cshtml*テンプレートでは、コードは各ムービーフィールドを `DisplayNameFor` に渡し、厳密に型指定された `Model` オブジェクトを使用して HTML ヘルパー[を](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)表示します。</span><span class="sxs-lookup"><span data-stu-id="465cd-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="465cd-157">`Create` メソッドと `Edit` メソッドとビューテンプレートも、ムービーモデルオブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="465cd-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="465cd-158">*MoviesController.cs*ファイルで、*インデックスの cshtml*ビューテンプレートと `Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="465cd-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="465cd-159">`Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="465cd-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="465cd-160">次に、コードはこの `Movies` リストを `Index` アクションメソッドからビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="465cd-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="465cd-161">ムービーコントローラーを作成すると、Visual Studio によって、次の `@model` ステートメントが*Index. cshtml*ファイルの先頭に自動的に含まれます。</span><span class="sxs-lookup"><span data-stu-id="465cd-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="465cd-162">この `@model` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="465cd-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="465cd-163">たとえば、 *Index. cshtml*テンプレートでは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。</span><span class="sxs-lookup"><span data-stu-id="465cd-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="465cd-164">`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="465cd-165">その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="465cd-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="465cd-167">SQL Server LocalDB の使用</span><span class="sxs-lookup"><span data-stu-id="465cd-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="465cd-168">Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="465cd-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="465cd-169">これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="465cd-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="465cd-170">*ムービーの .mdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、最新の情報に **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="465cd-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="465cd-171">[ *.Mdf* ] をダブルクリックして**サーバーエクスプローラー**を開き、 **[テーブル]** フォルダーを展開して、ムービーテーブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="465cd-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="465cd-172">[ID] の横にあるキーアイコンに注意してください。</span><span class="sxs-lookup"><span data-stu-id="465cd-172">Note the key icon next to ID.</span></span> <span data-ttu-id="465cd-173">既定では、EF は、ID という名前のプロパティを主キーとして作成します。</span><span class="sxs-lookup"><span data-stu-id="465cd-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="465cd-174">EF と MVC の詳細については、「Tom Dykstra's [mvc と ef](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)の優れたチュートリアル」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="465cd-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="465cd-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="465cd-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="465cd-176">`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="465cd-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="465cd-177">`Movies` テーブルを右クリックし、 **[テーブル定義を開く]** を選択して、Entity Framework 作成 Code First テーブルの構造を確認します。</span><span class="sxs-lookup"><span data-stu-id="465cd-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="465cd-178">`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。</span><span class="sxs-lookup"><span data-stu-id="465cd-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="465cd-179">このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。</span><span class="sxs-lookup"><span data-stu-id="465cd-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="465cd-180">操作が完了したら、 *Mo? Dbcontext*を右クリックし、 **[接続を閉じる]** を選択して接続を閉じます。</span><span class="sxs-lookup"><span data-stu-id="465cd-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="465cd-181">(接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。</span><span class="sxs-lookup"><span data-stu-id="465cd-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="465cd-182">これで、データを表示、編集、更新および削除できるデータベースができました。</span><span class="sxs-lookup"><span data-stu-id="465cd-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="465cd-183">次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="465cd-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="465cd-184">MVC での Entity Framework の使用の詳細については、「 [ASP.NET MVC アプリケーションの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="465cd-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="465cd-185">[前へ](creating-a-connection-string.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="465cd-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
