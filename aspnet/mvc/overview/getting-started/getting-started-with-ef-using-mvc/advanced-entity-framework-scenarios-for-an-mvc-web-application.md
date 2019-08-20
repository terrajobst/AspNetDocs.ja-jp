---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 'チュートリアル: MVC 5 Web アプリの高度な EF シナリオについて説明します。'
description: このチュートリアルでは、Entity Framework Code First を使用する ASP.NET web アプリケーションを開発する際の基本事項を理解するのに役立ついくつかのトピックを紹介します。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "58425276"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a><span data-ttu-id="6c496-103">チュートリアル: MVC 5 Web アプリの高度な EF シナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6c496-103">Tutorial: Learn about advanced EF Scenarios for an MVC 5 Web app</span></span>

<span data-ttu-id="6c496-104">前のチュートリアルでは、階層ごとの継承を実装しています。</span><span class="sxs-lookup"><span data-stu-id="6c496-104">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="6c496-105">このチュートリアルでは、Entity Framework Code First を使用する ASP.NET web アプリケーションを開発する際の基本事項を理解するのに役立ついくつかのトピックを紹介します。</span><span class="sxs-lookup"><span data-stu-id="6c496-105">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="6c496-106">最初のいくつかのセクションでは、コードを順を追って説明し、Visual Studio を使用してタスクを完了する手順について説明します。詳細については、次のセクションでは、簡単な紹介とリソースへのリンクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6c496-106">The first few sections have step-by-step instructions that walk you through the code and using Visual Studio to complete tasks The sections that follow introduce several topics with brief introductions followed by links to resources for more information.</span></span>

<span data-ttu-id="6c496-107">これらのトピックのほとんどでは、既に作成したページを操作します。</span><span class="sxs-lookup"><span data-stu-id="6c496-107">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="6c496-108">生の SQL を使用して一括更新を行うには、データベース内のすべてのコースのクレジット数を更新する新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="6c496-108">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="6c496-110">このチュートリアルでは、次の作業を行いました。</span><span class="sxs-lookup"><span data-stu-id="6c496-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c496-111">生 SQL クエリを実行する</span><span class="sxs-lookup"><span data-stu-id="6c496-111">Perform raw SQL queries</span></span>
> * <span data-ttu-id="6c496-112">追跡なしのクエリの実行</span><span class="sxs-lookup"><span data-stu-id="6c496-112">Perform no-tracking queries</span></span>
> * <span data-ttu-id="6c496-113">データベースに送信された SQL クエリの確認</span><span class="sxs-lookup"><span data-stu-id="6c496-113">Examine SQL queries sent to database</span></span>

<span data-ttu-id="6c496-114">以下についても説明します。</span><span class="sxs-lookup"><span data-stu-id="6c496-114">You also learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c496-115">抽象化レイヤーの作成</span><span class="sxs-lookup"><span data-stu-id="6c496-115">Creating an abstraction layer</span></span>
> * <span data-ttu-id="6c496-116">プロキシクラス</span><span class="sxs-lookup"><span data-stu-id="6c496-116">Proxy classes</span></span>
> * <span data-ttu-id="6c496-117">変更の自動検出</span><span class="sxs-lookup"><span data-stu-id="6c496-117">Automatic change detection</span></span>
> * <span data-ttu-id="6c496-118">自動検証</span><span class="sxs-lookup"><span data-stu-id="6c496-118">Automatic validation</span></span>
> * <span data-ttu-id="6c496-119">Entity Framework パワーツール</span><span class="sxs-lookup"><span data-stu-id="6c496-119">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="6c496-120">Entity Framework ソースコード</span><span class="sxs-lookup"><span data-stu-id="6c496-120">Entity Framework source code</span></span>

## <a name="prerequisite"></a><span data-ttu-id="6c496-121">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="6c496-121">Prerequisite</span></span>

* [<span data-ttu-id="6c496-122">継承の実装</span><span class="sxs-lookup"><span data-stu-id="6c496-122">Implementing Inheritance</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a><span data-ttu-id="6c496-123">生 SQL クエリを実行する</span><span class="sxs-lookup"><span data-stu-id="6c496-123">Perform raw SQL queries</span></span>

<span data-ttu-id="6c496-124">Entity Framework Code First API には、SQL コマンドをデータベースに直接渡すことができるようにするメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c496-124">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="6c496-125">次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="6c496-125">You have the following options:</span></span>

- <span data-ttu-id="6c496-126">エンティティ型を返すクエリには、 [Dbset SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c496-126">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="6c496-127">返されるオブジェクトは、 `DbSet`オブジェクトによって予期される型である必要があります。また、追跡をオフにしない限り、データベースコンテキストによって自動的に追跡されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-127">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="6c496-128">( [Asnotracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)メソッドについては、次のセクションを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6c496-128">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="6c496-129">エンティティではない型を返すクエリには、[データベースの SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c496-129">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="6c496-130">このメソッドを使用してエンティティ型を取得する場合でも、返されるデータはデータベース コンテキストによって追跡されません。</span><span class="sxs-lookup"><span data-stu-id="6c496-130">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="6c496-131">クエリ以外のコマンドには、[データベースの ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="6c496-131">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="6c496-132">Entity Framework を使用する利点の 1 つは、データを格納する特定のメソッドにコードを過度に接近させなくてもよい点です。</span><span class="sxs-lookup"><span data-stu-id="6c496-132">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="6c496-133">SQL クエリとコマンドが生成されるため、自分でこれらを記述する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="6c496-133">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="6c496-134">ただし、手動で作成した特定の SQL クエリを実行する必要がある場合は、例外的なシナリオがあります。これらのメソッドを使用すると、このような例外を処理できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-134">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="6c496-135">Web アプリケーションで SQL コマンドを実行する場合は常に、SQL インジェクション攻撃から自身のサイトを保護する対策を講じる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-135">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="6c496-136">これを行う 1 つの方法として、パラメーター化されたクエリを使用して、Web ページによって送信された文字列が SQL コマンドとして解釈できないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c496-136">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="6c496-137">このチュートリアルでは、ユーザー入力をクエリに統合するときに、パラメーター化されたクエリを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c496-137">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="6c496-138">エンティティを返すクエリの呼び出し</span><span class="sxs-lookup"><span data-stu-id="6c496-138">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="6c496-139">[&lt;DbsetTEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx)クラスには、型`TEntity`のエンティティを返すクエリを実行するために使用できるメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="6c496-139">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="6c496-140">このしくみを確認するには、 `Details` `Department`コントローラーのメソッドのコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="6c496-140">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="6c496-141">*DepartmentController.cs* `Details`のメソッドで`db.Departments.SqlQuery` 、次の強調表示されたコードに示すように、メソッドの呼び出しをメソッドの呼び出しに置き換えます。`db.Departments.FindAsync`</span><span class="sxs-lookup"><span data-stu-id="6c496-141">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="6c496-142">新しいコードが正しく動作することを確認するには、 **[Departments]\(部門\)** タブを選択し、いずれかの部門の **[Details]\(詳細\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6c496-142">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span> <span data-ttu-id="6c496-143">すべてのデータが想定どおりに表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c496-143">Make sure all of the data displays as expected.</span></span>

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="6c496-144">他の種類のオブジェクトを返すクエリの呼び出し</span><span class="sxs-lookup"><span data-stu-id="6c496-144">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="6c496-145">以前に、登録日ごとの学生数を示す About ページ用に、学生の統計グリッドを作成しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-145">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="6c496-146">*HomeController.cs*でこれを実行するコードは、LINQ を使用します。</span><span class="sxs-lookup"><span data-stu-id="6c496-146">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="6c496-147">LINQ を使用するのではなく、このデータを直接 SQL で取得するコードを記述するとします。</span><span class="sxs-lookup"><span data-stu-id="6c496-147">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="6c496-148">そのためには、エンティティオブジェクト以外のものを返すクエリを実行する必要があります。これは、[データベースの SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)メソッドを使用する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="6c496-148">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="6c496-149">*HomeController.cs*で、次の強調表示され`About`たコードに示すように、メソッド内の LINQ ステートメントを SQL ステートメントに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6c496-149">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="6c496-150">[バージョン情報] ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="6c496-150">Run the About page.</span></span> <span data-ttu-id="6c496-151">前と同じデータが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c496-151">Verify that it displays the same data it did before.</span></span>

### <a name="calling-an-update-query"></a><span data-ttu-id="6c496-152">更新クエリの呼び出し</span><span class="sxs-lookup"><span data-stu-id="6c496-152">Calling an Update Query</span></span>

<span data-ttu-id="6c496-153">Contoso 大学の管理者が、すべてのコースのクレジットの数を変更するなど、データベースで一括変更を実行できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="6c496-153">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="6c496-154">大学に多くのコースがある場合は、それらすべてをエンティティとして取得し、それらを個別に変更するのは非効率的です。</span><span class="sxs-lookup"><span data-stu-id="6c496-154">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="6c496-155">このセクションでは、すべてのコースのクレジット数を変更する要素をユーザーが指定できるようにする web ページを実装します。これにより、SQL `UPDATE`ステートメントを実行して変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-155">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> 

<span data-ttu-id="6c496-156">*CourseController.cs*で、と`UpdateCourseCredits`の`HttpGet`メソッドを`HttpPost`追加します。</span><span class="sxs-lookup"><span data-stu-id="6c496-156">In *CourseController.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="6c496-157">コントローラーが`HttpGet`要求を処理すると、 `ViewBag.RowsAffected`変数に何も返されず、ビューに空のテキストボックスと [送信] ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-157">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button.</span></span>

<span data-ttu-id="6c496-158">**[更新]** ボタンをクリック`HttpPost`すると、メソッド`multiplier`が呼び出され、テキストボックスに値が入力されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-158">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="6c496-159">次に、このコードは、コースを更新する SQL を実行し、影響を受ける行の`ViewBag.RowsAffected`数を変数のビューに返します。</span><span class="sxs-lookup"><span data-stu-id="6c496-159">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="6c496-160">ビューがその変数の値を取得すると、テキストボックスと送信ボタンではなく、更新された行の数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-160">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button.</span></span>

<span data-ttu-id="6c496-161">*CourseController.cs*で、いずれかの`UpdateCourseCredits`メソッドを右クリックし、[ビューの**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c496-161">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span> <span data-ttu-id="6c496-162">**[ビューの追加]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-162">The **Add View** dialog appears.</span></span> <span data-ttu-id="6c496-163">既定値のままにして、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6c496-163">Leave the defaults and select **Add**.</span></span>

<span data-ttu-id="6c496-164">*Views\Course\UpdateCourseCredits.cshtml*で、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6c496-164">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="6c496-165">**[Courses]\(コース\)** タブを選択してから、ブラウザーのアドレス バーで URL の末尾に "/UpdateCourseCredits" を追加して (例: `http://localhost:50205/Course/UpdateCourseCredits`)、`UpdateCourseCredits` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="6c496-165">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="6c496-166">テキスト ボックスに数値を入力します。</span><span class="sxs-lookup"><span data-stu-id="6c496-166">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="6c496-168">**[更新]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c496-168">Click **Update**.</span></span> <span data-ttu-id="6c496-169">影響を受けた行の数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-169">You see the number of rows affected.</span></span>

<span data-ttu-id="6c496-170">**[リストに戻る]** をクリックして、単位数が変更されたコースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="6c496-170">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="6c496-171">未加工の SQL クエリの詳細については、MSDN の「[未加工の Sql クエリ](https://msdn.microsoft.com/data/jj592907)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-171">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="6c496-172">追跡なしのクエリ</span><span class="sxs-lookup"><span data-stu-id="6c496-172">No-tracking queries</span></span>

<span data-ttu-id="6c496-173">データベース コンテキストは、テーブルの行を取得してそれらを表すエンティティ オブジェクトを作成するとき、既定では、メモリ内のエンティティがデータベース内のデータと同期されているかどうかを追跡します。</span><span class="sxs-lookup"><span data-stu-id="6c496-173">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="6c496-174">メモリ内のデータはキャッシュとして機能し、エンティティを更新するときに使われます。</span><span class="sxs-lookup"><span data-stu-id="6c496-174">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="6c496-175">Web アプリケーションでは、一般にコンテキスト インスタンスの存続期間は短く (要求ごとに新しいインスタンスが作成されて破棄されます)、通常、エンティティを読み取るコンテキストはエンティティが再び使われる前に破棄されるので、多くの場合、このようなキャッシュは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6c496-175">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="6c496-176">[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)メソッドを使用して、メモリ内のエンティティオブジェクトの追跡を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-176">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="6c496-177">追跡を無効にした方がよい一般的なシナリオを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="6c496-177">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="6c496-178">クエリでは、追跡を無効にする大量のデータを取得すると、パフォーマンスが著しく向上する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-178">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="6c496-179">エンティティを更新するためにアタッチする必要があるが、以前に別の目的で同じエンティティを取得した場合。</span><span class="sxs-lookup"><span data-stu-id="6c496-179">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="6c496-180">エンティティはデータベース コンテキストによって既に追跡されているため、変更するエンティティをアタッチできません。</span><span class="sxs-lookup"><span data-stu-id="6c496-180">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="6c496-181">この状況に対処する方法の`AsNoTracking` 1 つは、前のクエリでオプションを使用することです。</span><span class="sxs-lookup"><span data-stu-id="6c496-181">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="6c496-182">[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)メソッドの使用方法を示す例については、[このチュートリアルの前のバージョン](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-182">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="6c496-183">このバージョンのチュートリアルでは、編集メソッドでモデルバインダーによって作成されたエンティティに変更フラグが設定され`AsNoTracking`ていないため、必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6c496-183">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

## <a name="examine-sql-sent-to-database"></a><span data-ttu-id="6c496-184">データベースに送信された SQL を調べる</span><span class="sxs-lookup"><span data-stu-id="6c496-184">Examine SQL sent to database</span></span>

<span data-ttu-id="6c496-185">データベースに送信される実際の SQL クエリを確認できると役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-185">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="6c496-186">前のチュートリアルでは、インターセプターコードでこれを行う方法を説明しました。ここで、インターセプターコードを記述せずにこれを実行するいくつかの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6c496-186">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="6c496-187">これを試すには、単純なクエリを見て、一括読み込み、フィルター処理、並べ替えなどのオプションを追加したときに何が起こるかを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="6c496-187">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="6c496-188">の一括読み込みを一時的に停止`Index`するには、 *Controllers/CourseController*で、メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6c496-188">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="6c496-189">次に、 `return`ステートメントにブレークポイントを設定します (その行のカーソルを使用して、F9 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="6c496-189">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="6c496-190">**F5**キーを押してプロジェクトをデバッグモードで実行し、[Course Index] ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c496-190">Press **F5** to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="6c496-191">コードがブレークポイントに到達したら、 `sql`変数を調べます。</span><span class="sxs-lookup"><span data-stu-id="6c496-191">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="6c496-192">SQL Server に送信されるクエリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-192">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="6c496-193">これは単純な`Select`ステートメントです。</span><span class="sxs-lookup"><span data-stu-id="6c496-193">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="6c496-194">虫眼鏡をクリックすると、**テキストビジュアライザー**でクエリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-194">Click the magnifying glass to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="6c496-195">次に、ユーザーが特定の部門をフィルター処理できるように、[コースのインデックス] ページにドロップダウンリストを追加します。</span><span class="sxs-lookup"><span data-stu-id="6c496-195">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="6c496-196">コースはタイトルで並べ替えることができ、 `Department`ナビゲーションプロパティの一括読み込みを指定します。</span><span class="sxs-lookup"><span data-stu-id="6c496-196">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="6c496-197">*CourseController.cs*で、 `Index`メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6c496-197">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="6c496-198">`return`ステートメントにブレークポイントを復元します。</span><span class="sxs-lookup"><span data-stu-id="6c496-198">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="6c496-199">メソッドは、 `SelectedDepartment`パラメーターのドロップダウンリストの選択された値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="6c496-199">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="6c496-200">何も選択されていない場合、このパラメーターは null になります。</span><span class="sxs-lookup"><span data-stu-id="6c496-200">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="6c496-201">すべての部門を含むコレクションがドロップダウンリストのビューに渡されます。`SelectList`</span><span class="sxs-lookup"><span data-stu-id="6c496-201">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="6c496-202">`SelectList`コンストラクターに渡されるパラメーターは、値フィールド名、テキストフィールド名、および選択された項目を指定します。</span><span class="sxs-lookup"><span data-stu-id="6c496-202">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="6c496-203">このコードでは、 `Course`リポジトリの`Department` メソッドに対して、ナビゲーションプロパティのフィルター式、並べ替え順序、および一括読み込みを指定しています。`Get`</span><span class="sxs-lookup"><span data-stu-id="6c496-203">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="6c496-204">ドロップダウンリストで何`true`も選択されていない場合 (つまり、 `SelectedDepartment`が null の場合)、フィルター式は常にを返します。</span><span class="sxs-lookup"><span data-stu-id="6c496-204">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="6c496-205">*Views\Course\Index.cshtml*の開始`table`タグの直前に、ドロップダウンリストと [送信] ボタンを作成する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="6c496-205">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="6c496-206">ブレークポイントを設定したまま、[コースのインデックス] ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="6c496-206">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="6c496-207">コードが最初にブレークポイントにヒットしたときに、ページがブラウザーに表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="6c496-207">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="6c496-208">ドロップダウンリストから部門を選択し、 **[フィルター]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c496-208">Select a department from the drop-down list and click **Filter**.</span></span>

<span data-ttu-id="6c496-209">今回は、ドロップダウンリストの部門クエリの最初のブレークポイントになります。</span><span class="sxs-lookup"><span data-stu-id="6c496-209">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="6c496-210">これをスキップし、 `query`次にコードがブレークポイントに到達したときに変数を表示`Course`して、クエリがどのように見えるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c496-210">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="6c496-211">次のような内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-211">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="6c496-212">クエリが`JOIN` データと`Course`共にデータを読み込み`Department` 、句を`WHERE`含むクエリであることがわかります。</span><span class="sxs-lookup"><span data-stu-id="6c496-212">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="6c496-213">行を`var sql = courses.ToString()`削除します。</span><span class="sxs-lookup"><span data-stu-id="6c496-213">Remove the `var sql = courses.ToString()` line.</span></span>

## <a name="create-an-abstraction-layer"></a><span data-ttu-id="6c496-214">抽象化レイヤーを作成する</span><span class="sxs-lookup"><span data-stu-id="6c496-214">Create an abstraction layer</span></span>

<span data-ttu-id="6c496-215">多くの開発者は、Entity Framework で動作するコードをラップするラッパーとして、Repository パターンと Unit of Work パターンを実装するためのコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="6c496-215">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="6c496-216">これらのパターンは、アプリケーションのデータ アクセス層とビジネス ロジック層の間に抽象化レイヤーを作成するためのものです。</span><span class="sxs-lookup"><span data-stu-id="6c496-216">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="6c496-217">これらのパターンを実装すると、データ ストアの変更からアプリケーションを隔離でき、自動化された単体テストやテスト駆動開発 (TDD) を円滑化できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-217">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="6c496-218">ただし、次のような理由から、これらのパターンを実装するための追加コードを記述することは、EF を使用するアプリケーションには必ずしも最適な選択肢とは言えません。</span><span class="sxs-lookup"><span data-stu-id="6c496-218">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="6c496-219">EF コンテキスト クラス自体が、コードをデータ ストア固有のコードから隔離します。</span><span class="sxs-lookup"><span data-stu-id="6c496-219">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="6c496-220">EF コンテキスト クラスは、EF を使用して行っているデータベースの更新の unit-of-work クラスとして動作できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-220">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="6c496-221">Entity Framework 6 で導入された機能を使用すると、リポジトリコードを記述しなくても TDD を簡単に実装できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-221">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="6c496-222">リポジトリと作業単位パターンを実装する方法の詳細については、[このチュートリアルシリーズの Entity Framework 5 バージョン](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-222">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="6c496-223">Entity Framework 6 で TDD を実装する方法の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-223">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="6c496-224">EF6 による DbSets のモックの簡単な有効化</span><span class="sxs-lookup"><span data-stu-id="6c496-224">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="6c496-225">モックフレームワークを使用したテスト</span><span class="sxs-lookup"><span data-stu-id="6c496-225">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="6c496-226">独自のテストの倍精度でテストする</span><span class="sxs-lookup"><span data-stu-id="6c496-226">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a><span data-ttu-id="6c496-227">プロキシクラス</span><span class="sxs-lookup"><span data-stu-id="6c496-227">Proxy classes</span></span>

<span data-ttu-id="6c496-228">Entity Framework がエンティティインスタンスを作成するとき (たとえば、クエリの実行時)、エンティティのプロキシとして機能する動的に生成された派生型のインスタンスとして作成されることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="6c496-228">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="6c496-229">たとえば、次の2つのデバッガーイメージを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-229">For example, see the following two debugger images.</span></span> <span data-ttu-id="6c496-230">最初の図では、エンティティをインスタンス`student`化した直後`Student`に変数が予期される型であることがわかります。</span><span class="sxs-lookup"><span data-stu-id="6c496-230">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="6c496-231">2番目のイメージでは、EF を使用してデータベースから student エンティティを読み取ると、プロキシクラスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-231">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![Before プロキシクラス](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![After プロキシクラス](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="6c496-234">このプロキシクラスは、プロパティにアクセスしたときにアクションを自動的に実行するフックを挿入するために、エンティティの一部の仮想プロパティをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="6c496-234">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="6c496-235">このメカニズムを使用して遅延読み込みを行う関数が1つあります。</span><span class="sxs-lookup"><span data-stu-id="6c496-235">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="6c496-236">ほとんどの場合、このプロキシの使用を意識する必要はありませんが、例外があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-236">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="6c496-237">場合によっては、Entity Framework がプロキシインスタンスを作成できないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-237">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="6c496-238">たとえば、エンティティをシリアル化する場合、通常はプロキシクラスではなく、POCO クラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="6c496-238">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="6c496-239">シリアル化の問題を回避する1つの方法は、「 [Using WEB API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)チュートリアル」に示されているように、エンティティオブジェクトではなくデータ転送オブジェクト (dto) をシリアル化することです。</span><span class="sxs-lookup"><span data-stu-id="6c496-239">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="6c496-240">もう1つの方法は、[プロキシの作成を無効](https://msdn.microsoft.com/data/jj592886.aspx)にすることです。</span><span class="sxs-lookup"><span data-stu-id="6c496-240">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="6c496-241">`new`演算子を使用してエンティティクラスをインスタンス化する場合、プロキシインスタンスは取得されません。</span><span class="sxs-lookup"><span data-stu-id="6c496-241">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="6c496-242">これは、遅延読み込みや自動変更追跡などの機能を利用できないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="6c496-242">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="6c496-243">これは通常は問題ありません。通常、遅延読み込みは必要ありません。これは、データベースに存在しない新しいエンティティを作成しているためです。また、エンティティをとして`Added`明示的にマークしている場合は、通常、変更の追跡は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6c496-243">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="6c496-244">ただし、遅延読み込みが必要で、変更の追跡が必要な場合は、 `DbSet`クラスの[create](https://msdn.microsoft.com/library/gg679504.aspx)メソッドを使用して、プロキシを使用して新しいエンティティインスタンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-244">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="6c496-245">プロキシ型から実際のエンティティ型を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="6c496-245">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="6c496-246">`ObjectContext`クラスの[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)メソッドを使用して、プロキシ型インスタンスの実際のエンティティ型を取得できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-246">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="6c496-247">詳細については、MSDN の「[プロキシの](https://msdn.microsoft.com/data/JJ592886.aspx)使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-247">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="6c496-248">変更の自動検出</span><span class="sxs-lookup"><span data-stu-id="6c496-248">Automatic change detection</span></span>

<span data-ttu-id="6c496-249">Entity Framework では、エンティティの現在の値と元の値を比較して、エンティティがどのように変更されたか (およびそれによって、どの更新プログラムをデータベースに送信する必要があるか) を判断します。</span><span class="sxs-lookup"><span data-stu-id="6c496-249">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="6c496-250">元の値は、エンティティが照会されるかアタッチされるときに格納されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-250">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="6c496-251">変更の自動検出を行うメソッドには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="6c496-251">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="6c496-252">多数のエンティティを追跡していて、これらのメソッドのいずれかをループ内で何度も呼び出す場合、Autodetection の[有効な](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)プロパティを使用して自動変更検出を一時的に無効にすると、パフォーマンスが大幅に向上する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6c496-252">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="6c496-253">詳細については、MSDN の「[変更を自動的に検出](https://msdn.microsoft.com/data/jj556205)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-253">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

## <a name="automatic-validation"></a><span data-ttu-id="6c496-254">自動検証</span><span class="sxs-lookup"><span data-stu-id="6c496-254">Automatic validation</span></span>

<span data-ttu-id="6c496-255">`SaveChanges`メソッドを呼び出すと、既定では、Entity Framework は、データベースを更新する前に、変更されたすべてのエンティティのすべてのプロパティのデータを検証します。</span><span class="sxs-lookup"><span data-stu-id="6c496-255">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="6c496-256">多数のエンティティを更新していて、既にデータを検証している場合、この作業は不要であり、変更の保存プロセスを一時的に無効にすることによって時間を短縮することができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-256">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="6c496-257">これは、 [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)プロパティを使用して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-257">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="6c496-258">詳細については、MSDN の「[検証](https://msdn.microsoft.com/data/gg193959)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-258">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

## <a name="entity-framework-power-tools"></a><span data-ttu-id="6c496-259">Entity Framework パワーツール</span><span class="sxs-lookup"><span data-stu-id="6c496-259">Entity Framework Power Tools</span></span>

<span data-ttu-id="6c496-260">[Entity Framework パワーツール](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition)は、これらのチュートリアルで示すデータモデルダイアグラムを作成するために使用された Visual Studio アドインです。</span><span class="sxs-lookup"><span data-stu-id="6c496-260">[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="6c496-261">また、このツールでは、既存のデータベース内のテーブルに基づいてエンティティクラスを生成するなど、他の機能を実行して、Code First でデータベースを使用できるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="6c496-261">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="6c496-262">ツールをインストールすると、いくつかの追加オプションがコンテキストメニューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-262">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="6c496-263">たとえば、**ソリューションエクスプローラー**でコンテキストクラスを右クリックすると、と**Entity Framework**  オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c496-263">For example, when you right-click your context class in **Solution Explorer**, you see and **Entity Framework** option.</span></span> <span data-ttu-id="6c496-264">これにより、図を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-264">This gives you the ability to generate a diagram.</span></span> <span data-ttu-id="6c496-265">Code First を使用している場合、図のデータモデルを変更することはできませんが、わかりやすくするために移動することができます。</span><span class="sxs-lookup"><span data-stu-id="6c496-265">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![EF の図](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a><span data-ttu-id="6c496-267">Entity Framework ソースコード</span><span class="sxs-lookup"><span data-stu-id="6c496-267">Entity Framework source code</span></span>

<span data-ttu-id="6c496-268">Entity Framework 6 のソースコードは、 [GitHub](https://github.com/aspnet/EntityFramework6)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="6c496-268">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="6c496-269">バグを提出することができます。また、EF ソースコードに独自の拡張機能を提供することもできます。</span><span class="sxs-lookup"><span data-stu-id="6c496-269">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="6c496-270">ソースコードは開かれていますが、Entity Framework は Microsoft 製品として完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6c496-270">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="6c496-271">Microsoft Entity Framework チームは、各リリースの品質を保証するため、受け入れる投稿を管理し、すべてのコード変更をテストしています。</span><span class="sxs-lookup"><span data-stu-id="6c496-271">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="6c496-272">謝辞</span><span class="sxs-lookup"><span data-stu-id="6c496-272">Acknowledgments</span></span>

- <span data-ttu-id="6c496-273">Tom Dykstra は、このチュートリアルの元のバージョンを作成し、EF 5 更新プログラムを併置し、EF 6 更新プログラムを記述しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-273">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="6c496-274">Tom は、Microsoft Web Platform and Tools コンテンツチームのシニアプログラミングライターです。</span><span class="sxs-lookup"><span data-stu-id="6c496-274">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="6c496-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/)(twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) は、ef 5 および MVC 4 のチュートリアルを更新し、ef 6 更新プログラムを共同作成しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="6c496-276">Rick は、Microsoft が Azure と MVC に注力するシニアプログラミングライターです。</span><span class="sxs-lookup"><span data-stu-id="6c496-276">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="6c496-277">Entity Framework チームの[Rowan 明美](http://www.romiller.com)とその他のメンバーは、コードレビューを支援し、ef 5 および ef 6 のチュートリアルを更新している間に発生した移行に関する多くの問題のデバッグを支援しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-277">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

## <a name="troubleshoot-common-errors"></a><span data-ttu-id="6c496-278">一般的なエラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="6c496-278">Troubleshoot common errors</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="6c496-279">作成/シャドウコピーできません</span><span class="sxs-lookup"><span data-stu-id="6c496-279">Cannot create/shadow copy</span></span>

<span data-ttu-id="6c496-280">エラー メッセージ:</span><span class="sxs-lookup"><span data-stu-id="6c496-280">Error Message:</span></span>

> <span data-ttu-id="6c496-281">ファイルが既に存在する&lt;場合&gt;は、' filename ' を作成/シャドウコピーできません。</span><span class="sxs-lookup"><span data-stu-id="6c496-281">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>

<span data-ttu-id="6c496-282">ソリューション</span><span class="sxs-lookup"><span data-stu-id="6c496-282">Solution</span></span>

<span data-ttu-id="6c496-283">数秒待ってから、ページを更新してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-283">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="6c496-284">更新-データベースを認識できません</span><span class="sxs-lookup"><span data-stu-id="6c496-284">Update-Database not recognized</span></span>

<span data-ttu-id="6c496-285">エラーメッセージ (PMC の`Update-Database`コマンドから):</span><span class="sxs-lookup"><span data-stu-id="6c496-285">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="6c496-286">"データベースの更新" という用語は、コマンドレット、関数、スクリプトファイル、または操作可能なプログラムの名前として認識されません。</span><span class="sxs-lookup"><span data-stu-id="6c496-286">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="6c496-287">名前が正しく記述されていることを確認し、パスが含まれている場合はそのパスが正しいことを確認してから、再試行してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-287">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>

<span data-ttu-id="6c496-288">ソリューション</span><span class="sxs-lookup"><span data-stu-id="6c496-288">Solution</span></span>

<span data-ttu-id="6c496-289">Visual Studio を終了します。</span><span class="sxs-lookup"><span data-stu-id="6c496-289">Exit Visual Studio.</span></span> <span data-ttu-id="6c496-290">プロジェクトを再度開き、もう一度やり直してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-290">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="6c496-291">検証失敗</span><span class="sxs-lookup"><span data-stu-id="6c496-291">Validation failed</span></span>

<span data-ttu-id="6c496-292">エラーメッセージ (PMC の`Update-Database`コマンドから):</span><span class="sxs-lookup"><span data-stu-id="6c496-292">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="6c496-293">1つ以上のエンティティの検証に失敗しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-293">Validation failed for one or more entities.</span></span> <span data-ttu-id="6c496-294">詳細については、' EntityValidationErrors ' プロパティを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-294">See 'EntityValidationErrors' property for more details.</span></span>

<span data-ttu-id="6c496-295">ソリューション</span><span class="sxs-lookup"><span data-stu-id="6c496-295">Solution</span></span>

<span data-ttu-id="6c496-296">この問題の原因の1つは、メソッド`Seed`の実行時の検証エラーです。</span><span class="sxs-lookup"><span data-stu-id="6c496-296">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="6c496-297">メソッドのデバッグに関するヒントについては、 `Seed` 「 [Entity Framework (EF) db のシード処理とデバッグ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-297">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="6c496-298">HTTP 500.19 エラー</span><span class="sxs-lookup"><span data-stu-id="6c496-298">HTTP 500.19 error</span></span>

<span data-ttu-id="6c496-299">エラー メッセージ:</span><span class="sxs-lookup"><span data-stu-id="6c496-299">Error Message:</span></span>

> <span data-ttu-id="6c496-300">HTTP エラー 500.19-内部サーバーエラーページの関連する構成データが無効なため、要求されたページにアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="6c496-300">HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

<span data-ttu-id="6c496-301">ソリューション</span><span class="sxs-lookup"><span data-stu-id="6c496-301">Solution</span></span>

<span data-ttu-id="6c496-302">このエラーを発生させる1つの方法は、ソリューションの複数のコピーを保持し、それぞれが同じポート番号を使用することです。</span><span class="sxs-lookup"><span data-stu-id="6c496-302">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="6c496-303">通常、この問題を解決するには、Visual Studio のすべてのインスタンスを終了し、作業中のプロジェクトを再起動します。</span><span class="sxs-lookup"><span data-stu-id="6c496-303">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="6c496-304">それでもうまくいかない場合は、ポート番号を変更してみてください。</span><span class="sxs-lookup"><span data-stu-id="6c496-304">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="6c496-305">プロジェクトファイルを右クリックし、[プロパティ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c496-305">Right click on the project file and then click properties.</span></span> <span data-ttu-id="6c496-306">**[Web]** タブを選択し、 **[プロジェクトの Url]** テキストボックスでポート番号を変更します。</span><span class="sxs-lookup"><span data-stu-id="6c496-306">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="6c496-307">SQL Server インスタンスの位置を特定しているときのエラー</span><span class="sxs-lookup"><span data-stu-id="6c496-307">Error locating SQL Server instance</span></span>

<span data-ttu-id="6c496-308">エラー メッセージ:</span><span class="sxs-lookup"><span data-stu-id="6c496-308">Error Message:</span></span>

> <span data-ttu-id="6c496-309">SQL Server への接続を確立しているときに、ネットワーク関連またはインスタンス固有のエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-309">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="6c496-310">サーバーが見つからないかアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="6c496-310">The server was not found or was not accessible.</span></span> <span data-ttu-id="6c496-311">インスタンス名が正しいこと、および SQL Server がリモート接続を許可するように構成されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-311">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="6c496-312">(プロバイダー:SQL ネットワーク インターフェイス、エラー:26 - 指定されたサーバーまたはインスタンスの位置を特定しているときにエラーが発生しました)</span><span class="sxs-lookup"><span data-stu-id="6c496-312">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="6c496-313">ソリューション</span><span class="sxs-lookup"><span data-stu-id="6c496-313">Solution</span></span>

<span data-ttu-id="6c496-314">接続文字列を確認します。</span><span class="sxs-lookup"><span data-stu-id="6c496-314">Check the connection string.</span></span> <span data-ttu-id="6c496-315">データベースを手動で削除した場合は、構築文字列内のデータベースの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="6c496-315">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="6c496-316">コードを取得する</span><span class="sxs-lookup"><span data-stu-id="6c496-316">Get the code</span></span>

[<span data-ttu-id="6c496-317">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="6c496-317">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="6c496-318">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="6c496-318">Additional resources</span></span>

 <span data-ttu-id="6c496-319">Entity Framework を使用してデータを操作する方法の詳細については、 [MSDN の EF ドキュメントページ](https://msdn.microsoft.com/data/ee712907)および[ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-319">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="6c496-320">Web アプリケーションを構築した後にデプロイする方法の詳細については、MSDN ライブラリの「 [ASP.NET Web Deployment-推奨リソース](../../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-320">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="6c496-321">認証や承認など、MVC に関連するその他のトピックについては、 [ASP.NET mvc の推奨リソース](../recommended-resources-for-mvc.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-321">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c496-322">次の手順</span><span class="sxs-lookup"><span data-stu-id="6c496-322">Next steps</span></span>

<span data-ttu-id="6c496-323">このチュートリアルでは、次の作業を行いました。</span><span class="sxs-lookup"><span data-stu-id="6c496-323">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c496-324">生 SQL クエリを実行した</span><span class="sxs-lookup"><span data-stu-id="6c496-324">Performed raw SQL queries</span></span>
> * <span data-ttu-id="6c496-325">追跡なしのクエリを実行しました</span><span class="sxs-lookup"><span data-stu-id="6c496-325">Performed no-tracking queries</span></span>
> * <span data-ttu-id="6c496-326">データベースに送信された SQL クエリを調べています</span><span class="sxs-lookup"><span data-stu-id="6c496-326">Examined SQL queries sent to the database</span></span>

<span data-ttu-id="6c496-327">以下についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="6c496-327">You also learned about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c496-328">抽象化レイヤーの作成</span><span class="sxs-lookup"><span data-stu-id="6c496-328">Creating an abstraction layer</span></span>
> * <span data-ttu-id="6c496-329">プロキシクラス</span><span class="sxs-lookup"><span data-stu-id="6c496-329">Proxy classes</span></span>
> * <span data-ttu-id="6c496-330">変更の自動検出</span><span class="sxs-lookup"><span data-stu-id="6c496-330">Automatic change detection</span></span>
> * <span data-ttu-id="6c496-331">自動検証</span><span class="sxs-lookup"><span data-stu-id="6c496-331">Automatic validation</span></span>
> * <span data-ttu-id="6c496-332">Entity Framework パワーツール</span><span class="sxs-lookup"><span data-stu-id="6c496-332">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="6c496-333">Entity Framework ソースコード</span><span class="sxs-lookup"><span data-stu-id="6c496-333">Entity Framework source code</span></span>

<span data-ttu-id="6c496-334">これで、ASP.NET MVC アプリケーションでの Entity Framework の使用に関するこの一連のチュートリアルは完了です。</span><span class="sxs-lookup"><span data-stu-id="6c496-334">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="6c496-335">EF Database First について学習する場合は、DB の最初のチュートリアルシリーズを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c496-335">If you want to learn about EF Database First, see the DB First tutorial series.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6c496-336">Entity Framework Database First</span><span class="sxs-lookup"><span data-stu-id="6c496-336">Entity Framework Database First</span></span>](../database-first-development/setting-up-database.md)