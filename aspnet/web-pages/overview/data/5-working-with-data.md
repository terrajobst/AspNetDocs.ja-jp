---
uid: web-pages/overview/data/5-working-with-data
title: ASP.NET Web ページ (Razor) サイトでのデータベースの操作の概要 |Microsoft Docs
author: Rick-Anderson
description: この章では、ASP.NET Web ページを使用してデータベースのデータにアクセスし、そのデータを表示する方法について説明します。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474040"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="bfa57-103">ASP.NET Web ページ (Razor) サイトでのデータベースの操作の概要</span><span class="sxs-lookup"><span data-stu-id="bfa57-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="bfa57-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bfa57-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bfa57-105">この記事では、Microsoft WebMatrix ツールを使用して ASP.NET Web ページ (Razor) web サイトにデータベースを作成する方法と、データの表示、追加、編集、および削除を行うためのページの作成方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="bfa57-106">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="bfa57-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="bfa57-107">データベースを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="bfa57-107">How to create a database.</span></span>
> - <span data-ttu-id="bfa57-108">データベースに接続する方法。</span><span class="sxs-lookup"><span data-stu-id="bfa57-108">How to connect to a database.</span></span>
> - <span data-ttu-id="bfa57-109">Web ページでデータを表示する方法。</span><span class="sxs-lookup"><span data-stu-id="bfa57-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="bfa57-110">データベースレコードを挿入、更新、および削除する方法。</span><span class="sxs-lookup"><span data-stu-id="bfa57-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="bfa57-111">この記事で紹介した機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="bfa57-112">Microsoft SQL Server Compact Edition データベースを操作する。</span><span class="sxs-lookup"><span data-stu-id="bfa57-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="bfa57-113">SQL クエリの操作</span><span class="sxs-lookup"><span data-stu-id="bfa57-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="bfa57-114">`Database` クラスです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bfa57-115">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="bfa57-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bfa57-116">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="bfa57-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="bfa57-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="bfa57-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="bfa57-118">このチュートリアルでは、WebMatrix 3 も使用できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="bfa57-119">ASP.NET Web ページ3と Visual Studio 2013 (または、Web の場合は Visual Studio Express 2013) を使用できます。ただし、ユーザーインターフェイスは異なります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>

## <a name="introduction-to-databases"></a><span data-ttu-id="bfa57-120">データベースの概要</span><span class="sxs-lookup"><span data-stu-id="bfa57-120">Introduction to Databases</span></span>

<span data-ttu-id="bfa57-121">一般的なアドレス帳を想像してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-121">Imagine a typical address book.</span></span> <span data-ttu-id="bfa57-122">アドレス帳の各エントリ (つまり、各ユーザーについて) には、名、姓、住所、電子メールアドレス、電話番号など、いくつかの情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="bfa57-123">このようなデータをピクチャする一般的な方法は、行と列を含むテーブルです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="bfa57-124">データベース用語では、各行がレコードと呼ばれることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="bfa57-125">各列 (フィールドとも呼ばれます) には、各データ型の値 (名、姓、およびなど) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="bfa57-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="bfa57-126">**ID**</span></span> | <span data-ttu-id="bfa57-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="bfa57-127">**FirstName**</span></span> | <span data-ttu-id="bfa57-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="bfa57-128">**LastName**</span></span> | <span data-ttu-id="bfa57-129">**アドレス**</span><span class="sxs-lookup"><span data-stu-id="bfa57-129">**Address**</span></span> | <span data-ttu-id="bfa57-130">**電子メール**</span><span class="sxs-lookup"><span data-stu-id="bfa57-130">**Email**</span></span> | <span data-ttu-id="bfa57-131">**電話**</span><span class="sxs-lookup"><span data-stu-id="bfa57-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="bfa57-132">1</span><span class="sxs-lookup"><span data-stu-id="bfa57-132">1</span></span> | <span data-ttu-id="bfa57-133">Jim</span><span class="sxs-lookup"><span data-stu-id="bfa57-133">Jim</span></span> | <span data-ttu-id="bfa57-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="bfa57-134">Abrus</span></span> | <span data-ttu-id="bfa57-135">210 100th St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="bfa57-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="bfa57-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="bfa57-136">555 0100</span></span> |
| <span data-ttu-id="bfa57-137">2</span><span class="sxs-lookup"><span data-stu-id="bfa57-137">2</span></span> | <span data-ttu-id="bfa57-138">Terry</span><span class="sxs-lookup"><span data-stu-id="bfa57-138">Terry</span></span> | <span data-ttu-id="bfa57-139">Adams</span><span class="sxs-lookup"><span data-stu-id="bfa57-139">Adams</span></span> | <span data-ttu-id="bfa57-140">1234メインセント Seattle WA 99011</span><span class="sxs-lookup"><span data-stu-id="bfa57-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="bfa57-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="bfa57-141">555 0101</span></span> |

<span data-ttu-id="bfa57-142">ほとんどのデータベーステーブルでは、テーブルには、顧客番号や口座番号などの一意の識別子を含む列が必要です。これはテーブルの*主キー*と呼ばれ、テーブルの各行を識別するために使用します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="bfa57-143">この例では、ID 列はアドレス帳の主キーです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="bfa57-144">この基本的なデータベースの理解により、単純なデータベースを作成し、データの追加、変更、削除などの操作を実行する方法を学ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="bfa57-145">**リレーショナル データベース**</span><span class="sxs-lookup"><span data-stu-id="bfa57-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="bfa57-146">テキストファイルやスプレッドシートなど、さまざまな方法でデータを格納できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="bfa57-147">ただし、ほとんどのビジネスでは、データはリレーショナルデータベースに格納されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="bfa57-148">この記事では、データベースについてあまり詳しく説明しません。</span><span class="sxs-lookup"><span data-stu-id="bfa57-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="bfa57-149">ただし、この点について理解しておくと役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="bfa57-150">リレーショナルデータベースでは、情報は論理的に個別のテーブルに分割されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="bfa57-151">たとえば、school のデータベースには、学生やクラスオファリング用に個別のテーブルが含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="bfa57-152">データベースソフトウェア (SQL Server など) では、テーブル間のリレーションシップを動的に確立できる強力なコマンドがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="bfa57-153">たとえば、リレーショナルデータベースを使用して、スケジュールを作成するために、学生とクラスの間に論理的な関係を確立することができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="bfa57-154">データを別のテーブルに格納すると、テーブル構造の複雑さが軽減され、テーブルに冗長なデータを保持する必要性が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="bfa57-155">データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-155">Creating a Database</span></span>

<span data-ttu-id="bfa57-156">この手順では、WebMatrix に含まれる SQL Server Compact データベースデザインツールを使用して、SmallBakery という名前のデータベースを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="bfa57-157">コードを使用してデータベースを作成することもできますが、WebMatrix などのデザインツールを使用してデータベーステーブルとデータベーステーブルを作成する方が一般的です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="bfa57-158">WebMatrix を起動し、[クイックスタート] ページで、[**テンプレートからサイト**を] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="bfa57-159">**[空のサイト]** を選択し、 **[サイト名]** ボックスに「SmallBakery」と入力して、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="bfa57-160">サイトが作成され、WebMatrix で表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="bfa57-161">左側のウィンドウで、 **[データベース]** ワークスペースをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="bfa57-162">リボンの **[新しいデータベース]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="bfa57-163">空のデータベースは、サイトと同じ名前で作成されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="bfa57-164">左側のウィンドウで、 **SmallBakery**ノードを展開し、 **[テーブル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="bfa57-165">リボンの **[新しいテーブル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="bfa57-166">WebMatrix によってテーブルデザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-166">WebMatrix opens the table designer.</span></span>

    ![[画像]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="bfa57-168">**[名前]** 列をクリックし、&quot;Id&quot;を入力します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="bfa57-169">**[データ型]** 列で、 **[int]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="bfa57-170">[**主キー**を**指定**しますか?] オプションを **[はい]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="bfa57-171">名前が示すように、 **Is Primary Key は**、これがテーブルの主キーになることをデータベースに通知します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="bfa57-172">Id は、新しいレコードごとに自動的に ID 番号が作成**さ**れ、次の連続番号 (1 から開始) が割り当てられるように、データベースに指示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="bfa57-173">次の行をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-173">Click in the next row.</span></span> <span data-ttu-id="bfa57-174">新しい列の定義が開始されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="bfa57-175">[名前] の値には &quot;名前&quot;を入力します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="bfa57-176">**[データ型]** で &quot;nvarchar&quot; を選択し、長さを50に設定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="bfa57-177">`nvarchar` の*var*部分は、この列のデータがレコードごとにサイズが異なる可能性がある文字列であることをデータベースに伝えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="bfa57-178">( *N*プレフィックスは*national*を表します。これは、任意のアルファベットを表す文字データや、フィールド&#8212;が Unicode データを保持していることを示す書記体系を持つことができることを示します)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="bfa57-179">**[Null]** を許容 オプションを **[いいえ]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="bfa57-180">これにより、 *Name*列が空白のままにならないことが強制されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="bfa57-181">この同じプロセスを使用して、 *Description*という名前の列を作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="bfa57-182">長さとして **[データ型]** を "nvarchar"、"50" に設定し、 **[null]** を許容 を false に設定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="bfa57-183">*Price*という名前の列を作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-183">Create a column named *Price*.</span></span> <span data-ttu-id="bfa57-184">**[データ型] を "money" に**設定し、[ **null**を許容] を false に設定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="bfa57-185">上部にあるボックスに、テーブル &quot;Product&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="bfa57-186">完了すると、定義は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-186">When you're done, the definition will look like this:</span></span>

    ![[画像]](5-working-with-data/_static/image2.png)
17. <span data-ttu-id="bfa57-188">Ctrl + S キーを押して、テーブルを保存します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="bfa57-189">データベースへのデータの追加</span><span class="sxs-lookup"><span data-stu-id="bfa57-189">Adding Data to the Database</span></span>

<span data-ttu-id="bfa57-190">これで、記事の後半で使用するサンプルデータをデータベースに追加できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="bfa57-191">左側のウィンドウで、 **SmallBakery**ノードを展開し、 **[テーブル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="bfa57-192">Product テーブルを右クリックし、 **[データ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="bfa57-193">[編集] ウィンドウで、次のレコードを入力します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="bfa57-194">**名前**</span><span class="sxs-lookup"><span data-stu-id="bfa57-194">**Name**</span></span> | <span data-ttu-id="bfa57-195">**説明**</span><span class="sxs-lookup"><span data-stu-id="bfa57-195">**Description**</span></span> | <span data-ttu-id="bfa57-196">**標準**</span><span class="sxs-lookup"><span data-stu-id="bfa57-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="bfa57-197">階層</span><span class="sxs-lookup"><span data-stu-id="bfa57-197">Bread</span></span> | <span data-ttu-id="bfa57-198">毎日新しく焼きます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-198">Baked fresh every day.</span></span> | <span data-ttu-id="bfa57-199">2.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-199">2.99</span></span> |
    | <span data-ttu-id="bfa57-200">Strawberry の短いケーキ</span><span class="sxs-lookup"><span data-stu-id="bfa57-200">Strawberry Shortcake</span></span> | <span data-ttu-id="bfa57-201">この庭園から、有機いちごを使用しました。</span><span class="sxs-lookup"><span data-stu-id="bfa57-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="bfa57-202">9.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-202">9.99</span></span> |
    | <span data-ttu-id="bfa57-203">Apple 円</span><span class="sxs-lookup"><span data-stu-id="bfa57-203">Apple Pie</span></span> | <span data-ttu-id="bfa57-204">2番目は、mom の円に対してのみです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="bfa57-205">12.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-205">12.99</span></span> |
    | <span data-ttu-id="bfa57-206">Pecan 円</span><span class="sxs-lookup"><span data-stu-id="bfa57-206">Pecan Pie</span></span> | <span data-ttu-id="bfa57-207">Pecans を希望する場合は、この方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="bfa57-208">10.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-208">10.99</span></span> |
    | <span data-ttu-id="bfa57-209">レモン円</span><span class="sxs-lookup"><span data-stu-id="bfa57-209">Lemon Pie</span></span> | <span data-ttu-id="bfa57-210">最高の lemons が世界中で作成されました。</span><span class="sxs-lookup"><span data-stu-id="bfa57-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="bfa57-211">11.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-211">11.99</span></span> |
    | <span data-ttu-id="bfa57-212">カップケーキ</span><span class="sxs-lookup"><span data-stu-id="bfa57-212">Cupcakes</span></span> | <span data-ttu-id="bfa57-213">子供と子供たちはこれらを気に入っています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="bfa57-214">7.99</span><span class="sxs-lookup"><span data-stu-id="bfa57-214">7.99</span></span> |

    <span data-ttu-id="bfa57-215">*Id*列に何も入力する必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="bfa57-216">*Id*列を作成した場合**は**、[id] プロパティを [true] に設定します。これにより、自動的に入力されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="bfa57-217">データの入力が完了すると、テーブルデザイナーは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[画像]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="bfa57-219">データベースデータを含むタブを閉じます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="bfa57-220">データベースのデータの表示</span><span class="sxs-lookup"><span data-stu-id="bfa57-220">Displaying Data from a Database</span></span>

<span data-ttu-id="bfa57-221">データが含まれているデータベースがあれば、ASP.NET の web ページでデータを表示できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="bfa57-222">表示するテーブル行を選択するには、データベースに渡すコマンドである SQL ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="bfa57-223">左側のウィンドウで、 **[ファイル]** ワークスペースをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="bfa57-224">Web サイトのルートで、 *Listproducts. cshtml*という名前の新しい cshtml ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="bfa57-225">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="bfa57-226">最初のコードブロックで、前に作成した*SmallBakery*ファイル (データベース) を開きます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="bfa57-227">`Database.Open` メソッドは、 *.sdf*ファイルが web サイトの*アプリ\_Data*フォルダーにあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="bfa57-228">( *.Sdf*拡張子&#8212;を指定する必要がないことに注意してください。実行すると、`Open` メソッドは機能しません。)</span><span class="sxs-lookup"><span data-stu-id="bfa57-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="bfa57-229">*App\_data*フォルダーは、データファイルの格納に使用される ASP.NET の特別なフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="bfa57-230">詳細については、この記事で後述[する「データベースへの接続](#SB_ConnectingToADatabase)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="bfa57-231">次に、次の SQL `Select` ステートメントを使用して、データベースに対してクエリを実行するように要求します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="bfa57-232">ステートメントでは、`Product` は、クエリを実行するテーブルを識別します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="bfa57-233">`*` 文字は、クエリがテーブルからすべての列を返す必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="bfa57-234">(一部の列のみを表示する場合は、列をコンマで区切って個別に一覧表示することもできます)。`Order By` 句は、この場合、*名前*列を&#8212;使用してデータを並べ替える方法を示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="bfa57-235">つまり、各行の  *Name (名前*) 列の値に基づいてデータがアルファベット順に並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="bfa57-236">ページの本文では、マークアップによって、データの表示に使用される HTML テーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="bfa57-237">`<tbody>` 要素内では、クエリによって返される各データ行を個別に取得するために、`foreach` ループを使用します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="bfa57-238">各データ行に対して、HTML テーブルの行 (`<tr>` 要素) を作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="bfa57-239">次に、各列の HTML テーブルセル (`<td>` 要素) を作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="bfa57-240">ループを進めるたびに、データベースから次に使用できる行が `row` 変数に含まれます (`foreach` ステートメントで設定します)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="bfa57-241">行から個々の列を取得するには、`row.Name` または `row.Description` を使用するか、必要な列の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="bfa57-242">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-242">Run the page in a browser.</span></span> <span data-ttu-id="bfa57-243">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。ページには、次のような一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[画像]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="bfa57-245">**構造化照会言語 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="bfa57-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="bfa57-246">SQL は、データベース内のデータを管理するためにほとんどのリレーショナルデータベースで使用される言語です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="bfa57-247">これには、データを取得して更新するためのコマンドと、データベーステーブルの作成、変更、および管理を行うためのコマンドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="bfa57-248">Sql は、(WebMatrix で使用しているものと同様に) プログラミング言語とは異なります。 SQL では、データベースに必要なものを通知し、データを取得またはタスクを実行する方法を判断するためのデータベースのジョブです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="bfa57-249">いくつかの SQL コマンドとその実行内容の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="bfa57-250">*Price*の値が10を超える場合、これによって*Product*テーブルのレコードから*Id*、 *Name*、および*Price*列がフェッチされ、 *name*列の値に基づいてアルファベット順に結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="bfa57-251">このコマンドは、条件に一致するレコードを含む結果セットを返すか、レコードが一致しない場合は空のセットを返します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="bfa57-252">これにより、 *Product*テーブルに新しいレコードが挿入され、 *Name*列が &quot;クロワッサン&quot;に、 *Description*列が不安定な満足させる&quot;&quot;、価格が1.99 に設定されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="bfa57-253">このコマンドは、有効期限の日付列が2008年1月1日より前の*製品*テーブル内のレコードを削除します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="bfa57-254">(もちろん、 *Product*テーブルにはこのような列があることを前提としています)。日付は MM/DD/YYYY 形式で入力しますが、ロケールに使用する形式で入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="bfa57-255">`Insert Into` と `Delete` のコマンドでは、結果セットは返されません。</span><span class="sxs-lookup"><span data-stu-id="bfa57-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="bfa57-256">代わりに、コマンドによって影響を受けたレコードの数を示す数値が返されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="bfa57-257">これらの操作 (レコードの挿入や削除など) の一部では、操作を要求しているプロセスがデータベース内で適切な権限を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="bfa57-258">このため、実稼働データベースでは、データベースに接続するときにユーザー名とパスワードを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="bfa57-259">SQL コマンドは多数ありますが、これらはすべて、次のようなパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="bfa57-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="bfa57-260">SQL コマンドを使用して、データベーステーブルを作成したり、テーブル内のレコード数をカウントしたり、価格を計算したり、多くの操作を実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

## <a name="inserting-data-in-a-database"></a><span data-ttu-id="bfa57-261">データベースへのデータの挿入</span><span class="sxs-lookup"><span data-stu-id="bfa57-261">Inserting Data in a Database</span></span>

<span data-ttu-id="bfa57-262">このセクションでは、ユーザーが*製品*データベーステーブルに新しい製品を追加できるページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="bfa57-263">新しい製品レコードが挿入されると、前のセクションで作成した*Listproducts. cshtml*ページを使用して、更新されたテーブルがページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="bfa57-264">このページには、ユーザーが入力したデータがデータベースに対して有効であることを確認するための検証が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="bfa57-265">たとえば、ページ内のコードは、すべての必須列に対して値が入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="bfa57-266">Web サイトで、 *Insertproducts. cshtml*という名前の新しい cshtml ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="bfa57-267">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="bfa57-268">ページの本文には、ユーザーが名前、説明、および価格を入力できるようにする3つのテキストボックスを含む HTML フォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="bfa57-269">ユーザーが **[挿入]** ボタンをクリックすると、ページ上部のコードによって*SmallBakery*データベースへの接続が開かれます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="bfa57-270">次に、`Request` オブジェクトを使用してユーザーが送信した値を取得し、それらの値をローカル変数に代入します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="bfa57-271">ユーザーが各必須列に値を入力したことを検証するには、検証する各 `<input>` 要素を登録します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="bfa57-272">`Validation` ヘルパーは、登録した各フィールドに値があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="bfa57-273">`Validation.IsValid()`をチェックすることで、すべてのフィールドが検証に合格したかどうかをテストできます。通常は、ユーザーから取得した情報を処理する前に実行します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="bfa57-274">(`&&` 演算子は、とを意味します。このテストは、*これがフォーム送信であり、すべてのフィールドが検証に合格している場合*に行います)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="bfa57-275">すべての列が検証されている (空でない) 場合は、データを挿入する SQL ステートメントを作成し、次のように実行します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="bfa57-276">挿入する値には、パラメーターのプレースホルダー (`@0`、`@1`、`@2`) を含めます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="bfa57-277">セキュリティ上の理由から、前の例で示したように、パラメーターを使用して、常に値を SQL ステートメントに渡します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="bfa57-278">これにより、ユーザーのデータを検証できるだけでなく、悪意のあるコマンドをデータベースに送信しようとする試み (SQL インジェクション攻撃と呼ばれることもあります) を防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="bfa57-279">このクエリを実行するには、次のステートメントを使用して、プレースホルダーを置き換える値を含む変数を渡します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="bfa57-280">`Insert Into` ステートメントが実行された後、次の行を使用して製品の一覧を表示するページにユーザーを送信します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="bfa57-281">検証が成功しなかった場合は、挿入をスキップします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="bfa57-282">このページには、蓄積されたエラーメッセージを表示できるヘルパー (存在する場合) があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="bfa57-283">マークアップのスタイルブロックに `.validation-summary-errors`という名前の CSS クラス定義が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="bfa57-284">これは、検証エラーを含む `<div>` 要素に既定で使用される CSS クラスの名前です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="bfa57-285">この場合、CSS クラスは、検証の概要エラーを赤および太字で表示するように指定しますが、`.validation-summary-errors` クラスを定義して任意の書式を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="bfa57-286">挿入ページのテスト</span><span class="sxs-lookup"><span data-stu-id="bfa57-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="bfa57-287">ブラウザーでページを表示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-287">View the page in a browser.</span></span> <span data-ttu-id="bfa57-288">ページには、次の図に示すようなフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[画像]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="bfa57-290">すべての列の値を入力しますが、[*価格*] 列は空白のままにしてください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="bfa57-291">[挿入] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-291">Click **Insert**.</span></span> <span data-ttu-id="bfa57-292">次の図に示すように、ページにエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="bfa57-293">(新しいレコードは作成されません)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-293">(No new record is created.)</span></span>

    ![[画像]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="bfa57-295">フォーム全体を入力し、 **[挿入]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="bfa57-296">今度は、 *Listproducts. cshtml*ページが表示され、新しいレコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="bfa57-297">データベース内のデータの更新</span><span class="sxs-lookup"><span data-stu-id="bfa57-297">Updating Data in a Database</span></span>

<span data-ttu-id="bfa57-298">データがテーブルに入力されたら、更新が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="bfa57-299">この手順では、前にデータを挿入するために作成したものと似た2つのページを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="bfa57-300">最初のページには製品が表示され、ユーザーは変更する製品を選択できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="bfa57-301">2番目のページでは、ユーザーが実際に編集を行って保存することができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bfa57-302">**重要**運用 web サイトでは、通常、データを変更できるユーザーを制限します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="bfa57-303">メンバーシップの設定方法と、サイトでのタスクの実行をユーザーに承認する方法の詳細については、「 [ASP.NET Web ページサイトへのセキュリティとメンバーシップの追加](https://go.microsoft.com/fwlink/?LinkId=202904)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="bfa57-304">Web サイトで、 *Editproducts. cshtml*という名前の新しい cshtml ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="bfa57-305">ファイルの既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="bfa57-306">このページと前の*Listproducts. cshtml*ページの唯一の違いは、このページの HTML テーブルには、**編集**リンクを表示する列が追加されていることです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="bfa57-307">このリンクをクリックすると、選択したレコードを編集できる [ *Updateproducts. cshtml* ] ページ (次に作成します) に移動します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="bfa57-308">**編集**リンクを作成するコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="bfa57-309">これにより、`href` 属性が動的に設定される HTML `<a>` 要素が作成されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="bfa57-310">`href` 属性は、ユーザーがリンクをクリックしたときに表示されるページを指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="bfa57-311">また、現在の行の `Id` 値がリンクに渡されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="bfa57-312">ページが実行されると、ページソースに次のようなリンクが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="bfa57-313">`href` 属性が `UpdateProducts/n`に設定されていることに注意してください。ここで、 *n*は製品番号です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="bfa57-314">ユーザーがこれらのリンクのいずれかをクリックすると、結果の URL は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="bfa57-315">つまり、編集する製品番号は URL で渡されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="bfa57-316">ブラウザーでページを表示します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-316">View the page in a browser.</span></span> <span data-ttu-id="bfa57-317">ページには、次のような形式でデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-317">The page displays the data in a format like this:</span></span>

    ![[画像]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="bfa57-319">次に、ユーザーが実際にデータを更新できるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="bfa57-320">[更新] ページには、ユーザーが入力したデータを検証するための検証が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="bfa57-321">たとえば、ページ内のコードは、すべての必須列に対して値が入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="bfa57-322">Web サイトで、 *Updateproducts. cshtml*という名前の新しい cshtml ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="bfa57-323">ファイルの既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="bfa57-324">ページの本文には、製品が表示され、ユーザーが編集できる HTML フォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="bfa57-325">表示する製品を取得するには、次の SQL ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="bfa57-326">これにより、ID が `@0` パラメーターで渡された値と一致する製品が選択されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="bfa57-327">( *Id*は主キーであるため、一意である必要があるため、この方法で選択できる製品レコードは1つだけです)。この `Select` ステートメントに渡す ID 値を取得するには、次の構文を使用して、URL の一部としてページに渡される値を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="bfa57-328">実際に製品レコードをフェッチするには、`QuerySingle` メソッドを使用します。これにより、1つのレコードのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="bfa57-329">単一行が `row` 変数に返されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="bfa57-330">各列からデータを取得し、次のようにローカル変数に割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="bfa57-331">フォームのマークアップでは、次のような埋め込みコードを使用して、これらの値が個々のテキストボックスに自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="bfa57-332">コードのその部分では、更新する製品レコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="bfa57-333">レコードが表示されたら、ユーザーは個々の列を編集できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="bfa57-334">ユーザーが **[更新]** ボタンをクリックしてフォームを送信すると、`if(IsPost)` ブロック内のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="bfa57-335">これにより、`Request` オブジェクトからユーザーの値を取得し、値を変数に格納して、各列に入力されたことを検証します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="bfa57-336">検証が成功した場合、コードは次の SQL Update ステートメントを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="bfa57-337">SQL `Update` ステートメントでは、更新する各列と、それに設定する値を指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="bfa57-338">このコードでは、パラメーターのプレースホルダー `@0`、`@1`、`@2`などを使用して値を指定します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="bfa57-339">(前述のように、セキュリティのために、パラメーターを使用して、常に値を SQL ステートメントに渡す必要があります)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="bfa57-340">`db.Execute` メソッドを呼び出す場合は、次のように、SQL ステートメントのパラメーターに対応する順序で値を含む変数を渡します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="bfa57-341">`Update` ステートメントを実行した後、次のメソッドを呼び出して、ユーザーを編集ページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="bfa57-342">結果として、ユーザーにはデータベース内のデータの更新された一覧が表示され、別の製品を編集できるようになります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="bfa57-343">ページを保存します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-343">Save the page.</span></span>
7. <span data-ttu-id="bfa57-344">[更新] ページではなく [ *Editproducts. cshtml* ] ページを実行し、 **[編集]** をクリックして編集する製品を選択します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="bfa57-345">*Updateproducts. cshtml*ページが表示され、選択したレコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[画像]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="bfa57-347">変更を行い、 **[更新]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-347">Make a change and click **Update**.</span></span> <span data-ttu-id="bfa57-348">更新後のデータと共に、製品の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="bfa57-349">データベース内のデータの削除</span><span class="sxs-lookup"><span data-stu-id="bfa57-349">Deleting Data in a Database</span></span>

<span data-ttu-id="bfa57-350">このセクションで*は、ユーザーが製品データベーステーブル*から製品を削除できるようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="bfa57-351">この例は、2つのページで構成されています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-351">The example consists of two pages.</span></span> <span data-ttu-id="bfa57-352">最初のページでは、削除するレコードをユーザーが選択します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="bfa57-353">削除するレコードは、レコードを削除するかどうかを確認できる2番目のページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bfa57-354">**重要**運用 web サイトでは、通常、データを変更できるユーザーを制限します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="bfa57-355">メンバーシップを設定する方法と、サイトでのタスクの実行をユーザーに承認する方法については、「 [ASP.NET Web ページサイトへのセキュリティとメンバーシップの追加](https://go.microsoft.com/fwlink/?LinkId=202904)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfa57-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="bfa57-356">Web サイトで、 *List$ Fordelete. cshtml*という名前の新しい cshtml ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="bfa57-357">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="bfa57-358">このページは、前の「 *Editproducts. cshtml* 」ページに似ています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="bfa57-359">ただし、各製品の**編集**リンクを表示するのではなく、 **[削除]** リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="bfa57-360">**削除**リンクは、マークアップ内の次の埋め込みコードを使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="bfa57-361">これにより、ユーザーがリンクをクリックしたときに、次のような URL が作成されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="bfa57-362">URL は、 *deleteproduct. cshtml*という名前のページを呼び出し (次に作成します)、削除する製品の ID (ここでは 4) を渡します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="bfa57-363">ファイルを保存しますが、開いたままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="bfa57-364">*Deleteproduct. cshtml*という名前の別の CHTML ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="bfa57-365">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="bfa57-366">このページは*listproduct Fordelete. cshtml*によって呼び出され、ユーザーが製品を削除することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="bfa57-367">削除する製品の一覧を表示するには、次のコードを使用して、URL から削除する製品の ID を取得します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="bfa57-368">このページでは、ユーザーに対して、レコードを実際に削除するボタンをクリックするように求められます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="bfa57-369">これは重要なセキュリティ対策です。データの更新や削除など、web サイトで機密性の高い操作を実行する場合、これらの操作は常に、GET 操作ではなく POST 操作を使用して実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="bfa57-370">GET 操作を使用して削除操作を実行できるようにサイトがセットアップされている場合、だれでも `http://<server>/DeleteProduct/4` のような URL を渡したり、データベースから必要なものを削除したりできます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="bfa57-371">投稿を使用してのみ削除を実行できるように、確認を追加してページをコーディングすることで、サイトにセキュリティの測定単位を追加します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="bfa57-372">実際の削除操作は、次のコードを使用して実行されます。このコードは、最初にこれが post 操作であり、ID が空でないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="bfa57-373">このコードは、指定されたレコードを削除する SQL ステートメントを実行し、ユーザーをリストページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="bfa57-374">ブラウザーで*List$ Fordelete*を実行します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[画像]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="bfa57-376">いずれかの製品の **[削除]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="bfa57-377">削除するレコードがあることを確認するために、 *Deleteproduct. cshtml*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="bfa57-378">**[削除]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bfa57-378">Click the **Delete** button.</span></span> <span data-ttu-id="bfa57-379">製品レコードが削除され、更新された製品一覧でページが更新されます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="bfa57-380">データベースに接続する</span><span class="sxs-lookup"><span data-stu-id="bfa57-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="bfa57-381">データベースに接続するには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="bfa57-382">1つ目は、`Database.Open` メソッドを使用して、データベースファイルの名前を指定することです (.sdf 拡張子は*ありません*)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="bfa57-383">`Open` メソッドは、がであることを前提としています。 *.sdf*ファイルは、web サイトの*App\_Data*フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="bfa57-384">このフォルダーは、データを保持するために特に設計されています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="bfa57-385">たとえば、web サイトにデータの読み取りと書き込みを許可するための適切なアクセス許可があり、セキュリティ対策として、WebMatrix はこのフォルダーからのファイルへのアクセスを許可しません。</span><span class="sxs-lookup"><span data-stu-id="bfa57-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="bfa57-386">2番目の方法は、接続文字列を使用することです。</span><span class="sxs-lookup"><span data-stu-id="bfa57-386">The second way is to use a connection string.</span></span> <span data-ttu-id="bfa57-387">データベースに接続する方法に関する情報が含まれる接続文字列。</span><span class="sxs-lookup"><span data-stu-id="bfa57-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="bfa57-388">これにはファイルパスを含めることができます。または、ローカルサーバーまたはリモートサーバー上の SQL Server データベースの名前と、そのサーバーに接続するためのユーザー名とパスワードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="bfa57-389">(ホスティングプロバイダーのサイトなど、集中管理されているバージョンの SQL Server にデータを保持する場合は、常に接続文字列を使用してデータベース接続情報を指定します)。</span><span class="sxs-lookup"><span data-stu-id="bfa57-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="bfa57-390">WebMatrix では、通常、接続文字列は web.config という名前の XML ファイルに格納さ*れます。* 名前が示すように、 *web*サイトのルートにある web.config ファイルを使用して、サイトの構成情報 (サイトで必要となる可能性のある接続文字列など) を保存できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="bfa57-391">*Web.config ファイル内*の接続文字列の例は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="bfa57-392">この例では、接続文字列は、(ローカルの *.sdf*ファイルではなく) どこかのサーバーで実行されている SQL Server のインスタンス内のデータベースを指しています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="bfa57-393">`myServer` と `myDatabase`に適切な名前を置き換え、`username` および `password`に SQL Server ログイン値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfa57-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="bfa57-394">(ユーザー名とパスワードの値は、必ずしも Windows 資格情報と同じであるとは限りません。また、ホスティングプロバイダーからサーバーにログインするために指定された値と同じでもありません。</span><span class="sxs-lookup"><span data-stu-id="bfa57-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="bfa57-395">必要な値については、管理者に確認してください。)</span><span class="sxs-lookup"><span data-stu-id="bfa57-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="bfa57-396">`Database.Open` メソッドは柔軟です。これにより、データベースの *.sdf*ファイルの名前、または*web.config ファイルに*格納されている接続文字列の名前のいずれかを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="bfa57-397">次の例は、前の例で示した接続文字列を使用してデータベースに接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="bfa57-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="bfa57-398">前述のように、`Database.Open` メソッドを使用すると、データベース名または接続文字列のいずれかを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="bfa57-399">これは、web サイトをデプロイ (発行) するときに非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="bfa57-400">サイトの開発とテストを行う場合は、 *App\_Data*フォルダーにある *.sdf*ファイルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="bfa57-401">その後、サイトを実稼働サーバーに移動するときに、 *.sdf*ファイルと同じ名前を持つ*web.config ファイル内*の接続文字列を使用できますが、コードを変更しなくてもホスティングプロバイダー &#8212;のデータベースを参照します。</span><span class="sxs-lookup"><span data-stu-id="bfa57-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="bfa57-402">最後に、接続文字列を直接操作する場合は、`Database.OpenConnectionString` メソッドを呼び出し*て、web.config ファイルに*ある名前だけではなく、実際の接続文字列を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="bfa57-403">これは、ページが実行されるまで、何らかの理由で接続文字列 ( *.sdf*ファイル名などの値) にアクセスできない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="bfa57-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="bfa57-404">ただし、ほとんどのシナリオでは、この記事で説明されているように `Database.Open` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="bfa57-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfa57-405">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="bfa57-405">Additional Resources</span></span>

- [<span data-ttu-id="bfa57-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="bfa57-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="bfa57-407">WebMatrix での SQL Server または MySQL データベースへの接続</span><span class="sxs-lookup"><span data-stu-id="bfa57-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="bfa57-408">ASP.NET Web ページにおけるユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="bfa57-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
