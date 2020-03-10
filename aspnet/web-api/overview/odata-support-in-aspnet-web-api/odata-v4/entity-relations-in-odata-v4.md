---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: ASP.NET Web API 2.2 | を使用した OData v4 のエンティティの関係Microsoft Docs
author: MikeWasson
description: ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 クライアントは、OData を使用して移動できます...
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484462"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 を使用した OData v4 のエンティティの関係

[Mike Wasson](https://github.com/MikeWasson)

> ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 OData を使用すると、クライアントはエンティティの関係を移動できます。 製品を指定すると、業者を見つけることができます。 リレーションシップを作成または削除することもできます。 たとえば、製品の仕入先を設定できます。
>
> このチュートリアルでは、ASP.NET Web API を使用して OData v4 でこれらの操作をサポートする方法を示します。 このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - Web API 2.1
> - OData v4
> - Visual Studio 2013 (こちらから Visual Studio 2017 をダウンロードして[ください](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>チュートリアルのバージョン
>
> OData バージョン3については、「 [odata v3 でのエンティティリレーションのサポート](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)」を参照してください。

## <a name="add-a-supplier-entity"></a>Supplier エンティティを追加する

> [!NOTE]
> このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。

まず、関連エンティティが必要です。 `Supplier` という名前のクラスを [モデル] フォルダーに追加します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

`Product` クラスにナビゲーションプロパティを追加します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

新しい**Dbset**を `ProductsContext` クラスに追加して、Entity Framework に Supplier テーブルをデータベースに含めます。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

WebApiConfig.cs で、エンティティデータモデルに &quot;のサプライヤー&quot; エンティティセットを追加します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>サプライヤーコントローラーを追加する

Controllers フォルダーに `SuppliersController` クラスを追加します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

このコントローラーに対して CRUD 操作を追加する方法については説明しません。 これらの手順は、Products コントローラーの場合と同じです (「 [OData V4 エンドポイントを作成する](create-an-odata-v4-endpoint.md)」を参照してください)。

## <a name="getting-related-entities"></a>関連エンティティの取得

製品の供給業者を取得するために、クライアントは GET 要求を送信します。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

この要求をサポートするには、次のメソッドを `ProductsController` クラスに追加します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

このメソッドは、既定の名前付け規則を使用します。

- メソッド名: GetX。ここで、X はナビゲーションプロパティです。
- パラメーター名:*キー*

この名前付け規則に従うと、Web API によって HTTP 要求がコントローラーメソッドに自動的にマップされます。

HTTP 要求の例:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

HTTP 応答の例:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>関連コレクションの取得

前の例では、製品に1つの仕入先があります。 ナビゲーションプロパティは、コレクションを返すこともできます。 次のコードは、業者の製品を取得します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

この場合、メソッドは、 **SingleResult&lt;t**ではなく**IQueryable**を返し&gt;

HTTP 要求の例:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

HTTP 応答の例:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>エンティティ間のリレーションシップの作成

OData は、既存の2つのエンティティ間のリレーションシップの作成または削除をサポートしています。 OData v4 の用語では、リレーションシップは &quot;参照&quot;です。 (OData v3 では、リレーションシップは*リンク*と呼ばれていました。 このチュートリアルでは、プロトコルの違いはありません)。

参照には、`/Entity/NavigationProperty/$ref`という形式の独自の URI があります。 たとえば、製品とその業者との間の参照に対応する URI を次に示します。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

リレーションシップを追加するために、クライアントはこのアドレスに POST または PUT 要求を送信します。

- ナビゲーションプロパティが `Product.Supplier`などの単一のエンティティである場合は、を配置します。
- ナビゲーションプロパティが `Supplier.Products`などのコレクションである場合は POST。

要求の本文には、リレーションシップ内の他のエンティティの URI が含まれます。 要求の例を次に示します。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

この例では、クライアントが PUT 要求を `/Products(6)/Supplier/$ref`に送信します。これは、ID = 6 の製品の `Supplier` の $ref URI です。 要求が成功した場合、サーバーは 204 (コンテンツなし) の応答を送信します。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

`Product`にリレーションシップを追加するコントローラーメソッドを次に示します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*NavigationProperty*パラメーターは、設定するリレーションシップを指定します。 (エンティティに複数のナビゲーションプロパティがある場合は、さらに `case` ステートメントを追加できます)。

*Link*パラメーターには、業者の URI が含まれています。 Web API は、要求本文を自動的に解析して、このパラメーターの値を取得します。

業者を検索するには、*リンク*パラメーターの一部である ID (またはキー) が必要です。 これを行うには、次のヘルパーメソッドを使用します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

基本的に、このメソッドは、OData ライブラリを使用して URI パスをセグメントに分割し、キーを含むセグメントを見つけて、キーを正しい型に変換します。

## <a name="deleting-a-relationship-between-entities"></a>エンティティ間のリレーションシップの削除

リレーションシップを削除するために、クライアントは HTTP DELETE 要求を $ref URI に送信します。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

製品と業者の関係を削除するコントローラーメソッドを次に示します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

この場合、`Product.Supplier` は1対多の関係の &quot;1&quot; 終了であるため、`Product.Supplier` を `null`に設定するだけでリレーションシップを削除できます。

リレーションシップの多くの&quot; end &quot;、クライアントは、削除する関連エンティティを指定する必要があります。 これを行うために、クライアントは、要求のクエリ文字列内に関連エンティティの URI を送信します。 たとえば、"Supplier 1" から "Product 1" を削除するには、次のようにします。

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

Web API でこれをサポートするには、`DeleteRef` メソッドに追加のパラメーターを含める必要があります。 `Supplier.Products` 関係から製品を削除するコントローラーメソッドを次に示します。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*キー*パラメーターは業者のキーであり、関連*キー*パラメーターは、`Products` リレーションシップから削除する製品のキーです。 Web API は、クエリ文字列からキーを自動的に取得することに注意してください。
