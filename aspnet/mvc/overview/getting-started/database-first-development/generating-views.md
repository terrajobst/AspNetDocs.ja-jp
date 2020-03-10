---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'チュートリアル: ASP.NET MVC アプリで EF Database First のビューを生成する'
description: このチュートリアルでは、ASP.NET スキャフォールディングを使用してコントローラーとビューを生成する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499474"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="b0808-103">チュートリアル: ASP.NET MVC アプリで EF Database First のビューを生成する</span><span class="sxs-lookup"><span data-stu-id="b0808-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="b0808-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b0808-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="b0808-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b0808-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="b0808-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="b0808-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="b0808-107">このチュートリアルでは、ASP.NET スキャフォールディングを使用してコントローラーとビューを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b0808-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="b0808-108">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="b0808-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b0808-109">スキャフォールディングの追加</span><span class="sxs-lookup"><span data-stu-id="b0808-109">Add scaffold</span></span>
> * <span data-ttu-id="b0808-110">新しいビューへのリンクの追加</span><span class="sxs-lookup"><span data-stu-id="b0808-110">Add links to new views</span></span>
> * <span data-ttu-id="b0808-111">学生のビューを表示する</span><span class="sxs-lookup"><span data-stu-id="b0808-111">Display student views</span></span>
> * <span data-ttu-id="b0808-112">登録ビューを表示する</span><span class="sxs-lookup"><span data-stu-id="b0808-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="b0808-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="b0808-113">Prerequisite</span></span>

* [<span data-ttu-id="b0808-114">Web アプリケーションとデータモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="b0808-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="b0808-115">スキャフォールディングの追加</span><span class="sxs-lookup"><span data-stu-id="b0808-115">Add scaffold</span></span>

<span data-ttu-id="b0808-116">モデルクラスの標準的なデータ操作を提供するコードを生成する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="b0808-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="b0808-117">コードを追加するには、スキャフォールディング項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="b0808-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="b0808-118">追加できるスキャフォールディングの種類には、さまざまなオプションがあります。このチュートリアルでは、スキャフォールディングには、前のセクションで作成した学生および登録モデルに対応するコントローラーとビューが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b0808-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="b0808-119">プロジェクトの一貫性を維持するために、 **[既存のコントローラー]** フォルダーに新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b0808-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="b0808-120">**Controllers**フォルダーを右クリックし、[ **Add** > **New スキャフォールディング Item**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b0808-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="b0808-121">Entity Framework オプション**を使用して、ビューがある MVC 5 コントローラー**を選択します。</span><span class="sxs-lookup"><span data-stu-id="b0808-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="b0808-122">このオプションを選択すると、モデルのデータを更新、削除、作成、および表示するためのコントローラーとビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![mvc コントローラーの追加](generating-views/_static/image2.png)

<span data-ttu-id="b0808-124">モデルクラスの **[Student (ContosoSite)]** を選択し、コンテキストクラスに対して **[ContosoSite]** を選択し、コンテキストクラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="b0808-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="b0808-125">コントローラー名を**StudentsController**として保持します。</span><span class="sxs-lookup"><span data-stu-id="b0808-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="b0808-126">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b0808-126">Click **Add**.</span></span>

<span data-ttu-id="b0808-127">エラーが発生した場合は、前のセクションでプロジェクトをビルドしていないことが原因である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b0808-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="b0808-128">その場合は、プロジェクトをビルドしてから、スキャフォールディング項目をもう一度追加してみてください。</span><span class="sxs-lookup"><span data-stu-id="b0808-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="b0808-129">コード生成プロセスが完了すると、プロジェクトの **[コントローラー]** フォルダーと [**ビュー** > **Students** ] フォルダーに新しいコントローラーとビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="b0808-130">同じ手順をもう一度実行しますが、**登録**クラスのスキャフォールディングを追加します。</span><span class="sxs-lookup"><span data-stu-id="b0808-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="b0808-131">完了すると、 **EnrollmentsController.cs**ファイルと、Create、Delete、Details、Edit、および Index の各ビュー**を含む [** 登録] という名前のフォルダー**が表示さ**れます。</span><span class="sxs-lookup"><span data-stu-id="b0808-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="b0808-132">新しいビューへのリンクの追加</span><span class="sxs-lookup"><span data-stu-id="b0808-132">Add links to new views</span></span>

<span data-ttu-id="b0808-133">新しいビューへの移動を容易にするために、生徒用および登録用のインデックスビューにいくつかのハイパーリンクを追加できます。</span><span class="sxs-lookup"><span data-stu-id="b0808-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="b0808-134">[ **Views** > **home** > *Index. cshtml*] (サイトのホームページ) でファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="b0808-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="b0808-135">Jumbotron の下に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b0808-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="b0808-136">Html.actionlink メソッドの場合、最初のパラメーターはリンクに表示するテキストです。</span><span class="sxs-lookup"><span data-stu-id="b0808-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="b0808-137">2番目のパラメーターはアクションで、3番目のパラメーターはコントローラーの名前です。</span><span class="sxs-lookup"><span data-stu-id="b0808-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="b0808-138">たとえば、最初のリンクは StudentsController の Index アクションを指します。</span><span class="sxs-lookup"><span data-stu-id="b0808-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="b0808-139">実際のハイパーリンクは、これらの値から構築されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="b0808-140">最初のリンクでは、最終的に、 **Views/Students**フォルダー内の**インデックスの cshtml**ファイルに移動します。</span><span class="sxs-lookup"><span data-stu-id="b0808-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="b0808-141">学生のビューを表示する</span><span class="sxs-lookup"><span data-stu-id="b0808-141">Display student views</span></span>

<span data-ttu-id="b0808-142">プロジェクトに追加されたコードによって、学生の一覧が正しく表示され、ユーザーがデータベース内の学生レコードを編集、作成、または削除できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b0808-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="b0808-143">**Views** > **Home** > *Index. cshtml*ファイルを右クリックし、 **[ブラウザーで表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b0808-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="b0808-144">アプリケーションのホームページで、 **[学生のリスト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b0808-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="b0808-145">**[インデックス]** ページで、学生とこのデータを変更するためのリンクの一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="b0808-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="b0808-146">**[新規作成]** リンクを選択し、新しい学生の値をいくつか指定します。</span><span class="sxs-lookup"><span data-stu-id="b0808-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="b0808-147">**[作成]** をクリックすると、新しい学生がリストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="b0808-148">**[インデックス]** ページに戻り、 **[編集]** リンクを選択して、学生の値の一部を変更します。</span><span class="sxs-lookup"><span data-stu-id="b0808-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="b0808-149">**[保存]** をクリックすると、student レコードが変更されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="b0808-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="b0808-150">最後に、 **[削除]** リンクを選択し、 **[削除]** ボタンをクリックしてレコードを削除することを確認します。</span><span class="sxs-lookup"><span data-stu-id="b0808-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="b0808-151">コードを記述しなくても、Student テーブルのデータに対して一般的な操作を実行するビューが追加されています。</span><span class="sxs-lookup"><span data-stu-id="b0808-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="b0808-152">フィールドのテキストラベルはデータベースプロパティ ( **LastName**など) に基づいていることに気付いたかもしれませんが、web ページに表示するものとは必ずしも同じではありません。</span><span class="sxs-lookup"><span data-stu-id="b0808-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="b0808-153">たとえば、ラベルを**姓**にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b0808-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="b0808-154">この表示の問題は、このチュートリアルの後半で修正します。</span><span class="sxs-lookup"><span data-stu-id="b0808-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="b0808-155">登録ビューを表示する</span><span class="sxs-lookup"><span data-stu-id="b0808-155">Display enrollment views</span></span>

<span data-ttu-id="b0808-156">データベースには、Student テーブルと Enrollment テーブルの間の一対多リレーションシップと、コースと登録テーブルの間の一対多リレーションシップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b0808-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="b0808-157">登録のビューでは、これらのリレーションシップが正しく処理されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="b0808-158">サイトのホームページに移動**し、登録リンクを**選択してから、 **[新規作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b0808-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="b0808-159">ビューには、新しい登録レコードを作成するためのフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="b0808-160">特に、フォームには**CourseID**ドロップダウンリストと**StudentID**ドロップダウンリストが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b0808-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="b0808-161">両方に、関連テーブルの値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="b0808-162">さらに、指定された値の検証は、フィールドのデータ型に基づいて自動的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b0808-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="b0808-163">**グレード**には数値が必要であるため、互換性のない値を指定しようとするとエラーメッセージが表示されます。*フィールドグレードは数値である必要があります。*</span><span class="sxs-lookup"><span data-stu-id="b0808-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="b0808-164">自動的に生成されたビューで、ユーザーがデータベース内のデータを操作できることを確認しました。</span><span class="sxs-lookup"><span data-stu-id="b0808-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="b0808-165">このシリーズの次のチュートリアルでは、データベースを更新し、web アプリケーションで対応する変更を行います。</span><span class="sxs-lookup"><span data-stu-id="b0808-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0808-166">次のステップ</span><span class="sxs-lookup"><span data-stu-id="b0808-166">Next steps</span></span>

<span data-ttu-id="b0808-167">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="b0808-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b0808-168">追加されたスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="b0808-168">Added scaffold</span></span>
> * <span data-ttu-id="b0808-169">新しいビューへのリンクを追加しました</span><span class="sxs-lookup"><span data-stu-id="b0808-169">Added links to new views</span></span>
> * <span data-ttu-id="b0808-170">表示される学生の表示</span><span class="sxs-lookup"><span data-stu-id="b0808-170">Displayed student views</span></span>
> * <span data-ttu-id="b0808-171">表示される登録ビュー</span><span class="sxs-lookup"><span data-stu-id="b0808-171">Displayed enrollment views</span></span>

<span data-ttu-id="b0808-172">次のチュートリアルに進み、データベースを変更する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="b0808-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b0808-173">データベースの変更</span><span class="sxs-lookup"><span data-stu-id="b0808-173">Change the database</span></span>](changing-the-database.md)