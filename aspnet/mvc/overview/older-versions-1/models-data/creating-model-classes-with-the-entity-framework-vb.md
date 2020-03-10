---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Entity Framework を使用したモデルクラスの作成 (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、Microsoft Entity Framework で ASP.NET MVC を使用する方法について説明します。 Entity Wizard を使用して ADO.NET エンティティを作成する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: f6c896c6f5f6d898ac6f99d5998fb29cb73bcb10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437008"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="40025-104">Entity Framework でモデル クラスを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="40025-104">Creating Model Classes with the Entity Framework (VB)</span></span>

<span data-ttu-id="40025-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="40025-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="40025-106">このチュートリアルでは、Microsoft Entity Framework で ASP.NET MVC を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40025-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="40025-107">Entity Wizard を使用して、ADO.NET Entity Data Model を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40025-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="40025-108">このチュートリアルでは、Entity Framework を使用してデータベースデータを選択、挿入、更新、および削除する方法を示す web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="40025-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="40025-109">このチュートリアルの目的は、ASP.NET MVC アプリケーションを構築するときに、Microsoft Entity Framework を使用してデータアクセスクラスを作成する方法について説明することです。</span><span class="sxs-lookup"><span data-stu-id="40025-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="40025-110">このチュートリアルでは、Microsoft Entity Framework に関する以前の知識がないことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="40025-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="40025-111">このチュートリアルの最後に、Entity Framework を使用してデータベースレコードを選択、挿入、更新、および削除する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40025-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="40025-112">Microsoft Entity Framework は、オブジェクトリレーショナルマッピング (O/RM) ツールです。このツールを使用すると、データベースからデータアクセス層を自動的に生成できます。</span><span class="sxs-lookup"><span data-stu-id="40025-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="40025-113">Entity Framework を使用すると、手動でデータアクセスクラスを構築する面倒な作業を回避できます。</span><span class="sxs-lookup"><span data-stu-id="40025-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="40025-114">ASP.NET MVC と Microsoft Entity Framework の間には、重要な接続はありません。</span><span class="sxs-lookup"><span data-stu-id="40025-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="40025-115">ASP.NET MVC で使用できる Entity Framework には、いくつかの選択肢があります。</span><span class="sxs-lookup"><span data-stu-id="40025-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="40025-116">たとえば、Microsoft LINQ to SQL、NHibernate、SubSonic などの他の O/RM ツールを使用して、MVC モデルクラスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="40025-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

<span data-ttu-id="40025-117">ASP.NET MVC で Microsoft Entity Framework を使用する方法を説明するために、簡単なサンプルアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="40025-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="40025-118">ムービーデータベースアプリケーションを作成し、ムービーデータベースレコードを表示および編集できるようにします。</span><span class="sxs-lookup"><span data-stu-id="40025-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="40025-119">このチュートリアルでは、Visual Studio 2008 または Visual Web Developer 2008 (Service Pack 1) を使用していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="40025-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="40025-120">Entity Framework を使用するには、Service Pack 1 が必要です。</span><span class="sxs-lookup"><span data-stu-id="40025-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="40025-121">次のアドレスから、Visual Studio 2008 Service Pack 1 または Visual Web Developer with Service Pack 1 をダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="40025-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="40025-122">ムービーサンプルデータベースの作成</span><span class="sxs-lookup"><span data-stu-id="40025-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="40025-123">ムービーデータベースアプリケーションでは、次の列を含む、ムービーという名前のデータベーステーブルを使用します。</span><span class="sxs-lookup"><span data-stu-id="40025-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="40025-124">列名</span><span class="sxs-lookup"><span data-stu-id="40025-124">Column Name</span></span> | <span data-ttu-id="40025-125">データ型</span><span class="sxs-lookup"><span data-stu-id="40025-125">Data Type</span></span> | <span data-ttu-id="40025-126">Null を許容しますか?</span><span class="sxs-lookup"><span data-stu-id="40025-126">Allow Nulls?</span></span> | <span data-ttu-id="40025-127">主キーか?</span><span class="sxs-lookup"><span data-stu-id="40025-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40025-128">Id</span><span class="sxs-lookup"><span data-stu-id="40025-128">Id</span></span> | <span data-ttu-id="40025-129">INT</span><span class="sxs-lookup"><span data-stu-id="40025-129">int</span></span> | <span data-ttu-id="40025-130">False</span><span class="sxs-lookup"><span data-stu-id="40025-130">False</span></span> | <span data-ttu-id="40025-131">True</span><span class="sxs-lookup"><span data-stu-id="40025-131">True</span></span> |
| <span data-ttu-id="40025-132">タイトル</span><span class="sxs-lookup"><span data-stu-id="40025-132">Title</span></span> | <span data-ttu-id="40025-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="40025-133">nvarchar(100)</span></span> | <span data-ttu-id="40025-134">False</span><span class="sxs-lookup"><span data-stu-id="40025-134">False</span></span> | <span data-ttu-id="40025-135">False</span><span class="sxs-lookup"><span data-stu-id="40025-135">False</span></span> |
| <span data-ttu-id="40025-136">ディレクター</span><span class="sxs-lookup"><span data-stu-id="40025-136">Director</span></span> | <span data-ttu-id="40025-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="40025-137">nvarchar(100)</span></span> | <span data-ttu-id="40025-138">False</span><span class="sxs-lookup"><span data-stu-id="40025-138">False</span></span> | <span data-ttu-id="40025-139">False</span><span class="sxs-lookup"><span data-stu-id="40025-139">False</span></span> |

<span data-ttu-id="40025-140">このテーブルを ASP.NET MVC プロジェクトに追加するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="40025-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="40025-141">ソリューションエクスプローラーウィンドウで [App\_Data] フォルダーを右クリックし、メニューオプション [追加]、[新しい項目] の順に選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="40025-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="40025-142">**[新しい項目の追加]** ダイアログボックスで、 **[SQL Server データベース]** を選択し、データベースに MoviesDB という名前を付けて、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="40025-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="40025-143">MoviesDB ファイルをダブルクリックして、[サーバーエクスプローラー/データベースエクスプローラー] ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="40025-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="40025-144">MoviesDB データベース接続を展開し、テーブル フォルダーを右クリックして、**新しいテーブルの追加** メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="40025-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="40025-145">テーブルデザイナーで、Id、タイトル、ディレクター の各列を追加します。</span><span class="sxs-lookup"><span data-stu-id="40025-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="40025-146">**[保存]** ボタン (フロッピーのアイコン) をクリックして、ムービーという名前の新しいテーブルを保存します。</span><span class="sxs-lookup"><span data-stu-id="40025-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="40025-147">ムービーデータベーステーブルを作成したら、いくつかのサンプルデータをテーブルに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40025-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="40025-148">映画 テーブルを右クリックし、**テーブルデータの表示** メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="40025-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="40025-149">表示されるグリッドにフェイクムービーデータを入力できます。</span><span class="sxs-lookup"><span data-stu-id="40025-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="40025-150">ADO.NET Entity Data Model の作成</span><span class="sxs-lookup"><span data-stu-id="40025-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="40025-151">Entity Framework を使用するには、Entity Data Model を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40025-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="40025-152">Visual Studio の*Entity Data Model ウィザード*を利用すると、データベースから Entity Data Model を自動的に生成できます。</span><span class="sxs-lookup"><span data-stu-id="40025-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="40025-153">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="40025-153">Follow these steps:</span></span>

1. <span data-ttu-id="40025-154">ソリューションエクスプローラーウィンドウで [モデル] フォルダーを右クリックし、メニューオプション [**追加]、[新しい項目**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="40025-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="40025-155">**新しい項目の追加** ダイアログで、データ カテゴリを選択します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="40025-156">**ADO.NET Entity Data Model**テンプレートを選択し、Entity Data Model の名前を MoviesDBModel に指定して、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="40025-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="40025-157">**[追加]** ボタンをクリックすると、データモデルウィザードが起動します。</span><span class="sxs-lookup"><span data-stu-id="40025-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="40025-158">**[モデルの内容の選択]** ステップで、 **[データベースから生成]** オプションを選択し、 **[次へ]** ボタンをクリックします (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="40025-159">**[データ接続の選択]** 手順で、MoviesDB データベース接続を選択し、エンティティ接続設定の名前 MoviesDBEntities を入力して、 **[次へ]** ボタンをクリックします (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="40025-160">**[データベースオブジェクトの選択]** ステップで、ムービーデータベース テーブルを選択し、 **[完了]** ボタンをクリックします (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="40025-161">これらの手順を完了すると、ADO.NET Entity Data Model Designer (Entity Designer) が開きます。</span><span class="sxs-lookup"><span data-stu-id="40025-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="40025-162">**図1–新しい Entity Data Model の作成**</span><span class="sxs-lookup"><span data-stu-id="40025-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="40025-164">**図2–モデルの内容を選択する手順**</span><span class="sxs-lookup"><span data-stu-id="40025-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="40025-166">**図 3-データ接続を選択する**</span><span class="sxs-lookup"><span data-stu-id="40025-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="40025-168">**図4–データベースオブジェクトを選択する**</span><span class="sxs-lookup"><span data-stu-id="40025-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="40025-170">ADO.NET Entity Data Model の変更</span><span class="sxs-lookup"><span data-stu-id="40025-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="40025-171">Entity Data Model を作成したら、Entity Designer を利用してモデルを変更できます (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="40025-172">[ソリューションエクスプローラー] ウィンドウ内の [モデル] フォルダーに格納されている MoviesDBModel ファイルをダブルクリックすると、いつでも Entity Designer を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="40025-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="40025-173">**図 5: ADO.NET Entity Data Model デザイナー**</span><span class="sxs-lookup"><span data-stu-id="40025-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="40025-175">たとえば、エンティティモデルデータウィザードによって生成されるクラスの名前を変更するには、Entity Designer を使用します。</span><span class="sxs-lookup"><span data-stu-id="40025-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="40025-176">このウィザードでは、ムービーという名前の新しいデータアクセスクラスが作成されました。</span><span class="sxs-lookup"><span data-stu-id="40025-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="40025-177">つまり、ウィザードでは、データベーステーブルとまったく同じ名前が付けられています。</span><span class="sxs-lookup"><span data-stu-id="40025-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="40025-178">このクラスを使用して特定のムービーインスタンスを表すため、ムービーからムービーにクラスの名前を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40025-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="40025-179">エンティティクラスの名前を変更する場合は、Entity Designer でクラス名をダブルクリックし、新しい名前を入力します (図6を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="40025-180">また、Entity Designer でエンティティを選択した後で、プロパティウィンドウ内のエンティティの名前を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="40025-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="40025-181">**図6–エンティティ名の変更**</span><span class="sxs-lookup"><span data-stu-id="40025-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="40025-183">変更を行った後は、[保存] ボタン (フロッピーディスクのアイコン) をクリックして Entity Data Model を保存してください。</span><span class="sxs-lookup"><span data-stu-id="40025-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="40025-184">バックグラウンドでは、Entity Designer によって、一連の Visual Basic .NET クラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="40025-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="40025-185">これらのクラスを表示するには、[ソリューションエクスプローラー] ウィンドウで MoviesDBModel ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="40025-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>

<span data-ttu-id="40025-186">次に Entity Designer を使用するときに変更が上書きされるため、デザイナーの .vb ファイルのコードは変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="40025-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="40025-187">デザイナー .vb ファイルで定義されているエンティティクラスの機能を拡張する場合は、*部分クラス*を別々のファイルに作成できます。</span><span class="sxs-lookup"><span data-stu-id="40025-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="40025-188">Entity Framework を使用したデータベースレコードの選択</span><span class="sxs-lookup"><span data-stu-id="40025-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="40025-189">ムービーレコードの一覧を表示するページを作成して、ムービーデータベースアプリケーションの作成を開始しましょう。</span><span class="sxs-lookup"><span data-stu-id="40025-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="40025-190">リスト1のホームコントローラーは、Index () という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="40025-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="40025-191">Index () アクションは、Entity Framework を利用して、ムービーデータベーステーブルのすべてのムービーレコードを返します。</span><span class="sxs-lookup"><span data-stu-id="40025-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="40025-192">**リスト1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="40025-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="40025-193">リスト1のコントローラーには、コンストラクターが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40025-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="40025-194">コンストラクターは \_db という名前のクラスレベルのフィールドを初期化します。</span><span class="sxs-lookup"><span data-stu-id="40025-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="40025-195">\_db フィールドは、Microsoft Entity Framework によって生成されるデータベースエンティティを表します。</span><span class="sxs-lookup"><span data-stu-id="40025-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="40025-196">\_db フィールドは、Entity Designer によって生成された MoviesDBEntities クラスのインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="40025-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="40025-197">\_db フィールドは、ムービーデータベーステーブルからレコードを取得するために Index () アクション内で使用されます。</span><span class="sxs-lookup"><span data-stu-id="40025-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="40025-198">式 \_db です。Mo視聴セットは、ムービーデータベーステーブルのすべてのレコードを表します。</span><span class="sxs-lookup"><span data-stu-id="40025-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="40025-199">ToList () メソッドを使用して、映画のセットをムービーオブジェクトのジェネリックコレクション (映画のリスト) に変換します。</span><span class="sxs-lookup"><span data-stu-id="40025-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="40025-200">ムービーレコードは LINQ to Entities のヘルプを使用して取得されます。</span><span class="sxs-lookup"><span data-stu-id="40025-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="40025-201">リスト1の Index () アクションでは、LINQ*メソッド構文*を使用してデータベースレコードのセットを取得します。</span><span class="sxs-lookup"><span data-stu-id="40025-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="40025-202">必要に応じて、代わりに LINQ*クエリ構文*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="40025-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="40025-203">次の2つのステートメントは、まったく同じことを行います。</span><span class="sxs-lookup"><span data-stu-id="40025-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="40025-204">最も直感的にわかるような LINQ 構文 (メソッド構文またはクエリ構文) を使用します。</span><span class="sxs-lookup"><span data-stu-id="40025-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="40025-205">2つの方法の間でパフォーマンスに違いはありません。唯一の違いは style です。</span><span class="sxs-lookup"><span data-stu-id="40025-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="40025-206">リスト2のビューは、ムービーレコードを表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="40025-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="40025-207">**リスト2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="40025-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="40025-208">リスト2のビューには、各ムービーレコードを反復処理し、ムービーレコードのタイトルと監督のプロパティの値を表示する**For each**ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="40025-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="40025-209">各レコードの横に [編集] リンクと [削除] リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="40025-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="40025-210">さらに、[ムービーの追加] リンクがビューの下部に表示されます (図7を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="40025-211">**図 7: インデックスビュー**</span><span class="sxs-lookup"><span data-stu-id="40025-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="40025-213">インデックスビューは、*型指定*されたビューです。</span><span class="sxs-lookup"><span data-stu-id="40025-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="40025-214">インデックスビューには、Inherits 属性を含む &lt;% @ Page%&gt; ディレクティブがあります。</span><span class="sxs-lookup"><span data-stu-id="40025-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="40025-215">Inherits 属性は、ViewData プロパティを、ムービーオブジェクトの厳密に型指定されたジェネリックリストコレクション (映画のリスト) にキャストします。</span><span class="sxs-lookup"><span data-stu-id="40025-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="40025-216">Entity Framework を使用したデータベースレコードの挿入</span><span class="sxs-lookup"><span data-stu-id="40025-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="40025-217">Entity Framework を使用すると、データベーステーブルに新しいレコードを簡単に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="40025-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="40025-218">リスト3には、新しいレコードをムービーデータベーステーブルに挿入するために使用できる Home controller クラスに追加された2つの新しいアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="40025-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="40025-219">**リスト3– Controllers\HomeController.vb (メソッドの追加)**</span><span class="sxs-lookup"><span data-stu-id="40025-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="40025-220">最初の Add () アクションでは、単にビューを返します。</span><span class="sxs-lookup"><span data-stu-id="40025-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="40025-221">このビューには、新しいムービーデータベースレコードを追加するためのフォームが含まれています (図8を参照)。</span><span class="sxs-lookup"><span data-stu-id="40025-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="40025-222">フォームを送信すると、2番目の Add () アクションが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="40025-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="40025-223">2番目の Add () アクションが、AcceptVerbs 属性で修飾されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40025-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="40025-224">このアクションは、HTTP POST 操作を実行する場合にのみ呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="40025-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="40025-225">つまり、このアクションは、HTML フォームを投稿するときにのみ呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="40025-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="40025-226">2番目の Add () アクションは、ASP.NET MVC TryUpdateModel () メソッドを使用して、Entity Framework Movie クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="40025-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="40025-227">TryUpdateModel () メソッドは、Add () メソッドに渡された FormCollection 内のフィールドを受け取り、これらの HTML フォームフィールドの値を Movie クラスに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="40025-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="40025-228">Entity Framework を使用する場合は、TryUpdateModel メソッドまたは UpdateModel メソッドを使用してエンティティクラスのプロパティを更新するときに、プロパティの "ホワイトリスト" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40025-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="40025-229">次に、Add () アクションは、単純なフォーム検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="40025-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="40025-230">アクションは、Title プロパティと Director プロパティの両方に値があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="40025-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="40025-231">検証エラーが発生した場合は、検証エラーメッセージが ModelState に追加されます。</span><span class="sxs-lookup"><span data-stu-id="40025-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="40025-232">検証エラーがない場合は、Entity Framework のヘルプを含む新しいムービーレコードがムービーデータベーステーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="40025-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="40025-233">新しいレコードは、次の2行のコードを使用してデータベースに追加されます。</span><span class="sxs-lookup"><span data-stu-id="40025-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="40025-234">コードの1行目では、Entity Framework によって追跡されている一連のムービーに新しい Movie エンティティを追加します。</span><span class="sxs-lookup"><span data-stu-id="40025-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="40025-235">コードの2行目では、追跡しているムービーに加えられたすべての変更を、基になるデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="40025-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="40025-236">**図 8: [追加] ビュー**</span><span class="sxs-lookup"><span data-stu-id="40025-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="40025-238">Entity Framework を使用したデータベースレコードの更新</span><span class="sxs-lookup"><span data-stu-id="40025-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="40025-239">ほぼ同じアプローチに従って、新しいデータベースレコードを挿入する方法として Entity Framework を使用してデータベースレコードを編集できます。</span><span class="sxs-lookup"><span data-stu-id="40025-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="40025-240">リスト4には、Edit () という名前の新しいコントローラーアクションが2つ含まれています。</span><span class="sxs-lookup"><span data-stu-id="40025-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="40025-241">最初の Edit () アクションでは、ムービーレコードを編集するための HTML フォームが返されます。</span><span class="sxs-lookup"><span data-stu-id="40025-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="40025-242">2番目の Edit () アクションは、データベースを更新しようとします。</span><span class="sxs-lookup"><span data-stu-id="40025-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="40025-243">**リスト4– Controllers\HomeController.vb (メソッドの編集)**</span><span class="sxs-lookup"><span data-stu-id="40025-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="40025-244">2番目の Edit () アクションは、編集中のムービーの Id と一致するムービーレコードをデータベースから取得することによって開始されます。</span><span class="sxs-lookup"><span data-stu-id="40025-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="40025-245">次の LINQ to Entities ステートメントは、特定の Id に一致する最初のデータベースレコードを取得します。</span><span class="sxs-lookup"><span data-stu-id="40025-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="40025-246">次に、TryUpdateModel () メソッドを使用して、HTML フォームフィールドの値を movie エンティティのプロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="40025-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="40025-247">更新するプロパティを正確に指定するためのホワイトリストが提供されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="40025-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="40025-248">次に、ムービータイトルとディレクタープロパティの両方に値が設定されていることを確認するために、いくつかの単純な検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="40025-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="40025-249">いずれかのプロパティに値が指定されていない場合、ModelState と ModelState に検証エラーメッセージが追加されます。 IsValid は値 false を返します。</span><span class="sxs-lookup"><span data-stu-id="40025-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="40025-250">最後に、検証エラーがない場合は、SaveChanges () メソッドを呼び出すことにより、基になるムービーデータベーステーブルが変更されて更新されます。</span><span class="sxs-lookup"><span data-stu-id="40025-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="40025-251">データベースレコードを編集する場合は、編集するレコードの Id を、データベースの更新を実行するコントローラーアクションに渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="40025-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="40025-252">それ以外の場合、コントローラーアクションは、基になるデータベースで更新するレコードを認識しません。</span><span class="sxs-lookup"><span data-stu-id="40025-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="40025-253">リスト5に含まれる編集ビューには、編集中のデータベースレコードの Id を表す非表示のフォームフィールドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="40025-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="40025-254">**リスト5– Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="40025-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="40025-255">Entity Framework を使用したデータベースレコードの削除</span><span class="sxs-lookup"><span data-stu-id="40025-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="40025-256">このチュートリアルで対処する必要がある最後のデータベース操作は、データベースレコードを削除することです。</span><span class="sxs-lookup"><span data-stu-id="40025-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="40025-257">リスト6のコントローラーアクションを使用して、特定のデータベースレコードを削除できます。</span><span class="sxs-lookup"><span data-stu-id="40025-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="40025-258">**リスト 6--\Controllers\HomeController.vb (Delete アクション)**</span><span class="sxs-lookup"><span data-stu-id="40025-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="40025-259">Delete () アクションは、アクションに渡された Id と一致するムービーエンティティを最初に取得します。</span><span class="sxs-lookup"><span data-stu-id="40025-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="40025-260">次に、DeleteObject () メソッドを呼び出し、その後に SaveChanges () メソッドを呼び出して、ムービーをデータベースから削除します。</span><span class="sxs-lookup"><span data-stu-id="40025-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="40025-261">最後に、ユーザーはインデックスビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="40025-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="40025-262">まとめ</span><span class="sxs-lookup"><span data-stu-id="40025-262">Summary</span></span>

<span data-ttu-id="40025-263">このチュートリアルの目的は、ASP.NET MVC と Microsoft Entity Framework を利用して、データベース駆動型 web アプリケーションを構築する方法を示すことでした。</span><span class="sxs-lookup"><span data-stu-id="40025-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="40025-264">データベースレコードの選択、挿入、更新、および削除を可能にするアプリケーションを構築する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="40025-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="40025-265">まず、Entity Data Model ウィザードを使用して、Visual Studio 内から Entity Data Model を生成する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="40025-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="40025-266">次に、LINQ to Entities を使用してデータベーステーブルから一連のデータベースレコードを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40025-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="40025-267">最後に、Entity Framework を使用して、データベースレコードを挿入、更新、および削除しています。</span><span class="sxs-lookup"><span data-stu-id="40025-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="40025-268">[前へ](validation-with-the-data-annotation-validators-cs.md)
> [次へ](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="40025-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
