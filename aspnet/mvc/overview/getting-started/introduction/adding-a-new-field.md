---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 新しいフィールドの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 5974e53e4610dccc7812df261dc97a9b0327de85
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456687"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="9247a-102">新しいフィールドの追加</span><span class="sxs-lookup"><span data-stu-id="9247a-102">Adding a New Field</span></span>

<span data-ttu-id="9247a-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9247a-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="9247a-104">このセクションでは、Entity Framework Code First Migrations を使用して、変更がデータベースに適用されるように、モデルクラスにいくつかの変更を移行します。</span><span class="sxs-lookup"><span data-stu-id="9247a-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="9247a-105">既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="9247a-106">同期されていない場合は、Entity Framework によってエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="9247a-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="9247a-107">これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。</span><span class="sxs-lookup"><span data-stu-id="9247a-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="9247a-108">モデル変更の Code First Migrations の設定</span><span class="sxs-lookup"><span data-stu-id="9247a-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="9247a-109">ソリューションエクスプローラーに移動します。</span><span class="sxs-lookup"><span data-stu-id="9247a-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="9247a-110">*ムービーの .mdf*ファイルを右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。</span><span class="sxs-lookup"><span data-stu-id="9247a-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="9247a-111">*ムービーの .mdf*ファイルが表示されない場合は、次の赤いアウトラインにある **[すべてのファイルを表示]** アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="9247a-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="9247a-112">アプリケーションをビルドしてエラーがないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="9247a-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="9247a-113">**[ツール]** メニューで **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="9247a-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![パックマンの追加](adding-a-new-field/_static/image2.png)

<span data-ttu-id="9247a-115">**パッケージマネージャーコンソール**ウィンドウの `PM>` プロンプトで、「」と入力します。</span><span class="sxs-lookup"><span data-stu-id="9247a-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="9247a-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="9247a-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="9247a-117">(上の図に示した)**移行を有効に**するコマンドを実行すると、新しい*移行*フォルダーに*Configuration.cs*ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="9247a-118">Visual Studio によって*Configuration.cs*ファイルが開きます。</span><span class="sxs-lookup"><span data-stu-id="9247a-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="9247a-119">*Configuration.cs*ファイルの `Seed` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="9247a-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="9247a-120">`Movie` の下の赤い波線の上にマウスポインターを移動し、[`Show Potential Fixes`] をクリックして、[ **mvcmovie** **を使用する**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="9247a-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="9247a-121">これにより、次の using ステートメントが追加されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="9247a-122">Code First Migrations は、すべての移行の後 (つまり、パッケージマネージャーコンソールで**更新プログラムデータベース**を呼び出す) に `Seed` メソッドを呼び出します。このメソッドは、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。</span><span class="sxs-lookup"><span data-stu-id="9247a-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="9247a-123">次のコードの[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドは、"upsert" 操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="9247a-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="9247a-124">[シード](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドはすべての移行で実行されるため、データを挿入することはできません。これは、データベースを最初に移行した後に、追加しようとしている行が既に存在するためです。</span><span class="sxs-lookup"><span data-stu-id="9247a-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="9247a-125">"[Upsert](http://en.wikipedia.org/wiki/Upsert)" 操作は、既に存在する行を挿入しようとすると発生するエラーを防ぎますが、アプリケーションのテスト中に行われたデータの変更を上書きします。</span><span class="sxs-lookup"><span data-stu-id="9247a-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="9247a-126">一部のテーブルのテストデータでは、このような処理が不要な場合があります。テスト中にデータを変更し、データベースの更新後も変更を保持する場合があります。</span><span class="sxs-lookup"><span data-stu-id="9247a-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="9247a-127">その場合は、条件付き挿入操作を実行します。行がまだ存在しない場合にのみ、行を挿入します。</span><span class="sxs-lookup"><span data-stu-id="9247a-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="9247a-128">[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドに渡される最初のパラメーターは、行が既に存在するかどうかを確認するために使用するプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="9247a-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="9247a-129">提供しているテストムービーデータの場合は、リスト内の各タイトルが一意であるため、この目的には `Title` プロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="9247a-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="9247a-130">このコードは、タイトルが一意であることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="9247a-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="9247a-131">重複するタイトルを手動で追加すると、次に移行を実行したときに次の例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="9247a-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="9247a-132">*シーケンスに複数の要素が含まれています*</span><span class="sxs-lookup"><span data-stu-id="9247a-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="9247a-133">[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドの詳細については、「 [EF 4.3 Addorupdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="9247a-134">**CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。** (この時点でビルドしない場合、次の手順は失敗します)。</span><span class="sxs-lookup"><span data-stu-id="9247a-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="9247a-135">次の手順では、初期移行のために `DbMigration` クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="9247a-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="9247a-136">この移行によって新しいデータベースが作成されます。これは、前の手順で*ムービー .mdf*ファイルを削除したためです。</span><span class="sxs-lookup"><span data-stu-id="9247a-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="9247a-137">**パッケージマネージャーコンソール**ウィンドウで、コマンド `add-migration Initial` を入力して、初期移行を作成します。</span><span class="sxs-lookup"><span data-stu-id="9247a-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="9247a-138">"Initial" という名前は任意であり、作成される移行ファイルに名前を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="9247a-139">Code First Migrations は、*移行*フォルダー ( *{datestamp}\_Initial.cs* ) に別のクラスファイルを作成します。このクラスには、データベーススキーマを作成するコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9247a-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="9247a-140">移行ファイル名は、順序付けを支援するタイムスタンプで事前に固定されています。</span><span class="sxs-lookup"><span data-stu-id="9247a-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="9247a-141">*{Datestamp}\_Initial.cs*ファイルを調べます。このファイルには、Movie DB の `Movies` テーブルを作成するための手順が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9247a-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="9247a-142">以下の手順でデータベースを更新すると、この *{Datestamp}\_Initial.cs*ファイルが実行され、DB スキーマが作成されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="9247a-143">次に、 **Seed**メソッドを実行して、データベースにテストデータを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="9247a-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="9247a-144">**パッケージマネージャーコンソール**で、コマンド `update-database` を入力してデータベースを作成し、`Seed` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="9247a-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="9247a-145">テーブルが既に存在して作成できないことを示すエラーが表示された場合は、データベースを削除した後、`update-database`を実行する前にアプリケーションを実行したことが原因である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9247a-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="9247a-146">その場合は、もう一度*ムービーの .mdf*ファイルを削除し、`update-database` コマンドを再試行してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="9247a-147">それでもエラーが発生する場合は、移行フォルダとコンテンツを削除してから、このページの上部にある指示に従って作業を開始してください (*つまり、この*ページの内容を削除してから、移行の有効化に進みます)。</span><span class="sxs-lookup"><span data-stu-id="9247a-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="9247a-148">それでもエラーが発生する場合は、SQL Server オブジェクトエクスプローラーを開き、データベースを一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="9247a-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="9247a-149">アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="9247a-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="9247a-150">シードデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="9247a-151">ムービー モデルへの評価プロパティの追加</span><span class="sxs-lookup"><span data-stu-id="9247a-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="9247a-152">まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="9247a-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="9247a-153">*Modelthe modelfile*を開き、次のように `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="9247a-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="9247a-154">完成した `Movie` クラスは次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="9247a-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="9247a-155">アプリケーションをビルドします (Ctrl + Shift + B)。</span><span class="sxs-lookup"><span data-stu-id="9247a-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="9247a-156">新しいフィールドを `Movie` クラスに追加したので、この新しいプロパティが含まれるように、バインドの*ホワイトリスト*も更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9247a-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="9247a-157">`Create` および `Edit` アクションメソッドの `bind` 属性を更新して、`Rating` プロパティを含めます。</span><span class="sxs-lookup"><span data-stu-id="9247a-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="9247a-158">ブラウザー ビューで新しい `Rating` プロパティを表示、作成、編集する目的でビュー テンプレートを更新する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="9247a-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="9247a-159">*\Views\Movies\Index.cshtml*ファイルを開き、 **Price**列の直後に `<th>Rating</th>` 列見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="9247a-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="9247a-160">次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。</span><span class="sxs-lookup"><span data-stu-id="9247a-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="9247a-161">更新されたインデックスの例を次に示し*ます。 cshtml* view テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9247a-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="9247a-162">次に、 *\Views\Movies\Create.cshtml*ファイルを開き、次の強調表示されたマークアップを含む `Rating` フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="9247a-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="9247a-163">新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="9247a-164">これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。</span><span class="sxs-lookup"><span data-stu-id="9247a-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="9247a-165">アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="9247a-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="9247a-166">ただし、この操作を行うと、次のいずれかのエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="9247a-167">データベースが作成されてから、' Mo? Dbcontext ' コンテキストをバッキングするモデルが変更されました。</span><span class="sxs-lookup"><span data-stu-id="9247a-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="9247a-168">Code First Migrations を使用してデータベースを更新することを検討してください (https://go.microsoft.com/fwlink/?LinkId=238269)。</span><span class="sxs-lookup"><span data-stu-id="9247a-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="9247a-169">このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。</span><span class="sxs-lookup"><span data-stu-id="9247a-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="9247a-170">(データベース テーブルに `Rating` 列はありません)。</span><span class="sxs-lookup"><span data-stu-id="9247a-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="9247a-171">このエラーを解決するための手法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="9247a-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="9247a-172">Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。</span><span class="sxs-lookup"><span data-stu-id="9247a-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="9247a-173">この手法は、開発周期の早い段階で、テスト データベースで開発しているときに非常に便利です。モデルとデータベース スキーマを一緒に短期間で発展させることができます。</span><span class="sxs-lookup"><span data-stu-id="9247a-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="9247a-174">ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。</span><span class="sxs-lookup"><span data-stu-id="9247a-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="9247a-175">初期化子を利用し、データベースにテスト データを自動的に初期投入します。多くの場合、アプリケーション開発の手法として有益な方法です。</span><span class="sxs-lookup"><span data-stu-id="9247a-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="9247a-176">Entity Framework データベース初期化子の詳細については、「 [ASP.NET MVC/Entity Framework チュートリアル](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="9247a-177">モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。</span><span class="sxs-lookup"><span data-stu-id="9247a-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="9247a-178">この手法の長所は、データが維持されることです。</span><span class="sxs-lookup"><span data-stu-id="9247a-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="9247a-179">この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="9247a-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="9247a-180">Code First Migrations を使用して、データベース スキーマを更新します。</span><span class="sxs-lookup"><span data-stu-id="9247a-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="9247a-181">このチュートリアルでは、Code First Migrations を利用します。</span><span class="sxs-lookup"><span data-stu-id="9247a-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="9247a-182">新しい列の値を提供するように、Seed メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="9247a-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="9247a-183">Migrations\ configuration.cs ファイルを開き、各ムービーオブジェクトに評価フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="9247a-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="9247a-184">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開き、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="9247a-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="9247a-185">`add-migration` のコマンドは、現在のムービーの DB スキーマを使用して現在のムービーモデルを確認し、新しいモデルにデータベースを移行するために必要なコードを作成するように移行フレームワークに指示します。</span><span class="sxs-lookup"><span data-stu-id="9247a-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="9247a-186">名前の*評価*は任意であり、移行ファイルの名前を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="9247a-187">移行手順にわかりやすい名前を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="9247a-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="9247a-188">このコマンドが終了すると、Visual Studio によって、新しい `DbMigration` 派生クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="9247a-189">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで `update-database` コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="9247a-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="9247a-190">次の図は、**パッケージマネージャーコンソール**ウィンドウの出力を示しています (日付スタンプの前の*評価*は異なっています)。</span><span class="sxs-lookup"><span data-stu-id="9247a-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="9247a-191">アプリケーションを再実行し、/ムービーの URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="9247a-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="9247a-192">[新しい評価] フィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9247a-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="9247a-193">新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="9247a-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="9247a-194">評価を追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="9247a-196">[作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="9247a-196">Click **Create**.</span></span> <span data-ttu-id="9247a-197">新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="9247a-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="9247a-199">プロジェクトが移行を使用しているので、新しいフィールドを追加するとき、またはスキーマを更新するときに、データベースを削除する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9247a-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="9247a-200">次のセクションでは、より多くのスキーマ変更を行い、移行を使用してデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="9247a-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="9247a-201">また、[編集]、[詳細]、および [削除] ビューテンプレートに `Rating` フィールドを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9247a-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="9247a-202">**パッケージマネージャーコンソール**ウィンドウに [データベースの更新] コマンドをもう一度入力すると、スキーマがモデルに一致するので、移行コードは実行されません。</span><span class="sxs-lookup"><span data-stu-id="9247a-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="9247a-203">ただし、"データベースの更新" を実行すると、`Seed` メソッドが再度実行されます。また、いずれかのシードデータを変更した場合は、`Seed` メソッド upsert データによって変更が失われます。</span><span class="sxs-lookup"><span data-stu-id="9247a-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="9247a-204">`Seed` メソッドの詳細については、Tom Dykstra の一般的な[ASP.NET MVC/Entity Framework チュートリアル](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="9247a-205">このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="9247a-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="9247a-206">また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="9247a-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="9247a-207">これは、Code First について簡単に説明したばかりです。詳細については、「 [ASP.NET MVC アプリケーションの Entity Framework データモデルを作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9247a-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="9247a-208">次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="9247a-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9247a-209">[前へ](adding-search.md)
> [次へ](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="9247a-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
