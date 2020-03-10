---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 'チュートリアル: MVC 5 を使用した EF Database First の概要'
description: このチュートリアルでは、既存のデータベースを使用して作業を開始し、ユーザーがデータと対話できるようにする web アプリケーションをすばやく作成する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471460"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a><span data-ttu-id="27942-103">チュートリアル: MVC 5 を使用した EF Database First の概要</span><span class="sxs-lookup"><span data-stu-id="27942-103">Tutorial: Get started with EF Database First using MVC 5</span></span>

<span data-ttu-id="27942-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="27942-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="27942-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="27942-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="27942-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="27942-106">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="27942-107">シリーズの最後の部分では、データの注釈をデータモデルに追加して検証要件を指定し、書式設定を表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="27942-107">In the last part of the series, you learn how add data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="27942-108">完了したら、Azure の記事に進んで、Azure App Service に .NET アプリと SQL データベースをデプロイする方法を学習できます。</span><span class="sxs-lookup"><span data-stu-id="27942-108">When you're done, you can advance to an Azure article to learn how to deploy a .NET app and SQL database to Azure App Service.</span></span>

<span data-ttu-id="27942-109">このチュートリアルでは、既存のデータベースを使用して作業を開始し、ユーザーがデータと対話できるようにする web アプリケーションをすばやく作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="27942-109">This tutorial shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="27942-110">Entity Framework 6 と MVC 5 を使用して、web アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="27942-110">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="27942-111">ASP.NET スキャフォールディング機能を使用すると、データの表示、更新、作成、および削除のためのコードを自動的に生成できます。</span><span class="sxs-lookup"><span data-stu-id="27942-111">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="27942-112">Visual Studio 内で発行ツールを使用すると、サイトとデータベースを Azure に簡単にデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="27942-112">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="27942-113">シリーズのこの部分では、データベースを作成し、データを読み込む方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="27942-113">This part of the series focuses on creating a database and populating it with data.</span></span>

<span data-ttu-id="27942-114">このシリーズでは、Tom Dykstra と Rick Anderson からの投稿を執筆しました。</span><span class="sxs-lookup"><span data-stu-id="27942-114">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="27942-115">コメントセクションのユーザーからのフィードバックに基づいて改善されました。</span><span class="sxs-lookup"><span data-stu-id="27942-115">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="27942-116">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="27942-116">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="27942-117">データベースを設定する</span><span class="sxs-lookup"><span data-stu-id="27942-117">Set up the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27942-118">前提条件</span><span class="sxs-lookup"><span data-stu-id="27942-118">Prerequisites</span></span>

[<span data-ttu-id="27942-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="27942-119">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a><span data-ttu-id="27942-120">データベースを設定する</span><span class="sxs-lookup"><span data-stu-id="27942-120">Set up the database</span></span>

<span data-ttu-id="27942-121">既存のデータベースを使用する環境を模倣するには、まず、事前に入力されたデータを含むデータベースを作成し、次にデータベースに接続する web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="27942-121">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="27942-122">このチュートリアルは、Visual Studio 2017 で LocalDB を使用して開発されました。</span><span class="sxs-lookup"><span data-stu-id="27942-122">This tutorial was developed using LocalDB with Visual Studio 2017.</span></span> <span data-ttu-id="27942-123">LocalDB ではなく既存のデータベースサーバーを使用できますが、Visual studio のバージョンとデータベースの種類によっては、Visual Studio のすべてのデータツールがサポートされていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="27942-123">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="27942-124">データベースでツールを使用できない場合は、データベースの管理スイート内でデータベース固有の手順の一部を実行することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="27942-124">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="27942-125">お使いのバージョンの Visual Studio のデータベースツールに問題がある場合は、最新バージョンのデータベースツールがインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="27942-125">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="27942-126">データベースツールの更新またはインストールの詳細については、「 [Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27942-126">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="27942-127">Visual Studio を起動し、 **SQL Server データベースプロジェクト**を作成します。</span><span class="sxs-lookup"><span data-stu-id="27942-127">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="27942-128">**プロジェクトに名前を指定**します。</span><span class="sxs-lookup"><span data-stu-id="27942-128">Name the project **ContosoUniversityData**.</span></span>

![データベースプロジェクトの作成](setting-up-database/_static/image1.png)

<span data-ttu-id="27942-130">これで、空のデータベースプロジェクトが作成されました。</span><span class="sxs-lookup"><span data-stu-id="27942-130">You now have an empty database project.</span></span> <span data-ttu-id="27942-131">このデータベースを Azure にデプロイできるようにするには、プロジェクトのターゲットプラットフォームとして Azure SQL Database を設定します。</span><span class="sxs-lookup"><span data-stu-id="27942-131">To make sure that you can deploy this database to Azure, you'll set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="27942-132">ターゲットプラットフォームを設定しても、実際にはデータベースはデプロイされません。これは、データベースプロジェクトが、データベースの設計がターゲットプラットフォームと互換性があることを確認することのみを意味します。</span><span class="sxs-lookup"><span data-stu-id="27942-132">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="27942-133">ターゲットプラットフォームを設定するには、プロジェクトの**プロパティ**を開き、ターゲットプラットフォームの **[Microsoft Azure SQL Database]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="27942-133">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

<span data-ttu-id="27942-134">このチュートリアルに必要なテーブルを作成するには、テーブルを定義する SQL スクリプトを追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-134">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="27942-135">プロジェクトを右クリックし、新しい項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-135">Right-click your project and add a new item.</span></span> <span data-ttu-id="27942-136">テーブル**とビュー** > **テーブル**を選択し、「 *Student*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="27942-136">Select **Tables and Views** > **Table** and name it *Student*.</span></span>

<span data-ttu-id="27942-137">テーブルファイルで、T-sql コマンドを次のコードに置き換えて、テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="27942-137">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="27942-138">デザインウィンドウがコードと自動的に同期することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="27942-138">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="27942-139">コードまたはデザイナーを使用して作業することができます。</span><span class="sxs-lookup"><span data-stu-id="27942-139">You can work with either the code or designer.</span></span>

![コードとデザインを表示する](setting-up-database/_static/image5.png)

<span data-ttu-id="27942-141">別のテーブルを追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-141">Add another table.</span></span> <span data-ttu-id="27942-142">今回は、Course という名前を使用して、次の T-sql コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="27942-142">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="27942-143">さらにもう一度繰り返して、登録という名前のテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="27942-143">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="27942-144">データベースを配置した後に実行されるスクリプトを使用して、データベースにデータを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="27942-144">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="27942-145">配置後スクリプトをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-145">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="27942-146">プロジェクトを右クリックし、新しい項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-146">Right-click your project and add a new item.</span></span> <span data-ttu-id="27942-147">**配置後スクリプト** > **ユーザースクリプト**を選択します。</span><span class="sxs-lookup"><span data-stu-id="27942-147">Select **User Scripts** > **Post-Deployment Script**.</span></span> <span data-ttu-id="27942-148">既定の名前を使用できます。</span><span class="sxs-lookup"><span data-stu-id="27942-148">You can use the default name.</span></span>

<span data-ttu-id="27942-149">次の T-sql コードを配置後スクリプトに追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-149">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="27942-150">このスクリプトは、一致するレコードが見つからない場合に、単にデータベースにデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="27942-150">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="27942-151">データベースに入力したデータを上書きしたり削除したりすることはありません。</span><span class="sxs-lookup"><span data-stu-id="27942-151">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="27942-152">配置後スクリプトは、データベースプロジェクトを配置するたびに実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="27942-152">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="27942-153">このため、このスクリプトを記述するときは、要件を慎重に検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="27942-153">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="27942-154">場合によっては、プロジェクトが配置されるたびに既知のデータセットからやり直すことが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="27942-154">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="27942-155">それ以外の場合は、既存のデータを変更しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="27942-155">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="27942-156">要件に基づいて、配置後スクリプトが必要か、スクリプトに含める必要があるものかを決定できます。</span><span class="sxs-lookup"><span data-stu-id="27942-156">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="27942-157">配置後スクリプトを使用したデータベースの設定の詳細については、「 [SQL Server データベースプロジェクトにデータを含める](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27942-157">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="27942-158">これで、4つの SQL スクリプトファイルが作成されましたが、実際のテーブルはありません。</span><span class="sxs-lookup"><span data-stu-id="27942-158">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="27942-159">これで、データベースプロジェクトを localdb にデプロイする準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="27942-159">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="27942-160">Visual Studio で、[スタート] ボタン (または F5 キー) をクリックして、データベースプロジェクトをビルドして配置します。</span><span class="sxs-lookup"><span data-stu-id="27942-160">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="27942-161">**[出力]** タブを確認して、ビルドと配置が成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="27942-161">Check the **Output** tab to verify that the build and deployment succeeded.</span></span>

<span data-ttu-id="27942-162">新しいデータベースが作成されたことを確認するには、 **SQL Server オブジェクトエクスプローラー**を開き、正しいローカルデータベースサーバー (この場合は**localdb)** でプロジェクトの名前を探します。</span><span class="sxs-lookup"><span data-stu-id="27942-162">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV13**).</span></span>

<span data-ttu-id="27942-163">テーブルにデータが入力されていることを確認するには、テーブルを右クリックし、 **[データの表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="27942-163">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![テーブルデータの表示](setting-up-database/_static/image9.png)

<span data-ttu-id="27942-165">テーブルデータの編集可能なビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="27942-165">An editable view of the table data is displayed.</span></span> <span data-ttu-id="27942-166">たとえば、[**テーブル** > **dbo. course** > **データを表示**する] を選択した場合は、3つの列 (**コース**、**タイトル**、および**クレジット**) と4つの行を含むテーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="27942-166">For example, if you select **Tables** > **dbo.course** > **View Data**, you see a table with three columns (**Course**, **Title**, and **Credits**) and four rows.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27942-167">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="27942-167">Additional resources</span></span>

<span data-ttu-id="27942-168">Code First 開発の入門例については、「[はじめに with ASP.NET MVC 5](../introduction/getting-started.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27942-168">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="27942-169">より高度な例については、「 [ASP.NET MVC 4 アプリの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27942-169">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="27942-170">使用する Entity Framework 方法の選択に関するガイダンスについては、「[開発方法の Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27942-170">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27942-171">次のステップ</span><span class="sxs-lookup"><span data-stu-id="27942-171">Next steps</span></span>

<span data-ttu-id="27942-172">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="27942-172">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="27942-173">データベースを設定する</span><span class="sxs-lookup"><span data-stu-id="27942-173">Set up the database</span></span>

<span data-ttu-id="27942-174">次のチュートリアルに進み、web アプリケーションとデータモデルを作成する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="27942-174">Advance to the next tutorial to learn how to create the web application and data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="27942-175">Web アプリケーションとデータモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="27942-175">Create the web application and data models</span></span>](creating-the-web-application.md)
