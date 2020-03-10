---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2 | を使用して OData v4 エンドポイントを作成するMicrosoft Docs
author: MikeWasson
description: Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。 OData は、CRUD 操作によってデータセットをクエリおよび操作するための統一された方法を提供します...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484498"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="e7f04-104">ASP.NET Web API を使用して OData v4 エンドポイントを作成する</span><span class="sxs-lookup"><span data-stu-id="e7f04-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="e7f04-105">Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="e7f04-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="e7f04-106">OData は、CRUD 操作 (作成、読み取り、更新、および削除) によってデータセットをクエリおよび操作するための統一された方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="e7f04-107">ASP.NET Web API は、プロトコルの v3 と v4 の両方をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="e7f04-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="e7f04-108">V4 エンドポイントを、v3 エンドポイントとサイドバイサイドで実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="e7f04-109">このチュートリアルでは、CRUD 操作をサポートする OData v4 エンドポイントを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e7f04-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="e7f04-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="e7f04-111">Web API 5.2</span><span class="sxs-lookup"><span data-stu-id="e7f04-111">Web API 5.2</span></span>
> - <span data-ttu-id="e7f04-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="e7f04-112">OData v4</span></span>
> - <span data-ttu-id="e7f04-113">Visual Studio 2017 (Visual Studio 2017 を[こちら](https://visualstudio.microsoft.com/downloads/)からダウンロード)</span><span class="sxs-lookup"><span data-stu-id="e7f04-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="e7f04-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e7f04-114">Entity Framework 6</span></span>
> - <span data-ttu-id="e7f04-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e7f04-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="e7f04-116">チュートリアルのバージョン</span><span class="sxs-lookup"><span data-stu-id="e7f04-116">Tutorial versions</span></span>
>
> <span data-ttu-id="e7f04-117">OData バージョン3については、「 [odata V3 エンドポイントの作成](../odata-v3/creating-an-odata-endpoint.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e7f04-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e7f04-118">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="e7f04-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="e7f04-119">Visual Studio で、 **[ファイル]** メニューの [**新しい**&gt;**プロジェクト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7f04-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="e7f04-120">[**インストールされている**&gt;  **C# Visual** &gt; **web**] を展開し、 **[ASP.NET Web Application (.NET Framework)]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="e7f04-121">プロジェクトに ProductService&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="e7f04-122">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="e7f04-123">**[空]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-123">Select the **Empty** template.</span></span> <span data-ttu-id="e7f04-124">**[フォルダーとコア参照の追加先]** で、 **[Web API]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="e7f04-125">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="e7f04-126">OData パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="e7f04-126">Install the OData packages</span></span>

<span data-ttu-id="e7f04-127">**[ツール]** メニューで、 **[NuGet パッケージ マネージャー]** &gt; **[パッケージ マネージャー コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e7f04-128">[パッケージマネージャーコンソール] ウィンドウで、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="e7f04-129">このコマンドは、最新の OData NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e7f04-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="e7f04-130">モデル クラスの追加</span><span class="sxs-lookup"><span data-stu-id="e7f04-130">Add a model class</span></span>

<span data-ttu-id="e7f04-131">*モデル*は、アプリケーション内のデータエンティティを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="e7f04-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="e7f04-132">ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="e7f04-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="e7f04-133">コンテキストメニューから [&gt;**クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="e7f04-134">慣例により、モデルクラスは [モデル] フォルダーに配置されますが、独自のプロジェクトでこの規則に従う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e7f04-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="e7f04-135">クラスに `Product` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-135">Name the class `Product`.</span></span> <span data-ttu-id="e7f04-136">Product.cs ファイルで、定型コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="e7f04-137">`Id` プロパティは、エンティティキーです。</span><span class="sxs-lookup"><span data-stu-id="e7f04-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="e7f04-138">クライアントは、キーによってエンティティを照会できます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-138">Clients can query entities by key.</span></span> <span data-ttu-id="e7f04-139">たとえば、ID が5の製品を取得するために、URI は `/Products(5)`ます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="e7f04-140">`Id` プロパティは、バックエンドデータベースの主キーにもなります。</span><span class="sxs-lookup"><span data-stu-id="e7f04-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="e7f04-141">Entity Framework を有効にする</span><span class="sxs-lookup"><span data-stu-id="e7f04-141">Enable Entity Framework</span></span>

<span data-ttu-id="e7f04-142">このチュートリアルでは、Entity Framework (EF) Code First を使用してバックエンドデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="e7f04-143">Web API OData には EF は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="e7f04-143">Web API OData does not require EF.</span></span> <span data-ttu-id="e7f04-144">データベースエンティティをモデルに変換できる任意のデータアクセスレイヤーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="e7f04-145">最初に、EF 用の NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e7f04-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="e7f04-146">**[ツール]** メニューで、 **[NuGet パッケージ マネージャー]** &gt; **[パッケージ マネージャー コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e7f04-147">[パッケージマネージャーコンソール] ウィンドウで、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="e7f04-148">Web.config ファイルを開き、**構成**要素内の**configsections**要素の後に次のセクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="e7f04-149">この設定により、LocalDB データベースの接続文字列が追加されます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="e7f04-150">このデータベースは、アプリをローカルで実行するときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="e7f04-151">次に、`ProductsContext` という名前のクラスを [モデル] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="e7f04-152">コンストラクターでは、`"name=ProductsContext"` 接続文字列の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="e7f04-153">OData エンドポイントを構成する</span><span class="sxs-lookup"><span data-stu-id="e7f04-153">Configure the OData endpoint</span></span>

<span data-ttu-id="e7f04-154">File App\_Start/Webapiconfig.cs を開きます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="e7f04-155">次の**using ステートメントを追加し**ます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="e7f04-156">次に、 **Register**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="e7f04-157">このコードでは、次の2つの処理を行います。</span><span class="sxs-lookup"><span data-stu-id="e7f04-157">This code does two things:</span></span>

- <span data-ttu-id="e7f04-158">Entity Data Model (EDM) を作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="e7f04-159">ルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-159">Adds a route.</span></span>

<span data-ttu-id="e7f04-160">EDM は、データの抽象モデルです。</span><span class="sxs-lookup"><span data-stu-id="e7f04-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="e7f04-161">EDM は、サービスメタデータドキュメントの作成に使用されます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="e7f04-162">**ODataConventionModelBuilder**クラスは、既定の名前付け規則を使用して EDM を作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="e7f04-163">この方法では、最小限のコードが必要です。</span><span class="sxs-lookup"><span data-stu-id="e7f04-163">This approach requires the least code.</span></span> <span data-ttu-id="e7f04-164">EDM をより細かく制御する場合は、プロパティ、キー、およびナビゲーションプロパティを明示的に追加することで、**使用**クラスを使用して edm を作成できます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="e7f04-165">*ルート*は、HTTP 要求をエンドポイントにルーティングする方法を Web API に指示します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="e7f04-166">OData v4 ルートを作成するには、 **MapODataServiceRoute**拡張メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="e7f04-167">アプリケーションに複数の OData エンドポイントがある場合は、それぞれに対して個別のルートを作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="e7f04-168">各ルートに一意のルート名とプレフィックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="e7f04-169">OData コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="e7f04-169">Add the OData controller</span></span>

<span data-ttu-id="e7f04-170">*コントローラー*は、HTTP 要求を処理するクラスです。</span><span class="sxs-lookup"><span data-stu-id="e7f04-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="e7f04-171">OData サービスでは、エンティティセットごとに個別のコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="e7f04-172">このチュートリアルでは、`Product` エンティティ用に1つのコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="e7f04-173">ソリューションエクスプローラーで、Controllers フォルダーを右クリックし、[&gt;**クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="e7f04-174">クラスに `ProductsController` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="e7f04-175">OData v3 用のこのチュートリアルのバージョンでは、**コントローラーの追加**スキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="e7f04-176">現時点では、OData v4 のスキャフォールディングはありません。</span><span class="sxs-lookup"><span data-stu-id="e7f04-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="e7f04-177">ProductsController.cs の定型コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="e7f04-178">コントローラーは `ProductsContext` クラスを使用して、EF を使用してデータベースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e7f04-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="e7f04-179">コントローラーは、製品**コンテキスト**を破棄するために**dispose**メソッドをオーバーライドすることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e7f04-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="e7f04-180">これは、コントローラーの開始点です。</span><span class="sxs-lookup"><span data-stu-id="e7f04-180">This is the starting point for the controller.</span></span> <span data-ttu-id="e7f04-181">次に、すべての CRUD 操作に対してメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="e7f04-182">エンティティセットに対してクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="e7f04-182">Query the entity set</span></span>

<span data-ttu-id="e7f04-183">次のメソッドを `ProductsController`に追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="e7f04-184">`Get` メソッドのパラメーターなしのバージョンは、製品コレクション全体を返します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="e7f04-185">*キー*パラメーターを指定した `Get` メソッドでは、キー (この例では `Id` プロパティ) によって製品が検索されます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="e7f04-186">**[Enablequery]** 属性を使用すると、$filter、$sort、$page などのクエリオプションを使用して、クライアントがクエリを変更できます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="e7f04-187">詳細については、「 [OData クエリオプションのサポート](../supporting-odata-query-options.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e7f04-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="e7f04-188">エンティティをエンティティセットに追加する</span><span class="sxs-lookup"><span data-stu-id="e7f04-188">Add an entity to the entity set</span></span>

<span data-ttu-id="e7f04-189">クライアントがデータベースに新しい製品を追加できるようにするには、次のメソッドを `ProductsController`に追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="e7f04-190">エンティティを更新する</span><span class="sxs-lookup"><span data-stu-id="e7f04-190">Update an entity</span></span>

<span data-ttu-id="e7f04-191">OData は、エンティティ、修正プログラム、および PUT を更新するための2つの異なるセマンティクスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="e7f04-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="e7f04-192">PATCH は、部分的な更新を実行します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-192">PATCH performs a partial update.</span></span> <span data-ttu-id="e7f04-193">クライアントは、更新するプロパティだけを指定します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="e7f04-194">PUT は、エンティティ全体を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="e7f04-195">PUT の欠点は、クライアントがエンティティ内のすべてのプロパティの値を送信する必要があることです。変更されていない値も含まれます。</span><span class="sxs-lookup"><span data-stu-id="e7f04-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="e7f04-196">[OData 仕様](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)では、修正プログラムが推奨されています。</span><span class="sxs-lookup"><span data-stu-id="e7f04-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="e7f04-197">どのような場合でも、PATCH メソッドと PUT メソッドのコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e7f04-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="e7f04-198">パッチの場合、コントローラーは**デルタ&lt;t&gt;** 型を使用して変更を追跡します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="e7f04-199">エンティティを削除する</span><span class="sxs-lookup"><span data-stu-id="e7f04-199">Delete an entity</span></span>

<span data-ttu-id="e7f04-200">クライアントがデータベースから製品を削除できるようにするには、次のメソッドを `ProductsController`に追加します。</span><span class="sxs-lookup"><span data-stu-id="e7f04-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
