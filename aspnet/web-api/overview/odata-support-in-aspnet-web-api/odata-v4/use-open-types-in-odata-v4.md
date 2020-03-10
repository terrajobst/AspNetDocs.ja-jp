---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API | を使用した OData v4 のオープン型Microsoft Docs
author: microsoft
description: OData v4 では、オープン型は、型定義で宣言されているすべてのプロパティに加えて、動的プロパティを含む構造化された型です。 開く...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504580"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="bfe72-104">ASP.NET Web API を使用した OData v4 でのオープン型</span><span class="sxs-lookup"><span data-stu-id="bfe72-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="bfe72-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bfe72-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="bfe72-106">OData v4 では、*オープン型*は、型定義で宣言されているすべてのプロパティに加えて、動的プロパティを含む構造化された型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="bfe72-107">オープン型を使用すると、データモデルに柔軟性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="bfe72-108">このチュートリアルでは、ASP.NET Web API OData で open types を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="bfe72-109">このチュートリアルでは、ASP.NET Web API で OData エンドポイントを作成する方法を既に理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="bfe72-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="bfe72-110">それ以外の場合は、まず「 [Create a OData V4 Endpoint](create-an-odata-v4-endpoint.md) first」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfe72-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bfe72-111">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="bfe72-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bfe72-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="bfe72-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="bfe72-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="bfe72-113">OData v4</span></span>

<span data-ttu-id="bfe72-114">まず、OData のいくつかの用語を次に示します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-114">First, some OData terminology:</span></span>

- <span data-ttu-id="bfe72-115">エンティティ型: キーを持つ構造化型。</span><span class="sxs-lookup"><span data-stu-id="bfe72-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="bfe72-116">複合型: キーを持たない構造化された型。</span><span class="sxs-lookup"><span data-stu-id="bfe72-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="bfe72-117">Open type: 動的プロパティを持つ型。</span><span class="sxs-lookup"><span data-stu-id="bfe72-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="bfe72-118">エンティティ型と複合型の両方を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="bfe72-119">動的プロパティの値には、プリミティブ型、複合型、または列挙型を指定できます。または、これらの型のいずれかのコレクション。</span><span class="sxs-lookup"><span data-stu-id="bfe72-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="bfe72-120">オープン型の詳細については、 [OData v4 仕様](http://www.odata.org/documentation/odata-version-4-0/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfe72-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="bfe72-121">Web OData ライブラリをインストールする</span><span class="sxs-lookup"><span data-stu-id="bfe72-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="bfe72-122">NuGet パッケージマネージャーを使用して、最新の Web API OData ライブラリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="bfe72-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="bfe72-123">[パッケージマネージャーコンソール] ウィンドウから次のようにします。</span><span class="sxs-lookup"><span data-stu-id="bfe72-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="bfe72-124">CLR 型を定義する</span><span class="sxs-lookup"><span data-stu-id="bfe72-124">Define the CLR Types</span></span>

<span data-ttu-id="bfe72-125">まず、EDM モデルを CLR 型として定義します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="bfe72-126">Entity Data Model (EDM) が作成されると、</span><span class="sxs-lookup"><span data-stu-id="bfe72-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="bfe72-127">`Category` は列挙型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="bfe72-128">`Address` は複合型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-128">`Address` is a complex type.</span></span> <span data-ttu-id="bfe72-129">(キーがないため、エンティティ型ではありません)。</span><span class="sxs-lookup"><span data-stu-id="bfe72-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="bfe72-130">`Customer` はエンティティ型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-130">`Customer` is an entity type.</span></span> <span data-ttu-id="bfe72-131">(キーがあります)。</span><span class="sxs-lookup"><span data-stu-id="bfe72-131">(It has a key.)</span></span>
- <span data-ttu-id="bfe72-132">`Press` はオープン複合型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="bfe72-133">`Book` はオープンエンティティ型です。</span><span class="sxs-lookup"><span data-stu-id="bfe72-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="bfe72-134">オープン型を作成するには、CLR 型に、動的プロパティを保持する `IDictionary<string, object>`型のプロパティが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="bfe72-135">EDM モデルの構築</span><span class="sxs-lookup"><span data-stu-id="bfe72-135">Build the EDM Model</span></span>

<span data-ttu-id="bfe72-136">**ODataConventionModelBuilder**を使用して EDM を作成する場合は、`IDictionary<string, object>` プロパティの存在に基づいて、`Press` と `Book` がオープン型として自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="bfe72-137">**使用**を使用して、EDM を明示的に構築することもできます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="bfe72-138">OData コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="bfe72-138">Add an OData Controller</span></span>

<span data-ttu-id="bfe72-139">次に、OData コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-139">Next, add an OData controller.</span></span> <span data-ttu-id="bfe72-140">このチュートリアルでは、GET および POST 要求をサポートする単純なコントローラーを使用し、メモリ内のリストを使用してエンティティを格納します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="bfe72-141">最初の `Book` インスタンスに動的プロパティがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bfe72-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="bfe72-142">2番目の `Book` インスタンスには、次の動的プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="bfe72-143">"公開済み": プリミティブ型</span><span class="sxs-lookup"><span data-stu-id="bfe72-143">"Published": Primitive type</span></span>
- <span data-ttu-id="bfe72-144">"Authors": プリミティブ型のコレクション</span><span class="sxs-lookup"><span data-stu-id="bfe72-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="bfe72-145">"OtherCategories": 列挙型のコレクション。</span><span class="sxs-lookup"><span data-stu-id="bfe72-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="bfe72-146">また、その `Book` インスタンスの `Press` プロパティには、次の動的プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="bfe72-147">"ブログ": プリミティブ型</span><span class="sxs-lookup"><span data-stu-id="bfe72-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="bfe72-148">"Address": Complex type</span><span class="sxs-lookup"><span data-stu-id="bfe72-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="bfe72-149">メタデータのクエリ</span><span class="sxs-lookup"><span data-stu-id="bfe72-149">Query the Metadata</span></span>

<span data-ttu-id="bfe72-150">OData メタデータドキュメントを取得するには、GET 要求を `~/$metadata`に送信します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="bfe72-151">応答本文は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="bfe72-152">メタデータドキュメントから、次のことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="bfe72-153">`Book` 型および `Press` 型の場合、`OpenType` 属性の値は true になります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="bfe72-154">`Customer` 型と `Address` 型には、この属性がありません。</span><span class="sxs-lookup"><span data-stu-id="bfe72-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="bfe72-155">`Book` エンティティ型には、ISBN、Title、および Press という3つの宣言されたプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="bfe72-156">OData メタデータには、CLR クラスの `Book.Properties` プロパティは含まれません。</span><span class="sxs-lookup"><span data-stu-id="bfe72-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="bfe72-157">同様に、`Press` 複合型には、名前とカテゴリの2つの宣言されたプロパティのみがあります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="bfe72-158">メタデータには、CLR クラスの `Press.DynamicProperties` プロパティは含まれません。</span><span class="sxs-lookup"><span data-stu-id="bfe72-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="bfe72-159">エンティティのクエリ</span><span class="sxs-lookup"><span data-stu-id="bfe72-159">Query an Entity</span></span>

<span data-ttu-id="bfe72-160">ISBN が "978-0-7356-7942-9" である書籍を取得するには、GET 要求を `~/Books('978-0-7356-7942-9')`に送信します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="bfe72-161">応答本文は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-161">The response body should look similar to the following.</span></span> <span data-ttu-id="bfe72-162">(読みやすくするためにインデントが設定されています)。</span><span class="sxs-lookup"><span data-stu-id="bfe72-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="bfe72-163">動的プロパティは、宣言されたプロパティと共にインラインに含まれることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bfe72-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="bfe72-164">エンティティを投稿する</span><span class="sxs-lookup"><span data-stu-id="bfe72-164">POST an Entity</span></span>

<span data-ttu-id="bfe72-165">Book エンティティを追加するには、POST 要求を `~/Books`に送信します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="bfe72-166">クライアントは、要求ペイロードに動的なプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="bfe72-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="bfe72-167">要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="bfe72-167">Here is an example request.</span></span> <span data-ttu-id="bfe72-168">"Price" プロパティと "発行済み" プロパティに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bfe72-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="bfe72-169">コントローラーメソッドにブレークポイントを設定すると、Web API によってこれらのプロパティが `Properties` ディクショナリに追加されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="bfe72-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="bfe72-170">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="bfe72-170">Additional Resources</span></span>

[<span data-ttu-id="bfe72-171">OData オープン型のサンプル</span><span class="sxs-lookup"><span data-stu-id="bfe72-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
