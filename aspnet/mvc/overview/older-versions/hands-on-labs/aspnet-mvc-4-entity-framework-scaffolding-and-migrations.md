---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework スキャフォールディングと移行 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 コントローラーの方法に慣れている場合、またはハンズオンラボ&quot; &quot;ヘルパー、フォーム、検証を完了している場合は、以下の点に注意する必要があります...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484642"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="3d494-103">ASP.NET MVC 4 Entity Framework スキャフォールディングと移行</span><span class="sxs-lookup"><span data-stu-id="3d494-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="3d494-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="3d494-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="3d494-105">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="3d494-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="3d494-106">ASP.NET MVC 4 コントローラーの方法に慣れている場合、またはハンズオンラボ&quot; &quot;ヘルパー、フォーム、および検証を完了している場合は、アプリケーション間で繰り返されるデータエンティティを作成、更新、一覧表示、および削除するロジックの多くに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d494-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="3d494-107">これに触れないと、モデルに操作するクラスが複数ある場合、各エンティティ操作の POST アクションメソッドと GET アクションメソッドの作成にかなりの時間がかかる可能性があります。また、各ビューも同様です。</span><span class="sxs-lookup"><span data-stu-id="3d494-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="3d494-108">このラボでは、ASP.NET MVC 4 スキャフォールディングを使用して、アプリケーションの CRUD (作成、読み取り、更新、および削除) のベースラインを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3d494-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="3d494-109">単純なモデルクラスから開始し、1行のコードを記述せずに、すべての CRUD 操作と、必要なすべてのビューを格納するコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d494-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="3d494-110">単純なソリューションをビルドして実行すると、アプリケーションデータベースが生成され、データ操作用の MVC ロジックとビューが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="3d494-111">さらに、Entity Framework の移行を使用して、アプリケーション全体でモデルの更新を実行することがいかに簡単であるかについても説明します。</span><span class="sxs-lookup"><span data-stu-id="3d494-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="3d494-112">Entity Framework の移行では、簡単な手順でモデルを変更した後にデータベースを変更できます。</span><span class="sxs-lookup"><span data-stu-id="3d494-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="3d494-113">これらすべてを念頭に置いて、ASP.NET MVC 4 の最新の機能を活用して、web アプリケーションをより効率的に構築して管理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="3d494-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="3d494-114">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="3d494-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="3d494-115">このラボに固有のプロジェクトは、 [ASP.NET MVC 4 Entity Framework のスキャフォールディングと移行](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="3d494-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3d494-116">目標</span><span class="sxs-lookup"><span data-stu-id="3d494-116">Objectives</span></span>

<span data-ttu-id="3d494-117">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="3d494-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="3d494-118">コントローラーで CRUD 操作に ASP.NET スキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="3d494-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="3d494-119">Entity Framework の移行を使用してデータベースモデルを変更します。</span><span class="sxs-lookup"><span data-stu-id="3d494-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3d494-120">前提条件</span><span class="sxs-lookup"><span data-stu-id="3d494-120">Prerequisites</span></span>

<span data-ttu-id="3d494-121">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="3d494-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="3d494-122">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="3d494-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3d494-123">セットアップ</span><span class="sxs-lookup"><span data-stu-id="3d494-123">Setup</span></span>

<span data-ttu-id="3d494-124">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="3d494-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="3d494-125">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="3d494-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="3d494-126">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="3d494-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="3d494-127">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 B: コードスニペット](#AppendixB)&quot;の使用」 &quot;参照してください。</span><span class="sxs-lookup"><span data-stu-id="3d494-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3d494-128">手順</span><span class="sxs-lookup"><span data-stu-id="3d494-128">Exercises</span></span>

<span data-ttu-id="3d494-129">次の演習では、このハンズオンラボを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d494-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="3d494-130">Entity Framework 移行での ASP.NET MVC 4 スキャフォールディングの使用</span><span class="sxs-lookup"><span data-stu-id="3d494-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="3d494-131">この演習には、演習の完了後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="3d494-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="3d494-132">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="3d494-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="3d494-133">このラボの推定所要時間: **30 分**</span><span class="sxs-lookup"><span data-stu-id="3d494-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="3d494-134">演習 1: Entity Framework 移行での ASP.NET MVC 4 スキャフォールディングの使用</span><span class="sxs-lookup"><span data-stu-id="3d494-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="3d494-135">ASP.NET MVC スキャフォールディングは、CRUD 操作を標準化された方法で生成し、アプリケーションがデータベース層と対話できるようにするために必要なロジックを作成するための簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="3d494-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="3d494-136">この演習では、ASP.NET MVC 4 スキャフォールディングを code first と共に使用して CRUD メソッドを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3d494-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="3d494-137">次に、Entity Framework の移行を使用して、データベースの変更を適用してモデルを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3d494-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="3d494-138">タスク 1-スキャフォールディングを使用して新しい ASP.NET MVC 4 プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3d494-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="3d494-139">まだ開いていない場合は、 **Visual Studio 2012**を起動します。</span><span class="sxs-lookup"><span data-stu-id="3d494-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="3d494-140">ファイルの選択 **|新しいプロジェクト**。</span><span class="sxs-lookup"><span data-stu-id="3d494-140">Select **File | New Project**.</span></span> <span data-ttu-id="3d494-141">[新しいプロジェクト] ダイアログで、[ **Visual C# |] を選択します。[Web** ] セクションで、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="3d494-142">プロジェクトに**MVC4andEFMigrations**という名前を設定し、このラボの [location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** ] フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="3d494-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="3d494-143">**[ソリューション名]** を **[開始]** に設定し、 **[ソリューションのディレクトリを作成]** する がオンになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3d494-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="3d494-144">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-144">Click **OK**.</span></span>

    <span data-ttu-id="3d494-145">![[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="3d494-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="3d494-146">*[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="3d494-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="3d494-147">**[新しい ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション**] テンプレートを選択し、 **Razor**が選択した**ビューエンジン**であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3d494-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="3d494-148">**[OK]** をクリックしてプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d494-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="3d494-149">![新しい ASP.NET MVC 4 インターネットアプリケーション](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新しい ASP.NET MVC 4 インターネットアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="3d494-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="3d494-150">*新しい ASP.NET MVC 4 インターネットアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="3d494-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="3d494-151">ソリューションエクスプローラーで、**モデル** を右クリックし、追加 を選択します。 **クラス**を作成して、単純なクラス (POCO) を作成します。</span><span class="sxs-lookup"><span data-stu-id="3d494-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="3d494-152">「 **Person** 」という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="3d494-153">Person クラスを開き、次のプロパティを挿入します。</span><span class="sxs-lookup"><span data-stu-id="3d494-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="3d494-154">(コードスニペット- *ASP.NET MVC 4 および Entity Framework 移行-Ex1 Person プロパティ*)</span><span class="sxs-lookup"><span data-stu-id="3d494-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="3d494-155">[ビルド] をクリックします。 **ソリューションをビルド**して変更を保存し、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="3d494-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="3d494-156">![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "アプリケーションのビルド")</span><span class="sxs-lookup"><span data-stu-id="3d494-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="3d494-157">*アプリケーションのビルド*</span><span class="sxs-lookup"><span data-stu-id="3d494-157">*Building the Application*</span></span>
7. <span data-ttu-id="3d494-158">ソリューションエクスプローラーで、controllers フォルダーを右クリックし、[追加] を選択します。 **コントローラー**。</span><span class="sxs-lookup"><span data-stu-id="3d494-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="3d494-159">コントローラーに「*個人コントローラー* 」という名前を付け、次の値を使用して**スキャフォールディングオプション**を完成させます。</span><span class="sxs-lookup"><span data-stu-id="3d494-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="3d494-160">**[テンプレート]** ボックスの一覧で、Entity Framework オプション**を使用して、読み取り/書き込みアクションとビューを含む MVC コントローラー**を選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="3d494-161">**[モデルクラス]** ボックスの一覧で、 **Person**クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="3d494-162">**[データコンテキストクラス]** の一覧で [ **&lt;新しいデータコンテキスト...&gt;** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="3d494-163">任意の名前を選択し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="3d494-164">**[ビュー]** ドロップダウンリストで、 **[Razor]** が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3d494-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="3d494-165">![スキャフォールディングを使用した Person コントローラーの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "スキャフォールディングを使用した Person コントローラーの追加")</span><span class="sxs-lookup"><span data-stu-id="3d494-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="3d494-166">*スキャフォールディングを使用した Person コントローラーの追加*</span><span class="sxs-lookup"><span data-stu-id="3d494-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="3d494-167">**[追加]** をクリックして、スキャフォールディングを持つユーザーの新しいコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d494-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="3d494-168">これで、コントローラーアクションとビューが生成されました。</span><span class="sxs-lookup"><span data-stu-id="3d494-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="3d494-169">![スキャフォールディングを使用して Person コントローラーを作成した後](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "スキャフォールディングを使用して Person コントローラーを作成した後")</span><span class="sxs-lookup"><span data-stu-id="3d494-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="3d494-170">*スキャフォールディングを使用して Person コントローラーを作成した後*</span><span class="sxs-lookup"><span data-stu-id="3d494-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="3d494-171">[**個人] コントローラー**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="3d494-171">Open **PersonController** class.</span></span> <span data-ttu-id="3d494-172">完全な CRUD アクションメソッドが自動的に生成されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3d494-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="3d494-173">![Person コントローラー内](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Person コントローラー内")</span><span class="sxs-lookup"><span data-stu-id="3d494-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="3d494-174">*Person コントローラー内*</span><span class="sxs-lookup"><span data-stu-id="3d494-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="3d494-175">タスク 2-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="3d494-175">Task 2- Running the application</span></span>

<span data-ttu-id="3d494-176">この時点では、データベースはまだ作成されていません。</span><span class="sxs-lookup"><span data-stu-id="3d494-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="3d494-177">このタスクでは、初めてアプリケーションを実行し、CRUD 操作をテストします。</span><span class="sxs-lookup"><span data-stu-id="3d494-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="3d494-178">データベースは Code First を使用してすぐに作成されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="3d494-179">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="3d494-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="3d494-180">ブラウザーで、URL に **/person**を追加して、[person] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="3d494-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="3d494-181">![アプリケーションの初回実行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "アプリケーションの初回実行")</span><span class="sxs-lookup"><span data-stu-id="3d494-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="3d494-182">*アプリケーション: 最初の実行*</span><span class="sxs-lookup"><span data-stu-id="3d494-182">*Application: first run*</span></span>
3. <span data-ttu-id="3d494-183">ここでは、ユーザーのページを探索し、CRUD 操作をテストします。</span><span class="sxs-lookup"><span data-stu-id="3d494-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="3d494-184">**[新規作成]** をクリックして、新しいユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3d494-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="3d494-185">名と姓を入力し、 **[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="3d494-186">![新しいユーザーの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "新しいユーザーの追加")</span><span class="sxs-lookup"><span data-stu-id="3d494-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="3d494-187">*新しいユーザーの追加*</span><span class="sxs-lookup"><span data-stu-id="3d494-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="3d494-188">ユーザーの一覧で、アイテムの削除、編集、または追加を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="3d494-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="3d494-189">![個人一覧](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "個人一覧")</span><span class="sxs-lookup"><span data-stu-id="3d494-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="3d494-190">*個人一覧*</span><span class="sxs-lookup"><span data-stu-id="3d494-190">*Person list*</span></span>
    3. <span data-ttu-id="3d494-191">**[詳細]** をクリックすると、個人の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="3d494-192">![個人の詳細](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "個人の詳細")</span><span class="sxs-lookup"><span data-stu-id="3d494-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="3d494-193">*個人の詳細*</span><span class="sxs-lookup"><span data-stu-id="3d494-193">*Person's details*</span></span>
4. <span data-ttu-id="3d494-194">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="3d494-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="3d494-195">アプリケーション全体で person エンティティの CRUD 全体が作成されていることに注意してください。つまり、モデルからビューまで、1行のコードを記述する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3d494-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="3d494-196">タスク 3-Entity Framework の移行を使用してデータベースを更新する</span><span class="sxs-lookup"><span data-stu-id="3d494-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="3d494-197">このタスクでは、Entity Framework の移行を使用してデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="3d494-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="3d494-198">Entity Framework 移行機能を使用して、モデルを変更し、データベースの変更を反映することがいかに簡単であるかがわかります。</span><span class="sxs-lookup"><span data-stu-id="3d494-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="3d494-199">パッケージマネージャーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="3d494-199">Open the Package Manager Console.</span></span> <span data-ttu-id="3d494-200">**[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="3d494-201">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="3d494-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="3d494-202">PMC</span><span class="sxs-lookup"><span data-stu-id="3d494-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="3d494-203">![移行の有効化](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "移行を有効にする")</span><span class="sxs-lookup"><span data-stu-id="3d494-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="3d494-204">*移行の有効化*</span><span class="sxs-lookup"><span data-stu-id="3d494-204">*Enabling migrations*</span></span>

    <span data-ttu-id="3d494-205">[移行の有効化] コマンドを実行すると、**移行**フォルダーが作成されます。このフォルダーには、データベースを初期化するスクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3d494-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="3d494-206">![移行フォルダー](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "移行フォルダー")</span><span class="sxs-lookup"><span data-stu-id="3d494-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="3d494-207">*移行フォルダー*</span><span class="sxs-lookup"><span data-stu-id="3d494-207">*Migrations folder*</span></span>
3. <span data-ttu-id="3d494-208">[移行] フォルダーの**Configuration.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3d494-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="3d494-209">クラスコンストラクターを見つけて、 **AutomaticMigrationsEnabled**値を*true*に変更します。</span><span class="sxs-lookup"><span data-stu-id="3d494-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="3d494-210">Person クラスを開き、人名のミドルネームの属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="3d494-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="3d494-211">この新しい属性を使用して、モデルを変更します。</span><span class="sxs-lookup"><span data-stu-id="3d494-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="3d494-212">Build | を選択します。メニューの [ソリューションのビルド] をオンにして、アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="3d494-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="3d494-213">![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "アプリケーションのビルド")</span><span class="sxs-lookup"><span data-stu-id="3d494-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="3d494-214">*アプリケーションのビルド*</span><span class="sxs-lookup"><span data-stu-id="3d494-214">*Building the application*</span></span>
6. <span data-ttu-id="3d494-215">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="3d494-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="3d494-216">PMC</span><span class="sxs-lookup"><span data-stu-id="3d494-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="3d494-217">このコマンドにより、データオブジェクトの変更が検索され、それに応じてデータベースを変更するために必要なコマンドが追加されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="3d494-218">![ミドルネームの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "ミドルネームの追加")</span><span class="sxs-lookup"><span data-stu-id="3d494-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="3d494-219">*ミドルネームの追加*</span><span class="sxs-lookup"><span data-stu-id="3d494-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="3d494-220">Optional次のコマンドを実行すると、差分更新を使用して SQL スクリプトを生成できます。</span><span class="sxs-lookup"><span data-stu-id="3d494-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="3d494-221">これにより、データベースを手動で更新 (この場合は必要ありません) することができます。また、変更を他のデータベースに適用することもできます。</span><span class="sxs-lookup"><span data-stu-id="3d494-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="3d494-222">PMC</span><span class="sxs-lookup"><span data-stu-id="3d494-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="3d494-223">![SQL スクリプトの生成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL スクリプトを生成する")</span><span class="sxs-lookup"><span data-stu-id="3d494-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="3d494-224">*SQL スクリプトの生成*</span><span class="sxs-lookup"><span data-stu-id="3d494-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="3d494-225">![SQL スクリプトの更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL スクリプトの更新")</span><span class="sxs-lookup"><span data-stu-id="3d494-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="3d494-226">*SQL スクリプトの更新*</span><span class="sxs-lookup"><span data-stu-id="3d494-226">*SQL Script update*</span></span>
8. <span data-ttu-id="3d494-227">パッケージマネージャーコンソールで、次のコマンドを入力してデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="3d494-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="3d494-228">PMC</span><span class="sxs-lookup"><span data-stu-id="3d494-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="3d494-229">![データベースを更新しています](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "データベースの更新")</span><span class="sxs-lookup"><span data-stu-id="3d494-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="3d494-230">*データベースを更新しています*</span><span class="sxs-lookup"><span data-stu-id="3d494-230">*Updating the Database*</span></span>

    <span data-ttu-id="3d494-231">これに**より、Person テーブルの** **MiddleName**列が、 **Person**クラスの現在の定義に一致するように追加されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="3d494-232">データベースが更新されたら、コントローラーフォルダーを右クリックし、[追加] を選択します。Person コントローラーを再び追加するコントローラー (同じ値で完了します)。</span><span class="sxs-lookup"><span data-stu-id="3d494-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="3d494-233">これにより、既存のメソッドとビューが更新され、新しい属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="3d494-234">![コントローラー更新プログラムの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "コントローラー更新プログラムの追加")</span><span class="sxs-lookup"><span data-stu-id="3d494-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="3d494-235">*コントローラーを更新しています*</span><span class="sxs-lookup"><span data-stu-id="3d494-235">*Updating the controller*</span></span>
10. <span data-ttu-id="3d494-236">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-236">Click **Add**.</span></span> <span data-ttu-id="3d494-237">次に、 **PersonController.cs を上書き**する の値を選択し、**関連付けられているビューを上書き**します を選択し、 **OK**</span><span class="sxs-lookup"><span data-stu-id="3d494-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![コントローラーの上書きの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="3d494-239">*コントローラーを更新しています*</span><span class="sxs-lookup"><span data-stu-id="3d494-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="3d494-240">Task4-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="3d494-240">Task4- Running the application</span></span>

1. <span data-ttu-id="3d494-241">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="3d494-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="3d494-242">開く **/Person**。</span><span class="sxs-lookup"><span data-stu-id="3d494-242">Open **/Person**.</span></span> <span data-ttu-id="3d494-243">中央の [名前] 列が追加されたときに、データが保持されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3d494-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="3d494-244">![追加されたミドルネーム](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "追加されたミドルネーム")</span><span class="sxs-lookup"><span data-stu-id="3d494-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="3d494-245">*追加されたミドルネーム*</span><span class="sxs-lookup"><span data-stu-id="3d494-245">*Middle Name added*</span></span>
3. <span data-ttu-id="3d494-246">**[編集]** をクリックすると、現在のユーザーにミドルネームを追加できるようになります。</span><span class="sxs-lookup"><span data-stu-id="3d494-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="3d494-247">![ミドルネームエディション](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "ミドルネームエディション")</span><span class="sxs-lookup"><span data-stu-id="3d494-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3d494-248">まとめ</span><span class="sxs-lookup"><span data-stu-id="3d494-248">Summary</span></span>

<span data-ttu-id="3d494-249">このハンズオンラボでは、任意のモデルクラスを使用して ASP.NET MVC 4 スキャフォールディングで CRUD 操作を作成するための簡単な手順を学習しました。</span><span class="sxs-lookup"><span data-stu-id="3d494-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="3d494-250">次に、Entity Framework の移行を使用して、アプリケーションでエンドツーエンドの更新を実行する方法について説明しました。これは、データベースからビューへの更新です。</span><span class="sxs-lookup"><span data-stu-id="3d494-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="3d494-251">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="3d494-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="3d494-252">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3d494-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="3d494-253">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="3d494-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="3d494-254">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。</span><span class="sxs-lookup"><span data-stu-id="3d494-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="3d494-255">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="3d494-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="3d494-256">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-256">Click on **Install Now**.</span></span> <span data-ttu-id="3d494-257">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="3d494-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="3d494-258">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="3d494-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="3d494-259">![Visual Studio Express のインストール](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="3d494-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="3d494-260">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="3d494-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="3d494-261">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="3d494-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="3d494-263">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="3d494-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="3d494-264">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="3d494-264">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="3d494-266">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="3d494-266">*Installation progress*</span></span>
6. <span data-ttu-id="3d494-267">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-267">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="3d494-269">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="3d494-269">*Installation completed*</span></span>
7. <span data-ttu-id="3d494-270">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="3d494-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="3d494-271">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="3d494-273">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="3d494-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="3d494-274">付録 B: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="3d494-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="3d494-275">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="3d494-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="3d494-276">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="3d494-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="3d494-277">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="3d494-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="3d494-278">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="3d494-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="3d494-279">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="3d494-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="3d494-280">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="3d494-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="3d494-281">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="3d494-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="3d494-282">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="3d494-283">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="3d494-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="3d494-284">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="3d494-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="3d494-285">![スニペット名の入力を開始します](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="3d494-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="3d494-286">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="3d494-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="3d494-287">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="3d494-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="3d494-288">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="3d494-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="3d494-289">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="3d494-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="3d494-290">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="3d494-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="3d494-291">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="3d494-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="3d494-292">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="3d494-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="3d494-293">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="3d494-294">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="3d494-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="3d494-295">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="3d494-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="3d494-296">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="3d494-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="3d494-297">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="3d494-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="3d494-298">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="3d494-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
