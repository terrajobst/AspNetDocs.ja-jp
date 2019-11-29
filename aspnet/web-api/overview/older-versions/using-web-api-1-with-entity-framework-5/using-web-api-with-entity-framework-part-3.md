---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'パート 3: 管理コントローラーの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600041"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="91f16-102">パート 3: 管理コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="91f16-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="91f16-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="91f16-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="91f16-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="91f16-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="91f16-105">管理コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="91f16-105">Add an Admin Controller</span></span>

<span data-ttu-id="91f16-106">このセクションでは、CRUD (作成、読み取り、更新、および削除) 操作をサポートする Web API コントローラーを製品に追加します。</span><span class="sxs-lookup"><span data-stu-id="91f16-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="91f16-107">コントローラーは Entity Framework を使用してデータベース層と通信します。</span><span class="sxs-lookup"><span data-stu-id="91f16-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="91f16-108">このコントローラーを使用できるのは管理者のみです。</span><span class="sxs-lookup"><span data-stu-id="91f16-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="91f16-109">お客様は、別のコントローラーを通じて製品にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="91f16-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="91f16-110">ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="91f16-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="91f16-111">**[追加]** 、 **[コントローラー]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="91f16-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="91f16-112">**[コントローラーの追加]** ダイアログで、コントローラーに `AdminController`という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="91f16-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="91f16-113">**[テンプレート]** で、Entity Framework&quot;を使用して、読み取り/書き込みアクションを含む &quot;API コントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="91f16-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="91f16-114">**モデルクラス** で、Product (productstore) を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f16-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="91f16-115">**[データコンテキスト]** で、[新しいデータコンテキスト&gt;の&lt;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f16-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="91f16-116">モデル**クラス**のドロップダウンにモデルクラスが表示されない場合は、プロジェクトをコンパイルしたことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="91f16-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="91f16-117">Entity Framework はリフレクションを使用するため、コンパイルされたアセンブリが必要です。</span><span class="sxs-lookup"><span data-stu-id="91f16-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="91f16-118">[新しいデータコンテキスト&gt;を&lt;] を選択すると、 **[新しいデータコンテキスト]** ダイアログボックスが開きます。</span><span class="sxs-lookup"><span data-stu-id="91f16-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="91f16-119">データコンテキストに `ProductStore.Models.OrdersContext`名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="91f16-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="91f16-120">**[OK]** をクリックして、 **[新しいデータコンテキスト]** ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="91f16-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="91f16-121">**[コントローラーの追加]** ダイアログで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="91f16-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="91f16-122">プロジェクトに追加された内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="91f16-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="91f16-123">**Dbcontext**から派生する `OrdersContext` という名前のクラス。</span><span class="sxs-lookup"><span data-stu-id="91f16-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="91f16-124">このクラスは、POCO モデルとデータベース間の接着を提供します。</span><span class="sxs-lookup"><span data-stu-id="91f16-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="91f16-125">`AdminController`という名前の Web API コントローラー。</span><span class="sxs-lookup"><span data-stu-id="91f16-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="91f16-126">このコントローラーは `Product` インスタンスに対する CRUD 操作をサポートします。</span><span class="sxs-lookup"><span data-stu-id="91f16-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="91f16-127">`OrdersContext` クラスを使用して Entity Framework と通信します。</span><span class="sxs-lookup"><span data-stu-id="91f16-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="91f16-128">Web.config ファイル内の新しいデータベース接続文字列。</span><span class="sxs-lookup"><span data-stu-id="91f16-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="91f16-129">OrdersContext.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="91f16-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="91f16-130">コンストラクターはデータベース接続文字列の名前を指定することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="91f16-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="91f16-131">この名前は、web.config に追加された接続文字列を示します。</span><span class="sxs-lookup"><span data-stu-id="91f16-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="91f16-132">`OrdersContext` クラスに次のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="91f16-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="91f16-133">**Dbset**は、クエリ可能なエンティティのセットを表します。</span><span class="sxs-lookup"><span data-stu-id="91f16-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="91f16-134">`OrdersContext` クラスの完全な一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="91f16-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="91f16-135">`AdminController` クラスは、基本的な CRUD 機能を実装する5つのメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="91f16-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="91f16-136">各メソッドは、クライアントが呼び出すことができる URI に対応します。</span><span class="sxs-lookup"><span data-stu-id="91f16-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="91f16-137">コントローラーメソッド</span><span class="sxs-lookup"><span data-stu-id="91f16-137">Controller Method</span></span> | <span data-ttu-id="91f16-138">説明</span><span class="sxs-lookup"><span data-stu-id="91f16-138">Description</span></span> | <span data-ttu-id="91f16-139">URI</span><span class="sxs-lookup"><span data-stu-id="91f16-139">URI</span></span> | <span data-ttu-id="91f16-140">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="91f16-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="91f16-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="91f16-141">GetProducts</span></span> | <span data-ttu-id="91f16-142">すべての製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="91f16-142">Gets all products.</span></span> | <span data-ttu-id="91f16-143">api/製品</span><span class="sxs-lookup"><span data-stu-id="91f16-143">api/products</span></span> | <span data-ttu-id="91f16-144">GET</span><span class="sxs-lookup"><span data-stu-id="91f16-144">GET</span></span> |
| <span data-ttu-id="91f16-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="91f16-145">GetProduct</span></span> | <span data-ttu-id="91f16-146">ID で製品を検索します。</span><span class="sxs-lookup"><span data-stu-id="91f16-146">Finds a product by ID.</span></span> | <span data-ttu-id="91f16-147">api/製品/*id*</span><span class="sxs-lookup"><span data-stu-id="91f16-147">api/products/*id*</span></span> | <span data-ttu-id="91f16-148">GET</span><span class="sxs-lookup"><span data-stu-id="91f16-148">GET</span></span> |
| <span data-ttu-id="91f16-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="91f16-149">PutProduct</span></span> | <span data-ttu-id="91f16-150">製品を更新します。</span><span class="sxs-lookup"><span data-stu-id="91f16-150">Updates a product.</span></span> | <span data-ttu-id="91f16-151">api/製品/*id*</span><span class="sxs-lookup"><span data-stu-id="91f16-151">api/products/*id*</span></span> | <span data-ttu-id="91f16-152">PUT</span><span class="sxs-lookup"><span data-stu-id="91f16-152">PUT</span></span> |
| <span data-ttu-id="91f16-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="91f16-153">PostProduct</span></span> | <span data-ttu-id="91f16-154">新しい製品を作成します。</span><span class="sxs-lookup"><span data-stu-id="91f16-154">Creates a new product.</span></span> | <span data-ttu-id="91f16-155">api/製品</span><span class="sxs-lookup"><span data-stu-id="91f16-155">api/products</span></span> | <span data-ttu-id="91f16-156">投稿</span><span class="sxs-lookup"><span data-stu-id="91f16-156">POST</span></span> |
| <span data-ttu-id="91f16-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="91f16-157">DeleteProduct</span></span> | <span data-ttu-id="91f16-158">製品を削除します。</span><span class="sxs-lookup"><span data-stu-id="91f16-158">Deletes a product.</span></span> | <span data-ttu-id="91f16-159">api/製品/*id*</span><span class="sxs-lookup"><span data-stu-id="91f16-159">api/products/*id*</span></span> | <span data-ttu-id="91f16-160">Del</span><span class="sxs-lookup"><span data-stu-id="91f16-160">DELETE</span></span> |

<span data-ttu-id="91f16-161">各メソッドは、`OrdersContext` を呼び出してデータベースにクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="91f16-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="91f16-162">コレクション (PUT、POST、および DELETE) を変更するメソッドは、データベースへの変更を保持するために `db.SaveChanges` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="91f16-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="91f16-163">コントローラーは HTTP 要求ごとに作成され、破棄されます。そのため、メソッドが返される前に変更を保持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91f16-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="91f16-164">データベース初期化子の追加</span><span class="sxs-lookup"><span data-stu-id="91f16-164">Add a Database Initializer</span></span>

<span data-ttu-id="91f16-165">Entity Framework には、起動時にデータベースを設定したり、モデルが変更されるたびに自動的にデータベースを再作成したりできる便利な機能があります。</span><span class="sxs-lookup"><span data-stu-id="91f16-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="91f16-166">この機能は、モデルを変更した場合でも、常にテストデータがあるため、開発時に便利です。</span><span class="sxs-lookup"><span data-stu-id="91f16-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="91f16-167">ソリューションエクスプローラーで、[モデル] フォルダーを右クリックし、`OrdersContextInitializer`という名前の新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="91f16-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="91f16-168">次の実装を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="91f16-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="91f16-169">**Dropcreatedatabaseifmodelchanges**クラスから継承することにより、モデルクラスを変更するたびにデータベースを削除するように Entity Framework に指示します。</span><span class="sxs-lookup"><span data-stu-id="91f16-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="91f16-170">Entity Framework によってデータベースが作成 (または再作成) されるときに、 **Seed**メソッドを呼び出してテーブルを設定します。</span><span class="sxs-lookup"><span data-stu-id="91f16-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="91f16-171">**Seed**メソッドを使用して、いくつかのサンプル製品と注文例を追加します。</span><span class="sxs-lookup"><span data-stu-id="91f16-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="91f16-172">この機能はテストに適していますが、実稼働環境では**Dropcreatedatabaseifmodelchanges**クラスを使用しないでください。これは、他のユーザーがモデルクラスを変更した場合にデータが失われる可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="91f16-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="91f16-173">次に、global.asax を開き、次のコードを**Application\_Start**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="91f16-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="91f16-174">コントローラーに要求を送信する</span><span class="sxs-lookup"><span data-stu-id="91f16-174">Send a Request to the Controller</span></span>

<span data-ttu-id="91f16-175">この時点では、クライアントコードは作成されていませんが、web ブラウザーまたは[Fiddler](http://www.fiddler2.com/fiddler2/)などの HTTP デバッグツールを使用して web API を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="91f16-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="91f16-176">Visual Studio で、F5 キーを押してデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="91f16-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="91f16-177">Web ブラウザーで `http://localhost:*portnum*/`が開きます。ここで、 *portnum*はいくつかのポート番号です。</span><span class="sxs-lookup"><span data-stu-id="91f16-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="91f16-178">HTTP 要求を "`http://localhost:*portnum*/api/admin`に送信します。</span><span class="sxs-lookup"><span data-stu-id="91f16-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="91f16-179">最初の要求が完了するまでに時間がかかることがあります。これは Entity Framework がデータベースの作成とシードを行う必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="91f16-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="91f16-180">応答は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="91f16-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="91f16-181">[前へ](using-web-api-with-entity-framework-part-2.md)
> [次へ](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="91f16-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
