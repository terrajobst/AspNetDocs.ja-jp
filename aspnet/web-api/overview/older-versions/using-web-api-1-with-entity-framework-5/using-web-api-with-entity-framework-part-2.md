---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 'パート 2: ドメインモデルの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504274"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="7dfcd-102">パート 2: ドメインモデルの作成</span><span class="sxs-lookup"><span data-stu-id="7dfcd-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="7dfcd-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7dfcd-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7dfcd-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="7dfcd-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="7dfcd-105">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="7dfcd-105">Add Models</span></span>

<span data-ttu-id="7dfcd-106">Entity Framework アプローチには、次の3つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="7dfcd-107">データベース優先: データベースから開始し、Entity Framework によってコードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="7dfcd-108">モデル優先: ビジュアルモデルから開始すると、Entity Framework によってデータベースとコードの両方が生成されます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="7dfcd-109">Code first: code から開始し、Entity Framework によってデータベースが生成されます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="7dfcd-110">コード優先の方法を使用しているので、まず、ドメインオブジェクトを POCOs (plain old CLR object) として定義します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="7dfcd-111">コード優先のアプローチでは、データベースレイヤーをサポートするために、ドメインオブジェクトにはトランザクションや永続化などの追加のコードは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="7dfcd-112">(具体的には、 [Entityobject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)クラスから継承する必要はありません)。データ注釈を使用して、Entity Framework がデータベーススキーマを作成する方法を制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="7dfcd-113">POCOs には[データベースの状態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)を説明する追加のプロパティがないため、JSON または XML に簡単にシリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="7dfcd-114">ただし、このチュートリアルで後ほど説明するように、これは常に Entity Framework モデルをクライアントに直接公開する必要があるという意味ではありません。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="7dfcd-115">次の POCOs が作成されます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="7dfcd-116">Product</span><span class="sxs-lookup"><span data-stu-id="7dfcd-116">Product</span></span>
- <span data-ttu-id="7dfcd-117">Order</span><span class="sxs-lookup"><span data-stu-id="7dfcd-117">Order</span></span>
- <span data-ttu-id="7dfcd-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="7dfcd-118">OrderDetail</span></span>

<span data-ttu-id="7dfcd-119">各クラスを作成するには、ソリューションエクスプローラーで [モデル] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="7dfcd-120">コンテキストメニューから **追加** を選択し、クラス を選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="7dfcd-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="7dfcd-121">次の実装を使用して `Product` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="7dfcd-122">慣例により、Entity Framework は `Id` プロパティを主キーとして使用し、データベーステーブル内の id 列にマップします。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="7dfcd-123">新しい `Product` インスタンスを作成した場合、データベースで値が生成されるため、`Id`の値は設定されません。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="7dfcd-124">**ScaffoldColumn**属性は、エディターフォームを生成するときに、`Id` プロパティをスキップするように ASP.NET MVC に指示します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="7dfcd-125">**必須**の属性は、モデルの検証に使用されます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="7dfcd-126">`Name` プロパティは、空でない文字列である必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="7dfcd-127">`Order` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="7dfcd-128">`OrderDetail` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="7dfcd-129">外部キーの関係</span><span class="sxs-lookup"><span data-stu-id="7dfcd-129">Foreign Key Relations</span></span>

<span data-ttu-id="7dfcd-130">注文には多くの注文の詳細が含まれ、各注文の詳細は1つの製品を表します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="7dfcd-131">これらの関係を表すために、`OrderDetail` クラスは `OrderId` と `ProductId`という名前のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="7dfcd-132">Entity Framework は、これらのプロパティが外部キーを表していることを推定し、データベースに外部キー制約を追加します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="7dfcd-133">`Order` クラスと `OrderDetail` クラスには、関連オブジェクトへの参照を含む "ナビゲーション" プロパティも含まれています。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="7dfcd-134">順序を指定すると、ナビゲーションプロパティに従って、注文内の製品に移動できます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="7dfcd-135">ここでプロジェクトをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-135">Compile the project now.</span></span> <span data-ttu-id="7dfcd-136">Entity Framework は、リフレクションを使用してモデルのプロパティを検出します。そのため、データベーススキーマを作成するには、コンパイル済みのアセンブリが必要です。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="7dfcd-137">メディアの種類のフォーマッタを構成する</span><span class="sxs-lookup"><span data-stu-id="7dfcd-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="7dfcd-138">[メディアの種類のフォーマッタ](../../formats-and-model-binding/media-formatters.md)は、Web API が HTTP 応答の本文を書き込むときにデータをシリアル化するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="7dfcd-139">組み込みのフォーマッタは、JSON と XML の出力をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="7dfcd-140">既定では、これらのフォーマッタはいずれも、値によってすべてのオブジェクトをシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="7dfcd-141">値によるシリアル化では、オブジェクトグラフに循環参照が含まれている場合に問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="7dfcd-142">これは、それぞれが別の参照を保持しているため、`Order` クラスと `OrderDetail` クラスの場合とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="7dfcd-143">フォーマッタは参照に従い、各オブジェクトを値で書き込んで、円で囲みます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="7dfcd-144">そのため、既定の動作を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="7dfcd-145">ソリューションエクスプローラーで、アプリ\_スタートフォルダーを展開し、WebApiConfig.cs という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="7dfcd-146">以下のコードを `WebApiConfig` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="7dfcd-147">このコードは、オブジェクト参照を保持するように JSON フォーマッタを設定し、パイプラインから XML フォーマッタを完全に削除します。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="7dfcd-148">(XML フォーマッタは、オブジェクト参照を保持するように構成できますが、作業は少しだけで、このアプリケーションには JSON のみが必要です。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="7dfcd-149">詳細については、「[循環オブジェクト参照の処理](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7dfcd-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7dfcd-150">[前へ](using-web-api-with-entity-framework-part-1.md)
> [次へ](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="7dfcd-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
