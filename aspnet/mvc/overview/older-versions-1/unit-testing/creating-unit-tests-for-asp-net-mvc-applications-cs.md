---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: ASP.NET MVC アプリケーションの単体テストを作成C#する () |Microsoft Docs
author: StephenWalther
description: コントローラーアクションの単体テストを作成する方法について説明します。 このチュートリアルでは、Stephen Walther はコントローラーアクションが parti を返すかどうかをテストする方法を示しています。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595302"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="ccc2e-104">ASP.NET MVC アプリケーションの単体テストを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="ccc2e-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="ccc2e-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="ccc2e-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="ccc2e-107">コントローラーアクションの単体テストを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="ccc2e-108">このチュートリアルでは、Stephen Walther は、コントローラーアクションが特定のビューを返すか、特定のデータセットを返すか、または別の種類のアクション結果を返すかをテストする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="ccc2e-109">このチュートリアルの目的は、ASP.NET MVC アプリケーションでコントローラーの単体テストを作成する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="ccc2e-110">ここでは、3種類の単体テストを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="ccc2e-111">コントローラーアクションによって返されるビューをテストする方法、コントローラーアクションによって返されるビューデータをテストする方法、1つのコントローラーアクションが2番目のコントローラーアクションにリダイレクトするかどうかをテストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="ccc2e-112">テスト対象のコントローラーを作成しています</span><span class="sxs-lookup"><span data-stu-id="ccc2e-112">Creating the Controller under Test</span></span>

<span data-ttu-id="ccc2e-113">まず、テストするコントローラーを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="ccc2e-114">`ProductController`という名前のコントローラーは、リスト1に含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="ccc2e-115">**リスト1– `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="ccc2e-116">`ProductController` には、`Index()` と `Details()`という2つのアクションメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="ccc2e-117">どちらのアクションメソッドもビューを返します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-117">Both action methods return a view.</span></span> <span data-ttu-id="ccc2e-118">`Details()` アクションでは、Id という名前のパラメーターを受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="ccc2e-119">コントローラーによって返されるビューをテストする</span><span class="sxs-lookup"><span data-stu-id="ccc2e-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="ccc2e-120">`ProductController` が正しいビューを返すかどうかをテストするとします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="ccc2e-121">`ProductController.Details()` アクションが呼び出されたときに、詳細ビューが返されるようにします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="ccc2e-122">リスト2のテストクラスには、`ProductController.Details()` アクションによって返されたビューをテストするための単体テストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="ccc2e-123">**リスト2– `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="ccc2e-124">リスト2のクラスには、`TestDetailsView()`という名前のテストメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="ccc2e-125">このメソッドには3行のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-125">This method contains three lines of code.</span></span> <span data-ttu-id="ccc2e-126">コードの1行目では、`ProductController` クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="ccc2e-127">コードの2行目では、コントローラーの `Details()` アクションメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="ccc2e-128">最後に、コードの最後の行で、`Details()` アクションによって返されるビューが詳細ビューであるかどうかをチェックします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="ccc2e-129">`ViewResult.ViewName` プロパティは、コントローラーによって返されるビューの名前を表します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="ccc2e-130">このプロパティのテストに関する大きな警告が1つあります。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-130">One big warning about testing this property.</span></span> <span data-ttu-id="ccc2e-131">コントローラーがビューを返すには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="ccc2e-132">コントローラーは、次のようなビューを明示的に返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="ccc2e-133">また、ビューの名前は、次のようにコントローラーアクションの名前から推論することもできます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="ccc2e-134">このコントローラーアクションは、`Details`という名前のビューも返します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="ccc2e-135">ただし、ビューの名前はアクション名から推測されます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="ccc2e-136">ビュー名をテストする場合は、コントローラーアクションからビュー名を明示的に返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="ccc2e-137">リスト2で単体テストを実行するには、 **Ctrl + R キー**の組み合わせを入力するか、 **[ソリューション内のすべてのテストを実行]** ボタン (図1を参照) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="ccc2e-138">テストに合格すると、図2の [テスト結果] ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="ccc2e-139">[ソリューション内のすべてのテストを実行 ![](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="ccc2e-140">**図 01**: ソリューション内のすべてのテストを実行[する (クリックすると、フルサイズのイメージが表示](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png)される)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>

<span data-ttu-id="ccc2e-141">[![成功しました。](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="ccc2e-142">**図 02**: 成功!</span><span class="sxs-lookup"><span data-stu-id="ccc2e-142">**Figure 02**: Success!</span></span> <span data-ttu-id="ccc2e-143">([クリックすると、フルサイズの画像が表示](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png)される)</span><span class="sxs-lookup"><span data-stu-id="ccc2e-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="ccc2e-144">コントローラーによって返されるビューデータのテスト</span><span class="sxs-lookup"><span data-stu-id="ccc2e-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="ccc2e-145">MVC コントローラーは、 *`View Data`* と呼ばれるものを使用してビューにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="ccc2e-146">たとえば、`ProductController Details()` アクションを呼び出すときに、特定の製品の詳細を表示したいとします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="ccc2e-147">その場合は、モデルで定義されている `Product` クラスのインスタンスを作成し、`View Data`を利用して、そのインスタンスを `Details` ビューに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="ccc2e-148">一覧3の変更された `ProductController` には、製品を返す更新された `Details()` アクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="ccc2e-149">**リスト3– `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="ccc2e-150">まず、`Details()` アクションは、ラップトップコンピューターを表す `Product` クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="ccc2e-151">次に、`Product` クラスのインスタンスが、2番目のパラメーターとして `View()` メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="ccc2e-152">単体テストを記述して、予想されるデータがビューデータに含まれているかどうかをテストできます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="ccc2e-153">リスト4の単体テストでは、`ProductController Details()` アクションメソッドを呼び出すと、ラップトップコンピューターを表す製品が返されるかどうかをテストします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="ccc2e-154">**リスト4– `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="ccc2e-155">リスト4では、`TestDetailsView()` メソッドは、`Details()` メソッドを呼び出すことによって返されたビューデータをテストします。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="ccc2e-156">`ViewData` は、`Details()` メソッドを呼び出すことによって返される `ViewResult` のプロパティとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="ccc2e-157">`ViewData.Model` プロパティには、ビューに渡される製品が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="ccc2e-158">このテストでは、単に、ビューデータに含まれている製品に "ラップトップ" という名前が付いていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="ccc2e-159">コントローラーによって返されるアクションの結果のテスト</span><span class="sxs-lookup"><span data-stu-id="ccc2e-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="ccc2e-160">より複雑なコントローラーアクションは、コントローラーアクションに渡されるパラメーターの値に応じて、さまざまな種類のアクション結果を返す可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="ccc2e-161">コントローラーアクションは、`ViewResult`、`RedirectToRouteResult`、`JsonResult`など、さまざまな種類のアクション結果を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="ccc2e-162">たとえば、リスト5の変更された `Details()` アクションでは、有効な製品 Id をアクションに渡すと、`Details` ビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="ccc2e-163">無効な製品 Id (値が1未満の Id) を渡した場合、`Index()` アクションにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="ccc2e-164">**リスト5– `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="ccc2e-165">リスト6の単体テストを使用して、`Details()` アクションの動作をテストできます。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="ccc2e-166">リスト6の単体テストでは、値-1 の Id が `Details()` メソッドに渡されたときに `Index` ビューにリダイレクトされることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="ccc2e-167">**リスト6– `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ccc2e-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="ccc2e-168">コントローラーアクションで `RedirectToAction()` メソッドを呼び出すと、コントローラーアクションは `RedirectToRouteResult`を返します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="ccc2e-169">テストでは、`RedirectToRouteResult` が `Index`という名前のコントローラーアクションにユーザーをリダイレクトするかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="ccc2e-170">要約</span><span class="sxs-lookup"><span data-stu-id="ccc2e-170">Summary</span></span>

<span data-ttu-id="ccc2e-171">このチュートリアルでは、MVC コントローラーアクションの単体テストを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="ccc2e-172">まず、コントローラーアクションによって、右側のビューが返されるかどうかを確認する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="ccc2e-173">`ViewResult.ViewName` プロパティを使用して、ビューの名前を確認する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="ccc2e-174">次に、`View Data`の内容をテストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="ccc2e-175">コントローラーアクションを呼び出した後に `View Data` で正しい製品が返されたかどうかを確認する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="ccc2e-176">最後に、さまざまな種類のアクションの結果がコントローラーアクションから返されたかどうかをテストする方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="ccc2e-177">コントローラーが `ViewResult` と `RedirectToRouteResult`のどちらを返すかをテストする方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ccc2e-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ccc2e-178">次へ</span><span class="sxs-lookup"><span data-stu-id="ccc2e-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
