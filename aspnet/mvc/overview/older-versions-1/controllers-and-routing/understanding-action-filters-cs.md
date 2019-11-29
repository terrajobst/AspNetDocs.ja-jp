---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: アクションフィルターについC#て () |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、アクションフィルターについて説明することです。 アクションフィルターは、コントローラーアクションまたはコントローラー全体に適用できる属性です...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590092"
---
# <a name="understanding-action-filters-c"></a><span data-ttu-id="9c6bd-104">アクション フィルターについて理解する (C#)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-104">Understanding Action Filters (C#)</span></span>

<span data-ttu-id="9c6bd-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9c6bd-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="9c6bd-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="9c6bd-107">このチュートリアルの目的は、アクションフィルターについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="9c6bd-108">アクションフィルターは、アクションが実行される方法を変更するコントローラーアクション (またはコントローラー全体) に適用可能な属性です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="9c6bd-109">アクションフィルターについて</span><span class="sxs-lookup"><span data-stu-id="9c6bd-109">Understanding Action Filters</span></span>

<span data-ttu-id="9c6bd-110">このチュートリアルの目的は、アクションフィルターについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="9c6bd-111">アクションフィルターは、アクションが実行される方法を変更するコントローラーアクション (またはコントローラー全体) に適用可能な属性です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="9c6bd-112">ASP.NET MVC フレームワークには、いくつかのアクションフィルターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="9c6bd-113">OutputCache –このアクションフィルターは、指定された時間だけコントローラーアクションの出力をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="9c6bd-114">HandleError –このアクションフィルターは、コントローラーアクションの実行時に発生したエラーを処理します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="9c6bd-115">承認–このアクションフィルターを使用すると、特定のユーザーまたはロールへのアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="9c6bd-116">独自のカスタムアクションフィルターを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="9c6bd-117">たとえば、カスタム認証システムを実装するためにカスタムアクションフィルターを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="9c6bd-118">または、コントローラーアクションによって返されるビューデータを変更するアクションフィルターを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="9c6bd-119">このチュートリアルでは、最初からアクションフィルターを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="9c6bd-120">Visual Studio の [出力] ウィンドウに対するアクションの処理のさまざまな段階をログに記録するログアクションフィルターを作成します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="9c6bd-121">アクションフィルターの使用</span><span class="sxs-lookup"><span data-stu-id="9c6bd-121">Using an Action Filter</span></span>

<span data-ttu-id="9c6bd-122">アクションフィルターは属性です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-122">An action filter is an attribute.</span></span> <span data-ttu-id="9c6bd-123">ほとんどのアクションフィルターは、個々のコントローラーアクションまたはコントローラー全体に適用できます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="9c6bd-124">たとえば、リスト1のデータコントローラーは、現在の時刻を返す `Index()` という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="9c6bd-125">この操作は、`OutputCache` アクションフィルターで修飾されています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="9c6bd-126">このフィルターを使用すると、アクションによって返される値が10秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="9c6bd-127">**リスト1– `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="9c6bd-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="9c6bd-128">ブラウザーのアドレスバーに/Data/Index URL を入力して [更新] ボタンを複数回押すことによって `Index()` アクションを繰り返し呼び出すと、10秒間は同じ時間が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="9c6bd-129">`Index()` アクションの出力は10秒間キャッシュされます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="9c6bd-130">[![キャッシュ時間](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="9c6bd-131">**図 01**: キャッシュされた時間 ([クリックすると、フルサイズの画像が表示](understanding-action-filters-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>

<span data-ttu-id="9c6bd-132">リスト1では、1つのアクションフィルター (`OutputCache` アクションフィルター) が `Index()` メソッドに適用されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="9c6bd-133">必要に応じて、同じアクションに複数のアクションフィルターを適用できます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="9c6bd-134">たとえば、`OutputCache` と `HandleError` の両方のアクションフィルターを同じアクションに適用することができます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="9c6bd-135">リスト1では、`OutputCache` アクションフィルターが `Index()` アクションに適用されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="9c6bd-136">また、この属性を `DataController` クラス自体に適用することもできます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="9c6bd-137">その場合、コントローラーによって公開されたアクションによって返される結果は10秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="9c6bd-138">さまざまな種類のフィルター</span><span class="sxs-lookup"><span data-stu-id="9c6bd-138">The Different Types of Filters</span></span>

<span data-ttu-id="9c6bd-139">ASP.NET MVC フレームワークでは、次の4種類のフィルターがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="9c6bd-140">承認フィルター– `IAuthorizationFilter` 属性を実装します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="9c6bd-141">アクションフィルター– `IActionFilter` 属性を実装します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="9c6bd-142">結果フィルター– `IResultFilter` 属性を実装します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="9c6bd-143">例外フィルター– `IExceptionFilter` 属性を実装します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="9c6bd-144">フィルターは、上記の順序で実行されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="9c6bd-145">たとえば、承認フィルターは常に実行され、他のすべての種類のフィルターの後に常に例外フィルターが実行されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="9c6bd-146">承認フィルターは、コントローラーアクションの認証と承認を実装するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="9c6bd-147">たとえば、承認フィルターは、承認フィルターの一例です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="9c6bd-148">アクションフィルターには、コントローラーアクションの実行前と実行後に実行されるロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="9c6bd-149">たとえば、アクションフィルターを使用して、コントローラーアクションが返すビューデータを変更できます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="9c6bd-150">結果フィルターには、ビューの結果が実行される前後に実行されるロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="9c6bd-151">たとえば、ビューがブラウザーに表示される直前に、ビューの結果を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="9c6bd-152">例外フィルターは、実行するフィルターの最後の種類です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="9c6bd-153">例外フィルターを使用して、コントローラーアクションまたはコントローラーアクションの結果によって発生するエラーを処理できます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="9c6bd-154">また、例外フィルターを使用してエラーをログに記録することもできます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="9c6bd-155">それぞれの種類のフィルターは、特定の順序で実行されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="9c6bd-156">同じ種類のフィルターを実行する順序を制御する場合は、フィルターの [順序] プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="9c6bd-157">すべてのアクションフィルターの基本クラスは `System.Web.Mvc.FilterAttribute` クラスです。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="9c6bd-158">特定の種類のフィルターを実装する場合は、基本フィルタークラスを継承するクラスを作成し、1つ以上の `IAuthorizationFilter`、`IActionFilter`、`IResultFilter`、または `IExceptionFilter` インターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="9c6bd-159">基本 ActionFilterAttribute クラス</span><span class="sxs-lookup"><span data-stu-id="9c6bd-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="9c6bd-160">カスタムアクションフィルターを簡単に実装できるようにするために、ASP.NET MVC フレームワークには基本 `ActionFilterAttribute` クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="9c6bd-161">このクラスは、`IActionFilter` インターフェイスと `IResultFilter` インターフェイスの両方を実装し、`Filter` クラスから継承します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="9c6bd-162">ここでは、完全に一致していない用語について説明します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="9c6bd-163">技術的には、ActionFilterAttribute クラスを継承するクラスは、アクションフィルターと結果フィルターの両方です。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="9c6bd-164">ただし、厳密な意味では、ASP.NET MVC フレームワークの任意の種類のフィルターを参照するために、word アクションフィルターが使用されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="9c6bd-165">基本 `ActionFilterAttribute` クラスには、オーバーライドできる次のメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="9c6bd-166">OnActionExecuting –コントローラーアクションが実行される前に、このメソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="9c6bd-167">OnActionExecuted –このメソッドは、コントローラーアクションが実行された後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="9c6bd-168">OnResultExecuting –コントローラーアクションの結果が実行される前に、このメソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="9c6bd-169">OnResultExecuted –このメソッドは、コントローラーアクションの結果が実行された後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="9c6bd-170">次のセクションでは、これらのさまざまな方法を実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="9c6bd-171">ログアクションフィルターの作成</span><span class="sxs-lookup"><span data-stu-id="9c6bd-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="9c6bd-172">カスタムアクションフィルターを作成する方法を説明するために、Visual Studio の [出力] ウィンドウへのコントローラーアクションの処理の段階をログに記録するカスタムアクションフィルターを作成します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="9c6bd-173">この `LogActionFilter` は、リスト2に含まれています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="9c6bd-174">**リスト2– `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="9c6bd-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="9c6bd-175">リスト2では、`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`、および `OnResultExecuted()` の各メソッドはすべて、`Log()` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="9c6bd-176">メソッドの名前と現在のルートデータが `Log()` メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="9c6bd-177">`Log()` メソッドは、Visual Studio の出力ウィンドウにメッセージを書き込みます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="9c6bd-178">[Visual Studio の出力ウィンドウに書き込む ![](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="9c6bd-179">**図 02**: Visual Studio の出力ウィンドウへの書き込み ([クリックすると、フルサイズの画像が表示](understanding-action-filters-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>

<span data-ttu-id="9c6bd-180">リスト3の Home コントローラーは、ログアクションフィルターをコントローラークラス全体に適用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="9c6bd-181">Home コントローラーによって公開されているアクションのいずれかが呼び出されるたびに、`Index()` メソッドまたは `About()` メソッドのいずれかによって、アクションを処理する段階が Visual Studio の出力ウィンドウに記録されます。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="9c6bd-182">**リスト3– `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="9c6bd-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="9c6bd-183">要約</span><span class="sxs-lookup"><span data-stu-id="9c6bd-183">Summary</span></span>

<span data-ttu-id="9c6bd-184">このチュートリアルでは、ASP.NET MVC アクションフィルターについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="9c6bd-185">4種類のフィルター (承認フィルター、アクションフィルター、結果フィルター、例外フィルター) について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="9c6bd-186">また、基本 `ActionFilterAttribute` クラスについても学習しました。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="9c6bd-187">最後に、簡単なアクションフィルターを実装する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="9c6bd-188">ここでは、Visual Studio の出力ウィンドウへのコントローラーアクションの処理の段階をログに記録するログアクションフィルターを作成しました。</span><span class="sxs-lookup"><span data-stu-id="9c6bd-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9c6bd-189">[前へ](asp-net-mvc-routing-overview-cs.md)
> [次へ](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9c6bd-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
