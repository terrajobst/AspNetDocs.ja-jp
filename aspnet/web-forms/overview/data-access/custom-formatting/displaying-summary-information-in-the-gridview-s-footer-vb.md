---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
title: GridView のフッターに概要情報を表示する (VB) |Microsoft Docs
author: rick-anderson
description: 概要情報は、多くの場合、概要行のレポートの下部に表示されます。 GridView コントロールには、pr できるセルのフッター行を含めることができます...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 41c818b7-603a-402b-8847-890a63547b6f
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: c208b4a756f5700be46eec924d8cf8f49b9d2507
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616510"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-vb"></a>GridView のフッターに概要情報を表示する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe)または[PDF のダウンロード](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)

> 概要情報は、多くの場合、概要行のレポートの下部に表示されます。 GridView コントロールには、プログラムを使用して集計データを挿入できるセルを持つフッター行を含めることができます。 このチュートリアルでは、このフッター行に集計データを表示する方法について説明します。

## <a name="introduction"></a>はじめに

ユーザーは、各製品の価格、在庫の単位、注文の数、および並べ替えレベルを確認するだけでなく、平均価格、在庫数の合計数などの集計情報に関心がある場合もあります。 このような概要情報は、多くの場合、概要行のレポートの下部に表示されます。 GridView コントロールには、プログラムを使用して集計データを挿入できるセルを持つフッター行を含めることができます。

このタスクでは、3つの課題があります。

1. フッター行を表示するように GridView を構成する
2. 概要データの決定つまり、在庫数の平均価格または合計を計算するにはどうすればよいでしょうか。
3. フッター行の適切なセルに概要データを挿入する

このチュートリアルでは、これらの課題を克服する方法を説明します。 具体的には、選択したカテゴリの製品が GridView に表示されているドロップダウンリストのカテゴリを一覧表示するページを作成します。 GridView には、そのカテゴリの製品について、在庫の平均価格と総単位数を示すフッター行が含まれます。

[![概要情報が GridView のフッター行に表示されます](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image1.png)

**図 1**: 概要情報が GridView のフッター行に表示される ([クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png)されます)

このチュートリアルでは、カテゴリを製品マスター/詳細インターフェイスと共に使用して、前の[マスター/詳細フィルター処理](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)で説明されている概念を DropDownList チュートリアルに基づいて作成します。 前のチュートリアルをまだ実行していない場合は、このチュートリアルを続行する前に行ってください。

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>手順 1: DropDownList と製品のカテゴリ GridView を追加する

GridView のフッターに概要情報を追加する前に、まずマスター/詳細レポートを作成してみましょう。 この最初の手順を完了したら、概要データを含める方法を見ていきます。

まず、`CustomFormatting` フォルダーの [`SummaryDataInFooter.aspx`] ページを開きます。 DropDownList コントロールを追加し、その `ID` を `Categories`に設定します。 次に、DropDownList のスマートタグから [データソースの選択] リンクをクリックし、`CategoriesBLL` クラスの `GetCategories()` メソッドを呼び出す `CategoriesDataSource` という名前の新しい ObjectDataSource を追加することを選択します。

[新しい ObjectDataSource という名前の新しい名前のデータソースを追加 ![には](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image4.png)

**図 2**: `CategoriesDataSource` という名前の新しい ObjectDataSource を追加[する (クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png)される)

[ObjectDataSource が GetCategories () メソッドを呼び出す ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image7.png)

**図 3**: ObjectDataSource に `CategoriesBLL` クラスの `GetCategories()` メソッドを呼び出す ([クリックしてフルサイズのイメージを表示する](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))

ObjectDataSource を構成した後、ウィザードは DropDownList のデータソース構成ウィザードに戻ります。ここで、表示するデータフィールドの値と、DropDownList の `ListItem` s の値に対応するデータフィールドの値を指定する必要があります。 `CategoryName` フィールドを表示し、`CategoryID` を値として使用します。

[ListItems のテキストと値として、[区分値] フィールドと [CategoryID] フィールドをそれぞれ使用 ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image10.png)

**図 4**: `CategoryName` フィールドと `CategoryID` フィールドをそれぞれ `ListItem` の `Text` および `Value` として使用する ([クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png)されます)

この時点で、システム内のカテゴリを一覧表示する DropDownList (`Categories`) があります。 次に、選択したカテゴリに属する製品を一覧表示する GridView を追加する必要があります。 ただし、その前に、DropDownList のスマートタグの [AutoPostBack を有効にする] チェックボックスをオンにします。 「 *Dropdownlist を使用したマスター/詳細のフィルター処理*」のチュートリアルで説明したように、dropdownlist の `AutoPostBack` プロパティをに設定すると、dropdownlist 値が変更されるたびにページがポストバックされ `True` ます。 これにより、GridView が更新され、新しく選択されたカテゴリの製品が表示されます。 `AutoPostBack` プロパティが `False` (既定値) に設定されている場合、カテゴリを変更してもポストバックは行われないため、表示されている製品は更新されません。

[DropDownList のスマートタグの [AutoPostBack を有効にする] チェックボックスをオンに ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image13.png)

**図 5**: DropDownList のスマートタグの [AutoPostBack を有効にする] チェックボックスをオン[にする (クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png)されます)

選択したカテゴリの製品を表示するために、GridView コントロールをページに追加します。 GridView の `ID` を `ProductsInCategory` に設定し、`ProductsInCategoryDataSource`という名前の新しい ObjectDataSource にバインドします。

[新しい ObjectDataSource という名前の ProductsInCategoryDataSource を追加 ![には](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image16.png)

**図 6**: `ProductsInCategoryDataSource` という名前の新しい ObjectDataSource を追加[する (クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png)される)

`ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドを呼び出すように ObjectDataSource を構成します。

[ObjectDataSource が Get$ Bycategoryid (categoryID) メソッドを呼び出す ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image19.png)

**図 7**: ObjectDataSource で `GetProductsByCategoryID(categoryID)` メソッドを呼び出す ([クリックしてフルサイズのイメージを表示する](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png))

`GetProductsByCategoryID(categoryID)` メソッドは入力パラメーターを受け取るため、ウィザードの最後の手順では、パラメーター値のソースを指定できます。 選択したカテゴリの製品を表示するには、パラメーターを `Categories` DropDownList からプルします。

[選択したカテゴリから categoryID パラメーター値を取得 ![には、DropDownList](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image22.png)

**図 8**: 選択したカテゴリの DropDownList から *`categoryID`* パラメーター値を取得[する (クリックしてフルサイズのイメージを表示する](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))

ウィザードを完了すると、GridView には各製品プロパティの BoundField が表示されます。 これらの連結フィールドをクリーンアップして、`ProductName`、`UnitPrice`、`UnitsInStock`、および `UnitsOnOrder` BoundFields のみが表示されるようにしてみましょう。 フィールドレベルの設定は、残りの BoundFields に自由に追加できます (`UnitPrice` を通貨として書式設定するなど)。 これらの変更を行った後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample1.aspx)]

この時点で、マスター/詳細レポートが完全に機能しており、選択したカテゴリに属する製品の名前、単価、在庫数、および単位が表示されます。

[選択したカテゴリから categoryID パラメーター値を取得 ![には、DropDownList](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image25.png)

**図 9**: 選択したカテゴリの DropDownList から *`categoryID`* パラメーター値を取得[する (クリックしてフルサイズのイメージを表示する](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>手順 2: GridView でのフッターの表示

GridView コントロールは、ヘッダーとフッターの両方の行を表示できます。 これらの行は、それぞれ `ShowHeader` の値と `ShowFooter` プロパティの値に応じて表示されます。 `ShowHeader` 既定では、`True` して `ShowFooter` に `False`します。 GridView にフッターを含めるには、単に `ShowFooter` プロパティを `True`に設定します。

[GridView の ShowFooter プロパティを True に設定 ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image28.png)

**図 10**: GridView の `ShowFooter` プロパティを `True` に設定する ([クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png)されます)

フッター行には、GridView で定義されている各フィールドのセルがあります。ただし、これらのセルは既定では空です。 ブラウザーで進行状況を確認してください。 `ShowFooter` プロパティが `True`に設定され、GridView に空のフッター行が含まれるようになりました。

[GridView にフッター行が含まれるようになった ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image31.png)

**図 11**: GridView にフッター行が含まれるようになりました ([クリックしてフルサイズの画像を表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png))

図11のフッター行は、白の背景を持つためにはありません。 濃い赤の背景を指定する `Styles.css` で `FooterStyle` CSS クラスを作成してから、この CSS クラスを GridView の `FooterStyle`の `CssClass` プロパティに割り当てるように `DataWebControls` テーマの `GridView.skin` スキンファイルを構成します。 スキンとテーマに対してブラシを作成する必要がある場合は、「ObjectDataSource チュートリアルを使用した[データの表示](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)」を参照してください。

まず、`Styles.css`に次の CSS クラスを追加します。

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample2.css)]

`FooterStyle` CSS クラスは `HeaderStyle` クラスとスタイルが似ていますが、`HeaderStyle`の背景色は濃い色であり、そのテキストは太字のフォントで表示されます。 さらに、フッター内のテキストは右揃えになり、ヘッダーのテキストは中央揃えになります。

次に、この CSS クラスをすべての GridView のフッターに関連付けるには、`DataWebControls` テーマで `GridView.skin` ファイルを開き、`FooterStyle`の `CssClass` プロパティを設定します。 この追加後、ファイルのマークアップは次のようになります。

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample3.aspx)]

次のスクリーンショットに示すように、この変更により、フッターがより明確になります。

[GridView のフッター行に Reddish の背景色が設定されている ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image34.png)

**図 12**: GridView のフッター行に Reddish の背景色が設定されている ([クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png)される)

## <a name="step-3-computing-the-summary-data"></a>手順 3: 概要データを計算する

GridView のフッターが表示されたら、次に、概要データを計算する方法について説明します。 この集計情報を計算するには、次の2つの方法があります。

1. SQL クエリを使用すると、データベースに対して追加のクエリを発行し、特定のカテゴリの概要データを計算できます。 SQL には、データを集約するデータを指定するために、`GROUP BY` 句と共に多数の集計関数が含まれています。 次の SQL クエリを実行すると、必要な情報が返されます。  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample4.sql)]

    もちろん、このクエリを `SummaryDataInFooter.aspx` ページから直接発行するのではなく、`ProductsTableAdapter` と `ProductsBLL`でメソッドを作成する必要があります。
2. 「[データに基づくカスタム書式](custom-formatting-based-upon-data-cs.md)設定」のチュートリアルで説明されているように、gridview に追加されるときにこの情報を計算します。 gridview の `RowDataBound` イベントハンドラーは、データバインドされた後に、gridview に追加される各行に対して1回発生します。 このイベントのイベントハンドラーを作成することによって、集計する値の累計を保持できます。 最後のデータ行が GridView にバインドされると、平均の計算に必要な合計と情報が得られます。

通常は、データベースへのトリップを保存し、データアクセス層とビジネスロジック層で概要機能を実装するために必要な作業を行うために、2番目のアプローチを採用しますが、どちらの方法でも十分です。 このチュートリアルでは、2番目のオプションを使用して、`RowDataBound` イベントハンドラーを使用して累計を追跡します。

デザイナーで GridView を選択し、プロパティウィンドウの [稲妻] アイコンをクリックして、[`RowDataBound`] イベントをダブルクリックして、GridView の `RowDataBound` イベントハンドラーを作成します。 または、ASP.NET 分離コードクラスファイルの上部にあるドロップダウンリストから GridView とその行データバインドイベントを選択することもできます。 これにより、`SummaryDataInFooter.aspx` ページの分離コードクラスに `ProductsInCategory_RowDataBound` という名前の新しいイベントハンドラーが作成されます。

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample5.vb)]

累計を維持するために、イベントハンドラーのスコープ外で変数を定義する必要があります。 次の4つのページレベル変数を作成します。

- `_totalUnitPrice`、型 `Decimal`
- `_totalNonNullUnitPriceCount`、型 `Integer`
- `_totalUnitsInStock`、型 `Integer`
- `_totalUnitsOnOrder`、型 `Integer`

次に、`RowDataBound` イベントハンドラーで検出された各データ行に対して、これら3つの変数をインクリメントするコードを記述します。

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample6.vb)]

`RowDataBound` イベントハンドラーは、まず DataRow を処理することから始めます。 この設定が完了すると、`e.Row` の `GridViewRow` オブジェクトにバインドされた `Northwind.ProductsRow` インスタンスは、変数 `product`に格納されます。 次に、実行中の合計変数は、現在の製品の対応する値によってインクリメントされます (データベース `NULL` 値が含まれていないことを前提としています)。 平均価格はこれら2つの数値の商であるため、実行中の `UnitPrice` 合計と非`NULL` `UnitPrice` レコードの数を追跡します。

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>手順 4: 概要データをフッターに表示する

概要データの合計が表示されたら、最後に GridView のフッター行に表示します。 このタスクも、`RowDataBound` イベントハンドラーを使用してプログラムで実行できます。 フッター行を含め、GridView にバインドされている*すべて*の行に対して、`RowDataBound` イベントハンドラーが起動されることを思い出してください。 したがって、次のコードを使用して、フッター行にデータを表示するようにイベントハンドラーを拡張できます。

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample7.vb)]

すべてのデータ行が追加された後に、フッター行が GridView に追加されるため、集計データをフッターに表示する準備が完了したことを確信することができます。 最後の手順として、フッターのセルにこれらの値を設定します。

特定のフッターセルにテキストを表示するには、`e.Row.Cells(index).Text = value`を使用します。この場合、`Cells` のインデックスは0から始まります。 次のコードでは、平均価格 (製品数で割った合計価格) を計算し、その GridView の適切なフッターセル内の在庫数および単位の合計数と共に表示します。

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample8.vb)]

図13は、このコードが追加された後のレポートを示しています。 `ToString("c")` によって、平均価格の概要情報が通貨のように書式設定されることに注意してください。

[GridView のフッター行に Reddish の背景色が設定されている ![](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image37.png)

**図 13**: GridView のフッター行に Reddish の背景色が設定されている ([クリックすると、フルサイズの画像が表示](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png)される)

## <a name="summary"></a>要約

概要データの表示は一般的なレポートの要件であり、GridView コントロールを使用すると、そのような情報をフッター行に簡単に含めることができます。 フッター行は、GridView の `ShowFooter` プロパティが `True` に設定されている場合に表示されます。また、`RowDataBound` イベントハンドラーを使用して、セル内のテキストをプログラムによって設定することもできます。 概要データを計算するには、データベースに対してクエリを再実行するか、ASP.NET ページの分離コードクラスのコードを使用して、概要データをプログラムで計算します。

このチュートリアルでは、GridView、DetailsView、および FormView コントロールを使用したカスタム書式設定の検証を終了します。 次のチュートリアルでは、これらの同じコントロールを使用したデータの挿入、更新、および削除についての調査を開始します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](using-the-formview-s-templates-vb.md)
