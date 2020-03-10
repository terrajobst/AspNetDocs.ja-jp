---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 3: 並べ替えとフィルター |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512716"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="724b1-104">Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 3: 並べ替えとフィルター処理</span><span class="sxs-lookup"><span data-stu-id="724b1-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="724b1-105">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="724b1-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="724b1-106">このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](https://asp.net/entity-framework/tutorials#Getting%20Started)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="724b1-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="724b1-107">前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。</span><span class="sxs-lookup"><span data-stu-id="724b1-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="724b1-108">チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。</span><span class="sxs-lookup"><span data-stu-id="724b1-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="724b1-109">チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。</span><span class="sxs-lookup"><span data-stu-id="724b1-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="724b1-110">前のチュートリアルでは、Entity Framework と `ObjectDataSource` コントロールを使用する n 層 web アプリケーションにリポジトリパターンを実装しました。</span><span class="sxs-lookup"><span data-stu-id="724b1-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="724b1-111">このチュートリアルでは、並べ替えとフィルター処理を行い、マスタ詳細シナリオを処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="724b1-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="724b1-112">次の拡張機能を department *.aspx*ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="724b1-113">ユーザーが名前で部門を選択できるようにするテキストボックス。</span><span class="sxs-lookup"><span data-stu-id="724b1-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="724b1-114">グリッドに表示される各部署のコースの一覧。</span><span class="sxs-lookup"><span data-stu-id="724b1-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="724b1-115">列見出しをクリックして並べ替えることができます。</span><span class="sxs-lookup"><span data-stu-id="724b1-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="724b1-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="724b1-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="724b1-117">GridView 列を並べ替える機能の追加</span><span class="sxs-lookup"><span data-stu-id="724b1-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="724b1-118">Department ページ*を開き、`DepartmentsObjectDataSource`* という名前の `ObjectDataSource` コントロールに `SortParameterName="sortExpression"` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="724b1-119">(後で `sortExpression`という名前のパラメーターを受け取る `GetDepartments` メソッドを作成します)。コントロールの開始タグのマークアップは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="724b1-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="724b1-120">`GridView` コントロールの開始タグに `AllowSorting="true"` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="724b1-121">コントロールの開始タグのマークアップは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="724b1-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="724b1-122">*Departments.aspx.cs*で、`Page_Load` メソッドから `GridView` コントロールの `Sort` メソッドを呼び出すことによって、既定の並べ替え順序を設定します。</span><span class="sxs-lookup"><span data-stu-id="724b1-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="724b1-123">ビジネスロジッククラスまたはリポジトリクラスで並べ替えまたはフィルター処理を行うコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="724b1-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="724b1-124">ビジネスロジッククラスでこれを行う場合は、データがデータベースから取得された後に並べ替えまたはフィルター処理が行われます。これは、ビジネスロジッククラスがリポジトリによって返された `IEnumerable` オブジェクトを操作しているためです。</span><span class="sxs-lookup"><span data-stu-id="724b1-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="724b1-125">リポジトリクラスに並べ替えとフィルター処理のコードを追加し、LINQ 式またはオブジェクトのクエリを `IEnumerable` オブジェクトに変換する前に、この操作を実行すると、コマンドが処理のためにデータベースに渡されます。これは通常、より効率的です。</span><span class="sxs-lookup"><span data-stu-id="724b1-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="724b1-126">このチュートリアルでは、データベース (つまり、リポジトリ) によって処理が実行されるように、並べ替えとフィルター処理を実装します。</span><span class="sxs-lookup"><span data-stu-id="724b1-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="724b1-127">並べ替え機能を追加するには、リポジトリインターフェイスおよびリポジトリクラスに加えて、ビジネスロジッククラスに新しいメソッドを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="724b1-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="724b1-128">*ISchoolRepository.cs*ファイルに、返された部門の一覧の並べ替えに使用される `sortExpression` パラメーターを受け取る新しい `GetDepartments` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="724b1-129">`sortExpression` パラメーターでは、並べ替える列と並べ替えの方向を指定します。</span><span class="sxs-lookup"><span data-stu-id="724b1-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="724b1-130">新しいメソッドのコードを*SchoolRepository.cs*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="724b1-131">新しいメソッドを呼び出すように、既存のパラメーターなしの `GetDepartments` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="724b1-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="724b1-132">テストプロジェクトで、次の新しいメソッドを*MockSchoolRepository.cs*に追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="724b1-133">このメソッドに依存し、並べ替えられたリストを返す単体テストを作成する場合は、リストを返す前に並べ替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="724b1-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="724b1-134">このチュートリアルでは、このようなテストを作成するのではなく、並べ替えられていない部署のリストを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="724b1-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="724b1-135">*SchoolBL.cs*ファイルで、ビジネスロジッククラスに次の新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="724b1-136">このコードは、sort パラメーターを repository メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="724b1-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="724b1-137">Department *. .aspx*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="724b1-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="724b1-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="724b1-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="724b1-139">列見出しをクリックすると、その列で並べ替えることができるようになります。</span><span class="sxs-lookup"><span data-stu-id="724b1-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="724b1-140">列が既に並べ替えられている場合は、見出しをクリックすると並べ替えの方向が反転します。</span><span class="sxs-lookup"><span data-stu-id="724b1-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="724b1-141">検索ボックスの追加</span><span class="sxs-lookup"><span data-stu-id="724b1-141">Adding a Search Box</span></span>

<span data-ttu-id="724b1-142">このセクションでは、検索テキストボックスを追加し、コントロールパラメーターを使用して `ObjectDataSource` コントロールにリンクします。また、ビジネスロジッククラスにメソッドを追加して、フィルター処理をサポートします。</span><span class="sxs-lookup"><span data-stu-id="724b1-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="724b1-143">Department *.aspx*ページを開き、見出しと最初の `ObjectDataSource` コントロールの間に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="724b1-144">`DepartmentsObjectDataSource`という名前の `ObjectDataSource` コントロールで、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="724b1-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="724b1-145">`SearchTextBox` コントロールに入力された値を取得する `nameSearchString` という名前のパラメーターの `SelectParameters` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="724b1-146">`SelectMethod` 属性の値を `GetDepartmentsByName`に変更します。</span><span class="sxs-lookup"><span data-stu-id="724b1-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="724b1-147">(後でこのメソッドを作成します)。</span><span class="sxs-lookup"><span data-stu-id="724b1-147">(You'll create this method later.)</span></span>

<span data-ttu-id="724b1-148">`ObjectDataSource` コントロールのマークアップは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="724b1-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="724b1-149">*ISchoolRepository.cs*で、`sortExpression` と `nameSearchString` の両方のパラメーターを受け取る `GetDepartmentsByName` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="724b1-150">*SchoolRepository.cs*で、次の新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="724b1-151">このコードでは、`Where` メソッドを使用して、検索文字列を含む項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="724b1-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="724b1-152">検索文字列が空の場合は、すべてのレコードが選択されます。</span><span class="sxs-lookup"><span data-stu-id="724b1-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="724b1-153">メソッド呼び出しを、このような1つのステートメント (`Include`、`OrderBy`、`Where`) のように指定する場合、`Where` メソッドは常に最後にある必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="724b1-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="724b1-154">新しいメソッドを呼び出すために `sortExpression` パラメーターを受け取る既存の `GetDepartments` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="724b1-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="724b1-155">テストプロジェクトの*MockSchoolRepository.cs*に、次の新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="724b1-156">*SchoolBL.cs*で、次の新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="724b1-157">Department *.aspx*ページを実行し、検索文字列を入力して、選択ロジックが動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="724b1-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="724b1-158">テキストボックスを空のままにして、すべてのレコードが返されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="724b1-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="724b1-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="724b1-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="724b1-160">各グリッド行の詳細列の追加</span><span class="sxs-lookup"><span data-stu-id="724b1-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="724b1-161">次に、グリッドの右側のセルに表示される各部門のすべてのコースを確認します。</span><span class="sxs-lookup"><span data-stu-id="724b1-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="724b1-162">これを行うには、入れ子になった `GridView` コントロールを使用し、`Department` エンティティの `Courses` ナビゲーションプロパティからデータにデータをバインドします。</span><span class="sxs-lookup"><span data-stu-id="724b1-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="724b1-163">Department *.aspx*を開き、`GridView` コントロールのマークアップで、`RowDataBound` イベントのハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="724b1-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="724b1-164">コントロールの開始タグのマークアップは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="724b1-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="724b1-165">`Administrator` テンプレートフィールドの後に新しい `TemplateField` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="724b1-166">このマークアップは、コースの一覧のコース番号とタイトルを表示する、入れ子になった `GridView` コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="724b1-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="724b1-167">`RowDataBound` ハンドラーのコードにデータソースをバインドするので、データソースは指定しません。</span><span class="sxs-lookup"><span data-stu-id="724b1-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="724b1-168">*Departments.aspx.cs*を開き、`RowDataBound` イベントの次のハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="724b1-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="724b1-169">このコードは、イベント引数から `Department` エンティティを取得し、`Courses` ナビゲーションプロパティを `List` コレクションに変換して、入れ子になった `GridView` をコレクションにバインドします。</span><span class="sxs-lookup"><span data-stu-id="724b1-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="724b1-170">*SchoolRepository.cs*ファイルを開き、`GetDepartmentsByName` メソッドで作成したオブジェクトクエリで `Include` メソッドを呼び出して、`Courses` ナビゲーションプロパティの一括読み込みを指定します。</span><span class="sxs-lookup"><span data-stu-id="724b1-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="724b1-171">`GetDepartmentsByName` メソッドの `return` ステートメントは、次の例のようになりました。</span><span class="sxs-lookup"><span data-stu-id="724b1-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="724b1-172">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="724b1-172">Run the page.</span></span> <span data-ttu-id="724b1-173">前に追加した並べ替えとフィルター処理の機能に加えて、GridView コントロールには、各部門の入れ子になったコースの詳細が表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="724b1-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="724b1-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="724b1-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="724b1-175">これで、並べ替え、フィルター処理、およびマスタ詳細シナリオの概要が完成します。</span><span class="sxs-lookup"><span data-stu-id="724b1-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="724b1-176">次のチュートリアルでは、同時実行を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="724b1-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="724b1-177">[前へ](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [次へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="724b1-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
