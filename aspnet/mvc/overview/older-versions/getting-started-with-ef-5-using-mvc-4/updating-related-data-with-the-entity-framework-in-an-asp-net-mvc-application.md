---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの更新 (6/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468286"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="2d38f-103">ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの更新 (6/10)</span><span class="sxs-lookup"><span data-stu-id="2d38f-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>

<span data-ttu-id="2d38f-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2d38f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="2d38f-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="2d38f-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="2d38f-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="2d38f-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d38f-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="2d38f-108">チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="2d38f-109">解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。</span><span class="sxs-lookup"><span data-stu-id="2d38f-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="2d38f-110">一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="2d38f-111">一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d38f-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="2d38f-112">前のチュートリアルでは、関連データを表示していました。このチュートリアルでは、関連データを更新します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="2d38f-113">ほとんどのリレーションシップでは、適切な外部キーフィールドを更新することによってこれを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="2d38f-114">多対多リレーションシップの場合、Entity Framework は結合テーブルを直接公開しないため、適切なナビゲーションプロパティとの間でエンティティを明示的に追加および削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="2d38f-115">以下の図は、使用するページを示しています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="2d38f-118">Courses の Create ページと Edit ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="2d38f-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="2d38f-119">新しいコース エンティティが作成されると、既存の部門とのリレーションシップが必要になります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="2d38f-120">これを容易にするため、スキャフォールディング コードには、コントローラーのメソッドと、部門を選択するためのドロップダウン リストを含む Create ビューと Edit ビューが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="2d38f-121">ドロップダウンリストでは、`Course.DepartmentID` の外部キープロパティが設定されます。これは、適切な `Department` エンティティを使用して `Department` ナビゲーションプロパティを読み込むために必要な Entity Framework です。</span><span class="sxs-lookup"><span data-stu-id="2d38f-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="2d38f-122">このスキャフォールディング コードを使用しますが、エラー処理を追加し、ドロップダウン リストを並べ替えるために少し変更します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="2d38f-123">*CourseController.cs*で、4つの `Edit` と `Create` メソッドを削除し、次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="2d38f-124">`PopulateDepartmentsDropDownList` メソッドは、名前で並べ替えられたすべての部門の一覧を取得し、ドロップダウンリストの `SelectList` コレクションを作成して、`ViewBag` プロパティのビューにコレクションを渡します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="2d38f-125">このメソッドは、ドロップダウン リストがレンダリングされるときに選択される項目を指定するためのコード呼び出しを許可する、省略可能な `selectedDepartment` パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="2d38f-126">ビューは `DepartmentID` 名前を[`DropDownList` ヘルパー](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)に渡し、ヘルパーは `DepartmentID`という名前の `SelectList` の `ViewBag` オブジェクトを検索することを認識します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="2d38f-127">`HttpGet` `Create` メソッドは、選択された項目を設定せずに `PopulateDepartmentsDropDownList` メソッドを呼び出します。これは、新しいコースでは、部門がまだ確立されていないためです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="2d38f-128">`HttpGet` `Edit` メソッドは、選択した項目を、編集するコースに既に割り当てられている部署の ID に基づいて設定します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="2d38f-129">`Create` と `Edit` の両方の `HttpPost` メソッドには、エラー発生後にページを再表示するときに選択した項目を設定するコードも含まれています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="2d38f-130">このコードにより、ページを再表示してエラーメッセージが表示されるようになり、選択した部門が選択されたままになります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="2d38f-131">*Views\Course\Create.cshtml*で、強調表示されたコードを追加して、 **[タイトル]** フィールドの前に新しい "Course number" フィールドを作成します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="2d38f-132">前のチュートリアルで説明したように、主キーフィールドは既定ではスキャフォールディングませんが、この主キーは意味があるため、ユーザーがキー値を入力できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="2d38f-133">*Views\Course\Edit.cshtml*、 *Views\Course\Delete.cshtml*、および*Views\Course\Details.cshtml*で、 **Title**フィールドの前に "Course number" フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="2d38f-134">これは主キーであるため、表示されますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="2d38f-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="2d38f-135">**[作成]** ページを実行し (コースのインデックス ページを表示し、 **[新規作成]** をクリックして)、新しいコースのデータを入力します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="2d38f-137">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="2d38f-137">Click **Create**.</span></span> <span data-ttu-id="2d38f-138">新しいコースが一覧に追加された状態で、Course Index ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="2d38f-139">Index ページのリストの部門名は、ナビゲーション プロパティから取得され、リレーションシップが正常に確立されていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="2d38f-141">**編集**ページを実行します (コースのインデックスページを表示し、コースで **[編集]** をクリックします)。</span><span class="sxs-lookup"><span data-stu-id="2d38f-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="2d38f-143">ページ上のデータを変更し、 **[Save]\(保存\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="2d38f-144">コースデータが更新された状態で、コースのインデックスページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="2d38f-145">インストラクターの編集ページを追加する</span><span class="sxs-lookup"><span data-stu-id="2d38f-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="2d38f-146">インストラクター レコードを編集するときに、インストラクターのオフィスの割り当ての更新が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="2d38f-147">`Instructor` エンティティには、`OfficeAssignment` エンティティとの一対ゼロまたは一対一のリレーションシップがあります。つまり、次のような状況を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="2d38f-148">ユーザーがオフィスの割り当てをクリアし、最初に値を持っていた場合は、`OfficeAssignment` エンティティを削除して削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="2d38f-149">ユーザーがオフィスの割り当て値を入力し、最初は空だった場合は、新しい `OfficeAssignment` エンティティを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="2d38f-150">ユーザーがオフィスの割り当ての値を変更した場合は、既存の `OfficeAssignment` エンティティの値を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="2d38f-151">*InstructorController.cs*を開き、`HttpGet` `Edit` 方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="2d38f-152">スキャフォールディングのコードは、必要なものではありません。</span><span class="sxs-lookup"><span data-stu-id="2d38f-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="2d38f-153">ドロップダウンリストのデータは設定されていますが、必要なのはテキストボックスです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="2d38f-154">このメソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="2d38f-155">このコードは、`ViewBag` ステートメントを削除し、関連付けられた `OfficeAssignment` エンティティの一括読み込みを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="2d38f-156">`Find` メソッドを使用して一括読み込みを実行することはできません。そのため、`Where` と `Single` のメソッドを使用してインストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="2d38f-157">`HttpPost` `Edit` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="2d38f-158">office 割り当ての更新を処理します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="2d38f-159">このコードは、次の処理を実行します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-159">The code does the following:</span></span>

- <span data-ttu-id="2d38f-160">`Instructor` ナビゲーション プロパティの一括読み込みを使用して、現在の `OfficeAssignment` エンティティをデータベースから取得します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="2d38f-161">これは、`HttpGet` `Edit` メソッドで行ったものと同じです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="2d38f-162">モデル バインダーからの値を使用して、取得した `Instructor` エンティティを更新します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="2d38f-163">使用する[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)オーバーロードを使用すると、含めるプロパティを*ホワイトリスト*に追加できます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="2d38f-164">これにより、 [2 番目のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明されているように、過剰なポストを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="2d38f-165">オフィスの場所が空白の場合は、`Instructor.OfficeAssignment` プロパティを null に設定して、`OfficeAssignment` テーブル内の関連する行が削除されるようにします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="2d38f-166">データベースへの変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-166">Saves the changes to the database.</span></span>

<span data-ttu-id="2d38f-167">*Views\Instructor\Edit.cshtml*で、 **[入社日]** フィールドの `div` 要素の後に、オフィスの場所を編集するための新しいフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="2d38f-168">ページを実行します ([インストラクター **] タブを選択し、インストラクター**の **[編集]** をクリックします)。</span><span class="sxs-lookup"><span data-stu-id="2d38f-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="2d38f-169">**[Office Location]\(オフィスの場所\)** を変更し、 **[Save]\(保存\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="2d38f-171">インストラクターの編集ページにコースの割り当てを追加する</span><span class="sxs-lookup"><span data-stu-id="2d38f-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="2d38f-172">インストラクターは、任意の数のコースを担当する場合があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="2d38f-173">次のスクリーン ショットに示すように、チェック ボックスのグループを使用して、コースの割り当てを変更する機能を追加して、Instructor/Edit ページを拡張します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="2d38f-175">`Course` エンティティと `Instructor` エンティティ間のリレーションシップは多対多であるため、結合テーブルに直接アクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="2d38f-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="2d38f-176">代わりに、`Instructor.Courses` ナビゲーションプロパティからエンティティを追加および削除します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="2d38f-177">インストラクターに割り当てられるコースを変更できるようにする UI は、チェック ボックスのグループです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="2d38f-178">データベース内のすべてのコースのチェック ボックスが表示され、インストラクターに現在割り当てられているコースが選択されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="2d38f-179">ユーザーは、チェック ボックスをオンまたはオフにしてコースの割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="2d38f-180">コースの数がはるかに多い場合は、ビューにデータを表示する別の方法を使用することをお勧めしますが、リレーションシップを作成または削除するには、ナビゲーションプロパティを操作するのと同じ方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="2d38f-181">チェック ボックスのリストのためにデータをビューに提供するには、ビュー モデル クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="2d38f-182">*Viewmodel*フォルダーに*AssignedCourseData.cs*を作成し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="2d38f-183">*InstructorController.cs*で、`HttpGet` `Edit` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="2d38f-184">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="2d38f-185">このコードは、`Courses` ナビゲーション プロパティに一括読み込みを追加し、新しい `PopulateAssignedCourseData` メソッドを呼び出して、`AssignedCourseData` ビュー モデル クラスを使用してチェック ボックス配列に情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="2d38f-186">`PopulateAssignedCourseData` メソッドのコードは、ビューモデルクラスを使用してコースのリストを読み込むために、すべての `Course` エンティティを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="2d38f-187">各コースに対し、コードはそのコースがインストラクターの `Courses` ナビゲーション プロパティ内に存在しているかどうかをチェックします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="2d38f-188">コースがインストラクターに割り当てられているかどうかを確認するときに効率的な検索を作成するには、インストラクターに割り当てられたコースを[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)コレクションに含めます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="2d38f-189">`Assigned` プロパティは、インストラクターが割り当てられているコースの `true` に設定されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="2d38f-190">ビューは、このプロパティを使用して、どのチェック ボックスを選択済みとして表示する必要があるかを判断します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="2d38f-191">最後に、リストは `ViewBag` プロパティのビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="2d38f-192">次に、ユーザーが **[Save]\(保存\)** をクリックしたときに実行されるコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="2d38f-193">`HttpPost` `Edit` メソッドを次のコードに置き換えます。このコードは、`Instructor` エンティティの `Courses` ナビゲーションプロパティを更新する新しいメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="2d38f-194">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="2d38f-195">ビューには `Course` エンティティのコレクションがないため、モデルバインダーは、`Courses` ナビゲーションプロパティを自動的に更新することはできません。</span><span class="sxs-lookup"><span data-stu-id="2d38f-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="2d38f-196">モデルバインダーを使用して course ナビゲーションプロパティを更新するのではなく、新しい `UpdateInstructorCourses` メソッドで作成します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="2d38f-197">そのため、モデル バインドから `Courses` プロパティを除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="2d38f-198">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)を呼び出すコードを変更する必要はありません。これは、ホワイトリスト*のオーバーロードを*使用していて、`Courses` が含まれていないためです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="2d38f-199">チェックボックスが選択されていない場合、`UpdateInstructorCourses` のコードは、空のコレクションで `Courses` ナビゲーションプロパティを初期化します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="2d38f-200">その後コードは、データベース内のすべてのコースをループ処理し、各コースを現在インストラクターに割り当てられているコースとビューで選択されているコースを比較してチェックします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="2d38f-201">検索を効率化するため、最後の 2 つのコレクションが `HashSet` オブジェクトに格納されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="2d38f-202">コースのチェック ボックスが選択されたが、そのコースが `Instructor.Courses`ナビゲーション プロパティにない場合、そのコースがナビゲーション プロパティ内のコレクションに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="2d38f-203">コースのチェック ボックスが選択さていないが、そのコースが `Instructor.Courses`ナビゲーション プロパティにある場合、そのコースがナビゲーション プロパティから削除されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="2d38f-204">*Views\Instructor\Edit.cshtml*で、次の強調表示されたコードを `OfficeAssignment` フィールドの `div` 要素の直後に追加して、チェックボックスの配列を含む**course フィールドを**追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="2d38f-205">このコードは、3 つの列を含む HTML テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="2d38f-206">各列には、チェック ボックスとその後に続くキャプションがあります。キャプションは、コース番号とタイトルから構成されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="2d38f-207">すべてのチェックボックスに同じ名前 ("selectedCourses") があります。これは、グループとして扱われることをモデルバインダーに通知します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="2d38f-208">各チェックボックスの `value` 属性は、ページがポストされるときに `CourseID.` の値に設定されます。モデルバインダーは、選択されているチェックボックスのみの `CourseID` 値で構成される配列をコントローラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="2d38f-209">チェックボックスが最初に表示されたときに、インストラクターに割り当てられているコースの属性には `checked` の属性があります (チェックボックスがオンになっています)。</span><span class="sxs-lookup"><span data-stu-id="2d38f-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="2d38f-210">コースの割り当てを変更した後、サイトが `Index` ページに戻ったときに変更を確認できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="2d38f-211">そのため、そのページのテーブルに列を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="2d38f-212">この場合、`ViewBag` オブジェクトを使用する必要はありません。表示する情報は、モデルとしてページに渡す `Instructor` エンティティの `Courses` ナビゲーションプロパティに既に存在しているためです。</span><span class="sxs-lookup"><span data-stu-id="2d38f-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="2d38f-213">*Views\Instructor\Index.cshtml*で、次の例に示すように、 **Office**見出しの直後に**コース**見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="2d38f-214">次に、[office location detail] セルの直後に新しい詳細セルを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="2d38f-215">インストラクターの**インデックス**ページを実行して、各インストラクターに割り当てられているコースを確認します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="2d38f-217">インストラクターの **[編集]** をクリックして、編集ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="2d38f-219">いくつかのコースの割り当てを変更し、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="2d38f-220">行った変更が Index ページに反映されます。</span><span class="sxs-lookup"><span data-stu-id="2d38f-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="2d38f-221">注: インストラクターコースデータを編集する方法は、コースの数が限られている場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="2d38f-222">非常に大きいコレクションの場合、別の UI と別の更新方法が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2d38f-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  

## <a name="update-the-delete-method"></a><span data-ttu-id="2d38f-223">Delete メソッドを更新する</span><span class="sxs-lookup"><span data-stu-id="2d38f-223">Update the Delete Method</span></span>

<span data-ttu-id="2d38f-224">次のように、HttpPost Delete メソッドのコードを変更して、講師が削除されたときに office 割り当てレコード (存在する場合) が削除されるようにします。</span><span class="sxs-lookup"><span data-stu-id="2d38f-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

<span data-ttu-id="2d38f-225">管理者として部門に割り当てられているインストラクターを削除しようとすると、参照整合性エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="2d38f-226">インストラクターが管理者として割り当てられている任意の部門からインストラクターを自動的に削除するその他のコードについては[、このチュートリアルの現在のバージョン](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d38f-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="2d38f-227">まとめ</span><span class="sxs-lookup"><span data-stu-id="2d38f-227">Summary</span></span>

<span data-ttu-id="2d38f-228">これで、関連データの操作の概要が完了しました。</span><span class="sxs-lookup"><span data-stu-id="2d38f-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="2d38f-229">ここまでのチュートリアルでは、さまざまな CRUD 操作を行ってきましたが、同時実行の問題については扱いませんでした。</span><span class="sxs-lookup"><span data-stu-id="2d38f-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="2d38f-230">次のチュートリアルでは、同時実行のトピックを紹介し、それを処理するためのオプションについて説明し、1つのエンティティ型に対して既に記述した CRUD コードに同時実行処理を追加します。</span><span class="sxs-lookup"><span data-stu-id="2d38f-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="2d38f-231">その他の Entity Framework リソースへのリンクについては、[このシリーズの最後のチュートリアル](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)の最後に記載されています。</span><span class="sxs-lookup"><span data-stu-id="2d38f-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2d38f-232">[前へ](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="2d38f-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
