---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 'パート 7: メインページを作成する |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484450"
---
# <a name="part-7-creating-the-main-page"></a>パート 7: メインページの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>メイン ページの作成

このセクションでは、メインアプリケーションページを作成します。 このページは管理者ページより複雑になるため、いくつかの手順でアプローチします。 その過程で、いくつかの高度なノックアウト手法について説明します。 次に、ページの基本的なレイアウトを示します。

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "Products" は、製品の配列を保持します。
- "カート" は、数量を持つ製品の配列を保持します。 [カートに追加] をクリックすると、カートが更新されます。
- "Orders" は、注文 Id の配列を保持します。
- "詳細" は、商品の配列である注文明細 (数量を含む製品) を保持します。

まず、データバインドまたはスクリプトを使用せずに、HTML でいくつかの基本的なレイアウトを定義します。 Views/Home/Index を開き、すべての内容を次の内容に置き換えます。

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

次に、Scripts セクションを追加し、空のビューモデルを作成します。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

前の設計に基づいて、ビューモデルでは、製品、カート、注文、および詳細の observable が必要です。 `AppViewModel` オブジェクトに次の変数を追加します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

ユーザーは、製品リストからカートに商品を追加したり、カートから品目を削除したりできます。 これらの関数をカプセル化するには、製品を表すビューモデルクラスをもう1つ作成します。 `AppViewModel` に次のコードを追加します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` クラスには、カートに製品を移動するために使用する2つの関数が含まれています。 `addItemToCart` 製品の1つの単位をカートに追加し、`removeAllFromCart` 製品のすべての数量を削除します。

ユーザーは、既存の注文を選択して注文の詳細を取得できます。 この機能を別のビューモデルにカプセル化します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` は順序を使用して初期化され、サーバーに AJAX 要求を送信して注文の詳細をフェッチします。

また、`OrderDetailsViewModel`の `total` プロパティにも注目してください。 このプロパティは、計算された[観測](http://knockoutjs.com/documentation/computedObservables.html)可能なと呼ばれる特別な種類の観測可能なオブジェクトです。 この名前が示すように、計算された観測可能なデータを&#8212;使用して、この場合は、注文の合計コストを計算値にバインドします。

次に、次の関数を `AppViewModel`に追加します。

- `resetCart` カートからすべての項目を削除します。
- `getDetails` は、新しい `OrderDetailsViewModel` を `details` の一覧にプッシュすることによって、注文の詳細を取得します。
- `createOrder` によって新しい注文が作成され、カートが空になります。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

最後に、製品および注文に対して AJAX 要求を行うことで、ビューモデルを初期化します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

そうですね。コードは非常に簡単ですが、ステップバイステップで構築しましたので、設計は明確であることをお勧めします。 これで、いくつかのノックアウトバインドを HTML に追加できるようになりました。

**成果物**

製品リストのバインドは次のとおりです。

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

Products 配列に対して反復処理を行い、名前と価格を表示します。 [順序の追加] ボタンは、ユーザーがログインしている場合にのみ表示されます。

[順序の追加] ボタンをクリックすると、製品の `ProductViewModel` インスタンスで `addItemToCart` が呼び出されます。 これは、ノックアウトの便利な機能を示しています。ビューモデルに他のビューモデルが含まれている場合は、そのバインドを内部モデルに適用できます。 この例では、`foreach` 内のバインドが `ProductViewModel` の各インスタンスに適用されます。 この方法は、すべての機能を1つのビューモデルに配置するよりも、はるかにすっきりしています。

**カート**

カートのバインドは次のとおりです。

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

これにより、カート配列を反復処理し、名前、価格、および数量を表示します。 [削除] リンクと [注文の作成] ボタンがビューモデル関数にバインドされていることに注意してください。

**Orders (注文)**

Orders リストのバインドを次に示します。

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

注文を反復処理し、注文 ID を表示します。 リンク上の click イベントは、`getDetails` 関数にバインドされています。

**注文の詳細**

次に、注文の詳細のバインドを示します。

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

これにより、注文の項目を反復処理し、製品、価格、および数量を表示します。 周囲の div は、details 配列に1つ以上の項目が含まれている場合にのみ表示されます。

## <a name="conclusion"></a>まとめ

このチュートリアルでは、Entity Framework を使用してデータベースと通信するアプリケーションを作成し、データ層の上に公開インターフェイスを提供するように ASP.NET Web API しました。 ASP.NET MVC 4 を使用して HTML ページをレンダリングします。また、ページを再読み込みせずに動的な対話を行うために、ノックアウトと jQuery を組み合わせて使用します。

その他のリソース:

- [ASP.NET データアクセスコンテンツマップ](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework デベロッパーセンター](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [[戻る]](using-web-api-with-entity-framework-part-6.md)
