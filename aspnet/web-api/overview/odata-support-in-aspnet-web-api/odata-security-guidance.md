---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData-ASP.NET 4.x のセキュリティガイダンス
author: MikeWasson
description: ASP.NET 4.x で ASP.NET Web API 2 の OData を使用してデータセットを公開するときに考慮する必要があるセキュリティの問題について説明します。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448294"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="a638a-103">ASP.NET Web API 2 OData のセキュリティガイダンス</span><span class="sxs-lookup"><span data-stu-id="a638a-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="a638a-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a638a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a638a-105">このトピックでは、ASP.NET 4.x で ASP.NET Web API 2 の OData を使用してデータセットを公開するときに考慮する必要があるセキュリティの問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a638a-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="a638a-106">EDM のセキュリティ</span><span class="sxs-lookup"><span data-stu-id="a638a-106">EDM Security</span></span>

<span data-ttu-id="a638a-107">クエリセマンティクスは、基になるモデル型ではなく、entity data model (EDM) に基づいています。</span><span class="sxs-lookup"><span data-stu-id="a638a-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="a638a-108">EDM からプロパティを除外することはできますが、クエリには表示されません。</span><span class="sxs-lookup"><span data-stu-id="a638a-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="a638a-109">たとえば、モデルに Salary プロパティを持つ Employee 型が含まれているとします。</span><span class="sxs-lookup"><span data-stu-id="a638a-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="a638a-110">このプロパティを EDM から除外して、クライアントから非表示にすることができます。</span><span class="sxs-lookup"><span data-stu-id="a638a-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="a638a-111">EDM からプロパティを除外するには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="a638a-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="a638a-112">モデルクラスのプロパティに対して **[Ignoredatamember]** 属性を設定できます。</span><span class="sxs-lookup"><span data-stu-id="a638a-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="a638a-113">プログラムを使用して EDM からプロパティを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="a638a-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="a638a-114">クエリのセキュリティ</span><span class="sxs-lookup"><span data-stu-id="a638a-114">Query Security</span></span>

<span data-ttu-id="a638a-115">悪意のあるクライアントや単純なクライアントでは、実行に非常に長い時間がかかるクエリを作成できる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a638a-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="a638a-116">最悪の場合、これによってサービスへのアクセスが中断される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a638a-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="a638a-117">[クエリ可能 **]** 属性は、クエリを解析、検証、適用するアクションフィルターです。</span><span class="sxs-lookup"><span data-stu-id="a638a-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="a638a-118">このフィルターにより、クエリオプションが LINQ 式に変換されます。</span><span class="sxs-lookup"><span data-stu-id="a638a-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="a638a-119">OData コントローラーが**iqueryable**型を返すと、 **iqueryable** linq プロバイダーは linq 式をクエリに変換します。</span><span class="sxs-lookup"><span data-stu-id="a638a-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="a638a-120">そのため、パフォーマンスは、使用される LINQ プロバイダーと、データセットまたはデータベーススキーマの特定の特性に依存します。</span><span class="sxs-lookup"><span data-stu-id="a638a-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="a638a-121">ASP.NET Web API での OData クエリオプションの使用の詳細については、「 [Odata クエリオプションのサポート](supporting-odata-query-options.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="a638a-122">すべてのクライアントが信頼されている (たとえば、エンタープライズ環境で) ことがわかっている場合、またはデータセットが小さい場合は、クエリのパフォーマンスが問題になるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="a638a-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="a638a-123">それ以外の場合は、次の推奨事項を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a638a-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="a638a-124">さまざまなクエリを使用してサービスをテストし、データベースをプロファイルします。</span><span class="sxs-lookup"><span data-stu-id="a638a-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="a638a-125">サーバードリブンページングを有効にして、1つのクエリで大きなデータセットを返さないようにします。</span><span class="sxs-lookup"><span data-stu-id="a638a-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="a638a-126">詳細については、「[サーバードリブンページング](supporting-odata-query-options.md#server-paging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="a638a-127">$Filter と $orderby 必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="a638a-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="a638a-128">アプリケーションによっては、$top と $skip を使用したクライアントのページングが許可されているが、他のクエリオプションは無効になっている場合があります</span><span class="sxs-lookup"><span data-stu-id="a638a-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="a638a-129">クラスター化インデックスのプロパティに $orderby を制限することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="a638a-130">クラスター化インデックスを使用せずに大きなデータを並べ替えると、処理が遅くなります。</span><span class="sxs-lookup"><span data-stu-id="a638a-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="a638a-131">最大ノード数: **[クエリ可能]** の**MaxNodeCount**プロパティは、$filter 構文ツリーで許可される最大ノード数を設定します。</span><span class="sxs-lookup"><span data-stu-id="a638a-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="a638a-132">既定値は100ですが、多数のノードがコンパイルに時間がかかる場合があるため、値を小さく設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a638a-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="a638a-133">これは、LINQ to Objects (つまり、中間の LINQ プロバイダーを使用せずにメモリ内のコレクションに対する LINQ クエリ) を使用している場合に特に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="a638a-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="a638a-134">Any () 関数と all () 関数は、処理速度が低下する可能性があるため、無効にすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="a638a-135">文字列プロパティに大きな文字列&#8212;が含まれている場合は、製品の説明また&#8212;はブログのエントリによって文字列関数の無効化が検討されます。</span><span class="sxs-lookup"><span data-stu-id="a638a-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="a638a-136">ナビゲーションプロパティのフィルター選択を禁止することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="a638a-137">ナビゲーションプロパティをフィルター処理すると、データベーススキーマによっては、結合が遅くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a638a-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="a638a-138">次のコードは、ナビゲーションプロパティのフィルター処理を妨げるクエリ検証コントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="a638a-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="a638a-139">クエリ検証コントロールの詳細については、「[クエリの検証](supporting-odata-query-options.md#query-validation)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="a638a-140">データベース用にカスタマイズされたバリデーターを記述して、$filter クエリを制限することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="a638a-141">たとえば、次の2つのクエリについて考えてみます。</span><span class="sxs-lookup"><span data-stu-id="a638a-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="a638a-142">"A" で始まる姓を持つアクターを持つすべてのムービー。</span><span class="sxs-lookup"><span data-stu-id="a638a-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="a638a-143">1994でリリースされたすべてのムービー。</span><span class="sxs-lookup"><span data-stu-id="a638a-143">All movies released in 1994.</span></span>

    <span data-ttu-id="a638a-144">映画がアクターによってインデックス付けされていない限り、最初のクエリでは、データベースエンジンがムービーの一覧全体をスキャンするように要求することがあります。</span><span class="sxs-lookup"><span data-stu-id="a638a-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="a638a-145">2番目のクエリは許容できるかもしれませんが、release year によってムービーのインデックスが作成されると想定します。</span><span class="sxs-lookup"><span data-stu-id="a638a-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="a638a-146">次のコードは、"ReleaseYear" プロパティと "Title" プロパティをフィルター処理できますが、その他のプロパティは使用できないバリデーターを示しています。</span><span class="sxs-lookup"><span data-stu-id="a638a-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="a638a-147">一般に、必要な $filter 関数を検討してください。</span><span class="sxs-lookup"><span data-stu-id="a638a-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="a638a-148">クライアントが $filter の完全な表現力を必要としない場合は、許可される関数を制限できます。</span><span class="sxs-lookup"><span data-stu-id="a638a-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
