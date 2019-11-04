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
# <a name="create-data-transfer-objects-dtos"></a>データ転送オブジェクト (DTO) の作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

現在、web API では、データベースエンティティがクライアントに公開されています。 クライアントは、データベーステーブルに直接マップされるデータを受信します。 ただし、これは必ずしも良いアイデアではありません。 場合によっては、クライアントに送信するデータの形状を変更する必要があります。 たとえば、次の操作を行います。

- 循環参照を削除します (前のセクションを参照してください)。
- クライアントが表示することが想定されていない特定のプロパティを非表示にします。
- ペイロードサイズを減らすために、いくつかのプロパティを省略します。
- 入れ子になったオブジェクトを含むオブジェクトグラフをフラット化して、クライアントにとってより使いやすいようにします。
- "過剰投稿" の脆弱性を回避します。 (詳細については、「[モデルの検証](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください)。
- サービス層とデータベース層を分離します。

これを実現するには、*データ転送オブジェクト*(DTO) を定義します。 DTO は、データがネットワーク経由で送信される方法を定義するオブジェクトです。 Book エンティティのしくみを見てみましょう。 [モデル] フォルダーで、次の2つの DTO クラスを追加します。

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDto` クラスには、書籍モデルのすべてのプロパティが含まれています。ただし、`AuthorName` は作成者名を保持する文字列である点が異なります。 `BookDto` クラスには、`BookDetailDto`のプロパティのサブセットが含まれています。

次に、`BooksController` クラスの2つの GET メソッドを、Dto を返すバージョンに置き換えます。 ここでは、LINQ **Select**ステートメントを使用して、Book エンティティから dto に変換します。

[!code-csharp[Main](part-5/samples/sample2.cs)]

ここでは、新しい `GetBooks` メソッドによって生成される SQL を示します。 EF が LINQ **select**を SQL select ステートメントに変換することを確認できます。

[!code-sql[Main](part-5/samples/sample3.sql)]

最後に、DTO を返すように `PostBook` メソッドを変更します。

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> このチュートリアルでは、コード内の Dto に手動で変換します。 別の方法として、自動変換を自動的に処理する[Automapper](http://automapper.org/)などのライブラリを使用することもできます。
> 
> [!div class="step-by-step"]
> [前へ](part-4.md)
> [次へ](part-6.md)
