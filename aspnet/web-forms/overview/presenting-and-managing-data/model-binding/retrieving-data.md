---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: モデルバインドと web フォームを使用したデータの取得と表示 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 81cca22cb4752d071d2a68986ae9ac2bed737594
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520024"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="a5fc1-104">モデルバインドと web フォームを使用したデータの取得と表示</span><span class="sxs-lookup"><span data-stu-id="a5fc1-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="a5fc1-105">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="a5fc1-106">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="a5fc1-107">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="a5fc1-108">モデルバインドパターンは、任意のデータアクセステクノロジと連携します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="a5fc1-109">このチュートリアルでは Entity Framework を使用しますが、最も使い慣れたデータアクセステクノロジを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="a5fc1-110">GridView、ListView、DetailsView、FormView コントロールなどのデータバインドサーバーコントロールから、データの選択、更新、削除、および作成に使用するメソッドの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="a5fc1-111">このチュートリアルでは、SelectMethod の値を指定します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="a5fc1-112">そのメソッド内で、データを取得するためのロジックを提供します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="a5fc1-113">次のチュートリアルでは、UpdateMethod、DeleteMethod、および InsertMethod の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="a5fc1-114">完全なプロジェクトは、またはC# Visual Basic で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="a5fc1-115">ダウンロード可能なコードは、Visual Studio 2012 以降で動作します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="a5fc1-116">Visual Studio 2012 テンプレートが使用されています。このテンプレートは、このチュートリアルで示した Visual Studio 2017 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="a5fc1-117">このチュートリアルでは、Visual Studio でアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="a5fc1-118">また、アプリケーションをホスティングプロバイダーに展開し、インターネット経由で使用できるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="a5fc1-119">Microsoft では、最大10個の web サイトの web ホスティングを無料で提供しています。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="a5fc1-120">[無料の Azure 試用版アカウント](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="a5fc1-121">Visual Studio web プロジェクトを Azure App Service Web Apps にデプロイする方法の詳細については、「 [Visual studio シリーズを使用した ASP.NET Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="a5fc1-122">このチュートリアルでは、Entity Framework Code First Migrations を使用して、SQL Server データベースを Azure SQL Database にデプロイする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a5fc1-123">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="a5fc1-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="a5fc1-124">Microsoft Visual Studio 2017 または Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="a5fc1-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="a5fc1-125">このチュートリアルは、Visual Studio 2012 および Visual Studio 2013 でも動作しますが、ユーザーインターフェイスとプロジェクトテンプレートにはいくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="a5fc1-126">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="a5fc1-126">What you'll build</span></span>

<span data-ttu-id="a5fc1-127">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="a5fc1-128">学生がコースに登録されている大学を反映するデータオブジェクトを構築する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="a5fc1-129">オブジェクトからデータベーステーブルを作成する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-129">Build database tables from the objects</span></span>
* <span data-ttu-id="a5fc1-130">データベースにテストデータを設定する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-130">Populate the database with test data</span></span>
* <span data-ttu-id="a5fc1-131">Web フォームにデータを表示する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="a5fc1-132">プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="a5fc1-132">Create the project</span></span>

1. <span data-ttu-id="a5fc1-133">Visual Studio 2017 で、 **ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成します。このプロジェクトには、"_ **Osouniversitymodelbinding**" という名前を付いています。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![プロジェクトの作成](retrieving-data/_static/image19.png)

2. <span data-ttu-id="a5fc1-135">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-135">Select **OK**.</span></span> <span data-ttu-id="a5fc1-136">テンプレートを選択するためのダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-136">The dialog box to select a template appears.</span></span>

   ![web フォームの選択](retrieving-data/_static/image3.png)

3. <span data-ttu-id="a5fc1-138">**[Web フォーム]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="a5fc1-139">必要に応じて、認証を**個々のユーザーアカウント**に変更します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="a5fc1-140">**[OK]** をクリックして、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="a5fc1-141">サイトの外観を変更する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-141">Modify site appearance</span></span>

   <span data-ttu-id="a5fc1-142">サイトの外観をカスタマイズするには、いくつかの変更を行います。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="a5fc1-143">サイトのマスターファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="a5fc1-144">**ASP.NET アプリケーション**ではなく、 **Contoso 大学**を表示するようにタイトルを変更します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="a5fc1-145">ヘッダーテキストを**アプリケーション名**から**Contoso 大学**に変更します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="a5fc1-146">ナビゲーションヘッダーリンクをサイト適切なサイトに変更します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="a5fc1-147">**About**と**Contact**のリンクを削除し、代わりに **[学生]** ページにリンクします。このページでは、作成します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="a5fc1-148">Site. Master を保存します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="a5fc1-149">学生データを表示するための web フォームを追加する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="a5fc1-150">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="a5fc1-151">**[新しい項目の追加]** ダイアログボックスで、**マスターページ**テンプレートを使用して Web フォームを選択し、「 **student .aspx**」という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![ページの作成](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="a5fc1-153">**[追加]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="a5fc1-154">Web フォームのマスターページの場合は、 **[.master]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="a5fc1-155">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="a5fc1-156">データ モデルを追加する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-156">Add the data model</span></span>

<span data-ttu-id="a5fc1-157">**[モデル]** フォルダーで、 **UniversityModels.cs**という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="a5fc1-158">**[モデル]** を右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="a5fc1-159">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="a5fc1-160">左側のナビゲーションメニューから、 **[Code]** 、 **[Class]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![モデルクラスの作成](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="a5fc1-162">クラスに**UniversityModels.cs**という名前を指定し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="a5fc1-163">このファイルで、`SchoolContext`、`Student`、`Enrollment`、および `Course` クラスを次のように定義します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="a5fc1-164">`SchoolContext` クラスは、データベース接続とデータの変更を管理する `DbContext`から派生します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="a5fc1-165">`Student` クラスで、`FirstName`、`LastName`、および `Year` の各プロパティに適用されている属性を確認します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="a5fc1-166">このチュートリアルでは、これらの属性を使用してデータを検証します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="a5fc1-167">コードを簡略化するために、これらのプロパティのみがデータ検証属性でマークされます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="a5fc1-168">実際のプロジェクトでは、検証が必要なすべてのプロパティに検証属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="a5fc1-169">UniversityModels.cs を保存します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="a5fc1-170">クラスに基づいてデータベースを設定する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-170">Set up the database based on classes</span></span>

<span data-ttu-id="a5fc1-171">このチュートリアルでは、 [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)を使用してオブジェクトとデータベーステーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="a5fc1-172">これらのテーブルには、学生とそのコースに関する情報が格納されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="a5fc1-173">**[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="a5fc1-174">**パッケージマネージャーコンソール**で、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="a5fc1-175">コマンドが正常に完了した場合は、移行が有効になっているというメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![移行を有効にする](retrieving-data/_static/image8.png)

      <span data-ttu-id="a5fc1-177">*Configuration.cs*という名前のファイルが作成されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="a5fc1-178">`Configuration` クラスには、データベーステーブルにテストデータを事前に設定できる `Seed` メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="a5fc1-179">データベースを事前設定する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="a5fc1-180">Configuration.cs を開きます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="a5fc1-181">`Seed` メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="a5fc1-182">また、`ContosoUniversityModelBinding. Models` 名前空間の `using` ステートメントも追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="a5fc1-183">Configuration.cs を保存します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="a5fc1-184">パッケージマネージャーコンソールで、 **[追加-移行の初期]** コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="a5fc1-185">コマンド**update-database**を実行します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="a5fc1-186">このコマンドの実行時に例外が発生した場合は、`StudentID` と `CourseID` の値が `Seed` メソッドの値と異なる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="a5fc1-187">これらのデータベーステーブルを開き、`StudentID` と `CourseID`の既存の値を検索します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="a5fc1-188">これらの値をコードに追加して、`Enrollments` テーブルをシード処理します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="a5fc1-189">GridView コントロールの追加</span><span class="sxs-lookup"><span data-stu-id="a5fc1-189">Add a GridView control</span></span>

<span data-ttu-id="a5fc1-190">データベースデータが入力されたので、そのデータを取得して表示する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="a5fc1-191">Student を開きます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="a5fc1-192">`MainContent` プレースホルダーを見つけます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="a5fc1-193">このプレースホルダー内に、このコードを含む**GridView**コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="a5fc1-194">注意する点:</span><span class="sxs-lookup"><span data-stu-id="a5fc1-194">Things to note:</span></span>
   * <span data-ttu-id="a5fc1-195">GridView 要素の `SelectMethod` プロパティに設定されている値に注目してください。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="a5fc1-196">この値は、次の手順で作成する GridView データを取得するために使用するメソッドを指定します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="a5fc1-197">`ItemType` プロパティは、前に作成した `Student` クラスに設定されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="a5fc1-198">この設定により、マークアップでクラスのプロパティを参照できます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="a5fc1-199">たとえば、`Student` クラスには、`Enrollments`という名前のコレクションがあります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="a5fc1-200">`Item.Enrollments` を使用してそのコレクションを取得し、 [LINQ 構文](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)を使用して各学生の登録済みクレジットの合計を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="a5fc1-201">Student を保存します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="a5fc1-202">データを取得するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-202">Add code to retrieve data</span></span>

   <span data-ttu-id="a5fc1-203">Student 分離コードファイルで、`SelectMethod` 値に指定されたメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="a5fc1-204">Students.aspx.cs を開きます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="a5fc1-205">`ContosoUniversityModelBinding. Models` と `System.Data.Entity` 名前空間に `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="a5fc1-206">`SelectMethod`に指定したメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="a5fc1-207">`Include` 句を指定すると、クエリのパフォーマンスが向上しますが、必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="a5fc1-208">`Include` 句を指定しない場合は、[*遅延読み込み*](https://en.wikipedia.org/wiki/Lazy_loading)を使用してデータが取得されます。これには、関連するデータが取得されるたびに、データベースに個別のクエリを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="a5fc1-209">`Include` 句を使用すると、*一括読み込み*を使用してデータが取得されます。これは、1つのデータベースクエリですべての関連データを取得することを意味します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="a5fc1-210">関連するデータが使用されていない場合は、より多くのデータが取得されるため、一括読み込みの方が効率が悪くなります。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="a5fc1-211">ただし、この場合、一括読み込みでは、各レコードの関連データが表示されるため、最適なパフォーマンスが得られます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="a5fc1-212">関連データを読み込むときのパフォーマンスに関する考慮事項の詳細については、「 [ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」の記事の「関連データ**の遅延、一括読み込み、明示的な読み込み**」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="a5fc1-213">既定では、データは、キーとしてマークされているプロパティの値によって並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="a5fc1-214">`OrderBy` 句を追加して、別の並べ替え値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="a5fc1-215">この例では、並べ替えに既定の `StudentID` プロパティが使用されています。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="a5fc1-216">データの[並べ替え、ページング、およびフィルター処理](sorting-paging-and-filtering-data.md)の記事では、ユーザーは並べ替えの対象となる列を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="a5fc1-217">Students.aspx.cs を保存します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="a5fc1-218">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="a5fc1-218">Run your application</span></span> 

<span data-ttu-id="a5fc1-219">Web アプリケーション (**F5**) を実行し、 **[Students]** ページに移動します。次の内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![データの表示](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="a5fc1-221">モデルバインドメソッドの自動生成</span><span class="sxs-lookup"><span data-stu-id="a5fc1-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="a5fc1-222">このチュートリアルシリーズを通じて作業する場合は、チュートリアルのコードをプロジェクトにコピーするだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="a5fc1-223">ただし、この方法の欠点の1つは、モデルバインドメソッドのコードを自動的に生成するために Visual Studio によって提供される機能を認識できないことです。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="a5fc1-224">独自のプロジェクトで作業する場合、自動コード生成によって時間を節約し、操作を実装する方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="a5fc1-225">このセクションでは、自動コード生成機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="a5fc1-226">このセクションは情報提供のみを目的としており、プロジェクトに実装する必要があるコードは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="a5fc1-227">マークアップコードで `SelectMethod`、`UpdateMethod`、`InsertMethod`、または `DeleteMethod` プロパティの値を設定する場合は、[**新しいメソッドを作成**する] オプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![メソッドを作成する](retrieving-data/_static/image18.png)

<span data-ttu-id="a5fc1-229">Visual Studio では、適切なシグネチャを持つ分離コードでメソッドが作成されるだけでなく、操作を実行する実装コードも生成されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="a5fc1-230">自動コード生成機能を使用する前に最初に `ItemType` プロパティを設定した場合、生成されたコードはその型を操作に使用します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="a5fc1-231">たとえば、`UpdateMethod` プロパティを設定すると、次のコードが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="a5fc1-232">ここでも、このコードをプロジェクトに追加する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="a5fc1-233">次のチュートリアルでは、新しいデータを更新、削除、および追加するためのメソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="a5fc1-234">まとめ</span><span class="sxs-lookup"><span data-stu-id="a5fc1-234">Summary</span></span>

<span data-ttu-id="a5fc1-235">このチュートリアルでは、データモデルクラスを作成し、それらのクラスからデータベースを生成しました。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="a5fc1-236">データベーステーブルにテストデータが格納されています。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-236">You filled the database tables with test data.</span></span> <span data-ttu-id="a5fc1-237">モデルバインドを使用してデータベースからデータを取得し、GridView でデータを表示しています。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="a5fc1-238">このシリーズの次の[チュートリアル](updating-deleting-and-creating-data.md)では、データの更新、削除、および作成を有効にします。</span><span class="sxs-lookup"><span data-stu-id="a5fc1-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a5fc1-239">Next</span><span class="sxs-lookup"><span data-stu-id="a5fc1-239">Next</span></span>](updating-deleting-and-creating-data.md)
