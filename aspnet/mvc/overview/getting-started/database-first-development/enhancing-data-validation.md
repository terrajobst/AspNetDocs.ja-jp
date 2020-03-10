---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'チュートリアル: ASP.NET MVC アプリを使用して EF Database First のデータ検証を強化する'
description: このチュートリアルでは、データモデルへのデータ注釈の追加に焦点を当て、検証要件を指定し、書式設定を表示します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499534"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="b2e41-103">チュートリアル: ASP.NET MVC アプリを使用して EF Database First のデータ検証を強化する</span><span class="sxs-lookup"><span data-stu-id="b2e41-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="b2e41-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="b2e41-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="b2e41-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="b2e41-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="b2e41-107">このチュートリアルでは、データモデルへのデータ注釈の追加に焦点を当て、検証要件を指定し、書式設定を表示します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="b2e41-108">コメントセクションのユーザーからのフィードバックに基づいて改善されました。</span><span class="sxs-lookup"><span data-stu-id="b2e41-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="b2e41-109">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="b2e41-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2e41-110">データ注釈の追加</span><span class="sxs-lookup"><span data-stu-id="b2e41-110">Add data annotations</span></span>
> * <span data-ttu-id="b2e41-111">メタデータクラスの追加</span><span class="sxs-lookup"><span data-stu-id="b2e41-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2e41-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="b2e41-112">Prerequisites</span></span>

* [<span data-ttu-id="b2e41-113">ビューのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="b2e41-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="b2e41-114">データ注釈の追加</span><span class="sxs-lookup"><span data-stu-id="b2e41-114">Add data annotations</span></span>

<span data-ttu-id="b2e41-115">前のトピックで説明したように、一部のデータ検証規則はユーザー入力に自動的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="b2e41-116">たとえば、"学年" プロパティには数値のみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="b2e41-117">さらに多くのデータ検証規則を指定するには、モデルクラスにデータ注釈を追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="b2e41-118">これらの注釈は、指定されたプロパティの web アプリケーション全体に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="b2e41-119">また、プロパティの表示方法を変更する書式設定属性を適用することもできます。たとえば、テキストラベルに使用される値を変更します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="b2e41-120">このチュートリアルでは、FirstName、LastName、および MiddleName の各プロパティに指定された値の長さを制限するデータ注釈を追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="b2e41-121">データベースでは、これらの値は50文字までに制限されています。ただし、web アプリケーションでは、文字制限は現在適用されていません。</span><span class="sxs-lookup"><span data-stu-id="b2e41-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="b2e41-122">ユーザーがこれらの値の1つに対して50文字を超える文字を入力すると、データベースに値を保存しようとしたときにページがクラッシュします。</span><span class="sxs-lookup"><span data-stu-id="b2e41-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="b2e41-123">また、グレードを 0 ~ 4 の値に制限します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="b2e41-124">[ > **モデル**] を選択し、 **ContosoModel** > **ContosoModel.tt**を選択して、 *Student.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="b2e41-125">次の強調表示されたコードをクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="b2e41-126">*Enrollment.cs*を開き、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="b2e41-127">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="b2e41-127">Build the solution.</span></span>

<span data-ttu-id="b2e41-128">**[学生の一覧]** をクリックし、 **[編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="b2e41-129">50文字を超える文字を入力しようとすると、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![エラーメッセージを表示する](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="b2e41-131">ホームページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-131">Go back to the home page.</span></span> <span data-ttu-id="b2e41-132">登録 **[の一覧]** をクリックし、 **[編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="b2e41-133">4以上のレベルを指定しようとしています。</span><span class="sxs-lookup"><span data-stu-id="b2e41-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="b2e41-134">このエラーが表示されます。*フィールドグレードは0から4までの範囲で指定する必要があります。*</span><span class="sxs-lookup"><span data-stu-id="b2e41-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="b2e41-135">メタデータクラスの追加</span><span class="sxs-lookup"><span data-stu-id="b2e41-135">Add metadata classes</span></span>

<span data-ttu-id="b2e41-136">モデルクラスに検証属性を直接追加することは、データベースが変更されることを期待していない場合に機能します。ただし、データベースが変更され、モデルクラスを再生成する必要がある場合は、モデルクラスに適用したすべての属性が失われます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="b2e41-137">このアプローチは、非常に非効率的で、重要な検証ルールが失われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="b2e41-138">この問題を回避するには、属性を含むメタデータクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="b2e41-139">モデルクラスをメタデータクラスに関連付けると、それらの属性がモデルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="b2e41-140">この方法では、メタデータクラスに適用されているすべての属性を失うことなく、モデルクラスを再生成できます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="b2e41-141">**[モデル]** フォルダーで、 *Metadata.cs*という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="b2e41-142">*Metadata.cs*のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="b2e41-143">これらのメタデータクラスには、モデルクラスに以前に適用したすべての検証属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b2e41-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="b2e41-144">**表示**属性は、テキストラベルに使用される値を変更するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="b2e41-145">ここで、モデルクラスをメタデータクラスに関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="b2e41-146">**[モデル]** フォルダーで、 *PartialClasses.cs*という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="b2e41-147">このファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="b2e41-148">各クラスは `partial` クラスとしてマークされ、各クラスは、自動的に生成されるクラスと同じ名前と名前空間に一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="b2e41-149">メタデータ属性を部分クラスに適用することで、データ検証属性が自動的に生成されたクラスに適用されるようになります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="b2e41-150">これらの属性は、再生成されない部分クラスにメタデータ属性が適用されるため、モデルクラスを再生成しても失われません。</span><span class="sxs-lookup"><span data-stu-id="b2e41-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="b2e41-151">自動的に生成されたクラスを再生成するには、 *ContosoModel*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="b2e41-152">ここでも、デザイン画面を右クリックし、 **[データベースからモデルを更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="b2e41-153">データベースを変更していない場合でも、このプロセスによってクラスが再生成されます。</span><span class="sxs-lookup"><span data-stu-id="b2e41-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="b2e41-154">**[更新]** タブで、 **[テーブル]** を選択し、 **[完了**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b2e41-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="b2e41-155">*ContosoModel*ファイルを保存して、変更を適用します。</span><span class="sxs-lookup"><span data-stu-id="b2e41-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="b2e41-156">*Student.cs*ファイルまたは*Enrollment.cs*ファイルを開くと、前に適用したデータ検証属性がファイルに存在しなくなっていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="b2e41-157">ただし、アプリケーションを実行すると、データを入力したときに検証規則が適用されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="b2e41-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b2e41-158">まとめ</span><span class="sxs-lookup"><span data-stu-id="b2e41-158">Conclusion</span></span>

<span data-ttu-id="b2e41-159">このシリーズでは、ユーザーがデータを編集、更新、作成、および削除できるようにする、既存のデータベースからコードを生成する簡単な例を提供しました。</span><span class="sxs-lookup"><span data-stu-id="b2e41-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="b2e41-160">ASP.NET MVC 5、Entity Framework および ASP.NET スキャフォールディングを使用してプロジェクトを作成していました。</span><span class="sxs-lookup"><span data-stu-id="b2e41-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="b2e41-161">Code First 開発の入門例については、「[はじめに with ASP.NET MVC 5](../introduction/getting-started.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="b2e41-162">より高度な例については、「 [ASP.NET MVC 4 アプリの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="b2e41-163">Database First のデータを操作するために使用する DbContext API は、Code First でデータを操作するために使用する API と同じであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="b2e41-164">Database First を使用する場合でも、関連データの読み取りと更新、同時実行の競合の処理など、より複雑なシナリオを処理する方法については、Code First チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="b2e41-165">唯一の違いは、データベース、コンテキストクラス、およびエンティティクラスの作成方法です。</span><span class="sxs-lookup"><span data-stu-id="b2e41-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2e41-166">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="b2e41-166">Additional resources</span></span>

<span data-ttu-id="b2e41-167">プロパティとクラスに適用できるデータ検証注釈の完全な一覧については、「 [system.componentmodel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e41-168">次のステップ</span><span class="sxs-lookup"><span data-stu-id="b2e41-168">Next steps</span></span>

<span data-ttu-id="b2e41-169">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="b2e41-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2e41-170">追加されたデータ注釈</span><span class="sxs-lookup"><span data-stu-id="b2e41-170">Added data annotations</span></span>
> * <span data-ttu-id="b2e41-171">追加されたメタデータクラス</span><span class="sxs-lookup"><span data-stu-id="b2e41-171">Added metadata classes</span></span>

<span data-ttu-id="b2e41-172">Azure App Service に web アプリと SQL データベースをデプロイする方法については、次のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2e41-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b2e41-173">Azure App Service に .NET アプリをデプロイする</span><span class="sxs-lookup"><span data-stu-id="b2e41-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
