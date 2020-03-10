---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリケーションでの Entity Framework を使用した並べ替え、フィルター処理、およびページングの追加 |Microsoft Docs'
author: tdykstra
description: このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を**Students**インデックスページに追加します。 また、単純なグループ化ページも作成します。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499330"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="61ecf-104">チュートリアル: ASP.NET MVC アプリケーションでの Entity Framework を使用した並べ替え、フィルター処理、およびページングの追加</span><span class="sxs-lookup"><span data-stu-id="61ecf-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="61ecf-105">前の[チュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、`Student` エンティティに対する基本的な CRUD 操作用の一連の web ページを実装しています。</span><span class="sxs-lookup"><span data-stu-id="61ecf-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="61ecf-106">このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を**Students**インデックスページに追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="61ecf-107">また、単純なグループ化ページも作成します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="61ecf-108">次の図は、完了したときのページの外観を示しています。</span><span class="sxs-lookup"><span data-stu-id="61ecf-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="61ecf-109">列見出しとは、ユーザーがクリックしてその列で並べ替えを行うことができるリンクです。</span><span class="sxs-lookup"><span data-stu-id="61ecf-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="61ecf-110">列見出しを繰り返しクリックすると、昇順と降順の並べ替え順序が切り替えられます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="61ecf-112">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="61ecf-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61ecf-113">列の並べ替えリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-113">Add column sort links</span></span>
> * <span data-ttu-id="61ecf-114">[検索] ボックスを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-114">Add a Search box</span></span>
> * <span data-ttu-id="61ecf-115">ページングの追加</span><span class="sxs-lookup"><span data-stu-id="61ecf-115">Add paging</span></span>
> * <span data-ttu-id="61ecf-116">About ページを作成する</span><span class="sxs-lookup"><span data-stu-id="61ecf-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61ecf-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="61ecf-117">Prerequisites</span></span>

* [<span data-ttu-id="61ecf-118">基本 CRUD 機能を実装する</span><span class="sxs-lookup"><span data-stu-id="61ecf-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="61ecf-119">列の並べ替えリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-119">Add column sort links</span></span>

<span data-ttu-id="61ecf-120">学生用インデックスページに並べ替えを追加するには、`Student` コントローラーの `Index` メソッドを変更し、`Student` インデックスビューにコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="61ecf-121">Index メソッドに並べ替え機能を追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="61ecf-122">*Controllers\StudentController.cs*で、`Index` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="61ecf-123">このコードは、URL 内の文字列から `sortOrder` パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="61ecf-124">クエリ文字列値は、ASP.NET MVC によってアクションメソッドのパラメーターとして提供されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="61ecf-125">パラメーターは、"Name" または "Date" の文字列であり、必要に応じてアンダースコアと文字列 "desc" を降順で指定します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="61ecf-126">既定の並べ替え順は昇順です。</span><span class="sxs-lookup"><span data-stu-id="61ecf-126">The default sort order is ascending.</span></span>

<span data-ttu-id="61ecf-127">インデックス ページが初めて要求されたときには、クエリ文字列はありません。</span><span class="sxs-lookup"><span data-stu-id="61ecf-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="61ecf-128">学生は、`LastName`によって昇順に表示されます。これは、`switch` ステートメントのフォールスルーケースによって確立される既定の設定です。</span><span class="sxs-lookup"><span data-stu-id="61ecf-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="61ecf-129">ユーザーが列見出しハイパーリンクをクリックすると、適切な `sortOrder` 値がクエリ文字列で提供されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="61ecf-130">次の2つの `ViewBag` 変数を使用して、ビューが列見出しのハイパーリンクと適切なクエリ文字列値を構成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="61ecf-131">これらは、三項ステートメントです。</span><span class="sxs-lookup"><span data-stu-id="61ecf-131">These are ternary statements.</span></span> <span data-ttu-id="61ecf-132">最初のパラメーターでは、`sortOrder` パラメーターが null または空の場合、`ViewBag.NameSortParm` を "name\_desc" に設定する必要があることを指定します。それ以外の場合は、空の文字列に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="61ecf-133">これらの 2 つのステートメントを使用して、次のようにビューで列見出しのハイパーリンクの設定することができます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="61ecf-134">既定の並べ替え順</span><span class="sxs-lookup"><span data-stu-id="61ecf-134">Current sort order</span></span> | <span data-ttu-id="61ecf-135">姓のハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="61ecf-135">Last Name Hyperlink</span></span> | <span data-ttu-id="61ecf-136">日付のハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="61ecf-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ecf-137">姓の昇順</span><span class="sxs-lookup"><span data-stu-id="61ecf-137">Last Name ascending</span></span> | <span data-ttu-id="61ecf-138">descending</span><span class="sxs-lookup"><span data-stu-id="61ecf-138">descending</span></span> | <span data-ttu-id="61ecf-139">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-139">ascending</span></span> |
| <span data-ttu-id="61ecf-140">姓の降順</span><span class="sxs-lookup"><span data-stu-id="61ecf-140">Last Name descending</span></span> | <span data-ttu-id="61ecf-141">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-141">ascending</span></span> | <span data-ttu-id="61ecf-142">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-142">ascending</span></span> |
| <span data-ttu-id="61ecf-143">日付の昇順</span><span class="sxs-lookup"><span data-stu-id="61ecf-143">Date ascending</span></span> | <span data-ttu-id="61ecf-144">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-144">ascending</span></span> | <span data-ttu-id="61ecf-145">descending</span><span class="sxs-lookup"><span data-stu-id="61ecf-145">descending</span></span> |
| <span data-ttu-id="61ecf-146">日付の降順</span><span class="sxs-lookup"><span data-stu-id="61ecf-146">Date descending</span></span> | <span data-ttu-id="61ecf-147">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-147">ascending</span></span> | <span data-ttu-id="61ecf-148">ascending</span><span class="sxs-lookup"><span data-stu-id="61ecf-148">ascending</span></span> |

<span data-ttu-id="61ecf-149">このメソッドは[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)を使用して、並べ替えの基準となる列を指定します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="61ecf-150">このコードは、`switch` ステートメントの前に <xref:System.Linq.IQueryable%601> 変数を作成し、`switch` ステートメントで変更し、`switch` ステートメントの後に `ToList` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="61ecf-151">`IQueryable` 変数を作成および変更するときに、データベースに送信されるクエリはありません。</span><span class="sxs-lookup"><span data-stu-id="61ecf-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="61ecf-152">`ToList`などのメソッドを呼び出すことによって `IQueryable` オブジェクトをコレクションに変換するまで、クエリは実行されません。</span><span class="sxs-lookup"><span data-stu-id="61ecf-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="61ecf-153">このため、このコードでは、`return View` ステートメントまで実行されない1つのクエリが生成されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="61ecf-154">各並べ替え順序に対して異なる LINQ ステートメントを記述する代わりに、LINQ ステートメントを動的に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="61ecf-155">動的 LINQ の詳細については、「 [DYNAMIC linq](https://go.microsoft.com/fwlink/?LinkID=323957)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="61ecf-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="61ecf-156">列見出しのハイパーリンクを Student インデックスビューに追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="61ecf-157">*Views\Student\Index.cshtml*で、見出し行の `<tr>` と `<th>` の要素を、強調表示されたコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="61ecf-158">このコードでは、`ViewBag` プロパティの情報を使用して、適切なクエリ文字列値を持つハイパーリンクを設定します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="61ecf-159">ページを実行し、 **[Last Name]** と **[Enrollment Date]** 列見出しをクリックして、並べ替えが機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="61ecf-160">**最後の名前**の見出しをクリックすると、学生が姓の降順で表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="61ecf-161">[検索] ボックスを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-161">Add a Search box</span></span>

<span data-ttu-id="61ecf-162">Students インデックスページにフィルターを追加するには、テキストボックスと [送信] ボタンをビューに追加し、`Index` メソッドで対応する変更を行います。</span><span class="sxs-lookup"><span data-stu-id="61ecf-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="61ecf-163">テキストボックスを使用すると、[名] および [姓] フィールドで検索する文字列を入力できます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="61ecf-164">Index メソッドにフィルター機能を追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="61ecf-165">*Controllers\StudentController.cs*で、`Index` メソッドを次のコードに置き換えます (変更は強調表示されています)。</span><span class="sxs-lookup"><span data-stu-id="61ecf-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="61ecf-166">このコードは、`Index` メソッドに `searchString` パラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="61ecf-167">インデックス ビューに追加するテキスト ボックスから検索する文字列値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="61ecf-168">また、最初の名前または姓に検索文字列が含まれている学生だけを選択する LINQ ステートメントに `where` 句を追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="61ecf-169"><xref:System.Linq.Queryable.Where%2A> 句を追加するステートメントは、検索する値がある場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="61ecf-170">多くの場合、Entity Framework のエンティティセットまたはメモリ内のコレクションの拡張メソッドとして、同じメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="61ecf-171">通常、結果は同じですが、場合によっては異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="61ecf-172">たとえば、`Contains` メソッドの .NET Framework 実装では、空の文字列を渡すとすべての行が返されますが、SQL Server Compact 4.0 の Entity Framework プロバイダーは空の文字列に対して0行を返します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="61ecf-173">したがって、この例のコード (`if` ステートメント内に `Where` ステートメントを記述する) を使用すると、すべてのバージョンの SQL Server に対して同じ結果が得られるようになります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="61ecf-174">また、`Contains` メソッドの .NET Framework 実装では、既定で大文字と小文字を区別した比較が実行されますが、Entity Framework SQL Server プロバイダーは既定で大文字と小文字を区別しない比較を実行します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="61ecf-175">したがって、`ToUpper` メソッドを呼び出してテストを明示的に大文字と小文字を区別しないようにすると、後でリポジトリを使用するようにコードを変更したときに結果が変更されないようにすることができます。これにより、`IQueryable` オブジェクトではなく `IEnumerable` コレクションが返されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="61ecf-176">(`Contains` コレクションに対して `IEnumerable` メソッドを呼び出したときには、.NET Framework の実装を取得します。`IQueryable` オブジェクトに対して呼び出したときには、データベース プロバイダーの実装を取得します)。</span><span class="sxs-lookup"><span data-stu-id="61ecf-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="61ecf-177">また、Null 処理は、データベースプロバイダーによって異なる場合や、`IEnumerable` コレクションを使用する場合と比較して `IQueryable` オブジェクトを使用する場合には異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="61ecf-178">たとえば、一部のシナリオでは、`table.Column != 0` などの `Where` 条件で、値として `null` を持つ列が返されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="61ecf-179">既定では、EF は、メモリ内での動作と同様に、null 値間の等価性を高めるために追加の SQL 演算子を生成しますが、EF6 で[Usedatabasenullsemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)フラグを設定するか、または EF Core で[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)メソッドを呼び出してこの動作を構成することができます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="61ecf-180">学生用インデックスビューに検索ボックスを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="61ecf-181">*Views\Student\Index.cshtml*で、キャプション、テキストボックス、および**検索**ボタンを作成するために、開始 `table` タグの直前に強調表示されているコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="61ecf-182">ページを実行し、検索文字列を入力して **[検索]** をクリックし、フィルター処理が機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="61ecf-183">URL に "an" という検索文字列が含まれていないことに注意してください。つまり、このページにブックマークを指定すると、ブックマークを使用するとフィルター処理された一覧が表示されません。</span><span class="sxs-lookup"><span data-stu-id="61ecf-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="61ecf-184">これは、一覧全体を並べ替えるため、列の並べ替えリンクにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="61ecf-185">このチュートリアルの後の方で、フィルター条件にクエリ文字列を使用するように **[検索]** ボタンを変更します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="61ecf-186">ページングの追加</span><span class="sxs-lookup"><span data-stu-id="61ecf-186">Add paging</span></span>

<span data-ttu-id="61ecf-187">Students インデックスページにページングを追加するには、まず**PagedList** NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="61ecf-188">次に、`Index` メソッドに追加の変更を加え、ページングリンクを `Index` ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="61ecf-189">**PagedList**は、ASP.NET Mvc 用の多くの優れたページングおよび並べ替えパッケージの1つです。この使用方法は、他のオプションよりも推奨されるものではなく、例としてのみ使用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="61ecf-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="61ecf-190">PagedList NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="61ecf-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="61ecf-191">NuGet **PagedList**パッケージは、 **PagedList**パッケージを依存関係として自動的にインストールします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="61ecf-192">**PagedList**パッケージは `IQueryable` コレクションと `IEnumerable` コレクションの `PagedList` コレクション型および拡張メソッドをインストールします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="61ecf-193">拡張メソッドは、`IQueryable` または `IEnumerable`から `PagedList` コレクション内の1ページのデータを作成します。 `PagedList` コレクションには、ページングを容易にするいくつかのプロパティとメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="61ecf-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="61ecf-194">**PagedList**パッケージは、ページングボタンを表示するページングヘルパーをインストールします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="61ecf-195">**[ツール]** メニューの **[NuGet パッケージマネージャー]** をポイントし、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="61ecf-196">**パッケージマネージャーコンソール**ウィンドウで、**パッケージソース**が**nuget.org**で、**既定のプロジェクト**が**ContosoUniversity**であることを確認し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="61ecf-197">プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="61ecf-198">Index メソッドにページング機能を追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="61ecf-199">*Controllers\StudentController.cs*で、`PagedList` 名前空間の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="61ecf-200">`Index` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="61ecf-201">このコードでは、`page` パラメーター、現在の並べ替え順序パラメーター、および現在のフィルターパラメーターをメソッドシグネチャに追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="61ecf-202">ページが初めて表示されたとき、またはユーザーがページングまたは並べ替えリンクをクリックしていない場合は、すべてのパラメーターが null になります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="61ecf-203">ページングリンクがクリックされた場合、`page` 変数には、表示するページ番号が含まれます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="61ecf-204">`ViewBag` プロパティは、ページング中に並べ替え順序を同じにするためにページングリンクに含める必要があるため、ビューに現在の並べ替え順序を提供します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="61ecf-205">もう1つのプロパティである `ViewBag.CurrentFilter`は、現在のフィルター文字列を使用してビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="61ecf-206">ページング中にフィルターの設定を維持するために、ページングのリンクにこの値を含める必要があり、ページが再表示されるときに、この値をテキスト ボックスに復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="61ecf-207">ページングの中に検索文字列を変更した場合は、新しいフィルターのために別のデータが表示されるため、ページを 1 にリセットする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="61ecf-208">テキストボックスに値を入力し、[送信] ボタンを押すと、検索文字列が変更されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="61ecf-209">この場合、`searchString` パラメーターは null ではありません。</span><span class="sxs-lookup"><span data-stu-id="61ecf-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="61ecf-210">メソッドの末尾で、students `IQueryable` オブジェクトの `ToPagedList` 拡張メソッドは、ページングをサポートするコレクション型の生徒の1ページに学生クエリを変換します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="61ecf-211">これにより、学生の1つのページがビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="61ecf-212">`ToPagedList` メソッドは、ページ番号を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="61ecf-213">2つの疑問符は、 [null 合体演算子](/dotnet/csharp/language-reference/operators/null-coalescing-operator)を表します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="61ecf-214">null 合体演算子は null 許容型の既定値を定義します。式 `(page ?? 1)` は、値がある場合は `page` の値を返し、`page` が null の場合は 1 を返すことを意味します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="61ecf-215">Student インデックスビューにページングリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="61ecf-216">*Views\Student\Index.cshtml*で、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="61ecf-217">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="61ecf-218">ページの上部にある `@model` ステートメントは、ビューが `PagedList` オブジェクトの代わりに `List` オブジェクトを取得するようになったことを指定します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="61ecf-219">`PagedList.Mvc` の `using` ステートメントを使用すると、[ページング] ボタンの MVC ヘルパーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="61ecf-220">このコードでは、 [Beginform](/previous-versions/aspnet/dd492719(v=vs.108))のオーバーロードを使用して、 [Formmethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))を指定できます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="61ecf-221">既定の[Beginform](/previous-versions/aspnet/dd492719(v=vs.108))は POST を使用してフォームデータを送信します。つまり、パラメーターは URL ではなく、クエリ文字列として渡されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="61ecf-222">HTTP GET を指定すると、フォーム データがクエリ文字列として URL で渡され、ユーザーが URL をブックマークできるようになります。</span><span class="sxs-lookup"><span data-stu-id="61ecf-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="61ecf-223">[HTTP get を使用する場合の W3C ガイドライン](http://www.w3.org/2001/tag/doc/whenToUseGet.html)では、アクションによって更新されない場合に get を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="61ecf-224">テキストボックスは現在の検索文字列で初期化されるため、新しいページをクリックすると、現在の検索文字列を確認できます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="61ecf-225">列ヘッダーへのリンクは、フィルターの結果内でユーザーが並べ替えられるように、クエリ文字列を使用してコントローラーに現在の検索文字列を渡します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="61ecf-226">現在のページとページの合計数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="61ecf-227">表示するページがない場合は、"Page 0 of 0" が表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="61ecf-228">(この場合、ページ番号はページ数よりも大きくなります。 `Model.PageNumber` が1で、`Model.PageCount` が0であるためです)。</span><span class="sxs-lookup"><span data-stu-id="61ecf-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="61ecf-229">ページングボタンは `PagedListPager` ヘルパーによって表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="61ecf-230">`PagedListPager` helper には、Url やスタイルなど、カスタマイズできるさまざまなオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="61ecf-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="61ecf-231">詳細については、GitHub サイトの「 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="61ecf-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="61ecf-232">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-232">Run the page.</span></span>

   <span data-ttu-id="61ecf-233">異なる並べ替え順でページングのリンクをクリックし、ページングが機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="61ecf-234">その後で、検索文字列を入力して、ページングをもう一度試し、並べ替えとフィルター処理を使用してもページングが正しく機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="61ecf-235">About ページを作成する</span><span class="sxs-lookup"><span data-stu-id="61ecf-235">Create an About page</span></span>

<span data-ttu-id="61ecf-236">Contoso 大学の web サイトの [About] ページには、登録日ごとに登録された学生の数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="61ecf-237">これには、グループ化とグループに関する簡単な計算が必要です。</span><span class="sxs-lookup"><span data-stu-id="61ecf-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="61ecf-238">これを実行するためには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="61ecf-239">ビューに渡す必要があるデータのビュー モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="61ecf-240">`Home` コントローラーの `About` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="61ecf-241">`About` ビューを変更します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="61ecf-242">ビューモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="61ecf-242">Create the View Model</span></span>

<span data-ttu-id="61ecf-243">プロジェクトフォルダーに*viewmodel*フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="61ecf-244">そのフォルダーで、クラスファイル*EnrollmentDateGroup.cs*を追加し、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="61ecf-245">Home コントローラーを変更する</span><span class="sxs-lookup"><span data-stu-id="61ecf-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="61ecf-246">*HomeController.cs*で、ファイルの先頭に次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="61ecf-247">クラスの左中かっこの直後に、データベースコンテキストのクラス変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="61ecf-248">`About` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="61ecf-249">LINQ ステートメントは、登録日で受講者エンティティをグループ化し、各グループ内のエンティティの数を計算して、結果を `EnrollmentDateGroup` ビュー モデル オブジェクトのコレクションに格納します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="61ecf-250">`Dispose` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="61ecf-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="61ecf-251">About ビューを変更する</span><span class="sxs-lookup"><span data-stu-id="61ecf-251">Modify the About View</span></span>

1. <span data-ttu-id="61ecf-252">*Views\Home\About.cshtml*ファイルのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="61ecf-253">アプリを実行し、 **[バージョン情報]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61ecf-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="61ecf-254">登録日ごとの生徒の数がテーブルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="61ecf-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="61ecf-256">コードの入手</span><span class="sxs-lookup"><span data-stu-id="61ecf-256">Get the code</span></span>

[<span data-ttu-id="61ecf-257">完成したプロジェクトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="61ecf-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="61ecf-258">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="61ecf-258">Additional resources</span></span>

<span data-ttu-id="61ecf-259">その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="61ecf-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61ecf-260">次のステップ</span><span class="sxs-lookup"><span data-stu-id="61ecf-260">Next steps</span></span>

<span data-ttu-id="61ecf-261">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="61ecf-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61ecf-262">列の並べ替えリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-262">Add column sort links</span></span>
> * <span data-ttu-id="61ecf-263">[検索] ボックスを追加する</span><span class="sxs-lookup"><span data-stu-id="61ecf-263">Add a Search box</span></span>
> * <span data-ttu-id="61ecf-264">ページングの追加</span><span class="sxs-lookup"><span data-stu-id="61ecf-264">Add paging</span></span>
> * <span data-ttu-id="61ecf-265">About ページを作成する</span><span class="sxs-lookup"><span data-stu-id="61ecf-265">Create an About page</span></span>

<span data-ttu-id="61ecf-266">次の記事に進み、接続の回復性とコマンドインターセプトの使用方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="61ecf-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="61ecf-267">接続の回復性とコマンドのインターセプト</span><span class="sxs-lookup"><span data-stu-id="61ecf-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
