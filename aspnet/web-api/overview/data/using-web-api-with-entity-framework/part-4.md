---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: エンティティリレーションの処理 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449122"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="5a886-102">エンティティ関係の処理</span><span class="sxs-lookup"><span data-stu-id="5a886-102">Handling Entity Relations</span></span>

<span data-ttu-id="5a886-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5a886-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5a886-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="5a886-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="5a886-105">ここでは、EF が関連エンティティを読み込む方法と、モデルクラスで循環ナビゲーションプロパティを処理する方法の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="5a886-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="5a886-106">(このセクションでは、背景知識について説明します。チュートリアルを完了するためには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5a886-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="5a886-107">必要に応じて、[パート 5](part-5.md)に進みます。)</span><span class="sxs-lookup"><span data-stu-id="5a886-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="5a886-108">一括読み込みと遅延読み込み</span><span class="sxs-lookup"><span data-stu-id="5a886-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="5a886-109">リレーショナルデータベースで EF を使用する場合は、EF が関連データを読み込む方法について理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="5a886-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="5a886-110">EF によって生成される SQL クエリを確認するのにも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5a886-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="5a886-111">SQL をトレースするには、`BookServiceContext` コンストラクターに次のコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="5a886-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="5a886-112">GET 要求を/api/books に送信すると、次のような JSON が返されます。</span><span class="sxs-lookup"><span data-stu-id="5a886-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="5a886-113">ブックに有効な AuthorId が含まれている場合でも、Author プロパティが null であることがわかります。</span><span class="sxs-lookup"><span data-stu-id="5a886-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="5a886-114">これは、EF が関連する作成者エンティティを読み込まないためです。</span><span class="sxs-lookup"><span data-stu-id="5a886-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="5a886-115">SQL クエリのトレースログでは、次のことが確認されます。</span><span class="sxs-lookup"><span data-stu-id="5a886-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="5a886-116">SELECT ステートメントは Books テーブルから取得し、Author テーブルを参照しません。</span><span class="sxs-lookup"><span data-stu-id="5a886-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="5a886-117">参考までに、本の一覧を返す `BooksController` クラスのメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5a886-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="5a886-118">ここでは、JSON データの一部として著者を返す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5a886-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="5a886-119">Entity Framework に関連データを読み込むには、一括読み込み、遅延読み込み、および明示的な読み込みの3つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="5a886-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="5a886-120">各手法にはトレードオフがあるため、どのように動作するかを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="5a886-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="5a886-121">一括読み込み</span><span class="sxs-lookup"><span data-stu-id="5a886-121">Eager Loading</span></span>

<span data-ttu-id="5a886-122">*一括読み込み*では、EF は最初のデータベースクエリの一部として関連エンティティを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="5a886-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="5a886-123">一括読み込みを実行する**には、拡張メソッド**を使用します。</span><span class="sxs-lookup"><span data-stu-id="5a886-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="5a886-124">これは、クエリに作成者データを含めるように EF に指示します。</span><span class="sxs-lookup"><span data-stu-id="5a886-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="5a886-125">この変更を行ってアプリを実行すると、JSON データは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5a886-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="5a886-126">トレースログには、EF がブックと作成テーブルに対して結合を実行したことが示されます。</span><span class="sxs-lookup"><span data-stu-id="5a886-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="5a886-127">遅延読み込み</span><span class="sxs-lookup"><span data-stu-id="5a886-127">Lazy Loading</span></span>

<span data-ttu-id="5a886-128">遅延読み込みを使用すると、そのエンティティのナビゲーションプロパティが逆参照されるときに、EF によって関連エンティティが自動的に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="5a886-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="5a886-129">遅延読み込みを有効にするには、ナビゲーションプロパティを仮想にします。</span><span class="sxs-lookup"><span data-stu-id="5a886-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="5a886-130">たとえば、Book クラスでは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5a886-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="5a886-131">ここで、次のコードについて考えてみます。</span><span class="sxs-lookup"><span data-stu-id="5a886-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="5a886-132">遅延読み込みが有効になっている場合、`books[0]` の `Author` プロパティにアクセスすると、EF によって作成者のデータベースが照会されます。</span><span class="sxs-lookup"><span data-stu-id="5a886-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="5a886-133">遅延読み込みでは、関連エンティティを取得するたびにクエリが送信されるため、複数のデータベーストリップが必要になります。</span><span class="sxs-lookup"><span data-stu-id="5a886-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="5a886-134">通常、シリアル化するオブジェクトに対して遅延読み込みを無効にします。</span><span class="sxs-lookup"><span data-stu-id="5a886-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="5a886-135">シリアライザーは、モデルのすべてのプロパティを読み取る必要があります。これにより、関連エンティティの読み込みがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="5a886-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="5a886-136">たとえば、EF が遅延読み込みが有効になっているブックの一覧を表示する場合、SQL クエリは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5a886-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="5a886-137">EF によって、3人の作成者に対して3つの個別のクエリが作成されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="5a886-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="5a886-138">遅延読み込みを使用する場合もあります。</span><span class="sxs-lookup"><span data-stu-id="5a886-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="5a886-139">一括読み込みでは、EF によって非常に複雑な結合が生成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5a886-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="5a886-140">または、データの小さなサブセットに関連エンティティが必要な場合や、遅延読み込みの方が効率的な場合もあります。</span><span class="sxs-lookup"><span data-stu-id="5a886-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="5a886-141">シリアル化の問題を回避する1つの方法は、エンティティオブジェクトではなくデータ転送オブジェクト (Dto) をシリアル化することです。</span><span class="sxs-lookup"><span data-stu-id="5a886-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="5a886-142">この方法については、この記事の後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="5a886-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="5a886-143">明示的な読み込み</span><span class="sxs-lookup"><span data-stu-id="5a886-143">Explicit Loading</span></span>

<span data-ttu-id="5a886-144">明示的な読み込みは、コード内で関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。</span><span class="sxs-lookup"><span data-stu-id="5a886-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="5a886-145">明示的な読み込みでは、関連データを読み込むタイミングをより細かく制御できますが、追加のコードが必要です。</span><span class="sxs-lookup"><span data-stu-id="5a886-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="5a886-146">明示的な読み込みの詳細については、「[関連エンティティの読み込み](https://msdn.microsoft.com/data/jj574232#explicit)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5a886-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="5a886-147">ナビゲーションプロパティと循環参照</span><span class="sxs-lookup"><span data-stu-id="5a886-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="5a886-148">書籍と作成者のモデルを定義したときに、著者のリレーションシップに対して `Book` クラスにナビゲーションプロパティを定義しましたが、他の方向にナビゲーションプロパティを定義していませんでした。</span><span class="sxs-lookup"><span data-stu-id="5a886-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="5a886-149">対応するナビゲーションプロパティを `Author` クラスに追加するとどうなりますか。</span><span class="sxs-lookup"><span data-stu-id="5a886-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="5a886-150">残念ながら、これにより、モデルをシリアル化するときに問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="5a886-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="5a886-151">関連データを読み込むと、円形のオブジェクトグラフが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5a886-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="5a886-152">JSON または XML フォーマッタがグラフをシリアル化しようとすると、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="5a886-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="5a886-153">2つのフォーマッタは、異なる例外メッセージをスローします。</span><span class="sxs-lookup"><span data-stu-id="5a886-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="5a886-154">JSON フォーマッタの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5a886-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="5a886-155">XML フォーマッタは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5a886-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="5a886-156">1つの解決策は、次のセクションで説明する Dto を使用することです。</span><span class="sxs-lookup"><span data-stu-id="5a886-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="5a886-157">また、グラフのサイクルを処理するように JSON および XML フォーマッタを構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5a886-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="5a886-158">詳細については、「[循環オブジェクト参照の処理](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5a886-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="5a886-159">このチュートリアルでは、`Author.Book` ナビゲーションプロパティは必要ありません。そのままにしておくことができます。</span><span class="sxs-lookup"><span data-stu-id="5a886-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5a886-160">[前へ](part-3.md)
> [次へ](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="5a886-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
