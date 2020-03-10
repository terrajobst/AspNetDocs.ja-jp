---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4.x で CRUD 操作を有効にする
author: MikeWasson
description: チュートリアルでは、ASP.NET 4.x の ASP.NET Web API を使用して、HTTP サービスで CRUD 操作をサポートする方法を示します。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448042"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="b4615-103">ASP.NET Web API 1 で CRUD 操作を有効にする</span><span class="sxs-lookup"><span data-stu-id="b4615-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="b4615-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b4615-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b4615-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="b4615-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="b4615-106">このチュートリアルでは、ASP.NET 4.x の ASP.NET Web API を使用して、HTTP サービスで CRUD 操作をサポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b4615-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b4615-107">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="b4615-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b4615-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b4615-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="b4615-109">Web API 1 (Web API 2 でも動作)</span><span class="sxs-lookup"><span data-stu-id="b4615-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="b4615-110">CRUD は、4つの基本的なデータベース操作である &quot;作成、読み取り、更新、および削除の&quot; を意味します。</span><span class="sxs-lookup"><span data-stu-id="b4615-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="b4615-111">多くの HTTP サービスは、REST や REST に似た Api を使用して CRUD 操作もモデル化します。</span><span class="sxs-lookup"><span data-stu-id="b4615-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="b4615-112">このチュートリアルでは、非常に単純な web API を構築して製品の一覧を管理します。</span><span class="sxs-lookup"><span data-stu-id="b4615-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="b4615-113">各製品には、名前、価格、カテゴリ (&quot;toys&quot; や &quot;ハードウェア&quot;など)、および製品 ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="b4615-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="b4615-114">Products API は、次のメソッドを公開します。</span><span class="sxs-lookup"><span data-stu-id="b4615-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="b4615-115">アクション</span><span class="sxs-lookup"><span data-stu-id="b4615-115">Action</span></span> | <span data-ttu-id="b4615-116">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="b4615-116">HTTP method</span></span> | <span data-ttu-id="b4615-117">相対 URI</span><span class="sxs-lookup"><span data-stu-id="b4615-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4615-118">すべての製品の一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="b4615-118">Get a list of all products</span></span> | <span data-ttu-id="b4615-119">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-119">GET</span></span> | <span data-ttu-id="b4615-120">/api/products</span><span class="sxs-lookup"><span data-stu-id="b4615-120">/api/products</span></span> |
| <span data-ttu-id="b4615-121">ID によって製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="b4615-121">Get a product by ID</span></span> | <span data-ttu-id="b4615-122">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-122">GET</span></span> | <span data-ttu-id="b4615-123">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="b4615-123">/api/products/*id*</span></span> |
| <span data-ttu-id="b4615-124">カテゴリ別に製品を取得する</span><span class="sxs-lookup"><span data-stu-id="b4615-124">Get a product by category</span></span> | <span data-ttu-id="b4615-125">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-125">GET</span></span> | <span data-ttu-id="b4615-126">/api/products? category =*category*</span><span class="sxs-lookup"><span data-stu-id="b4615-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="b4615-127">新しい製品を作成する</span><span class="sxs-lookup"><span data-stu-id="b4615-127">Create a new product</span></span> | <span data-ttu-id="b4615-128">POST</span><span class="sxs-lookup"><span data-stu-id="b4615-128">POST</span></span> | <span data-ttu-id="b4615-129">/api/products</span><span class="sxs-lookup"><span data-stu-id="b4615-129">/api/products</span></span> |
| <span data-ttu-id="b4615-130">製品を更新する</span><span class="sxs-lookup"><span data-stu-id="b4615-130">Update a product</span></span> | <span data-ttu-id="b4615-131">PUT</span><span class="sxs-lookup"><span data-stu-id="b4615-131">PUT</span></span> | <span data-ttu-id="b4615-132">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="b4615-132">/api/products/*id*</span></span> |
| <span data-ttu-id="b4615-133">製品を削除する</span><span class="sxs-lookup"><span data-stu-id="b4615-133">Delete a product</span></span> | <span data-ttu-id="b4615-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="b4615-134">DELETE</span></span> | <span data-ttu-id="b4615-135">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="b4615-135">/api/products/*id*</span></span> |

<span data-ttu-id="b4615-136">Uri の一部には、パスに製品 ID が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b4615-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="b4615-137">たとえば、ID が28の製品を取得するために、クライアントは `http://hostname/api/products/28`の GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="b4615-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="b4615-138">リソース</span><span class="sxs-lookup"><span data-stu-id="b4615-138">Resources</span></span>

<span data-ttu-id="b4615-139">Products API は、次の2つのリソースの種類の Uri を定義します。</span><span class="sxs-lookup"><span data-stu-id="b4615-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="b4615-140">リソース</span><span class="sxs-lookup"><span data-stu-id="b4615-140">Resource</span></span> | <span data-ttu-id="b4615-141">URI</span><span class="sxs-lookup"><span data-stu-id="b4615-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="b4615-142">すべての製品の一覧。</span><span class="sxs-lookup"><span data-stu-id="b4615-142">The list of all the products.</span></span> | <span data-ttu-id="b4615-143">/api/products</span><span class="sxs-lookup"><span data-stu-id="b4615-143">/api/products</span></span> |
| <span data-ttu-id="b4615-144">個々の製品。</span><span class="sxs-lookup"><span data-stu-id="b4615-144">An individual product.</span></span> | <span data-ttu-id="b4615-145">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="b4615-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="b4615-146">メソッド</span><span class="sxs-lookup"><span data-stu-id="b4615-146">Methods</span></span>

<span data-ttu-id="b4615-147">次のように、4つの主要な HTTP メソッド (GET、PUT、POST、および DELETE) を CRUD 操作にマップできます。</span><span class="sxs-lookup"><span data-stu-id="b4615-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="b4615-148">GET は、指定された URI にあるリソースの表現を取得します。</span><span class="sxs-lookup"><span data-stu-id="b4615-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="b4615-149">GET はサーバーに副作用を与えません。</span><span class="sxs-lookup"><span data-stu-id="b4615-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="b4615-150">PUT は、指定された URI のリソースを更新します。</span><span class="sxs-lookup"><span data-stu-id="b4615-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="b4615-151">サーバーで新しい Uri を指定できるようにする場合は、PUT を使用して、指定した URI で新しいリソースを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b4615-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="b4615-152">このチュートリアルでは、API は PUT を使用した作成をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="b4615-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="b4615-153">POST によって新しいリソースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-153">POST creates a new resource.</span></span> <span data-ttu-id="b4615-154">サーバーは、新しいオブジェクトの URI を割り当て、この URI を応答メッセージの一部として返します。</span><span class="sxs-lookup"><span data-stu-id="b4615-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="b4615-155">DELETE は、指定された URI にあるリソースを削除します。</span><span class="sxs-lookup"><span data-stu-id="b4615-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="b4615-156">注: PUT メソッドは、product エンティティ全体を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b4615-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="b4615-157">つまり、クライアントは、更新された製品の完全な表現を送信することを想定しています。</span><span class="sxs-lookup"><span data-stu-id="b4615-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="b4615-158">部分更新をサポートする場合は、PATCH メソッドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b4615-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="b4615-159">このチュートリアルは PATCH を実装していません。</span><span class="sxs-lookup"><span data-stu-id="b4615-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="b4615-160">新しい Web API プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="b4615-160">Create a New Web API Project</span></span>

<span data-ttu-id="b4615-161">まず、Visual Studio を実行し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="b4615-162">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="b4615-163">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="b4615-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="b4615-164">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="b4615-165">プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="b4615-166">プロジェクトに ProductStore という名前を &quot;&quot; [ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="b4615-167">**[New ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[Web API]** を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="b4615-168">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="b4615-168">Adding a Model</span></span>

<span data-ttu-id="b4615-169">*"モデル"* は、アプリケーションでデータを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="b4615-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="b4615-170">ASP.NET Web API では、厳密に型指定された CLR オブジェクトをモデルとして使用できます。これらのオブジェクトは、クライアントの XML または JSON に自動的にシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="b4615-171">ProductStore API では、データは製品で構成されているため、`Product`という名前の新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b4615-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="b4615-172">ソリューション エクスプローラーが表示されていない場合は、 **[表示]** メニューをクリックし、 **[ソリューション エクスプローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="b4615-173">ソリューションエクスプローラーで、 **[モデル]** フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="b4615-174">コンテキストメニューから **[追加]** を選択し、 **[クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="b4615-175">クラスに Product&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b4615-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="b4615-176">次のプロパティを `Product` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="b4615-177">リポジトリの追加</span><span class="sxs-lookup"><span data-stu-id="b4615-177">Adding a Repository</span></span>

<span data-ttu-id="b4615-178">製品のコレクションを格納する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4615-178">We need to store a collection of products.</span></span> <span data-ttu-id="b4615-179">サービス実装からコレクションを分離することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b4615-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="b4615-180">このようにして、サービスクラスを書き直すことなくバッキングストアを変更できます。</span><span class="sxs-lookup"><span data-stu-id="b4615-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="b4615-181">この種類の設計は、*リポジトリ*パターンと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="b4615-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="b4615-182">まず、リポジトリのジェネリックインターフェイスを定義します。</span><span class="sxs-lookup"><span data-stu-id="b4615-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="b4615-183">ソリューションエクスプローラーで、 **[モデル]** フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="b4615-184">**[追加]** を選択し、 **[新しい項目]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="b4615-185">**[テンプレート]** ウィンドウで、 **[インストールされ]** たC#テンプレート を選択し、ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="b4615-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="b4615-186">でC#、 **[コード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-186">Under C#, select **Code**.</span></span> <span data-ttu-id="b4615-187">コードテンプレートの一覧で、 **[インターフェイス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="b4615-188">インターフェイスに IProductRepository&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b4615-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="b4615-189">次の実装を追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="b4615-190">次に、&quot;ProductRepository という名前の別のクラスを [モデル] フォルダーに追加します。&quot; このクラスは、`IProductRepository` インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="b4615-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="b4615-191">次の実装を追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="b4615-192">リポジトリでは、リストはローカルメモリ内に保持されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="b4615-193">これはチュートリアルでは問題ありませんが、実際のアプリケーションでは、データベースまたはクラウドストレージにデータを外部に格納することになります。</span><span class="sxs-lookup"><span data-stu-id="b4615-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="b4615-194">リポジトリパターンを使用すると、後で実装を変更しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="b4615-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="b4615-195">Web API コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="b4615-195">Adding a Web API Controller</span></span>

<span data-ttu-id="b4615-196">ASP.NET MVC を使用している場合は、既にコントローラーに精通しています。</span><span class="sxs-lookup"><span data-stu-id="b4615-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="b4615-197">ASP.NET Web API では、*コントローラー*は、クライアントからの HTTP 要求を処理するクラスです。</span><span class="sxs-lookup"><span data-stu-id="b4615-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="b4615-198">新しいプロジェクトウィザードでは、プロジェクトの作成時に2つのコントローラーが作成されました。</span><span class="sxs-lookup"><span data-stu-id="b4615-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="b4615-199">これらのファイルを表示するには、ソリューションエクスプローラーで [Controllers] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="b4615-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="b4615-200">HomeController は従来の ASP.NET MVC コントローラーです。</span><span class="sxs-lookup"><span data-stu-id="b4615-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="b4615-201">これは、サイトの HTML ページを提供する役割を担い、web API に直接関連するものではありません。</span><span class="sxs-lookup"><span data-stu-id="b4615-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="b4615-202">WebAPI controller の例です。</span><span class="sxs-lookup"><span data-stu-id="b4615-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="b4615-203">ソリューションエクスプローラーのファイルを右クリックし、[削除] を選択して、[を削除] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="b4615-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="b4615-204">次のように、新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="b4615-205">**ソリューション エクスプローラー**で、[コントローラー] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="b4615-206">**[追加]** 、 **[コントローラー]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="b4615-207">コントローラーの**追加**ウィザードで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b4615-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="b4615-208">**[テンプレート]** ボックスの一覧で、 **[空の API コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b4615-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="b4615-209">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b4615-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="b4615-210">コントローラーを Controllers という名前のフォルダーに配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b4615-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="b4615-211">フォルダー名は重要ではありません。これは、ソースファイルを整理するための便利な方法にすぎません。</span><span class="sxs-lookup"><span data-stu-id="b4615-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="b4615-212">**コントローラーの追加**ウィザードでは、ProductsController.cs という名前のファイルが Controllers フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="b4615-213">このファイルがまだ開かれていない場合は、ファイルをダブルクリックして開きます。</span><span class="sxs-lookup"><span data-stu-id="b4615-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="b4615-214">次の **using** ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="b4615-215">**Iproductrepository**インスタンスを保持するフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="b4615-216">コントローラーが `IProductRepository`の特定の実装に結び付けられるため、コントローラーで `new ProductRepository()` を呼び出すことは最適な設計ではありません。</span><span class="sxs-lookup"><span data-stu-id="b4615-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="b4615-217">より適切な方法については、「 [WEB API 依存関係競合回避モジュールの使用](../advanced/dependency-injection.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b4615-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="b4615-218">リソースを取得する</span><span class="sxs-lookup"><span data-stu-id="b4615-218">Getting a Resource</span></span>

<span data-ttu-id="b4615-219">ProductStore API は、いくつかの &quot;読み取り&quot; アクションを HTTP GET メソッドとして公開します。</span><span class="sxs-lookup"><span data-stu-id="b4615-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="b4615-220">各アクションは、`ProductsController` クラスのメソッドに対応します。</span><span class="sxs-lookup"><span data-stu-id="b4615-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="b4615-221">アクション</span><span class="sxs-lookup"><span data-stu-id="b4615-221">Action</span></span> | <span data-ttu-id="b4615-222">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="b4615-222">HTTP method</span></span> | <span data-ttu-id="b4615-223">相対 URI</span><span class="sxs-lookup"><span data-stu-id="b4615-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4615-224">すべての製品の一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="b4615-224">Get a list of all products</span></span> | <span data-ttu-id="b4615-225">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-225">GET</span></span> | <span data-ttu-id="b4615-226">/api/products</span><span class="sxs-lookup"><span data-stu-id="b4615-226">/api/products</span></span> |
| <span data-ttu-id="b4615-227">ID によって製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="b4615-227">Get a product by ID</span></span> | <span data-ttu-id="b4615-228">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-228">GET</span></span> | <span data-ttu-id="b4615-229">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="b4615-229">/api/products/*id*</span></span> |
| <span data-ttu-id="b4615-230">カテゴリ別に製品を取得する</span><span class="sxs-lookup"><span data-stu-id="b4615-230">Get a product by category</span></span> | <span data-ttu-id="b4615-231">GET</span><span class="sxs-lookup"><span data-stu-id="b4615-231">GET</span></span> | <span data-ttu-id="b4615-232">/api/products? category =*category*</span><span class="sxs-lookup"><span data-stu-id="b4615-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="b4615-233">すべての製品の一覧を取得するには、次のメソッドを `ProductsController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="b4615-234">メソッド名は &quot;Get&quot;で始まるため、規約によって GET 要求にマップされます。</span><span class="sxs-lookup"><span data-stu-id="b4615-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="b4615-235">また、メソッドにはパラメーターがないため、パスに *&quot;id&quot;* セグメントを含まない URI にマップされます。</span><span class="sxs-lookup"><span data-stu-id="b4615-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="b4615-236">ID で製品を取得するには、次のメソッドを `ProductsController` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="b4615-237">このメソッド名も &quot;Get&quot;で始まりますが、メソッドには*id*という名前のパラメーターがあります。このパラメーターは、URI パスの &quot;id&quot; セグメントにマップされます。</span><span class="sxs-lookup"><span data-stu-id="b4615-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="b4615-238">ASP.NET Web API framework では、ID がパラメーターの正しいデータ型 (**int**) に自動的に変換されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="b4615-239">*Id*が有効でない場合、getproduct メソッドは**HttpResponseException**型の例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="b4615-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="b4615-240">この例外は、フレームワークによって 404 (見つかりません) エラーに変換されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="b4615-241">最後に、カテゴリ別に製品を検索するメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="b4615-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="b4615-242">要求 URI にクエリ文字列が含まれている場合、Web API はクエリパラメーターをコントローラーメソッドのパラメーターと照合しようとします。</span><span class="sxs-lookup"><span data-stu-id="b4615-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="b4615-243">そのため、"api/products? category =*category*" という形式の URI は、このメソッドにマップされます。</span><span class="sxs-lookup"><span data-stu-id="b4615-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="b4615-244">リソースの作成</span><span class="sxs-lookup"><span data-stu-id="b4615-244">Creating a Resource</span></span>

<span data-ttu-id="b4615-245">次に、`ProductsController` クラスにメソッドを追加して、新しい製品を作成します。</span><span class="sxs-lookup"><span data-stu-id="b4615-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="b4615-246">メソッドの単純な実装を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b4615-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="b4615-247">この方法については、次の2点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b4615-247">Note two things about this method:</span></span>

- <span data-ttu-id="b4615-248">メソッド名は &quot;Post...&quot;で始まります。</span><span class="sxs-lookup"><span data-stu-id="b4615-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="b4615-249">新しい製品を作成するために、クライアントは HTTP POST 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="b4615-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="b4615-250">メソッドは、Product 型のパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="b4615-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="b4615-251">Web API では、複合型のパラメーターは要求本文から逆シリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="b4615-252">したがって、クライアントは、XML 形式または JSON 形式のいずれかで、製品オブジェクトのシリアル化された表現を送信することを想定しています。</span><span class="sxs-lookup"><span data-stu-id="b4615-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="b4615-253">この実装は機能しますが、まだ完全ではありません。</span><span class="sxs-lookup"><span data-stu-id="b4615-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="b4615-254">HTTP 応答には、次のようなものが含まれているのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="b4615-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="b4615-255">**応答コード:** 既定では、Web API フレームワークは応答状態コードを 200 (OK) に設定します。</span><span class="sxs-lookup"><span data-stu-id="b4615-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="b4615-256">ただし、HTTP/1.1 プロトコルによっては、POST 要求によってリソースが作成されるときに、サーバーは状態 201 (Created) を使用して応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4615-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="b4615-257">**場所:** サーバーは、リソースを作成するときに、応答の Location ヘッダーに新しいリソースの URI を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4615-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="b4615-258">ASP.NET Web API を使用すると、HTTP 応答メッセージを簡単に操作できます。</span><span class="sxs-lookup"><span data-stu-id="b4615-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="b4615-259">次に、強化された実装を示します。</span><span class="sxs-lookup"><span data-stu-id="b4615-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="b4615-260">メソッドの戻り値の型が**HttpResponseMessage**になっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b4615-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="b4615-261">製品の代わりに**HttpResponseMessage**を返すことによって、ステータスコードや場所ヘッダーなどの HTTP 応答メッセージの詳細を制御できます。</span><span class="sxs-lookup"><span data-stu-id="b4615-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="b4615-262">**CreateResponse**メソッドは、 **HttpResponseMessage**を作成し、シリアル化された製品オブジェクトの表現を応答メッセージの本文に自動的に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="b4615-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="b4615-263">この例では、`Product`は検証されません。</span><span class="sxs-lookup"><span data-stu-id="b4615-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="b4615-264">モデルの検証の詳細については、「 [ASP.NET Web API でのモデルの検証](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b4615-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="b4615-265">リソースの更新</span><span class="sxs-lookup"><span data-stu-id="b4615-265">Updating a Resource</span></span>

<span data-ttu-id="b4615-266">PUT を使用して製品を更新するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="b4615-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="b4615-267">メソッド名は &quot;Put...&quot;で始まります。これにより、Web API は PUT 要求と照合します。</span><span class="sxs-lookup"><span data-stu-id="b4615-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="b4615-268">このメソッドは、製品 ID と更新された製品の2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="b4615-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="b4615-269">*Id*パラメーターは URI パスから取得され、 *product*パラメーターは要求本文から逆シリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="b4615-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="b4615-270">既定では、ASP.NET Web API framework は、要求本文からルートと複合型からの単純なパラメーター型を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="b4615-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="b4615-271">リソースの削除</span><span class="sxs-lookup"><span data-stu-id="b4615-271">Deleting a Resource</span></span>

<span data-ttu-id="b4615-272">リソースを削除するには、"削除..." を定義します。b.</span><span class="sxs-lookup"><span data-stu-id="b4615-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="b4615-273">削除要求が成功すると、状態を説明するエンティティ本体を含むステータス 200 (OK) を返すことができます。削除がまだ保留中の場合、状態 202 (受理)または、エンティティ本体のない状態 204 (コンテンツなし)。</span><span class="sxs-lookup"><span data-stu-id="b4615-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="b4615-274">この場合、`DeleteProduct` メソッドには `void` 戻り値の型があるため、ASP.NET Web API はこれを自動的に状態コード 204 (コンテンツなし) に変換します。</span><span class="sxs-lookup"><span data-stu-id="b4615-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
