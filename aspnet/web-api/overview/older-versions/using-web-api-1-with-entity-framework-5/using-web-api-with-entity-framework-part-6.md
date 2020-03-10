---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 'パート 6: 製品および注文のコントローラーの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421288"
---
# <a name="part-6-creating-product-and-order-controllers"></a>パート 6: 製品および注文コントローラーの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>製品コントローラーを追加する

管理コントローラーは、管理者特権を持つユーザーのためのものです。 一方、顧客は製品を表示できますが、作成、更新、または削除することはできません。

Get メソッドを開いたままにして、Post、Put、Delete の各メソッドへのアクセスを簡単に制限することができます。 しかし、製品に関して返されるデータを見てみましょう。

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

`ActualCost` のプロパティは、お客様に表示されません。 この問題を解決するには、ユーザーに表示する必要があるプロパティのサブセットを含む*データ転送オブジェクト*(DTO) を定義します。 ここでは、LINQ を使用してインスタンスを `ProductDTO` `Product` インスタンスを射影します。

`ProductDTO` という名前のクラスを [モデル] フォルダーに追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

次に、コントローラーを追加します。 ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。 **[追加]** を選択し、 **[コントローラー]** を選択します。 **[コントローラーの追加]** ダイアログボックスで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。 **[テンプレート]** で **[空の API コントローラー]** を選択します。

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

ソースファイル内のすべてのものを次のコードに置き換えます。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

コントローラーは引き続き `OrdersContext` を使用してデータベースを照会します。 ただし、`Product` インスタンスを直接返すのではなく、`MapProducts` を呼び出して `ProductDTO` インスタンスに射影します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts` メソッドは**IQueryable**を返します。そのため、他のクエリパラメーターを使用して結果を構成できます。 これは、 **where**句をクエリに追加する `GetProduct` メソッドで確認できます。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>Orders コントローラーを追加する

次に、ユーザーが注文を作成および表示できるようにするコントローラーを追加します。

まず、別の DTO を使用します。 ソリューションエクスプローラーで、[モデル] フォルダーを右クリックし、次の実装を使用して `OrderDTO` という名前のクラスを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

次に、コントローラーを追加します。 ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。 **[追加]** を選択し、 **[コントローラー]** を選択します。 **[コントローラーの追加]** ダイアログで、次のオプションを設定します。

- **[コントローラー名]** に「OrdersController」と入力します。
- **テンプレート** で、Entity Framework を使用した、読み取り/書き込みアクションがある API コントローラー を選択します。
- **モデルクラス** で、&quot;の順序 (Productstore. モデル)&quot;を選択します。
- **[データコンテキストクラス]** で、[&quot;OrdersContext (Productstore. モデル)&quot;] を選択します。

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

**[追加]** をクリックします。 これにより、OrdersController.cs という名前のファイルが追加されます。 次に、コントローラーの既定の実装を変更する必要があります。

最初に、`PutOrder` および `DeleteOrder` メソッドを削除します。 このサンプルでは、顧客が既存の注文を変更または削除することはできません。 実際のアプリケーションでは、これらのケースを処理するために多くのバックエンドロジックが必要になります。 (たとえば、注文は既に発送されていますか)。

ユーザーに属する注文だけを返すように `GetOrders` メソッドを変更します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

`GetOrder` メソッドを次のように変更します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

メソッドに加えられた変更を次に示します。

- 戻り値は、`Order`ではなく、`OrderDTO` インスタンスです。
- データベースに対して注文のクエリを実行する場合は、 [Dbquery. Include](https://msdn.microsoft.com/library/gg696395)メソッドを使用して、関連する `OrderDetail` および `Product` エンティティをフェッチします。
- 射影を使用して結果を平坦化します。

HTTP 応答には、数量を含む製品の配列が含まれます。

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

この形式は、クライアントが、入れ子になったエンティティ (順序、詳細、および製品) を含む元のオブジェクトグラフよりも簡単に使用できます。

`PostOrder`を考慮する最後のメソッド。 現時点では、このメソッドは `Order` インスタンスを受け取ります。 しかし、クライアントが次のような要求本文を送信した場合はどうなるかを検討してください。

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

これは適切に構成された順序であり、Entity Framework によってデータベースに挿入されます。 ただし、これには以前に存在していなかった製品エンティティが含まれています。 クライアントは、データベースに新しい製品を作成しました。 これは、注文調達部門に対して、お客様が注文を受けたときに驚くようになります。 教訓は、POST または PUT 要求で受け入れられるデータについて慎重に検討することです。

この問題を回避するには、`OrderDTO` インスタンスを取得するように `PostOrder` メソッドを変更します。 `Order`を作成するには、`OrderDTO` を使用します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

`ProductID` と `Quantity` のプロパティを使用し、クライアントが製品名または価格に対して送信した値は無視されることに注意してください。 製品 ID が有効でない場合は、データベース内の foreign key 制約に違反するため、挿入は失敗します。

`PostOrder` の完全な方法を次に示します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

最後に、**承認**属性をコントローラーに追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

登録済みのユーザーのみが注文を作成または表示できるようになりました。

> [!div class="step-by-step"]
> [前へ](using-web-api-with-entity-framework-part-5.md)
> [次へ](using-web-api-with-entity-framework-part-7.md)
