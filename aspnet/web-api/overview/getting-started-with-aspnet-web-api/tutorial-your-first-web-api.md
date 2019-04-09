---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 の概要 (C#)-ASP.NET 4.x
author: MikeWasson
description: コードのチュートリアルです。 Web API を製品の一覧を返すを作成するのにには、ASP.NET Web API を使用します。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5e3c049ba4349301c3c2d173d4311b3d0883bf68
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401752"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="78b4f-104">ASP.NET Web API 2 (c#) の概要します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="78b4f-105">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="78b4f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="78b4f-106">完成したプロジェクトをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="78b4f-107">このチュートリアルでは、web を製品の一覧を返す API を作成するのに ASP.NET Web API を使用します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="78b4f-108">HTTP は web ページを提供するためだけではありません。</span><span class="sxs-lookup"><span data-stu-id="78b4f-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="78b4f-109">HTTP は、サービスとデータを公開する Api を構築するための強力なプラットフォームではまたです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="78b4f-110">HTTP は、シンプルかつ柔軟なユビキタスです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="78b4f-111">考えることができ、ほとんどすべてのプラットフォームでは、HTTP ライブラリを持つため、HTTP サービスがクライアント、ブラウザー、モバイル デバイスは、従来のデスクトップ アプリケーションなどの広範な範囲に到達できます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="78b4f-112">ASP.NET Web API とは、web Api、.NET Framework 上に構築するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="78b4f-113">このチュートリアルで使用されるソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="78b4f-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="78b4f-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="78b4f-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="78b4f-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="78b4f-115">Web API 2</span></span>

<span data-ttu-id="78b4f-116">参照してください[ASP.NET Core と Windows の Visual Studio で web API の作成](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api)のこのチュートリアルの最新バージョン。</span><span class="sxs-lookup"><span data-stu-id="78b4f-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="78b4f-117">Web API プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-117">Create a Web API Project</span></span>

<span data-ttu-id="78b4f-118">このチュートリアルでは、web を製品の一覧を返す API を作成するのに ASP.NET Web API を使用します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="78b4f-119">フロント エンドの web ページは、結果を表示するのに jQuery を使用します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="78b4f-120">Visual Studio を起動し、選択**新しいプロジェクト**から、**開始**ページ。</span><span class="sxs-lookup"><span data-stu-id="78b4f-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="78b4f-121">またはから、**ファイル**メニューの **新規**し**プロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="78b4f-122">**テンプレート**ペインで、**インストールされたテンプレート**を展開し、 **Visual c#** ノード。</span><span class="sxs-lookup"><span data-stu-id="78b4f-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="78b4f-123">**Visual c#**、 **Web**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="78b4f-124">プロジェクト テンプレートの一覧で選択**ASP.NET Web アプリケーション**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="78b4f-125">プロジェクトに"ProductsApp"という名前にして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="78b4f-126">**新しい ASP.NET プロジェクト**ダイアログ ボックスで、**空**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="78b4f-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="78b4f-127">&quot;フォルダーを追加し、参照用のコア&quot;、確認**Web API**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="78b4f-128">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="78b4f-129">使用して Web API プロジェクトを作成することも、 &quot;Web API&quot;テンプレート。</span><span class="sxs-lookup"><span data-stu-id="78b4f-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="78b4f-130">Web API テンプレートでは、ASP.NET MVC を使用して、API のヘルプ ページを提供します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="78b4f-131">MVC せず Web API を表示する必要があるために、このチュートリアルでは、空のテンプレートを使っています。</span><span class="sxs-lookup"><span data-stu-id="78b4f-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="78b4f-132">一般に、Web API を使用して ASP.NET MVC を把握する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="78b4f-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="78b4f-133">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="78b4f-133">Adding a Model</span></span>

<span data-ttu-id="78b4f-134">*モデル*は、アプリケーションのデータを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="78b4f-135">ASP.NET Web API では、JSON、XML、またはその他のいくつかの形式にモデルを自動的にシリアル化でき、HTTP 応答メッセージの本文にシリアル化されたデータを記述することができます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="78b4f-136">クライアントでは、シリアル化形式を読み取り、限り、オブジェクトを逆シリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="78b4f-137">ほとんどのクライアントには、XML または JSON を解析できます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="78b4f-138">さらに、クライアントは、HTTP 要求メッセージに Accept ヘッダーを設定して、どの形式を指定できます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="78b4f-139">製品を表す単純なモデルを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="78b4f-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="78b4f-140">ソリューション エクスプ ローラーが表示されない場合は、クリックして、**ビュー**メニュー選択し、**ソリューション エクスプ ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="78b4f-141">ソリューション エクスプ ローラーで、Models フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="78b4f-142">コンテキスト メニューでは、次のように選択します。**追加**選び**クラス**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="78b4f-143">クラスの名前&quot;製品&quot;します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="78b4f-144">次のプロパティを追加、`Product`クラス。</span><span class="sxs-lookup"><span data-stu-id="78b4f-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="78b4f-145">コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="78b4f-145">Adding a Controller</span></span>

<span data-ttu-id="78b4f-146">Web api で、*コント ローラー*は HTTP 要求を処理するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="78b4f-147">ID で指定された 1 つの製品または製品の一覧のいずれかを返すことができるコント ローラーを追加します</span><span class="sxs-lookup"><span data-stu-id="78b4f-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="78b4f-148">ASP.NET MVC を使用している場合を理解しているコント ローラー。</span><span class="sxs-lookup"><span data-stu-id="78b4f-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="78b4f-149">Web API コント ローラーは MVC コント ローラーに似ていますが、継承、 **ApiController**クラスの代わりに、**コント ローラー**クラス。</span><span class="sxs-lookup"><span data-stu-id="78b4f-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="78b4f-150">**ソリューション エクスプ ローラー**、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="78b4f-151">選択**追加**選び**コント ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="78b4f-152">**スキャフォールディングの追加**ダイアログ ボックスで、 **Web API コント ローラー - 空**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="78b4f-153">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="78b4f-154">**コント ローラーの追加**ダイアログ ボックスで、名前、コント ローラー &quot;ProductsController&quot;します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="78b4f-155">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="78b4f-156">スキャフォールディングは、Controllers フォルダーで ProductsController.cs という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="78b4f-157">コント ローラーをという名前のフォルダーに、コント ローラーを配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="78b4f-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="78b4f-158">フォルダー名が、ソース ファイルを整理する便利な方法だけです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-158">The folder name is just a convenient way to organize your source files.</span></span>


<span data-ttu-id="78b4f-159">このファイルがまだ開いていない場合、は、開くファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="78b4f-160">次のようにこのファイル内のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="78b4f-161">例を簡潔にするには、製品は、コント ローラー クラス内で固定長の配列に格納されます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="78b4f-162">もちろん、実際のアプリケーションには、データベースの照会または他の外部データ ソースを使用するは。</span><span class="sxs-lookup"><span data-stu-id="78b4f-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="78b4f-163">コント ローラーには、製品を返す 2 つのメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="78b4f-164">`GetAllProducts`メソッド全体として製品のリストを返します、 **IEnumerable&lt;製品&gt;** 型。</span><span class="sxs-lookup"><span data-stu-id="78b4f-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="78b4f-165">`GetProduct`メソッドは、ID によって 1 つの製品を検索</span><span class="sxs-lookup"><span data-stu-id="78b4f-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="78b4f-166">これで完了です。</span><span class="sxs-lookup"><span data-stu-id="78b4f-166">That's it!</span></span> <span data-ttu-id="78b4f-167">作業用の web API があります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-167">You have a working web API.</span></span> <span data-ttu-id="78b4f-168">コント ローラーの各メソッドは、1 つまたは複数の Uri に対応します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="78b4f-169">コント ローラー メソッド</span><span class="sxs-lookup"><span data-stu-id="78b4f-169">Controller Method</span></span> | <span data-ttu-id="78b4f-170">URI</span><span class="sxs-lookup"><span data-stu-id="78b4f-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="78b4f-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="78b4f-171">GetAllProducts</span></span> | <span data-ttu-id="78b4f-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="78b4f-172">/api/products</span></span> |
| <span data-ttu-id="78b4f-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="78b4f-173">GetProduct</span></span> | <span data-ttu-id="78b4f-174">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="78b4f-174">/api/products/*id*</span></span> |

<span data-ttu-id="78b4f-175">`GetProduct`メソッド、 *id* URI にプレース ホルダーです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="78b4f-176">たとえば、id が 5 の製品を取得する URI は`api/products/5`します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="78b4f-177">Web API がコント ローラーのメソッドに HTTP 要求をルーティングする方法の詳細については、次を参照してください。 [ASP.NET Web API におけるルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="78b4f-178">Javascript や jQuery による Web API を呼び出す</span><span class="sxs-lookup"><span data-stu-id="78b4f-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="78b4f-179">このセクションでは、web API を呼び出す AJAX を使用する HTML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="78b4f-180">AJAX 呼び出しを実行して結果で、ページを更新することも、jQuery を使用します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="78b4f-181">ソリューション エクスプ ローラーでプロジェクトを右クリックし、選択**追加**を選択し、**新しい項目の**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="78b4f-182">**新しい項目の追加**ダイアログ ボックスで、 **Web**ノードの下**Visual c#** を選び、 **HTML ページ**項目。</span><span class="sxs-lookup"><span data-stu-id="78b4f-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="78b4f-183">ページの名前を付けます&quot;index.html&quot;します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="78b4f-184">次のように、このファイル内のすべてを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="78b4f-185">jQuery を取得するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="78b4f-186">この例では使用して、 [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="78b4f-187">ダウンロードすることも[ http://jquery.com/ ](http://jquery.com/)、および"Web API"の ASP.NET プロジェクト テンプレートが jQuery にも含まれています。</span><span class="sxs-lookup"><span data-stu-id="78b4f-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="78b4f-188">製品の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-188">Getting a List of Products</span></span>

<span data-ttu-id="78b4f-189">製品の一覧を取得する HTTP GET 要求を送信&quot;api/製品&quot;します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="78b4f-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)関数は、AJAX 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="78b4f-191">応答には、JSON オブジェクトの配列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="78b4f-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="78b4f-192">`done`関数は、要求が成功した場合に呼び出されるコールバックを指定します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="78b4f-193">コールバックでは、製品情報、DOM を更新します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="78b4f-194">ID によって製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-194">Getting a Product By ID</span></span>

<span data-ttu-id="78b4f-195">ID によって製品を取得する HTTP GET 要求を送信&quot;/api/製品/*id*&quot;ここで、 *id*は製品 ID です。</span><span class="sxs-lookup"><span data-stu-id="78b4f-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="78b4f-196">まだ呼んで`getJSON`この時間が、AJAX 要求を送信する要求 URI に ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="78b4f-197">この要求からの応答は、1 つの製品の JSON 表現です。</span><span class="sxs-lookup"><span data-stu-id="78b4f-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="78b4f-198">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="78b4f-198">Running the Application</span></span>

<span data-ttu-id="78b4f-199">F5 キーを押して、アプリケーションのデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="78b4f-200">Web ページは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="78b4f-201">ID によって製品を取得するには、ID を入力し、検索 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="78b4f-202">無効な ID を入力すると、サーバーは HTTP エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="78b4f-203">F12 キーを使用して、HTTP 要求と応答を表示するには</span><span class="sxs-lookup"><span data-stu-id="78b4f-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="78b4f-204">HTTP サービスを使用する場合は、HTTP 要求を表示、メッセージを要求する非常に便利ですができます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="78b4f-205">Internet Explorer 9 で F12 開発者ツールを使用して、これを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="78b4f-206">Internet Explorer 9 からキーを押します。 **F12**ツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="78b4f-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="78b4f-207">をクリックして、**ネットワーク**タブ キーを押します**キャプチャ開始**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="78b4f-208">キーを押して、web ページに移動**F5** web ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="78b4f-209">Internet Explorer では、ブラウザーと web サーバー間の HTTP トラフィックをキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="78b4f-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="78b4f-210">概要ビューは、ページのすべてのネットワーク トラフィックを示しています。</span><span class="sxs-lookup"><span data-stu-id="78b4f-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="78b4f-211">相対 URI のエントリを見つけ"api/製品/"。</span><span class="sxs-lookup"><span data-stu-id="78b4f-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="78b4f-212">このエントリを選択し、クリックして**詳細ビューに移動**します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="78b4f-213">詳細ビューでは、要求と応答ヘッダーと本文を表示するタブがあります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="78b4f-214">たとえばをクリックする、**要求ヘッダー**  タブで、クライアントが要求された参照できます&quot;、application/json&quot; Accept ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="78b4f-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="78b4f-215">応答の本文 タブをクリックすると、製品一覧が JSON にシリアル化する方法がわかります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="78b4f-216">その他のブラウザーでは、同様の機能があります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="78b4f-217">もう 1 つの便利なツールが[Fiddler](http://www.fiddler2.com/fiddler2/)の web デバッグ プロキシです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="78b4f-218">使用できます Fiddler、HTTP トラフィックを表示して、HTTP 要求を作成することも、要求で HTTP ヘッダーを完全に制御を提供します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="78b4f-219">Azure で実行されているこのアプリを参照してください。</span><span class="sxs-lookup"><span data-stu-id="78b4f-219">See this App Running on Azure</span></span>

<span data-ttu-id="78b4f-220">ライブ web アプリとして実行されている完成したサイトを参照してもよろしいですか。</span><span class="sxs-lookup"><span data-stu-id="78b4f-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="78b4f-221">Azure アカウントに、アプリの完全なバージョンを展開するには、次のボタンをクリックするだけです。</span><span class="sxs-lookup"><span data-stu-id="78b4f-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="78b4f-222">このソリューションを Azure にデプロイする Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="78b4f-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="78b4f-223">アカウントがいない場合は、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="78b4f-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="78b4f-224">[無料 Azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-クレジットを取得する有料の Azure サービスを使用することができますをも使用されるアカウントは維持する最大無料の Azure サービスを使用します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="78b4f-225">[MSDN サブスクライバーの特典をアクティブ化](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN サブスクリプションでは、クレジットの有料の Azure サービスを使用することができる毎月。</span><span class="sxs-lookup"><span data-stu-id="78b4f-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78b4f-226">次の手順</span><span class="sxs-lookup"><span data-stu-id="78b4f-226">Next Steps</span></span>

- <span data-ttu-id="78b4f-227">POST、PUT、および DELETE 操作をサポートし、データベースに書き込みます HTTP サービスのより完全な例を参照してください。 [Entity Framework 6 で Web API 2 を使用して](../data/using-web-api-with-entity-framework/part-1.md)します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="78b4f-228">HTTP サービス上で流動性と応答性の高い web アプリケーションを作成する方法の詳細は、次を参照してください。 [ASP.NET Single Page Application](../../../single-page-application/index.md)します。</span><span class="sxs-lookup"><span data-stu-id="78b4f-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="78b4f-229">Visual Studio web プロジェクトを Azure App Service にデプロイする方法については、次を参照してください。 [Azure App Service で ASP.NET web アプリを作成](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)です。</span><span class="sxs-lookup"><span data-stu-id="78b4f-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
