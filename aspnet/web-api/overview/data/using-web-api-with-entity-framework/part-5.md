---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: データ転送オブジェクトの作成 (Dto) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445759"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="0c733-102">データ転送オブジェクト (DTO) の作成</span><span class="sxs-lookup"><span data-stu-id="0c733-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="0c733-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0c733-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0c733-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="0c733-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="0c733-105">現在、web API では、データベースエンティティがクライアントに公開されています。</span><span class="sxs-lookup"><span data-stu-id="0c733-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="0c733-106">クライアントは、データベーステーブルに直接マップされるデータを受信します。</span><span class="sxs-lookup"><span data-stu-id="0c733-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="0c733-107">ただし、これは必ずしも良いアイデアではありません。</span><span class="sxs-lookup"><span data-stu-id="0c733-107">However, that's not always a good idea.</span></span> <span data-ttu-id="0c733-108">場合によっては、クライアントに送信するデータの形状を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c733-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="0c733-109">たとえば、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="0c733-109">For example, you might want to:</span></span>

- <span data-ttu-id="0c733-110">循環参照を削除します (前のセクションを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="0c733-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="0c733-111">クライアントが表示することが想定されていない特定のプロパティを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="0c733-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="0c733-112">ペイロードサイズを減らすために、いくつかのプロパティを省略します。</span><span class="sxs-lookup"><span data-stu-id="0c733-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="0c733-113">入れ子になったオブジェクトを含むオブジェクトグラフをフラット化して、クライアントにとってより使いやすいようにします。</span><span class="sxs-lookup"><span data-stu-id="0c733-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="0c733-114">"過剰投稿" の脆弱性を回避します。</span><span class="sxs-lookup"><span data-stu-id="0c733-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="0c733-115">(詳細については、「[モデルの検証](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="0c733-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="0c733-116">サービス層とデータベース層を分離します。</span><span class="sxs-lookup"><span data-stu-id="0c733-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="0c733-117">これを実現するには、*データ転送オブジェクト*(DTO) を定義します。</span><span class="sxs-lookup"><span data-stu-id="0c733-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="0c733-118">DTO は、データがネットワーク経由で送信される方法を定義するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="0c733-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="0c733-119">Book エンティティのしくみを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0c733-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="0c733-120">[モデル] フォルダーで、次の2つの DTO クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="0c733-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="0c733-121">`BookDetailDto` クラスには、書籍モデルのすべてのプロパティが含まれています。ただし、`AuthorName` は作成者名を保持する文字列である点が異なります。</span><span class="sxs-lookup"><span data-stu-id="0c733-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="0c733-122">`BookDto` クラスには、`BookDetailDto`のプロパティのサブセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c733-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="0c733-123">次に、`BooksController` クラスの2つの GET メソッドを、Dto を返すバージョンに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0c733-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="0c733-124">ここでは、LINQ **Select**ステートメントを使用して、Book エンティティから dto に変換します。</span><span class="sxs-lookup"><span data-stu-id="0c733-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="0c733-125">ここでは、新しい `GetBooks` メソッドによって生成される SQL を示します。</span><span class="sxs-lookup"><span data-stu-id="0c733-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="0c733-126">EF が LINQ **select**を SQL select ステートメントに変換することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0c733-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="0c733-127">最後に、DTO を返すように `PostBook` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="0c733-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="0c733-128">このチュートリアルでは、コード内の Dto に手動で変換します。</span><span class="sxs-lookup"><span data-stu-id="0c733-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="0c733-129">別の方法として、自動変換を自動的に処理する[Automapper](http://automapper.org/)などのライブラリを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="0c733-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="0c733-130">[前へ](part-4.md)
> [次へ](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="0c733-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
