---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: データベースの作成 | Microsoft Docs
author: microsoft
description: 手順 2. では、データベースを作成する手順を示します。この手順では、すべてのディナーデータと、このアプリケーションのすべてのデータを保持します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469300"
---
# <a name="create-a-database"></a><span data-ttu-id="0f6b2-103">データベースの作成</span><span class="sxs-lookup"><span data-stu-id="0f6b2-103">Create a Database</span></span>

<span data-ttu-id="0f6b2-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0f6b2-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="0f6b2-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="0f6b2-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="0f6b2-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションチュートリアル](introducing-the-nerddinner-tutorial.md)の手順2です。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="0f6b2-107">手順 2. では、データベースを作成する手順を示します。この手順では、すべてのディナーデータと、このアプリケーションのすべてのデータを保持します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="0f6b2-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="0f6b2-109">手順 2: データベースを作成する</span><span class="sxs-lookup"><span data-stu-id="0f6b2-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="0f6b2-110">ここでは、データベースを使用して、世界中のアプリケーションのディナーと RSVP のすべてのデータを格納します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="0f6b2-111">次の手順では、free SQL Server Express edition ( [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用して簡単にインストールできる) を使用してデータベースを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="0f6b2-112">記述するすべてのコードは、SQL Server Express と完全 SQL Server の両方で動作します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="0f6b2-113">新しい SQL Server Express データベースの作成</span><span class="sxs-lookup"><span data-stu-id="0f6b2-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="0f6b2-114">まず、web プロジェクトを右クリックし、 **[新しい項目の追加]** メニューコマンド&gt;選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="0f6b2-115">これにより、Visual Studio の [新しい項目の追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="0f6b2-116">"データ" カテゴリでフィルター処理し、"SQL Server データベース" 項目テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="0f6b2-117">ここでは、"" を作成する SQL Server Express データベースに名前を指定し、[ok] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="0f6b2-118">次に、このファイルをアプリの\_データディレクトリ (読み取りと書き込みの両方のセキュリティ Acl が既に設定されているディレクトリ) に追加するかどうかを確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="0f6b2-119">[はい] をクリックすると、新しいデータベースが作成され、ソリューションエクスプローラーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="0f6b2-120">データベース内にテーブルを作成する</span><span class="sxs-lookup"><span data-stu-id="0f6b2-120">Creating Tables within our Database</span></span>

<span data-ttu-id="0f6b2-121">これで、新しい空のデータベースが作成されました。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-121">We now have a new empty database.</span></span> <span data-ttu-id="0f6b2-122">いくつかのテーブルを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-122">Let's add some tables to it.</span></span>

<span data-ttu-id="0f6b2-123">これを行うには、Visual Studio 内の [サーバーエクスプローラー] タブウィンドウに移動します。これにより、データベースとサーバーを管理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="0f6b2-124">アプリケーションの \ App\_Data フォルダーに格納されている SQL Server Express データベースは、サーバーエクスプローラー内に自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="0f6b2-125">必要に応じて、[サーバーエクスプローラー] ウィンドウの上部にある [データベースに接続] アイコンを使用して、一覧に SQL Server データベース (ローカルとリモートの両方) を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="0f6b2-126">このデータベースに2つのテーブルを追加します。1つはディナーを格納するテーブル、もう1つは RSVP acceptances を追跡するためのテーブルです。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="0f6b2-127">新しいテーブルを作成するには、データベース内の "Tables" フォルダーを右クリックし、[新しいテーブルの追加] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="0f6b2-128">テーブルデザイナーが開き、テーブルのスキーマを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="0f6b2-129">"ディナー" テーブルでは、次の10列のデータが追加されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="0f6b2-130">"Dinid" 列をテーブルの一意の主キーにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="0f6b2-131">これを構成するには、[Dinid] 列を右クリックし、[主キーの設定] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="0f6b2-132">Dinare Id を主キーにするだけでなく、新しいデータ行がテーブルに追加されたときに自動的に値がインクリメントされる "identity" 列として構成する必要もあります (つまり、挿入された最初のディナー行の Dinは1、2番目に挿入された行になります)。には、2のような Dinid が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="0f6b2-133">これを行うには、[Dinid] 列を選択し、[列のプロパティ] エディターを使用して、列の "(Is Id)" プロパティを "Yes" に設定します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="0f6b2-134">標準の id の既定値を使用します (新しいディナー行ごとに1から増分1を開始します)。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="0f6b2-135">次に、Ctrl + S キーを押すか、または [**ファイル&gt;保存**] メニューコマンドを使用して、テーブルを保存します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="0f6b2-136">これにより、テーブルに名前を指定するように求められます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-136">This will prompt us to name the table.</span></span> <span data-ttu-id="0f6b2-137">"ディナー" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="0f6b2-138">新しいディナーテーブルは、サーバーエクスプローラーのデータベース内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="0f6b2-139">次に、上記の手順を繰り返し、"RSVP" テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="0f6b2-140">このテーブルには3つの列があります。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-140">This table with have 3 columns.</span></span> <span data-ttu-id="0f6b2-141">RsvpID 列を主キーとして設定し、さらに id 列にします。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="0f6b2-142">このファイルを保存し、"RSVP" という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="0f6b2-143">テーブル間の外部キーリレーションシップの設定</span><span class="sxs-lookup"><span data-stu-id="0f6b2-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="0f6b2-144">これで、データベース内に2つのテーブルが作成されました。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-144">We now have two tables within our database.</span></span> <span data-ttu-id="0f6b2-145">スキーマデザインの最後の手順では、これら2つのテーブル間に "一対多" リレーションシップを設定します。これにより、各ディナー行を、それに適用される0個以上の RSVP 行に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="0f6b2-146">これを行うには、"ディナー" テーブルの "Din Id" 列との外部キーリレーションシップを持つように、RSVP テーブルの "Dinの Id" 列を構成します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="0f6b2-147">これを行うには、サーバーエクスプローラーでテーブルデザイナー内の RSVP テーブルをダブルクリックして、そのテーブルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="0f6b2-148">次に、その中の "Dinの Id" 列を選択し、右クリックして、[リレーションシップ...] を選択します。コンテキストメニューコマンド:</span><span class="sxs-lookup"><span data-stu-id="0f6b2-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="0f6b2-149">これにより、テーブル間のリレーションシップを設定するために使用できるダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="0f6b2-150">[追加] ボタンをクリックして、ダイアログに新しいリレーションシップを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="0f6b2-151">リレーションシップを追加したら、ダイアログの右側にあるプロパティグリッド内の [テーブルと列の指定] ツリービューノードを展開し、[...] をクリックします。右側のボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="0f6b2-152">[...] をクリックすると、ボタンをクリックすると、リレーションシップに関係するテーブルと列を指定したり、リレーションシップに名前を付けたりできるようにするためのダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="0f6b2-153">主キーテーブルを "ディナー" に変更し、ディナーテーブル内の "Din Id" 列を主キーとして選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="0f6b2-154">RSVP テーブルは外部キーテーブル、および RSVP です。Dinの Id 列は、外部キーとして関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="0f6b2-155">これで、RSVP テーブルの各行が、ディナーテーブルの行に関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="0f6b2-156">SQL Server は参照整合性を維持し、有効なディナー行を指していない場合は新しい RSVP 行を追加しないようにします。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="0f6b2-157">また、これを参照している予約行がある場合は、ディナー行を削除できなくなります。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="0f6b2-158">テーブルへのデータの追加</span><span class="sxs-lookup"><span data-stu-id="0f6b2-158">Adding Data to our Tables</span></span>

<span data-ttu-id="0f6b2-159">それでは、いくつかのサンプルデータをディナーテーブルに追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="0f6b2-160">テーブルにデータを追加するには、サーバーエクスプローラー内で右クリックし、[テーブルデータの表示] コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="0f6b2-161">ここでは、アプリケーションの実装を開始するときに使用できるディナーデータを数行追加します。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="0f6b2-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="0f6b2-162">Next Step</span></span>

<span data-ttu-id="0f6b2-163">これで、データベースの作成が完了しました。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-163">We've finished creating our database.</span></span> <span data-ttu-id="0f6b2-164">クエリと更新に使用できるモデルクラスを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="0f6b2-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0f6b2-165">[前へ](create-a-new-aspnet-mvc-project.md)
> [次へ](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="0f6b2-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
