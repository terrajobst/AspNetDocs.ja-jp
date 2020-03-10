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
# <a name="handling-entity-relations"></a>エンティティ関係の処理

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

ここでは、EF が関連エンティティを読み込む方法と、モデルクラスで循環ナビゲーションプロパティを処理する方法の詳細について説明します。 (このセクションでは、背景知識について説明します。チュートリアルを完了するためには必要ありません。 必要に応じて、[パート 5](part-5.md)に進みます。)

## <a name="eager-loading-versus-lazy-loading"></a>一括読み込みと遅延読み込み

リレーショナルデータベースで EF を使用する場合は、EF が関連データを読み込む方法について理解しておくことが重要です。

EF によって生成される SQL クエリを確認するのにも役立ちます。 SQL をトレースするには、`BookServiceContext` コンストラクターに次のコード行を追加します。

[!code-csharp[Main](part-4/samples/sample1.cs)]

GET 要求を/api/books に送信すると、次のような JSON が返されます。

[!code-console[Main](part-4/samples/sample2.cmd)]

ブックに有効な AuthorId が含まれている場合でも、Author プロパティが null であることがわかります。 これは、EF が関連する作成者エンティティを読み込まないためです。 SQL クエリのトレースログでは、次のことが確認されます。

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT ステートメントは Books テーブルから取得し、Author テーブルを参照しません。

参考までに、本の一覧を返す `BooksController` クラスのメソッドを次に示します。

[!code-csharp[Main](part-4/samples/sample4.cs)]

ここでは、JSON データの一部として著者を返す方法について説明します。 Entity Framework に関連データを読み込むには、一括読み込み、遅延読み込み、および明示的な読み込みの3つの方法があります。 各手法にはトレードオフがあるため、どのように動作するかを理解することが重要です。

### <a name="eager-loading"></a>一括読み込み

*一括読み込み*では、EF は最初のデータベースクエリの一部として関連エンティティを読み込みます。 一括読み込みを実行する**には、拡張メソッド**を使用します。

[!code-csharp[Main](part-4/samples/sample5.cs)]

これは、クエリに作成者データを含めるように EF に指示します。 この変更を行ってアプリを実行すると、JSON データは次のようになります。

[!code-console[Main](part-4/samples/sample6.cmd)]

トレースログには、EF がブックと作成テーブルに対して結合を実行したことが示されます。

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>遅延読み込み

遅延読み込みを使用すると、そのエンティティのナビゲーションプロパティが逆参照されるときに、EF によって関連エンティティが自動的に読み込まれます。 遅延読み込みを有効にするには、ナビゲーションプロパティを仮想にします。 たとえば、Book クラスでは、次のようになります。

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

ここで、次のコードについて考えてみます。

[!code-csharp[Main](part-4/samples/sample9.cs)]

遅延読み込みが有効になっている場合、`books[0]` の `Author` プロパティにアクセスすると、EF によって作成者のデータベースが照会されます。

遅延読み込みでは、関連エンティティを取得するたびにクエリが送信されるため、複数のデータベーストリップが必要になります。 通常、シリアル化するオブジェクトに対して遅延読み込みを無効にします。 シリアライザーは、モデルのすべてのプロパティを読み取る必要があります。これにより、関連エンティティの読み込みがトリガーされます。 たとえば、EF が遅延読み込みが有効になっているブックの一覧を表示する場合、SQL クエリは次のようになります。 EF によって、3人の作成者に対して3つの個別のクエリが作成されていることがわかります。

[!code-console[Main](part-4/samples/sample10.sql)]

遅延読み込みを使用する場合もあります。 一括読み込みでは、EF によって非常に複雑な結合が生成される可能性があります。 または、データの小さなサブセットに関連エンティティが必要な場合や、遅延読み込みの方が効率的な場合もあります。

シリアル化の問題を回避する1つの方法は、エンティティオブジェクトではなくデータ転送オブジェクト (Dto) をシリアル化することです。 この方法については、この記事の後半で説明します。

### <a name="explicit-loading"></a>明示的な読み込み

明示的な読み込みは、コード内で関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。 明示的な読み込みでは、関連データを読み込むタイミングをより細かく制御できますが、追加のコードが必要です。 明示的な読み込みの詳細については、「[関連エンティティの読み込み](https://msdn.microsoft.com/data/jj574232#explicit)」を参照してください。

## <a name="navigation-properties-and-circular-references"></a>ナビゲーションプロパティと循環参照

書籍と作成者のモデルを定義したときに、著者のリレーションシップに対して `Book` クラスにナビゲーションプロパティを定義しましたが、他の方向にナビゲーションプロパティを定義していませんでした。

対応するナビゲーションプロパティを `Author` クラスに追加するとどうなりますか。

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

残念ながら、これにより、モデルをシリアル化するときに問題が発生します。 関連データを読み込むと、円形のオブジェクトグラフが作成されます。

![](part-4/_static/image1.png)

JSON または XML フォーマッタがグラフをシリアル化しようとすると、例外がスローされます。 2つのフォーマッタは、異なる例外メッセージをスローします。 JSON フォーマッタの例を次に示します。

[!code-console[Main](part-4/samples/sample12.cmd)]

XML フォーマッタは次のようになります。

[!code-xml[Main](part-4/samples/sample13.xml)]

1つの解決策は、次のセクションで説明する Dto を使用することです。 また、グラフのサイクルを処理するように JSON および XML フォーマッタを構成することもできます。 詳細については、「[循環オブジェクト参照の処理](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)」を参照してください。

このチュートリアルでは、`Author.Book` ナビゲーションプロパティは必要ありません。そのままにしておくことができます。

> [!div class="step-by-step"]
> [前へ](part-3.md)
> [次へ](part-5.md)
