---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: モデルバインドと web フォームを使用したデータの更新、削除、および作成 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474136"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="d543f-104">モデルバインドと web フォームを使用したデータの更新、削除、および作成</span><span class="sxs-lookup"><span data-stu-id="d543f-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="d543f-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d543f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d543f-106">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="d543f-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="d543f-107">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="d543f-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="d543f-108">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="d543f-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="d543f-109">このチュートリアルでは、モデルバインディングを使用してデータを作成、更新、および削除する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d543f-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="d543f-110">次のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="d543f-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="d543f-111">DeleteMethod</span></span>
> - <span data-ttu-id="d543f-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="d543f-112">InsertMethod</span></span>
> - <span data-ttu-id="d543f-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="d543f-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="d543f-114">これらのプロパティは、対応する操作を処理するメソッドの名前を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="d543f-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="d543f-115">そのメソッド内で、データと対話するためのロジックを提供します。</span><span class="sxs-lookup"><span data-stu-id="d543f-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="d543f-116">このチュートリアルは、シリーズの第 1[部](retrieving-data.md)で作成したプロジェクトに基づいています。</span><span class="sxs-lookup"><span data-stu-id="d543f-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="d543f-117">完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="d543f-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="d543f-118">ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。</span><span class="sxs-lookup"><span data-stu-id="d543f-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="d543f-119">このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="d543f-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d543f-120">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="d543f-120">What you'll build</span></span>

<span data-ttu-id="d543f-121">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d543f-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="d543f-122">動的データテンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="d543f-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="d543f-123">モデルバインドメソッドを使用したデータの更新と削除を有効にする</span><span class="sxs-lookup"><span data-stu-id="d543f-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="d543f-124">データ検証規則の適用-データベースでの新しいレコードの作成を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d543f-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="d543f-125">動的データテンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="d543f-125">Add dynamic data templates</span></span>

<span data-ttu-id="d543f-126">最適なユーザーエクスペリエンスを提供し、コードの繰り返しを最小限に抑えるには、動的なデータテンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="d543f-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="d543f-127">NuGet パッケージをインストールすると、事前に構築された動的なデータテンプレートを既存のサイトに簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="d543f-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="d543f-128">**[NuGet パッケージの管理]** で、 **DynamicDataTemplatesCS**をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d543f-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![動的なデータテンプレート](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="d543f-130">プロジェクトに**DynamicData**という名前のフォルダーが追加されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d543f-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="d543f-131">このフォルダーには、web フォームの動的コントロールに自動的に適用されるテンプレートがあります。</span><span class="sxs-lookup"><span data-stu-id="d543f-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![動的データフォルダー](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="d543f-133">更新と削除を有効にする</span><span class="sxs-lookup"><span data-stu-id="d543f-133">Enable updating and deleting</span></span>

<span data-ttu-id="d543f-134">ユーザーがデータベース内のレコードを更新および削除できるようにすることは、データを取得するプロセスと非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="d543f-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="d543f-135">**UpdateMethod**プロパティと**DeleteMethod**プロパティでは、これらの操作を実行するメソッドの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="d543f-136">GridView コントロールでは、[編集] ボタンと [削除] ボタンの自動生成を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="d543f-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="d543f-137">次の強調表示されたコードは、GridView コードへの追加を示しています。</span><span class="sxs-lookup"><span data-stu-id="d543f-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="d543f-138">分離コードファイルで、using ステートメントを追加して、system.object を追加し**ます。**</span><span class="sxs-lookup"><span data-stu-id="d543f-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="d543f-139">次に、update メソッドと delete メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="d543f-140">**TryUpdateModel**メソッドは、web フォームからデータ項目に、一致するデータバインド値を適用します。</span><span class="sxs-lookup"><span data-stu-id="d543f-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="d543f-141">データ項目は、id パラメーターの値に基づいて取得されます。</span><span class="sxs-lookup"><span data-stu-id="d543f-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="d543f-142">検証要件の適用</span><span class="sxs-lookup"><span data-stu-id="d543f-142">Enforce validation requirements</span></span>

<span data-ttu-id="d543f-143">Student クラスの FirstName、LastName、および Year プロパティに適用した検証属性は、データの更新時に自動的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="d543f-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="d543f-144">DynamicField は、検証属性に基づいてクライアントとサーバーの検証コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="d543f-145">FirstName と LastName の両方のプロパティが必要です。</span><span class="sxs-lookup"><span data-stu-id="d543f-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="d543f-146">FirstName は、長さが20文字を超えることはできず、LastName は40文字を超えることはできません。</span><span class="sxs-lookup"><span data-stu-id="d543f-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="d543f-147">Year は、AcademicYear 列挙型の有効な値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d543f-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="d543f-148">ユーザーがいずれかの検証要件に違反している場合、更新は続行されません。</span><span class="sxs-lookup"><span data-stu-id="d543f-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="d543f-149">エラーメッセージを表示するには、GridView の上に ValidationSummary コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="d543f-150">モデルバインドの検証エラーを表示するには、 **Showmodelstateerrors**プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="d543f-151">Web アプリケーションを実行し、レコードを更新して削除します。</span><span class="sxs-lookup"><span data-stu-id="d543f-151">Run the web application, and update and delete any of the records.</span></span>

![データの更新](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="d543f-153">編集モードでは、Year プロパティの値がドロップダウンリストとして自動的に表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d543f-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="d543f-154">Year プロパティは列挙値で、列挙値の動的データテンプレートは編集用のドロップダウンリストを指定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="d543f-155">このテンプレートを見つけるには、 **DynamicData**/**fieldtemplates**フォルダーで**列挙\_編集 .ascx**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="d543f-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="d543f-156">有効な値を指定した場合、更新は正常に完了します。</span><span class="sxs-lookup"><span data-stu-id="d543f-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="d543f-157">検証要件のいずれかに違反した場合、更新は続行されず、グリッドの上にエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d543f-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![error message](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="d543f-159">新しいレコードの追加</span><span class="sxs-lookup"><span data-stu-id="d543f-159">Add new records</span></span>

<span data-ttu-id="d543f-160">GridView コントロールには**Insertmethod**プロパティが含まれていないため、モデルバインドで新しいレコードを追加するために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="d543f-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="d543f-161">InsertMethod プロパティは、 **FormView**、 **DetailsView**、または**ListView**コントロールで見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="d543f-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="d543f-162">このチュートリアルでは、FormView コントロールを使用して新しいレコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="d543f-163">まず、新しいレコードを追加するために作成する新しいページへのリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="d543f-164">ValidationSummary の上に、次のように追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="d543f-165">新しいリンクは、[Students] ページのコンテンツの上部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d543f-165">The new link will appear at the top of the content for the Students page.</span></span>

![新しいリンク](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="d543f-167">次に、マスターページを使用して新しい web フォームを追加し、「 **Addstudent**」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="d543f-168">マスターページとして [.Master] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d543f-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="d543f-169">**DynamicEntity**コントロールを使用して、新しい学生を追加するためのフィールドを表示します。</span><span class="sxs-lookup"><span data-stu-id="d543f-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="d543f-170">DynamicEntity コントロールは、ItemType プロパティで指定されたクラスの編集可能なプロパティをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="d543f-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="d543f-171">StudentID プロパティは、表示されないように、 **[ScaffoldColumn (false)]** 属性でマークされています。</span><span class="sxs-lookup"><span data-stu-id="d543f-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="d543f-172">AddStudent ページの MainContent プレースホルダーで、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d543f-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="d543f-173">分離コードファイル (AddStudent.aspx.cs) で、コンテキスト**の名前空間**に対して、using ステートメントを追加し**て**ください。</span><span class="sxs-lookup"><span data-stu-id="d543f-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="d543f-174">次に、次のメソッドを追加して、新しいレコードの挿入方法と [キャンセル] ボタンのイベントハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="d543f-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="d543f-175">すべての変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="d543f-175">Save all of the changes.</span></span>

<span data-ttu-id="d543f-176">Web アプリケーションを実行し、新しい学生を作成します。</span><span class="sxs-lookup"><span data-stu-id="d543f-176">Run the web application and create a new student.</span></span>

![新しい学生の追加](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="d543f-178">**[挿入]** をクリックすると、新しい学生が作成されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="d543f-178">Click **Insert** and notice the new student has been created.</span></span>

![新しい学生を表示](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="d543f-180">まとめ</span><span class="sxs-lookup"><span data-stu-id="d543f-180">Conclusion</span></span>

<span data-ttu-id="d543f-181">このチュートリアルでは、データの更新、削除、および作成を有効にしました。</span><span class="sxs-lookup"><span data-stu-id="d543f-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="d543f-182">データを操作するときに検証規則が適用されることを確認しました。</span><span class="sxs-lookup"><span data-stu-id="d543f-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="d543f-183">このシリーズの次の[チュートリアル](sorting-paging-and-filtering-data.md)では、データの並べ替え、ページング、フィルター処理を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d543f-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d543f-184">[前へ](retrieving-data.md)
> [次へ](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="d543f-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
