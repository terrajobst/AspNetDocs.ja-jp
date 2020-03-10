---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2.2 を使用して OData v4 でシングルトンを作成する |Microsoft Docs
author: rick-anderson
description: このトピックでは、Web API 2.2 で OData エンドポイントにシングルトンを定義する方法について説明します。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504502"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="9df0d-103">Web API 2.2 を使用して OData v4 でシングルトンを作成する</span><span class="sxs-lookup"><span data-stu-id="9df0d-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="9df0d-104">Zoe Luo 別</span><span class="sxs-lookup"><span data-stu-id="9df0d-104">by Zoe Luo</span></span>

> <span data-ttu-id="9df0d-105">従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。</span><span class="sxs-lookup"><span data-stu-id="9df0d-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="9df0d-106">ただし、OData v4 には、シングルトンとコンテインメントという2つの追加オプションが用意されています。どちらも WebAPI 2.2 でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9df0d-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="9df0d-107">この記事では、Web API 2.2 で OData エンドポイントにシングルトンを定義する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="9df0d-108">シングルトンとは何か、およびそれを使用する利点については、「[シングルトンを使用した特殊なエンティティの定義](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9df0d-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="9df0d-109">Web API で OData V4 エンドポイントを作成するには、「 [ASP.NET Web API 2.2 を使用して odata V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9df0d-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="9df0d-110">次のデータモデルを使用して、Web API プロジェクトにシングルトンを作成します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![データ モデル](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="9df0d-112">`Umbrella` という名前のシングルトンが `Company`型に基づいて定義され、`Employees` という名前のエンティティセットが `Employee`型に基づいて定義されます。</span><span class="sxs-lookup"><span data-stu-id="9df0d-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="9df0d-113">このチュートリアルで使用するソリューションは、 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="9df0d-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="9df0d-114">データ モデルを定義する</span><span class="sxs-lookup"><span data-stu-id="9df0d-114">Define the data model</span></span>

1. <span data-ttu-id="9df0d-115">CLR 型を定義します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="9df0d-116">CLR 型に基づいて EDM モデルを生成します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="9df0d-117">ここでは、`builder.Singleton<Company>("Umbrella")` はモデルビルダーに対して、EDM モデルで `Umbrella` という名前のシングルトンを作成するように指示します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="9df0d-118">生成されたメタデータは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="9df0d-119">メタデータから、`Employees` エンティティセットのナビゲーションプロパティ `Company` がシングルトン `Umbrella`にバインドされていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="9df0d-120">バインドは `ODataConventionModelBuilder`によって自動的に行われます。これは、`Umbrella` には `Company` 型しかないためです。</span><span class="sxs-lookup"><span data-stu-id="9df0d-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="9df0d-121">モデルにあいまいさがある場合は、`HasSingletonBinding` を使用して、ナビゲーションプロパティをシングルトンに明示的にバインドすることができます。`HasSingletonBinding` は、CLR 型定義で `Singleton` 属性を使用するのと同じ効果があります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="9df0d-122">シングルトンコントローラーを定義する</span><span class="sxs-lookup"><span data-stu-id="9df0d-122">Define the singleton controller</span></span>

<span data-ttu-id="9df0d-123">EntitySet コントローラーと同様に、シングルトンコントローラーは `ODataController`から継承し、シングルトンコントローラー名を `[singletonName]Controller`する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="9df0d-124">さまざまな種類の要求を処理するには、コントローラーでアクションを事前定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="9df0d-125">WebApi 2.2 では、既定で**属性ルーティング**が有効になっています。</span><span class="sxs-lookup"><span data-stu-id="9df0d-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="9df0d-126">たとえば、属性ルーティングを使用して `Company` からの `Revenue` のクエリを処理するアクションを定義するには、次のように指定します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="9df0d-127">各アクションの属性を定義しない場合は、 [OData ルーティング規則](../odata-routing-conventions.md)に従うアクションを定義するだけです。</span><span class="sxs-lookup"><span data-stu-id="9df0d-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="9df0d-128">シングルトンに対してクエリを実行するためにキーは必要ないため、シングルトンコントローラーで定義されたアクションは、entityset コントローラーで定義されているアクションとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="9df0d-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="9df0d-129">参照用に、シングルトンコントローラーのすべてのアクション定義のメソッドシグネチャを次に示します。</span><span class="sxs-lookup"><span data-stu-id="9df0d-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="9df0d-130">基本的に、これはサービス側で行う必要があることです。</span><span class="sxs-lookup"><span data-stu-id="9df0d-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="9df0d-131">[サンプルプロジェクト](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)には、ソリューションのすべてのコードと、シングルトンの使用方法を示す OData クライアントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9df0d-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="9df0d-132">クライアントは、「 [OData V4 クライアントアプリの作成](create-an-odata-v4-client-app.md)」の手順に従って構築されます。</span><span class="sxs-lookup"><span data-stu-id="9df0d-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="9df0d-133">。</span><span class="sxs-lookup"><span data-stu-id="9df0d-133">.</span></span> 

<span data-ttu-id="9df0d-134">*この記事の元の内容については、Leo Hu に感謝します。*</span><span class="sxs-lookup"><span data-stu-id="9df0d-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
