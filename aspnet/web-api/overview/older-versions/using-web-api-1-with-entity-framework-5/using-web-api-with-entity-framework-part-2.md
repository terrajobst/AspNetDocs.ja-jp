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
# <a name="part-2-creating-the-domain-models"></a>パート 2: ドメインモデルの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>モデルの追加

Entity Framework アプローチには、次の3つの方法があります。

- データベース優先: データベースから開始し、Entity Framework によってコードが生成されます。
- モデル優先: ビジュアルモデルから開始すると、Entity Framework によってデータベースとコードの両方が生成されます。
- Code first: code から開始し、Entity Framework によってデータベースが生成されます。

コード優先の方法を使用しているので、まず、ドメインオブジェクトを POCOs (plain old CLR object) として定義します。 コード優先のアプローチでは、データベースレイヤーをサポートするために、ドメインオブジェクトにはトランザクションや永続化などの追加のコードは必要ありません。 (具体的には、 [Entityobject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)クラスから継承する必要はありません)。データ注釈を使用して、Entity Framework がデータベーススキーマを作成する方法を制御することもできます。

POCOs には[データベースの状態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)を説明する追加のプロパティがないため、JSON または XML に簡単にシリアル化できます。 ただし、このチュートリアルで後ほど説明するように、これは常に Entity Framework モデルをクライアントに直接公開する必要があるという意味ではありません。

次の POCOs が作成されます。

- Product
- Order
- OrderDetail

各クラスを作成するには、ソリューションエクスプローラーで [モデル] フォルダーを右クリックします。 コンテキストメニューから **追加** を選択し、クラス を選択し**ます。**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

次の実装を使用して `Product` クラスを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

慣例により、Entity Framework は `Id` プロパティを主キーとして使用し、データベーステーブル内の id 列にマップします。 新しい `Product` インスタンスを作成した場合、データベースで値が生成されるため、`Id`の値は設定されません。

**ScaffoldColumn**属性は、エディターフォームを生成するときに、`Id` プロパティをスキップするように ASP.NET MVC に指示します。 **必須**の属性は、モデルの検証に使用されます。 `Name` プロパティは、空でない文字列である必要があることを指定します。

`Order` クラスを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

`OrderDetail` クラスを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>外部キーの関係

注文には多くの注文の詳細が含まれ、各注文の詳細は1つの製品を表します。 これらの関係を表すために、`OrderDetail` クラスは `OrderId` と `ProductId`という名前のプロパティを定義します。 Entity Framework は、これらのプロパティが外部キーを表していることを推定し、データベースに外部キー制約を追加します。

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order` クラスと `OrderDetail` クラスには、関連オブジェクトへの参照を含む "ナビゲーション" プロパティも含まれています。 順序を指定すると、ナビゲーションプロパティに従って、注文内の製品に移動できます。

ここでプロジェクトをコンパイルします。 Entity Framework は、リフレクションを使用してモデルのプロパティを検出します。そのため、データベーススキーマを作成するには、コンパイル済みのアセンブリが必要です。

## <a name="configure-the-media-type-formatters"></a>メディアの種類のフォーマッタを構成する

[メディアの種類のフォーマッタ](../../formats-and-model-binding/media-formatters.md)は、Web API が HTTP 応答の本文を書き込むときにデータをシリアル化するオブジェクトです。 組み込みのフォーマッタは、JSON と XML の出力をサポートしています。 既定では、これらのフォーマッタはいずれも、値によってすべてのオブジェクトをシリアル化します。

値によるシリアル化では、オブジェクトグラフに循環参照が含まれている場合に問題が発生します。 これは、それぞれが別の参照を保持しているため、`Order` クラスと `OrderDetail` クラスの場合とまったく同じです。 フォーマッタは参照に従い、各オブジェクトを値で書き込んで、円で囲みます。 そのため、既定の動作を変更する必要があります。

ソリューションエクスプローラーで、アプリ\_スタートフォルダーを展開し、WebApiConfig.cs という名前のファイルを開きます。 以下のコードを `WebApiConfig` クラスに追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

このコードは、オブジェクト参照を保持するように JSON フォーマッタを設定し、パイプラインから XML フォーマッタを完全に削除します。 (XML フォーマッタは、オブジェクト参照を保持するように構成できますが、作業は少しだけで、このアプリケーションには JSON のみが必要です。 詳細については、「[循環オブジェクト参照の処理](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)」を参照してください。

> [!div class="step-by-step"]
> [前へ](using-web-api-with-entity-framework-part-1.md)
> [次へ](using-web-api-with-entity-framework-part-3.md)
