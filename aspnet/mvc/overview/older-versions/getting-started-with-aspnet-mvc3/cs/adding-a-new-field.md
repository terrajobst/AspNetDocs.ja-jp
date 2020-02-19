---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: ムービーモデルとテーブルに新しいフィールドを追加する (C#) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457452"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="22d29-103">Movie モデルとテーブルに新しいフィールドを追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="22d29-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="22d29-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="22d29-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="22d29-105">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="22d29-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="22d29-106">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="22d29-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="22d29-107">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="22d29-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="22d29-108">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="22d29-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="22d29-109">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="22d29-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="22d29-110">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="22d29-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="22d29-111">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="22d29-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="22d29-112">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="22d29-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="22d29-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="22d29-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="22d29-114">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="22d29-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="22d29-115">このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="22d29-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="22d29-116">[バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="22d29-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="22d29-117">Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。</span><span class="sxs-lookup"><span data-stu-id="22d29-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="22d29-118">このセクションでは、モデルクラスにいくつかの変更を加え、モデルの変更に合わせてデータベーススキーマを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="22d29-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="22d29-119">ムービー モデルへの評価プロパティの追加</span><span class="sxs-lookup"><span data-stu-id="22d29-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="22d29-120">まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="22d29-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="22d29-121">*Movie.cs*ファイルを開き、次のように `Rating` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="22d29-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="22d29-122">完成した `Movie` クラスは次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="22d29-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="22d29-123">[**デバッグ**&gt;**ビルドのムービー** ] メニューコマンドを使用して、アプリケーションを再コンパイルします。</span><span class="sxs-lookup"><span data-stu-id="22d29-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="22d29-124">`Model` クラスを更新したので、新しい `Rating` プロパティをサポートするために、 *\Views\Movies\Index.cshtml*および *\Views\Movies\Create.cshtml* view テンプレートも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="22d29-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="22d29-125">*\Views\Movies\Index.cshtml*ファイルを開き、 **Price**列の直後に `<th>Rating</th>` 列見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="22d29-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="22d29-126">次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。</span><span class="sxs-lookup"><span data-stu-id="22d29-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="22d29-127">更新されたインデックスの例を次に示し*ます。 cshtml* view テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="22d29-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="22d29-128">次に、 *\Views\Movies\Create.cshtml*ファイルを開き、フォームの末尾付近に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="22d29-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="22d29-129">新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="22d29-130">モデルとデータベーススキーマの違いの管理</span><span class="sxs-lookup"><span data-stu-id="22d29-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="22d29-131">これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。</span><span class="sxs-lookup"><span data-stu-id="22d29-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="22d29-132">次に、アプリケーションを実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="22d29-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="22d29-133">ただし、この操作を行うと、次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="22d29-134">このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。</span><span class="sxs-lookup"><span data-stu-id="22d29-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="22d29-135">(データベース テーブルに `Rating` 列はありません)。</span><span class="sxs-lookup"><span data-stu-id="22d29-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="22d29-136">既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="22d29-137">同期されていない場合は、Entity Framework によってエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="22d29-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="22d29-138">これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。</span><span class="sxs-lookup"><span data-stu-id="22d29-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="22d29-139">同期チェック機能により、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="22d29-140">このエラーを解決するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="22d29-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="22d29-141">Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。</span><span class="sxs-lookup"><span data-stu-id="22d29-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="22d29-142">この方法は、テストデータベースに対してアクティブな開発を行う場合に非常に便利です。これにより、モデルとデータベーススキーマを一緒に迅速に進化させることができます。</span><span class="sxs-lookup"><span data-stu-id="22d29-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="22d29-143">ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。</span><span class="sxs-lookup"><span data-stu-id="22d29-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="22d29-144">モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。</span><span class="sxs-lookup"><span data-stu-id="22d29-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="22d29-145">この手法の長所は、データが維持されることです。</span><span class="sxs-lookup"><span data-stu-id="22d29-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="22d29-146">この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="22d29-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="22d29-147">このチュートリアルでは、最初の方法を使用します。モデルが変更されるたびに、データベースを自動的に再作成 Code First Entity Framework します。</span><span class="sxs-lookup"><span data-stu-id="22d29-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="22d29-148">モデルの変更時にデータベースを自動的に再作成する</span><span class="sxs-lookup"><span data-stu-id="22d29-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="22d29-149">アプリケーションのモデルを変更するたびに、Code First によってデータベースが自動的に削除され、再作成されるようにアプリケーションを更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="22d29-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22d29-150">**警告**データベースを自動的に削除して再作成するには、この方法を有効にする必要があります。この方法では、開発またはテストデータベースを使用していて、実際のデータが含まれている実稼働データベースでは使用し*ません*。</span><span class="sxs-lookup"><span data-stu-id="22d29-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="22d29-151">実稼働サーバーで使用すると、データが失われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="22d29-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="22d29-152">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="22d29-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="22d29-153">クラスに "Moの初期化子" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="22d29-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="22d29-154">次のコードを含むように `MovieInitializer` クラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="22d29-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="22d29-155">`MovieInitializer` クラスは、モデルクラスが変更された場合に、モデルによって使用されるデータベースを削除し、自動的に再作成する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="22d29-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="22d29-156">コードには、作成 (または再作成) のたびにデータベースに自動的に追加される既定のデータを指定する `Seed` メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="22d29-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="22d29-157">これにより、モデルを変更するたびに手動でデータを入力することなく、いくつかのサンプルデータをデータベースに読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="22d29-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="22d29-158">`MovieInitializer` クラスの定義が完了したので、アプリケーションを実行するたびに、モデルクラスがデータベースのスキーマと異なるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="22d29-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="22d29-159">そのような場合は、初期化子を実行して、モデルに一致するデータベースを再作成してから、サンプルデータをデータベースに設定できます。</span><span class="sxs-lookup"><span data-stu-id="22d29-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="22d29-160">`MvcMovies` プロジェクトのルートにある*global.asax*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="22d29-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="22d29-161">*Global.asax*ファイルには、プロジェクトのアプリケーション全体を定義するクラスが含まれており、アプリケーションの最初の起動時に実行される `Application_Start` イベントハンドラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="22d29-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="22d29-162">ファイルの先頭に2つの using ステートメントを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="22d29-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="22d29-163">最初のは Entity Framework 名前空間を参照し、2番目のは `MovieInitializer` クラスが存在する名前空間を参照します。</span><span class="sxs-lookup"><span data-stu-id="22d29-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="22d29-164">次に示すように、`Application_Start` メソッドを見つけて、メソッドの先頭に `Database.SetInitializer` の呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="22d29-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="22d29-165">追加した `Database.SetInitializer` ステートメントは、スキーマとデータベースが一致しない場合に、`MovieDBContext` インスタンスで使用されているデータベースを自動的に削除して再作成する必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="22d29-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="22d29-166">また、先ほど見たように、`MovieInitializer` クラスに指定されているサンプルデータもデータベースに設定します。</span><span class="sxs-lookup"><span data-stu-id="22d29-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="22d29-167">*Global.asax*ファイルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="22d29-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="22d29-168">アプリケーションを再実行し、 */ムービー*の URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="22d29-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="22d29-169">アプリケーションが起動すると、モデル構造がデータベーススキーマと一致しなくなったことが検出されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="22d29-170">新しいモデル構造と一致するようにデータベースが自動的に再作成され、データベースにサンプルムービーが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="22d29-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="22d29-172">新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="22d29-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="22d29-173">評価を追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="22d29-173">Note that you can add a rating.</span></span>

<span data-ttu-id="22d29-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="22d29-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="22d29-175">[作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="22d29-175">Click **Create**.</span></span> <span data-ttu-id="22d29-176">新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="22d29-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="22d29-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="22d29-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="22d29-178">このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="22d29-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="22d29-179">また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="22d29-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="22d29-180">次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="22d29-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22d29-181">[前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="22d29-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
