---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 4 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518284"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="7fe59-104">Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート4</span><span class="sxs-lookup"><span data-stu-id="7fe59-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>

<span data-ttu-id="7fe59-105">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7fe59-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="7fe59-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7fe59-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="7fe59-107">チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7fe59-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data"></a><span data-ttu-id="7fe59-108">関連データの操作</span><span class="sxs-lookup"><span data-stu-id="7fe59-108">Working with Related Data</span></span>

<span data-ttu-id="7fe59-109">前のチュートリアルでは、`EntityDataSource` コントロールを使用して、データのフィルター処理、並べ替え、およびグループ化を行っていました。</span><span class="sxs-lookup"><span data-stu-id="7fe59-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="7fe59-110">このチュートリアルでは、関連データを表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="7fe59-111">インストラクターの一覧を表示する講師ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="7fe59-112">インストラクターを選択すると、そのインストラクターがトレーニングしたコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="7fe59-113">コースを選択すると、コースの詳細と、コースに登録されている学生の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="7fe59-114">講師の名前、採用日、およびオフィスの割り当てを編集できます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="7fe59-115">オフィスの割り当ては、ナビゲーションプロパティを使用してアクセスする個別のエンティティセットです。</span><span class="sxs-lookup"><span data-stu-id="7fe59-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="7fe59-116">マークアップまたはコードで、マスターデータを詳細データにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="7fe59-117">チュートリアルのこの部分では、両方の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="7fe59-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="7fe59-119">GridView コントロールの関連エンティティの表示と更新</span><span class="sxs-lookup"><span data-stu-id="7fe59-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="7fe59-120">*.Master* *という名前の*新しい web ページを作成し、次のマークアップを `Content2`という名前の `Content` コントロールに追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="7fe59-121">このマークアップは、インストラクターを選択して更新を有効にする `EntityDataSource` コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="7fe59-122">`div` 要素は、後で列を追加できるように、左に表示するマークアップを構成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="7fe59-123">`EntityDataSource` マークアップと終了 `</div>` タグの間に、`GridView` コントロールを作成する次のマークアップと、エラーメッセージに使用する `Label` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="7fe59-124">この `GridView` コントロールを使用すると、行の選択が可能になり、選択した行が明るい灰色の背景色で強調表示されます。また、`SelectedIndexChanged` イベントと `Updating` イベントに対して、後で作成するハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="7fe59-125">また、`DataKeyNames` プロパティの `PersonID` を指定して、選択した行のキー値を後で追加する別のコントロールに渡すことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="7fe59-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="7fe59-126">最後の列には、インストラクターのオフィスの割り当てが含まれています。これは、関連付けられているエンティティからのものであるため、`Person` エンティティのナビゲーションプロパティに格納されています。</span><span class="sxs-lookup"><span data-stu-id="7fe59-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="7fe59-127">`EditItemTemplate` 要素は `Bind`ではなく `Eval` を指定していることに注意してください。これは、`GridView` コントロールがナビゲーションプロパティに直接バインドして更新することができないためです。</span><span class="sxs-lookup"><span data-stu-id="7fe59-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="7fe59-128">コードでオフィスの割り当てを更新します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="7fe59-129">これを行うには、`TextBox` コントロールへの参照が必要です。これを取得して、`TextBox` コントロールの `Init` イベントに保存します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="7fe59-130">`GridView` コントロールに従うことは、エラーメッセージに使用される `Label` コントロールです。</span><span class="sxs-lookup"><span data-stu-id="7fe59-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="7fe59-131">コントロールの `Visible` プロパティは `false`、ビューステートはオフになっています。これにより、エラーに応じてコードが表示される場合にのみ、ラベルが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="7fe59-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="7fe59-132">*Instructors.aspx.cs*ファイルを開き、次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="7fe59-133">[Office の割り当て] テキストボックスへの参照を保持するために、部分クラス名の宣言の直後にプライベートクラスフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="7fe59-134">後でコードを追加する `SelectedIndexChanged` イベントハンドラーのスタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="7fe59-135">また、office 割り当て `TextBox` コントロールの `Init` イベントのハンドラーを追加して、`TextBox` コントロールへの参照を格納できるようにします。</span><span class="sxs-lookup"><span data-stu-id="7fe59-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="7fe59-136">この参照を使用して、ナビゲーションプロパティに関連付けられているエンティティを更新するためにユーザーが入力した値を取得します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="7fe59-137">`GridView` コントロールの `Updating` イベントを使用して、関連付けられている `OfficeAssignment` エンティティの `Location` プロパティを更新します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="7fe59-138">`Updating` イベントに対して次のハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="7fe59-139">このコードは、ユーザーが `GridView` 行で  **Update (更新**) をクリックしたときに実行されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="7fe59-140">このコードでは、イベント引数から選択された行の `PersonID` を使用して、現在の `Person` エンティティに関連付けられている `OfficeAssignment` エンティティを取得するために LINQ to Entities を使用します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="7fe59-141">このコードは、`InstructorOfficeTextBox` コントロールの値に応じて、次のいずれかのアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="7fe59-142">テキストボックスに値があり、更新する `OfficeAssignment` エンティティがない場合は、それが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="7fe59-143">テキストボックスに値があり、`OfficeAssignment` エンティティがある場合は、`Location` プロパティ値が更新されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="7fe59-144">テキストボックスが空で `OfficeAssignment` エンティティが存在する場合は、エンティティが削除されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="7fe59-145">その後、変更内容がデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="7fe59-146">例外が発生した場合は、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="7fe59-147">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-147">Run the page.</span></span>

<span data-ttu-id="7fe59-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="7fe59-149">**[編集]** をクリックすると、すべてのフィールドがテキストボックスに変わります。</span><span class="sxs-lookup"><span data-stu-id="7fe59-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="7fe59-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="7fe59-151">**Office の割り当て**など、これらの値のいずれかを変更します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="7fe59-152">**[更新]** をクリックすると、一覧に反映された変更が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="7fe59-153">別のコントロールでの関連エンティティの表示</span><span class="sxs-lookup"><span data-stu-id="7fe59-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="7fe59-154">各インストラクターは1つまたは複数のコースを教えることができるので、`EntityDataSource` コントロールと `GridView` コントロールを追加して、インストラクター `GridView` コントロールで選択されているインストラクターに関連するコースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="7fe59-155">Course エンティティの見出しと `EntityDataSource` コントロールを作成するには、エラーメッセージ `Label` コントロールと終了 `</div>` タグの間に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="7fe59-156">`Where` パラメーターには、`InstructorsGridView` コントロールで行が選択されているインストラクターの `PersonID` の値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7fe59-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="7fe59-157">`Where` プロパティには、`Course` エンティティの `People` ナビゲーションプロパティから関連付けられているすべての `Person` エンティティを取得し、関連付けられているいずれかの `Course` エンティティに選択した `Person` 値が含まれている場合にのみ、`PersonID` エンティティを選択するサブセレクトコマンドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7fe59-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="7fe59-158">`GridView` コントロールを作成するには、`CoursesEntityDataSource` コントロールの直後 (終了 `</div>` タグの前) に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="7fe59-159">インストラクターが選択されていない場合はコースが表示されないため、`EmptyDataTemplate` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="7fe59-160">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-160">Run the page.</span></span>

<span data-ttu-id="7fe59-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="7fe59-162">1つ以上のコースが割り当てられているインストラクターを選択すると、コースやコースが一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="7fe59-163">(注: データベーススキーマでは複数のコースが許可されていますが、データベースに用意されているテストデータでは、インストラクターには複数のコースがありません。</span><span class="sxs-lookup"><span data-stu-id="7fe59-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="7fe59-164">**サーバーエクスプローラー**ウィンドウまたは*CoursesAdd*ページを使用して、データベースにコースを追加できます。このページは、後のチュートリアルで追加します)。</span><span class="sxs-lookup"><span data-stu-id="7fe59-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="7fe59-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="7fe59-166">`CoursesGridView` コントロールには、いくつかのコースフィールドのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="7fe59-167">コースの詳細をすべて表示するには、ユーザーが選択したコースに対して `DetailsView` コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="7fe59-168">*講師*の `</div>` タグの後に、次のマークアップを追加します (このマークアップは、終了 div タグの**後**に配置してください)。</span><span class="sxs-lookup"><span data-stu-id="7fe59-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="7fe59-169">このマークアップは、`Courses` エンティティセットにバインドされている `EntityDataSource` コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="7fe59-170">`Where` プロパティは、コース `GridView` コントロールで選択された行の `CourseID` 値を使用してコースを選択します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="7fe59-171">マークアップは `Selected` イベントのハンドラーを指定します。これは、階層内の別のレベルである学生の成績を表示するために後で使用します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="7fe59-172">*Instructors.aspx.cs*で、`CourseDetailsEntityDataSource_Selected` メソッドに対して次のスタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="7fe59-173">(このスタブは、このチュートリアルで後ほど説明します。ここでは、ページをコンパイルして実行するために必要になります)。</span><span class="sxs-lookup"><span data-stu-id="7fe59-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="7fe59-174">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-174">Run the page.</span></span>

<span data-ttu-id="7fe59-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="7fe59-176">コースが選択されていないため、最初はコースの詳細はありません。</span><span class="sxs-lookup"><span data-stu-id="7fe59-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="7fe59-177">コースが割り当てられているインストラクターを選択し、コースを選択して詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="7fe59-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="7fe59-179">EntityDataSource "Selected" イベントを使用して関連データを表示する</span><span class="sxs-lookup"><span data-stu-id="7fe59-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="7fe59-180">最後に、選択したコースのすべての登録済み学生とその成績を表示します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="7fe59-181">これを行うには、コース `DetailsView`にバインドされている `EntityDataSource` コントロールの `Selected` イベントを使用します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="7fe59-182">*講師*の `DetailsView` コントロールの後に、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="7fe59-183">このマークアップは、選択したコースの学生とその成績のリストを表示する `ListView` コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="7fe59-184">コントロールをコードにバインドするため、データソースは指定されません。</span><span class="sxs-lookup"><span data-stu-id="7fe59-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="7fe59-185">`EmptyDataTemplate` 要素は、コースが選択されていないときに表示するメッセージを提供します。この場合、表示する学生は存在しません。</span><span class="sxs-lookup"><span data-stu-id="7fe59-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="7fe59-186">`LayoutTemplate` 要素は、リストを表示するための HTML テーブルを作成し、`ItemTemplate` は表示する列を指定します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="7fe59-187">学生 ID と学生の成績は `StudentGrade` エンティティからのもので、学生名は、Entity Framework が `StudentGrade` エンティティの `Person` ナビゲーションプロパティで使用できる `Person` エンティティからのものです。</span><span class="sxs-lookup"><span data-stu-id="7fe59-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="7fe59-188">*Instructors.aspx.cs*で、スタブアウト `CourseDetailsEntityDataSource_Selected` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7fe59-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="7fe59-189">このイベントのイベント引数は、選択されたデータをコレクションの形式で提供します。これは、何も選択されていない場合、または `Course` エンティティが選択されている場合に1つの項目がある場合に、項目が0になります。</span><span class="sxs-lookup"><span data-stu-id="7fe59-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="7fe59-190">`Course` エンティティが選択されている場合、コードは、`First` メソッドを使用してコレクションを単一のオブジェクトに変換します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="7fe59-191">次に、ナビゲーションプロパティから `StudentGrade` エンティティを取得し、コレクションに変換して、`GradesListView` コントロールをコレクションにバインドします。</span><span class="sxs-lookup"><span data-stu-id="7fe59-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="7fe59-192">これで成績を表示できますが、最初にページが表示されたときと、コースが選択されていないときに、空のデータテンプレート内のメッセージが表示されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7fe59-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="7fe59-193">これを行うには、次の2つの場所から呼び出すメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="7fe59-194">ページを初めて表示するときに空のデータテンプレートを表示するには、`Page_Load` メソッドからこの新しいメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="7fe59-195">また、インストラクターが選択されたときにそのイベントが発生するので、`InstructorsGridView_SelectedIndexChanged` メソッドから呼び出します。これは、新しいコースがコース `GridView` コントロールに読み込まれ、何も選択されていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="7fe59-196">2つの呼び出しを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="7fe59-197">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-197">Run the page.</span></span>

<span data-ttu-id="7fe59-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="7fe59-199">コースが割り当てられているインストラクターを選択し、コースを選択します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="7fe59-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="7fe59-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="7fe59-201">これで、関連データを操作するいくつかの方法が見られました。</span><span class="sxs-lookup"><span data-stu-id="7fe59-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="7fe59-202">次のチュートリアルでは、既存のエンティティ間のリレーションシップを追加する方法、リレーションシップを削除する方法、既存のエンティティとのリレーションシップを持つ新しいエンティティを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7fe59-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7fe59-203">[前へ](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="7fe59-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
