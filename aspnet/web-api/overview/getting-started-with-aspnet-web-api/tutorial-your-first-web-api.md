---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)-ASP.NET 4.X の概要
author: MikeWasson
description: コードを使用したチュートリアル。 製品の一覧を返す Web API を作成するには、ASP.NET Web API を使用します。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 2717d93f47be9d4a6548731d8deeca312b25f39f
ms.sourcegitcommit: 9e3ca74997a67c18589729d4b7303799905473eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79084052"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="1ae85-104">ASP.NET Web API 2 (C#) を使ってみる</span><span class="sxs-lookup"><span data-stu-id="1ae85-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="1ae85-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1ae85-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1ae85-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="1ae85-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="1ae85-107">このチュートリアルでは、ASP.NET Web API を使用して、製品の一覧を返す Web API を作成します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="1ae85-108">HTTP は web ページを提供するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="1ae85-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="1ae85-109">HTTP は、サービスとデータを公開する Api を構築するための強力なプラットフォームでもあります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="1ae85-110">HTTP はシンプルで柔軟性があり、ユビキタスです。</span><span class="sxs-lookup"><span data-stu-id="1ae85-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="1ae85-111">考えられるほとんどすべてのプラットフォームは HTTP ライブラリを持っているので、HTTP サービスは、ブラウザー、モバイルデバイス、従来のデスクトップアプリケーションを含む広範なクライアントに接続できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="1ae85-112">ASP.NET Web API は、.NET Framework 上に Web Api を構築するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="1ae85-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1ae85-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="1ae85-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="1ae85-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1ae85-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="1ae85-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="1ae85-115">Web API 2</span></span>

<span data-ttu-id="1ae85-116">このチュートリアルの新しいバージョンについては、「 [ASP.NET Core と Visual Studio For Windows で WEB API を作成する](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ae85-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="1ae85-117">Web API プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="1ae85-117">Create a Web API Project</span></span>

<span data-ttu-id="1ae85-118">このチュートリアルでは、ASP.NET Web API を使用して、製品の一覧を返す Web API を作成します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="1ae85-119">フロントエンド web ページでは、jQuery を使用して結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="1ae85-120">Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="1ae85-121">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="1ae85-122">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="1ae85-123">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1ae85-124">プロジェクトテンプレートの一覧で、 **[ASP.NET Web Application]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="1ae85-125">プロジェクトに "製品アプリ" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="1ae85-126">**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="1ae85-127">&quot;のフォルダーとコア参照を追加 &quot;には、**WEB API** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="1ae85-128">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="1ae85-129">&quot;Web API&quot; テンプレートを使用して Web API プロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="1ae85-130">Web API テンプレートでは、ASP.NET MVC を使用して API のヘルプページを提供します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="1ae85-131">このチュートリアルでは、MVC を使用せずに Web API を表示するため、空のテンプレートを使用しています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="1ae85-132">一般に、Web API を使用するために ASP.NET MVC を理解する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1ae85-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="1ae85-133">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="1ae85-133">Adding a Model</span></span>

<span data-ttu-id="1ae85-134">*"モデル"* は、アプリケーションでデータを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1ae85-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="1ae85-135">ASP.NET Web API は、モデルを JSON、XML、またはその他の形式に自動的にシリアル化し、シリアル化されたデータを HTTP 応答メッセージの本文に書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="1ae85-136">クライアントがシリアル化形式を読み取ることができる限り、オブジェクトを逆シリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="1ae85-137">ほとんどのクライアントは、XML または JSON を解析できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="1ae85-138">さらに、クライアントは、HTTP 要求メッセージで Accept ヘッダーを設定することによって、必要な形式を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="1ae85-139">まず、製品を表す単純なモデルを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ae85-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="1ae85-140">ソリューション エクスプローラーが表示されていない場合は、 **[表示]** メニューをクリックし、 **[ソリューション エクスプローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="1ae85-141">ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="1ae85-142">コンテキスト メニューの **[追加]** を選択し、 **[クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="1ae85-143">クラスに Product&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="1ae85-144">次のプロパティを `Product` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="1ae85-145">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="1ae85-145">Adding a Controller</span></span>

<span data-ttu-id="1ae85-146">Web API では、"*コントローラー*" は、HTTP 要求を処理するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1ae85-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="1ae85-147">製品の一覧または ID で指定された1つの製品のいずれかを返すことができるコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae85-148">ASP.NET MVC を使用している場合は、既にコントローラーに精通しています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="1ae85-149">Web API コントローラーは MVC コントローラーに似ていますが、**コントローラー**クラスではなく**ApiController**クラスを継承します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="1ae85-150">**ソリューション エクスプローラー**で、[コントローラー] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="1ae85-151">**[追加]** 、 **[コントローラー]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="1ae85-152">**[スキャフォールディングの追加]** ダイアログで **[Web API コントローラー - 空]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="1ae85-153">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="1ae85-154">**[コントローラーの追加]** ダイアログボックスで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="1ae85-155">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="1ae85-156">スキャフォールディングによって、Controllers フォルダーに ProductsController.cs という名前のファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="1ae85-157">コントローラーを Controllers という名前のフォルダーに配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1ae85-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="1ae85-158">フォルダー名は、ソースファイルを整理するための便利な方法にすぎません。</span><span class="sxs-lookup"><span data-stu-id="1ae85-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="1ae85-159">このファイルがまだ開かれていない場合は、ファイルをダブルクリックして開きます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="1ae85-160">このファイルのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="1ae85-161">例を単純にするために、製品はコントローラークラス内の固定配列に格納されています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="1ae85-162">もちろん、実際のアプリケーションでは、データベースに対してクエリを実行したり、他の外部データソースを使用したりすることがあります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="1ae85-163">コントローラーは、製品を返す2つのメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="1ae85-164">`GetAllProducts` メソッドは、製品のリスト全体を**IEnumerable&lt;Product&gt;** 型として返します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="1ae85-165">`GetProduct` メソッドは、1つの製品をその ID で検索します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="1ae85-166">これで完了です。</span><span class="sxs-lookup"><span data-stu-id="1ae85-166">That's it!</span></span> <span data-ttu-id="1ae85-167">Web API が動作しています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-167">You have a working web API.</span></span> <span data-ttu-id="1ae85-168">コントローラーの各メソッドは、1つまたは複数の Uri に対応します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="1ae85-169">コントローラーメソッド</span><span class="sxs-lookup"><span data-stu-id="1ae85-169">Controller Method</span></span> | <span data-ttu-id="1ae85-170">URI</span><span class="sxs-lookup"><span data-stu-id="1ae85-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="1ae85-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="1ae85-171">GetAllProducts</span></span> | <span data-ttu-id="1ae85-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="1ae85-172">/api/products</span></span> |
| <span data-ttu-id="1ae85-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="1ae85-173">GetProduct</span></span> | <span data-ttu-id="1ae85-174">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="1ae85-174">/api/products/*id*</span></span> |

<span data-ttu-id="1ae85-175">`GetProduct` メソッドの場合、URI の*id*はプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="1ae85-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="1ae85-176">たとえば、ID が5の製品を取得するために、URI は `api/products/5`ます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="1ae85-177">Web API が HTTP 要求をコントローラーメソッドにルーティングする方法の詳細については、「 [ASP.NET Web API でのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ae85-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="1ae85-178">Javascript と jQuery を使用した Web API の呼び出し</span><span class="sxs-lookup"><span data-stu-id="1ae85-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="1ae85-179">このセクションでは、AJAX を使用して web API を呼び出す HTML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="1ae85-180">ここでは、jQuery を使用して AJAX 呼び出しを行い、結果を使用してページを更新します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="1ae85-181">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="1ae85-182">**[新しい項目の追加]** ダイアログで、 **[ビジュアルC# ]** の下にある **[Web]** ノードを選択し、 **[HTML ページ]** 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="1ae85-183">ページに「index .html&quot;&quot;名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="1ae85-184">このファイル内のすべてを次のものに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="1ae85-185">jQuery を取得するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="1ae85-186">この例では、 [Microsoft AJAX CDN](../../../ajax/cdn/overview.md)を使用しました。</span><span class="sxs-lookup"><span data-stu-id="1ae85-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="1ae85-187">また、 [http://jquery.com/](http://jquery.com/)からダウンロードすることもできます。また、ASP.NET "Web API" プロジェクトテンプレートには jQuery も含まれています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="1ae85-188">製品の一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="1ae85-188">Getting a List of Products</span></span>

<span data-ttu-id="1ae85-189">製品の一覧を取得するには、HTTP GET 要求を &quot;/api&quot;に送信します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="1ae85-190">JQuery [Getjson](http://api.jquery.com/jQuery.getJSON/)関数は、AJAX 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="1ae85-191">応答には、JSON オブジェクトの配列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-191">The response contains array of JSON objects.</span></span> <span data-ttu-id="1ae85-192">`done` 関数は、要求が成功した場合に呼び出されるコールバックを指定します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="1ae85-193">コールバックで、DOM を製品情報で更新します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="1ae85-194">ID で製品を取得する</span><span class="sxs-lookup"><span data-stu-id="1ae85-194">Getting a Product By ID</span></span>

<span data-ttu-id="1ae85-195">ID で製品を取得するには、HTTP GET 要求を &quot;/api/*id*&quot;に送信します。ここで、 *ID*は製品 id です。</span><span class="sxs-lookup"><span data-stu-id="1ae85-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="1ae85-196">引き続き AJAX 要求を送信するために `getJSON` を呼び出しますが、今回は要求 URI に ID を含めます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="1ae85-197">この要求からの応答は、1つの製品の JSON 表現です。</span><span class="sxs-lookup"><span data-stu-id="1ae85-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="1ae85-198">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="1ae85-198">Running the Application</span></span>

<span data-ttu-id="1ae85-199">F5 キーを押してアプリケーションのデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="1ae85-200">Web ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="1ae85-201">ID で製品を取得するには、ID を入力し、[検索] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="1ae85-202">無効な ID を入力すると、サーバーから HTTP エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="1ae85-203">F12 を使用した HTTP 要求と応答の表示</span><span class="sxs-lookup"><span data-stu-id="1ae85-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="1ae85-204">HTTP サービスを使用している場合は、HTTP 要求メッセージと応答メッセージを確認すると非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="1ae85-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and response messages.</span></span> <span data-ttu-id="1ae85-205">これを行うには、Internet Explorer 9 の F12 開発者ツールを使用します。</span><span class="sxs-lookup"><span data-stu-id="1ae85-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="1ae85-206">Internet Explorer 9 で、 **F12**キーを押してツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="1ae85-207">**[ネットワーク]** タブをクリックし、 **[キャプチャの開始]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="1ae85-208">次に、web ページに戻り、 **F5**キーを押して web ページを再読み込みします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="1ae85-209">Internet Explorer は、ブラウザーと web サーバー間の HTTP トラフィックをキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="1ae85-210">[概要] ビューには、ページのすべてのネットワークトラフィックが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="1ae85-211">相対 URI "api/products/" のエントリを見つけます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="1ae85-212">このエントリを選択し、[**詳細ビューにジャンプ] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="1ae85-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="1ae85-213">詳細ビューには、要求と応答のヘッダーと本文を表示するタブがあります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="1ae85-214">たとえば、 **[要求ヘッダー]** タブをクリックすると、クライアントが Accept ヘッダーで &quot;application/json&quot; を要求したことがわかります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="1ae85-215">[応答本文] タブをクリックすると、製品リストが JSON にシリアル化された方法を確認できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="1ae85-216">他のブラウザーも同様の機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="1ae85-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="1ae85-217">もう1つの便利なツールとして、web デバッグプロキシ[Fiddler](http://www.fiddler2.com/fiddler2/)があります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="1ae85-218">Fiddler を使用して HTTP トラフィックを表示することができます。また、http 要求を構成することもできます。これにより、要求の HTTP ヘッダーを完全に制御できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="1ae85-219">このアプリが Azure で実行されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="1ae85-219">See this App Running on Azure</span></span>

<span data-ttu-id="1ae85-220">完成したサイトがライブ web アプリとして実行されていることを確認しますか?</span><span class="sxs-lookup"><span data-stu-id="1ae85-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="1ae85-221">次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="1ae85-222">このソリューションを Azure にデプロイするには、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="1ae85-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="1ae85-223">まだアカウントを持っていない場合は、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="1ae85-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="1ae85-224">[無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="1ae85-225">[Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。</span><span class="sxs-lookup"><span data-stu-id="1ae85-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ae85-226">次の手順</span><span class="sxs-lookup"><span data-stu-id="1ae85-226">Next Steps</span></span>

- <span data-ttu-id="1ae85-227">POST、PUT、DELETE の各アクションとデータベースへの書き込みをサポートする HTTP サービスの完全な例については、「 [Using WEB API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ae85-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="1ae85-228">HTTP サービス上に流動的で応答性の高い web アプリケーションを作成する方法の詳細については、「 [ASP.NET Single Page Application](../../../single-page-application/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ae85-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="1ae85-229">Azure App Service に Visual Studio web プロジェクトを配置する方法の詳細については、「 [Azure App Service での ASP.NET web アプリの作成](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ae85-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
