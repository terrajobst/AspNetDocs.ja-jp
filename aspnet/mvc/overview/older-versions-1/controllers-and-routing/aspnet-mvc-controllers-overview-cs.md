---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET MVC コントローラーの概要C#() |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。 新しいコントローラーを作成し、さまざまな種類のアクションを返す方法について説明します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a287b37742400a17c2ed53cfd00bfb053b4f3d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437680"
---
# <a name="aspnet-mvc-controller-overview-c"></a><span data-ttu-id="9ebba-104">ASP.NET MVC コントローラーの概要 (C#)</span><span class="sxs-lookup"><span data-stu-id="9ebba-104">ASP.NET MVC Controller Overview (C#)</span></span>

<span data-ttu-id="9ebba-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9ebba-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9ebba-106">このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="9ebba-107">新しいコントローラーを作成し、さまざまな種類のアクション結果を返す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="9ebba-108">このチュートリアルでは、ASP.NET MVC コントローラー、コントローラーアクション、およびアクションの結果について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="9ebba-109">このチュートリアルを完了すると、ユーザーが ASP.NET MVC web サイトと対話する方法を制御するためにコントローラーがどのように使用されるかを理解できます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="9ebba-110">コントローラーについて</span><span class="sxs-lookup"><span data-stu-id="9ebba-110">Understanding Controllers</span></span>

<span data-ttu-id="9ebba-111">MVC コントローラーは、ASP.NET MVC web サイトに対して行われた要求に応答する役割を担います。</span><span class="sxs-lookup"><span data-stu-id="9ebba-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="9ebba-112">各ブラウザー要求は、特定のコントローラーにマップされます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="9ebba-113">たとえば、ブラウザーのアドレスバーに次の URL を入力したとします。</span><span class="sxs-lookup"><span data-stu-id="9ebba-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="9ebba-114">この場合、ProductController という名前のコントローラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="9ebba-115">ProductController は、ブラウザー要求に対する応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="9ebba-116">たとえば、コントローラーが特定のビューをブラウザーに返す場合や、コントローラーがユーザーを別のコントローラーにリダイレクトする場合があります。</span><span class="sxs-lookup"><span data-stu-id="9ebba-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="9ebba-117">リスト1には、ProductController という名前のシンプルなコントローラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9ebba-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="9ebba-118">**Listing1 (productコントローラー)**</span><span class="sxs-lookup"><span data-stu-id="9ebba-118">**Listing1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

<span data-ttu-id="9ebba-119">リスト1からわかるように、コントローラーはクラス (Visual Basic .NET またはC#クラス) にすぎません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="9ebba-120">コントローラーは、基本の System.web. Mvc クラスから派生するクラスです。</span><span class="sxs-lookup"><span data-stu-id="9ebba-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="9ebba-121">コントローラーはこの基本クラスを継承するため、コントローラーはいくつかの便利なメソッドを無料で継承します (これらのメソッドについては後で説明します)。</span><span class="sxs-lookup"><span data-stu-id="9ebba-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="9ebba-122">コントローラーアクションについて</span><span class="sxs-lookup"><span data-stu-id="9ebba-122">Understanding Controller Actions</span></span>

<span data-ttu-id="9ebba-123">コントローラーは、コントローラーアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-123">A controller exposes controller actions.</span></span> <span data-ttu-id="9ebba-124">アクションは、ブラウザーのアドレスバーに特定の URL を入力したときに呼び出されるコントローラー上のメソッドです。</span><span class="sxs-lookup"><span data-stu-id="9ebba-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="9ebba-125">たとえば、次の URL に対して要求を行うとします。</span><span class="sxs-lookup"><span data-stu-id="9ebba-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="9ebba-126">この場合、ProductController クラスで Index () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="9ebba-127">Index () メソッドは、コントローラーアクションの一例です。</span><span class="sxs-lookup"><span data-stu-id="9ebba-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="9ebba-128">コントローラーアクションは、コントローラークラスのパブリックメソッドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ebba-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="9ebba-129">C#既定では、メソッドはプライベートメソッドです。</span><span class="sxs-lookup"><span data-stu-id="9ebba-129">C# methods, by default, are private methods.</span></span> <span data-ttu-id="9ebba-130">コントローラークラスに追加したパブリックメソッドは、コントローラーアクションとして自動的に公開されることに注意してください (コントローラーアクションは、ブラウザーのアドレスバーに適切な URL を入力するだけで、宇宙の任意のユーザーによって呼び出すことができるため、注意する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="9ebba-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="9ebba-131">コントローラーアクションによって満たされる必要がある追加の要件がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="9ebba-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="9ebba-132">コントローラーアクションとして使用されているメソッドをオーバーロードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="9ebba-133">さらに、コントローラーアクションを静的メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="9ebba-134">それ以外の場合は、任意のメソッドをコントローラーアクションとしてのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="9ebba-135">アクションの結果について</span><span class="sxs-lookup"><span data-stu-id="9ebba-135">Understanding Action Results</span></span>

<span data-ttu-id="9ebba-136">コントローラーアクションは、*アクション結果*と呼ばれるものを返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="9ebba-137">アクションの結果は、ブラウザー要求に応じてコントローラーアクションが返すものです。</span><span class="sxs-lookup"><span data-stu-id="9ebba-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="9ebba-138">ASP.NET MVC フレームワークでは、次のようないくつかの種類のアクションの結果をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="9ebba-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="9ebba-139">ViewResult-HTML およびマークアップを表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="9ebba-140">EmptyResult-結果を表しません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="9ebba-141">RedirectResult-新しい URL へのリダイレクトを表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="9ebba-142">JsonResult-AJAX アプリケーションで使用できる JavaScript Object Notation の結果を表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="9ebba-143">JavaScriptResult-JavaScript スクリプトを表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="9ebba-144">ContentResult-テキストの結果を表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="9ebba-145">FileContentResult-ダウンロード可能なファイルを表します (バイナリコンテンツを含む)。</span><span class="sxs-lookup"><span data-stu-id="9ebba-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="9ebba-146">FilePathResult-ダウンロード可能なファイル (パスを含む) を表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="9ebba-147">FileStreamResult-ダウンロード可能なファイル (ファイルストリームを含む) を表します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="9ebba-148">これらのアクションの結果はすべて、基本 ActionResult クラスから継承されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="9ebba-149">ほとんどの場合、コントローラーアクションは ViewResult を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="9ebba-150">たとえば、リスト2のインデックスコントローラーアクションは ViewResult を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="9ebba-151">**リスト 2-コントローラー (& c)**</span><span class="sxs-lookup"><span data-stu-id="9ebba-151">**Listing 2 - Controllers\BookController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

<span data-ttu-id="9ebba-152">アクションから ViewResult が返されると、ブラウザーに HTML が返されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="9ebba-153">リスト2の Index () メソッドは、ブラウザーに Index という名前のビューを返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="9ebba-154">リスト2の Index () アクションから ViewResult () が返されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9ebba-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="9ebba-155">代わりに、コントローラーの基底クラスの View () メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="9ebba-156">通常、アクションの結果は直接返されません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="9ebba-157">代わりに、コントローラーの基本クラスの次のいずれかのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="9ebba-158">View-ViewResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="9ebba-159">リダイレクト-RedirectResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="9ebba-160">RedirectToAction-RedirectToRouteResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="9ebba-161">RedirectToRoute-RedirectToRouteResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="9ebba-162">Json-JsonResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="9ebba-163">JavaScriptResult-JavaScriptResult を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="9ebba-164">Content-ContentResult アクションの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="9ebba-165">File-メソッドに渡されたパラメーターに応じて、FileContentResult、FilePathResult、または FileStreamResult を返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="9ebba-166">そのため、ビューをブラウザーに返す場合は、View () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="9ebba-167">コントローラーアクション間でユーザーをリダイレクトする場合は、RedirectToAction () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="9ebba-168">たとえば、リスト3の Details () アクションは、Id パラメーターに値があるかどうかに応じて、ビューを表示するか、ユーザーを Index () アクションにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="9ebba-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="9ebba-169">**リスト 3-CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="9ebba-169">**Listing 3 - CustomerController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

<span data-ttu-id="9ebba-170">ContentResult アクションの結果は特殊です。</span><span class="sxs-lookup"><span data-stu-id="9ebba-170">The ContentResult action result is special.</span></span> <span data-ttu-id="9ebba-171">ContentResult アクションの結果を使用して、アクションの結果をプレーンテキストとして返すことができます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="9ebba-172">たとえば、リスト4の Index () メソッドは、HTML としてではなく、プレーンテキストとしてメッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="9ebba-173">**リスト 4-コントローラーの一覧 (& c)**</span><span class="sxs-lookup"><span data-stu-id="9ebba-173">**Listing 4 - Controllers\StatusController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

<span data-ttu-id="9ebba-174">StatusController. Index () アクションを呼び出すと、ビューは返されません。</span><span class="sxs-lookup"><span data-stu-id="9ebba-174">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="9ebba-175">代わりに、生のテキスト "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="9ebba-175">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="9ebba-176">がブラウザーに返されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-176">is returned to the browser.</span></span>

<span data-ttu-id="9ebba-177">コントローラーアクションが、アクション結果ではない結果 (日付や整数など) を返す場合、結果は ContentResult に自動的にラップされます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-177">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="9ebba-178">たとえば、リスト5のワークコントローラーの Index () アクションが呼び出されると、その日付は ContentResult として自動的に返されます。</span><span class="sxs-lookup"><span data-stu-id="9ebba-178">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="9ebba-179">**リスト 5-WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="9ebba-179">**Listing 5 - WorkController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

<span data-ttu-id="9ebba-180">リスト5の Index () アクションは、DateTime オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="9ebba-180">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="9ebba-181">ASP.NET MVC フレームワークは、DateTime オブジェクトを文字列に変換し、ContentResult の DateTime 値を自動的にラップします。</span><span class="sxs-lookup"><span data-stu-id="9ebba-181">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="9ebba-182">ブラウザーは、日付と時刻をプレーンテキストとして受け取ります。</span><span class="sxs-lookup"><span data-stu-id="9ebba-182">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="9ebba-183">まとめ</span><span class="sxs-lookup"><span data-stu-id="9ebba-183">Summary</span></span>

<span data-ttu-id="9ebba-184">このチュートリアルの目的は、ASP.NET MVC コントローラー、コントローラーアクション、およびコントローラーアクションの結果の概念を紹介することでした。</span><span class="sxs-lookup"><span data-stu-id="9ebba-184">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="9ebba-185">最初のセクションでは、ASP.NET MVC プロジェクトに新しいコントローラーを追加する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9ebba-185">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="9ebba-186">次に、コントローラーのパブリックメソッドをコントローラーアクションとして universe に公開する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="9ebba-186">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="9ebba-187">最後に、コントローラーアクションから返される可能性があるさまざまな種類のアクションの結果について説明しました。</span><span class="sxs-lookup"><span data-stu-id="9ebba-187">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="9ebba-188">特に、ViewResult、RedirectToActionResult、および ContentResult をコントローラーアクションから返す方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="9ebba-188">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ebba-189">[前へ](creating-an-action-vb.md)
> [次へ](creating-custom-routes-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9ebba-189">[Previous](creating-an-action-vb.md)
[Next](creating-custom-routes-cs.md)</span></span>
