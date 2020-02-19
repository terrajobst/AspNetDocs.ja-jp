---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: ムービーモデルとテーブルに新しいフィールドを追加する |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457701"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="bc0cd-104">Movie モデルとテーブルに新しいフィールドを追加する</span><span class="sxs-lookup"><span data-stu-id="bc0cd-104">Adding a New Field to the Movie Model and Table</span></span>

<span data-ttu-id="bc0cd-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bc0cd-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="bc0cd-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="bc0cd-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="bc0cd-108">このセクションでは、Entity Framework Code First Migrations を使用して、変更がデータベースに適用されるように、モデルクラスにいくつかの変更を移行します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="bc0cd-109">既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="bc0cd-110">同期されていない場合は、Entity Framework によってエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="bc0cd-111">これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="bc0cd-112">モデル変更の Code First Migrations の設定</span><span class="sxs-lookup"><span data-stu-id="bc0cd-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="bc0cd-113">Visual Studio 2012 を使用している場合は、ソリューションエクスプローラーからの*ムービーの .mdf*ファイルをダブルクリックして、データベースツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="bc0cd-114">Web 用の Visual Studio Express にデータベースエクスプローラーが表示され、Visual Studio 2012 にサーバーエクスプローラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="bc0cd-115">Visual Studio 2010 を使用している場合は、SQL Server オブジェクトエクスプローラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="bc0cd-116">データベースツール (データベースエクスプローラー、サーバーエクスプローラーまたは SQL Server オブジェクトエクスプローラー) で、`MovieDBContext` を右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="bc0cd-117">ソリューションエクスプローラーに戻ります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="bc0cd-118">*ムービーの .mdf*ファイルを右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="bc0cd-119">アプリケーションをビルドしてエラーがないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="bc0cd-120">**[ツール]** メニューで **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![パックマンの追加](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="bc0cd-122">**パッケージマネージャーコンソール**ウィンドウの `PM>` プロンプトで、「Enable-移行-ContextTypeName MvcMovie」と入力します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="bc0cd-123">(上の図に示した)**移行を有効に**するコマンドを実行すると、新しい*移行*フォルダーに*Configuration.cs*ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="bc0cd-124">Visual Studio によって*Configuration.cs*ファイルが開きます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="bc0cd-125">*Configuration.cs*ファイルの `Seed` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="bc0cd-126">`Movie` の下の赤い波線を右クリックし、 **[解決]** 、[ **mvcmovie の** **使用**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="bc0cd-127">これにより、次の using ステートメントが追加されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="bc0cd-128">Code First Migrations は、すべての移行の後 (つまり、パッケージマネージャーコンソールで**更新プログラムデータベース**を呼び出す) に `Seed` メソッドを呼び出します。このメソッドは、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>

<span data-ttu-id="bc0cd-129">**CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。** (この時点でをビルドしないと、次の手順は失敗します)。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="bc0cd-130">次の手順では、初期移行のために `DbMigration` クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="bc0cd-131">この移行によって新しいデータベースが作成されます。これは、前の手順で*ムービーの .mdf*ファイルを削除したためです。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="bc0cd-132">**パッケージマネージャーコンソール**ウィンドウで、"追加-移行の初期" コマンドを入力して、初期移行を作成します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="bc0cd-133">"Initial" という名前は任意であり、作成される移行ファイルに名前を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="bc0cd-134">Code First Migrations は、*移行*フォルダー ( *{datestamp}\_Initial.cs* ) に別のクラスファイルを作成します。このクラスには、データベーススキーマを作成するコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="bc0cd-135">移行ファイル名は、順序付けを支援するタイムスタンプで事前に固定されています。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="bc0cd-136">*{Datestamp}\_Initial.cs*ファイルを調べます。このファイルには、Movie DB のムービーテーブルを作成するための手順が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="bc0cd-137">以下の手順でデータベースを更新すると、この *{Datestamp}\_Initial.cs*ファイルが実行され、DB スキーマが作成されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="bc0cd-138">次に、 **Seed**メソッドを実行して、データベースにテストデータを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="bc0cd-139">**パッケージマネージャーコンソール**で、"データベースの更新" コマンドを入力してデータベースを作成し、 **Seed**メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="bc0cd-140">テーブルが既に存在して作成できないことを示すエラーが表示された場合は、データベースを削除した後、`update-database`を実行する前にアプリケーションを実行したことが原因である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="bc0cd-141">その場合は、もう一度*ムービーの .mdf*ファイルを削除し、`update-database` コマンドを再試行してください。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="bc0cd-142">それでもエラーが発生する場合は、移行フォルダとコンテンツを削除してから、このページの上部にある指示に従って作業を開始してください (*つまり、この*ページの内容を削除してから、移行の有効化に進みます)。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="bc0cd-143">アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="bc0cd-144">シードデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="bc0cd-145">ムービー モデルへの評価プロパティの追加</span><span class="sxs-lookup"><span data-stu-id="bc0cd-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="bc0cd-146">まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="bc0cd-147">*Modelthe modelfile*を開き、次のように `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="bc0cd-148">完成した `Movie` クラスは次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="bc0cd-149">[ビルド &gt;**ビルド**] メニューコマンドを使用するか、CTRL + SHIFT + B キーを押し**て、アプリケーション**をビルドします。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="bc0cd-150">`Model` クラスを更新したので、新しい `Rating` プロパティをブラウザービューで表示するために、 *\Views\Movies\Index.cshtml*および *\Views\Movies\Create.cshtml* view テンプレートも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="bc0cd-151"><em>\Views\Movies\Index.cshtml</em>ファイルを開き、 <strong>Price</strong>列の直後に `<th>Rating</th>` 列見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="bc0cd-152">次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="bc0cd-153">更新されたインデックスの例を次に示し<em>ます。 cshtml</em> view テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="bc0cd-154">次に、 *\Views\Movies\Create.cshtml*ファイルを開き、フォームの末尾付近に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="bc0cd-155">新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="bc0cd-156">これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="bc0cd-157">次に、アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="bc0cd-158">ただし、この操作を行うと、次のいずれかのエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="bc0cd-159">このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="bc0cd-160">(データベース テーブルに `Rating` 列はありません)。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-160">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="bc0cd-161">このエラーを解決するための手法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="bc0cd-162">Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="bc0cd-163">この方法は、テストデータベースに対してアクティブな開発を行う場合に非常に便利です。これにより、モデルとデータベーススキーマを一緒に迅速に進化させることができます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="bc0cd-164">ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="bc0cd-165">初期化子を使用して、データベースをテストデータで自動的にシード処理することは、多くの場合、アプリケーションを開発するための生産性の高い方法です。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="bc0cd-166">Entity Framework データベース初期化子の詳細については、「Tom Dykstra の[ASP.NET MVC/Entity Framework チュートリアル](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="bc0cd-167">モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="bc0cd-168">この手法の長所は、データが維持されることです。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="bc0cd-169">この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="bc0cd-170">Code First Migrations を使用して、データベース スキーマを更新します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-170">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="bc0cd-171">このチュートリアルでは、Code First Migrations を利用します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="bc0cd-172">新しい列の値を提供するように、Seed メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="bc0cd-173">Migrations\ configuration.cs ファイルを開き、各ムービーオブジェクトに評価フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="bc0cd-174">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開き、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="bc0cd-175">`add-migration` のコマンドは、現在のムービーの DB スキーマを使用して現在のムービーモデルを確認し、新しいモデルにデータベースを移行するために必要なコードを作成するように移行フレームワークに指示します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="bc0cd-176">AddRatingMig は任意であり、移行ファイルの名前を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="bc0cd-177">移行手順にわかりやすい名前を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="bc0cd-178">このコマンドが終了すると、Visual Studio によって、新しい `DbMigration` 派生クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="bc0cd-179">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで "データベースの更新" コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="bc0cd-180">次の図は、**パッケージマネージャーコンソール**ウィンドウの出力を示しています (日付スタンプの前に AddRatingMig があります)。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="bc0cd-181">アプリケーションを再実行し、/ムービーの URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="bc0cd-182">[新しい評価] フィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="bc0cd-183">新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="bc0cd-184">評価を追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="bc0cd-186">[作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-186">Click **Create**.</span></span> <span data-ttu-id="bc0cd-187">新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="bc0cd-189">また、[編集]、[詳細]、および [SearchIndex view] テンプレートに `Rating` フィールドを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="bc0cd-190">**パッケージマネージャーコンソール**ウィンドウに [データベースの更新] コマンドをもう一度入力すると、スキーマがモデルに一致するため、変更は行われません。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="bc0cd-191">このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="bc0cd-192">また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="bc0cd-193">次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="bc0cd-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bc0cd-194">[前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="bc0cd-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
