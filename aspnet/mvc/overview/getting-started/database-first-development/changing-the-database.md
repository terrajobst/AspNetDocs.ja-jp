---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'チュートリアル: ASP.NET MVC アプリで EF Database First のデータベースを変更する'
description: このチュートリアルでは、データベース構造を更新し、web アプリケーション全体でその変更を反映する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499522"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="47266-103">チュートリアル: ASP.NET MVC アプリで EF Database First のデータベースを変更する</span><span class="sxs-lookup"><span data-stu-id="47266-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="47266-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="47266-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="47266-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="47266-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="47266-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="47266-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="47266-107">このチュートリアルでは、データベース構造を更新し、web アプリケーション全体でその変更を反映する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="47266-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="47266-108">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="47266-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47266-109">列を追加する</span><span class="sxs-lookup"><span data-stu-id="47266-109">Add a column</span></span>
> * <span data-ttu-id="47266-110">ビューにプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="47266-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47266-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="47266-111">Prerequisites</span></span>

* [<span data-ttu-id="47266-112">ビューの生成</span><span class="sxs-lookup"><span data-stu-id="47266-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="47266-113">列を追加する</span><span class="sxs-lookup"><span data-stu-id="47266-113">Add a column</span></span>

<span data-ttu-id="47266-114">データベース内のテーブルの構造を更新する場合は、変更がデータモデル、ビュー、およびコントローラーに反映されていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="47266-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="47266-115">このチュートリアルでは、student テーブルに新しい列を追加して、学生のミドルネームを記録します。</span><span class="sxs-lookup"><span data-stu-id="47266-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="47266-116">この列を追加するには、データベースプロジェクトを開き、Student .sql ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="47266-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="47266-117">デザイナーまたは T-sql コードを使用して、 **MiddleName**という名前の列を追加します。これは NVARCHAR (50) であり、NULL 値を許容します。</span><span class="sxs-lookup"><span data-stu-id="47266-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="47266-118">データベースプロジェクト (または F5 キー) を起動して、この変更をローカルデータベースに配置します。</span><span class="sxs-lookup"><span data-stu-id="47266-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="47266-119">新しいフィールドがテーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="47266-119">The new field is added to the table.</span></span> <span data-ttu-id="47266-120">SQL Server オブジェクトエクスプローラーに表示されない場合は、ウィンドウの [更新] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="47266-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![新しい列の表示](changing-the-database/_static/image2.png)

<span data-ttu-id="47266-122">新しい列はデータベーステーブルに存在しますが、現在はデータモデルクラスに存在しません。</span><span class="sxs-lookup"><span data-stu-id="47266-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="47266-123">新しい列を含めるようにモデルを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="47266-123">You must update the model to include your new column.</span></span> <span data-ttu-id="47266-124">**[モデル]** フォルダーで、 **ContosoModel**ファイルを開いてモデル図を表示します。</span><span class="sxs-lookup"><span data-stu-id="47266-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="47266-125">学生モデルには、MiddleName プロパティが含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="47266-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="47266-126">デザイン画面の任意の場所を右クリックし、 **[データベースからモデルを更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="47266-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="47266-127">更新ウィザードで、[最新の情報に**更新**] タブを選択し、[**テーブル** > **dbo** > **Student**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="47266-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="47266-128">**[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="47266-128">Click **Finish**.</span></span>

<span data-ttu-id="47266-129">更新プロセスが完了すると、データベースダイアグラムに新しい**MiddleName**プロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="47266-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="47266-130">**ContosoModel**ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="47266-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="47266-131">新しいプロパティを**Student.cs**クラスに反映させるには、このファイルを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="47266-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="47266-132">これで、データベースとモデルが更新されました。</span><span class="sxs-lookup"><span data-stu-id="47266-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="47266-133">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="47266-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="47266-134">ビューにプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="47266-134">Add the property to the views</span></span>

<span data-ttu-id="47266-135">残念ながら、ビューには新しいプロパティが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="47266-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="47266-136">ビューを更新するには、2つのオプションがあります。もう一度 Student クラスのスキャフォールディングを追加することで、ビューを再生成するか、既存のビューに新しいプロパティを手動で追加することができます。</span><span class="sxs-lookup"><span data-stu-id="47266-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="47266-137">このチュートリアルでは、自動的に生成されたビューに変更を加えていないため、スキャフォールディングを再び追加します。</span><span class="sxs-lookup"><span data-stu-id="47266-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="47266-138">ビューに変更を加えたときに、その変更が失われないようにする場合は、プロパティを手動で追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="47266-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="47266-139">ビューが再作成されるようにするには、 **[表示]** の下にある **[Students]** フォルダーを削除し、 **StudentsController**を削除します。</span><span class="sxs-lookup"><span data-stu-id="47266-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="47266-140">次に、 **Controllers**フォルダーを右クリックし、 **Student**モデルのスキャフォールディングを追加します。</span><span class="sxs-lookup"><span data-stu-id="47266-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="47266-141">ここでも、コントローラーに**StudentsController**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="47266-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="47266-142">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="47266-142">Select **Add**.</span></span>

<span data-ttu-id="47266-143">ソリューションをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="47266-143">Build the solution again.</span></span> <span data-ttu-id="47266-144">ビューには、MiddleName プロパティが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="47266-144">The views now contain the MiddleName property.</span></span>

![ミドルネームの表示](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="47266-146">次のステップ</span><span class="sxs-lookup"><span data-stu-id="47266-146">Next steps</span></span>

<span data-ttu-id="47266-147">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="47266-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47266-148">列を追加しました</span><span class="sxs-lookup"><span data-stu-id="47266-148">Added a column</span></span>
> * <span data-ttu-id="47266-149">ビューにプロパティを追加しました</span><span class="sxs-lookup"><span data-stu-id="47266-149">Added the property to the views</span></span>

<span data-ttu-id="47266-150">次のチュートリアルに進み、学生レコードの詳細を表示するようにビューをカスタマイズする方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="47266-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="47266-151">ビューのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="47266-151">Customize a view</span></span>](customizing-a-view.md)