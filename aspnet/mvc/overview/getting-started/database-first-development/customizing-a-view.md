---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'チュートリアル: ASP.NET MVC アプリで EF Database First のビューをカスタマイズする'
description: このチュートリアルでは、自動的に生成されたビューを変更してプレゼンテーションを拡張する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471520"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="875d9-103">チュートリアル: ASP.NET MVC アプリで EF Database First のビューをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="875d9-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="875d9-104">MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="875d9-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="875d9-105">このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="875d9-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="875d9-106">生成されたコードは、データベーステーブルの列に対応しています。</span><span class="sxs-lookup"><span data-stu-id="875d9-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="875d9-107">このチュートリアルでは、自動的に生成されたビューを変更してプレゼンテーションを拡張する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="875d9-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="875d9-108">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="875d9-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="875d9-109">学生の詳細ページにコースを追加する</span><span class="sxs-lookup"><span data-stu-id="875d9-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="875d9-110">コースがページに追加されたことを確認する</span><span class="sxs-lookup"><span data-stu-id="875d9-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="875d9-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="875d9-111">Prerequisites</span></span>

* [<span data-ttu-id="875d9-112">データベースの変更</span><span class="sxs-lookup"><span data-stu-id="875d9-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="875d9-113">学生の詳細にコースを追加する</span><span class="sxs-lookup"><span data-stu-id="875d9-113">Add courses to student detail</span></span>

<span data-ttu-id="875d9-114">生成されたコードはアプリケーションの開始点として適していますが、必ずしもアプリケーションで必要なすべての機能を提供するわけではありません。</span><span class="sxs-lookup"><span data-stu-id="875d9-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="875d9-115">コードをカスタマイズして、アプリケーションの特定の要件を満たすことができます。</span><span class="sxs-lookup"><span data-stu-id="875d9-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="875d9-116">現在、選択した学生に登録されているコースはアプリケーションで表示されません。</span><span class="sxs-lookup"><span data-stu-id="875d9-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="875d9-117">このセクションでは、受講者ごとに登録されているコースを、学生の**詳細**ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="875d9-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="875d9-118"> > **Students** > Details. *Cshtml*という**ビュー**を開きます。</span><span class="sxs-lookup"><span data-stu-id="875d9-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="875d9-119">最後の &lt;/dl&gt; タグの下に、終了 &lt;/div&gt; タグの前に、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="875d9-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="875d9-120">このコードは、選択した学生の登録テーブル内の各レコードの行を表示するテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="875d9-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="875d9-121">**Display**メソッドは、式を表すオブジェクト (modelitem) の HTML をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="875d9-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="875d9-122">(単にプロパティ値をコードに埋め込むのではなく) 表示メソッドを使用して、その型とその型のテンプレートに基づいて値が正しく書式設定されるようにします。</span><span class="sxs-lookup"><span data-stu-id="875d9-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="875d9-123">この例では、各式はループ内の現在のレコードから1つのプロパティを返し、値はテキストとして表示されるプリミティブ型です。</span><span class="sxs-lookup"><span data-stu-id="875d9-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="875d9-124">コースが追加されたことを確認する</span><span class="sxs-lookup"><span data-stu-id="875d9-124">Confirm courses are added</span></span>

<span data-ttu-id="875d9-125">ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="875d9-125">Run the solution.</span></span> <span data-ttu-id="875d9-126">**[学生の一覧]** をクリックし、いずれかの学生の **[詳細]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="875d9-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="875d9-127">登録されているコースがビューに含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="875d9-127">You will see the enrolled courses have been included in the view.</span></span>

![登録される学生](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="875d9-129">次のステップ</span><span class="sxs-lookup"><span data-stu-id="875d9-129">Next steps</span></span>
<span data-ttu-id="875d9-130">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="875d9-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="875d9-131">学生の詳細ページへのコースの追加</span><span class="sxs-lookup"><span data-stu-id="875d9-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="875d9-132">コースがページに追加されたことを確認しました</span><span class="sxs-lookup"><span data-stu-id="875d9-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="875d9-133">次のチュートリアルに進み、データ注釈を追加して検証要件を指定し、書式設定を表示する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="875d9-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="875d9-134">データの検証を強化する</span><span class="sxs-lookup"><span data-stu-id="875d9-134">Enhance data validation</span></span>](enhancing-data-validation.md)
