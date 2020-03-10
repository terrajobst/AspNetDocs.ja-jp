---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 8 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473506"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="b121e-104">Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート8</span><span class="sxs-lookup"><span data-stu-id="b121e-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>

<span data-ttu-id="b121e-105">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b121e-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="b121e-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b121e-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="b121e-107">チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b121e-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="b121e-108">動的データ機能を使用したデータの書式設定と検証</span><span class="sxs-lookup"><span data-stu-id="b121e-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="b121e-109">前のチュートリアルでは、ストアドプロシージャを実装しています。</span><span class="sxs-lookup"><span data-stu-id="b121e-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="b121e-110">このチュートリアルでは、動的データ機能によって次のような利点が得られることについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b121e-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="b121e-111">フィールドは、データ型に基づいて自動的に書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="b121e-112">フィールドは、データ型に基づいて自動的に検証されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="b121e-113">データモデルにメタデータを追加して、書式設定や検証の動作をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="b121e-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="b121e-114">これを行うと、書式設定規則と検証規則を1つの場所にのみ追加できます。また、動的データコントロールを使用して、フィールドにアクセスするすべての場所に自動的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="b121e-115">これがどのように動作するかを確認するには、既存の*student .aspx*ページのフィールドの表示と編集に使用するコントロールを変更し、`Student` エンティティ型の名前と日付のフィールドに書式設定および検証メタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="b121e-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="b121e-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="b121e-117">DynamicField および Dynamicfield コントロールの使用</span><span class="sxs-lookup"><span data-stu-id="b121e-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="b121e-118">*Student*ページを開き、`StudentsGridView` コントロールで、**名前**と**登録の日付**`TemplateField` 要素を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b121e-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="b121e-119">このマークアップは、[student name template] フィールドの `TextBox` および `Label` コントロールの代わりに `DynamicControl` コントロールを使用し、登録日に `DynamicField` コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="b121e-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="b121e-120">書式指定文字列が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="b121e-120">No format strings are specified.</span></span>

<span data-ttu-id="b121e-121">`StudentsGridView` コントロールの後に `ValidationSummary` コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="b121e-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="b121e-122">`SearchGridView` コントロールで、 **[名前]** 列と **[登録日付]** 列のマークアップを、`StudentsGridView` コントロールで行ったように置き換えます。ただし、`EditItemTemplate` 要素は省略します。</span><span class="sxs-lookup"><span data-stu-id="b121e-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="b121e-123">`SearchGridView` コントロールの `Columns` 要素には、次のマークアップが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b121e-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="b121e-124">*Students.aspx.cs*を開き、次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="b121e-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="b121e-125">ページの `Init` イベントのハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b121e-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="b121e-126">このコードは、`Student` エンティティのフィールドに対して、これらのデータバインドコントロールで書式設定と検証を行う動的データことを指定します。</span><span class="sxs-lookup"><span data-stu-id="b121e-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="b121e-127">ページを実行するときに、次の例のようなエラーメッセージが表示された場合は、通常、`Page_Init`で `EnableDynamicData` メソッドを呼び出さないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="b121e-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="b121e-128">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="b121e-128">Run the page.</span></span>

<span data-ttu-id="b121e-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="b121e-130">**[登録日]** 列には、プロパティの型が `DateTime`なので、日付と共に時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="b121e-131">これは後で修正します。</span><span class="sxs-lookup"><span data-stu-id="b121e-131">You'll fix that later.</span></span>

<span data-ttu-id="b121e-132">ここでは、動的データによって基本的なデータの検証が自動的に提供されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b121e-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="b121e-133">たとえば、 **[編集]** をクリックし、日付 フィールドをオフにして、 **[更新]** をクリックすると、データモデルで null 値が許容されないため、動的データによって自動的に必須フィールドになります。</span><span class="sxs-lookup"><span data-stu-id="b121e-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="b121e-134">このページでは、フィールドの後にアスタリスクが表示され、`ValidationSummary` コントロールにエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="b121e-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="b121e-136">エラーメッセージを表示するには、アスタリスクの上にマウスポインターを置くこともできるため、`ValidationSummary` コントロールを省略できます。</span><span class="sxs-lookup"><span data-stu-id="b121e-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="b121e-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="b121e-138">また動的データは、**登録日**フィールドに入力されたデータが有効な日付であることを検証します。</span><span class="sxs-lookup"><span data-stu-id="b121e-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="b121e-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="b121e-140">ご覧のように、これは一般的なエラーメッセージです。</span><span class="sxs-lookup"><span data-stu-id="b121e-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="b121e-141">次のセクションでは、メッセージのカスタマイズ方法と検証規則および書式設定規則について説明します。</span><span class="sxs-lookup"><span data-stu-id="b121e-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="b121e-142">データモデルへのメタデータの追加</span><span class="sxs-lookup"><span data-stu-id="b121e-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="b121e-143">通常は、動的データによって提供される機能をカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="b121e-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="b121e-144">たとえば、データの表示方法とエラーメッセージの内容を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="b121e-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="b121e-145">また、データ型に基づいて自動的に提供される機能動的データよりも多くの機能を提供するように、データ検証ルールをカスタマイズすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b121e-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="b121e-146">これを行うには、エンティティ型に対応する部分クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b121e-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="b121e-147">**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクトを右クリックし、 **[参照の追加]** を選択して、`System.ComponentModel.DataAnnotations`への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="b121e-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="b121e-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="b121e-149">*DAL*フォルダーで、新しいクラスファイルを作成し、 *Student.cs*という名前を付け、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b121e-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="b121e-150">このコードでは、`Student` エンティティの部分クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b121e-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="b121e-151">この部分クラスに適用される `MetadataType` 属性は、メタデータの指定に使用しているクラスを識別します。</span><span class="sxs-lookup"><span data-stu-id="b121e-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="b121e-152">メタデータクラスには任意の名前を付けることができますが、エンティティ名と "メタデータ" を使用するのが一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="b121e-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="b121e-153">メタデータクラスのプロパティに適用される属性は、書式設定、検証、規則、およびエラーメッセージを指定します。</span><span class="sxs-lookup"><span data-stu-id="b121e-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="b121e-154">ここに表示される属性の結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="b121e-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="b121e-155">`EnrollmentDate` は日付として表示されます (時刻は含まれません)。</span><span class="sxs-lookup"><span data-stu-id="b121e-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="b121e-156">両方の名前フィールドは25文字以下である必要があり、カスタムエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="b121e-157">両方の名前フィールドが必須であり、カスタムエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="b121e-158">もう一度*student*ページを実行すると、日付が何度も表示されなくなっていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="b121e-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="b121e-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="b121e-160">行を編集して、[名前] フィールドの値をクリアします。</span><span class="sxs-lookup"><span data-stu-id="b121e-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="b121e-161">**[更新]** をクリックする前に、フィールドを終了するとすぐにフィールドエラーを示すアスタリスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="b121e-162">**[更新]** をクリックすると、指定したエラーメッセージのテキストがページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="b121e-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="b121e-164">25文字を超える名前を入力してください。 **[更新]** をクリックすると、指定したエラーメッセージのテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="b121e-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="b121e-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="b121e-166">これで、これらの書式設定と検証規則がデータモデルメタデータに設定されたので、`DynamicControl` または `DynamicField` コントロールを使用している限り、これらのフィールドを表示または変更できるすべてのページに規則が自動的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b121e-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="b121e-167">これにより、記述する必要がある冗長なコードの量が減り、プログラミングとテストが容易になり、アプリケーション全体でデータの書式設定と検証の一貫性が保たれます。</span><span class="sxs-lookup"><span data-stu-id="b121e-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="b121e-168">詳細情報</span><span class="sxs-lookup"><span data-stu-id="b121e-168">More Information</span></span>

<span data-ttu-id="b121e-169">これで、Entity Framework を使用したはじめにに関するこの一連のチュートリアルは終了です。</span><span class="sxs-lookup"><span data-stu-id="b121e-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="b121e-170">Entity Framework の使用方法を学習するのに役立つその他のリソースについては、[次の Entity Framework チュートリアルシリーズの最初のチュートリアル](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)に進んでください。または、次のサイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b121e-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="b121e-171">Entity Framework FAQ</span><span class="sxs-lookup"><span data-stu-id="b121e-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="b121e-172">Entity Framework チームのブログ</span><span class="sxs-lookup"><span data-stu-id="b121e-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="b121e-173">MSDN ライブラリの Entity Framework</span><span class="sxs-lookup"><span data-stu-id="b121e-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="b121e-174">MSDN Data Developer Center の Entity Framework</span><span class="sxs-lookup"><span data-stu-id="b121e-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="b121e-175">MSDN ライブラリの EntityDataSource Web サーバーコントロールの概要</span><span class="sxs-lookup"><span data-stu-id="b121e-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="b121e-176">MSDN ライブラリの EntityDataSource control API リファレンス</span><span class="sxs-lookup"><span data-stu-id="b121e-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="b121e-177">MSDN の Entity Framework フォーラム</span><span class="sxs-lookup"><span data-stu-id="b121e-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="b121e-178">ジュリー Lerman のブログ</span><span class="sxs-lookup"><span data-stu-id="b121e-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> <span data-ttu-id="b121e-179">[[戻る]](the-entity-framework-and-aspnet-getting-started-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b121e-179">[Previous](the-entity-framework-and-aspnet-getting-started-part-7.md)</span></span>
