---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: モデルバインドと web フォームを使用するプロジェクトへのビジネスロジック層の追加 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515428"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="320be-104">モデルバインドと web フォームを使用するプロジェクトへのビジネスロジック層の追加</span><span class="sxs-lookup"><span data-stu-id="320be-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="320be-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="320be-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="320be-106">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="320be-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="320be-107">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="320be-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="320be-108">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="320be-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="320be-109">このチュートリアルでは、ビジネスロジック層でモデルバインドを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="320be-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="320be-110">現在のページ以外のオブジェクトを使用してデータメソッドを呼び出すように指定するには、OnCallingDataMethods メンバーを設定します。</span><span class="sxs-lookup"><span data-stu-id="320be-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="320be-111">このチュートリアルは、シリーズの[前](retrieving-data.md)のパートで作成したプロジェクトに基づいています。</span><span class="sxs-lookup"><span data-stu-id="320be-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="320be-112">完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="320be-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="320be-113">ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。</span><span class="sxs-lookup"><span data-stu-id="320be-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="320be-114">このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="320be-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="320be-115">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="320be-115">What you'll build</span></span>

<span data-ttu-id="320be-116">モデルバインドを使用すると、web ページの分離コードファイルまたは別のビジネスロジッククラスにデータの相互作用コードを配置できます。</span><span class="sxs-lookup"><span data-stu-id="320be-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="320be-117">前のチュートリアルでは、分離コードファイルを使用してデータ相互作用コードを記述する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="320be-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="320be-118">この方法は小規模なサイトに対しては機能しますが、大規模なサイトを維持する場合は、コードの繰り返しにより困難になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="320be-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="320be-119">また、抽象化レイヤーが存在しないため、分離コードファイルに存在するコードをプログラムによってテストするのは非常に困難です。</span><span class="sxs-lookup"><span data-stu-id="320be-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="320be-120">データ相互作用コードを一元化するために、データと対話するためのすべてのロジックを含むビジネスロジック層を作成できます。</span><span class="sxs-lookup"><span data-stu-id="320be-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="320be-121">次に、web ページからビジネスロジックレイヤーを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="320be-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="320be-122">このチュートリアルでは、前のチュートリアルで作成したすべてのコードをビジネスロジックレイヤーに移動し、そのコードをページから使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="320be-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="320be-123">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="320be-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="320be-124">分離コードファイルからビジネスロジック層にコードを移動する</span><span class="sxs-lookup"><span data-stu-id="320be-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="320be-125">ビジネスロジック層のメソッドを呼び出すようにデータバインドコントロールを変更します。</span><span class="sxs-lookup"><span data-stu-id="320be-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="320be-126">ビジネスロジックレイヤーの作成</span><span class="sxs-lookup"><span data-stu-id="320be-126">Create business logic layer</span></span>

<span data-ttu-id="320be-127">次に、web ページから呼び出されるクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="320be-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="320be-128">このクラスのメソッドは、前のチュートリアルで使用したメソッドに似ており、値プロバイダー属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="320be-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="320be-129">まず、 **BLL**という名前の新しいフォルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="320be-129">First, add a new folder called **BLL**.</span></span>

![フォルダーの追加](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="320be-131">[BLL] フォルダーで、 **SchoolBL.cs**という名前の新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="320be-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="320be-132">これには、分離コードファイルにもともと存在していたすべてのデータ操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="320be-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="320be-133">メソッドは分離コードファイルのメソッドとほぼ同じですが、いくつかの変更が含まれます。</span><span class="sxs-lookup"><span data-stu-id="320be-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="320be-134">注意する必要がある最も重要な変更は、 **Page**クラスのインスタンス内からコードを実行しなくなったことです。</span><span class="sxs-lookup"><span data-stu-id="320be-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="320be-135">Page クラスには、 **TryUpdateModel**メソッドと**modelstate**プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="320be-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="320be-136">このコードをビジネスロジック層に移動すると、これらのメンバーを呼び出すためのページクラスのインスタンスがなくなります。</span><span class="sxs-lookup"><span data-stu-id="320be-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="320be-137">この問題を回避するには、TryUpdateModel または ModelState にアクセスするすべてのメソッドに**Modelmethodcontext**パラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="320be-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="320be-138">この ModelMethodContext パラメーターを使用して TryUpdateModel を呼び出すか、ModelState を取得します。</span><span class="sxs-lookup"><span data-stu-id="320be-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="320be-139">この新しいパラメーターを考慮するために、web ページ内の何も変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="320be-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="320be-140">SchoolBL.cs のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="320be-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="320be-141">既存のページを更新してビジネスロジックレイヤーからデータを取得する</span><span class="sxs-lookup"><span data-stu-id="320be-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="320be-142">最後に、分離コードファイルのクエリを使用して、ビジネスロジックレイヤーを使用するように、ページの Student、AddStudent .aspx、および course を変換します。</span><span class="sxs-lookup"><span data-stu-id="320be-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="320be-143">Students、AddStudent、および course の分離コードファイルで、次のクエリメソッドを削除またはコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="320be-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="320be-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="320be-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="320be-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="320be-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="320be-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="320be-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="320be-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="320be-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="320be-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="320be-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="320be-149">データ操作に関連するコードが分離コードファイルにないはずです。</span><span class="sxs-lookup"><span data-stu-id="320be-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="320be-150">**OnCallingDataMethods**イベントハンドラーを使用すると、データメソッドに使用するオブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="320be-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="320be-151">Student で、そのイベントハンドラーの値を追加し、ビジネスロジッククラスのメソッドの名前にデータメソッドの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="320be-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="320be-152">Student の分離コードファイルで、CallingDataMethods イベントのイベントハンドラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="320be-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="320be-153">このイベントハンドラーでは、データ操作のビジネスロジッククラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="320be-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="320be-154">AddStudent .aspx で、同様の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="320be-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="320be-155">Course .aspx で、同様の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="320be-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="320be-156">アプリケーションを実行して、すべてのページが以前と同じように機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="320be-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="320be-157">検証ロジックも正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="320be-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="320be-158">まとめ</span><span class="sxs-lookup"><span data-stu-id="320be-158">Conclusion</span></span>

<span data-ttu-id="320be-159">このチュートリアルでは、データアクセス層とビジネスロジック層を使用するようにアプリケーションを再構築します。</span><span class="sxs-lookup"><span data-stu-id="320be-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="320be-160">データ操作の現在のページではないオブジェクトをデータコントロールが使用するように指定しました。</span><span class="sxs-lookup"><span data-stu-id="320be-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="320be-161">前へ</span><span class="sxs-lookup"><span data-stu-id="320be-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
