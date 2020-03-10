---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC ルーティングの概要 (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがブラウザー要求をコントローラーアクションにマップする方法を示しています。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486898"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="331c7-103">ASP.NET MVC ルーティング概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="331c7-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="331c7-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="331c7-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="331c7-105">このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがブラウザー要求をコントローラーアクションにマップする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="331c7-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="331c7-106">このチュートリアルでは、 *ASP.NET Routing*という名前のすべての ASP.NET MVC アプリケーションの重要な機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="331c7-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="331c7-107">ASP.NET ルーティングモジュールは、受信ブラウザー要求を特定の MVC コントローラーアクションにマップする役割を担います。</span><span class="sxs-lookup"><span data-stu-id="331c7-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="331c7-108">このチュートリアルを終了すると、標準のルートテーブルが要求をコントローラーアクションにどのようにマップするかを理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="331c7-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="331c7-109">既定のルートテーブルを使用する</span><span class="sxs-lookup"><span data-stu-id="331c7-109">Using the Default Route Table</span></span>

<span data-ttu-id="331c7-110">新しい ASP.NET MVC アプリケーションを作成する場合、アプリケーションは既に ASP.NET Routing を使用するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="331c7-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="331c7-111">ASP.NET ルーティングは2か所で設定されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="331c7-112">まず、アプリケーションの Web 構成ファイル (web.config ファイル) で ASP.NET ルーティングが有効になっています。</span><span class="sxs-lookup"><span data-stu-id="331c7-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="331c7-113">ルーティングに関連する構成ファイルには、次の4つのセクションがあります。-system.servicemodel セクション、system.web. httpHandlers セクション、system.webserver. modules セクション、および system.webserver. ハンドラーセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="331c7-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="331c7-114">これらのセクションを削除しないように注意してください。これらのセクションでは、ルーティングが機能しなくなります。</span><span class="sxs-lookup"><span data-stu-id="331c7-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="331c7-115">2つ目は、さらに重要なのは、アプリケーションの global.asax ファイルにルートテーブルを作成することです。</span><span class="sxs-lookup"><span data-stu-id="331c7-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="331c7-116">Global.asax ファイルは、ASP.NET アプリケーションライフサイクルイベントのイベントハンドラーを含む特殊なファイルです。</span><span class="sxs-lookup"><span data-stu-id="331c7-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="331c7-117">ルートテーブルは、アプリケーションの開始イベント時に作成されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="331c7-118">リスト1のファイルには、ASP.NET MVC アプリケーションの既定の global.asax ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="331c7-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="331c7-119">**リスト 1-global.asax**</span><span class="sxs-lookup"><span data-stu-id="331c7-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="331c7-120">MVC アプリケーションを初めて起動すると、アプリケーション\_Start () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="331c7-121">次に、このメソッドは RegisterRoutes () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="331c7-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="331c7-122">RegisterRoutes () メソッドは、ルートテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="331c7-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="331c7-123">既定のルートテーブルには、1つのルートが含まれています (既定)。</span><span class="sxs-lookup"><span data-stu-id="331c7-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="331c7-124">既定のルートは、URL の最初のセグメントをコントローラー名に、URL の2番目のセグメントをコントローラーアクションに、3番目のセグメントを**id**という名前のパラメーターにマップします。</span><span class="sxs-lookup"><span data-stu-id="331c7-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="331c7-125">Web ブラウザーのアドレスバーに次の URL を入力したとします。</span><span class="sxs-lookup"><span data-stu-id="331c7-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="331c7-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="331c7-126">/Home/Index/3</span></span>

<span data-ttu-id="331c7-127">既定のルートは、この URL を次のパラメーターにマップします。</span><span class="sxs-lookup"><span data-stu-id="331c7-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="331c7-128">controller = Home</span><span class="sxs-lookup"><span data-stu-id="331c7-128">controller = Home</span></span>

- <span data-ttu-id="331c7-129">action = Index</span><span class="sxs-lookup"><span data-stu-id="331c7-129">action = Index</span></span>

- <span data-ttu-id="331c7-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="331c7-130">id = 3</span></span>

<span data-ttu-id="331c7-131">URL/Home/Index/3 を要求すると、次のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="331c7-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="331c7-132">HomeController.Index(3)</span></span>

<span data-ttu-id="331c7-133">既定のルートには、3つのパラメーターすべての既定値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="331c7-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="331c7-134">コントローラーを指定しない場合、コントローラーパラメーターの既定値は**Home**です。</span><span class="sxs-lookup"><span data-stu-id="331c7-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="331c7-135">アクションを指定しない場合、アクションパラメーターの既定値は**Index**です。</span><span class="sxs-lookup"><span data-stu-id="331c7-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="331c7-136">最後に、id を指定しない場合、id パラメーターの既定値は空の文字列になります。</span><span class="sxs-lookup"><span data-stu-id="331c7-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="331c7-137">既定のルートでは、Url をコントローラーアクションにマップする方法の例をいくつか見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="331c7-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="331c7-138">ブラウザーのアドレスバーに次の URL を入力したとします。</span><span class="sxs-lookup"><span data-stu-id="331c7-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="331c7-139">/Home</span><span class="sxs-lookup"><span data-stu-id="331c7-139">/Home</span></span>

<span data-ttu-id="331c7-140">既定のルートパラメーターの既定値が指定されているため、この URL を入力すると、リスト2の HomeController クラスの Index () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="331c7-141">**リスティング 2-HomeController**</span><span class="sxs-lookup"><span data-stu-id="331c7-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="331c7-142">リスト2では、HomeController クラスに、Id という名前の単一のパラメーターを受け取る Index () という名前のメソッドが含まれています。URL/Home を使用すると、Id パラメーターの値として Nothing を指定して Index () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="331c7-143">MVC フレームワークがコントローラーアクションを呼び出す方法により、URL/Home も、リスト3の HomeController クラスの Index () メソッドに一致します。</span><span class="sxs-lookup"><span data-stu-id="331c7-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="331c7-144">**リスト 3-HomeController (パラメーターなしのインデックスアクション)**</span><span class="sxs-lookup"><span data-stu-id="331c7-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="331c7-145">リスト3の Index () メソッドは、パラメーターを受け取りません。</span><span class="sxs-lookup"><span data-stu-id="331c7-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="331c7-146">URL/Home によって、この Index () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="331c7-147">また、URL /Home/Index/3 は、(Id は無視されます) このメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="331c7-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="331c7-148">また、URL/Home は、リスト4の HomeController クラスの Index () メソッドにも一致します。</span><span class="sxs-lookup"><span data-stu-id="331c7-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="331c7-149">**リスト 4-HomeController (null 値を許容するパラメーターを持つインデックスアクション)**</span><span class="sxs-lookup"><span data-stu-id="331c7-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="331c7-150">リスティング4では、Index () メソッドに1つの整数パラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="331c7-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="331c7-151">パラメーターは null 許容型パラメーターであるため (値は Nothing でもかまいません)、エラーを発生させることなくインデックス () を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="331c7-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="331c7-152">最後に、URL/Home を使用してリスト5の Index () メソッドを呼び出すと、Id パラメーターが null 許容パラメーターで*はない*ため、例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="331c7-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="331c7-153">Index () メソッドを呼び出そうとすると、図1にエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="331c7-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="331c7-154">**リスト 5-HomeController (Id パラメーターを持つインデックスアクション)**</span><span class="sxs-lookup"><span data-stu-id="331c7-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="331c7-155">[パラメーター値を要求するコントローラーアクションを呼び出す ![](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="331c7-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="331c7-156">**図 01**: パラメーター値を必要とするコントローラーアクションを呼び出す ([クリックすると、フルサイズのイメージが表示](asp-net-mvc-routing-overview-vb/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="331c7-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="331c7-157">URL /Home/Index/3 は一方で、リスト 5 でインデックスのコント ローラー アクションでうまくいきます。</span><span class="sxs-lookup"><span data-stu-id="331c7-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="331c7-158">要求/Home/Index/3 は、値が3の Id パラメーターを使用して Index () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="331c7-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="331c7-159">まとめ</span><span class="sxs-lookup"><span data-stu-id="331c7-159">Summary</span></span>

<span data-ttu-id="331c7-160">このチュートリアルの目的は、ASP.NET ルーティングの概要を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="331c7-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="331c7-161">新しい ASP.NET MVC アプリケーションを使用して取得した既定のルートテーブルを調べます。</span><span class="sxs-lookup"><span data-stu-id="331c7-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="331c7-162">既定のルートでは、Url をコントローラーアクションにマップする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="331c7-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="331c7-163">[前へ](creating-an-action-cs.md)
> [次へ](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="331c7-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
