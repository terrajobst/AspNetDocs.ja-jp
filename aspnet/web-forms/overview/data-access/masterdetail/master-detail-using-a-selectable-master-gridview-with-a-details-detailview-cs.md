---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: 詳細詳細ビューを含む選択可能なマスター GridView を使用したC#マスター/詳細 () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、各製品の名前と価格を選択ボタンと共に含む行を含む GridView を使用します。 [選択] ボタンをクリックして
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: 04c427341f063729bd23b416a96f5acb20702792
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74632296"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>選択可能なマスター GridView と詳細 DetailView を使用してマスター/詳細を表示する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe)または[PDF のダウンロード](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> このチュートリアルでは、各製品の名前と価格を選択ボタンと共に含む行を含む GridView を使用します。 特定の製品の [選択] ボタンをクリックすると、完全な詳細が同じページの DetailsView コントロールに表示されます。

## <a name="introduction"></a>はじめに

前の[チュートリアル](master-detail-filtering-across-two-pages-cs.md)では、2つの web ページを使用してマスター/詳細レポートを作成する方法を説明しました。 "マスター" web ページには、サプライヤーの一覧が表示されています。また、選択した業者によって提供される製品の一覧を示す "詳細" web ページが表示されます。 この2ページのレポート形式は、1ページに縮小することができます。 このチュートリアルでは、各製品の名前と価格を選択ボタンと共に含む行を含む GridView を使用します。 特定の製品の [選択] ボタンをクリックすると、完全な詳細が同じページの DetailsView コントロールに表示されます。

[[選択] ボタンをクリック ![と、製品の詳細が表示されます](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**図 1**: [選択] ボタンをクリックすると、製品の詳細が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png)されます)

## <a name="step-1-creating-a-selectable-gridview"></a>手順 1: 選択可能な GridView の作成

2ページのマスター/詳細レポートで、各マスターレコードにハイパーリンクが含まれていることを思い出してください。クリックすると、クリックした行の `SupplierID` 値がクエリ文字列に渡され、詳細ページにユーザーが送信されます。 このようなハイパーリンクは、ハイパーリンクフィールドを使用して各 GridView 行に追加されています。 1ページのマスター/詳細レポートでは、クリックすると詳細が表示される各 GridView 行に対してボタンが必要になります。 GridView コントロールは、ポストバックの原因となった行ごとに Select ボタンを含めて、その行を GridView の[Selectedrow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)としてマークするように構成できます。

まず、GridView コントロールを `Filtering` フォルダーの `DetailsBySelecting.aspx` ページに追加し、その `ID` プロパティを `ProductsGrid`に設定します。 次に、`ProductsBLL` クラスの `GetProducts()` メソッドを呼び出す `AllProductsDataSource` という名前の新しい ObjectDataSource を追加します。

[![、All$ Datasource という名前の ObjectDataSource を作成する](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**図 2**: `AllProductsDataSource` という名前の ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png)されます)

[製品の Bll クラスを使用 ![には](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**図 3**: `ProductsBLL` クラスを使用[する (クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png)されます)

[GetProducts () メソッドを呼び出すように ObjectDataSource を構成 ![には](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**図 4**: `GetProducts()` メソッドを呼び出すように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))

GridView のフィールドを編集し、`ProductName` フィールドと `UnitPrice` BoundFields 以外はすべて削除します。 また、`UnitPrice` BoundField を通貨として書式設定したり、BoundFields の `HeaderText` プロパティを変更したりするなど、必要に応じてこれらの BoundFields を自由にカスタマイズできます。 これらの手順は、GridView のスマートタグから [列の編集] リンクをクリックするか、宣言型の構文を手動で構成することによって、グラフィカルに行うことができます。

[ProductName フィールドと UnitPrice BoundFields 以外のすべてのフィールドを削除 ![には](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**図 5**: `ProductName` フィールドと `UnitPrice` boundfields 以外のすべてを削除[する (クリックしてフルサイズのイメージを表示する](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))

GridView の最終的なマークアップは次のとおりです。

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

次に、GridView を選択可能としてマークする必要があります。これにより、各行に Select ボタンが追加されます。 これを実現するには、GridView のスマートタグの [選択を有効にする] チェックボックスをオンにします。

[GridView の行を選択可能にする ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**図 6**: GridView の行を選択可能[にする (クリックすると、フルサイズのイメージが表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png)されます)

[選択範囲の有効化] オプションをオンにすると、`ShowSelectButton` プロパティが True に設定された `ProductsGrid` GridView に CommandField が追加されます。 この結果、図6に示すように、GridView の行ごとに [選択] ボタンが表示されます。 既定では、[選択] ボタンはリンクボタンとして表示されますが、CommandField の `ButtonType` プロパティではなく、ボタンまたは ImageButtons を使用できます。

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

GridView 行の Select ボタンがポストバック ensues をクリックすると、GridView の `SelectedRow` プロパティが更新されます。 GridView には、`SelectedRow` プロパティに加えて、 [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx)、 [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)、 [selecteddatakey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx)の各プロパティが用意されています。 `SelectedIndex` プロパティは、選択された行のインデックスを返します。一方、`SelectedValue` プロパティと `SelectedDataKey` プロパティは、GridView の[いる datakeynames プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)に基づいて値を返します。

`DataKeyNames` プロパティは、1つまたは複数のデータフィールドの値を各行に関連付けるために使用され、一般的には、基になるデータから各 GridView 行の情報を一意に識別するために使用されます。 `SelectedValue` プロパティは、選択された行の最初の `DataKeyNames` データフィールドの値を返します。ここで、`SelectedDataKey` プロパティは選択された行の `DataKey` オブジェクトを返します。このオブジェクトには、その行の指定されたデータキーフィールドのすべての値が含まれます。

デザイナーを使用してデータソースを GridView、DetailsView、または FormView にバインドすると、[`DataKeyNames`] プロパティが自動的に一意に識別されるデータフィールドに設定されます。 このプロパティは、前のチュートリアルで自動的に設定されていますが、この例では、`DataKeyNames` プロパティが指定されていない状態で動作しています。 ただし、このチュートリアルで選択可能な GridView に加えて、挿入、更新、および削除を確認する今後のチュートリアルについては、`DataKeyNames` プロパティを適切に設定する必要があります。 GridView の `DataKeyNames` プロパティが `ProductID`に設定されていることを確認します。

ブラウザーを通じてこれまでの進行状況を見てみましょう。 GridView には、すべての製品の名前と価格が、Select LinkButton と共に表示されることに注意してください。 [選択] ボタンをクリックすると、ポストバックが発生します。 手順 2. では、選択した製品の詳細を表示して、このポストバックに対して DetailsView を応答させる方法について説明します。

[各製品行に Select LinkButton が含まれて ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**図 7**: 各製品行に Select LinkButton が含まれている ([クリックしてフルサイズの画像を表示する](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png))

### <a name="highlighting-the-selected-row"></a>選択された行の強調表示

`ProductsGrid` GridView には、選択した行の視覚スタイルを指定するために使用できる `SelectedRowStyle` プロパティがあります。 適切に使用すると、現在選択されている GridView の行をより明確に表示することで、ユーザーのエクスペリエンスを向上させることができます。 このチュートリアルでは、選択した行を黄色の背景で強調表示してみましょう。

前のチュートリアルと同様に、見た目に関連する設定を CSS クラスとして定義したままにしておきましょう。 したがって、`Styles.css` `SelectedRowStyle`という名前の新しい CSS クラスを作成します。

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

この CSS クラスをチュートリアルシリーズの*すべて*の gridviews の `SelectedRowStyle` プロパティに適用するには、`DataWebControls` テーマの `GridView.skin` スキンを編集して、次のように `SelectedRowStyle` 設定を含めます。

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

この追加により、選択した GridView 行が黄色の背景色で強調表示されるようになりました。

[GridView の SelectedRowStyle プロパティを使用して、選択した行の外観をカスタマイズ ![には](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**図 8**: GridView の `SelectedRowStyle` プロパティを使用して、選択した行の外観をカスタマイズ[する (クリックしてフルサイズのイメージを表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>手順 2: 選択した製品の詳細を DetailsView に表示する

GridView の `ProductsGrid` が完了したら、選択した特定の製品に関する情報を表示する DetailsView を追加します。 GridView の上に DetailsView コントロールを追加し、`ProductDetailsDataSource`という名前の新しい ObjectDataSource を作成します。 この DetailsView で、選択した製品に関する特定の情報が表示されるようにするため、`ProductsBLL` クラスの `GetProductByProductID(productID)` メソッドを使用するように `ProductDetailsDataSource` を構成します。

[Productbll クラスの GetProductByProductID (productID) メソッドを呼び出す ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**図 9**: `ProductsBLL` クラスの `GetProductByProductID(productID)` メソッドを呼び出す ([クリックしてフルサイズのイメージを表示する](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))

GridView コントロールの `SelectedValue` プロパティから取得した *`productID`* パラメーターの値を取得します。 前に説明したように、GridView の `SelectedValue` プロパティは、選択された行の最初のデータキー値を返します。 そのため、選択した行の `ProductID` 値が `SelectedValue`によって返されるように、GridView の `DataKeyNames` プロパティを `ProductID`に設定する必要があります。

[productID パラメーターを GridView の SelectedValue プロパティに設定 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**図 10**: *`productID`* パラメーターを GridView の `SelectedValue` プロパティに設定する ([クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png)されます)

`productDetailsDataSource` ObjectDataSource が正しく構成され、DetailsView にバインドされると、このチュートリアルは完了です。 ページに最初にアクセスしたときに行が選択されていないため、GridView の `SelectedValue` プロパティは `null`を返します。 `NULL` `ProductID` 値を持つ製品は存在しないため、`GetProductByProductID(productID)` メソッドによってレコードが返されることはありません。これは、DetailsView が表示されないことを意味します (図11を参照)。 GridView 行の Select ボタンをクリックすると、ポストバック ensues と DetailsView が更新されます。 このとき、GridView の `SelectedValue` プロパティは選択された行の `ProductID` を返し、`GetProductByProductID(productID)` メソッドはその特定の製品に関する情報を含む `ProductsDataTable` を返し、DetailsView にこれらの詳細を表示します (図12を参照)。

[![最初にアクセスしたときに、GridView のみが表示されます。](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**図 11**: 最初にアクセスしたときに GridView のみが表示される ([クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png)されます)

[行を選択すると、製品の詳細が表示され ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**図 12**: 行を選択すると、製品の詳細が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png)されます)

## <a name="summary"></a>要約

この3つのチュートリアルでは、マスター/詳細レポートを表示するためのいくつかの手法について説明しました。 このチュートリアルでは、選択可能な GridView を使用してマスターレコードを格納し、DetailsView を使用して、選択したマスターレコードの詳細を同じページに表示します。 前のチュートリアルでは、DropDownLists を使用してマスター/詳細レポートを表示する方法と、1つの web ページにマスターレコードを表示する方法と、別の web ページで詳細レコードを表示する方法を説明しました。

このチュートリアルでは、マスター/詳細レポートの検査について説明します。 次のチュートリアルでは、GridView、DetailsView、および FormView を使用したカスタマイズされた書式設定の探索を開始します。 これらのコントロールの外観は、バインドされたデータに基づいてカスタマイズする方法、GridView のフッターにデータを要約する方法、およびテンプレートを使用してレイアウトをより細かく制御する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-filtering-across-two-pages-cs.md)
> [次へ](master-detail-filtering-with-a-dropdownlist-vb.md)
