---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC コントローラーの概要 (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。 新しいコントローラーを作成し、さまざまな種類のアクションを返す方法について説明します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486922"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="2ae34-104">ASP.NET MVC コントローラーの概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="2ae34-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="2ae34-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="2ae34-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="2ae34-106">このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="2ae34-107">新しいコントローラーを作成し、さまざまな種類のアクション結果を返す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="2ae34-108">このチュートリアルでは、ASP.NET MVC コントローラー、コントローラーアクション、およびアクションの結果について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="2ae34-109">このチュートリアルを完了すると、ユーザーが ASP.NET MVC web サイトと対話する方法を制御するためにコントローラーがどのように使用されるかを理解できます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="2ae34-110">コントローラーについて</span><span class="sxs-lookup"><span data-stu-id="2ae34-110">Understanding Controllers</span></span>

<span data-ttu-id="2ae34-111">MVC コントローラーは、ASP.NET MVC web サイトに対して行われた要求に応答する役割を担います。</span><span class="sxs-lookup"><span data-stu-id="2ae34-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="2ae34-112">各ブラウザー要求は、特定のコントローラーにマップされます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="2ae34-113">たとえば、ブラウザーのアドレスバーに次の URL を入力したとします。</span><span class="sxs-lookup"><span data-stu-id="2ae34-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="2ae34-114">この場合、ProductController という名前のコントローラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="2ae34-115">ProductController は、ブラウザー要求に対する応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="2ae34-116">たとえば、コントローラーが特定のビューをブラウザーに返す場合や、コントローラーがユーザーを別のコントローラーにリダイレクトする場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ae34-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="2ae34-117">リスト1には、ProductController という名前のシンプルなコントローラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2ae34-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="2ae34-118">**Listing1-visual basic**</span><span class="sxs-lookup"><span data-stu-id="2ae34-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="2ae34-119">リスト1からわかるように、コントローラーはクラス (Visual Basic .NET またはC#クラス) にすぎません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="2ae34-120">コントローラーは、基本の System.web. Mvc クラスから派生するクラスです。</span><span class="sxs-lookup"><span data-stu-id="2ae34-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="2ae34-121">コントローラーはこの基本クラスを継承するため、コントローラーはいくつかの便利なメソッドを無料で継承します (これらのメソッドについては後で説明します)。</span><span class="sxs-lookup"><span data-stu-id="2ae34-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="2ae34-122">コントローラーアクションについて</span><span class="sxs-lookup"><span data-stu-id="2ae34-122">Understanding Controller Actions</span></span>

<span data-ttu-id="2ae34-123">コントローラーは、コントローラーアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-123">A controller exposes controller actions.</span></span> <span data-ttu-id="2ae34-124">アクションは、ブラウザーのアドレスバーに特定の URL を入力したときに呼び出されるコントローラー上のメソッドです。</span><span class="sxs-lookup"><span data-stu-id="2ae34-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="2ae34-125">たとえば、次の URL に対して要求を行うとします。</span><span class="sxs-lookup"><span data-stu-id="2ae34-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="2ae34-126">この場合、ProductController クラスで Index () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="2ae34-127">Index () メソッドは、コントローラーアクションの一例です。</span><span class="sxs-lookup"><span data-stu-id="2ae34-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="2ae34-128">コントローラーアクションは、コントローラークラスのパブリックメソッドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ae34-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="2ae34-129">既定では、Visual Basic.NET メソッドはパブリックメソッドです。</span><span class="sxs-lookup"><span data-stu-id="2ae34-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="2ae34-130">コントローラークラスに追加したパブリックメソッドは、コントローラーアクションとして自動的に公開されることに注意してください (コントローラーアクションは、ブラウザーのアドレスバーに適切な URL を入力するだけで、宇宙の任意のユーザーによって呼び出すことができるため、注意する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="2ae34-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="2ae34-131">コントローラーアクションによって満たされる必要がある追加の要件がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="2ae34-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="2ae34-132">コントローラーアクションとして使用されているメソッドをオーバーロードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="2ae34-133">さらに、コントローラーアクションを静的メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="2ae34-134">それ以外の場合は、任意のメソッドをコントローラーアクションとしてのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="2ae34-135">アクションの結果について</span><span class="sxs-lookup"><span data-stu-id="2ae34-135">Understanding Action Results</span></span>

<span data-ttu-id="2ae34-136">コントローラーアクションは、*アクション結果*と呼ばれるものを返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="2ae34-137">アクションの結果は、ブラウザー要求に応じてコントローラーアクションが返すものです。</span><span class="sxs-lookup"><span data-stu-id="2ae34-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="2ae34-138">ASP.NET MVC フレームワークでは、次のようないくつかの種類のアクションの結果をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2ae34-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="2ae34-139">ViewResult-HTML およびマークアップを表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="2ae34-140">EmptyResult-結果を表しません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="2ae34-141">RedirectResult-新しい URL へのリダイレクトを表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="2ae34-142">JsonResult-AJAX アプリケーションで使用できる JavaScript Object Notation の結果を表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="2ae34-143">JavaScriptResult-JavaScript スクリプトを表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="2ae34-144">ContentResult-テキストの結果を表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="2ae34-145">FileContentResult-ダウンロード可能なファイルを表します (バイナリコンテンツを含む)。</span><span class="sxs-lookup"><span data-stu-id="2ae34-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="2ae34-146">FilePathResult-ダウンロード可能なファイル (パスを含む) を表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="2ae34-147">FileStreamResult-ダウンロード可能なファイル (ファイルストリームを含む) を表します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="2ae34-148">これらのアクションの結果はすべて、基本 ActionResult クラスから継承されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="2ae34-149">ほとんどの場合、コントローラーアクションは ViewResult を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="2ae34-150">たとえば、リスト2のインデックスコントローラーアクションは ViewResult を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="2ae34-151">**リスト 2-コントローラーの一覧表示 (vb)**</span><span class="sxs-lookup"><span data-stu-id="2ae34-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="2ae34-152">アクションから ViewResult が返されると、ブラウザーに HTML が返されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="2ae34-153">リスト2の Index () メソッドは、ブラウザーに Index という名前のビューを返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="2ae34-154">リスト2の Index () アクションから ViewResult () が返されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2ae34-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="2ae34-155">代わりに、コントローラーの基底クラスの View () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="2ae34-156">通常、アクションの結果は直接返されません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="2ae34-157">代わりに、コントローラーの基本クラスの次のいずれかのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="2ae34-158">View-ViewResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="2ae34-159">リダイレクト-RedirectResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="2ae34-160">RedirectToAction-RedirectToRouteResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="2ae34-161">RedirectToRoute-RedirectToRouteResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="2ae34-162">Json-JsonResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="2ae34-163">JavaScriptResult-JavaScriptResult を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="2ae34-164">Content-ContentResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="2ae34-165">File-メソッドに渡されたパラメーターに応じて、FileContentResult、FilePathResult、または FileStreamResult を返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="2ae34-166">そのため、ビューをブラウザーに返す場合は、View () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="2ae34-167">コントローラーアクション間でユーザーをリダイレクトする場合は、RedirectToAction () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="2ae34-168">たとえば、リスト3の Details () アクションは、Id パラメーターに値があるかどうかに応じて、ビューを表示するか、ユーザーを Index () アクションにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2ae34-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="2ae34-169">**リスト 3-顧客コントローラー .vb**</span><span class="sxs-lookup"><span data-stu-id="2ae34-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="2ae34-170">ContentResult アクションの結果は特殊です。</span><span class="sxs-lookup"><span data-stu-id="2ae34-170">The ContentResult action result is special.</span></span> <span data-ttu-id="2ae34-171">ContentResult アクションの結果を使用して、アクションの結果をプレーンテキストとして返すことができます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="2ae34-172">たとえば、リスト4の Index () メソッドは、HTML としてではなく、プレーンテキストとしてメッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="2ae34-173">**リスト 4-コントローラーのステータスコントローラー**</span><span class="sxs-lookup"><span data-stu-id="2ae34-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="2ae34-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="2ae34-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="2ae34-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="2ae34-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="2ae34-176">StatusController. Index () アクションを呼び出すと、ビューは返されません。</span><span class="sxs-lookup"><span data-stu-id="2ae34-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="2ae34-177">代わりに、生のテキスト "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="2ae34-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="2ae34-178">がブラウザーに返されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-178">is returned to the browser.</span></span>

<span data-ttu-id="2ae34-179">コントローラーアクションが、アクション結果ではない結果 (日付や整数など) を返す場合、結果は ContentResult に自動的にラップされます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="2ae34-180">たとえば、リスト5のワークコントローラーの Index () アクションが呼び出されると、その日付は ContentResult として自動的に返されます。</span><span class="sxs-lookup"><span data-stu-id="2ae34-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="2ae34-181">**リスト 5-ワークコントローラー .vb**</span><span class="sxs-lookup"><span data-stu-id="2ae34-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="2ae34-182">リスト5の Index () アクションは、DateTime オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="2ae34-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="2ae34-183">ASP.NET MVC フレームワークは、DateTime オブジェクトを文字列に変換し、ContentResult の DateTime 値を自動的にラップします。</span><span class="sxs-lookup"><span data-stu-id="2ae34-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="2ae34-184">ブラウザーは、日付と時刻をプレーンテキストとして受け取ります。</span><span class="sxs-lookup"><span data-stu-id="2ae34-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="2ae34-185">まとめ</span><span class="sxs-lookup"><span data-stu-id="2ae34-185">Summary</span></span>

<span data-ttu-id="2ae34-186">このチュートリアルの目的は、ASP.NET MVC コントローラー、コントローラーアクション、およびコントローラーアクションの結果の概念を紹介することでした。</span><span class="sxs-lookup"><span data-stu-id="2ae34-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="2ae34-187">最初のセクションでは、ASP.NET MVC プロジェクトに新しいコントローラーを追加する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="2ae34-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="2ae34-188">次に、コントローラーのパブリックメソッドをコントローラーアクションとして universe に公開する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="2ae34-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="2ae34-189">最後に、コントローラーアクションから返される可能性があるさまざまな種類のアクションの結果について説明しました。</span><span class="sxs-lookup"><span data-stu-id="2ae34-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="2ae34-190">特に、ViewResult、RedirectToActionResult、および ContentResult をコントローラーアクションから返す方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="2ae34-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2ae34-191">[前へ](creating-a-custom-route-constraint-cs.md)
> [次へ](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2ae34-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
