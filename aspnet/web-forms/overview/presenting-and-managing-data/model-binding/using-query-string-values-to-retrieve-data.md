---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: クエリ文字列値を使用してモデルバインドと web フォームを使用してデータをフィルター処理する |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519082"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="a5d1f-104">クエリ文字列値を使用してモデルバインドと web フォームを使用してデータをフィルター処理する</span><span class="sxs-lookup"><span data-stu-id="a5d1f-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="a5d1f-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a5d1f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a5d1f-106">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="a5d1f-107">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="a5d1f-108">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="a5d1f-109">このチュートリアルでは、クエリ文字列に値を渡し、その値を使用してモデルバインドを通じてデータを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="a5d1f-110">このチュートリアルは、シリーズの[前](retrieving-data.md)のパートで作成したプロジェクトに基づいています。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="a5d1f-111">完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="a5d1f-112">ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="a5d1f-113">このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="a5d1f-114">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="a5d1f-114">What you'll build</span></span>

<span data-ttu-id="a5d1f-115">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="a5d1f-116">学生に登録されたコースを表示する新しいページを追加する</span><span class="sxs-lookup"><span data-stu-id="a5d1f-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="a5d1f-117">クエリ文字列の値に基づいて、選択した学生の登録済みコースを取得します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="a5d1f-118">グリッドビューから新しいページにクエリ文字列値を含むハイパーリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="a5d1f-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="a5d1f-119">このチュートリアルの手順は、前の[チュートリアル](sorting-paging-and-filtering-data.md)で説明した手順とほぼ同じですが、ドロップダウンリストでのユーザー選択に基づいて、表示される学生をフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="a5d1f-120">このチュートリアルでは、select メソッドで**control**属性を使用して、パラメーター値がコントロールから取得されるように指定しています。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="a5d1f-121">このチュートリアルでは、select メソッドで**QueryString**属性を使用して、パラメーター値をクエリ文字列から取得するように指定します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="a5d1f-122">学生のコースを表示するための新しいページを追加する</span><span class="sxs-lookup"><span data-stu-id="a5d1f-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="a5d1f-123">.Master マスターページを使用する新しい web フォームを追加し、そのページに**コース**の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="a5d1f-124">コースの **.aspx**ファイルで、選択した学生のコースを表示するグリッドビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="a5d1f-125">Select メソッドを定義する</span><span class="sxs-lookup"><span data-stu-id="a5d1f-125">Define the select method</span></span>

<span data-ttu-id="a5d1f-126">**Courses.aspx.cs**では、grid ビューの**SelectMethod**プロパティで指定した名前を使用して、select メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="a5d1f-127">このメソッドでは、学生のコースを取得するためのクエリを定義し、パラメーターと同じ名前のクエリ文字列値からパラメーターを取得するように指定します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="a5d1f-128">まず、次の**using**ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="a5d1f-129">次に、Courses.aspx.cs に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="a5d1f-130">QueryString 属性は、StudentID という名前のクエリ文字列値がこのメソッドのパラメーターに自動的に割り当てられることを意味します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="a5d1f-131">クエリ文字列値を含むハイパーリンクの追加</span><span class="sxs-lookup"><span data-stu-id="a5d1f-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="a5d1f-132">Student のグリッドビューでは、[新しいコース] ページにリンクするハイパーリンクフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="a5d1f-133">ハイパーリンクには、学生の id を持つクエリ文字列値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="a5d1f-134">Student で、合計クレジットのフィールドのすぐ下に、次のフィールドをグリッドビューの列に追加します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="a5d1f-135">アプリケーションを実行し、グリッドビューに [コース] リンクが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![ハイパーリンクの追加](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="a5d1f-137">いずれかのリンクをクリックすると、学生の登録済みコースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![コースを表示](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="a5d1f-139">まとめ</span><span class="sxs-lookup"><span data-stu-id="a5d1f-139">Conclusion</span></span>

<span data-ttu-id="a5d1f-140">このチュートリアルでは、クエリ文字列値を含むリンクを追加しました。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="a5d1f-141">このクエリ文字列値は、select メソッドのパラメーター値として使用しています。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="a5d1f-142">次の[チュートリアル](adding-business-logic-layer.md)では、分離コードファイルのコードをビジネスロジック層とデータアクセス層に移動します。</span><span class="sxs-lookup"><span data-stu-id="a5d1f-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a5d1f-143">[前へ](integrating-jquery-ui.md)
> [次へ](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="a5d1f-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
