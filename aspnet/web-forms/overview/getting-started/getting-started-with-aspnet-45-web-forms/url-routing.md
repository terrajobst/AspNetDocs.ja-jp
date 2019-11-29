---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL ルーティング |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590708"
---
# <a name="url-routing"></a><span data-ttu-id="6720e-103">URL ルーティング</span><span class="sxs-lookup"><span data-stu-id="6720e-103">URL Routing</span></span>

<span data-ttu-id="6720e-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="6720e-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="6720e-105">[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。</span><span class="sxs-lookup"><span data-stu-id="6720e-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="6720e-106">このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。</span><span class="sxs-lookup"><span data-stu-id="6720e-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="6720e-107">このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。</span><span class="sxs-lookup"><span data-stu-id="6720e-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="6720e-108">このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、URL ルーティングをサポートします。</span><span class="sxs-lookup"><span data-stu-id="6720e-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="6720e-109">ルーティングを使用すると、web アプリケーションは、検索エンジンによって、わかりやすく、覚えやすく、より優れた Url を使用できます。</span><span class="sxs-lookup"><span data-stu-id="6720e-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="6720e-110">このチュートリアルは、前の「メンバーシップと管理」チュートリアルに基づいており、Wingtip Toys チュートリアルシリーズの一部です。</span><span class="sxs-lookup"><span data-stu-id="6720e-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="6720e-111">学習内容:</span><span class="sxs-lookup"><span data-stu-id="6720e-111">What you'll learn:</span></span>

- <span data-ttu-id="6720e-112">ASP.NET Web フォームアプリケーションのルートを登録する方法。</span><span class="sxs-lookup"><span data-stu-id="6720e-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="6720e-113">Web ページにルートを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="6720e-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="6720e-114">ルートをサポートするためにデータベースからデータを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="6720e-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="6720e-115">ASP.NET ルーティングの概要</span><span class="sxs-lookup"><span data-stu-id="6720e-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="6720e-116">URL ルーティングを使用すると、物理ファイルにマップされていない要求 Url を受け入れるようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="6720e-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="6720e-117">要求 URL は、ユーザーがブラウザーに入力して web サイト上のページを見つけるための URL です。</span><span class="sxs-lookup"><span data-stu-id="6720e-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="6720e-118">ルーティングを使用して、ユーザーに意味のある Url を定義し、検索エンジンの最適化 (SEO) に役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="6720e-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="6720e-119">既定では、Web フォームテンプレートには[ASP.NET フレンドリな url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6720e-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="6720e-120">基本的なルーティング作業の多くは、*わかりやすい url*を使用して実装されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="6720e-121">ただし、このチュートリアルでは、カスタマイズされたルーティング機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="6720e-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="6720e-122">URL ルーティングをカスタマイズする前に、Wingtip Toys サンプルアプリケーションは次の URL を使用して製品にリンクできます。</span><span class="sxs-lookup"><span data-stu-id="6720e-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="6720e-123">URL ルーティングをカスタマイズすることで、Wingtip Toys サンプルアプリケーションは、読みやすい URL を使用して同じ製品にリンクします。</span><span class="sxs-lookup"><span data-stu-id="6720e-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="6720e-124">ルート</span><span class="sxs-lookup"><span data-stu-id="6720e-124">Routes</span></span>

<span data-ttu-id="6720e-125">ルートは、ハンドラーにマップされる URL パターンです。</span><span class="sxs-lookup"><span data-stu-id="6720e-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="6720e-126">ハンドラーは、Web フォームアプリケーションの .aspx ファイルなどの物理ファイルにすることができます。</span><span class="sxs-lookup"><span data-stu-id="6720e-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="6720e-127">ハンドラーは、要求を処理するクラスにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="6720e-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="6720e-128">ルートを定義するには、ルートクラスのインスタンスを作成します。そのためには、URL パターン、ハンドラー、および必要に応じてルートの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="6720e-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="6720e-129">ルートをアプリケーションに追加するには、`Route` オブジェクトを `RouteTable` クラスの static `Routes` プロパティに追加します。</span><span class="sxs-lookup"><span data-stu-id="6720e-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="6720e-130">Route プロパティは、アプリケーションのすべてのルートを格納する `RouteCollection` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="6720e-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="6720e-131">URL パターン</span><span class="sxs-lookup"><span data-stu-id="6720e-131">URL Patterns</span></span>

<span data-ttu-id="6720e-132">URL パターンには、リテラル値と変数プレースホルダー (URL パラメーターと呼ばれます) を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="6720e-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="6720e-133">リテラルとプレースホルダーは、スラッシュ (`/`) 文字で区切られた URL のセグメントに配置されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="6720e-134">Web アプリケーションへの要求が行われると、URL がセグメントとプレースホルダーに解析され、変数の値が要求ハンドラーに提供されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="6720e-135">このプロセスは、クエリ文字列内のデータを解析して要求ハンドラーに渡す方法と似ています。</span><span class="sxs-lookup"><span data-stu-id="6720e-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="6720e-136">どちらの場合も、変数情報は URL に含まれ、キーと値のペアの形式でハンドラーに渡されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="6720e-137">クエリ文字列の場合、キーと値の両方が URL に含まれます。</span><span class="sxs-lookup"><span data-stu-id="6720e-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="6720e-138">ルートの場合、キーは URL パターンで定義されているプレースホルダー名で、値のみが URL に含まれます。</span><span class="sxs-lookup"><span data-stu-id="6720e-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="6720e-139">URL パターンでは、プレースホルダーを中かっこ (`{` および `}`) で囲んで定義します。</span><span class="sxs-lookup"><span data-stu-id="6720e-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="6720e-140">1つのセグメントに複数のプレースホルダーを定義できますが、プレースホルダーはリテラル値で区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="6720e-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="6720e-141">たとえば、`{language}-{country}/{action}` は有効なルートパターンです。</span><span class="sxs-lookup"><span data-stu-id="6720e-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="6720e-142">ただし、`{language}{country}/{action}` は有効なパターンではありません。これは、プレースホルダーの間にリテラル値または区切り記号がないためです。</span><span class="sxs-lookup"><span data-stu-id="6720e-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="6720e-143">そのため、言語プレースホルダーの値を country プレースホルダーの値と区切る場所をルーティングで決定することはできません。</span><span class="sxs-lookup"><span data-stu-id="6720e-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="6720e-144">ルートのマッピングと登録</span><span class="sxs-lookup"><span data-stu-id="6720e-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="6720e-145">Wingtip Toys サンプルアプリケーションのページにルートを追加するには、アプリケーションの起動時にルートを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6720e-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="6720e-146">ルートを登録するには、`Application_Start` イベントハンドラーを変更します。</span><span class="sxs-lookup"><span data-stu-id="6720e-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="6720e-147">Visual Studio の**ソリューションエクスプローラー**で、 *Global.asax.cs*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="6720e-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="6720e-148">次のように、黄色で強調表示されているコードを*Global.asax.cs*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="6720e-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="6720e-149">Wingtip Toys サンプルアプリケーションが起動すると、`Application_Start` イベントハンドラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="6720e-150">このイベントハンドラーの最後に、`RegisterCustomRoutes` メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="6720e-151">`RegisterCustomRoutes` メソッドは、`RouteCollection` オブジェクトの `MapPageRoute` メソッドを呼び出すことによって各ルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="6720e-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="6720e-152">ルートは、ルート名、ルート URL、および物理 URL を使用して定義されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="6720e-153">最初のパラメーター ("`ProductsByCategoryRoute`") は、ルート名です。</span><span class="sxs-lookup"><span data-stu-id="6720e-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="6720e-154">必要に応じてルートを呼び出すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="6720e-155">2番目のパラメーター ("`Category/{categoryName}`") は、コードに基づいて動的に使用できる代替 URL を定義します。</span><span class="sxs-lookup"><span data-stu-id="6720e-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="6720e-156">データに基づいて生成されるリンクをデータコントロールに設定する場合は、このルートを使用します。</span><span class="sxs-lookup"><span data-stu-id="6720e-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="6720e-157">ルートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6720e-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="6720e-158">ルートの2番目のパラメーターには、中かっこ (`{ }`) で指定された動的な値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6720e-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="6720e-159">この場合、`categoryName` は、適切なルーティングパスを決定するために使用される変数です。</span><span class="sxs-lookup"><span data-stu-id="6720e-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6720e-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6720e-160">**Optional**</span></span>
> 
> <span data-ttu-id="6720e-161">`RegisterCustomRoutes` メソッドを別のクラスに移動することで、コードの管理が容易になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6720e-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="6720e-162">*Logic*フォルダーで、別個の `RouteActions` クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="6720e-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="6720e-163">上の `RegisterCustomRoutes` メソッドを*Global.asax.cs*ファイルから新しい `RoutesActions` クラスに移動します。</span><span class="sxs-lookup"><span data-stu-id="6720e-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="6720e-164">*Global.asax.cs*ファイルから `RegisterCustomRoutes` メソッドを呼び出す方法の例として、`RoleActions` クラスと `createAdmin` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="6720e-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>

<span data-ttu-id="6720e-165">また、`Application_Start` イベントハンドラーの先頭にある `RouteConfig` オブジェクトを使用して、`RegisterRoutes` メソッドの呼び出しを確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="6720e-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="6720e-166">この呼び出しは、既定のルーティングを実装するために行われます。</span><span class="sxs-lookup"><span data-stu-id="6720e-166">This call is made to implement default routing.</span></span> <span data-ttu-id="6720e-167">これは、Visual Studio の Web フォームテンプレートを使用してアプリケーションを作成したときに既定のコードとして含まれていました。</span><span class="sxs-lookup"><span data-stu-id="6720e-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="6720e-168">ルートデータの取得と使用</span><span class="sxs-lookup"><span data-stu-id="6720e-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="6720e-169">前述のように、ルートを定義できます。</span><span class="sxs-lookup"><span data-stu-id="6720e-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="6720e-170">*Global.asax.cs*ファイルの `Application_Start` イベントハンドラーに追加したコードによって、定義可能なルートが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="6720e-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="6720e-171">ルートの設定</span><span class="sxs-lookup"><span data-stu-id="6720e-171">Setting Routes</span></span>

<span data-ttu-id="6720e-172">ルートでは、追加のコードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6720e-172">Routes require you to add additional code.</span></span> <span data-ttu-id="6720e-173">このチュートリアルでは、モデルバインドを使用して、データコントロールのデータを使用してルートを生成するときに使用される `RouteValueDictionary` オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="6720e-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="6720e-174">`RouteValueDictionary` オブジェクトには、製品の特定のカテゴリに属する製品名の一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6720e-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="6720e-175">データとルートに基づいて、製品ごとにリンクが作成されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="6720e-176">カテゴリと製品のルートを有効にする</span><span class="sxs-lookup"><span data-stu-id="6720e-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="6720e-177">次に、`ProductsByCategoryRoute` を使用するようにアプリケーションを更新して、各製品カテゴリリンクに含める正しいルートを決定します。</span><span class="sxs-lookup"><span data-stu-id="6720e-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="6720e-178">また、 *Productlist .aspx*ページを更新して、各製品のルーティングリンクを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="6720e-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="6720e-179">リンクは変更前として表示されますが、リンクは URL ルーティングを使用するようになります。</span><span class="sxs-lookup"><span data-stu-id="6720e-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="6720e-180">**ソリューションエクスプローラー**で、まだ開いていない場合は、[ *.master* ] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="6720e-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="6720e-181">"`categoryList`" という名前の**ListView**コントロールを、黄色で強調表示されている変更で更新します。これにより、マークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6720e-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="6720e-182">**ソリューションエクスプローラー**で、 *productlist .aspx*ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="6720e-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="6720e-183">更新プログラムが黄色で強調表示されている状態で、 *Productlist .aspx*ページの `ItemTemplate` 要素を更新します。これにより、マークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6720e-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="6720e-184">*ProductList.aspx.cs*の分離コードを開き、黄色で強調表示されている次の名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="6720e-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="6720e-185">分離コード (*ProductList.aspx.cs*) の `GetProducts` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6720e-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="6720e-186">製品の詳細のコードを追加する</span><span class="sxs-lookup"><span data-stu-id="6720e-186">Add Code for Product Details</span></span>

<span data-ttu-id="6720e-187">次に、 *Productdetails .aspx*ページの分離コード (*ProductDetails.aspx.cs*) を更新して、ルートデータを使用するようにします。</span><span class="sxs-lookup"><span data-stu-id="6720e-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="6720e-188">新しい `GetProduct` メソッドでは、ユーザーが、古い非ルーティング URL を使用するリンクがブックマークに登録されている場合にもクエリ文字列値を受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6720e-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="6720e-189">分離コード (*ProductDetails.aspx.cs*) の `GetProduct` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6720e-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="6720e-190">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="6720e-190">Running the Application</span></span>

<span data-ttu-id="6720e-191">アプリケーションを今すぐ実行して、更新されたルートを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="6720e-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="6720e-192">**F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="6720e-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="6720e-193">ブラウザーが開き、 *default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="6720e-194">ページの上部にある **[Products]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6720e-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="6720e-195">すべての製品が*Productlist .aspx*ページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="6720e-196">ブラウザーでは、次の URL (ポート番号を使用) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="6720e-197">次に、ページの上部近くにある **[車両]** カテゴリリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6720e-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="6720e-198">[ *Productlist] .aspx*ページには、自動車のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="6720e-199">ブラウザーでは、次の URL (ポート番号を使用) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="6720e-200">ページに一覧表示されている最初の車の名前 ("**コンバーチブル車**") を含むリンクをクリックして、製品の詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="6720e-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="6720e-201">ブラウザーでは、次の URL (ポート番号を使用) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6720e-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="6720e-202">次に、ルーティングされていない次の URL (ポート番号を使用) をブラウザーに入力します。</span><span class="sxs-lookup"><span data-stu-id="6720e-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="6720e-203">このコードは、ユーザーがリンクをブックマークした場合に、クエリ文字列を含む URL を引き続き認識します。</span><span class="sxs-lookup"><span data-stu-id="6720e-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="6720e-204">要約</span><span class="sxs-lookup"><span data-stu-id="6720e-204">Summary</span></span>

<span data-ttu-id="6720e-205">このチュートリアルでは、カテゴリと製品のルートを追加しました。</span><span class="sxs-lookup"><span data-stu-id="6720e-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="6720e-206">ここでは、モデルバインドを使用するデータコントロールとルートを統合する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="6720e-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="6720e-207">次のチュートリアルでは、グローバルエラー処理を実装します。</span><span class="sxs-lookup"><span data-stu-id="6720e-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6720e-208">その他の資料</span><span class="sxs-lookup"><span data-stu-id="6720e-208">Additional Resources</span></span>

[<span data-ttu-id="6720e-209">ASP.NET のフレンドリな Url</span><span class="sxs-lookup"><span data-stu-id="6720e-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="6720e-210">メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure App Service にデプロイする</span><span class="sxs-lookup"><span data-stu-id="6720e-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="6720e-211">Microsoft Azure-無料試用版</span><span class="sxs-lookup"><span data-stu-id="6720e-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="6720e-212">[前へ](membership-and-administration.md)
> [次へ](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="6720e-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
