---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First Migrations を使用してデータベースをシードする |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449116"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="53782-102">Code First Migrations を使用してデータベースをシード処理する</span><span class="sxs-lookup"><span data-stu-id="53782-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="53782-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="53782-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="53782-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="53782-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="53782-105">このセクションでは、EF の[Code First Migrations](https://msdn.microsoft.com/data/jj591621)を使用して、データベースにテストデータをシードします。</span><span class="sxs-lookup"><span data-stu-id="53782-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="53782-106">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="53782-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="53782-107">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="53782-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="53782-108">このコマンドは、移行という名前のフォルダーをプロジェクトに追加し、Configuration.cs という名前のコードファイルを [移行] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="53782-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="53782-109">Configuration.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="53782-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="53782-110">次の**using ステートメントを**追加します。</span><span class="sxs-lookup"><span data-stu-id="53782-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="53782-111">次に、次のコードを**構成の Seed**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="53782-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="53782-112">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="53782-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="53782-113">最初のコマンドは、データベースを作成するコードを生成し、2番目のコマンドはそのコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="53782-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="53782-114">データベースは、 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)を使用してローカルに作成されます。</span><span class="sxs-lookup"><span data-stu-id="53782-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="53782-115">API を探索する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="53782-115">Explore the API (Optional)</span></span>

<span data-ttu-id="53782-116">F5 キーを押してデバッグ モードでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="53782-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="53782-117">Visual Studio が起動し IIS Express、web アプリが実行されます。</span><span class="sxs-lookup"><span data-stu-id="53782-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="53782-118">その後、Visual Studio によってブラウザーが起動され、アプリのホームページが開きます。</span><span class="sxs-lookup"><span data-stu-id="53782-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="53782-119">Visual Studio で web プロジェクトを実行すると、ポート番号が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="53782-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="53782-120">次の図では、ポート番号は50524です。</span><span class="sxs-lookup"><span data-stu-id="53782-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="53782-121">アプリケーションを実行すると、別のポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="53782-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="53782-122">ホームページは、ASP.NET MVC を使用して実装されます。</span><span class="sxs-lookup"><span data-stu-id="53782-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="53782-123">ページの上部には、"API" というリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="53782-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="53782-124">このリンクを使用すると、web API の自動生成されたヘルプページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="53782-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="53782-125">(このヘルプページの生成方法と、独自のドキュメントをページに追加する方法については、「 [ASP.NET Web API のヘルプページの作成](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)」を参照してください)。[ヘルプ] ページのリンクをクリックすると、要求と応答の形式など、API の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="53782-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="53782-126">この API により、データベースに対する CRUD 操作が有効になります。</span><span class="sxs-lookup"><span data-stu-id="53782-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="53782-127">API の概要を次に示します。</span><span class="sxs-lookup"><span data-stu-id="53782-127">The following summarizes the API.</span></span>

| <span data-ttu-id="53782-128">Authors</span><span class="sxs-lookup"><span data-stu-id="53782-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="53782-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="53782-129">GET api/authors</span></span> | <span data-ttu-id="53782-130">すべての作成者を取得します。</span><span class="sxs-lookup"><span data-stu-id="53782-130">Get all authors.</span></span> |
| <span data-ttu-id="53782-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-131">GET api/authors/{id}</span></span> | <span data-ttu-id="53782-132">ID で作成者を取得します。</span><span class="sxs-lookup"><span data-stu-id="53782-132">Get an author by ID.</span></span> |
| <span data-ttu-id="53782-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="53782-133">POST /api/authors</span></span> | <span data-ttu-id="53782-134">新しい作成者を作成します。</span><span class="sxs-lookup"><span data-stu-id="53782-134">Create a new author.</span></span> |
| <span data-ttu-id="53782-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="53782-136">既存の作成者を更新します。</span><span class="sxs-lookup"><span data-stu-id="53782-136">Update an existing author.</span></span> |
| <span data-ttu-id="53782-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="53782-138">作成者を削除します。</span><span class="sxs-lookup"><span data-stu-id="53782-138">Delete an author.</span></span> |

| <span data-ttu-id="53782-139">書籍</span><span class="sxs-lookup"><span data-stu-id="53782-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="53782-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="53782-140">GET /api/books</span></span> | <span data-ttu-id="53782-141">すべてのブックを取得します。</span><span class="sxs-lookup"><span data-stu-id="53782-141">Get all books.</span></span> |
| <span data-ttu-id="53782-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-142">GET /api/books/{id}</span></span> | <span data-ttu-id="53782-143">ID でブックを取得します。</span><span class="sxs-lookup"><span data-stu-id="53782-143">Get a book by ID.</span></span> |
| <span data-ttu-id="53782-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="53782-144">POST /api/books</span></span> | <span data-ttu-id="53782-145">新しい本を作成します。</span><span class="sxs-lookup"><span data-stu-id="53782-145">Create a new book.</span></span> |
| <span data-ttu-id="53782-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="53782-147">既存のブックを更新します。</span><span class="sxs-lookup"><span data-stu-id="53782-147">Update an existing book.</span></span> |
| <span data-ttu-id="53782-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="53782-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="53782-149">ブックを削除します。</span><span class="sxs-lookup"><span data-stu-id="53782-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="53782-150">データベースを表示する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="53782-150">View the Database (Optional)</span></span>

<span data-ttu-id="53782-151">データベースの更新コマンドを実行すると、EF によってデータベースが作成され、`Seed` メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="53782-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="53782-152">アプリケーションをローカルで実行すると、EF によって[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="53782-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="53782-153">データベースは Visual Studio で表示できます。</span><span class="sxs-lookup"><span data-stu-id="53782-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="53782-154">**[表示]** メニューの **[SQL Server オブジェクト エクスプローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="53782-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="53782-155">**[サーバーへの接続]** ダイアログの **[サーバー名]** ボックスに「(localdb) \ v11.0」と入力します。</span><span class="sxs-lookup"><span data-stu-id="53782-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="53782-156">**認証** オプションは Windows 認証 のままにします。</span><span class="sxs-lookup"><span data-stu-id="53782-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="53782-157">**[接続]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="53782-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="53782-158">Visual Studio は LocalDB に接続し、[SQL Server オブジェクトエクスプローラー] ウィンドウに既存のデータベースを表示します。</span><span class="sxs-lookup"><span data-stu-id="53782-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="53782-159">ノードを展開して、EF によって作成されたテーブルを表示できます。</span><span class="sxs-lookup"><span data-stu-id="53782-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="53782-160">データを表示するには、テーブルを右クリックし、 **[データの表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="53782-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="53782-161">次のスクリーンショットは、Books テーブルの結果を示しています。</span><span class="sxs-lookup"><span data-stu-id="53782-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="53782-162">EF によってシードデータがデータベースに設定され、テーブルに Authors テーブルへの外部キーが格納されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="53782-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="53782-163">[前へ](part-2.md)
> [次へ](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="53782-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
