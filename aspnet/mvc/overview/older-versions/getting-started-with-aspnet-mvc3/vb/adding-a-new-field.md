---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: ムービーモデルとデータベーステーブルに新しいフィールドを追加する (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457267"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a><span data-ttu-id="3e286-103">Movie モデルとテーブルに新しいフィールドを追加する (VB)</span><span class="sxs-lookup"><span data-stu-id="3e286-103">Adding a New Field to the Movie Model and Database Table (VB)</span></span>

<span data-ttu-id="3e286-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3e286-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3e286-105">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="3e286-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3e286-106">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3e286-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3e286-107">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3e286-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3e286-108">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="3e286-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3e286-109">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="3e286-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3e286-110">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="3e286-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3e286-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="3e286-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3e286-112">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3e286-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3e286-113">このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="3e286-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3e286-114">[VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="3e286-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3e286-115">必要に応じC#て[ C# ](../cs/adding-a-new-field.md) 、このチュートリアルのバージョンに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="3e286-115">If you prefer C#, switch to the [C# version](../cs/adding-a-new-field.md) of this tutorial.</span></span>

<span data-ttu-id="3e286-116">このセクションでは、モデルクラスにいくつかの変更を加え、モデルの変更に合わせてデータベーススキーマを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3e286-116">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="3e286-117">ムービー モデルへの評価プロパティの追加</span><span class="sxs-lookup"><span data-stu-id="3e286-117">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="3e286-118">まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e286-118">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="3e286-119">*Movie.cs*ファイルを開き、次のように `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e286-119">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

<span data-ttu-id="3e286-120">完成した `Movie` クラスは次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="3e286-120">The complete `Movie` class now looks like the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

<span data-ttu-id="3e286-121">[**デバッグ**&gt;**ビルドのムービー** ] メニューコマンドを使用して、アプリケーションを再コンパイルします。</span><span class="sxs-lookup"><span data-stu-id="3e286-121">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="3e286-122">`Model` クラスを更新したので、新しい `Rating` プロパティをサポートするために、 *\Views\Movies\Index.vbhtml*および *\Views\Movies\Create.vbhtml* view テンプレートも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e286-122">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.vbhtml* and *\Views\Movies\Create.vbhtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="3e286-123"><em>\Views\Movies\Index.vbhtml</em>ファイルを開き、 <strong>Price</strong>列の直後に `<th>Rating</th>` 列見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e286-123">Open the<em>\Views\Movies\Index.vbhtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="3e286-124">次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。</span><span class="sxs-lookup"><span data-stu-id="3e286-124">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="3e286-125">更新されたインデックスの例を次に示し<em>ます。 vbhtml</em>ビューテンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3e286-125">Below is what the updated <em>Index.vbhtml</em> view template looks like:</span></span>

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

<span data-ttu-id="3e286-126">次に、 *\Views\Movies\Create.vbhtml*ファイルを開き、フォームの末尾付近に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e286-126">Next, open the *\Views\Movies\Create.vbhtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="3e286-127">新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-127">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="3e286-128">モデルとデータベーススキーマの違いの管理</span><span class="sxs-lookup"><span data-stu-id="3e286-128">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="3e286-129">これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。</span><span class="sxs-lookup"><span data-stu-id="3e286-129">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="3e286-130">次に、アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="3e286-130">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3e286-131">ただし、この操作を行うと、次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-131">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="3e286-132">このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。</span><span class="sxs-lookup"><span data-stu-id="3e286-132">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="3e286-133">(データベース テーブルに `Rating` 列はありません)。</span><span class="sxs-lookup"><span data-stu-id="3e286-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="3e286-134">既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-134">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="3e286-135">同期されていない場合は、Entity Framework によってエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="3e286-135">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="3e286-136">これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。</span><span class="sxs-lookup"><span data-stu-id="3e286-136">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="3e286-137">同期チェック機能により、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-137">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="3e286-138">このエラーを解決するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="3e286-138">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="3e286-139">Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。</span><span class="sxs-lookup"><span data-stu-id="3e286-139">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="3e286-140">この方法は、テストデータベースに対してアクティブな開発を行う場合に非常に便利です。これにより、モデルとデータベーススキーマを一緒に迅速に進化させることができます。</span><span class="sxs-lookup"><span data-stu-id="3e286-140">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="3e286-141">ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。</span><span class="sxs-lookup"><span data-stu-id="3e286-141">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="3e286-142">モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。</span><span class="sxs-lookup"><span data-stu-id="3e286-142">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="3e286-143">この手法の長所は、データが維持されることです。</span><span class="sxs-lookup"><span data-stu-id="3e286-143">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="3e286-144">この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="3e286-144">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="3e286-145">このチュートリアルでは、最初の方法を使用します。モデルが変更されるたびに、データベースを自動的に再作成 Code First Entity Framework します。</span><span class="sxs-lookup"><span data-stu-id="3e286-145">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="3e286-146">モデルの変更時にデータベースを自動的に再作成する</span><span class="sxs-lookup"><span data-stu-id="3e286-146">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="3e286-147">アプリケーションのモデルを変更するたびに、Code First によってデータベースが自動的に削除され、再作成されるようにアプリケーションを更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="3e286-147">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3e286-148">**警告**データベースを自動的に削除して再作成するには、この方法を有効にする必要があります。この方法では、開発またはテストデータベースを使用していて、実際のデータが含まれている実稼働データベースでは使用し*ません*。</span><span class="sxs-lookup"><span data-stu-id="3e286-148">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="3e286-149">実稼働サーバーで使用すると、データが失われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3e286-149">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="3e286-150">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="3e286-150">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="3e286-151">クラスに &quot;Moの初期化子&quot;の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="3e286-151">Name the class &quot;MovieInitializer&quot;.</span></span> <span data-ttu-id="3e286-152">次のコードを含むように `MovieInitializer` クラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="3e286-152">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

<span data-ttu-id="3e286-153">`MovieInitializer` クラスは、モデルクラスが変更された場合に、モデルによって使用されるデータベースを削除し、自動的に再作成する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="3e286-153">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="3e286-154">コードには、作成 (または再作成) のたびにデータベースに自動的に追加される既定のデータを指定する `Seed` メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e286-154">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="3e286-155">これにより、モデルを変更するたびに手動でデータを入力することなく、いくつかのサンプルデータをデータベースに読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="3e286-155">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="3e286-156">`MovieInitializer` クラスの定義が完了したので、アプリケーションを実行するたびに、モデルクラスがデータベースのスキーマと異なるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="3e286-156">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="3e286-157">そのような場合は、初期化子を実行して、モデルに一致するデータベースを再作成してから、サンプルデータをデータベースに設定できます。</span><span class="sxs-lookup"><span data-stu-id="3e286-157">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="3e286-158">`MvcMovies` プロジェクトのルートにある*global.asax*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3e286-158">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

<span data-ttu-id="3e286-159">*Global.asax*ファイルには、プロジェクトのアプリケーション全体を定義するクラスが含まれており、アプリケーションの最初の起動時に実行される `Application_Start` イベントハンドラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e286-159">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="3e286-160">次に示すように、`Application_Start` メソッドを見つけて、メソッドの先頭に `Database.SetInitializer` の呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e286-160">Find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

<span data-ttu-id="3e286-161">追加した `Database.SetInitializer` ステートメントは、スキーマとデータベースが一致しない場合に、`MovieDBContext` インスタンスで使用されているデータベースを自動的に削除して再作成する必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="3e286-161">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="3e286-162">また、先ほど見たように、`MovieInitializer` クラスに指定されているサンプルデータもデータベースに設定します。</span><span class="sxs-lookup"><span data-stu-id="3e286-162">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="3e286-163">*Global.asax*ファイルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="3e286-163">Close the *Global.asax* file.</span></span>

<span data-ttu-id="3e286-164">アプリケーションを再実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="3e286-164">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3e286-165">アプリケーションが起動すると、モデル構造がデータベーススキーマと一致しなくなったことが検出されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-165">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="3e286-166">新しいモデル構造と一致するようにデータベースが自動的に再作成され、データベースにサンプルムービーが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="3e286-166">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

<span data-ttu-id="3e286-168">新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3e286-168">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="3e286-169">評価を追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3e286-169">Note that you can add a rating.</span></span>

<span data-ttu-id="3e286-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3e286-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span></span>

<span data-ttu-id="3e286-171">[作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3e286-171">Click **Create**.</span></span> <span data-ttu-id="3e286-172">新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3e286-172">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

<span data-ttu-id="3e286-174">このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="3e286-174">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="3e286-175">また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="3e286-175">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="3e286-176">次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="3e286-176">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e286-177">[前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="3e286-177">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
