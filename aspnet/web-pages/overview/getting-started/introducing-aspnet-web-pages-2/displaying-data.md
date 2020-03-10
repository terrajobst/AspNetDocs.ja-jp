---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: 'ASP.NET Web ページの概要: データの表示 |Microsoft Docs'
author: Rick-Anderson
description: このチュートリアルでは、WebMatrix でデータベースを作成する方法と、ASP.NET Web ページ (Razor) を使用してデータベースデータをページに表示する方法について説明します。 この例では、y...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421486"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="f5b75-104">ASP.NET Web ページの概要-データの表示</span><span class="sxs-lookup"><span data-stu-id="f5b75-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>

<span data-ttu-id="f5b75-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f5b75-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f5b75-106">このチュートリアルでは、WebMatrix でデータベースを作成する方法と、ASP.NET Web ページ (Razor) を使用してデータベースデータをページに表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="f5b75-107">この記事では、 [ASP.NET Web ページプログラミングの概要につい](../introducing-razor-syntax-c.md)て説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="f5b75-108">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f5b75-109">WebMatrix ツールを使用してデータベースとデータベーステーブルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="f5b75-110">WebMatrix ツールを使用してデータベースにデータを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="f5b75-111">ページのデータベースのデータを表示する方法。</span><span class="sxs-lookup"><span data-stu-id="f5b75-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="f5b75-112">ASP.NET Web ページで SQL コマンドを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="f5b75-113">`WebGrid` ヘルパーをカスタマイズしてデータ表示を変更し、ページングと並べ替えを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="f5b75-114">説明する機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="f5b75-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="f5b75-115">WebMatrix データベースツール。</span><span class="sxs-lookup"><span data-stu-id="f5b75-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="f5b75-116">`WebGrid` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="f5b75-116">`WebGrid` helper.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="f5b75-117">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="f5b75-117">What You'll Build</span></span>

<span data-ttu-id="f5b75-118">前のチュートリアルでは、ASP.NET Web ページ (*cshtml*ファイル) を Razor 構文の基本とヘルパーに導入しました。</span><span class="sxs-lookup"><span data-stu-id="f5b75-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="f5b75-119">このチュートリアルでは、シリーズの残りの部分で使用する実際の web アプリケーションの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="f5b75-120">アプリは、ムービーに関する情報を表示、追加、変更、および削除できる単純なムービーアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="f5b75-121">このチュートリアルを完了すると、次のようなムービーの一覧を表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![CSS クラス名に設定されたパラメーターを含む WebGrid 表示](displaying-data/_static/image1.png)

<span data-ttu-id="f5b75-123">ただし、開始するには、データベースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="f5b75-124">データベースの概要</span><span class="sxs-lookup"><span data-stu-id="f5b75-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="f5b75-125">このチュートリアルでは、データベースの briefest の概要についてのみ説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="f5b75-126">データベースの使用経験がある場合は、この短いセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="f5b75-127">データベースには、顧客、注文、および仕入先のテーブルや、学生、教師、クラス、グレードなどの情報 &mdash; を含むテーブルが1つ以上含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="f5b75-128">構造的には、データベーステーブルはスプレッドシートに似ています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="f5b75-129">一般的なアドレス帳を想像してください。</span><span class="sxs-lookup"><span data-stu-id="f5b75-129">Imagine a typical address book.</span></span> <span data-ttu-id="f5b75-130">アドレス帳の各エントリ (つまり、各ユーザーについて) には、名、姓、住所、電子メールアドレス、電話番号など、いくつかの情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![単純なグリッドとしてのサンプルデータベーステーブル](displaying-data/_static/image2.png)

<span data-ttu-id="f5b75-132">(行は*レコード*と呼ばれることもあり、列は*フィールド*と呼ばれることもあります)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="f5b75-133">ほとんどのデータベーステーブルでは、テーブルには、顧客番号や勘定科目番号などの一意の値を含む列が必要です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="f5b75-134">この値はテーブルの*主キー*と呼ばれ、テーブルの各行を識別するために使用します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="f5b75-135">この例では、ID 列は、前の例で示したアドレス帳の主キーです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="f5b75-136">Web アプリケーションで行う作業の多くは、データベースから情報を読み取り、ページに表示することで構成されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="f5b75-137">また、多くの場合、ユーザーから情報を収集してデータベースに追加するか、データベースに既に存在するレコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="f5b75-138">(このすべての操作については、このチュートリアルセットで説明します)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="f5b75-139">データベース作業は非常に複雑で、特別な知識が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="f5b75-140">ただし、このチュートリアルでは、基本的な概念について理解しておく必要があります。これについてはすべて説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="f5b75-141">データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-141">Creating a Database</span></span>

<span data-ttu-id="f5b75-142">WebMatrix には、データベースを簡単に作成したり、データベースにテーブルを作成したりするためのツールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="f5b75-143">(データベースの構造は、データベースの*スキーマ*と呼ばれます)。このチュートリアルセットでは、&mdash; 映画にテーブルが1つだけ含まれるデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="f5b75-144">WebMatrix をまだ開いていない場合は開き、前のチュートリアルで作成した Webweb ムービーサイトを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="f5b75-145">左側のウィンドウで、 **[データベース]** ワークスペースをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix データベースワークスペースタブ](displaying-data/_static/image3.png)

<span data-ttu-id="f5b75-147">リボンが変更され、データベース関連のタスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="f5b75-148">リボンの **[新しいデータベース]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-148">In the ribbon, click **New Database**.</span></span>

![WebMatrix リボンの [新しいデータベース] ボタン](displaying-data/_static/image4.png)

<span data-ttu-id="f5b75-150">WebMatrix では、&mdash; サイトと同じ名前の SQL Server の CE データベース ( *.sdf*ファイル) が*作成され*ます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="f5b75-151">(これはここでは実行しませんが、ファイル名は *.sdf*拡張子が付いている限り、好きな名前に変更できます)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="f5b75-152">テーブルの作成</span><span class="sxs-lookup"><span data-stu-id="f5b75-152">Creating a Table</span></span>

<span data-ttu-id="f5b75-153">リボンの **[新しいテーブル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="f5b75-154">WebMatrix では、テーブルデザイナーが新しいタブで開きます。 ([新しいテーブル] オプションが使用できない場合は、左側のツリービューで新しいデータベースが選択されていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

![WebMatrix リボンの [新しいテーブル] ボタン](displaying-data/_static/image5.png)

<span data-ttu-id="f5b75-156">上部のテキストボックス (ウォーターマークの [テーブル名の入力] と表示されます) で、「ムービー」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![WebMatrix データベースデザイナーでのテーブル名の入力](displaying-data/_static/image6.png)

<span data-ttu-id="f5b75-158">テーブル名の下のペインには、個々の列を定義します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="f5b75-159">このチュートリアルの*ムービー*テーブルでは、 *ID*、*タイトル*、*ジャンル*、*年*など、いくつかの列のみを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="f5b75-160">**[名前]** ボックスに「ID」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="f5b75-161">ここで値を入力すると、新しい列のすべてのコントロールがアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="f5b75-162">Tab キーを押して **[データ型]** の一覧に入力し、 **[int]** を選択します。この値は、ID 列に整数 (数値) データが含まれることを指定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="f5b75-163">ここではそれ以上のことはありませんが、標準の Windows キーボードジェスチャを使用してこのグリッド内を移動できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="f5b75-164">たとえば、フィールド間で tab キーを押すと、リスト内の項目を選択するために入力を開始できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>

<span data-ttu-id="f5b75-165">Tab キーを使用して、**既定値**ボックスの後に移動します (空白のままにします)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="f5b75-166">**[Is Primary Key]** チェックボックスをオンにして選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="f5b75-167">このオプションを使用すると、 *ID*列に個々の行を識別するデータが含まれることがデータベースに通知されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="f5b75-168">(つまり、各行の ID 列には、その行を検索するために使用できる一意の値が含まれます)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="f5b75-169">**[Id]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="f5b75-170">このオプションは、新しい行ごとに次の連続する数値を自動的に生成するようにデータベースに指示します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="f5b75-171">**[Is Identity]** オプションは、 **[主キー]** オプションも選択した場合にのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="f5b75-172">次のグリッド行をクリックするか、Tab キーを2回押して、現在の行を完成させます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="f5b75-173">どちらのジェスチャも、現在の行を保存し、次の行を開始します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="f5b75-174">**既定値**の列に  **Null**」と表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5b75-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="f5b75-175">(既定値の既定値は Null です)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="f5b75-176">新しい**ID**列の定義が完了すると、デザイナーは次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![ムービーテーブルの ID 列を定義した後の WebMatrix データベースデザイナー](displaying-data/_static/image7.png)

<span data-ttu-id="f5b75-178">次の列を作成するには、 **[名前]** 列のボックス内をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="f5b75-179">列に「Title」と入力し、 **[データ型]** の値として **[nvarchar]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="f5b75-180">**Nvarchar**の "var" 部分は、この列のデータが、レコードごとにサイズが異なる可能性がある文字列であることをデータベースに伝えます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="f5b75-181">"N" プレフィックスは "national" を表します。これは、フィールドが任意のアルファベットまたは書記体系の文字データを保持できること、つまり、フィールドが Unicode データを保持していることを示します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="f5b75-182">**[Nvarchar]** を選択すると、フィールドの最大長を入力できる別のボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="f5b75-183">このチュートリアルで使用するムービータイトルが50文字を超えないことを想定して、50を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="f5b75-184">**既定値**をスキップし、[ **null**を許容] オプションをオフにします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="f5b75-185">タイトルのないデータベースへのムービーの入力をデータベースに許可しないようにします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="f5b75-186">次の行に進むと、デザイナーは次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![ムービーテーブルのタイトル列を定義した後の WebMatrix データベースデザイナー](displaying-data/_static/image8.png)

<span data-ttu-id="f5b75-188">この手順を繰り返して、"Genre" という名前の列を作成します。長さを除き、30に設定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="f5b75-189">"Year" という名前の別の列を作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-189">Create another column named "Year."</span></span> <span data-ttu-id="f5b75-190">[データ型] で、[ **nchar** ( **nvarchar**以外)] を選択し、長さを4に設定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="f5b75-191">年については、"1995" または "2010" のような4桁の数字を使用します。そのため、可変サイズの列は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="f5b75-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="f5b75-192">完成した設計は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-192">Here's what the finished design looks like:</span></span>

![すべてのフィールドがムービーテーブルに対して定義された後の WebMatrix データベースデザイナー](displaying-data/_static/image9.png)

<span data-ttu-id="f5b75-194">Ctrl + S キーを押すか、クイックアクセスツールバーの **[保存]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="f5b75-195">タブを閉じて、データベースデザイナーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="f5b75-196">サンプルデータの追加</span><span class="sxs-lookup"><span data-stu-id="f5b75-196">Adding Some Example Data</span></span>

<span data-ttu-id="f5b75-197">このチュートリアルシリーズの後半では、フォームに新しいムービーを入力できるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="f5b75-198">ただし、ここでは、ページに表示できるデータの例をいくつか追加することができます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="f5b75-199">WebMatrix の **[データベース]** ワークスペースに、前に作成した *.sdf*ファイルを示すツリーが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="f5b75-200">新しい *.sdf*ファイルのノードを開き、 **[テーブル]** ノードを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![[ムービーに対してツリーを開く] という WebMatrix データベースワークスペース](displaying-data/_static/image10.png)

<span data-ttu-id="f5b75-202">**[ムービー]** ノードを右クリックし、 **[データ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="f5b75-203">WebMatrix では、次のようなグリッドが開き、*ムービー*テーブルのデータを入力できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix のデータベースエントリグリッド (空)](displaying-data/_static/image11.png)

<span data-ttu-id="f5b75-205">**[タイトル]** 列をクリックし、「When Harry が大いに一致した場合」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="f5b75-206">**Genre**列に移動し (Tab キーを使用できます)、「ロマンチックコメディ」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="f5b75-207">**年**の列に移動し、「1989」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-207">Move to the **Year** column and enter "1989":</span></span>

![1つのレコードを含む WebMatrix のデータベースエントリグリッド](displaying-data/_static/image12.png)

<span data-ttu-id="f5b75-209">Enter キーを押すと、WebMatrix によって新しいムービーが保存されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="f5b75-210">**ID**列が入力されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5b75-210">Notice that the **ID** column has been filled in.</span></span>

![1つのレコードと自動生成 ID を持つ WebMatrix のデータベースエントリグリッド](displaying-data/_static/image13.png)

<span data-ttu-id="f5b75-212">別のムービーを入力します (たとえば、"ドラマ"、""、"1939")。</span><span class="sxs-lookup"><span data-stu-id="f5b75-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="f5b75-213">ID 列にもう一度入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-213">The ID column is filled in again:</span></span>

![2つのレコードと自動生成された Id を持つ WebMatrix のデータベースエントリグリッド](displaying-data/_static/image14.png)

<span data-ttu-id="f5b75-215">3番目のムービー (たとえば、"Ghostbusters"、"コメディ") を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="f5b75-216">実験として、**年**の列を空白のままにして、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="f5b75-217">**[Null を許容]** オプションを選択しなかったため、データベースにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![必要な列の値が空白のままになっていると、' 無効なデータ ' エラーが表示される](displaying-data/_static/image15.png)

<span data-ttu-id="f5b75-219">**[OK]** をクリックして戻って、エントリ ("Ghostbusters" の年は 1984) を修正し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="f5b75-220">8個以上のムービーを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="f5b75-221">(8 を入力すると、後でページングを簡単に操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="f5b75-222">しかし、それが多すぎる場合は、今すぐ数だけ入力してください)。実際のデータは重要ではありません。</span><span class="sxs-lookup"><span data-stu-id="f5b75-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![いずれかのレコードを含む WebMatrix のデータベースエントリグリッド](displaying-data/_static/image16.png)

<span data-ttu-id="f5b75-224">すべてのムービーをエラーなしで入力した場合、ID 値は順次です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="f5b75-225">不完全なムービーレコードを保存しようとした場合、ID 番号が連続していない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="f5b75-226">そうすれば大丈夫です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-226">If so, that's okay.</span></span> <span data-ttu-id="f5b75-227">これらの数値には固有の意味はありません。重要なのは、これらが*ムービー*テーブル内で一意であることだけです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="f5b75-228">データベースデザイナーを含むタブを閉じます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="f5b75-229">これで、このデータを web ページに表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f5b75-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="f5b75-230">WebGrid Helper を使用してページ内のデータを表示する</span><span class="sxs-lookup"><span data-stu-id="f5b75-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="f5b75-231">ページにデータを表示するには、`WebGrid` ヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="f5b75-232">このヘルパーは、グリッドまたはテーブル (行と列) に表示を生成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="f5b75-233">ご覧のように、書式設定やその他の機能を使用してグリッドを調整できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="f5b75-234">グリッドを実行するには、数行のコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="f5b75-235">これらの数行は、このチュートリアルで実行するほとんどすべてのデータアクセスに対して、一種のパターンとして機能します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="f5b75-236">実際には、ページにデータを表示するためのオプションが多数あります。`WebGrid` ヘルパーはただ1つです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="f5b75-237">このチュートリアルでは、データを表示するための最も簡単な方法であるため、このチュートリアルではこれを選択しました。これは、柔軟性に優れているためです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="f5b75-238">次のチュートリアルセットでは、ページ内のデータを操作するための "手動" の方法を使用する方法について説明します。これにより、データの表示方法をより直接的に制御できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>

<span data-ttu-id="f5b75-239">WebMatrix の左側のウィンドウで、 **[ファイル]** ワークスペースをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="f5b75-240">作成した新しいデータベースは、 *App\_Data*フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="f5b75-241">フォルダーが既に存在していない場合は、新しいデータベース用に作成されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="f5b75-242">(以前にヘルパーをインストールした場合は、フォルダーが存在していた可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="f5b75-243">ツリービューで、web サイトのルートを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="f5b75-244">Web サイトのルートを選択する必要があります。それ以外の場合は、新しいファイルが App\_Data フォルダーに追加される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="f5b75-245">リボンで **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="f5b75-246">**[ファイルの種類の選択]** ボックスで、 **[CSHTML]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="f5b75-247">**[名前]** ボックスに、新しいページに「"ムービー. cshtml" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

![' ムービー ' ページが表示された [ファイルの種類を選択] ダイアログボックス](displaying-data/_static/image17.png)

<span data-ttu-id="f5b75-249">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-249">Click the **OK** button.</span></span> <span data-ttu-id="f5b75-250">WebMatrix は、一部のスケルトン要素を含む新しいファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="f5b75-251">まず、データベースからデータを取得するためのコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="f5b75-252">次に、ページにマークアップを追加して、実際にデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="f5b75-253">データクエリコードの記述</span><span class="sxs-lookup"><span data-stu-id="f5b75-253">Writing the Data Query Code</span></span>

<span data-ttu-id="f5b75-254">ページの上部で、`@{` と `}` の文字の間に、次のコードを入力します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="f5b75-255">(始めかっこと終わりかっこの間にこのコードを入力してください)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="f5b75-256">最初の行では、前に作成したデータベースが開きます。これは、データベースに対して何らかの処理を実行する前の最初の手順です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="f5b75-257">開くデータベースの `Database.Open` メソッド名を指定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="f5b75-258">名前には *.sdf*を含めないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5b75-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="f5b75-259">`Open` メソッドでは、 *.sdf*ファイル (つまり*web\* ) が検索され、 *.Sdf*ファイルが*App\_Data\*フォルダーにあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="f5b75-260">(前述のように、 *App\_Data*フォルダーは予約されています。このシナリオは、ASP.NET がその名前について想定している場所の1つです)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="f5b75-261">データベースを開くと、そのデータベースへの参照が `db`という名前の変数に格納されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="f5b75-262">(名前は任意です)。`db` 変数は、データベースとの対話を終了する方法です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="f5b75-263">2行目では、実際には `Query` メソッドを使用してデータベースデータをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="f5b75-264">このコードの動作に注意してください。 `db` 変数には、開いているデータベースへの参照があり、`db` 変数 (`db.Query`) を使用して `Query` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="f5b75-265">クエリ自体は SQL `Select` ステートメントです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="f5b75-266">(SQL の概要については、後述の説明を参照してください)。ステートメントでは、`Movies` は、クエリを実行するテーブルを識別します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="f5b75-267">`*` 文字は、クエリがテーブルからすべての列を返す必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="f5b75-268">(列をコンマで区切って個別に一覧表示することもできます)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="f5b75-269">クエリの結果 (存在する場合) が返され、`selectedData` 変数で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="f5b75-270">ここでも、変数には任意の名前を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="f5b75-271">最後に、3行目では、`WebGrid` ヘルパーのインスタンスを使用することを ASP.NET に指示します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="f5b75-272">`new` キーワードを使用してヘルパーオブジェクトを作成 (*インスタンス化*) し、`selectedData` 変数を使用してクエリ結果を渡します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="f5b75-273">新しい `WebGrid` オブジェクトは、データベースクエリの結果と共に、`grid` 変数で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="f5b75-274">実際にページのデータを表示するには、結果が必要になります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="f5b75-275">この段階で、データベースが開かれ、必要なデータが得られました。また、そのデータを使用して `WebGrid` ヘルパーを準備しました。</span><span class="sxs-lookup"><span data-stu-id="f5b75-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="f5b75-276">次に、ページにマークアップを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="f5b75-277">**構造化照会言語 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="f5b75-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="f5b75-278">SQL は、データベース内のデータを管理するためにほとんどのリレーショナルデータベースで使用される言語です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="f5b75-279">これには、データを取得して更新するためのコマンドが含まれています。このコマンドを使用すると、データベーステーブルのデータを作成、変更、および管理できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="f5b75-280">SQL は、プログラミング言語 (C#) のように異なります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="f5b75-281">SQL を使用すると、データベースに必要なものが通知され、データベースのジョブによってデータを取得したりタスクを実行したりする方法がわかります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="f5b75-282">いくつかの SQL コマンドとその実行内容の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="f5b75-283">最初の `Select` ステートメントは、`*`によって指定されたすべての列を、*ムービー*テーブルから取得します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="f5b75-284">2番目の `Select` ステートメントは、Price 列の値が10を超える*Product*テーブルのレコードから、ID、Name、および price 列をフェッチします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="f5b75-285">このコマンドは、Name 列の値に基づいて、結果をアルファベット順に返します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="f5b75-286">価格条件に一致するレコードがない場合、コマンドは空のセットを返します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="f5b75-287">このコマンドは、 *Product*テーブルに新しいレコードを挿入し、Name 列を "クロワッサン" に、Description 列を "a 不安定な満足させる" に、price を1.99 に設定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="f5b75-288">数値以外の値を指定する場合に、値を単一引用符 (いない二重引用符、C# と同様) で囲むことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5b75-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="f5b75-289">これらの引用符は、テキストまたは日付の値を囲むのではなく、数字の周りに使用します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="f5b75-290">このコマンドは、有効期限の日付列が2008年1月1日より前の*製品*テーブル内のレコードを削除します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="f5b75-291">(もちろん、このコマンドでは、 *Product*テーブルにこのような列があることを前提としています)。日付は MM/DD/YYYY 形式で入力しますが、ロケールに使用する形式で入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="f5b75-292">`Insert` と `Delete` のコマンドでは、結果セットは返されません。</span><span class="sxs-lookup"><span data-stu-id="f5b75-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="f5b75-293">代わりに、コマンドによって影響を受けたレコードの数を示す数値が返されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="f5b75-294">これらの操作 (レコードの挿入や削除など) の一部では、操作を要求しているプロセスがデータベース内で適切な権限を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="f5b75-295">そのため、データベースに接続するときに、多くの場合、運用データベースではユーザー名とパスワードを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="f5b75-296">SQL コマンドは多数ありますが、これらはすべて、ここに表示されるコマンドのようなパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="f5b75-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="f5b75-297">SQL コマンドを使用して、データベーステーブルを作成したり、テーブル内のレコード数をカウントしたり、価格を計算したり、多くの操作を実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="f5b75-298">データを表示するためのマークアップの追加</span><span class="sxs-lookup"><span data-stu-id="f5b75-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="f5b75-299">`<head>` 要素内で、`<title>` 要素の内容を "映画" に設定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="f5b75-300">ページの `<body>` 要素内に、次の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="f5b75-301">これで終了です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-301">That's it.</span></span> <span data-ttu-id="f5b75-302">`grid` 変数は、前のコードで `WebGrid` オブジェクトを作成したときに作成した値です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="f5b75-303">WebMatrix ツリービューで、ページを右クリックし、 **[ブラウザーで起動]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="f5b75-304">次のようなページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-304">You'll see something like this page:</span></span>

![ムービーテーブルからの既定の WebGrid helper の出力](displaying-data/_static/image18.png)

<span data-ttu-id="f5b75-306">列見出しのリンクをクリックすると、その列で並べ替えることができます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="f5b75-307">見出しをクリックして並べ替えることができるのは、 **WebGrid**ヘルパーに組み込まれている機能です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="f5b75-308">`GetHtml` メソッドは、名前のように、データを表示するマークアップを生成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="f5b75-309">既定では、`GetHtml` メソッドは HTML `<table>` 要素を生成します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="f5b75-310">(必要に応じて、ブラウザーのページのソースを見て、表示を確認できます)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="f5b75-311">グリッドの外観の変更</span><span class="sxs-lookup"><span data-stu-id="f5b75-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="f5b75-312">`WebGrid` ヘルパーを使用するのは簡単ですが、結果として表示される表示は単純です。</span><span class="sxs-lookup"><span data-stu-id="f5b75-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="f5b75-313">`WebGrid` ヘルパーには、データの表示方法を制御できるあらゆる種類のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="f5b75-314">このチュートリアルでは、このチュートリアルでは詳しく説明しませんが、このセクションではこれらのオプションのいくつかについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="f5b75-315">このシリーズの後のチュートリアルでは、いくつかの追加オプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="f5b75-316">表示する個々の列の指定</span><span class="sxs-lookup"><span data-stu-id="f5b75-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="f5b75-317">まず、特定の列のみを表示するように指定できます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="f5b75-318">既定では、このグリッドには、*ムービー*テーブルの4つの列がすべて表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="f5b75-319">次のように、*ムービーの cshtml*ファイルで、追加した `@grid.GetHtml()` マークアップを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="f5b75-320">表示する列をヘルパーに伝えるには、`GetHtml` メソッドに `columns` パラメーターを含め、列のコレクションを渡します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="f5b75-321">コレクションでは、含める各列を指定します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="f5b75-322">`grid.Column` オブジェクトを含めることによって、表示する個々の列を指定し、必要なデータ列の名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="f5b75-323">(これらの列は SQL クエリの結果に含まれる必要があります。 `WebGrid` ヘルパーは、クエリによって返されなかった列を表示することはできません)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="f5b75-324">ブラウザーでもう一度 [*ムービー* ] ページを開きます。今度は、次のような画面が表示されます (ID 列が表示されていないことに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="f5b75-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![選択された列のみを表示する WebGrid](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="f5b75-326">グリッドの外観の変更</span><span class="sxs-lookup"><span data-stu-id="f5b75-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="f5b75-327">列を表示するためのオプションは他にもいくつかあります。その一部については、このセットの以降のチュートリアルで説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="f5b75-328">ここでは、グリッド全体をスタイル指定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="f5b75-329">ページの `<head>` セクション内で、終了 `</head>` タグの直前に、次の `<style>` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="f5b75-330">この CSS マークアップは、`grid`、`head`などという名前のクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="f5b75-331">これらのスタイル定義を別の *.css*ファイルに配置して、ページにリンクすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="f5b75-332">(実際には、このチュートリアルで後ほど説明します)。しかし、このチュートリアルを簡単にするために、データが表示されるのと同じページ内に配置されています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="f5b75-333">これで、これらのスタイルクラスを使用するための `WebGrid` ヘルパーを取得できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f5b75-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="f5b75-334">ヘルパーには、この目的でいくつかのプロパティ (`tableStyle`など) があります。このクラスに CSS スタイルクラス名を割り当てます。そのクラス名は、ヘルパーによってレンダリングされるマークアップの一部としてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="f5b75-335">`grid.GetHtml` マークアップを次のコードのように変更します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="f5b75-336">ここでの新機能として、`tableStyle`、`headerStyle`、`alternatingRowStyle` のパラメーターを `GetHtml` メソッドに追加しました。</span><span class="sxs-lookup"><span data-stu-id="f5b75-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="f5b75-337">これらのパラメーターは、少し前に追加した CSS スタイルの名前に設定されています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="f5b75-338">ページを実行します。今度は、次のような形式のグリッドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![CSS クラス名に設定されたパラメーターを含む WebGrid 表示](displaying-data/_static/image20.png)

<span data-ttu-id="f5b75-340">`GetHtml` メソッドが生成された内容を確認するには、ブラウザーでページのソースを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="f5b75-341">ここでは詳しく説明しませんが、重要な点は、`tableStyle`のようなパラメーターを指定することで、グリッドが次のような HTML タグを生成することです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="f5b75-342">`<table>` タグには、前に追加した CSS ルールの1つを参照する `class` 属性が追加されています。</span><span class="sxs-lookup"><span data-stu-id="f5b75-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="f5b75-343">このコードは、`GetHtml` メソッドのさまざまなパラメーター &mdash; 基本パターンを示しています。これにより、メソッドがマークアップと共に生成する CSS クラスを参照できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="f5b75-344">CSS クラスを使用して何を行うかは、ユーザーによって決まります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="f5b75-345">ページングの追加</span><span class="sxs-lookup"><span data-stu-id="f5b75-345">Adding Paging</span></span>

<span data-ttu-id="f5b75-346">このチュートリアルの最後のタスクとして、グリッドにページングを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="f5b75-347">現時点では、すべてのムービーを一度に表示するのは問題ではありません。</span><span class="sxs-lookup"><span data-stu-id="f5b75-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="f5b75-348">しかし、何百ものムービーを追加した場合は、ページの表示が長くなります。</span><span class="sxs-lookup"><span data-stu-id="f5b75-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="f5b75-349">ページコードで、`WebGrid` オブジェクトを作成する行を次のコードに変更します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="f5b75-350">以前の唯一の違いは、3に設定された `rowsPerPage` パラメーターを追加したことです。</span><span class="sxs-lookup"><span data-stu-id="f5b75-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="f5b75-351">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-351">Run the page.</span></span> <span data-ttu-id="f5b75-352">グリッドには、一度に3つの行が表示されます。また、データベース内のムービーのページを表示するためのナビゲーションリンクも表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5b75-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![ページングによる WebGrid の表示](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="f5b75-354">次へ</span><span class="sxs-lookup"><span data-stu-id="f5b75-354">Coming Up Next</span></span>

<span data-ttu-id="f5b75-355">次のチュートリアルでは、Razor および C# のコードを使用して、フォーム内のユーザー入力を取得する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f5b75-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="f5b75-356">[ムービー] ページに検索ボックスを追加して、タイトルまたはジャンルで映画を検索できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f5b75-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="f5b75-357">[ムービーの完全な一覧表示] ページ</span><span class="sxs-lookup"><span data-stu-id="f5b75-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="f5b75-358">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="f5b75-358">Additional Resources</span></span>

- [<span data-ttu-id="f5b75-359">Razor 構文を使用した ASP.NET Web プログラミングの概要</span><span class="sxs-lookup"><span data-stu-id="f5b75-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="f5b75-360">[前へ](intro-to-web-pages-programming.md)
> [次へ](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="f5b75-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
