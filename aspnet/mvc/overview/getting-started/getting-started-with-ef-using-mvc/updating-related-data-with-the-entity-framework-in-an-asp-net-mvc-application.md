---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを更新する'
description: このチュートリアルでは、関連データを更新します。 ほとんどのリレーションシップでは、外部キーフィールドまたはナビゲーションプロパティを更新することによってこれを行うことができます。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499300"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="eefef-104">チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを更新する</span><span class="sxs-lookup"><span data-stu-id="eefef-104">Tutorial: Update related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="eefef-105">前のチュートリアルでは、関連データを表示しています。</span><span class="sxs-lookup"><span data-stu-id="eefef-105">In the previous tutorial you displayed related data.</span></span> <span data-ttu-id="eefef-106">このチュートリアルでは、関連データを更新します。</span><span class="sxs-lookup"><span data-stu-id="eefef-106">In this tutorial you'll update related data.</span></span> <span data-ttu-id="eefef-107">ほとんどのリレーションシップでは、外部キーフィールドまたはナビゲーションプロパティを更新することによってこれを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="eefef-107">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="eefef-108">多対多リレーションシップの場合、Entity Framework は結合テーブルを直接公開しないため、適切なナビゲーションプロパティとの間でエンティティを追加したり削除したりできます。</span><span class="sxs-lookup"><span data-stu-id="eefef-108">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="eefef-109">以下の図は、使用するページの一部を示しています。</span><span class="sxs-lookup"><span data-stu-id="eefef-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![コースでのインストラクターによる編集](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="eefef-113">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="eefef-113">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eefef-114">コースページのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="eefef-114">Customize courses pages</span></span>
> * <span data-ttu-id="eefef-115">[講師にオフィスを追加する] ページ</span><span class="sxs-lookup"><span data-stu-id="eefef-115">Add office to instructors page</span></span>
> * <span data-ttu-id="eefef-116">コースを講師ページに追加する</span><span class="sxs-lookup"><span data-stu-id="eefef-116">Add courses to instructors page</span></span>
> * <span data-ttu-id="eefef-117">DeleteConfirmed の更新</span><span class="sxs-lookup"><span data-stu-id="eefef-117">Update DeleteConfirmed</span></span>
> * <span data-ttu-id="eefef-118">オフィスの場所とコースを Create ページに追加する</span><span class="sxs-lookup"><span data-stu-id="eefef-118">Add office location and courses to the Create page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eefef-119">前提条件</span><span class="sxs-lookup"><span data-stu-id="eefef-119">Prerequisites</span></span>

* [<span data-ttu-id="eefef-120">関連データの読み取り</span><span class="sxs-lookup"><span data-stu-id="eefef-120">Reading Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a><span data-ttu-id="eefef-121">コースページのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="eefef-121">Customize courses pages</span></span>

<span data-ttu-id="eefef-122">新しいコース エンティティが作成されると、既存の部門とのリレーションシップが必要になります。</span><span class="sxs-lookup"><span data-stu-id="eefef-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="eefef-123">これを容易にするため、スキャフォールディング コードには、コントローラーのメソッドと、部門を選択するためのドロップダウン リストを含む Create ビューと Edit ビューが含まれます。</span><span class="sxs-lookup"><span data-stu-id="eefef-123">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="eefef-124">ドロップダウンリストでは、`Course.DepartmentID` の外部キープロパティが設定されます。これは、適切な `Department` エンティティを使用して `Department` ナビゲーションプロパティを読み込むために必要な Entity Framework です。</span><span class="sxs-lookup"><span data-stu-id="eefef-124">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="eefef-125">このスキャフォールディング コードを使用しますが、エラー処理を追加し、ドロップダウン リストを並べ替えるために少し変更します。</span><span class="sxs-lookup"><span data-stu-id="eefef-125">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="eefef-126">*CourseController.cs*で、4つの `Create` と `Edit` メソッドを削除し、次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eefef-126">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="eefef-127">ファイルの先頭に次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-127">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="eefef-128">`PopulateDepartmentsDropDownList` メソッドは、名前で並べ替えられたすべての部門の一覧を取得し、ドロップダウンリストの `SelectList` コレクションを作成して、`ViewBag` プロパティのビューにコレクションを渡します。</span><span class="sxs-lookup"><span data-stu-id="eefef-128">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="eefef-129">このメソッドは、ドロップダウン リストがレンダリングされるときに選択される項目を指定するためのコード呼び出しを許可する、省略可能な `selectedDepartment` パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="eefef-129">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="eefef-130">ビューでは `DepartmentID` 名前が[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)ヘルパーに渡され、ヘルパーは `DepartmentID`という名前の `SelectList` の `ViewBag` オブジェクトを検索することを認識します。</span><span class="sxs-lookup"><span data-stu-id="eefef-130">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="eefef-131">`HttpGet` `Create` メソッドは、選択された項目を設定せずに `PopulateDepartmentsDropDownList` メソッドを呼び出します。これは、新しいコースでは、部門がまだ確立されていないためです。</span><span class="sxs-lookup"><span data-stu-id="eefef-131">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="eefef-132">`HttpGet` `Edit` メソッドは、選択した項目を、編集するコースに既に割り当てられている部署の ID に基づいて設定します。</span><span class="sxs-lookup"><span data-stu-id="eefef-132">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="eefef-133">`Create` と `Edit` の両方の `HttpPost` メソッドには、エラー発生後にページを再表示するときに選択した項目を設定するコードも含まれています。</span><span class="sxs-lookup"><span data-stu-id="eefef-133">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="eefef-134">このコードにより、ページを再表示してエラーメッセージが表示されるようになり、選択した部門が選択されたままになります。</span><span class="sxs-lookup"><span data-stu-id="eefef-134">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="eefef-135">コースビューは既に department フィールドのドロップダウンリストにスキャフォールディングていますが、このフィールドには DepartmentID キャプションは必要ないので、 *Views\Course\Create.cshtml*ファイルに対して次の強調表示された変更を行い、キャプションを変更します。</span><span class="sxs-lookup"><span data-stu-id="eefef-135">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="eefef-136">*Views\Course\Edit.cshtml*で同じ変更を行います。</span><span class="sxs-lookup"><span data-stu-id="eefef-136">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="eefef-137">通常、scaffolder は、キー値がデータベースによって生成され、変更することはできず、ユーザーに表示される意味のある値ではないため、主キーをスキャフォールディングしません。</span><span class="sxs-lookup"><span data-stu-id="eefef-137">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="eefef-138">Course エンティティの場合、scaffolder には `CourseID` フィールドのテキストボックスが含まれています。これは、ユーザーが主キーの値を入力できる必要があることを `DatabaseGeneratedOption.None` 属性で認識しているためです。</span><span class="sxs-lookup"><span data-stu-id="eefef-138">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="eefef-139">しかし、数値は意味があるため、他のビューで表示することをお勧めします。そのため、手動で追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-139">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="eefef-140">*Views\Course\Edit.cshtml*で、 **[タイトル]** フィールドの前に "Course number" フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-140">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="eefef-141">これは主キーであるため、表示されますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="eefef-141">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="eefef-142">編集ビューでは、コース番号の隠しフィールド (`Html.HiddenFor` ヘルパー) が既に存在しています。</span><span class="sxs-lookup"><span data-stu-id="eefef-142">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="eefef-143">ヘルパー*の .html*を追加しても、ユーザーが 編集 ページの **保存** をクリックしたときに、ポストされたデータにコース番号が含まれないため、隠しフィールドは不要になります。</span><span class="sxs-lookup"><span data-stu-id="eefef-143">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="eefef-144">*Views\Course\Delete.cshtml*と*Views\Course\Details.cshtml*で、学科名のキャプションを "Name" から "department" に変更し、 **[タイトル]** フィールドの前に "Course number" フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-144">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="eefef-145">**[作成]** ページを実行し (コースのインデックス ページを表示し、 **[新規作成]** をクリックして)、新しいコースのデータを入力します。</span><span class="sxs-lookup"><span data-stu-id="eefef-145">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

| <span data-ttu-id="eefef-146">値</span><span class="sxs-lookup"><span data-stu-id="eefef-146">Value</span></span> | <span data-ttu-id="eefef-147">設定</span><span class="sxs-lookup"><span data-stu-id="eefef-147">Setting</span></span> |
| ----- | ------- |
| <span data-ttu-id="eefef-148">Number</span><span class="sxs-lookup"><span data-stu-id="eefef-148">Number</span></span> | <span data-ttu-id="eefef-149">「 *1000*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="eefef-149">Enter *1000*.</span></span> |
| <span data-ttu-id="eefef-150">タイトル</span><span class="sxs-lookup"><span data-stu-id="eefef-150">Title</span></span> | <span data-ttu-id="eefef-151">*代数*を入力します。</span><span class="sxs-lookup"><span data-stu-id="eefef-151">Enter *Algebra*.</span></span> |
| <span data-ttu-id="eefef-152">謝辞</span><span class="sxs-lookup"><span data-stu-id="eefef-152">Credits</span></span> | <span data-ttu-id="eefef-153">「 *4*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="eefef-153">Enter *4*.</span></span> |
|<span data-ttu-id="eefef-154">部署</span><span class="sxs-lookup"><span data-stu-id="eefef-154">Department</span></span> | <span data-ttu-id="eefef-155">**[数学]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="eefef-155">Select **Mathematics**.</span></span> |

<span data-ttu-id="eefef-156">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="eefef-156">Click **Create**.</span></span> <span data-ttu-id="eefef-157">新しいコースが一覧に追加された状態で、Course Index ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-157">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="eefef-158">Index ページのリストの部門名は、ナビゲーション プロパティから取得され、リレーションシップが正常に確立されていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="eefef-158">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="eefef-159">**編集**ページを実行します (コースのインデックスページを表示し、コースで **[編集]** をクリックします)。</span><span class="sxs-lookup"><span data-stu-id="eefef-159">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

<span data-ttu-id="eefef-160">ページ上のデータを変更し、 **[Save]\(保存\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eefef-160">Change data on the page and click **Save**.</span></span> <span data-ttu-id="eefef-161">コースデータが更新された状態で、コースのインデックスページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-161">The Course Index page is displayed with the updated course data.</span></span>

## <a name="add-office-to-instructors-page"></a><span data-ttu-id="eefef-162">[講師にオフィスを追加する] ページ</span><span class="sxs-lookup"><span data-stu-id="eefef-162">Add office to instructors page</span></span>

<span data-ttu-id="eefef-163">インストラクター レコードを編集するときに、インストラクターのオフィスの割り当ての更新が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-163">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="eefef-164">`Instructor` エンティティには、`OfficeAssignment` エンティティとの一対ゼロまたは一対一のリレーションシップがあります。つまり、次のような状況を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-164">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="eefef-165">ユーザーがオフィスの割り当てをクリアし、最初に値を持っていた場合は、`OfficeAssignment` エンティティを削除して削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-165">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="eefef-166">ユーザーがオフィスの割り当て値を入力し、最初は空だった場合は、新しい `OfficeAssignment` エンティティを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-166">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="eefef-167">ユーザーがオフィスの割り当ての値を変更した場合は、既存の `OfficeAssignment` エンティティの値を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-167">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="eefef-168">*InstructorController.cs*を開き、`HttpGet` `Edit` 方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="eefef-168">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="eefef-169">スキャフォールディングのコードは、必要なものではありません。</span><span class="sxs-lookup"><span data-stu-id="eefef-169">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="eefef-170">ドロップダウンリストのデータは設定されていますが、必要なのはテキストボックスです。</span><span class="sxs-lookup"><span data-stu-id="eefef-170">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="eefef-171">このメソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eefef-171">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="eefef-172">このコードは、`ViewBag` ステートメントを削除し、関連付けられた `OfficeAssignment` エンティティの一括読み込みを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-172">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="eefef-173">`Find` メソッドを使用して一括読み込みを実行することはできません。そのため、`Where` と `Single` のメソッドを使用してインストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="eefef-173">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="eefef-174">`HttpPost` `Edit` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eefef-174">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="eefef-175">office 割り当ての更新を処理します。</span><span class="sxs-lookup"><span data-stu-id="eefef-175">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="eefef-176">`RetryLimitExceededException` への参照には、`using` ステートメントが必要です。これを追加するには、`RetryLimitExceededException`上にマウスポインターを置きます。</span><span class="sxs-lookup"><span data-stu-id="eefef-176">The reference to `RetryLimitExceededException` requires a `using` statement; to add it - hover your mouse over `RetryLimitExceededException`.</span></span> <span data-ttu-id="eefef-177">次のメッセージが表示されます: ![ 再試行の例外メッセージ](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="eefef-177">The following message appears: ![ Retry exception message](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span></span>

<span data-ttu-id="eefef-178">**潜在的な修正プログラムの表示** を選択し、次へ を**使用**します。</span><span class="sxs-lookup"><span data-stu-id="eefef-178">Select **Show potential fixes**, then **using System.Data.Entity.Infrastructure**</span></span>

![再試行の例外を解決する](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="eefef-180">このコードは、次の処理を実行します。</span><span class="sxs-lookup"><span data-stu-id="eefef-180">The code does the following:</span></span>

- <span data-ttu-id="eefef-181">シグネチャが `HttpGet` メソッドと同じであるため、メソッド名を `EditPost` に変更します (`ActionName` 属性では、/Edit/URL が引き続き使用されていることを指定します)。</span><span class="sxs-lookup"><span data-stu-id="eefef-181">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="eefef-182">`Instructor` ナビゲーション プロパティの一括読み込みを使用して、現在の `OfficeAssignment` エンティティをデータベースから取得します。</span><span class="sxs-lookup"><span data-stu-id="eefef-182">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="eefef-183">これは、`HttpGet` `Edit` メソッドで行ったものと同じです。</span><span class="sxs-lookup"><span data-stu-id="eefef-183">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="eefef-184">モデル バインダーからの値を使用して、取得した `Instructor` エンティティを更新します。</span><span class="sxs-lookup"><span data-stu-id="eefef-184">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="eefef-185">使用する[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)オーバーロードを使用すると、含めるプロパティを*ホワイトリスト*に追加できます。</span><span class="sxs-lookup"><span data-stu-id="eefef-185">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="eefef-186">これにより、 [2 番目のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明されているように、過剰なポストを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="eefef-186">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="eefef-187">オフィスの場所が空白の場合は、`Instructor.OfficeAssignment` プロパティを null に設定して、`OfficeAssignment` テーブル内の関連する行が削除されるようにします。</span><span class="sxs-lookup"><span data-stu-id="eefef-187">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="eefef-188">データベースへの変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="eefef-188">Saves the changes to the database.</span></span>

<span data-ttu-id="eefef-189">*Views\Instructor\Edit.cshtml*で、 **[入社日]** フィールドの `div` 要素の後に、オフィスの場所を編集するための新しいフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-189">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="eefef-190">ページを実行します ([インストラクター **] タブを選択し、インストラクター**の **[編集]** をクリックします)。</span><span class="sxs-lookup"><span data-stu-id="eefef-190">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="eefef-191">**[Office Location]\(オフィスの場所\)** を変更し、 **[Save]\(保存\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eefef-191">Change the **Office Location** and click **Save**.</span></span>

## <a name="add-courses-to-instructors-page"></a><span data-ttu-id="eefef-192">コースを講師ページに追加する</span><span class="sxs-lookup"><span data-stu-id="eefef-192">Add courses to instructors page</span></span>

<span data-ttu-id="eefef-193">インストラクターは、任意の数のコースを担当する場合があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-193">Instructors may teach any number of courses.</span></span> <span data-ttu-id="eefef-194">次に、チェックボックスのグループを使用してコースの割り当てを変更する機能を追加して、インストラクターの編集ページを拡張します。</span><span class="sxs-lookup"><span data-stu-id="eefef-194">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes.</span></span>

<span data-ttu-id="eefef-195">`Course` エンティティと `Instructor` エンティティ間のリレーションシップは多対多であるため、結合テーブル内の外部キープロパティに直接アクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="eefef-195">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="eefef-196">代わりに、`Instructor.Courses` ナビゲーションプロパティからエンティティを追加および削除します。</span><span class="sxs-lookup"><span data-stu-id="eefef-196">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="eefef-197">インストラクターに割り当てられるコースを変更できるようにする UI は、チェック ボックスのグループです。</span><span class="sxs-lookup"><span data-stu-id="eefef-197">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="eefef-198">データベース内のすべてのコースのチェック ボックスが表示され、インストラクターに現在割り当てられているコースが選択されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-198">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="eefef-199">ユーザーは、チェック ボックスをオンまたはオフにしてコースの割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="eefef-199">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="eefef-200">コースの数がはるかに多い場合は、ビューにデータを表示する別の方法を使用することをお勧めしますが、リレーションシップを作成または削除するには、ナビゲーションプロパティを操作するのと同じ方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="eefef-200">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="eefef-201">チェック ボックスのリストのためにデータをビューに提供するには、ビュー モデル クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="eefef-201">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="eefef-202">*Viewmodel*フォルダーに*AssignedCourseData.cs*を作成し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eefef-202">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="eefef-203">*InstructorController.cs*で、`HttpGet` `Edit` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eefef-203">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="eefef-204">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-204">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="eefef-205">このコードは、`Courses` ナビゲーション プロパティに一括読み込みを追加し、新しい `PopulateAssignedCourseData` メソッドを呼び出して、`AssignedCourseData` ビュー モデル クラスを使用してチェック ボックス配列に情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="eefef-205">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="eefef-206">`PopulateAssignedCourseData` メソッドのコードは、ビューモデルクラスを使用してコースのリストを読み込むために、すべての `Course` エンティティを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="eefef-206">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="eefef-207">各コースに対し、コードはそのコースがインストラクターの `Courses` ナビゲーション プロパティ内に存在しているかどうかをチェックします。</span><span class="sxs-lookup"><span data-stu-id="eefef-207">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="eefef-208">コースがインストラクターに割り当てられているかどうかを確認するときに効率的な検索を作成するには、インストラクターに割り当てられたコースを[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)コレクションに含めます。</span><span class="sxs-lookup"><span data-stu-id="eefef-208">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="eefef-209">`Assigned` プロパティは、インストラクターが割り当てられているコースの `true` に設定されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-209">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="eefef-210">ビューは、このプロパティを使用して、どのチェック ボックスを選択済みとして表示する必要があるかを判断します。</span><span class="sxs-lookup"><span data-stu-id="eefef-210">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="eefef-211">最後に、リストは `ViewBag` プロパティのビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-211">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="eefef-212">次に、ユーザーが **[Save]\(保存\)** をクリックしたときに実行されるコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-212">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="eefef-213">`EditPost` メソッドを次のコードに置き換えます。このコードは、`Instructor` エンティティの `Courses` ナビゲーションプロパティを更新する新しいメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="eefef-213">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="eefef-214">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-214">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="eefef-215">メソッドシグネチャが `HttpGet` `Edit` メソッドとは異なるようになったため、メソッド名は `EditPost` から `Edit`に変更されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-215">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="eefef-216">ビューには `Course` エンティティのコレクションがないため、モデルバインダーは、`Courses` ナビゲーションプロパティを自動的に更新することはできません。</span><span class="sxs-lookup"><span data-stu-id="eefef-216">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="eefef-217">モデルバインダーを使用して `Courses` ナビゲーションプロパティを更新する代わりに、新しい `UpdateInstructorCourses` メソッドでこれを行います。</span><span class="sxs-lookup"><span data-stu-id="eefef-217">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="eefef-218">そのため、モデル バインドから `Courses` プロパティを除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-218">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="eefef-219">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)を呼び出すコードを変更する必要はありません。これは、ホワイトリスト*のオーバーロードを*使用していて、`Courses` が含まれていないためです。</span><span class="sxs-lookup"><span data-stu-id="eefef-219">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="eefef-220">チェックボックスが選択されていない場合、`UpdateInstructorCourses` のコードは、空のコレクションで `Courses` ナビゲーションプロパティを初期化します。</span><span class="sxs-lookup"><span data-stu-id="eefef-220">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="eefef-221">その後コードは、データベース内のすべてのコースをループ処理し、各コースを現在インストラクターに割り当てられているコースとビューで選択されているコースを比較してチェックします。</span><span class="sxs-lookup"><span data-stu-id="eefef-221">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="eefef-222">検索を効率化するため、最後の 2 つのコレクションが `HashSet` オブジェクトに格納されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-222">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="eefef-223">コースのチェック ボックスが選択されたが、そのコースが `Instructor.Courses`ナビゲーション プロパティにない場合、そのコースがナビゲーション プロパティ内のコレクションに追加されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-223">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="eefef-224">コースのチェック ボックスが選択さていないが、そのコースが `Instructor.Courses`ナビゲーション プロパティにある場合、そのコースがナビゲーション プロパティから削除されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-224">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="eefef-225">*Views\Instructor\Edit.cshtml*で、次のコードを `OfficeAssignment` フィールドの `div` 要素の直後、および **[保存]** ボタンの `div` 要素の前に追加して、チェックボックスの配列を含む**course フィールドを**追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-225">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="eefef-226">コードを貼り付けた後、改行やインデントがここに表示されない場合は、すべてを手動で修正して、ここに表示されているようにします。</span><span class="sxs-lookup"><span data-stu-id="eefef-226">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="eefef-227">インデントは完璧である必要はありませんが、`@</tr><tr>`、`@:<td>`、`@:</td>`、および `@</tr>` の行は、示されているようにそれぞれ 1 行にする必要があります。そうしないと、ランタイム エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="eefef-227">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="eefef-228">このコードは、3 つの列を含む HTML テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="eefef-228">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="eefef-229">各列には、チェック ボックスとその後に続くキャプションがあります。キャプションは、コース番号とタイトルから構成されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-229">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="eefef-230">すべてのチェックボックスに同じ名前 ("selectedCourses") があります。これは、グループとして扱われることをモデルバインダーに通知します。</span><span class="sxs-lookup"><span data-stu-id="eefef-230">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="eefef-231">各チェックボックスの `value` 属性は、ページがポストされるときに `CourseID.` の値に設定されます。モデルバインダーは、選択されているチェックボックスのみの `CourseID` 値で構成される配列をコントローラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="eefef-231">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="eefef-232">チェックボックスが最初に表示されたときに、インストラクターに割り当てられているコースの属性には `checked` の属性があります (チェックボックスがオンになっています)。</span><span class="sxs-lookup"><span data-stu-id="eefef-232">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="eefef-233">コースの割り当てを変更した後、サイトが `Index` ページに戻ったときに変更を確認できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-233">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="eefef-234">そのため、そのページのテーブルに列を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-234">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="eefef-235">この場合、`ViewBag` オブジェクトを使用する必要はありません。表示する情報は、モデルとしてページに渡す `Instructor` エンティティの `Courses` ナビゲーションプロパティに既に存在しているためです。</span><span class="sxs-lookup"><span data-stu-id="eefef-235">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="eefef-236">*Views\Instructor\Index.cshtml*で、次の例に示すように、 **Office**見出しの直後に**コース**見出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-236">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="eefef-237">次に、[office location detail] セルの直後に新しい詳細セルを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-237">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="eefef-238">インストラクターの**インデックス**ページを実行して、各インストラクターに割り当てられているコースを確認します。</span><span class="sxs-lookup"><span data-stu-id="eefef-238">Run the **Instructor Index** page to see the courses assigned to each instructor.</span></span>

<span data-ttu-id="eefef-239">インストラクターの **[編集]** をクリックして、編集ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="eefef-239">Click **Edit** on an instructor to see the Edit page.</span></span>

<span data-ttu-id="eefef-240">いくつかのコースの割り当てを変更し、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eefef-240">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="eefef-241">行った変更が Index ページに反映されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-241">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="eefef-242">注: インストラクターコースデータを編集するために使用する方法は、コースの数が限られている場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="eefef-242">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="eefef-243">非常に大きいコレクションの場合、別の UI と別の更新方法が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="eefef-243">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-deleteconfirmed"></a><span data-ttu-id="eefef-244">DeleteConfirmed の更新</span><span class="sxs-lookup"><span data-stu-id="eefef-244">Update DeleteConfirmed</span></span>

<span data-ttu-id="eefef-245">*InstructorController.cs*で、`DeleteConfirmed` メソッドを削除し、その場所に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="eefef-245">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="eefef-246">このコードにより、次のように変更されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-246">This code makes the following change:</span></span>

- <span data-ttu-id="eefef-247">インストラクターが任意の部門の管理者として割り当てられている場合、はその部門からインストラクターの割り当てを削除します。</span><span class="sxs-lookup"><span data-stu-id="eefef-247">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="eefef-248">このコードがないと、部門の管理者として割り当てられたインストラクターを削除しようとすると、参照整合性エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="eefef-248">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="eefef-249">このコードでは、複数の部門の管理者として割り当てられた1人のインストラクターのシナリオを処理しません。</span><span class="sxs-lookup"><span data-stu-id="eefef-249">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="eefef-250">最後のチュートリアルでは、このシナリオが発生しないようにするコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-250">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="eefef-251">オフィスの場所とコースを Create ページに追加する</span><span class="sxs-lookup"><span data-stu-id="eefef-251">Add office location and courses to the Create page</span></span>

<span data-ttu-id="eefef-252">*InstructorController.cs*で、`HttpGet` と `HttpPost` `Create` メソッドを削除し、その場所に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-252">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="eefef-253">このコードは、最初はコースが選択されていない点を除いて、Edit メソッドで見たものと似ています。</span><span class="sxs-lookup"><span data-stu-id="eefef-253">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="eefef-254">`HttpGet` `Create` メソッドは、コースが選択されている可能性がありますが、ビューの `foreach` ループに空のコレクションを提供するために、`PopulateAssignedCourseData` メソッドを呼び出します (それ以外の場合、ビューコードは null 参照例外をスローします)。</span><span class="sxs-lookup"><span data-stu-id="eefef-254">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="eefef-255">HttpPost の Create メソッドは、検証エラーをチェックし、新しいインストラクターをデータベースに追加するテンプレートコードの前に、選択した各コースを course ナビゲーションプロパティに追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-255">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="eefef-256">モデルエラーが発生した場合でもコースが追加されるので (たとえば、ユーザーが無効な日付でキーを指定した場合)、ページがエラーメッセージと共に再表示されると、実行されたすべてのコース選択が自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="eefef-256">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="eefef-257">コースを `Courses` ナビゲーション プロパティに追加できるようにするには、プロパティを空のコレクションとして初期化する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eefef-257">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="eefef-258">コントローラー コードでこれを行うための別の方法として、Instructor モデルでこれを行うことができます。このためには、プロパティ ゲッターを変更して、コレクションが存在しない場合に自動的に作成するようにします。次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="eefef-258">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="eefef-259">`Courses` プロパティをこの方法で変更する場合、コントローラー内の明示的なプロパティの初期化コードを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="eefef-259">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="eefef-260">*Views\Instructor\Create.cshtml*で、入社日] フィールドの後、 **[送信]** ボタンの前に、[オフィスの場所 テキストボックスとコースのチェックボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-260">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="eefef-261">コードを貼り付けた後、前に編集ページで行ったように、改行とインデントを修正します。</span><span class="sxs-lookup"><span data-stu-id="eefef-261">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="eefef-262">[作成] ページを実行し、インストラクターを追加します。</span><span class="sxs-lookup"><span data-stu-id="eefef-262">Run the Create page and add an instructor.</span></span>

<a id="transactions"></a>

## <a name="handling-transactions"></a><span data-ttu-id="eefef-263">トランザクションの処理</span><span class="sxs-lookup"><span data-stu-id="eefef-263">Handling transactions</span></span>

<span data-ttu-id="eefef-264">[基本的な CRUD 機能のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明したように、既定では Entity Framework はトランザクションを暗黙的に実装します。</span><span class="sxs-lookup"><span data-stu-id="eefef-264">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="eefef-265">より詳細な制御が必要なシナリオ (たとえば、トランザクションで Entity Framework 以外で行われた操作を含める場合) については、「MSDN での[トランザクション](https://msdn.microsoft.com/data/dn456843)の使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eefef-265">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="eefef-266">コードの入手</span><span class="sxs-lookup"><span data-stu-id="eefef-266">Get the code</span></span>

[<span data-ttu-id="eefef-267">完成したプロジェクトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="eefef-267">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="eefef-268">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="eefef-268">Additional resources</span></span>

<span data-ttu-id="eefef-269">その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eefef-269">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="eefef-270">次のステップ</span><span class="sxs-lookup"><span data-stu-id="eefef-270">Next step</span></span>

<span data-ttu-id="eefef-271">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="eefef-271">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eefef-272">カスタマイズしたコースページ</span><span class="sxs-lookup"><span data-stu-id="eefef-272">Customized courses pages</span></span>
> * <span data-ttu-id="eefef-273">インストラクターのページに office を追加しました</span><span class="sxs-lookup"><span data-stu-id="eefef-273">Added office to instructors page</span></span>
> * <span data-ttu-id="eefef-274">コースを講師ページに追加しました</span><span class="sxs-lookup"><span data-stu-id="eefef-274">Added courses to instructors page</span></span>
> * <span data-ttu-id="eefef-275">更新された DeleteConfirmed 確定</span><span class="sxs-lookup"><span data-stu-id="eefef-275">Updated DeleteConfirmed</span></span>
> * <span data-ttu-id="eefef-276">作成ページにオフィスの場所とコースを追加しました</span><span class="sxs-lookup"><span data-stu-id="eefef-276">Added office location and courses to the Create page</span></span>

<span data-ttu-id="eefef-277">次の記事に進み、非同期プログラミングモデルを実装する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="eefef-277">Advance to the next article to learn how to implement an asynchronous programming model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="eefef-278">非同期プログラミングモデル</span><span class="sxs-lookup"><span data-stu-id="eefef-278">Asynchronous programming model</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
