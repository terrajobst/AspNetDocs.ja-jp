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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API を使用した OData v4 でのオープン型

[Microsoft](https://github.com/microsoft)

> OData v4 では、*オープン型*は、型定義で宣言されているすべてのプロパティに加えて、動的プロパティを含む構造化された型です。 オープン型を使用すると、データモデルに柔軟性を追加できます。 このチュートリアルでは、ASP.NET Web API OData で open types を使用する方法について説明します。
> 
> このチュートリアルでは、ASP.NET Web API で OData エンドポイントを作成する方法を既に理解していることを前提としています。 それ以外の場合は、まず「 [Create a OData V4 Endpoint](create-an-odata-v4-endpoint.md) first」を参照してください。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API OData 5.3
> - OData v4

まず、OData のいくつかの用語を次に示します。

- エンティティ型: キーを持つ構造化型。
- 複合型: キーを持たない構造化された型。
- Open type: 動的プロパティを持つ型。 エンティティ型と複合型の両方を開くことができます。

動的プロパティの値には、プリミティブ型、複合型、または列挙型を指定できます。または、これらの型のいずれかのコレクション。 オープン型の詳細については、 [OData v4 仕様](http://www.odata.org/documentation/odata-version-4-0/)を参照してください。

## <a name="install-the-web-odata-libraries"></a>Web OData ライブラリをインストールする

NuGet パッケージマネージャーを使用して、最新の Web API OData ライブラリをインストールします。 [パッケージマネージャーコンソール] ウィンドウから次のようにします。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR 型を定義する

まず、EDM モデルを CLR 型として定義します。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Entity Data Model (EDM) が作成されると、

- `Category` は列挙型です。
- `Address` は複合型です。 (キーがないため、エンティティ型ではありません)。
- `Customer` はエンティティ型です。 (キーがあります)。
- `Press` はオープン複合型です。
- `Book` はオープンエンティティ型です。

オープン型を作成するには、CLR 型に、動的プロパティを保持する `IDictionary<string, object>`型のプロパティが含まれている必要があります。

## <a name="build-the-edm-model"></a>EDM モデルの構築

**ODataConventionModelBuilder**を使用して EDM を作成する場合は、`IDictionary<string, object>` プロパティの存在に基づいて、`Press` と `Book` がオープン型として自動的に追加されます。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

**使用**を使用して、EDM を明示的に構築することもできます。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData コントローラーを追加する

次に、OData コントローラーを追加します。 このチュートリアルでは、GET および POST 要求をサポートする単純なコントローラーを使用し、メモリ内のリストを使用してエンティティを格納します。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

最初の `Book` インスタンスに動的プロパティがないことに注意してください。 2番目の `Book` インスタンスには、次の動的プロパティがあります。

- "公開済み": プリミティブ型
- "Authors": プリミティブ型のコレクション
- "OtherCategories": 列挙型のコレクション。

また、その `Book` インスタンスの `Press` プロパティには、次の動的プロパティがあります。

- "ブログ": プリミティブ型
- "Address": Complex type

## <a name="query-the-metadata"></a>メタデータのクエリ

OData メタデータドキュメントを取得するには、GET 要求を `~/$metadata`に送信します。 応答本文は次のようになります。

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

メタデータドキュメントから、次のことを確認できます。

- `Book` 型および `Press` 型の場合、`OpenType` 属性の値は true になります。 `Customer` 型と `Address` 型には、この属性がありません。
- `Book` エンティティ型には、ISBN、Title、および Press という3つの宣言されたプロパティがあります。 OData メタデータには、CLR クラスの `Book.Properties` プロパティは含まれません。
- 同様に、`Press` 複合型には、名前とカテゴリの2つの宣言されたプロパティのみがあります。 メタデータには、CLR クラスの `Press.DynamicProperties` プロパティは含まれません。

## <a name="query-an-entity"></a>エンティティのクエリ

ISBN が "978-0-7356-7942-9" である書籍を取得するには、GET 要求を `~/Books('978-0-7356-7942-9')`に送信します。 応答本文は次のようになります。 (読みやすくするためにインデントが設定されています)。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

動的プロパティは、宣言されたプロパティと共にインラインに含まれることに注意してください。

## <a name="post-an-entity"></a>エンティティを投稿する

Book エンティティを追加するには、POST 要求を `~/Books`に送信します。 クライアントは、要求ペイロードに動的なプロパティを設定できます。

要求の例を次に示します。 "Price" プロパティと "発行済み" プロパティに注意してください。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

コントローラーメソッドにブレークポイントを設定すると、Web API によってこれらのプロパティが `Properties` ディクショナリに追加されたことがわかります。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>その他のリソース

[OData オープン型のサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
