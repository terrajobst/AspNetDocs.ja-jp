---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'チュートリアル: ASP.NET MVC を使用して EF Database First 用の Web アプリケーションとデータモデルを作成する'
description: このチュートリアルでは、web アプリケーションを作成し、データベーステーブルに基づいてデータモデルを生成する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499528"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="3592a-103">チュートリアル: ASP.NET MVC を使用して EF Database First 用の Web アプリケーションとデータモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="3592a-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="3592a-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3592a-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="3592a-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3592a-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="3592a-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="3592a-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="3592a-107">このチュートリアルでは、web アプリケーションを作成し、データベーステーブルに基づいてデータモデルを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3592a-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="3592a-108">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="3592a-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3592a-109">ASP.NET Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="3592a-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="3592a-110">モデルを生成する</span><span class="sxs-lookup"><span data-stu-id="3592a-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3592a-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="3592a-111">Prerequisites</span></span>

* [<span data-ttu-id="3592a-112">MVC 5 を使用した Entity Framework 6 Database First の概要</span><span class="sxs-lookup"><span data-stu-id="3592a-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="3592a-113">ASP.NET Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="3592a-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="3592a-114">新しいソリューションまたはデータベースプロジェクトと同じソリューションのどちらかで、Visual Studio で新しいプロジェクトを作成し、 **ASP.NET Web アプリケーション**テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="3592a-115">プロジェクトに**ContosoSite**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="3592a-115">Name the project **ContosoSite**.</span></span>

![プロジェクトの作成](creating-the-web-application/_static/image1.png)

<span data-ttu-id="3592a-117">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-117">Click **OK**.</span></span>

<span data-ttu-id="3592a-118">New ASP.NET プロジェクト ウィンドウで、 **MVC** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="3592a-119">ここでは、クラウドにアプリケーションを後でデプロイするため、[クラウド] オプション**でホスト**をクリアできます。</span><span class="sxs-lookup"><span data-stu-id="3592a-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="3592a-120">**[OK]** をクリックしてアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="3592a-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="3592a-121">既定のファイルとフォルダーを使用してプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3592a-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="3592a-122">このチュートリアルでは Entity Framework 6 を使用します。</span><span class="sxs-lookup"><span data-stu-id="3592a-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="3592a-123">[NuGet パッケージの管理] ウィンドウで、プロジェクトの Entity Framework のバージョンを再確認できます。</span><span class="sxs-lookup"><span data-stu-id="3592a-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="3592a-124">必要に応じて、Entity Framework のバージョンを更新します。</span><span class="sxs-lookup"><span data-stu-id="3592a-124">If necessary, update your version of Entity Framework.</span></span>

![バージョンの表示](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="3592a-126">モデルを生成する</span><span class="sxs-lookup"><span data-stu-id="3592a-126">Generate the models</span></span>

<span data-ttu-id="3592a-127">次に、データベーステーブルから Entity Framework モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3592a-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="3592a-128">これらのモデルは、データを操作するために使用するクラスです。</span><span class="sxs-lookup"><span data-stu-id="3592a-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="3592a-129">各モデルは、データベース内のテーブルをミラー化し、テーブル内の列に対応するプロパティを格納します。</span><span class="sxs-lookup"><span data-stu-id="3592a-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="3592a-130">**[モデル]** フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="3592a-131">新しい項目の追加 ウィンドウで、左ペインの **データ** を選択し、中央のウィンドウのオプションから**Entity Data Model を ADO.NET**します。</span><span class="sxs-lookup"><span data-stu-id="3592a-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="3592a-132">新しいモデルファイルに**ContosoModel**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="3592a-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="3592a-133">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-133">Click **Add**.</span></span>

<span data-ttu-id="3592a-134">Entity Data Model ウィザードで、 **[データベースから EF Designer]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="3592a-135">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-135">Click **Next**.</span></span>

<span data-ttu-id="3592a-136">開発環境内にデータベース接続が定義されている場合は、これらの接続のいずれかが事前に選択されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3592a-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="3592a-137">ただし、このチュートリアルの最初の部分で作成したデータベースへの新しい接続を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3592a-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="3592a-138">**[新しい接続]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="3592a-139">接続プロパティウィンドウで、データベースが作成されたローカルサーバーの名前を指定します (この場合は **(localdb)、projectsv13**)。</span><span class="sxs-lookup"><span data-stu-id="3592a-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="3592a-140">サーバー名を指定した後、使用可能なデータベースからコンテキストデータを選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![接続プロパティの設定](creating-the-web-application/_static/image8.png)

<span data-ttu-id="3592a-142">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-142">Click **OK**.</span></span>

<span data-ttu-id="3592a-143">これで、正しい接続プロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3592a-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="3592a-144">Web.config ファイルでは、接続の既定の名前を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3592a-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="3592a-145">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-145">Click **Next**.</span></span>

<span data-ttu-id="3592a-146">Entity Framework の最新バージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3592a-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="3592a-147">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-147">Click **Next**.</span></span>

<span data-ttu-id="3592a-148">**[テーブル]** を選択すると、3つのテーブルすべてに対してモデルが生成されます。</span><span class="sxs-lookup"><span data-stu-id="3592a-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="3592a-149">**[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3592a-149">Click **Finish**.</span></span>

<span data-ttu-id="3592a-150">セキュリティの警告が表示された場合は、 **[OK]** を選択してテンプレートの実行を続行します。</span><span class="sxs-lookup"><span data-stu-id="3592a-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="3592a-151">モデルはデータベーステーブルから生成され、テーブル間のプロパティとリレーションシップを示すダイアグラムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3592a-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![モデルの図](creating-the-web-application/_static/image11.png)

<span data-ttu-id="3592a-153">[モデル] フォルダーには、データベースから生成されたモデルに関連する多数の新しいファイルが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3592a-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="3592a-154">**ContosoModel.Context.cs**ファイルには、 **dbcontext**クラスから派生したクラスが含まれており、データベーステーブルに対応する各モデルクラスのプロパティを提供します。</span><span class="sxs-lookup"><span data-stu-id="3592a-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="3592a-155">**Course.cs**、 **Enrollment.cs**、および**Student.cs**の各ファイルには、databases テーブルを表すモデルクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3592a-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="3592a-156">スキャフォールディングを操作するときは、コンテキストクラスとモデルクラスの両方を使用します。</span><span class="sxs-lookup"><span data-stu-id="3592a-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="3592a-157">このチュートリアルを続行する前に、プロジェクトをビルドしてください。</span><span class="sxs-lookup"><span data-stu-id="3592a-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="3592a-158">次のセクションでは、データモデルに基づいてコードを生成しますが、プロジェクトがビルドされていない場合は、そのセクションは機能しません。</span><span class="sxs-lookup"><span data-stu-id="3592a-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3592a-159">次のステップ</span><span class="sxs-lookup"><span data-stu-id="3592a-159">Next steps</span></span>

<span data-ttu-id="3592a-160">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="3592a-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3592a-161">ASP.NET web アプリを作成しました</span><span class="sxs-lookup"><span data-stu-id="3592a-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="3592a-162">モデルが生成されました</span><span class="sxs-lookup"><span data-stu-id="3592a-162">Generated the models</span></span>

<span data-ttu-id="3592a-163">次のチュートリアルに進み、データモデルに基づいてコードを生成する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="3592a-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3592a-164">ビューの生成</span><span class="sxs-lookup"><span data-stu-id="3592a-164">Generating views</span></span>](generating-views.md)
