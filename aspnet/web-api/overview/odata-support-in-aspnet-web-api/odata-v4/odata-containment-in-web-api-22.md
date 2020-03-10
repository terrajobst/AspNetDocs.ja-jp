---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2.2 | を使用した OData v4 の含有Microsoft Docs
author: rick-anderson
description: 従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。 ただし、OData v4 には、シングルトンと Con という2つの追加オプションがあります。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 50050e40c4c42bf6d769d077c27864ee6417d4db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421402"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="e1dcf-104">Web API 2.2 を使用した OData v4 の含有</span><span class="sxs-lookup"><span data-stu-id="e1dcf-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="e1dcf-105">Jinfu Tan 別</span><span class="sxs-lookup"><span data-stu-id="e1dcf-105">by Jinfu Tan</span></span>

> <span data-ttu-id="e1dcf-106">従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="e1dcf-107">ただし、OData v4 には、シングルトンとコンテインメントという2つの追加オプションが用意されています。どちらも WebAPI 2.2 でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="e1dcf-108">このトピックでは、WebApi 2.2 の OData エンドポイントでコンテインメントを定義する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="e1dcf-109">コンテインメントの詳細については、「[コンテインメントは OData v4 に付属](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)しています」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="e1dcf-110">Web API で OData V4 エンドポイントを作成するには、「 [ASP.NET Web API 2.2 を使用して odata V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="e1dcf-111">まず、次のデータモデルを使用して、OData サービスにコンテインメントドメインモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![データ モデル](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="e1dcf-113">アカウントには多くの PaymentInstruments (PI) が含まれていますが、PI のエンティティセットは定義されていません。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="e1dcf-114">代わりに、Pi にはアカウントを使用してのみアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="e1dcf-115">このトピックで使用するソリューションは、 [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="e1dcf-116">データモデルの定義</span><span class="sxs-lookup"><span data-stu-id="e1dcf-116">Defining the data model</span></span>

1. <span data-ttu-id="e1dcf-117">CLR 型を定義します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="e1dcf-118">`Contained` 属性は、コンテインメントナビゲーションプロパティに使用されます。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="e1dcf-119">CLR 型に基づいて EDM モデルを生成します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="e1dcf-120">`Contained` 属性が対応するナビゲーションプロパティに追加された場合、`ODataConventionModelBuilder` は EDM モデルの作成を処理します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="e1dcf-121">プロパティがコレクション型の場合は、`GetCount(string NameContains)` 関数も作成されます。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="e1dcf-122">生成されたメタデータは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="e1dcf-123">`ContainsTarget` 属性は、ナビゲーションプロパティがコンテインメントであることを示します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="e1dcf-124">含まれているエンティティセットコントローラーを定義する</span><span class="sxs-lookup"><span data-stu-id="e1dcf-124">Define the containing entity set controller</span></span>

<span data-ttu-id="e1dcf-125">含まれているエンティティは独自のコントローラーを持っていません。アクションは、含んでいるエンティティセットコントローラーで定義されています。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="e1dcf-126">このサンプルでは、AccountsController がありますが、PaymentInstrumentsController はありません。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="e1dcf-127">OData パスが4つ以上のセグメントの場合、上記のコントローラーの `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` など、属性ルーティングのみが機能します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="e1dcf-128">それ以外の場合は、属性と従来のルーティングの両方が機能します。たとえば、`GetPayInPIs(int key)` は `GET ~/Accounts(1)/PayinPIs`と一致します。</span><span class="sxs-lookup"><span data-stu-id="e1dcf-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="e1dcf-129">*この記事の元の内容については、Leo Hu に感謝します。*</span><span class="sxs-lookup"><span data-stu-id="e1dcf-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
