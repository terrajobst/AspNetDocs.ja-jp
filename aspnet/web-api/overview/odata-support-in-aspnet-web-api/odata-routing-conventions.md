---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 でのルーティング規則-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の Web API 2 が OData エンドポイントに使用するルーティング規則について説明します。
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498196"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 Odata でのルーティング規則

[Mike Wasson](https://github.com/MikeWasson)

> この記事では、ASP.NET 4.x の Web API 2 が OData エンドポイントに使用するルーティング規則について説明します。

Web API が OData 要求を取得すると、コントローラー名とアクション名に要求がマップされます。 マッピングは、HTTP メソッドと URI に基づいています。 たとえば、`GET /odata/Products(1)` は `ProductsController.GetProduct`にマップされます。

この記事のパート1では、組み込みの OData ルーティング規則について説明します。 これらの規則は、特に OData エンドポイント専用に設計されており、既定の Web API ルーティングシステムを置き換えます。 (置換は**MapODataRoute**を呼び出すと発生します)。

パート2では、カスタムルーティング規則を追加する方法について説明します。 現時点では、組み込み規則は OData Uri の範囲全体をカバーしていませんが、追加のケースを処理するように拡張することができます。

- [組み込みのルーティング規則](#conventions)
- [カスタムルーティング規則](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>組み込みのルーティング規則

Web API で OData ルーティング規則を記述する前に、OData Uri について理解しておくことをお勧めします。 [ODATA URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)は次の要素で構成されます。

- サービスルート
- リソースパス
- クエリ オプション

![](odata-routing-conventions/_static/image1.png)

ルーティングの場合、重要な部分はリソースパスです。 リソースパスはセグメントに分割されます。 たとえば、`/Products(1)/Supplier` には次の3つのセグメントがあります。

- `Products` は、"Products" という名前のエンティティセットを参照します。
- `1` は、セットから1つのエンティティを選択するエンティティキーです。
- `Supplier` は、関連エンティティを選択するナビゲーションプロパティです。

このパスは、製品1の供給業者を取得します。

> [!NOTE]
> OData パスセグメントは、常に URI セグメントに対応するとは限りません。 たとえば、"1" はパスセグメントと見なされます。

**コントローラー名。** コントローラー名は、常に、リソースパスのルートにあるエンティティセットから派生します。 たとえば、リソースパスが `/Products(1)/Supplier`場合、Web API は `ProductsController`という名前のコントローラーを検索します。

**アクション名。** アクション名は、次の表に示すように、パスセグメントと entity data model (EDM) から派生します。 場合によっては、アクション名に2つの選択肢があります。 たとえば、"Get" または &quot;GetProducts&quot;です。

**エンティティの照会**

| Request | URI の例 | アクション名 | アクションの例 |
| --- | --- | --- | --- |
| GET /entityset | /Products | GetEntitySet または Get | GetProducts |
| GET /entityset(key) | /製品 (1) | GetEntityType または Get | GetProduct |
| GET /entityset(key)/cast | /製品 (1)/Models.Book | GetEntityType または Get | GetBook |

詳細については、「読み取り専用の[OData エンドポイントを作成する](odata-v3/creating-an-odata-endpoint.md)」を参照してください。

**エンティティの作成、更新、および削除**

| Request | URI の例 | アクション名 | アクションの例 |
| --- | --- | --- | --- |
| 投稿/entityset | /Products | PostEntityType または Post | PostProduct |
| PUT /entityset(key) | /製品 (1) | PutEntityType または Put | PutProduct |
| PUT/entityset (キー)/cast | /製品 (1)/Models.Book | PutEntityType または Put | PutBook |
| PATCH /entityset(key) | /製品 (1) | Patch Entitytype または Patch | パッチ製品 |
| PATCH /entityset(key)/cast | /製品 (1)/Models.Book | Patch Entitytype または Patch | パッチブック |
| DELETE /entityset(key) | /製品 (1) | DeleteEntityType または Delete | DeleteProduct |
| DELETE /entityset(key)/cast | /製品 (1)/Models.Book | DeleteEntityType または Delete | DeleteBook |

**ナビゲーションプロパティのクエリ**

| Request | URI の例 | アクション名 | アクションの例 |
| --- | --- | --- | --- |
| GET /entityset(key)/navigation | /製品 (1)/仕入先 | GetNavigationFromEntityType または GetNavigation | GetSupplierFromProduct |
| GET/entityset (キー)/cast/navigation | /Products(1)/Models.Book/Author | GetNavigationFromEntityType または GetNavigation | GetAuthorFromBook |

詳細については、「[エンティティリレーションの操作](odata-v3/working-with-entity-relations.md)」を参照してください。

**リンクの作成と削除**

| Request | URI の例 | アクション名 |
| --- | --- | --- |
| POST /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | CreateLink |
| 配置/entityset (キー)/$links/ナビゲーション | /Products(1)/$links/Supplier | CreateLink |
| DELETE /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | DeleteLink |
| DELETE /entityset(key)/$links/navigation(relatedKey) | /製品/(1)/$links/仕入先 (1) | DeleteLink |

詳細については、「[エンティティリレーションの操作](odata-v3/working-with-entity-relations.md)」を参照してください。

**Properties**

*Web API 2 が必要です*

| Request | URI の例 | アクション名 | アクションの例 |
| --- | --- | --- | --- |
| GET /entityset(key)/property | /製品 (1)/Name | GetPropertyFromEntityType または GetProperty | GetNameFromProduct |
| GET /entityset(key)/cast/property | /Products(1)/Models.Book/Author | GetPropertyFromEntityType または GetProperty | Getタイトル Frombook |

**アクション**

| Request | URI の例 | アクション名 | アクションの例 |
| --- | --- | --- | --- |
| POST /entityset(key)/action | /製品 (1)/レート | ActionNameOnEntityType または ActionName | RateOnProduct |
| POST/entityset (キー)/cast/action | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType または ActionName | CheckOutOnBook |

詳細については、「 [OData アクション](odata-v3/odata-actions.md)」を参照してください。

**メソッドシグネチャ**

メソッドシグネチャの規則をいくつか次に示します。

- パスにキーが含まれている場合、アクションには*key*という名前のパラメーターが必要です。
- パスにナビゲーションプロパティへのキーが含まれている場合、アクションには、[関連性*キー*] という名前のパラメーターが必要です。
- *キー*および関連性のある*キー*パラメーターを **[fromodatauri]** パラメーターで修飾します。
- POST および PUT 要求は、エンティティ型のパラメーターを受け取ります。
- PATCH 要求では、型が**Delta&lt;t&gt;** のパラメーターを受け取ります。ここで、 *t*はエンティティ型です。

ここでは、組み込みの OData ルーティング規則ごとにメソッドシグネチャを示す例を紹介します。

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>カスタムルーティング規則

現時点では、組み込みの規則は、使用可能なすべての OData Uri に対応しているわけではありません。 **IODataRoutingConvention**インターフェイスを実装することで、新しい規則を追加できます。 このインターフェイスには、次の2つのメソッドがあります。

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **Selectcontroller**はコントローラーの名前を返します。
- **Selectaction**は、アクションの名前を返します。

どちらの方法でも、規則がその要求に適用されない場合、メソッドは null を返す必要があります。

**ODataPath**パラメーターは、解析された OData リソースパスを表します。 これには、リソースパスのセグメントごとに1つの **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** インスタンスのリストが含まれています。 **ODataPathSegment**は抽象クラスです。各セグメントの種類は、 **ODataPathSegment**から派生したクラスによって表されます。

**ODataPath path**プロパティは、すべてのパスセグメントの連結を表す文字列です。 たとえば、URI が `/Products(1)/Supplier`の場合、パステンプレートは次のように &quot;ます&quot;。 セグメントが URI セグメントに直接対応していないことに注意してください。 たとえば、エンティティキー (1) は、それ自体の**ODataPathSegment**として表されます。

通常、 **IODataRoutingConvention**の実装は次のことを行います。

1. パステンプレートを比較して、この規則が現在の要求に適用されるかどうかを確認します。 適用されない場合は、null を返します。
2. 規則が適用される場合は、 **ODataPathSegment**インスタンスのプロパティを使用して、コントローラー名とアクション名を取得します。
3. アクションの場合は、アクションパラメーター (通常はエンティティキー) にバインドする必要がある値をルートディクショナリに追加します。

具体的な例を見てみましょう。 組み込みのルーティング規則では、ナビゲーションコレクションへのインデックス作成はサポートされていません。 言い換えると、次のような Uri には規則がありません。

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

この種類のクエリを処理するカスタムルーティング規則を次に示します。

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

注:

1. **EntitySetRoutingConvention**から派生します。これは、そのクラスの**selectcontroller**メソッドがこの新しいルーティング規則に適しているためです。 これは、 **Selectcontroller**を再実装する必要がないことを意味します。
2. この規則は GET 要求のみに適用され、パステンプレートが&quot;&quot;場合にのみ適用されます。
3. アクション名は &quot;Get {EntityType}&quot;です。ここで、 *{entitytype}* はナビゲーションコレクションの種類です。 たとえば、GetSupplier&quot;&quot;ます。 コントローラーアクションが一致していることを&#8212;確認するだけで、任意の名前付け規則を使用できます。
4. このアクションでは、 *key*および関連性*キー*という名前の2つのパラメーターを受け取ります。 (定義済みのパラメーター名の一覧については、「 [Odatarouteconstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)」を参照してください)。

次の手順では、新しい規則をルーティング規則の一覧に追加します。 これは、次のコードに示すように、構成中に発生します。

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

調査に役立つその他のサンプルルーティング規則を次に示します。

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

もちろん、Web API 自体はオープンソースであるため、組み込みのルーティング規則の[ソースコード](http://aspnetwebstack.codeplex.com/)を確認できます。 これら**は、system.servicemodel**名前空間で定義されています。
