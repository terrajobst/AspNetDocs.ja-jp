---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: コントローラーとビューを使用して、リスティング/Details UI を実装します。Microsoft Docs
author: microsoft
description: 手順 4. では、モデルを利用してアプリケーションにコントローラーを追加し、ユーザーにデータリスト/詳細ナビゲーションエクスペリエンスを提供する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486220"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="591e1-103">コントローラーとビューを使用し、リスティング/詳細 UI を実装する</span><span class="sxs-lookup"><span data-stu-id="591e1-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="591e1-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="591e1-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="591e1-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="591e1-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="591e1-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順4です。</span><span class="sxs-lookup"><span data-stu-id="591e1-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="591e1-107">手順 4. では、モデルを利用してアプリケーションにコントローラーを追加し、ユーザーにディナーのデータリスト/詳細ナビゲーションエクスペリエンスを提供する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="591e1-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="591e1-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="591e1-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="591e1-109">ステップ 4: コントローラーとビューの操作</span><span class="sxs-lookup"><span data-stu-id="591e1-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="591e1-110">従来の web フレームワーク (classic ASP、PHP、ASP.NET Web Forms など) では、通常、着信 Url はディスク上のファイルにマップされます。</span><span class="sxs-lookup"><span data-stu-id="591e1-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="591e1-111">たとえば、"/-.Aspx" や "/" などの URL の要求は、"Products" ファイルまたは "Products. php" ファイルによって処理される場合があります。</span><span class="sxs-lookup"><span data-stu-id="591e1-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="591e1-112">Web ベースの MVC フレームワークでは、Url が少し異なる方法でサーバーコードにマップされます。</span><span class="sxs-lookup"><span data-stu-id="591e1-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="591e1-113">受信 Url をファイルにマッピングする代わりに、代わりに、Url をクラスのメソッドにマップします。</span><span class="sxs-lookup"><span data-stu-id="591e1-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="591e1-114">これらのクラスは "コントローラー" と呼ばれ、受信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返信するための応答の決定 (HTML の表示、ファイルのダウンロード、別のファイルへのリダイレクトなど) を担当します。URL など)。</span><span class="sxs-lookup"><span data-stu-id="591e1-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="591e1-115">私たちは、このアプリケーションの基本的なモデルを構築したので、次のステップとして、アプリケーションにコントローラーを追加して、ユーザーにサイトのディナーのデータリスト/詳細ナビゲーションエクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="591e1-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="591e1-116">Dinのコントローラーコントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="591e1-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="591e1-117">まず、web プロジェクト内の "Controllers" フォルダーを右クリックし、[ **&gt;コントローラー** ] メニューコマンドを選択します (このコマンドは、Ctrl + M キー、Ctrl + C キーを押して実行することもできます)。</span><span class="sxs-lookup"><span data-stu-id="591e1-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="591e1-118">これにより、[コントローラーの追加] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="591e1-119">新しいコントローラーに "Din" という名前を指定し、[追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="591e1-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="591e1-120">次に、DinnersController.cs ファイルが \ Controllers ディレクトリに追加されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="591e1-121">また、コードエディター内で新しい Dinのコントローラークラスも開きます。</span><span class="sxs-lookup"><span data-stu-id="591e1-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="591e1-122">Index () アクションメソッドと Details () アクションメソッドを Dinのコントローラークラスに追加する</span><span class="sxs-lookup"><span data-stu-id="591e1-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="591e1-123">アプリケーションを使用している訪問者が、今後のディナーの一覧を参照し、リスト内のディナーをクリックして、その詳細を確認できるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="591e1-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="591e1-124">これを行うには、アプリケーションから次の Url を発行します。</span><span class="sxs-lookup"><span data-stu-id="591e1-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="591e1-125">**[URL]**</span><span class="sxs-lookup"><span data-stu-id="591e1-125">**URL**</span></span> | <span data-ttu-id="591e1-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="591e1-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="591e1-127">*ディナー*</span><span class="sxs-lookup"><span data-stu-id="591e1-127">*/Dinners/*</span></span> | <span data-ttu-id="591e1-128">今後のディナーの HTML リストを表示する</span><span class="sxs-lookup"><span data-stu-id="591e1-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="591e1-129">*///[Id]*</span><span class="sxs-lookup"><span data-stu-id="591e1-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="591e1-130">URL 内に埋め込まれている "id" パラメーターによって示される特定のディナーに関する詳細を表示します。これは、データベース内の夕食の Dinid と一致します。</span><span class="sxs-lookup"><span data-stu-id="591e1-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="591e1-131">たとえば、次の例では、Dinid 値が2であるディナーに関する詳細を含む HTML ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="591e1-132">これらの Url の初期実装は、次のような2つのパブリック "アクションメソッド" を Dinのコントローラークラスに追加することによって発行されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="591e1-133">次に、このアプリケーションを実行し、ブラウザーを使用して呼び出します。</span><span class="sxs-lookup"><span data-stu-id="591e1-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="591e1-134">*"/Din" と*いう URL を入力すると、 *Index ()* メソッドが実行され、次の応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="591e1-135">*"/Din/詳細/月"* の URL を入力すると、 *Details ()* メソッドが実行され、次の応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="591e1-136">ASP.NET MVC では、Dinのコントローラークラスを作成し、それらのメソッドを呼び出す方法について疑問に思うかもしれません。</span><span class="sxs-lookup"><span data-stu-id="591e1-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="591e1-137">ここでは、ルーティングのしくみについて簡単に見ていきましょう。</span><span class="sxs-lookup"><span data-stu-id="591e1-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="591e1-138">ASP.NET MVC ルーティングについて</span><span class="sxs-lookup"><span data-stu-id="591e1-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="591e1-139">ASP.NET MVC には、Url をコントローラークラスにマップする方法を柔軟に制御できる強力な URL ルーティングエンジンが用意されています。</span><span class="sxs-lookup"><span data-stu-id="591e1-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="591e1-140">これにより、ASP.NET MVC では、作成するコントローラークラスをどのように選択するか、どの方法を呼び出すか、また、変数が URL/Querystring から自動的に解析され、パラメーター引数としてメソッドに渡されるさまざまな方法を構成することができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="591e1-141">また、SEO (検索エンジンの最適化) のためにサイトを完全に最適化し、必要な URL 構造をアプリケーションから発行できる柔軟性を備えています。</span><span class="sxs-lookup"><span data-stu-id="591e1-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="591e1-142">既定では、新しい ASP.NET MVC プロジェクトには、既に登録済みの URL ルーティングルールのセットが付属しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="591e1-143">これにより、何も明示的に構成することなく、簡単にアプリケーションを開始できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="591e1-144">既定のルーティング規則の登録は、プロジェクトの "Application" クラス内にあります。これは、プロジェクトのルートにある "global.asax" ファイルをダブルクリックして開くことができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="591e1-145">既定の ASP.NET MVC ルーティング規則は、このクラスの "RegisterRoutes" メソッド内に登録されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="591e1-146">"ルート。MapRoute () "上記のメソッド呼び出しは、次の URL 形式を使用して、受信 Url をコントローラークラスにマップする既定のルーティング規則を登録します。"/{"コントローラー" は、インスタンス化するコントローラークラスの名前、"action" はそれに対して呼び出すパブリックメソッドの名前、"id" は、引数としてメソッドに渡すことができる URL 内に埋め込まれた省略可能なパラメーターである/{/}</span><span class="sxs-lookup"><span data-stu-id="591e1-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="591e1-147">"MapRoute ()" メソッド呼び出しに渡される3番目のパラメーターは、URL (Controller = "Home"、Action = "Index"、Id = "") に存在しない場合に、コントローラー/アクション/id 値に使用する既定値のセットです。</span><span class="sxs-lookup"><span data-stu-id="591e1-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="591e1-148">次の表は、既定の "<em>/{controllers}/{action}/{id}"</em>ルート規則を使用してさまざまな url がどのようにマップされるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="591e1-149">**[URL]**</span><span class="sxs-lookup"><span data-stu-id="591e1-149">**URL**</span></span> | <span data-ttu-id="591e1-150">**コントローラークラス**</span><span class="sxs-lookup"><span data-stu-id="591e1-150">**Controller Class**</span></span> | <span data-ttu-id="591e1-151">**アクションメソッド**</span><span class="sxs-lookup"><span data-stu-id="591e1-151">**Action Method**</span></span> | <span data-ttu-id="591e1-152">**渡されたパラメーター**</span><span class="sxs-lookup"><span data-stu-id="591e1-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="591e1-153">*/月/月*</span><span class="sxs-lookup"><span data-stu-id="591e1-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="591e1-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="591e1-154">DinnersController</span></span> | <span data-ttu-id="591e1-155">詳細 (id)</span><span class="sxs-lookup"><span data-stu-id="591e1-155">Details(id)</span></span> | <span data-ttu-id="591e1-156">id=2</span><span class="sxs-lookup"><span data-stu-id="591e1-156">id=2</span></span> |
| <span data-ttu-id="591e1-157">*//編集/5*</span><span class="sxs-lookup"><span data-stu-id="591e1-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="591e1-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="591e1-158">DinnersController</span></span> | <span data-ttu-id="591e1-159">編集 (id)</span><span class="sxs-lookup"><span data-stu-id="591e1-159">Edit(id)</span></span> | <span data-ttu-id="591e1-160">id=5</span><span class="sxs-lookup"><span data-stu-id="591e1-160">id=5</span></span> |
| <span data-ttu-id="591e1-161">*/Din*</span><span class="sxs-lookup"><span data-stu-id="591e1-161">*/Dinners/Create*</span></span> | <span data-ttu-id="591e1-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="591e1-162">DinnersController</span></span> | <span data-ttu-id="591e1-163">Create()</span><span class="sxs-lookup"><span data-stu-id="591e1-163">Create()</span></span> | <span data-ttu-id="591e1-164">該当なし</span><span class="sxs-lookup"><span data-stu-id="591e1-164">N/A</span></span> |
| <span data-ttu-id="591e1-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="591e1-165">*/Dinners*</span></span> | <span data-ttu-id="591e1-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="591e1-166">DinnersController</span></span> | <span data-ttu-id="591e1-167">Index ()</span><span class="sxs-lookup"><span data-stu-id="591e1-167">Index()</span></span> | <span data-ttu-id="591e1-168">該当なし</span><span class="sxs-lookup"><span data-stu-id="591e1-168">N/A</span></span> |
| <span data-ttu-id="591e1-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="591e1-169">*/Home*</span></span> | <span data-ttu-id="591e1-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="591e1-170">HomeController</span></span> | <span data-ttu-id="591e1-171">Index ()</span><span class="sxs-lookup"><span data-stu-id="591e1-171">Index()</span></span> | <span data-ttu-id="591e1-172">該当なし</span><span class="sxs-lookup"><span data-stu-id="591e1-172">N/A</span></span> |
| */* | <span data-ttu-id="591e1-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="591e1-173">HomeController</span></span> | <span data-ttu-id="591e1-174">Index ()</span><span class="sxs-lookup"><span data-stu-id="591e1-174">Index()</span></span> | <span data-ttu-id="591e1-175">該当なし</span><span class="sxs-lookup"><span data-stu-id="591e1-175">N/A</span></span> |

<span data-ttu-id="591e1-176">最後の3行は、使用されている既定値 (Controller = Home、Action = Index、Id = "") を示しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="591e1-177">"Index" メソッドが指定されていない場合は、既定のアクション名として登録されるため、"/Dinners" と "/Home" の Url によって、コントローラークラスで Index () アクションメソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="591e1-178">"Home" コントローラーが指定されていない場合、"Home" コントローラーは既定のコントローラーとして登録されるため、"/" URL によって HomeController が作成され、Index () アクションメソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="591e1-179">これらの既定の URL ルーティングルールが気に入らない場合は、簡単に変更できます。上記の RegisterRoutes メソッド内で編集するだけです。</span><span class="sxs-lookup"><span data-stu-id="591e1-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="591e1-180">ただし、このアプリケーションでは、既定の URL ルーティングルールを変更することはありません。代わりにそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="591e1-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="591e1-181">Dinのコントローラーからの Dinレポジトリの使用</span><span class="sxs-lookup"><span data-stu-id="591e1-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="591e1-182">ここでは、Dinの現在の実装である、() および Details () アクションメソッドを、モデルを使用する実装に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="591e1-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="591e1-183">以前に構築した Dinのリポジトリクラスを使用して、動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="591e1-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="591e1-184">まず、"using" ステートメントを追加し、"" を "使用" します。次に、"the" という名前空間を参照する "using" ステートメントを追加し、dinをコントローラークラスのフィールドとして、そのインスタンスを宣言します。</span><span class="sxs-lookup"><span data-stu-id="591e1-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="591e1-185">この章の後半では、"依存関係の挿入" の概念を紹介します。また、コントローラーが単体テストを有効にする Dinのリポジトリへの参照を取得するもう1つの方法を示しますが、ここでは、Dinレポジトリのインスタンスを作成するだけです。次のようにインライン化します。</span><span class="sxs-lookup"><span data-stu-id="591e1-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="591e1-186">これで、取得したデータモデルオブジェクトを使用して HTML 応答を返す準備ができました。</span><span class="sxs-lookup"><span data-stu-id="591e1-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="591e1-187">コントローラーでのビューの使用</span><span class="sxs-lookup"><span data-stu-id="591e1-187">Using Views with our Controller</span></span>

<span data-ttu-id="591e1-188">HTML をアセンブルするためのアクションメソッド内にコードを記述し、それをクライアントに送信するために*Response ()* ヘルパーメソッドを使用することは可能ですが、この方法は非常に扱いにくくなります。</span><span class="sxs-lookup"><span data-stu-id="591e1-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="591e1-189">はるかに優れたアプローチは、アプリケーションとデータロジックを Dincontroller のアクションメソッド内でのみ実行し、html 応答のレンダリングに必要なデータを、HTML 表現の出力を行う別の "view" テンプレートに渡すことです。このようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="591e1-190">すぐにわかるように、"view" テンプレートは、通常、HTML マークアップと埋め込みのレンダリングコードの組み合わせを含むテキストファイルです。</span><span class="sxs-lookup"><span data-stu-id="591e1-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="591e1-191">ビューレンダリングからコントローラーロジックを分離すると、いくつかの大きな利点が得られます。</span><span class="sxs-lookup"><span data-stu-id="591e1-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="591e1-192">特に、アプリケーションコードと UI 書式設定/レンダリングコードの間で、明確な "問題の分離" を適用するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="591e1-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="591e1-193">これにより、UI レンダリングロジックから分離されたアプリケーションロジックの単体テストがはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="591e1-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="591e1-194">これにより、アプリケーションコードを変更することなく、UI レンダリングテンプレートを後で簡単に変更できるようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="591e1-195">また、開発者やデザイナーがプロジェクトで共同作業を簡単に行えるようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="591e1-196">Dinの Scontroller クラスを更新して、ビューテンプレートを使用して、2つのアクションメソッドの戻り値の型を "void" にして、代わりに戻り値の型が "ActionResult" になるようにすることで、HTML UI の応答を返信するように指定できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="591e1-197">次のように、コントローラーの基本クラスで*View ()* ヘルパーメソッドを呼び出して、"viewresult" オブジェクトを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="591e1-198">上記で使用している*View ()* ヘルパーメソッドのシグネチャは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="591e1-199">*View ()* ヘルパーメソッドの最初のパラメーターは、HTML 応答を表示するために使用するビューテンプレートファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="591e1-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="591e1-200">2番目のパラメーターは、ビューテンプレートが HTML 応答を表示するために必要なデータを含むモデルオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="591e1-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="591e1-201">Index () アクションメソッドでは、 *view ()* ヘルパーメソッドを呼び出し、"index" ビューテンプレートを使用してディナーの HTML リストを表示することを示しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="591e1-202">ここでは、リストを生成するディナーオブジェクトのシーケンスをビューテンプレートに渡しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="591e1-203">詳細 () アクションメソッド内で、URL 内で指定された id を使用してディナーオブジェクトを取得しようとしています。</span><span class="sxs-lookup"><span data-stu-id="591e1-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="591e1-204">有効なディナーが見つかった場合は、 *view ()* ヘルパーメソッドを呼び出します。これは、取得したディナーオブジェクトを表示するために "Details" ビューテンプレートを使用することを示します。</span><span class="sxs-lookup"><span data-stu-id="591e1-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="591e1-205">無効なディナーが要求された場合は、"NotFound" ビューテンプレート (および、テンプレート名を受け取る*ビュー ()* ヘルパーメソッドのオーバーロードされたバージョン) を使用してディナーが存在しないことを示す役立つエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="591e1-206">ここで、"NotFound"、"Details"、"Index" の各ビューテンプレートを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="591e1-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="591e1-207">"NotFound" ビューテンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="591e1-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="591e1-208">まず、"NotFound" ビューテンプレートを実装します。これにより、要求されたディナーが見つからないことを示すわかりやすいエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="591e1-209">コントローラーアクションメソッド内にテキストカーソルを配置し、右クリックして [ビューの追加] メニューコマンドを選択することによって、新しいビューテンプレートを作成します (Ctrl + M、Ctrl + V キーを押して、このコマンドを実行することもできます)。</span><span class="sxs-lookup"><span data-stu-id="591e1-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="591e1-210">これにより、次のような [ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="591e1-211">既定では、ダイアログが起動されたときのアクションメソッド (この場合は "Details") の名前と一致するように、作成するビューの名前が事前に設定されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="591e1-212">最初に "NotFound" テンプレートを実装するので、このビュー名をオーバーライドし、代わりに "NotFound" に設定します。</span><span class="sxs-lookup"><span data-stu-id="591e1-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="591e1-213">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "NotFound" ビューテンプレートを作成します (ディレクトリがまだ存在しない場合にも作成されます)。</span><span class="sxs-lookup"><span data-stu-id="591e1-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="591e1-214">また、コードエディター内で新しい "NotFound" ビューテンプレートが開きます。</span><span class="sxs-lookup"><span data-stu-id="591e1-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="591e1-215">既定では、ビューテンプレートには、コンテンツとコードを追加できる2つの "コンテンツ領域" があります。</span><span class="sxs-lookup"><span data-stu-id="591e1-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="591e1-216">1つ目の方法では、返信した HTML ページの "タイトル" をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="591e1-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="591e1-217">2つ目の方法では、返信した HTML ページの "メインコンテンツ" をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="591e1-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="591e1-218">"NotFound" ビューテンプレートを実装するには、いくつかの基本的なコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="591e1-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="591e1-219">その後、ブラウザー内で試してみることができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-219">We can then try it out within the browser.</span></span> <span data-ttu-id="591e1-220">これを行うには、 *"/Din/9999"* の URL を要求します。</span><span class="sxs-lookup"><span data-stu-id="591e1-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="591e1-221">これは、データベースに現在存在していないディナーを指し、"NotFound" ビューテンプレートをレンダリングするために、Din() アクションメソッドによって表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="591e1-222">上のスクリーンショットでは、基本的なビューテンプレートによって、画面上のメインコンテンツを囲む HTML がいくつか継承されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="591e1-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="591e1-223">これは、ビューテンプレートが "マスターページ" テンプレートを使用しているためです。これにより、サイト上のすべてのビューで一貫したレイアウトを適用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="591e1-224">このチュートリアルの後半では、マスターページがどのように機能するかについて説明します。</span><span class="sxs-lookup"><span data-stu-id="591e1-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="591e1-225">"Details" ビューテンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="591e1-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="591e1-226">ここで、"Details" ビューテンプレートを実装します。これにより、単一のディナーモデルの HTML が生成されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="591e1-227">これを行うには、詳細アクションメソッド内にテキストカーソルを配置し、右クリックして [ビューの追加] メニューコマンドを選択します (または、Ctrl + M キー、Ctrl キーを押しながら V キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="591e1-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="591e1-228">[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="591e1-229">既定のビュー名 ("Details") はそのままにします。</span><span class="sxs-lookup"><span data-stu-id="591e1-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="591e1-230">また、ダイアログの [厳密に型指定されたビューを作成する] チェックボックスをオンにし、コントローラーからビューに渡すモデルの種類の名前を選択します (コンボボックスのドロップダウンリストを使用します)。</span><span class="sxs-lookup"><span data-stu-id="591e1-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="591e1-231">このビューでは、ディナーオブジェクトを渡しています (この型の完全修飾名は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="591e1-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="591e1-232">"空のビュー" の作成を選択した前のテンプレートとは異なり、今回は "詳細" テンプレートを使用してビューを自動的に "スキャフォールディング" することを選択します。</span><span class="sxs-lookup"><span data-stu-id="591e1-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="591e1-233">これを示すには、上のダイアログボックスの [コンテンツの表示] ドロップダウンを変更します。</span><span class="sxs-lookup"><span data-stu-id="591e1-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="591e1-234">"スキャフォールディング" は、渡されるディナーオブジェクトに基づいて、詳細ビューテンプレートの初期実装を生成します。</span><span class="sxs-lookup"><span data-stu-id="591e1-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="591e1-235">これにより、ビューテンプレートの実装を簡単に開始できるようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="591e1-236">[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Details" ビューテンプレートファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="591e1-237">また、コードエディター内で新しい "Details" ビューテンプレートが開きます。</span><span class="sxs-lookup"><span data-stu-id="591e1-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="591e1-238">これには、ディナーモデルに基づく詳細ビューの初期スキャフォールディング実装が含まれます。</span><span class="sxs-lookup"><span data-stu-id="591e1-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="591e1-239">スキャフォールディングエンジンは、.NET リフレクションを使用して、渡されたクラスで公開されているパブリックプロパティを確認し、見つかった各型に基づいて適切なコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="591e1-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="591e1-240">*"/Dinners/Details/1"* という URL を要求して、ブラウザーでのこの "詳細" スキャフォールディング実装の外観を確認できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="591e1-241">この URL を使用すると、最初にデータベースを作成したときにデータベースに手動で追加したディナーの1つが表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="591e1-242">これにより、すぐに稼働が開始され、詳細な .aspx ビューの初期実装が提供されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="591e1-243">それを調整して、UI を満足できるようにカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="591e1-244">詳細 .aspx テンプレートについて詳しく説明すると、静的な HTML と埋め込みの描画コードが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="591e1-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="591e1-245">&lt;%%&gt; コードナゲットはビューテンプレートのレンダリング時にコードを実行し、&lt;% =%&gt; コードナゲットに含まれるコードを実行し、その結果をテンプレートの出力ストリームにレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="591e1-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="591e1-246">このビューには、厳密に型指定された "モデル" プロパティを使用してコントローラーから渡された "ディナー" モデルオブジェクトにアクセスするコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="591e1-247">Visual Studio には、エディター内でこの "モデル" プロパティにアクセスするときに完全なコード intellisense が用意されています。</span><span class="sxs-lookup"><span data-stu-id="591e1-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="591e1-248">最終的な詳細ビューテンプレートのソースが次のようになるように、いくつかの調整を行いましょう。</span><span class="sxs-lookup"><span data-stu-id="591e1-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="591e1-249">*"/Dinners/Details/1"* URL にもう一度アクセスすると、次のように表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="591e1-250">"Index" ビューテンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="591e1-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="591e1-251">"Index" ビューテンプレートを実装しましょう。これにより、今後のディナーの一覧が生成されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="591e1-252">これを行うには、Index アクションメソッド内にテキストカーソルを置き、右クリックして [ビューの追加] メニューコマンドを選択します (または、Ctrl + M キー、Ctrl キーを押しながら V キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="591e1-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="591e1-253">[ビューの追加] ダイアログボックスで、"Index" という名前のビューテンプレートを保持し、[厳密に型指定されたビューを作成する] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="591e1-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="591e1-254">今回は、"リスト" ビューテンプレートを自動的に生成し、ビューに渡されるモデルの種類として "スキャフォールディング" を選択します。これは、"リスト" を作成すると、[ビューの追加] ダイアログでは次のようになります。コントローラーからビューにディナーオブジェクトのシーケンスを渡します。</span><span class="sxs-lookup"><span data-stu-id="591e1-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="591e1-255">[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Index" ビューテンプレートファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="591e1-256">ビューに渡すディナーの HTML テーブルリストを提供する、その内部の初期実装を "スキャフォールディング" します。</span><span class="sxs-lookup"><span data-stu-id="591e1-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="591e1-257">アプリケーションを実行して *"* ディナー" の URL にアクセスすると、次のような一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="591e1-258">上のテーブルソリューションでは、ディナーデータのグリッド形式のレイアウトが提供されています。これは、お客様に向けたディナーのリストについてはあまり必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="591e1-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="591e1-259">次のコードを使用して、インデックスの .aspx ビューテンプレートを更新し、それを変更してデータの列数を減らすことができます。また、&lt;ul&gt; 要素を使用して、テーブルではなくレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="591e1-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="591e1-260">上記の foreach ステートメントでは、モデルの各ディナーをループ処理する "var" キーワードを使用しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="591e1-261">3\.0 にC#精通している方は、"var" を使用すると、ディナーオブジェクトが遅延バインディングされることを意味します。</span><span class="sxs-lookup"><span data-stu-id="591e1-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="591e1-262">代わりに、コンパイラが厳密に型指定された "Model" プロパティ ("IEnumerable&lt;ディナー&gt;") に対して型の推論を使用し、ローカルの "ディナー" 変数をディナー型としてコンパイルしていることを意味します。これは、intellisense を完全に取得し、コードブロック内でコンパイル時にチェックします。</span><span class="sxs-lookup"><span data-stu-id="591e1-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="591e1-263">ブラウザーで */Dinners* URL の更新にヒットすると、更新されたビューは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="591e1-264">この方が優れていますが、まだ完全ではありません。</span><span class="sxs-lookup"><span data-stu-id="591e1-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="591e1-265">最後の手順は、エンドユーザーがリスト内の個々のディナーをクリックして、その詳細を確認できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="591e1-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="591e1-266">これを実装するには、Dinのコントローラーの Details アクションメソッドにリンクする HTML ハイパーリンク要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="591e1-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="591e1-267">これらのハイパーリンクは、次の2つの方法のいずれかで、インデックスビュー内に生成できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="591e1-268">1つ目は、次のような&gt; の要素 &lt;HTML を手動で作成することです。ここでは、&lt;%%&gt; ブロックを &lt;HTML 要素&gt; に埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="591e1-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="591e1-269">別の方法として、ASP.NET MVC 内で組み込みの "Html.actionlink ()" ヘルパーメソッドを利用して、プログラムによって、コントローラー上の別のアクションメソッドにリンクする HTML &lt;&gt; 要素を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="591e1-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="591e1-270">Html の最初のパラメーター。 Html.actionlink () ヘルパーメソッドは、表示するリンクテキスト (この場合はディナーのタイトル)、2番目のパラメーターはリンクを生成するコントローラーアクション名 (この場合は詳細メソッド)、3番目のパラメーターはアクションに送信するパラメーターのセットです (プロパティ名/値を持つ匿名型として実装されます)。</span><span class="sxs-lookup"><span data-stu-id="591e1-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="591e1-271">この例では、リンク先のディナーの "id" パラメーターを指定しています。また、ASP.NET MVC の既定の URL ルーティングルールは "{Controller}/{action}/{Html.actionlink () ヘルパーメソッドによって次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="591e1-272">この例では、Html.actionlink () ヘルパーメソッドを使用して、リスト内の各ディナーを適切な詳細 URL にリンクします。</span><span class="sxs-lookup"><span data-stu-id="591e1-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="591e1-273">*/Dinners*の URL にヒットすると、ディナーリストは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="591e1-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="591e1-274">一覧でディナーのいずれかをクリックすると、その詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="591e1-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="591e1-275">規則ベースの名前付けおよび \ ビューのディレクトリ構造</span><span class="sxs-lookup"><span data-stu-id="591e1-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="591e1-276">既定では、ASP.NET MVC アプリケーションは、ビューテンプレートを解決するときに、規則ベースのディレクトリ名前付け構造を使用します。</span><span class="sxs-lookup"><span data-stu-id="591e1-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="591e1-277">これにより、開発者は、コントローラークラス内からビューを参照するときに、ロケーションパスを完全修飾する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="591e1-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="591e1-278">既定では、ASP.NET MVC は、アプリケーションの下にある \* \ Views\[ControllerName]\* ディレクトリ内のビューテンプレートファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="591e1-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="591e1-279">たとえば、"Index"、"Details"、"NotFound" という3つのビューテンプレートを明示的に参照する、Din: Controller クラスに取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="591e1-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="591e1-280">既定では、ASP.NET MVC は、アプリケーションのルートディレクトリの下にある *\Views\Dinners*ディレクトリ内でこれらのビューを検索します。</span><span class="sxs-lookup"><span data-stu-id="591e1-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="591e1-281">プロジェクト内に現在3つのコントローラークラスがあることに注目してください (HomeController と AccountController –プロジェクトの作成時に既定で最後の2つが追加されています)。サブディレクトリは3つあります (コントローラー) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="591e1-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="591e1-282">ホームコントローラーとアカウントコントローラーから参照されているビューは、それぞれの *\Views\Home*ディレクトリと *\Views\Account*ディレクトリから、ビューテンプレートを自動的に解決します。</span><span class="sxs-lookup"><span data-stu-id="591e1-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="591e1-283">*ある \views\shared*サブディレクトリは、アプリケーション内の複数のコントローラー間で再利用されるビューテンプレートを格納するための方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="591e1-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="591e1-284">ASP.NET MVC は、ビューテンプレートを解決しようとすると、最初に *\ Views\[Controller]* 特定のディレクトリ内をチェックし、ビューテンプレートが見つからない場合は*ある \views\shared*ディレクトリ内で確認します。</span><span class="sxs-lookup"><span data-stu-id="591e1-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="591e1-285">個々のビューテンプレートに名前を付ける場合は、ビューテンプレートでレンダリングの原因となったアクションメソッドと同じ名前を共有することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="591e1-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="591e1-286">たとえば、"Index" アクションメソッドの上では、"Index" ビューを使用してビューの結果を表示し、"Details" アクションメソッドは "Details" ビューを使用して結果を表示しています。</span><span class="sxs-lookup"><span data-stu-id="591e1-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="591e1-287">これにより、各アクションに関連付けられているテンプレートを簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="591e1-288">ビューテンプレートの名前がコントローラーで呼び出されているアクションメソッドと同じである場合、開発者はビューテンプレート名を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="591e1-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="591e1-289">代わりに、モデルオブジェクトを "View ()" ヘルパーメソッドに渡すだけで (ビュー名を指定する必要はありません)、ASP.NET MVC は *\[ControllerName を\[* 使用してディスク上に ActionName] ビューテンプレートをレンダリングすることを自動的に推測します。</span><span class="sxs-lookup"><span data-stu-id="591e1-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="591e1-290">これにより、コントローラーコードを少しクリーンアップし、コードで名前を2回複製することを回避できます。</span><span class="sxs-lookup"><span data-stu-id="591e1-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="591e1-291">上記のコードは、サイトのディナーリスト/詳細エクスペリエンスを実装するために必要なすべてのものです。</span><span class="sxs-lookup"><span data-stu-id="591e1-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="591e1-292">次の手順</span><span class="sxs-lookup"><span data-stu-id="591e1-292">Next Step</span></span>

<span data-ttu-id="591e1-293">これで、ディナーブラウズエクスペリエンスが作成されました。</span><span class="sxs-lookup"><span data-stu-id="591e1-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="591e1-294">CRUD (作成、読み取り、更新、削除) データフォーム編集サポートを有効にしましょう。</span><span class="sxs-lookup"><span data-stu-id="591e1-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="591e1-295">[前へ](build-a-model-with-business-rule-validations.md)
> [次へ](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="591e1-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
