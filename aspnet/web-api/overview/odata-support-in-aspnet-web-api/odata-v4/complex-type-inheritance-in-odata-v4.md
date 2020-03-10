---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API | を使用した OData v4 での複合型の継承Microsoft Docs
author: microsoft
description: OData v4 仕様によれば、複合型は別の複合型から継承できます。 複合型は、キーを持たない構造化された型です。Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448132"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="7fd32-104">ASP.NET Web API を使用した OData v4 での複合型の継承</span><span class="sxs-lookup"><span data-stu-id="7fd32-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="7fd32-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7fd32-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7fd32-106">OData v4[仕様](http://www.odata.org/documentation/odata-version-4-0/)によれば、複合型は別の複合型から継承できます。</span><span class="sxs-lookup"><span data-stu-id="7fd32-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="7fd32-107">*複合*型は、キーを持たない構造化された型です。Web API OData 5.3 では、複合型の継承がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7fd32-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="7fd32-108">このトピックでは、複雑な継承型を使用して entity data model (EDM) を構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="7fd32-109">完全なソースコードについては、「 [OData 複合型の継承のサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7fd32-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7fd32-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7fd32-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7fd32-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="7fd32-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="7fd32-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="7fd32-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="7fd32-113">モデル階層</span><span class="sxs-lookup"><span data-stu-id="7fd32-113">Model Hierarchy</span></span>

<span data-ttu-id="7fd32-114">複合型の継承について説明するために、次のクラス階層を使用します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="7fd32-115">`Shape` は抽象複合型です。</span><span class="sxs-lookup"><span data-stu-id="7fd32-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="7fd32-116">`Rectangle`、`Triangle`、および `Circle` は `Shape`から派生した複合型であり、`RoundRectangle` から派生します。`Rectangle`</span><span class="sxs-lookup"><span data-stu-id="7fd32-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="7fd32-117">`Window` はエンティティ型で、`Shape` インスタンスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7fd32-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="7fd32-118">これらの型を定義する CLR クラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="7fd32-119">EDM モデルの構築</span><span class="sxs-lookup"><span data-stu-id="7fd32-119">Build the EDM Model</span></span>

<span data-ttu-id="7fd32-120">EDM を作成するには、CLR 型から継承関係を推論する**ODataConventionModelBuilder**を使用できます。</span><span class="sxs-lookup"><span data-stu-id="7fd32-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="7fd32-121">**使用**を使用して、EDM を明示的に構築することもできます。</span><span class="sxs-lookup"><span data-stu-id="7fd32-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="7fd32-122">この処理にはより多くのコードが必要ですが、EDM をより細かく制御できます。</span><span class="sxs-lookup"><span data-stu-id="7fd32-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="7fd32-123">次の2つの例では、同じ EDM スキーマを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="7fd32-124">メタデータドキュメント</span><span class="sxs-lookup"><span data-stu-id="7fd32-124">Metadata Document</span></span>

<span data-ttu-id="7fd32-125">ここでは、複合型の継承を示す OData メタデータドキュメントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="7fd32-126">メタデータドキュメントから、次のことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7fd32-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="7fd32-127">`Shape` 複合型は abstract です。</span><span class="sxs-lookup"><span data-stu-id="7fd32-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="7fd32-128">`Rectangle`、`Triangle`、および `Circle` 複合型には `Shape`の基本型があります。</span><span class="sxs-lookup"><span data-stu-id="7fd32-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="7fd32-129">`RoundRectangle` 型には `Rectangle`基本型があります。</span><span class="sxs-lookup"><span data-stu-id="7fd32-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="7fd32-130">キャスト (複合型を)</span><span class="sxs-lookup"><span data-stu-id="7fd32-130">Casting Complex Types</span></span>

<span data-ttu-id="7fd32-131">複合型へのキャストがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="7fd32-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="7fd32-132">たとえば、次のクエリでは、`Shape` を `Rectangle`にキャストします。</span><span class="sxs-lookup"><span data-stu-id="7fd32-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="7fd32-133">応答ペイロードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7fd32-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
