---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: モデルバインドと web フォームを使用したデータの並べ替え、ページング、フィルター処理 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441064"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="d0809-104">モデルバインドと web フォームを使用したデータの並べ替え、ページング、およびフィルター処理</span><span class="sxs-lookup"><span data-stu-id="d0809-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="d0809-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d0809-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d0809-106">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="d0809-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="d0809-107">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="d0809-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="d0809-108">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="d0809-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="d0809-109">このチュートリアルでは、モデルバインドを使用してデータの並べ替え、ページング、およびフィルター処理を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d0809-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="d0809-110">このチュートリアルは、シリーズの第 1[部](retrieving-data.md)で作成したプロジェクトに基づいています。</span><span class="sxs-lookup"><span data-stu-id="d0809-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="d0809-111">完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="d0809-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="d0809-112">ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。</span><span class="sxs-lookup"><span data-stu-id="d0809-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="d0809-113">このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="d0809-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d0809-114">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="d0809-114">What you'll build</span></span>

<span data-ttu-id="d0809-115">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d0809-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="d0809-116">データの並べ替えとページングを有効にする</span><span class="sxs-lookup"><span data-stu-id="d0809-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="d0809-117">ユーザーによる選択に基づいたデータのフィルター処理を有効にする</span><span class="sxs-lookup"><span data-stu-id="d0809-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="d0809-118">並べ替えの追加</span><span class="sxs-lookup"><span data-stu-id="d0809-118">Add sorting</span></span>

<span data-ttu-id="d0809-119">GridView での並べ替えを有効にするのは非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="d0809-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="d0809-120">Student ファイルでは、GridView で**Allowsorting**を**true**に設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="d0809-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="d0809-121">DataField が自動的に使用されるため、各列に**SortExpression**値を設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d0809-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="d0809-122">GridView は、選択された値によってデータの順序付けを含むようにクエリを変更します。</span><span class="sxs-lookup"><span data-stu-id="d0809-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="d0809-123">下の強調表示されているコードは、並べ替えを有効にするために必要な追加を示しています。</span><span class="sxs-lookup"><span data-stu-id="d0809-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="d0809-124">Web アプリケーションを実行し、異なる列の値で生徒のレコードの並べ替えをテストします。</span><span class="sxs-lookup"><span data-stu-id="d0809-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![生徒の並べ替え](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="d0809-126">ページングの追加</span><span class="sxs-lookup"><span data-stu-id="d0809-126">Add paging</span></span>

<span data-ttu-id="d0809-127">ページングを有効にすることも非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="d0809-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="d0809-128">GridView で、 **Allowpaging**プロパティを**true**に設定し、 **PageSize**プロパティに、各ページに表示するレコード数を設定します。</span><span class="sxs-lookup"><span data-stu-id="d0809-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="d0809-129">このチュートリアルでは、4に設定できます。</span><span class="sxs-lookup"><span data-stu-id="d0809-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="d0809-130">Web アプリケーションを実行すると、レコードが1ページに表示されるレコードが4つ以下の複数のページに分割されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="d0809-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![ページングの追加](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="d0809-132">クエリの遅延実行により、アプリケーションの効率が向上します。</span><span class="sxs-lookup"><span data-stu-id="d0809-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="d0809-133">GridView は、データセット全体を取得するのではなく、現在のページのレコードのみを取得するようにクエリを変更します。</span><span class="sxs-lookup"><span data-stu-id="d0809-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="d0809-134">ユーザー選択でレコードをフィルター処理する</span><span class="sxs-lookup"><span data-stu-id="d0809-134">Filter records by user selection</span></span>

<span data-ttu-id="d0809-135">モデルバインドでは、モデルバインドメソッドでパラメーターの値を設定する方法を指定できるように、いくつかの属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="d0809-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="d0809-136">これらの属性は、 **System.web バインド**名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="d0809-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="d0809-137">それには以下が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d0809-137">They include:</span></span>

- <span data-ttu-id="d0809-138">コントロール</span><span class="sxs-lookup"><span data-stu-id="d0809-138">Control</span></span>
- <span data-ttu-id="d0809-139">クッキー</span><span class="sxs-lookup"><span data-stu-id="d0809-139">Cookie</span></span>
- <span data-ttu-id="d0809-140">Form</span><span class="sxs-lookup"><span data-stu-id="d0809-140">Form</span></span>
- <span data-ttu-id="d0809-141">Profile</span><span class="sxs-lookup"><span data-stu-id="d0809-141">Profile</span></span>
- <span data-ttu-id="d0809-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="d0809-142">QueryString</span></span>
- <span data-ttu-id="d0809-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="d0809-143">RouteData</span></span>
- <span data-ttu-id="d0809-144">セッション</span><span class="sxs-lookup"><span data-stu-id="d0809-144">Session</span></span>
- <span data-ttu-id="d0809-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="d0809-145">UserProfile</span></span>
- <span data-ttu-id="d0809-146">ビューの状態</span><span class="sxs-lookup"><span data-stu-id="d0809-146">ViewState</span></span>

<span data-ttu-id="d0809-147">このチュートリアルでは、コントロールの値を使用して、GridView に表示するレコードをフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="d0809-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="d0809-148">前の手順で作成したクエリメソッドに**コントロール**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="d0809-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="d0809-149">[後](using-query-string-values-to-retrieve-data.md)のチュートリアルでは、パラメーターにクエリ文字列値を使用することを指定するために、 **QueryString**属性をパラメーターに適用します。</span><span class="sxs-lookup"><span data-stu-id="d0809-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="d0809-150">まず、ValidationSummary の上に、表示される学生をフィルター処理するためのドロップダウンリストを追加します。</span><span class="sxs-lookup"><span data-stu-id="d0809-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="d0809-151">分離コードファイルで、コントロールから値を受け取るように選択メソッドを変更し、パラメーターの名前を、値を提供するコントロールの名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0809-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="d0809-152">Control 属性を解決するには、 **System.web binding**名前空間の**using**ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0809-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="d0809-153">次のコードは、ドロップダウンリストの値に基づいて、返されたデータをフィルター処理するための選択メソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="d0809-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="d0809-154">パラメーターの前にコントロール属性を追加すると、このパラメーターの値は同じ名前のコントロールから取得されます。</span><span class="sxs-lookup"><span data-stu-id="d0809-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="d0809-155">Web アプリケーションを実行し、ドロップダウンリストから別の値を選択して、学生の一覧をフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="d0809-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![学生のフィルター処理](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="d0809-157">まとめ</span><span class="sxs-lookup"><span data-stu-id="d0809-157">Conclusion</span></span>

<span data-ttu-id="d0809-158">このチュートリアルでは、データの並べ替えとページングを有効にしました。</span><span class="sxs-lookup"><span data-stu-id="d0809-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="d0809-159">また、コントロールの値によってデータのフィルター処理を有効にしました。</span><span class="sxs-lookup"><span data-stu-id="d0809-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="d0809-160">次の[チュートリアル](integrating-jquery-ui.md)では、JQuery ui ウィジェットを動的データテンプレートに統合することによって、UI を強化します。</span><span class="sxs-lookup"><span data-stu-id="d0809-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d0809-161">[前へ](updating-deleting-and-creating-data.md)
> [次へ](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="d0809-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
