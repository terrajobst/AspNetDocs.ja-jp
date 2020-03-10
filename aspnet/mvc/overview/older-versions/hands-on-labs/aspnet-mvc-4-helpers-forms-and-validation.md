---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 ヘルパー、フォーム、および検証 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 モデルとデータアクセスのハンズオンラボでは、データベースのデータを読み込んで表示しています。 このハンズオンラボでは、次のように追加します...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433792"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="50226-104">ASP.NET MVC 4 ヘルパー、フォーム、検証</span><span class="sxs-lookup"><span data-stu-id="50226-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="50226-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="50226-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="50226-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="50226-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="50226-107">**ASP.NET MVC 4 モデルとデータアクセス**のハンズオンラボでは、データベースのデータを読み込んで表示しています。</span><span class="sxs-lookup"><span data-stu-id="50226-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="50226-108">このハンズオンラボでは、このデータを編集する機能を**ミュージックストア**アプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="50226-109">この目標を念頭に置いて、最初に、アルバムの作成、読み取り、更新、削除 (CRUD) アクションをサポートするコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="50226-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="50226-110">ASP.NET MVC のスキャフォールディング機能を利用して、HTML テーブルにアルバムのプロパティを表示する、インデックスビューテンプレートを生成します。</span><span class="sxs-lookup"><span data-stu-id="50226-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="50226-111">このビューを強化するには、長い説明を切り捨てるカスタム HTML ヘルパーを追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="50226-112">その後、[編集] ビューと [作成] ビューを追加します。このビューでは、データベースのアルバムを変更でき、ドロップダウンなどのフォーム要素を使用できます。</span><span class="sxs-lookup"><span data-stu-id="50226-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="50226-113">最後に、ユーザーがアルバムを削除できるようにします。また、入力を検証することで間違ったデータを入力できないようにします。</span><span class="sxs-lookup"><span data-stu-id="50226-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="50226-114">このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="50226-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="50226-115">以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET mvc の基礎**となるハンズオンラボに進むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="50226-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="50226-116">このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="50226-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="50226-117">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="50226-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="50226-118">このラボに固有のプロジェクトは、 [ASP.NET MVC 4 のヘルパー、フォーム、および検証](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="50226-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="50226-119">目標</span><span class="sxs-lookup"><span data-stu-id="50226-119">Objectives</span></span>

<span data-ttu-id="50226-120">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="50226-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="50226-121">CRUD 操作をサポートするコントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="50226-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="50226-122">エンティティのプロパティを HTML テーブルに表示するためのインデックスビューの生成</span><span class="sxs-lookup"><span data-stu-id="50226-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="50226-123">カスタム HTML ヘルパーを追加する</span><span class="sxs-lookup"><span data-stu-id="50226-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="50226-124">編集ビューを作成およびカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="50226-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="50226-125">HTTP GET または HTTP POST 呼び出しのいずれかに対応するアクションメソッドを区別する</span><span class="sxs-lookup"><span data-stu-id="50226-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="50226-126">作成ビューを追加およびカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="50226-126">Add and customize a Create View</span></span>
- <span data-ttu-id="50226-127">エンティティの削除を処理する</span><span class="sxs-lookup"><span data-stu-id="50226-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="50226-128">ユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="50226-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="50226-129">前提条件</span><span class="sxs-lookup"><span data-stu-id="50226-129">Prerequisites</span></span>

<span data-ttu-id="50226-130">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="50226-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="50226-131">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="50226-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="50226-132">セットアップ</span><span class="sxs-lookup"><span data-stu-id="50226-132">Setup</span></span>

<span data-ttu-id="50226-133">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="50226-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="50226-134">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="50226-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="50226-135">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="50226-136">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 B: コードスニペット](#AppendixB)&quot;の使用」 &quot;参照してください。</span><span class="sxs-lookup"><span data-stu-id="50226-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="50226-137">手順</span><span class="sxs-lookup"><span data-stu-id="50226-137">Exercises</span></span>

<span data-ttu-id="50226-138">このハンズオンラボは、次の演習によって構成されています。</span><span class="sxs-lookup"><span data-stu-id="50226-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="50226-139">ストアマネージャーコントローラーとそのインデックスビューを作成する</span><span class="sxs-lookup"><span data-stu-id="50226-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="50226-140">HTML ヘルパーの追加</span><span class="sxs-lookup"><span data-stu-id="50226-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="50226-141">編集ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="50226-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="50226-142">作成ビューの追加</span><span class="sxs-lookup"><span data-stu-id="50226-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="50226-143">削除の処理</span><span class="sxs-lookup"><span data-stu-id="50226-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="50226-144">検証の追加</span><span class="sxs-lookup"><span data-stu-id="50226-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="50226-145">クライアント側での控えめな jQuery の使用</span><span class="sxs-lookup"><span data-stu-id="50226-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="50226-146">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="50226-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="50226-147">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="50226-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="50226-148">このラボの推定所要時間: **60 分**</span><span class="sxs-lookup"><span data-stu-id="50226-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="50226-149">演習 1: ストアマネージャーコントローラーとそのインデックスビューの作成</span><span class="sxs-lookup"><span data-stu-id="50226-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="50226-150">この演習では、CRUD 操作をサポートする新しいコントローラーを作成する方法、データベースからアルバムの一覧を返すようにインデックスアクションメソッドをカスタマイズする方法、最後に ASP.NET MVC のスキャフォールディングを利用してインデックスビューテンプレートを生成する方法について説明します。アルバムのプロパティを HTML テーブルに表示する機能。</span><span class="sxs-lookup"><span data-stu-id="50226-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="50226-151">タスク 1-StoreManagerController の作成</span><span class="sxs-lookup"><span data-stu-id="50226-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="50226-152">このタスクでは、CRUD 操作をサポートするために**StoreManagerController**という名前の新しいコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="50226-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="50226-153">**Source/Ex1-CreatingTheStoreManagerController/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="50226-154">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-155">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-156">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-157">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-158">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-159">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-160">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-161">新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-161">Add a new controller.</span></span> <span data-ttu-id="50226-162">これを行うには、ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** を選択して、 **[コントローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="50226-163">**コントローラー** **名**を**StoreManagerController**に変更し、 **[読み取り/書き込みアクションが空の MVC コントローラー]** オプションが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="50226-164">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-164">Click **Add**.</span></span>

    <span data-ttu-id="50226-165">![[コントローラーの追加] ダイアログ](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "[コントローラーの追加] ダイアログ")</span><span class="sxs-lookup"><span data-stu-id="50226-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="50226-166">*[コントローラーの追加] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="50226-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="50226-167">新しいコントローラークラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="50226-167">A new Controller class is generated.</span></span> <span data-ttu-id="50226-168">読み取り/書き込み用のアクションを追加するように指定したため、これらのスタブメソッドには、TODO コメントを入力して、アプリケーション固有のロジックを含めるよう求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="50226-169">タスク 2-StoreManager インデックスのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="50226-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="50226-170">このタスクでは、データベースからアルバムの一覧と共にビューを返すように、StoreManager インデックスアクションメソッドをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="50226-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="50226-171">StoreManagerController クラスに、次の*using*ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="50226-172">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 を使用した MvcMusicStore*)</span><span class="sxs-lookup"><span data-stu-id="50226-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="50226-173">MusicStoreEntities のインスタンスを保持するフィールドを**StoreManagerController**に追加**します。**</span><span class="sxs-lookup"><span data-stu-id="50226-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="50226-174">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="50226-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="50226-175">アルバムの一覧と共にビューを返すには、StoreManagerController Index アクションを実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="50226-176">コントローラーアクションロジックは、前に記述した StoreController のインデックスアクションと非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="50226-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="50226-177">LINQ を使用して、表示するジャンルとアーティストの情報を含むすべてのアルバムを取得します。</span><span class="sxs-lookup"><span data-stu-id="50226-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="50226-178">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 StoreManagerController Index*)</span><span class="sxs-lookup"><span data-stu-id="50226-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="50226-179">タスク 3-インデックスビューを作成する</span><span class="sxs-lookup"><span data-stu-id="50226-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="50226-180">このタスクでは、インデックスビューテンプレートを作成して、 **Storemanager**コントローラーによって返されたアルバムの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="50226-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="50226-181">新しいビューテンプレートを作成する前に、[**ビューの追加] ダイアログ**で使用する**アルバム**クラスが認識されるように、プロジェクトをビルドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="50226-182">Build | を選択します。 **MvcMusicStore をビルド**してプロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="50226-183">**Index**アクションメソッド内を右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="50226-184">**[ビューの追加]** ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="50226-185">![ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="50226-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="50226-186">*Index メソッド内からビューを追加する*</span><span class="sxs-lookup"><span data-stu-id="50226-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="50226-187">ビューの追加 ダイアログで、ビュー名が **インデックス** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="50226-188">**[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="50226-189">**[スキャフォールディング template]** ドロップダウンリストから **[List]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="50226-190">**ビューエンジン**を**Razor**に、その他のフィールドに既定値をそのまま使用し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="50226-191">![インデックスビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "インデックスビューの追加")</span><span class="sxs-lookup"><span data-stu-id="50226-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="50226-192">*インデックスビューの追加*</span><span class="sxs-lookup"><span data-stu-id="50226-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="50226-193">タスク 4-インデックスビューのスキャフォールディングのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="50226-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="50226-194">このタスクでは、ASP.NET MVC スキャフォールディング機能で作成された単純なビューテンプレートを調整して、必要なフィールドを表示するようにします。</span><span class="sxs-lookup"><span data-stu-id="50226-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="50226-195">ASP.NET MVC 内での**スキャフォールディング**のサポートにより、アルバムモデルのすべてのフィールドを一覧表示する簡易ビューテンプレートが生成されます。</span><span class="sxs-lookup"><span data-stu-id="50226-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="50226-196">**スキャフォールディング**は、厳密に型指定されたビューをすばやく開始するための簡単な方法を提供します。ビューテンプレートを手動で記述するのではなく、スキャフォールディングによって既定のテンプレートがすばやく生成され、生成されたコードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="50226-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="50226-197">作成されたコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-197">Review the code created.</span></span> <span data-ttu-id="50226-198">生成されたフィールドの一覧は、**スキャフォールディング**が表形式データを表示するために使用する次の HTML テーブルの一部になります。</span><span class="sxs-lookup"><span data-stu-id="50226-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="50226-199">**&lt;テーブル&gt;** コードを次のコードに置き換えて、**ジャンル**、**アーティスト**、**アルバムタイトル**、および**価格**フィールドのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="50226-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="50226-200">これにより、 **AlbumId**と**アルバムアートの URL**列が削除されます。</span><span class="sxs-lookup"><span data-stu-id="50226-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="50226-201">また、 **Artist.Name**と**Genre.Name**のリンクされたクラスプロパティを表示するように Genreid 列と artistid 列を変更し、 **Details**リンクを削除します。</span><span class="sxs-lookup"><span data-stu-id="50226-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="50226-202">次の説明を変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="50226-203">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="50226-204">このタスクでは、 **Storemanager** **インデックス**ビューテンプレートで、前の手順の設計に従ってアルバムの一覧が表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="50226-205">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-206">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-206">The project starts in the Home page.</span></span> <span data-ttu-id="50226-207">URL を「 **/storemanager** 」に変更して、アルバムの一覧が表示され **、タイトル**、**アーティスト**、**ジャンル**を表示していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="50226-208">![アルバムの一覧の参照](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "アルバムの一覧の参照")</span><span class="sxs-lookup"><span data-stu-id="50226-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="50226-209">*アルバムの一覧の参照*</span><span class="sxs-lookup"><span data-stu-id="50226-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="50226-210">演習 2: HTML ヘルパーの追加</span><span class="sxs-lookup"><span data-stu-id="50226-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="50226-211">StoreManager インデックスページには、考えられる問題が1つあります。 Title とアーティスト名のプロパティは、テーブルの書式設定を破棄するのに十分な長さであることが必要です。</span><span class="sxs-lookup"><span data-stu-id="50226-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="50226-212">この演習では、カスタム HTML ヘルパーを追加してそのテキストを切り捨てる方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="50226-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="50226-213">次の図では、小さなブラウザーサイズを使用すると、テキストの長さによって形式がどのように変更されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="50226-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="50226-214">![切り捨てられたテキストのないアルバムの一覧の参照](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "切り捨てられたテキストのないアルバムの一覧の参照")</span><span class="sxs-lookup"><span data-stu-id="50226-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="50226-215">*切り捨てられたテキストのないアルバムの一覧の参照*</span><span class="sxs-lookup"><span data-stu-id="50226-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="50226-216">タスク 1-HTML ヘルパーの拡張</span><span class="sxs-lookup"><span data-stu-id="50226-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="50226-217">このタスクでは、ASP.NET MVC ビュー内で公開されている**HTML**オブジェクトに新しいメソッドの**切り捨て**を追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="50226-218">これを行うには、ASP.NET MVC によって提供される組み込みの**System.web ヘルパー**クラスに**拡張メソッド**を実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="50226-219">**拡張メソッド**の詳細については、こちらの msdn 記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="50226-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="50226-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50226-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="50226-221">**Source/Ex2-アドオン**/フォルダーにある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="50226-222">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-223">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-224">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-225">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-226">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-227">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-228">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-229">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-230">StoreManager のインデックスビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="50226-231">これを行うには、ソリューションエクスプローラー **Views**  フォルダーを展開し、 **storemanager**を選択して、**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="50226-232"><strong>@model</strong>ディレクティブの下に次のコードを追加して、 <strong>Truncate</strong> helper メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="50226-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="50226-233">タスク 2-ページ内のテキストの切り捨て</span><span class="sxs-lookup"><span data-stu-id="50226-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="50226-234">このタスクでは、 **truncate**メソッドを使用して、ビューテンプレート内のテキストを切り捨てます。</span><span class="sxs-lookup"><span data-stu-id="50226-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="50226-235">StoreManager のインデックスビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="50226-236">これを行うには、ソリューションエクスプローラー **Views**  フォルダーを展開し、 **storemanager**を選択して、**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="50226-237">**アーティスト名**とアルバムの**タイトル**が表示されている行を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="50226-238">これを行うには、次の行を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="50226-239">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="50226-240">このタスクでは、 **Storemanager** **インデックス**ビューテンプレートによって、アルバムのタイトルとアーティスト名が切り詰められていることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="50226-241">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-242">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-242">The project starts in the Home page.</span></span> <span data-ttu-id="50226-243">URL を「 **/storemanager** 」に変更し、 **[タイトル]** 列と **[アーティスト]** 列の長いテキストが切り捨てられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="50226-244">![タイトルとアーティスト名の切り捨て](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "タイトルとアーティスト名の切り捨て")</span><span class="sxs-lookup"><span data-stu-id="50226-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="50226-245">*タイトルとアーティスト名が切り詰められました*</span><span class="sxs-lookup"><span data-stu-id="50226-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="50226-246">演習 3: 編集ビューの作成</span><span class="sxs-lookup"><span data-stu-id="50226-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="50226-247">この演習では、ストアマネージャーがアルバムを編集できるようにするフォームを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="50226-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="50226-248">**/StoreManager/Edit/id** URL (**id**は編集するアルバムの一意の id である) を参照するため、サーバーに対して HTTP GET 呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="50226-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="50226-249">Controller Edit action メソッドは、データベースから適切なアルバムを取得し、 **StoreManagerViewModel**オブジェクトを作成してそれをカプセル化します (さらに、アーティストとジャンルのリストを表示します)。その後、このオブジェクトをビューテンプレートに渡して、HTML ページをユーザーに戻します。</span><span class="sxs-lookup"><span data-stu-id="50226-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="50226-250">このページには、アルバムのプロパティを編集するためのテキストボックスとドロップダウンを含む **&lt;フォーム&gt;** 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="50226-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="50226-251">ユーザーがアルバムフォームの値を更新して **[保存]** ボタンをクリックすると、変更が **/StoreManager/Edit/id**にポストバックされて送信されます。URL は最後の呼び出しと同じままですが、ASP.NET MVC では、今度は HTTP POST であることが識別されます。そのため、別の編集アクションメソッド ( **[Httppost]** で修飾されたもの) を実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="50226-252">タスク 1-HTTP 取得の編集アクションメソッドを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="50226-253">このタスクでは、編集アクションメソッドの HTTP GET バージョンを実装して、適切なアルバムをデータベースから取得します。また、すべてのジャンルとアーティストのリストも取得します。</span><span class="sxs-lookup"><span data-stu-id="50226-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="50226-254">このデータは、最後のステップで定義されている**StoreManagerViewModel**オブジェクトにパッケージ化されます。これは、と共に応答を表示するためにビューテンプレートに渡されます。</span><span class="sxs-lookup"><span data-stu-id="50226-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="50226-255">**Source/Ex3-さくせいビュー/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="50226-256">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-257">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-258">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-259">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-260">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-261">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-262">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-263">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-264">**StoreManagerController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="50226-265">これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="50226-266">**HTTP-GET Edit** action メソッドを次のコードに置き換えて、適切な**アルバム**と**ジャンル**と**アーティスト**の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="50226-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="50226-267">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex3 STOREMANAGERCONTROLLER HTTP-編集アクションの取得*)</span><span class="sxs-lookup"><span data-stu-id="50226-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="50226-268">システムの**コレクション**ではなく、アーティストとジャンルに対して**System.web. Mvc** **selectlist**を使用しています。</span><span class="sxs-lookup"><span data-stu-id="50226-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="50226-269">**Selectlist**は、HTML ドロップダウンを設定し、現在の選択などを管理するための、すっきりした方法です。</span><span class="sxs-lookup"><span data-stu-id="50226-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="50226-270">コントローラーアクションでこれらのビューモデルオブジェクトをインスタンス化して後で設定すると、フォームの編集シナリオがすっきりします。</span><span class="sxs-lookup"><span data-stu-id="50226-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="50226-271">タスク 2-編集ビューの作成</span><span class="sxs-lookup"><span data-stu-id="50226-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="50226-272">このタスクでは、後でアルバムのプロパティを表示する編集ビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="50226-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="50226-273">編集ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="50226-273">Create the Edit View.</span></span> <span data-ttu-id="50226-274">これを行うには、アクションの **[編集]** メソッド内を右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="50226-275">[ビューの追加] ダイアログで、ビュー名が**Edit**であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="50226-276">厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[データクラスの表示]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="50226-277">**[スキャフォールディングテンプレート]** ドロップダウンから **[編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="50226-278">他のフィールドは既定値のままにして、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="50226-279">![編集ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "編集ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="50226-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="50226-280">*編集ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="50226-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="50226-281">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="50226-282">このタスクでは、 **Storemanager**の [ビューの**編集**] ページに、パラメーターとして渡されたアルバムのプロパティの値が表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="50226-283">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-284">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-284">The project starts in the Home page.</span></span> <span data-ttu-id="50226-285">URL を **/StoreManager/Edit/1**に変更し、渡されたアルバムのプロパティの値が表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="50226-286">![アルバムの編集ビューを閲覧する](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "アルバムの編集ビューを閲覧する")</span><span class="sxs-lookup"><span data-stu-id="50226-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="50226-287">*アルバムの編集ビューを閲覧する*</span><span class="sxs-lookup"><span data-stu-id="50226-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="50226-288">タスク 4-アルバムエディターテンプレートにドロップダウンを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="50226-289">このタスクでは、最後のタスクで作成されたビューテンプレートにドロップダウンを追加して、ユーザーがアーティストとジャンルの一覧から選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="50226-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="50226-290">すべての**アルバム**のフィールドセットコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="50226-291">アーティストとジャンルを選択するためのレンダードロップダウンに、 **Html の DropDownList**ヘルパーが追加されました。</span><span class="sxs-lookup"><span data-stu-id="50226-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="50226-292">**Html**に渡されるパラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="50226-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="50226-293">フォームフィールドの名前 ( **&quot;ArtistId&quot;** )。</span><span class="sxs-lookup"><span data-stu-id="50226-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="50226-294">ドロップダウンの値の**Selectlist** 。</span><span class="sxs-lookup"><span data-stu-id="50226-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="50226-295">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="50226-296">このタスクでは、 **Storemanager**の [ビューの**編集**] ページに、アーティストおよびジャンル ID のテキストフィールドではなくドロップダウンが表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="50226-297">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-298">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-298">The project starts in the Home page.</span></span> <span data-ttu-id="50226-299">URL を **/StoreManager/Edit/1**に変更して、アーティストと Genre ID のテキストフィールドではなくドロップダウンが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="50226-300">![ドロップダウンでアルバムの編集ビューを閲覧する](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "ドロップダウンでアルバムの編集ビューを閲覧する")</span><span class="sxs-lookup"><span data-stu-id="50226-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="50226-301">*アルバムの編集ビューを閲覧する、今回はドロップダウン*</span><span class="sxs-lookup"><span data-stu-id="50226-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="50226-302">タスク 6-HTTP ポスト編集アクションメソッドを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="50226-303">編集ビューが想定どおりに表示されたので、アルバムに加えられた変更を保存するには、HTTP POST Edit アクションメソッドを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="50226-304">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="50226-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="50226-305">**Controllers**フォルダーから**StoreManagerController**を開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="50226-306">**HTTP ポスト編集**アクションメソッドのコードを次のコードに置き換えます (置き換える必要があるメソッドは、2つのパラメーターを受け取るオーバーロードされたバージョンであることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="50226-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="50226-307">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex3 STOREMANAGERCONTROLLER HTTP-編集後のアクション*)</span><span class="sxs-lookup"><span data-stu-id="50226-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="50226-308">このメソッドは、ユーザーがビューの **[保存]** ボタンをクリックしたときに実行され、フォーム値の HTTP POST をサーバーに返して、データベースに保持します。</span><span class="sxs-lookup"><span data-stu-id="50226-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="50226-309">デコレータ **[Httppost]** は、これらの HTTP ポストシナリオに対してメソッドを使用する必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="50226-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="50226-310">このメソッドは、**アルバム**オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="50226-310">The method takes an **Album** object.</span></span> <span data-ttu-id="50226-311">ASP.NET MVC は、投稿された &lt;フォーム&gt; 値からアルバムオブジェクトを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="50226-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="50226-312">メソッドは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="50226-313">モデルが有効な場合:</span><span class="sxs-lookup"><span data-stu-id="50226-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="50226-314">コンテキストのアルバムエントリを更新して、変更されたオブジェクトとしてマークします。</span><span class="sxs-lookup"><span data-stu-id="50226-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="50226-315">変更を保存し、インデックスビューにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="50226-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="50226-316">モデルが有効でない場合は、ViewBag に**Genreid**と**artistid**が設定され、ユーザーが必要な更新を実行できるように、受信したアルバムオブジェクトを含むビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="50226-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="50226-317">タスク 7-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="50226-318">このタスクでは、 **Storemanager Edit** View ページが実際に更新されたアルバムデータをデータベースに保存することをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="50226-319">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-320">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-320">The project starts in the Home page.</span></span> <span data-ttu-id="50226-321">URL を **/StoreManager/Edit/1**に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="50226-322">アルバムのタイトルを **[読み込み]** に変更し、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="50226-323">アルバムの一覧でアルバムのタイトルが実際に変更されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="50226-324">![アルバムを更新する](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "アルバムを更新する")</span><span class="sxs-lookup"><span data-stu-id="50226-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="50226-325">*アルバムを更新する*</span><span class="sxs-lookup"><span data-stu-id="50226-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="50226-326">演習 4: Create ビューの追加</span><span class="sxs-lookup"><span data-stu-id="50226-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="50226-327">**StoreManagerController**が**編集**機能をサポートするようになったので、この演習では、ストアマネージャーが新しいアルバムをアプリケーションに追加できるように、Create View テンプレートを追加する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="50226-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="50226-328">編集機能を使用した場合と同様に、 **StoreManagerController**クラス内の2つの異なるメソッドを使用して作成シナリオを実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="50226-329">ストアマネージャーが最初に **/StoreManager/Create** URL にアクセスすると、1つのアクションメソッドで空のフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="50226-330">2番目のアクションメソッドでは、ストアマネージャーがフォーム内の **[保存]** ボタンをクリックして、 **/StoreManager/Create** URL に値を送信するというシナリオを処理します。</span><span class="sxs-lookup"><span data-stu-id="50226-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="50226-331">タスク 1-HTTP 取得の Create action メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="50226-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="50226-332">このタスクでは、Create action メソッドの HTTP GET バージョンを実装して、すべてのジャンルとアーティストの一覧を取得し、このデータを**StoreManagerViewModel**オブジェクトにパッケージ化します。これはビューテンプレートに渡されます。</span><span class="sxs-lookup"><span data-stu-id="50226-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="50226-333">**Source/Ex4-/begin** /folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="50226-334">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-335">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-336">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-337">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-338">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-339">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-340">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-341">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-342">**StoreManagerController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="50226-343">これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="50226-344">**Create** action メソッドのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="50226-345">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex4 STOREMANAGERCONTROLLER HTTP-Create アクションの取得*)</span><span class="sxs-lookup"><span data-stu-id="50226-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="50226-346">タスク 2-作成ビューの追加</span><span class="sxs-lookup"><span data-stu-id="50226-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="50226-347">このタスクでは、新しい (空の) アルバムフォームを表示する Create View テンプレートを追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="50226-348">**Create** action メソッド内を右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="50226-349">[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="50226-350">ビューの追加 ダイアログで、ビュー名が **作成** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="50226-351">**[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択し、 **[スキャフォールディングテンプレート]** ドロップダウンから **[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="50226-352">他のフィールドは既定値のままにして、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="50226-353">![作成ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view")</span><span class="sxs-lookup"><span data-stu-id="50226-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="50226-354">*Create ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="50226-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="50226-355">次に示すように、ドロップダウンリストを使用するように**Genreid**フィールドと**artistid**フィールドを更新します。</span><span class="sxs-lookup"><span data-stu-id="50226-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="50226-356">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="50226-357">このタスクでは、 **Storemanager**の [ビューの**作成**] ページに空のアルバムフォームが表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="50226-358">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-359">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-359">The project starts in the Home page.</span></span> <span data-ttu-id="50226-360">URL を **/StoreManager/Create**に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="50226-361">新しいアルバムのプロパティを入力するための空のフォームが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="50226-362">![空のフォームを持つビューを作成する](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "空のフォームを持つビューを作成する")</span><span class="sxs-lookup"><span data-stu-id="50226-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="50226-363">*空のフォームを持つビューを作成する*</span><span class="sxs-lookup"><span data-stu-id="50226-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="50226-364">タスク 4-HTTP ポスト作成アクションメソッドを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="50226-365">このタスクでは、ユーザーが **[保存]** ボタンをクリックしたときに呼び出される、Create action メソッドの HTTP POST バージョンを実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="50226-366">メソッドでは、新しいアルバムをデータベースに保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="50226-367">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="50226-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="50226-368">**StoreManagerController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="50226-369">これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="50226-370">**HTTP ポストの Create**アクションメソッドのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="50226-371">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex4 STOREMANAGERCONTROLLER HTTP-投稿作成アクション*)</span><span class="sxs-lookup"><span data-stu-id="50226-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="50226-372">作成アクションは、前の編集アクションメソッドと非常に似ていますが、オブジェクトを変更済みとして設定するのではなく、コンテキストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="50226-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="50226-373">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="50226-374">このタスクでは、 **Storemanager**の [ビューの作成] ページを使用して、新しいアルバムを作成し、Storemanager インデックスビューにリダイレクトすることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="50226-375">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-376">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-376">The project starts in the Home page.</span></span> <span data-ttu-id="50226-377">URL を **/StoreManager/Create**に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="50226-378">次の図に示すように、すべてのフォームフィールドに新しいアルバムのデータを入力します。</span><span class="sxs-lookup"><span data-stu-id="50226-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="50226-379">![アルバムを作成する](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "アルバムを作成する")</span><span class="sxs-lookup"><span data-stu-id="50226-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="50226-380">*アルバムを作成する*</span><span class="sxs-lookup"><span data-stu-id="50226-380">*Creating an Album*</span></span>
3. <span data-ttu-id="50226-381">作成したばかりの新しいアルバムを含む StoreManager インデックスビューにリダイレクトされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="50226-382">![新しく作成されたアルバム](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "新しく作成されたアルバム")</span><span class="sxs-lookup"><span data-stu-id="50226-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="50226-383">*新しく作成されたアルバム*</span><span class="sxs-lookup"><span data-stu-id="50226-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="50226-384">演習 5: 削除の処理</span><span class="sxs-lookup"><span data-stu-id="50226-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="50226-385">アルバムを削除する機能はまだ実装されていません。</span><span class="sxs-lookup"><span data-stu-id="50226-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="50226-386">この演習では、このことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="50226-386">This is what this exercise will be about.</span></span> <span data-ttu-id="50226-387">前と同様に、 **StoreManagerController**クラス内の2つの異なるメソッドを使用して、削除シナリオを実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="50226-388">1つのアクションメソッドで確認フォームが表示される</span><span class="sxs-lookup"><span data-stu-id="50226-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="50226-389">2番目のアクションメソッドは、フォームの送信を処理します。</span><span class="sxs-lookup"><span data-stu-id="50226-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="50226-390">タスク 1-HTTP 取得の削除アクションメソッドを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="50226-391">このタスクでは、Delete アクションメソッドの HTTP GET バージョンを実装して、アルバムの情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="50226-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="50226-392">**Source/Ex5-HandlingDeletion/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="50226-393">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-394">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-395">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-396">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-397">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-398">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-399">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-400">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-401">**StoreManagerController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="50226-402">これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="50226-403">[コントローラーの削除] アクションは、以前の [ストアの詳細] コントローラーアクションとまったく同じです。 URL で指定された**id**を使用してデータベースから**アルバム**オブジェクトに対してクエリを実行し、適切な**ビュー**を返します。</span><span class="sxs-lookup"><span data-stu-id="50226-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="50226-404">これを行うには、HTTP-GET **Delete**アクションメソッドのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="50226-405">(コードスニペット- *ASP.NET MVC 4 ヘルパー And Forms And Validation-Ex5 処理削除 HTTP-Delete Delete アクション*)</span><span class="sxs-lookup"><span data-stu-id="50226-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="50226-406">**Delete**アクションメソッド内で右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="50226-407">[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="50226-408">ビューの追加 ダイアログで、ビュー名が **削除** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="50226-409">**[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="50226-410">**[スキャフォールディング template]** ドロップダウンから **[削除]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="50226-411">他のフィールドは既定値のままにして、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="50226-412">![削除ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "削除ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="50226-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="50226-413">*削除ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="50226-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="50226-414">削除テンプレートには、モデルのすべてのフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="50226-415">アルバムのタイトルのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-415">You will show only the album's title.</span></span> <span data-ttu-id="50226-416">これを行うには、ビューの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="50226-417">タスク 2-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="50226-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="50226-418">このタスクでは、 **Storemanager**の [ビューの**削除**] ページに確認の削除フォームが表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="50226-419">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-420">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-420">The project starts in the Home page.</span></span> <span data-ttu-id="50226-421">URL を「 **/storemanager**」に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="50226-422">削除するアルバムを1つ選択し、 **[削除]** をクリックして、新しいビューがアップロードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="50226-423">![アルバムの削除](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "アルバムの削除")</span><span class="sxs-lookup"><span data-stu-id="50226-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="50226-424">*アルバムの削除*</span><span class="sxs-lookup"><span data-stu-id="50226-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="50226-425">タスク 3-HTTP ポスト削除アクションメソッドを実装する</span><span class="sxs-lookup"><span data-stu-id="50226-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="50226-426">このタスクでは、ユーザーが **[削除]** ボタンをクリックしたときに呼び出される、delete アクションメソッドの HTTP ポストバージョンを実装します。</span><span class="sxs-lookup"><span data-stu-id="50226-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="50226-427">メソッドは、データベース内のアルバムを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="50226-428">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="50226-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="50226-429">**StoreManagerController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="50226-430">これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="50226-431">**HTTP ポスト削除**アクションメソッドのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="50226-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="50226-432">(コードスニペット- *ASP.NET MVC 4 ヘルパー And Forms And Validation-Ex5 処理削除 HTTP-Delete Delete アクション*)</span><span class="sxs-lookup"><span data-stu-id="50226-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="50226-433">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="50226-434">このタスクでは、 **Storemanager**の [ビューの削除] ページでアルバムを削除し、Storemanager インデックスビューにリダイレクトできることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="50226-435">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-436">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-436">The project starts in the Home page.</span></span> <span data-ttu-id="50226-437">URL を「 **/storemanager**」に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="50226-438">[削除] をクリックして、削除するアルバムを1つ選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="50226-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="50226-439">削除を確認するには、 **[削除]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="50226-440">![アルバムの削除](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "アルバムの削除")</span><span class="sxs-lookup"><span data-stu-id="50226-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="50226-441">*アルバムの削除*</span><span class="sxs-lookup"><span data-stu-id="50226-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="50226-442">アルバムが削除されたことを確認します。これは、 **[インデックス]** ページに表示されません。</span><span class="sxs-lookup"><span data-stu-id="50226-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="50226-443">演習 6: 検証の追加</span><span class="sxs-lookup"><span data-stu-id="50226-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="50226-444">現時点では、作成および編集フォームでは、どのような種類の検証も実行されません。</span><span class="sxs-lookup"><span data-stu-id="50226-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="50226-445">ユーザーが必要なフィールドを空白のままにするか、price フィールドに文字を入力すると、最初に発生するエラーはデータベースから取得されます。</span><span class="sxs-lookup"><span data-stu-id="50226-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="50226-446">モデルクラスにデータ注釈を追加することで、アプリケーションに検証を追加できます。</span><span class="sxs-lookup"><span data-stu-id="50226-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="50226-447">データ注釈を使用すると、モデルのプロパティに適用するルールを記述できます。また、ASP.NET MVC は、適切なメッセージをユーザーに適用し、表示する処理を行います。</span><span class="sxs-lookup"><span data-stu-id="50226-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="50226-448">タスク 1-データ注釈を追加する</span><span class="sxs-lookup"><span data-stu-id="50226-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="50226-449">このタスクでは、必要に応じて、Create ページと Edit ページに検証メッセージを表示するデータ注釈をアルバムモデルに追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="50226-450">単純なモデルクラスの場合、データ注釈を追加するには、 **system.componentmodel**の**using**ステートメントを追加してから、適切なプロパティに **[Required]** 属性を配置します。</span><span class="sxs-lookup"><span data-stu-id="50226-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="50226-451">次の例では、 **Name**プロパティをビューの必須フィールドにします。</span><span class="sxs-lookup"><span data-stu-id="50226-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="50226-452">これは、Entity Data Model が生成されるこのアプリケーションのような場合には少し複雑です。</span><span class="sxs-lookup"><span data-stu-id="50226-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="50226-453">モデルクラスにデータ注釈を直接追加した場合は、データベースからモデルを更新すると上書きされます。</span><span class="sxs-lookup"><span data-stu-id="50226-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="50226-454">代わりに、注釈を保持するために存在し、 **[Metadatatype]** 属性を使用してモデルクラスに関連付けられているメタデータ部分クラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="50226-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="50226-455">**Source/Ex6-の検証/開始/** フォルダーにある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="50226-456">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-457">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-458">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-459">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-460">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-461">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-462">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-463">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-464">**[モデル]** フォルダーから**Album.cs**を開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="50226-465">**Album.cs**の内容を強調表示されたコードに置き換えて、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="50226-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="50226-466">**[Displayformat (ConvertEmptyStringToNull = false)]** という行は、データソースのデータフィールドが更新されたときに、モデルの空の文字列が null に変換されないことを示します。</span><span class="sxs-lookup"><span data-stu-id="50226-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="50226-467">データ注釈によってフィールドが検証される前に、Entity Framework によってモデルに null 値が割り当てられる場合、この設定は例外を回避します。</span><span class="sxs-lookup"><span data-stu-id="50226-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="50226-468">(コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex6 アルバムメタデータ部分クラス*)</span><span class="sxs-lookup"><span data-stu-id="50226-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="50226-469">この**アルバム**部分クラスには、データ注釈の**AlbumMetaData**クラスを指す**metadatatype**属性があります。</span><span class="sxs-lookup"><span data-stu-id="50226-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="50226-470">アルバムモデルに注釈を付けるために使用しているデータ注釈属性の一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="50226-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="50226-471">必須-プロパティが必須フィールドであることを示します。</span><span class="sxs-lookup"><span data-stu-id="50226-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="50226-472">DisplayName-フォームフィールドと検証メッセージに使用するテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="50226-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="50226-473">DisplayFormat-データフィールドを表示および書式設定する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="50226-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="50226-474">StringLength-文字列フィールドの最大長を定義します。</span><span class="sxs-lookup"><span data-stu-id="50226-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="50226-475">範囲-数値フィールドの最大値と最小値を指定します。</span><span class="sxs-lookup"><span data-stu-id="50226-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="50226-476">ScaffoldColumn-エディターフォームからのフィールドの非表示を許可します</span><span class="sxs-lookup"><span data-stu-id="50226-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="50226-477">タスク 2-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="50226-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="50226-478">このタスクでは、最後のタスクで選択した表示名を使用して、Create ページと Edit ページがフィールドを検証するかどうかをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="50226-479">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="50226-480">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-480">The project starts in the Home page.</span></span> <span data-ttu-id="50226-481">URL を **/StoreManager/Create**に変更します。</span><span class="sxs-lookup"><span data-stu-id="50226-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="50226-482">表示名が部分クラスの名前と一致していることを確認します ( **AlbumArtUrl**の代わりに**アルバムアートの URL**など)。</span><span class="sxs-lookup"><span data-stu-id="50226-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="50226-483">フォームに入力せずに **[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="50226-484">対応する検証メッセージが取得されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="50226-485">![[作成] ページで検証されたフィールド](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "[作成] ページで検証されたフィールド")</span><span class="sxs-lookup"><span data-stu-id="50226-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="50226-486">*[作成] ページで検証されたフィールド*</span><span class="sxs-lookup"><span data-stu-id="50226-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="50226-487">**[編集]** ページでも同じことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="50226-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="50226-488">URL を **/StoreManager/Edit/1**に変更し、表示名が部分クラスの名前と一致していることを確認します ( **AlbumArtUrl**の代わりに**アルバムアートの URL**など)。</span><span class="sxs-lookup"><span data-stu-id="50226-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="50226-489">**タイトル**と**価格**フィールドを空にして、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="50226-490">対応する検証メッセージが取得されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-490">Verify that you get the corresponding validation messages.</span></span>

    ![[編集] ページの検証済みフィールド](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="50226-492">*[編集] ページの検証済みフィールド*</span><span class="sxs-lookup"><span data-stu-id="50226-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="50226-493">演習 7: クライアント側で控えめな jQuery を使用する</span><span class="sxs-lookup"><span data-stu-id="50226-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="50226-494">この演習では、クライアント側で MVC 4 の控えめな jQuery 検証を有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="50226-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="50226-495">控えめな jQuery は、データ ajax プレフィックス JavaScript を使用して、インラインクライアントスクリプトを出力するのではなく、サーバー上のアクションメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="50226-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="50226-496">タスク 1-控えめな jQuery を有効にする前にアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="50226-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="50226-497">このタスクでは、両方の検証モデルを比較するために、jQuery をインクルードする前にアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="50226-498">**Source/Ex7-UnobtrusivejQueryValidation/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="50226-499">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="50226-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="50226-500">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="50226-501">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="50226-502">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50226-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="50226-503">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="50226-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50226-504">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="50226-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="50226-505">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="50226-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="50226-506">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="50226-507">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="50226-508">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-508">The project starts in the Home page.</span></span> <span data-ttu-id="50226-509">**/StoreManager/Create**を参照し、フォームに入力せずに **[作成]** をクリックして、検証メッセージが表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="50226-510">![クライアント検証が無効](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "クライアント検証が無効")</span><span class="sxs-lookup"><span data-stu-id="50226-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="50226-511">*クライアント検証が無効*</span><span class="sxs-lookup"><span data-stu-id="50226-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="50226-512">ブラウザーで、HTML ソースコードを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="50226-513">タスク 2-控えめなクライアント検証の有効化</span><span class="sxs-lookup"><span data-stu-id="50226-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="50226-514">このタスクでは、 **web.config ファイルから**jQuery の控えめな**クライアント検証**を有効にします。これは、すべての新しい ASP.NET MVC 4 プロジェクトで既定で false に設定されています。</span><span class="sxs-lookup"><span data-stu-id="50226-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="50226-515">また、jQuery の控えめなクライアント検証を行うために必要なスクリプト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="50226-516">プロジェクトルートで**web.config**ファイルを開き、 **Clientvalidationenabled**と**UnobtrusiveJavaScriptEnabled** keys の値が**true**に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="50226-517">Global.asax.cs のコードでクライアント検証を有効にすることで、同じ結果を得ることもできます。</span><span class="sxs-lookup"><span data-stu-id="50226-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="50226-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="50226-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="50226-519">また、ClientValidationEnabled 属性を任意のコントローラーに割り当てて、カスタム動作を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="50226-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="50226-520">**Views\StoreManager**で、 **Create. cshtml**を開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="50226-521">&quot; **~/bundles/jqueryval**&quot; バンドルを通じて、次のスクリプトファイル ( **jquery. validate**および**jquery**) がビューで参照されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="50226-522">これらの jQuery ライブラリはすべて、MVC 4 の新しいプロジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="50226-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="50226-523">その他のライブラリは、プロジェクトの **[スクリプト]** フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="50226-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="50226-524">この検証ライブラリを機能させるには、jQuery framework ライブラリへの参照を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50226-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="50226-525">この参照は既に **\_Layout. cshtml**ファイルに追加されているため、この特定のビューに追加する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="50226-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="50226-526">タスク 3-控えめな jQuery 検証を使用したアプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="50226-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="50226-527">このタスクでは、ユーザーが新しいアルバムを作成するときに、 **Storemanager** create view テンプレートによって jQuery ライブラリを使用したクライアント側の検証が実行されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="50226-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="50226-528">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="50226-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="50226-529">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-529">The project starts in the Home page.</span></span> <span data-ttu-id="50226-530">**/StoreManager/Create**を参照し、フォームに入力せずに **[作成]** をクリックして、検証メッセージが表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="50226-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="50226-531">![JQuery が有効になっているクライアント検証](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery が有効になっているクライアント検証")</span><span class="sxs-lookup"><span data-stu-id="50226-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="50226-532">*JQuery が有効になっているクライアント検証*</span><span class="sxs-lookup"><span data-stu-id="50226-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="50226-533">ブラウザーで、Create view のソースコードを開きます。</span><span class="sxs-lookup"><span data-stu-id="50226-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="50226-534">各クライアント検証規則について、控えめな jQuery は*rulename*=&quot;*message*&quot;を持つ属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="50226-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="50226-535">次に、クライアント検証を実行するために、控えめな jQuery が html 入力フィールドに挿入するタグの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="50226-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="50226-536">データ-val</span><span class="sxs-lookup"><span data-stu-id="50226-536">Data-val</span></span>
   > - <span data-ttu-id="50226-537">データ-val</span><span class="sxs-lookup"><span data-stu-id="50226-537">Data-val-number</span></span>
   > - <span data-ttu-id="50226-538">データ値-範囲</span><span class="sxs-lookup"><span data-stu-id="50226-538">Data-val-range</span></span>
   > - <span data-ttu-id="50226-539">データ範囲-最小値/データ範囲-最大値</span><span class="sxs-lookup"><span data-stu-id="50226-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="50226-540">データ val-必須</span><span class="sxs-lookup"><span data-stu-id="50226-540">Data-val-required</span></span>
   > - <span data-ttu-id="50226-541">データ val-長さ</span><span class="sxs-lookup"><span data-stu-id="50226-541">Data-val-length</span></span>
   > - <span data-ttu-id="50226-542">データ-長さ-最大/データ-長さ-最小</span><span class="sxs-lookup"><span data-stu-id="50226-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="50226-543">すべてのデータ値は、モデル**データ注釈**で塗りつぶされます。</span><span class="sxs-lookup"><span data-stu-id="50226-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="50226-544">次に、サーバー側で動作するすべてのロジックをクライアント側で実行できます。</span><span class="sxs-lookup"><span data-stu-id="50226-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="50226-545">たとえば、Price 属性には、モデルに次のデータ注釈があります。</span><span class="sxs-lookup"><span data-stu-id="50226-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="50226-546">控えめな jQuery を使用すると、生成されるコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="50226-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="50226-547">まとめ</span><span class="sxs-lookup"><span data-stu-id="50226-547">Summary</span></span>

<span data-ttu-id="50226-548">このハンズオンラボを完了することで、ユーザーがデータベースに格納されているデータを次のように変更できるようにする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="50226-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="50226-549">インデックス、作成、編集、削除などのコントローラーアクション</span><span class="sxs-lookup"><span data-stu-id="50226-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="50226-550">HTML テーブルにプロパティを表示するための ASP.NET MVC のスキャフォールディング機能</span><span class="sxs-lookup"><span data-stu-id="50226-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="50226-551">ユーザーエクスペリエンスを向上させるためのカスタム HTML ヘルパー</span><span class="sxs-lookup"><span data-stu-id="50226-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="50226-552">HTTP GET または HTTP POST 呼び出しのいずれかに対応するアクションメソッド</span><span class="sxs-lookup"><span data-stu-id="50226-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="50226-553">作成や編集などの類似ビューテンプレート用の共有エディターテンプレート</span><span class="sxs-lookup"><span data-stu-id="50226-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="50226-554">ドロップダウンなどのフォーム要素</span><span class="sxs-lookup"><span data-stu-id="50226-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="50226-555">モデル検証のデータ注釈</span><span class="sxs-lookup"><span data-stu-id="50226-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="50226-556">JQuery の控えめのライブラリを使用したクライアント側の検証</span><span class="sxs-lookup"><span data-stu-id="50226-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="50226-557">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="50226-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="50226-558">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="50226-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="50226-559">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="50226-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="50226-560">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="50226-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="50226-561">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="50226-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="50226-562">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-562">Click on **Install Now**.</span></span> <span data-ttu-id="50226-563">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="50226-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="50226-564">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="50226-565">![Visual Studio Express のインストール](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="50226-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="50226-566">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="50226-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="50226-567">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="50226-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="50226-569">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="50226-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="50226-570">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="50226-570">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="50226-572">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="50226-572">*Installation progress*</span></span>
6. <span data-ttu-id="50226-573">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-573">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="50226-575">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="50226-575">*Installation completed*</span></span>
7. <span data-ttu-id="50226-576">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="50226-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="50226-577">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="50226-579">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="50226-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="50226-580">付録 B: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="50226-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="50226-581">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="50226-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="50226-582">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="50226-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="50226-583">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="50226-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="50226-584">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="50226-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="50226-585">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="50226-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="50226-586">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="50226-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="50226-587">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="50226-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="50226-588">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="50226-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="50226-589">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="50226-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="50226-590">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="50226-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="50226-591">![スニペット名の入力を開始します](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="50226-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="50226-592">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="50226-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="50226-593">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="50226-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="50226-594">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="50226-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="50226-595">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="50226-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="50226-596">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="50226-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="50226-597">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="50226-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="50226-598">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="50226-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="50226-599">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="50226-600">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="50226-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="50226-601">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="50226-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="50226-602">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="50226-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="50226-603">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="50226-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="50226-604">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="50226-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
