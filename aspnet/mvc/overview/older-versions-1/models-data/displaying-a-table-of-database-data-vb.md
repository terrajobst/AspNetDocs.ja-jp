---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: データベースデータのテーブルを表示する (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、一連のデータベースレコードを表示する2つの方法について説明します。 HTML ta でデータベースレコードのセットを書式設定する2つの方法を示しています...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590913"
---
# <a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="7e837-104">データベース データの表を表示する (VB)</span><span class="sxs-lookup"><span data-stu-id="7e837-104">Displaying a Table of Database Data (VB)</span></span>

<span data-ttu-id="7e837-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7e837-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7e837-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="7e837-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="7e837-107">このチュートリアルでは、一連のデータベースレコードを表示する2つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="7e837-108">ここでは、一連のデータベースレコードを HTML テーブルに書式設定する2つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="7e837-109">まず、ビュー内でデータベースレコードを直接書式設定する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="7e837-110">次に、データベースレコードを書式設定するときにパーシャルを活用する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="7e837-111">このチュートリアルの目的は、ASP.NET MVC アプリケーションでデータベースデータの HTML テーブルを表示する方法について説明することです。</span><span class="sxs-lookup"><span data-stu-id="7e837-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="7e837-112">まず、Visual Studio に含まれているスキャフォールディングツールを使用して、レコードのセットを自動的に表示するビューを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="7e837-113">次に、データベースレコードを書式設定するときに、部分をテンプレートとして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e837-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="7e837-114">モデルクラスを作成する</span><span class="sxs-lookup"><span data-stu-id="7e837-114">Create the Model Classes</span></span>

<span data-ttu-id="7e837-115">ここでは、ムービーデータベーステーブルのレコードのセットを表示します。</span><span class="sxs-lookup"><span data-stu-id="7e837-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="7e837-116">ムービーデータベーステーブルには、次の列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7e837-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>

| <span data-ttu-id="7e837-117">**列名**</span><span class="sxs-lookup"><span data-stu-id="7e837-117">**Column Name**</span></span> | <span data-ttu-id="7e837-118">**データ型**</span><span class="sxs-lookup"><span data-stu-id="7e837-118">**Data Type**</span></span> | <span data-ttu-id="7e837-119">**Null を許容**</span><span class="sxs-lookup"><span data-stu-id="7e837-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e837-120">Id</span><span class="sxs-lookup"><span data-stu-id="7e837-120">Id</span></span> | <span data-ttu-id="7e837-121">Int</span><span class="sxs-lookup"><span data-stu-id="7e837-121">Int</span></span> | <span data-ttu-id="7e837-122">[False]</span><span class="sxs-lookup"><span data-stu-id="7e837-122">False</span></span> |
| <span data-ttu-id="7e837-123">[タイトル]</span><span class="sxs-lookup"><span data-stu-id="7e837-123">Title</span></span> | <span data-ttu-id="7e837-124">Nvarchar (200)</span><span class="sxs-lookup"><span data-stu-id="7e837-124">Nvarchar(200)</span></span> | <span data-ttu-id="7e837-125">[False]</span><span class="sxs-lookup"><span data-stu-id="7e837-125">False</span></span> |
| <span data-ttu-id="7e837-126">・</span><span class="sxs-lookup"><span data-stu-id="7e837-126">Director</span></span> | <span data-ttu-id="7e837-127">NVarchar (50)</span><span class="sxs-lookup"><span data-stu-id="7e837-127">NVarchar(50)</span></span> | <span data-ttu-id="7e837-128">[False]</span><span class="sxs-lookup"><span data-stu-id="7e837-128">False</span></span> |
| <span data-ttu-id="7e837-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="7e837-129">DateReleased</span></span> | <span data-ttu-id="7e837-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="7e837-130">DateTime</span></span> | <span data-ttu-id="7e837-131">[False]</span><span class="sxs-lookup"><span data-stu-id="7e837-131">False</span></span> |

<span data-ttu-id="7e837-132">ASP.NET MVC アプリケーションのムービーテーブルを表すために、モデルクラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e837-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="7e837-133">このチュートリアルでは、Microsoft Entity Framework を使用して、モデルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="7e837-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7e837-134">このチュートリアルでは、Microsoft Entity Framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="7e837-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="7e837-135">ただし、LINQ to SQL、NHibernate、ADO.NET などの ASP.NET MVC アプリケーションでは、さまざまなテクノロジを使用してデータベースとやり取りできることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="7e837-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="7e837-136">Entity Data Model ウィザードを起動するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="7e837-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="7e837-137">ソリューションエクスプローラーウィンドウで モデル フォルダーを右クリックし、メニューオプション 追加、**新しい項目** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="7e837-138">**[データ]** カテゴリを選択し、 **[ADO.NET Entity Data Model]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="7e837-139">データモデルに*MoviesDBModel*という名前を付け、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e837-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="7e837-140">[追加] ボタンをクリックすると、Entity Data Model ウィザードが表示されます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="7e837-141">ウィザードを完了するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="7e837-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="7e837-142">**[モデルの内容の選択]** ステップで、 **[データベースから生成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="7e837-143">**[データ接続の選択]** 手順で、 *MoviesDB*データ接続を使用し、接続設定に*MoviesDBEntities*という名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="7e837-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="7e837-144">**[次へ]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e837-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="7e837-145">**データベースオブジェクトの選択** ステップで、テーブル ノードを展開し、映画 テーブルを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="7e837-146">名前空間*モデル*を入力し、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e837-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="7e837-147">[LINQ to SQL クラスの作成 ![](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="7e837-148">**図 01**: LINQ to SQL クラスの作成 ([クリックしてフルサイズのイメージを表示する](displaying-a-table-of-database-data-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7e837-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>

<span data-ttu-id="7e837-149">Entity Data Model ウィザードを完了すると、Entity Data Model デザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="7e837-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="7e837-150">デザイナーには、ムービーエンティティが表示されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="7e837-151">[Entity Data Model デザイナーの ![](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span></span>

<span data-ttu-id="7e837-152">**図 02**: Entity Data Model デザイナー ([クリックしてフルサイズのイメージを表示](displaying-a-table-of-database-data-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7e837-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>

<span data-ttu-id="7e837-153">続行する前に、1つの変更を加える必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e837-153">We need to make one change before we continue.</span></span> <span data-ttu-id="7e837-154">Entity Data Wizard では、ムービーデータベーステーブルを表す、*ムービー*という名前のモデルクラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="7e837-155">映画クラスを使用して特定の映画を表現するため、クラスの名前を *、ムービーで*はなく*ムービー* (複数形ではなく単数形) に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e837-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="7e837-156">デザイナー画面でクラスの名前をダブルクリックし、ムービーからムービーにクラスの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e837-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="7e837-157">この変更を行った後、 **[保存]** ボタン (フロッピーディスクのアイコン) をクリックして、Movie クラスを生成します。</span><span class="sxs-lookup"><span data-stu-id="7e837-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="7e837-158">ムービーコントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="7e837-158">Create the Movies Controller</span></span>

<span data-ttu-id="7e837-159">これで、データベースレコードを表すことができるようになったので、映画のコレクションを返すコントローラーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="7e837-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="7e837-160">Visual Studio のソリューションエクスプローラーウィンドウで、Controllers フォルダーを右クリックし、メニューオプション [**追加]、[コントローラー** ] の順に選択します (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="7e837-161">[[コントローラーの追加] メニューの ![](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-161">[![The Add Controller Menu](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span></span>

<span data-ttu-id="7e837-162">**図 03**: [コントローラーの追加] メニュー ([クリックすると、フルサイズのイメージが表示](displaying-a-table-of-database-data-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7e837-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>

<span data-ttu-id="7e837-163">**[コントローラーの追加]** ダイアログが表示されたら、コントローラー名 MovieController を入力します (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="7e837-164">**[追加]** ボタンをクリックして、新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e837-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="7e837-165">[[コントローラーの追加] ダイアログ ![](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-165">[![The Add Controller dialog](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span></span>

<span data-ttu-id="7e837-166">**図 04**: [コントローラーの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image8.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7e837-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>

<span data-ttu-id="7e837-167">データベースレコードのセットを返すように、ムービーコントローラーによって公開されている Index () アクションを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e837-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="7e837-168">リスト1のコントローラーのようにコントローラーを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e837-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="7e837-169">**リスト1– Controllers\MovieController.vb**</span><span class="sxs-lookup"><span data-stu-id="7e837-169">**Listing 1 – Controllers\MovieController.vb**</span></span>

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="7e837-170">リスト1では、MoviesDBEntities クラスを使用して MoviesDB データベースを表します。</span><span class="sxs-lookup"><span data-stu-id="7e837-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="7e837-171">式の*エンティティ。Mo視聴セット。 ToList ()* は、ムービーデータベーステーブルからすべてのムービーのセットを返します。</span><span class="sxs-lookup"><span data-stu-id="7e837-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="7e837-172">ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="7e837-172">Create the View</span></span>

<span data-ttu-id="7e837-173">一連のデータベースレコードを HTML テーブルに表示する最も簡単な方法は、Visual Studio に用意されているスキャフォールディングを利用することです。</span><span class="sxs-lookup"><span data-stu-id="7e837-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="7e837-174">[ビルド] メニューの [ソリューションの**ビルド**] を選択して、アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="7e837-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="7e837-175">**[ビューの追加]** ダイアログボックスを開く前にアプリケーションをビルドする必要があります。そうしないと、データクラスがダイアログに表示されません。</span><span class="sxs-lookup"><span data-stu-id="7e837-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="7e837-176">Index () アクションを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="7e837-177">[ビューを追加 ![には](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-177">[![Adding a view](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="7e837-178">**図 05**: ビューを追加[する (クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image10.png)される)</span><span class="sxs-lookup"><span data-stu-id="7e837-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>

<span data-ttu-id="7e837-179">**[ビューの追加]** ダイアログボックスで、 **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="7e837-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="7e837-180">[ムービー] クラスを**ビューデータクラス**として選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="7e837-181">**ビューコンテンツ**として [*リスト*] を選択します (図6を参照)。</span><span class="sxs-lookup"><span data-stu-id="7e837-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="7e837-182">これらのオプションを選択すると、ムービーの一覧を表示する厳密に型指定されたビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="7e837-183">[[ビューの追加] ダイアログ ![](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-183">[![The Add View dialog](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="7e837-184">**図 06**: [ビューの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image12.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7e837-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>

<span data-ttu-id="7e837-185">**[追加]** ボタンをクリックすると、リスト2のビューが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="7e837-186">このビューには、映画のコレクションを反復処理し、ムービーの各プロパティを表示するために必要なコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7e837-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="7e837-187">**リスト2– Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7e837-187">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="7e837-188">アプリケーションを実行するには、メニューオプション [**デバッグ]、[デバッグの開始**] の順に選択するか、F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="7e837-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="7e837-189">アプリケーションを実行すると、Internet Explorer が起動します。</span><span class="sxs-lookup"><span data-stu-id="7e837-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="7e837-190">/ムービーの URL に移動すると、図7にページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="7e837-191">[映画のテーブルを ![する](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-191">[![A table of movies](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span></span>

<span data-ttu-id="7e837-192">**図 07**: ムービーのテーブル ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image14.png)される)</span><span class="sxs-lookup"><span data-stu-id="7e837-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>

<span data-ttu-id="7e837-193">図7のデータベースレコードのグリッドの外観について何も気にしない場合は、単純にインデックスビューを変更できます。</span><span class="sxs-lookup"><span data-stu-id="7e837-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="7e837-194">たとえば、インデックスビューを変更すると、 *DateReleased*ヘッダーを [*リリース日*] に変更できます。</span><span class="sxs-lookup"><span data-stu-id="7e837-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="7e837-195">部分的なテンプレートを作成する</span><span class="sxs-lookup"><span data-stu-id="7e837-195">Create a Template with a Partial</span></span>

<span data-ttu-id="7e837-196">ビューが複雑すぎる場合は、ビューをパーシャルに分割することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7e837-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="7e837-197">パーシャルを使用すると、ビューの理解と保守が容易になります。</span><span class="sxs-lookup"><span data-stu-id="7e837-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="7e837-198">各ムービーデータベースレコードをフォーマットするためのテンプレートとして使用できる部分を作成します。</span><span class="sxs-lookup"><span data-stu-id="7e837-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="7e837-199">部分を作成するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7e837-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="7e837-200">Views\Movie フォルダーを右クリックし、 **[ビューの追加]** メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="7e837-201">[*部分ビュー (.ascx) を作成する*] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="7e837-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="7e837-202">部分的な*テンプレート*に名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="7e837-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="7e837-203">**[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="7e837-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="7e837-204">*ビューデータクラス*として [ムービー] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="7e837-205">*ビューのコンテンツ*として [空] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e837-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="7e837-206">**[追加]** ボタンをクリックして、プロジェクトに部分を追加します。</span><span class="sxs-lookup"><span data-stu-id="7e837-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="7e837-207">これらの手順を完了したら、リスト3のように Molook テンプレート部分を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e837-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="7e837-208">**リスト3– Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="7e837-208">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="7e837-209">リスト3の部分には、1行のレコードのテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7e837-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="7e837-210">リスト4の変更されたインデックスビューでは、Mo閲覧テンプレート partial が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="7e837-211">**リスト4– Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7e837-211">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="7e837-212">リスト4のビューには、すべてのムービーを反復処理する For Each ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7e837-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="7e837-213">ムービーのフォーマットには、各ムービーに対して Mo視聴テンプレート部分が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="7e837-214">MovieTemplate は、RenderPartial () ヘルパーメソッドを呼び出すことによってレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="7e837-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="7e837-215">変更されたインデックスビューでは、データベースレコードのまったく同じ HTML テーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e837-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="7e837-216">しかし、ビューは大幅に簡素化されています。</span><span class="sxs-lookup"><span data-stu-id="7e837-216">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="7e837-217">RenderPartial () メソッドは、文字列を返さないため、他のヘルパーメソッドとは異なります。</span><span class="sxs-lookup"><span data-stu-id="7e837-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="7e837-218">そのため、&lt;% = Html. RenderPartial ()%&gt;ではなく &lt;% .Html 部分 ()%&gt; を使用して、RenderPartial () メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e837-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="7e837-219">要約</span><span class="sxs-lookup"><span data-stu-id="7e837-219">Summary</span></span>

<span data-ttu-id="7e837-220">このチュートリアルの目的は、一連のデータベースレコードを HTML テーブルに表示する方法を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="7e837-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="7e837-221">まず、Microsoft Entity Framework を利用して、コントローラーアクションから一連のデータベースレコードを返す方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="7e837-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="7e837-222">次に、Visual Studio のスキャフォールディングを使用して、項目のコレクションを自動的に表示するビューを生成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7e837-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="7e837-223">最後に、部分的なを利用して、ビューを簡略化する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="7e837-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="7e837-224">各データベースレコードをフォーマットできるように、部分をテンプレートとして使用する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="7e837-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e837-225">[前へ](creating-model-classes-with-linq-to-sql-vb.md)
> [次へ](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7e837-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
