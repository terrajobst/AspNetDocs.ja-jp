---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF を使用して非同期およびストアドプロシージャを使用する'
description: このチュートリアルでは、非同期プログラミングモデルを実装する方法と、ストアドプロシージャの使用方法について説明します。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471388"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="bb61e-103">チュートリアル: ASP.NET MVC アプリで EF を使用して非同期およびストアドプロシージャを使用する</span><span class="sxs-lookup"><span data-stu-id="bb61e-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="bb61e-104">前のチュートリアルでは、同期プログラミングモデルを使用してデータの読み取りと更新を行う方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="bb61e-105">このチュートリアルでは、非同期プログラミングモデルを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="bb61e-106">非同期コードを使用すると、アプリケーションのパフォーマンスを向上させることができます。これは、サーバーリソースをより効果的に使用するためです。</span><span class="sxs-lookup"><span data-stu-id="bb61e-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="bb61e-107">このチュートリアルでは、エンティティに対する挿入、更新、および削除の各操作にストアドプロシージャを使用する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="bb61e-108">最後に、アプリケーションを初めてデプロイした後に実装したすべてのデータベースの変更と共に、Azure に再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="bb61e-109">以下の図は、使用するページの一部を示しています。</span><span class="sxs-lookup"><span data-stu-id="bb61e-109">The following illustrations show some of the pages that you'll work with.</span></span>

![[部門] ページ](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![部署の作成](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="bb61e-112">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb61e-113">非同期コードの詳細</span><span class="sxs-lookup"><span data-stu-id="bb61e-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="bb61e-114">Department コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="bb61e-114">Create a Department controller</span></span>
> * <span data-ttu-id="bb61e-115">ストアドプロシージャを使用する</span><span class="sxs-lookup"><span data-stu-id="bb61e-115">Use stored procedures</span></span>
> * <span data-ttu-id="bb61e-116">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="bb61e-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb61e-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="bb61e-117">Prerequisites</span></span>

* [<span data-ttu-id="bb61e-118">関連データの更新</span><span class="sxs-lookup"><span data-stu-id="bb61e-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="bb61e-119">非同期コードを使用する理由</span><span class="sxs-lookup"><span data-stu-id="bb61e-119">Why use asynchronous code</span></span>

<span data-ttu-id="bb61e-120">Web サーバーでは、利用できるスレッド数に限りがあります。負荷が高い状況では、利用できるスレッドが全部使われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="bb61e-121">その場合、スレッドが解放されるまでサーバーは新しい要求を処理できません。</span><span class="sxs-lookup"><span data-stu-id="bb61e-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="bb61e-122">同期コードの場合、たくさんのスレッドが関連付けられていても、I/O の完了を待っているため、実際には何の作業も行っていないということがあります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="bb61e-123">非同期コードの場合、あるプロセスが I/O の完了を待っているとき、そのスレッドは解放され、サーバーによって他の要求の処理に利用できます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="bb61e-124">その結果、非同期コードによってサーバーリソースの使用効率が向上し、サーバーは遅延なしでより多くのトラフィックを処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="bb61e-125">以前のバージョンの .NET では、非同期コードの記述とテストは複雑で、エラーが発生しやすく、デバッグが困難でした。</span><span class="sxs-lookup"><span data-stu-id="bb61e-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="bb61e-126">.NET 4.5 では、非同期コードの記述、テスト、およびデバッグが非常に簡単になりました。通常、そうでない場合を除き、非同期コードを記述することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="bb61e-127">非同期コードでは少量のオーバーヘッドが発生しますが、トラフィックが少ない状況では、パフォーマンスの低下はほとんどありませんが、トラフィックの量が多い場合は、パフォーマンスが大幅に向上する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="bb61e-128">非同期プログラミングの詳細については、「 [.net 4.5 の非同期サポートを使用してブロック呼び出しを回避する](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb61e-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="bb61e-129">Department コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="bb61e-129">Create Department controller</span></span>

<span data-ttu-id="bb61e-130">以前のコントローラーと同じ方法で Department コントローラーを作成します。ただし、今回は **[非同期コントローラーアクションを使用する]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="bb61e-131">次の点は、非同期にするために `Index` メソッドの同期コードに追加されたものを示しています。</span><span class="sxs-lookup"><span data-stu-id="bb61e-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="bb61e-132">Entity Framework データベースクエリを非同期に実行できるようにするために、次の4つの変更が適用されました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="bb61e-133">メソッドは `async` キーワードでマークされます。これにより、メソッド本体の一部に対するコールバックを生成し、返された `Task<ActionResult>` オブジェクトを自動的に作成するようにコンパイラに指示します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="bb61e-134">戻り値の型が `ActionResult` から `Task<ActionResult>`に変更されました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="bb61e-135">`Task<T>` 型は、`T`型の結果で進行中の作業を表します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="bb61e-136">`await` キーワードが web サービス呼び出しに適用されました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="bb61e-137">コンパイラは、このキーワードを認識すると、メソッドを2つの部分に分割します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="bb61e-138">最初の部分は、非同期的に開始される操作で終了します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="bb61e-139">2番目の部分は、操作の完了時に呼び出されるコールバックメソッドに配置されます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="bb61e-140">`ToList` 拡張メソッドの非同期バージョンが呼び出されました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="bb61e-141">`departments.ToList` ステートメントが変更されたが、`departments = db.Departments` ステートメントが変更されたのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="bb61e-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="bb61e-142">これは、クエリまたはコマンドをデータベースに送信するステートメントのみが非同期に実行されるためです。</span><span class="sxs-lookup"><span data-stu-id="bb61e-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="bb61e-143">`departments = db.Departments` ステートメントはクエリを設定しますが、クエリは `ToList` メソッドが呼び出されるまで実行されません。</span><span class="sxs-lookup"><span data-stu-id="bb61e-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="bb61e-144">したがって、`ToList` メソッドのみが非同期に実行されます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="bb61e-145">`Details` メソッドと `HttpGet` `Edit` および `Delete` メソッドでは、`Find` メソッドを使用して、クエリがデータベースに送信されるようにします。これは、非同期的に実行されるメソッドです。</span><span class="sxs-lookup"><span data-stu-id="bb61e-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="bb61e-146">`Create`、`HttpPost Edit`、および `DeleteConfirmed` メソッドでは、これはコマンドを実行する `SaveChanges` メソッド呼び出しであり、メモリ内のエンティティが変更されるだけの `db.Departments.Add(department)` などのステートメントではありません。</span><span class="sxs-lookup"><span data-stu-id="bb61e-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="bb61e-147">*Views\Department\Index.cshtml*を開き、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="bb61e-148">このコードでは、Index から department にタイトルを変更し、管理者名を右に移動して、管理者の完全な名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="bb61e-149">[作成]、[削除]、[詳細]、および [編集] ビューで、[`InstructorID`] フィールドのキャプションを「管理者」に変更します。これは、学科名フィールドをコースビューの "Department" に変更した場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="bb61e-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="bb61e-150">[作成] ビューと [編集] ビューでは、次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="bb61e-151">[削除] ビューと [詳細] ビューでは、次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="bb61e-152">アプリケーションを実行し、 **[部門]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="bb61e-153">すべての動作は他のコントローラーと同じですが、このコントローラーでは、すべての SQL クエリが非同期に実行されます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="bb61e-154">Entity Framework で非同期プログラミングを使用する場合は、次の点に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="bb61e-155">非同期コードはスレッドセーフではありません。</span><span class="sxs-lookup"><span data-stu-id="bb61e-155">The async code is not thread safe.</span></span> <span data-ttu-id="bb61e-156">言い換えると、同じコンテキストインスタンスを使用して複数の操作を並行して実行しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="bb61e-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="bb61e-157">非同期コードのパフォーマンス上の利点を最大限に活用する場合、(ページングなどのために) ライブラリ パッケージを利用しているのであれば、それがクエリをデータベースに送信させる Entity Framework メソッドを呼び出す場合、非同期を利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="bb61e-158">ストアドプロシージャを使用する</span><span class="sxs-lookup"><span data-stu-id="bb61e-158">Use stored procedures</span></span>

<span data-ttu-id="bb61e-159">一部の開発者や Dba は、ストアドプロシージャを使用してデータベースにアクセスしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="bb61e-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="bb61e-160">以前のバージョンの Entity Framework では、[生の SQL クエリを実行](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)することで、ストアドプロシージャを使用してデータを取得できますが、update 操作にストアドプロシージャを使用するように EF に指示することはできません。</span><span class="sxs-lookup"><span data-stu-id="bb61e-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="bb61e-161">EF 6 では、ストアドプロシージャを使用するように Code First を簡単に構成できます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="bb61e-162">*DAL\SchoolContext.cs*で、強調表示されているコードを `OnModelCreating` メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="bb61e-163">このコードは、`Department` エンティティに対する挿入、更新、および削除操作にストアドプロシージャを使用するように Entity Framework に指示します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="bb61e-164">パッケージ管理コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="bb61e-165">*\\&lt;timestamp&gt;\_DepartmentSP.cs*を開いて、Insert、Update、Delete の各ストアドプロシージャを作成するコードを `Up` メソッドに表示します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="bb61e-166">パッケージ管理コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="bb61e-167">アプリケーションをデバッグモードで実行し、 **[部門]** タブをクリックして、 **[新規作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="bb61e-168">新しい部署のデータを入力し、 **[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="bb61e-169">Visual Studio で、 **[出力]** ウィンドウのログを見て、新しい部門の行を挿入するためにストアドプロシージャが使用されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![Department の挿入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="bb61e-171">Code First 既定のストアドプロシージャ名を作成します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="bb61e-172">既存のデータベースを使用している場合は、データベースで既に定義されているストアドプロシージャを使用するために、ストアドプロシージャ名のカスタマイズが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="bb61e-173">その方法の詳細については、「 [Entity Framework Code First Insert/Update/Delete ストアドプロシージャ](https://msdn.microsoft.com/data/dn468673)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb61e-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="bb61e-174">生成されたストアドプロシージャをカスタマイズする場合は、スキャフォールディングコードを編集して、ストアドプロシージャを作成する移行 `Up` 方法を選択できます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="bb61e-175">これにより、移行が実行されるたびに変更が反映され、展開後に運用環境で自動的に移行が実行されるときに、運用データベースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="bb61e-176">以前の移行で作成された既存のストアドプロシージャを変更する場合は、[追加-移行] コマンドを使用して空の移行を生成し、 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)メソッドを呼び出すコードを手動で記述します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="bb61e-177">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="bb61e-177">Deploy to Azure</span></span>

<span data-ttu-id="bb61e-178">このセクションでは、このシリーズの[移行とデプロイ](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するチュートリアルの「 **Azure へのアプリのデプロイ**」セクションを完了している必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb61e-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="bb61e-179">ローカルプロジェクトでデータベースを削除することによって解決した移行エラーが発生した場合は、このセクションをスキップします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="bb61e-180">Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、コンテキスト メニューの **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="bb61e-181">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb61e-181">Click **Publish**.</span></span>

    <span data-ttu-id="bb61e-182">Visual Studio によってアプリケーションが Azure にデプロイされ、アプリケーションが既定のブラウザーで開き、Azure で実行されます。</span><span class="sxs-lookup"><span data-stu-id="bb61e-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="bb61e-183">アプリケーションをテストして、動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="bb61e-184">データベースにアクセスするページを初めて実行する場合、Entity Framework は、現在のデータモデルを使用してデータベースを最新の状態にするために必要なすべての移行 `Up` 方法を実行します。</span><span class="sxs-lookup"><span data-stu-id="bb61e-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="bb61e-185">このチュートリアルで追加した Department ページを含め、最後にデプロイした後に追加したすべての web ページを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="bb61e-186">コードの入手</span><span class="sxs-lookup"><span data-stu-id="bb61e-186">Get the code</span></span>

[<span data-ttu-id="bb61e-187">完成したプロジェクトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="bb61e-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="bb61e-188">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="bb61e-188">Additional resources</span></span>

<span data-ttu-id="bb61e-189">その他の Entity Framework リソースへのリンクについては、 [ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb61e-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb61e-190">次のステップ</span><span class="sxs-lookup"><span data-stu-id="bb61e-190">Next steps</span></span>

<span data-ttu-id="bb61e-191">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="bb61e-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb61e-192">非同期コードについて学習しました</span><span class="sxs-lookup"><span data-stu-id="bb61e-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="bb61e-193">Department コントローラーを作成しました</span><span class="sxs-lookup"><span data-stu-id="bb61e-193">Created a Department controller</span></span>
> * <span data-ttu-id="bb61e-194">使用されたストアドプロシージャ</span><span class="sxs-lookup"><span data-stu-id="bb61e-194">Used stored procedures</span></span>
> * <span data-ttu-id="bb61e-195">Azure にデプロイ済み</span><span class="sxs-lookup"><span data-stu-id="bb61e-195">Deployed to Azure</span></span>

<span data-ttu-id="bb61e-196">複数のユーザーが同時に同じエンティティを更新した場合の競合の処理方法については、次の記事に進んでください。</span><span class="sxs-lookup"><span data-stu-id="bb61e-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bb61e-197">同時実行の処理</span><span class="sxs-lookup"><span data-stu-id="bb61e-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
