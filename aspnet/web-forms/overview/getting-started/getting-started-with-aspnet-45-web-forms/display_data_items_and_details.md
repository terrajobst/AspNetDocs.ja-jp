---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: データ項目と詳細の表示 |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.7 および Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎を説明します。
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520810"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="5d3ac-103">データ項目と詳細の表示</span><span class="sxs-lookup"><span data-stu-id="5d3ac-103">Display data items and details</span></span>

<span data-ttu-id="5d3ac-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="5d3ac-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="5d3ac-105">このチュートリアルシリーズでは、ASP.NET 4.7 と Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="5d3ac-106">このチュートリアルでは、ASP.NET Web フォームおよび Entity Framework Code First でデータ項目とデータ項目の詳細を表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="5d3ac-107">このチュートリアルは、Wingtip 玩具 Store チュートリアルシリーズの一部として、前の「UI とナビゲーション」チュートリアルに基づいています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="5d3ac-108">このチュートリアルを完了すると、 *Productdetails .aspx*ページに製品が表示され、 *productdetails .aspx*ページに製品の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="5d3ac-109">学習内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-109">You'll learn how to:</span></span>

- <span data-ttu-id="5d3ac-110">データベースから製品を表示するデータコントロールを追加する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="5d3ac-111">データコントロールを選択したデータに接続する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="5d3ac-112">データコントロールを追加して、製品の詳細をデータベースから表示する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="5d3ac-113">クエリ文字列から値を取得し、その値を使用して、データベースから取得されるデータを制限します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="5d3ac-114">このチュートリアルで導入された機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="5d3ac-115">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="5d3ac-115">Model binding</span></span>
- <span data-ttu-id="5d3ac-116">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="5d3ac-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="5d3ac-117">データコントロールを追加する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-117">Add a data control</span></span>

<span data-ttu-id="5d3ac-118">サーバーコントロールにデータをバインドするには、いくつかの異なるオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="5d3ac-119">最も一般的なものは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-119">The most common include:</span></span>

* <span data-ttu-id="5d3ac-120">データソースコントロールの追加</span><span class="sxs-lookup"><span data-stu-id="5d3ac-120">Adding a data source control</span></span>
* <span data-ttu-id="5d3ac-121">手動によるコードの追加</span><span class="sxs-lookup"><span data-stu-id="5d3ac-121">Adding code by hand</span></span>
* <span data-ttu-id="5d3ac-122">モデルバインドの使用</span><span class="sxs-lookup"><span data-stu-id="5d3ac-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="5d3ac-123">データソースコントロールを使用してデータをバインドする</span><span class="sxs-lookup"><span data-stu-id="5d3ac-123">Use a data source control to bind data</span></span>

<span data-ttu-id="5d3ac-124">データソースコントロールを追加すると、データを表示するコントロールにデータソースコントロールをリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="5d3ac-125">この方法では、プログラムによってサーバー側のコントロールをデータソースに接続するのではなく、宣言によって宣言できます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="5d3ac-126">データをバインドするための手作業のコード</span><span class="sxs-lookup"><span data-stu-id="5d3ac-126">Code by hand to bind data</span></span>

<span data-ttu-id="5d3ac-127">手作業でコーディングするには、次の作業が必要です。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="5d3ac-128">値の読み取り</span><span class="sxs-lookup"><span data-stu-id="5d3ac-128">Reading a value</span></span>
2. <span data-ttu-id="5d3ac-129">Null であるかどうかを確認しています</span><span class="sxs-lookup"><span data-stu-id="5d3ac-129">Checking if it's null</span></span>
3. <span data-ttu-id="5d3ac-130">適切な型への変換</span><span class="sxs-lookup"><span data-stu-id="5d3ac-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="5d3ac-131">変換が成功したかどうかのチェック</span><span class="sxs-lookup"><span data-stu-id="5d3ac-131">Checking conversion success</span></span>
5. <span data-ttu-id="5d3ac-132">クエリで値を使用する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-132">Using the value in the query</span></span> 

<span data-ttu-id="5d3ac-133">この方法では、データアクセスロジックを完全に制御できます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="5d3ac-134">モデルバインドを使用したデータのバインド</span><span class="sxs-lookup"><span data-stu-id="5d3ac-134">Use model binding to bind data</span></span>

<span data-ttu-id="5d3ac-135">モデルバインドを使用すると、結果をはるかに少ないコードでバインドできるため、アプリケーション全体で機能を再利用することができます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="5d3ac-136">コード中心のデータアクセスロジックを簡単に操作できるだけでなく、豊富なデータバインディングフレームワークも提供します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="5d3ac-137">製品の表示</span><span class="sxs-lookup"><span data-stu-id="5d3ac-137">Display products</span></span>

<span data-ttu-id="5d3ac-138">このチュートリアルでは、モデルバインドを使用してデータをバインドします。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="5d3ac-139">モデルバインドを使用してデータを選択するようにデータコントロールを構成するには、コントロールの `SelectMethod` プロパティをページのコードのメソッド名に設定します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="5d3ac-140">データコントロールは、ページライフサイクルの適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="5d3ac-141">`DataBind` メソッドを明示的に呼び出す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="5d3ac-142">**ソリューションエクスプローラー**で、 *productlist .aspx*を開きます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="5d3ac-143">既存のマークアップを次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="5d3ac-144">このコードでは、`productList` という名前の**ListView**コントロールを使用して、製品を表示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="5d3ac-145">テンプレートとスタイルを使用して、 **ListView**コントロールでデータを表示する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="5d3ac-146">これは、任意の繰り返し構造のデータに便利です。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="5d3ac-147">この**ListView**の例では、データベースデータを表示するだけでなく、コードを使用せずに、ユーザーがデータを編集、挿入、および削除したり、データを並べ替えたり、ページしたりできるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="5d3ac-148">**ListView**コントロールの `ItemType` プロパティを設定することにより、データバインディング式 `Item` を使用できるようになり、コントロールが厳密に型指定されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="5d3ac-149">前のチュートリアルで説明したように、`ProductName`を指定するなど、IntelliSense を使用して Item オブジェクトの詳細を選択できます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![データ項目と詳細の表示-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="5d3ac-151">また、モデルバインディングを使用して `SelectMethod` 値を指定しています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="5d3ac-152">この値 (`GetProducts`) は、次の手順で製品を表示するために分離コードに追加するメソッドに対応しています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="5d3ac-153">製品を表示するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-153">Add code to display products</span></span>

<span data-ttu-id="5d3ac-154">この手順では、データベースの製品データを**ListView**コントロールに設定するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="5d3ac-155">このコードでは、すべての製品と個々のカテゴリ製品の表示をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="5d3ac-156">**ソリューションエクスプローラー**で、[ *productlist* ] を右クリックし、 **[コードの表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="5d3ac-157">*ProductList.aspx.cs*ファイル内の既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="5d3ac-158">このコードは、 **ListView**コントロールの `ItemType` プロパティが*productlist. .aspx*ページで参照する `GetProducts` メソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="5d3ac-159">結果を特定のデータベースカテゴリに制限するために、コードは*Productlist. .aspx*ページに移動したときに、 *productlist. .aspx*ページに渡されるクエリ文字列値の `categoryId` 値を設定します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="5d3ac-160">`System.Web.ModelBinding` 名前空間の `QueryStringAttribute` クラスは、クエリ文字列変数 `id`の値を取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="5d3ac-161">これにより、モデルバインドは、クエリ文字列の値を実行時に `categoryId` パラメーターにバインドするように指示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="5d3ac-162">有効なカテゴリがクエリ文字列としてページに渡されると、クエリの結果は、`categoryId` 値に一致するデータベース内の製品に制限されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="5d3ac-163">たとえば、製品*リスト .aspx*ページの URL が次のようになっているとします。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="5d3ac-164">このページには、`categoryId` が `1`に等しい製品のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="5d3ac-165">*Productlist .aspx*ページが呼び出されたときにクエリ文字列が含まれていない場合は、すべての製品が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="5d3ac-166">これらのメソッドの値のソースは、*値*プロバイダー ( *QueryString*など) と呼ばれ、使用する値プロバイダーを示すパラメーター属性は、*値プロバイダー属性*(`id`など) と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="5d3ac-167">ASP.NET には、クエリ文字列、cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイルプロパティなど、Web フォームアプリケーションでのユーザー入力のすべての一般的なソースに対して、値プロバイダーとそれに対応する属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="5d3ac-168">カスタム値プロバイダーを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="5d3ac-169">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="5d3ac-169">Run the application</span></span>

<span data-ttu-id="5d3ac-170">今すぐアプリケーションを実行して、すべての製品またはカテゴリの製品を表示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="5d3ac-171">Visual Studio で**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="5d3ac-172">ブラウザーが開き、 *default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="5d3ac-173">製品カテゴリのナビゲーションメニューから **[車両]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="5d3ac-174">*Productlist .aspx*ページには、**車両**カテゴリの製品のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="5d3ac-175">このチュートリアルの後半では、製品の詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-175">Later in this tutorial, you'll display product details.</span></span>  

    ![データ項目と詳細を表示する-自動車](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="5d3ac-177">上部のナビゲーションメニューから **[製品]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="5d3ac-178">ここでも、 *productlist .aspx*ページが表示されますが、今回は製品の一覧全体が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![データ項目と詳細の表示-製品](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="5d3ac-180">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="5d3ac-181">データコントロールを追加して製品の詳細を表示する</span><span class="sxs-lookup"><span data-stu-id="5d3ac-181">Add a data control to display product details</span></span>

<span data-ttu-id="5d3ac-182">次に、前のチュートリアルで追加した*Productdetails .aspx*ページのマークアップを変更して、特定の製品情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="5d3ac-183">**ソリューションエクスプローラー**で、 *productdetails .aspx*を開きます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="5d3ac-184">既存のマークアップを次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="5d3ac-185">このコードでは、 **FormView**コントロールを使用して特定の製品の詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="5d3ac-186">このマークアップは、 *Productlist. .aspx*ページでのデータの表示に使用されるメソッドなどのメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="5d3ac-187">**FormView**コントロールは、データソースから一度に1つのレコードを表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="5d3ac-188">**FormView**コントロールを使用する場合は、データバインド値を表示および編集するためのテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="5d3ac-189">これらのテンプレートには、フォームの外観と機能を定義するコントロール、バインド式、および書式設定が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="5d3ac-190">前のマークアップをデータベースに接続するには、追加のコードが必要です。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="5d3ac-191">**ソリューションエクスプローラー**で、[ *productdetails. .aspx* ] を右クリックし、 **[コードの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="5d3ac-192">*ProductDetails.aspx.cs*ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="5d3ac-193">既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="5d3ac-194">このコードでは、"`productID`" クエリ文字列値があるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="5d3ac-195">有効なクエリ文字列値が見つかった場合は、照合製品が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="5d3ac-196">クエリ文字列が見つからない場合、またはその値が有効でない場合は、製品は表示されません。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="5d3ac-197">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="5d3ac-197">Run the application</span></span>

<span data-ttu-id="5d3ac-198">これで、アプリケーションを実行して、製品 ID に基づいて表示される個々の製品を確認できます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="5d3ac-199">Visual Studio で**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="5d3ac-200">ブラウザーが開き、 *default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="5d3ac-201">カテゴリナビゲーションメニューから **[ボート]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="5d3ac-202">*Productlist .aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="5d3ac-203">製品リストから **[用紙ボート]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="5d3ac-204">*Productdetails .aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![データ項目と詳細の表示-製品](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="5d3ac-206">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d3ac-207">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="5d3ac-207">Additional resources</span></span>

[<span data-ttu-id="5d3ac-208">モデルバインドと web フォームを使用したデータの取得と表示</span><span class="sxs-lookup"><span data-stu-id="5d3ac-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="5d3ac-209">次のステップ</span><span class="sxs-lookup"><span data-stu-id="5d3ac-209">Next steps</span></span>

<span data-ttu-id="5d3ac-210">このチュートリアルでは、製品と製品の詳細を表示するためのマークアップとコードを追加しました。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="5d3ac-211">厳密に型指定されたデータコントロール、モデルバインディング、および値プロバイダーについて学習しました。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="5d3ac-212">次のチュートリアルでは、Wingtip Toys サンプルアプリケーションにショッピングカートを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d3ac-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="5d3ac-213">[前へ](ui_and_navigation.md)
> [次へ](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="5d3ac-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
