---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 を使用して OData v3 エンドポイントを作成する |Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。 OData は、データの構造化、データのクエリ、データの操作を行うための統一された方法を提供します...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600429"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="95df2-104">Web API 2 で OData v3 エンドポイントを作成する</span><span class="sxs-lookup"><span data-stu-id="95df2-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="95df2-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="95df2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="95df2-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="95df2-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="95df2-107">[Open Data Protocol](http://www.odata.org/) (OData) は、web 用のデータアクセスプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="95df2-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="95df2-108">OData は、CRUD 操作 (作成、読み取り、更新、および削除) を使用してデータを構造化し、データを照会し、データセットを操作するための統一された方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="95df2-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="95df2-109">OData は、AtomPub (XML) 形式と JSON 形式の両方をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="95df2-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="95df2-110">OData では、データに関するメタデータを公開する方法も定義されています。</span><span class="sxs-lookup"><span data-stu-id="95df2-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="95df2-111">クライアントはメタデータを使用して、データセットの型情報と関係を検出できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="95df2-112">ASP.NET Web API を使用すると、データセットの OData エンドポイントを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="95df2-113">エンドポイントがサポートする OData 操作を正確に制御できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="95df2-114">OData 以外のエンドポイントと共に、複数の OData エンドポイントをホストできます。</span><span class="sxs-lookup"><span data-stu-id="95df2-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="95df2-115">データモデル、バックエンドビジネスロジック、およびデータ層を完全に制御できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="95df2-116">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="95df2-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="95df2-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="95df2-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="95df2-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="95df2-118">Web API 2</span></span>
> - <span data-ttu-id="95df2-119">OData バージョン3</span><span class="sxs-lookup"><span data-stu-id="95df2-119">OData Version 3</span></span>
> - <span data-ttu-id="95df2-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="95df2-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="95df2-121">Fiddler Web デバッグプロキシ (省略可能)</span><span class="sxs-lookup"><span data-stu-id="95df2-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="95df2-122">Web API の OData サポートが[ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)で追加されました。</span><span class="sxs-lookup"><span data-stu-id="95df2-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="95df2-123">ただし、このチュートリアルでは Visual Studio 2013 に追加されたスキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="95df2-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="95df2-124">このチュートリアルでは、クライアントがクエリを実行できる単純な OData エンドポイントを作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="95df2-125">また、エンドポイントのC#クライアントも作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="95df2-126">このチュートリアルを完了すると、次の一連のチュートリアルでは、エンティティの関係、アクション、$expand/$select を含む機能を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="95df2-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="95df2-127">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="95df2-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="95df2-128">エンティティモデルを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="95df2-129">OData コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="95df2-130">EDM とルートを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="95df2-131">データベースをシード処理する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="95df2-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="95df2-132">OData エンドポイントの探索</span><span class="sxs-lookup"><span data-stu-id="95df2-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="95df2-133">OData シリアル化形式</span><span class="sxs-lookup"><span data-stu-id="95df2-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="95df2-134">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="95df2-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="95df2-135">このチュートリアルでは、基本的な CRUD 操作をサポートする OData エンドポイントを作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="95df2-136">エンドポイントは、1つのリソース (製品の一覧) を公開します。</span><span class="sxs-lookup"><span data-stu-id="95df2-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="95df2-137">後のチュートリアルでは、さらに多くの機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="95df2-138">Visual Studio を起動し、スタートページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="95df2-139">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="95df2-140">**[テンプレート]** ペインで、 **[インストールされ]** たテンプレートC# を選択し、ビジュアルノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="95df2-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="95df2-141">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="95df2-142">**ASP.NET Web アプリケーション**テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="95df2-143">**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="95df2-144">[&quot;のフォルダーとコア参照の追加]&quot;で、 **[WEB API]** をオンにします。</span><span class="sxs-lookup"><span data-stu-id="95df2-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="95df2-145">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="95df2-146">エンティティモデルを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-146">Add an Entity Model</span></span>

<span data-ttu-id="95df2-147">*モデル*は、アプリケーションのデータを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="95df2-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="95df2-148">このチュートリアルでは、製品を表すモデルが必要です。</span><span class="sxs-lookup"><span data-stu-id="95df2-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="95df2-149">このモデルは、OData エンティティ型に対応しています。</span><span class="sxs-lookup"><span data-stu-id="95df2-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="95df2-150">ソリューションエクスプローラーで、[モデル] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="95df2-151">コンテキストメニューから **[追加]** を選択し、 **[クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="95df2-152">[新しい項目の**追加**] ダイアログボックスで、クラスに Product&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="95df2-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="95df2-153">慣例により、モデルクラスは [モデル] フォルダーに配置されます。</span><span class="sxs-lookup"><span data-stu-id="95df2-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="95df2-154">独自のプロジェクトでこの規則に従う必要はありませんが、このチュートリアルで使用します。</span><span class="sxs-lookup"><span data-stu-id="95df2-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="95df2-155">Product.cs ファイルで、次のクラス定義を追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="95df2-156">ID プロパティはエンティティキーになります。</span><span class="sxs-lookup"><span data-stu-id="95df2-156">The ID property will be the entity key.</span></span> <span data-ttu-id="95df2-157">クライアントは、ID で製品を照会できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-157">Clients can query products by ID.</span></span> <span data-ttu-id="95df2-158">このフィールドは、バックエンドデータベースの主キーでもあります。</span><span class="sxs-lookup"><span data-stu-id="95df2-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="95df2-159">ここでプロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="95df2-159">Build the project now.</span></span> <span data-ttu-id="95df2-160">次の手順では、リフレクションを使用して製品の種類を検索する Visual Studio のスキャフォールディングをいくつか使用します。</span><span class="sxs-lookup"><span data-stu-id="95df2-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="95df2-161">OData コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-161">Add an OData Controller</span></span>

<span data-ttu-id="95df2-162">*コントローラー*は、HTTP 要求を処理するクラスです。</span><span class="sxs-lookup"><span data-stu-id="95df2-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="95df2-163">OData サービスでは、エンティティセットごとに個別のコントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="95df2-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="95df2-164">このチュートリアルでは、1つのコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="95df2-165">ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="95df2-166">**[追加]** を選択し、 **[コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="95df2-167">**[スキャフォールディングの追加]** ダイアログボックスで、Entity Framework&quot;を使用して &quot;Web API 2 OData コントローラーとアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="95df2-168">**[コントローラーの追加]** ダイアログで、コントローラーに "製品コントローラー" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="95df2-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="95df2-169">非同期コントローラーアクションを使用する &quot;&quot; チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="95df2-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="95df2-170">**[モデル]** ドロップダウンリストで、Product クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="95df2-171">**[新しいデータコンテキスト...]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-171">Click the **New data context...** button.</span></span> <span data-ttu-id="95df2-172">データコンテキストの種類には既定の名前をそのまま使用し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="95df2-173">[コントローラーの追加] ダイアログボックスの [追加] をクリックして、コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="95df2-174">注: 種類...&quot;の取得中にエラーが発生しました &quot;というエラーメッセージが表示された場合は、Product クラスを追加した後に Visual Studio プロジェクトをビルドしたことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="95df2-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="95df2-175">スキャフォールディングは、リフレクションを使用してクラスを検索します。</span><span class="sxs-lookup"><span data-stu-id="95df2-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="95df2-176">スキャフォールディングは、次の2つのコードファイルをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="95df2-177">Products.cs は、OData エンドポイントを実装する Web API コントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="95df2-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="95df2-178">ProductServiceContext.cs を使用 Entity Framework して、基になるデータベースに対してクエリを実行するメソッドをに提供します。</span><span class="sxs-lookup"><span data-stu-id="95df2-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="95df2-179">EDM とルートを追加する</span><span class="sxs-lookup"><span data-stu-id="95df2-179">Add the EDM and Route</span></span>

<span data-ttu-id="95df2-180">ソリューションエクスプローラーで、アプリ\_スタートフォルダーを展開し、WebApiConfig.cs という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="95df2-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="95df2-181">このクラスは、Web API の構成コードを保持します。</span><span class="sxs-lookup"><span data-stu-id="95df2-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="95df2-182">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="95df2-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="95df2-183">このコードでは、次の2つの処理を行います。</span><span class="sxs-lookup"><span data-stu-id="95df2-183">This code does two things:</span></span>

- <span data-ttu-id="95df2-184">OData エンドポイントの Entity Data Model (EDM) を作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="95df2-185">エンドポイントのルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="95df2-186">EDM は、データの抽象モデルです。</span><span class="sxs-lookup"><span data-stu-id="95df2-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="95df2-187">EDM は、メタデータドキュメントを作成し、サービスの Uri を定義するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="95df2-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="95df2-188">**ODataConventionModelBuilder**は、既定の名前付け規則 edm のセットを使用して edm を作成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="95df2-189">この方法では、最小限のコードが必要です。</span><span class="sxs-lookup"><span data-stu-id="95df2-189">This approach requires the least code.</span></span> <span data-ttu-id="95df2-190">EDM をより細かく制御する場合は、プロパティ、キー、およびナビゲーションプロパティを明示的に追加することで、**使用**クラスを使用して edm を作成できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="95df2-191">**EntitySet**メソッドは、エンティティセットを EDM に追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="95df2-192">"Products" という文字列は、エンティティセットの名前を定義します。</span><span class="sxs-lookup"><span data-stu-id="95df2-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="95df2-193">コントローラーの名前は、エンティティセットの名前と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="95df2-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="95df2-194">このチュートリアルでは、エンティティセットの名前は "Products" で、コントローラーの名前は `ProductsController`です。</span><span class="sxs-lookup"><span data-stu-id="95df2-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="95df2-195">エンティティセットに "ProductSet" という名前を付けた場合は、コントローラーに `ProductSetController`という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="95df2-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="95df2-196">エンドポイントは複数のエンティティセットを持つことができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95df2-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="95df2-197">各エンティティセットに対して**EntitySet&lt;t&gt;** を呼び出して、対応するコントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="95df2-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="95df2-198">**MapODataRoute**メソッドは、OData エンドポイントのルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="95df2-199">最初のパラメーターは、ルートのフレンドリ名です。</span><span class="sxs-lookup"><span data-stu-id="95df2-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="95df2-200">サービスのクライアントには、この名前が表示されません。</span><span class="sxs-lookup"><span data-stu-id="95df2-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="95df2-201">2番目のパラメーターは、エンドポイントの URI プレフィックスです。</span><span class="sxs-lookup"><span data-stu-id="95df2-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="95df2-202">このコードの場合、Products エンティティセットの URI は http://<em>hostname</em>/odata/Products. になります。</span><span class="sxs-lookup"><span data-stu-id="95df2-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="95df2-203">アプリケーションには複数の OData エンドポイントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="95df2-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="95df2-204">各エンドポイントに対して<strong>MapODataRoute</strong>を呼び出し、一意のルート名と一意の URI プレフィックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="95df2-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="95df2-205">データベースをシード処理する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="95df2-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="95df2-206">この手順では、Entity Framework を使用して、いくつかのテストデータをデータベースにシード処理します。</span><span class="sxs-lookup"><span data-stu-id="95df2-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="95df2-207">この手順は省略可能ですが、OData エンドポイントをすぐにテストできます。</span><span class="sxs-lookup"><span data-stu-id="95df2-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="95df2-208">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="95df2-209">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="95df2-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="95df2-210">これにより、移行という名前のフォルダーと Configuration.cs という名前のコードファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="95df2-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="95df2-211">このファイルを開き、`Configuration.Seed` メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="95df2-212">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="95df2-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="95df2-213">これらのコマンドは、データベースを作成し、そのコードを実行するコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="95df2-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="95df2-214">OData エンドポイントの探索</span><span class="sxs-lookup"><span data-stu-id="95df2-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="95df2-215">このセクションでは、 [Fiddler Web デバッグプロキシ](http://www.fiddler2.com)を使用して、エンドポイントに要求を送信し、応答メッセージを確認します。</span><span class="sxs-lookup"><span data-stu-id="95df2-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="95df2-216">これは、OData エンドポイントの機能を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="95df2-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="95df2-217">Visual Studio で、F5 キーを押してデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="95df2-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="95df2-218">既定では、Visual Studio はブラウザーを開いて `http://localhost:*port*`します。ここで、 *port*はプロジェクト設定で構成されているポート番号です。</span><span class="sxs-lookup"><span data-stu-id="95df2-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="95df2-219">プロジェクト設定でポート番号を変更できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="95df2-220">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="95df2-221">プロパティ ウィンドウで、 **Web** を選択します。</span><span class="sxs-lookup"><span data-stu-id="95df2-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="95df2-222">**[プロジェクト Url]** にポート番号を入力します。</span><span class="sxs-lookup"><span data-stu-id="95df2-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="95df2-223">サービスドキュメント</span><span class="sxs-lookup"><span data-stu-id="95df2-223">Service Document</span></span>

<span data-ttu-id="95df2-224">*サービスドキュメント*には、OData エンドポイントのエンティティセットの一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="95df2-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="95df2-225">サービスドキュメントを取得するには、サービスのルート URI に GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="95df2-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="95df2-226">Fiddler を使用して、 **[Composer]** タブに次の URI を入力します `http://localhost:port/odata/`。ここで、 *port*はポート番号です。</span><span class="sxs-lookup"><span data-stu-id="95df2-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="95df2-227">**[実行]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95df2-227">Click the **Execute** button.</span></span> <span data-ttu-id="95df2-228">Fiddler は、アプリケーションに HTTP GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="95df2-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="95df2-229">[Web セッション] の一覧に応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="95df2-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="95df2-230">すべてが動作している場合、状態コードは200になります。</span><span class="sxs-lookup"><span data-stu-id="95df2-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="95df2-231">[Web セッション] の一覧で応答をダブルクリックすると、[インスペクター] タブに応答メッセージの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="95df2-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="95df2-232">未加工の HTTP 応答メッセージは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="95df2-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="95df2-233">既定では、Web API はサービスドキュメントを AtomPub 形式で返します。</span><span class="sxs-lookup"><span data-stu-id="95df2-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="95df2-234">JSON を要求するには、HTTP 要求に次のヘッダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="95df2-235">HTTP 応答に JSON ペイロードが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="95df2-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="95df2-236">サービスメタデータドキュメント</span><span class="sxs-lookup"><span data-stu-id="95df2-236">Service Metadata Document</span></span>

<span data-ttu-id="95df2-237">*サービスメタデータドキュメント*では、概念スキーマ定義言語 (CSDL) と呼ばれる XML 言語を使用した、サービスのデータモデルについて説明します。</span><span class="sxs-lookup"><span data-stu-id="95df2-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="95df2-238">メタデータドキュメントには、サービス内のデータの構造が表示され、クライアントコードを生成するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="95df2-239">メタデータドキュメントを取得するには、GET 要求を `http://localhost:port/odata/$metadata`に送信します。</span><span class="sxs-lookup"><span data-stu-id="95df2-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="95df2-240">このチュートリアルでは、エンドポイントのメタデータを次に示します。</span><span class="sxs-lookup"><span data-stu-id="95df2-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="95df2-241">エンティティ セット</span><span class="sxs-lookup"><span data-stu-id="95df2-241">Entity Set</span></span>

<span data-ttu-id="95df2-242">Products エンティティセットを取得するには、GET 要求を `http://localhost:port/odata/Products`に送信します。</span><span class="sxs-lookup"><span data-stu-id="95df2-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="95df2-243">エンティティ</span><span class="sxs-lookup"><span data-stu-id="95df2-243">Entity</span></span>

<span data-ttu-id="95df2-244">個々の製品を取得するには、GET 要求を `http://localhost:port/odata/Products(1)`に送信します。 "1" は製品 ID です。</span><span class="sxs-lookup"><span data-stu-id="95df2-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="95df2-245">OData シリアル化形式</span><span class="sxs-lookup"><span data-stu-id="95df2-245">OData Serialization Formats</span></span>

<span data-ttu-id="95df2-246">OData は、いくつかのシリアル化形式をサポートします。</span><span class="sxs-lookup"><span data-stu-id="95df2-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="95df2-247">Atom Pub (XML)</span><span class="sxs-lookup"><span data-stu-id="95df2-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="95df2-248">JSON "light" (OData v3 で導入)</span><span class="sxs-lookup"><span data-stu-id="95df2-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="95df2-249">JSON "verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="95df2-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="95df2-250">既定では、Web API は AtomPubJSON "light" 形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="95df2-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="95df2-251">AtomPub 形式を取得するには、Accept ヘッダーを "application/atom + xml" に設定します。</span><span class="sxs-lookup"><span data-stu-id="95df2-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="95df2-252">応答本文の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="95df2-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="95df2-253">Atom 形式の1つの明確な欠点を確認できます。これは、JSON ライトよりもはるかに詳細です。</span><span class="sxs-lookup"><span data-stu-id="95df2-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="95df2-254">ただし、AtomPub を認識するクライアントがある場合、クライアントは JSON よりも形式を優先する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="95df2-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="95df2-255">同じエンティティの JSON light バージョンを次に示します。</span><span class="sxs-lookup"><span data-stu-id="95df2-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="95df2-256">JSON light 形式は、OData プロトコルのバージョン3で導入されました。</span><span class="sxs-lookup"><span data-stu-id="95df2-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="95df2-257">旧バージョンとの互換性を維持するために、クライアントは古い "verbose" JSON 形式を要求できます。</span><span class="sxs-lookup"><span data-stu-id="95df2-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="95df2-258">詳細な JSON を要求するには、Accept ヘッダーを `application/json;odata=verbose`に設定します。</span><span class="sxs-lookup"><span data-stu-id="95df2-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="95df2-259">詳細バージョンは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="95df2-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="95df2-260">この形式では、応答本文により多くのメタデータが伝達されます。これにより、セッション全体でかなりのオーバーヘッドが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="95df2-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="95df2-261">また、"d" という名前のプロパティにオブジェクトをラップすることによって、レベルの間接参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="95df2-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="95df2-262">次のステップ</span><span class="sxs-lookup"><span data-stu-id="95df2-262">Next Steps</span></span>

- [<span data-ttu-id="95df2-263">エンティティリレーションの追加</span><span class="sxs-lookup"><span data-stu-id="95df2-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="95df2-264">OData アクションの追加</span><span class="sxs-lookup"><span data-stu-id="95df2-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="95df2-265">.NET クライアントから OData サービスを呼び出す</span><span class="sxs-lookup"><span data-stu-id="95df2-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
