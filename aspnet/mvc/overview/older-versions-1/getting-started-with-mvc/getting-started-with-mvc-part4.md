---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: データベースを作成する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469672"
---
# <a name="creating-a-database"></a><span data-ttu-id="7040d-104">データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="7040d-104">Creating a Database</span></span>

<span data-ttu-id="7040d-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="7040d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="7040d-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="7040d-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="7040d-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="7040d-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="7040d-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7040d-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="7040d-109">このセクションでは、ムービーデータを格納および取得するために使用する新しい SQL Express データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="7040d-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="7040d-110">Visual Web Developer IDE 内から、[表示] を選択します。サーバー エクスプローラー。</span><span class="sxs-lookup"><span data-stu-id="7040d-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="7040d-111">[データ接続] を右クリックし、[接続の追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7040d-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="7040d-113">データソースの選択 ダイアログで、Microsoft SQL Server を選択し、続行 を選択します。</span><span class="sxs-lookup"><span data-stu-id="7040d-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="7040d-114">[接続の追加] ダイアログボックスで、サーバー名として「.\SQLEXPRESS」と入力し、新しいデータベースの名前として「ムービー」と入力します。</span><span class="sxs-lookup"><span data-stu-id="7040d-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="7040d-115">[[接続の追加] ダイアログ ![](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="7040d-116">[OK] をクリックすると、そのデータベースを作成するかどうかを確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7040d-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="7040d-117">[はい] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7040d-117">Select yes.</span></span>

<span data-ttu-id="7040d-118">[ムービーを作成 ![には](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="7040d-119">サーバーエクスプローラーに空のデータベースが作成されました。</span><span class="sxs-lookup"><span data-stu-id="7040d-119">Now you've got an empty database in Server Explorer.</span></span>

![新しいテーブルの追加](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="7040d-121">テーブルを右クリックし、[テーブルの追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7040d-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="7040d-122">テーブルデザイナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7040d-122">The Table Designer will appear.</span></span> <span data-ttu-id="7040d-123">Id、タイトル、ReleaseDate、Genre、および Price の列を追加します。</span><span class="sxs-lookup"><span data-stu-id="7040d-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="7040d-124">[ID] 列を右クリックし、[主キーの設定] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7040d-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="7040d-125">デザイン領域は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7040d-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="7040d-126">[![データベーステーブルエディター](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="7040d-127">また、[Id] 列を選択し、[列のプロパティ] の下にある [Identity Specification] を [Yes] に変更します。</span><span class="sxs-lookup"><span data-stu-id="7040d-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="7040d-128">[![IsIdentity のプロパティ](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="7040d-129">完了したら、ツールバーの [保存] アイコンをクリックするか、[ファイル] を選択します。メニューから [保存] を指定し、テーブルに "**Movie**" という名前を付けます (単数形)。</span><span class="sxs-lookup"><span data-stu-id="7040d-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="7040d-130">データベースとテーブルがあります。</span><span class="sxs-lookup"><span data-stu-id="7040d-130">We've got a database and a table!</span></span>

<span data-ttu-id="7040d-131">[![名の選択](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="7040d-132">サーバーエクスプローラーに戻り、Movie テーブルを右クリックして、[テーブルデータの表示] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7040d-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="7040d-133">いくつかのムービーを入力すると、データベースにいくつかのデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7040d-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="7040d-134">[![データベーステーブルの編集](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="7040d-135">モデルの作成</span><span class="sxs-lookup"><span data-stu-id="7040d-135">Creating a Model</span></span>

<span data-ttu-id="7040d-136">次に、IDE の右側にあるソリューションエクスプローラーに戻り、[モデル] フォルダーを右クリックして [追加] を選択します。新しい項目。</span><span class="sxs-lookup"><span data-stu-id="7040d-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="7040d-137">[addnewmodelitem の ![](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="7040d-138">ここでは、新しいデータベースからエンティティモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7040d-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="7040d-139">これにより、一連のクラスがプロジェクトに追加され、データベース内のデータを簡単に照会して操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7040d-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="7040d-140">ダイアログの左側にある [データ] ノードを選択し、ADO.NET Entity Data Model 項目テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="7040d-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="7040d-141">「ムービー .edmx」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="7040d-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="7040d-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="7040d-143">[追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7040d-143">Click the "Add" button.</span></span> <span data-ttu-id="7040d-144">これにより、"Entity Data Model ウィザード" が起動します。</span><span class="sxs-lookup"><span data-stu-id="7040d-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="7040d-145">ポップアップ表示された新しいダイアログボックスで、[データベースから生成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7040d-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="7040d-146">データベースを作成したばかりなので、新しいデータベースとそのテーブルに関する Entity Framework についてのみ説明します。</span><span class="sxs-lookup"><span data-stu-id="7040d-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="7040d-147">[次へ] をクリックして、web アプリケーションの構成にデータベース接続を保存します。</span><span class="sxs-lookup"><span data-stu-id="7040d-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="7040d-148">次に、[テーブルとムービー] チェックボックスをオンにして、[完了] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7040d-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="7040d-149">[![Entity Data Model ウィザード](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="7040d-150">これで、Entity Framework Designer に新しいムービーテーブルが表示され、コードからアクセスできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="7040d-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="7040d-151">[![映画-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="7040d-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="7040d-152">デザイン画面には、"Movie" クラスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7040d-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="7040d-153">このクラスは、データベースの "Movie" テーブルにマップされ、その中の各プロパティはテーブルを含む列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="7040d-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="7040d-154">"Movie" クラスの各インスタンスは、"Movie" テーブル内の行に対応します。</span><span class="sxs-lookup"><span data-stu-id="7040d-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="7040d-155">Entity Framework によって使用される既定の名前付け規則とマッピング規則が気に入らない場合は、Entity Framework デザイナーを使用して変更またはカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="7040d-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="7040d-156">このアプリケーションでは、既定値を使用し、ファイルをそのまま保存します。</span><span class="sxs-lookup"><span data-stu-id="7040d-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="7040d-157">では、実際のデータを使用してみましょう。</span><span class="sxs-lookup"><span data-stu-id="7040d-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7040d-158">[前へ](getting-started-with-mvc-part3.md)
> [次へ](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="7040d-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
