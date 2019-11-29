---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
title: DetailsView コントロールで TemplateFields を使用するC#() |Microsoft Docs
author: rick-anderson
description: GridView で使用できるのと同じ TemplateFields 機能も、DetailsView コントロールで使用できます。 このチュートリアルでは、1つの製品を表示します...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 83efb21f-b231-446e-9356-f4c6cbcc6713
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 55c667800a9fb19d200bcf4b68e2c59ca4ef5d0e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622234"
---
# <a name="using-templatefields-in-the-detailsview-control-c"></a>DetailsView コントロールで TemplateFields を使用する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_13_CS.exe)または[PDF のダウンロード](using-templatefields-in-the-detailsview-control-cs/_static/datatutorial13cs1.pdf)

> GridView で使用できるのと同じ TemplateFields 機能も、DetailsView コントロールで使用できます。 このチュートリアルでは、TemplateFields を含む DetailsView を使用して、一度に1つの製品を表示します。

## <a name="introduction"></a>はじめに

TemplateField は、BoundField、CheckBoxField、ハイパーリンクフィールド、およびその他のデータフィールドコントロールよりも高い柔軟性を備えています。 前の[チュートリアル](using-templatefields-in-the-gridview-control-cs.md)では、GridView で TemplateField を使用して次のことを確認しました。

- 複数のデータフィールド値を1つの列に表示します。 具体的には、`FirstName` と `LastName` の両方のフィールドが1つの GridView 列に結合されていました。
- 代替 Web コントロールを使用して、データフィールド値を表します。 カレンダーコントロールを使用して `HiredDate` の値を表示する方法について説明しました。
- 基になるデータに基づいてステータス情報を表示します。 `Employees` テーブルには、従業員がジョブに対して行った日数を返す列が含まれていませんが、TemplateField と書式指定メソッドを使用して、前のチュートリアルの GridView の例にそのような情報を表示できました。

GridView で使用できるのと同じ TemplateFields 機能も、DetailsView コントロールで使用できます。 このチュートリアルでは、2つの TemplateFields を含む DetailsView を使用して、一度に1つの製品を表示します。 最初の TemplateField は、`UnitPrice`、`UnitsInStock`、および `UnitsOnOrder` データフィールドを1つの DetailsView 行に結合します。 2番目の TemplateField には `Discontinued` フィールドの値が表示されますが、`Discontinued` が `true`の場合は "YES"、それ以外の場合は "NO" が表示されます。

[![2 つの TemplateFields を使用して、表示をカスタマイズします。](using-templatefields-in-the-detailsview-control-cs/_static/image2.png)](using-templatefields-in-the-detailsview-control-cs/_static/image1.png)

**図 1**: 2 つの Templatefields を使用してディスプレイをカスタマイズする ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image3.png)されます)

では、始めましょう。

## <a name="step-1-binding-the-data-to-the-detailsview"></a>手順 1: データを DetailsView にバインドする

前のチュートリアルで説明したように、TemplateFields を使用する場合は、通常、連結されたフィールドのみを含む DetailsView コントロールを作成し、次に新しい TemplateFields を追加するか、必要に応じて既存の BoundFields を TemplateFields に変換することから始めるのが最も簡単です. そのため、このチュートリアルを開始するには、デザイナーでページに DetailsView を追加し、製品の一覧を返す ObjectDataSource にバインドします。 これらの手順では、各製品の非ブール値フィールドに対して BoundFields を使用して DetailsView を作成し、1つのブール値フィールドに対して CheckBoxField を作成します (廃止されました)。

[`DetailsViewTemplateField.aspx`] ページを開き、[ツールボックス] から [DetailsView] をデザイナーにドラッグします。 DetailsView のスマートタグから、`ProductsBLL` クラスの `GetProducts()` メソッドを呼び出す新しい ObjectDataSource コントロールを追加することを選択します。

[GetProducts () メソッドを呼び出す新しい ObjectDataSource コントロールを追加 ![には](using-templatefields-in-the-detailsview-control-cs/_static/image5.png)](using-templatefields-in-the-detailsview-control-cs/_static/image4.png)

**図 2**: `GetProducts()` メソッドを呼び出す新しい ObjectDataSource コントロールを追加する ([クリックしてフルサイズのイメージを表示する](using-templatefields-in-the-detailsview-control-cs/_static/image6.png))

このレポートでは、`ProductID`、`SupplierID`、`CategoryID`、および `ReorderLevel` BoundFields を削除します。 次に、BoundFields の順序を変更して、`ProductName` BoundField の直後に `CategoryName` および `SupplierName` BoundFields が表示されるようにします。 必要に応じて、連結フィールドの `HeaderText` プロパティと書式設定プロパティを自由に調整してください。 GridView の場合と同様に、これらの BoundField レベルの編集は、[フィールド] ダイアログボックス (DetailsView のスマートタグの [フィールドの編集] リンクをクリックすることによって、または宣言型の構文を使用して実行できます) で実行できます。 最後に、DetailsView の `Height` をオフにし、表示されるデータに基づいて DetailsView コントロールを拡張できるようにプロパティ値を `Width` して、スマートタグの [ページングを有効にする] チェックボックスをオンにします。

これらの変更を行った後、DetailsView コントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample1.aspx)]

ブラウザーでページを表示してみましょう。 この時点で、製品の名前、カテゴリ、仕入先、価格、在庫のユニット、注文の単位、および廃止された状態を示す行を含む単一の製品 (Chai) が表示されます。

[製品の詳細 ![、一連の連結フィールドを使用して表示されます。](using-templatefields-in-the-detailsview-control-cs/_static/image8.png)](using-templatefields-in-the-detailsview-control-cs/_static/image7.png)

**図 3**: 製品の詳細は、一連の Boundfields を使用して表示されます ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image9.png)されます)

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>手順 2: 価格、在庫数、および単位数を1行に結合する

DetailsView には、`UnitPrice`、`UnitsInStock`、および `UnitsOnOrder` フィールドの行があります。 新しい TemplateField を追加するか、既存の `UnitPrice`、`UnitsInStock`、および `UnitsOnOrder` BoundFields の1つを TemplateField に変換することによって、これらのデータフィールドを1つの行に結合できます。 既存の連結フィールドを変換することをお勧めしますが、新しい TemplateField を追加してみましょう。

まず、DetailsView のスマートタグの [フィールドの編集] リンクをクリックして、[フィールド] ダイアログボックスを表示します。 次に、新しい TemplateField を追加し、その `HeaderText` プロパティを "Price and Inventory" に設定し、`UnitPrice` BoundField の上に配置されるように新しい TemplateField を移動します。

[DetailsView コントロールに新しい TemplateField を追加 ![には](using-templatefields-in-the-detailsview-control-cs/_static/image11.png)](using-templatefields-in-the-detailsview-control-cs/_static/image10.png)

**図 4**: DetailsView コントロールに新しい TemplateField を追加する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image12.png)されます)

この新しい TemplateField には、`UnitPrice`、`UnitsInStock`、および `UnitsOnOrder` BoundFields に現在表示されている値が含まれているため、それらを削除してみましょう。

この手順の最後の作業は、Price および Inventory TemplateField のマークアップを `ItemTemplate` 定義することです。これは、デザイナーの DetailsView のテンプレート編集インターフェイスを使用するか、コントロールの宣言構文を使用して手動で行うことができます。 GridView の場合と同様に、DetailsView のテンプレート編集インターフェイスにアクセスするには、スマートタグの [テンプレートの編集] リンクをクリックします。 ここでは、ドロップダウンリストから編集するテンプレートを選択し、ツールボックスから任意の Web コントロールを追加できます。

このチュートリアルでは、まず Price および Inventory TemplateField の `ItemTemplate`にラベルコントロールを追加します。 次に、[ラベル] Web コントロールのスマートタグから [連結の編集] リンクをクリックし、[`Text`] プロパティを [`UnitPrice`] フィールドにバインドします。

[ラベルの Text プロパティを UnitPrice データフィールドにバインド ![には](using-templatefields-in-the-detailsview-control-cs/_static/image14.png)](using-templatefields-in-the-detailsview-control-cs/_static/image13.png)

**図 5**: ラベルの `Text` プロパティを `UnitPrice` データフィールドにバインドする ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image15.png)されます)

## <a name="formatting-the-price-as-a-currency"></a>価格を通貨として書式設定する

この追加により、[Web コントロール価格] と [在庫 TemplateField] というラベルに、選択した製品の価格のみが表示されるようになります。 図6は、ブラウザーを通じて表示されるときの、これまでの進行状況を示すスクリーンショットを示しています。

[価格と在庫 TemplateField の ![価格が表示されます](using-templatefields-in-the-detailsview-control-cs/_static/image17.png)](using-templatefields-in-the-detailsview-control-cs/_static/image16.png)

**図 6**: Price And Inventory TemplateField に価格が表示される ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image18.png)されます)

製品の価格が通貨として書式設定されていないことに注意してください。 BoundField を使用すると、`HtmlEncode` プロパティを `false` に設定し、`DataFormatString` プロパティを `{0:formatSpecifier}`に設定することにより、書式設定を行うことができます。 ただし、TemplateField の場合は、データバインド構文で書式設定命令を指定するか、アプリケーションのコード内で定義されている書式指定メソッド (ASP.NET ページの分離コードクラスなど) を使用する必要があります。

ラベル Web コントロールで使用されるデータバインド構文の書式を指定するには、ラベルのスマートタグから [データバインディングの編集] リンクをクリックして、[データ連結] ダイアログボックスに戻ります。 書式設定の手順は、[形式] ボックスの一覧に直接入力するか、定義されている書式指定文字列の1つを選択します。 BoundField の `DataFormatString` プロパティと同様に、書式設定は `{0:formatSpecifier}`を使用して指定します。

[`UnitPrice`] フィールドでは、適切なドロップダウンリストの値を選択するか、`{0:C}` 入力して、指定された通貨の書式を使用します。

[価格を通貨として書式設定 ![](using-templatefields-in-the-detailsview-control-cs/_static/image20.png)](using-templatefields-in-the-detailsview-control-cs/_static/image19.png)

**図 7**: 価格を通貨として書式設定[する (クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image21.png)されます)

宣言的には、書式設定の指定は、`Bind` または `Eval` メソッドに2番目のパラメーターとして示されます。 デザイナーを使用して行った設定は、宣言型マークアップ内の次のデータバインド式になります。

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>残りのデータフィールドを TemplateField に追加する

この時点で、Price and Inventory TemplateField に `UnitPrice` データフィールドが表示され、書式設定されましたが、`UnitsInStock` と `UnitsOnOrder` のフィールドを表示する必要があります。 価格とかっこ内の行にこれらを表示してみましょう。 デザイナーのテンプレート編集インターフェイスから、このようなマークアップを追加するには、テンプレート内にカーソルを置き、表示されるテキストを入力するだけです。 または、このマークアップを宣言構文に直接入力することもできます。

次のような価格と在庫の TemplateField が表示されるように、静的マークアップ、ラベル Web コントロール、およびデータバインド構文を追加します。

*UnitPrice*  
(**在庫/発注日:** *在庫 / * *UnitsOnOrder*)

このタスクを実行すると、DetailsView の宣言型マークアップは次のようになります。

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample3.aspx)]

これらの変更により、価格および在庫情報が1つの DetailsView 行に統合されました。

[価格および在庫情報が1行に表示される ![](using-templatefields-in-the-detailsview-control-cs/_static/image23.png)](using-templatefields-in-the-detailsview-control-cs/_static/image22.png)

**図 8**: 価格および在庫情報が1行に表示される ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image24.png)されます)

## <a name="step-3-customizing-the-discontinued-field-information"></a>手順 3: 廃止されたフィールド情報のカスタマイズ

`Products` テーブルの `Discontinued` 列は、製品が廃止されたかどうかを示すビット値です。 DetailsView (または GridView) をデータソースコントロールにバインドする場合、`Discontinued`のようなブール値フィールドは CheckBoxFields として実装され、`ProductID`、`ProductName`などの非ブール値フィールドは BoundFields として実装されます。 CheckBoxField は無効なチェックボックスとして表示され、データフィールドの値が True であるかどうかがチェックされます。それ以外の場合はオフになります。

CheckBoxField を表示するのではなく、製品が廃止されたかどうかを示すテキストを表示することが必要になる場合があります。 これを実現するには、DetailsView から CheckBoxField を削除し、`DataField` プロパティが `Discontinued`に設定されている BoundField を追加します。 少し時間を取ってください。 この変更を行った後、DetailsView は、廃止された製品の場合は "True"、まだアクティブな製品の場合は "False" と表示されます。

["True" と "False" の文字列を ![して、廃止された状態を表示します。](using-templatefields-in-the-detailsview-control-cs/_static/image26.png)](using-templatefields-in-the-detailsview-control-cs/_static/image25.png)

**図 9**: "True" と "False" という文字列を使用して、廃止された状態を表示する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image27.png)されます)

文字列 "True" または "False" を使用する必要がないとします。ただし、代わりに "YES" と "NO" を使用します。 このようなカスタマイズは、TemplateField と書式設定の方法を使用して実行できます。 書式指定メソッドは、任意の数の入力パラメーターを受け取ることができますが、テンプレートに挿入する HTML を (文字列として) 返す必要があります。

入力パラメーターとしてブール値を受け取り、文字列を返す `DisplayDiscontinuedAsYESorNO` という名前の `DetailsViewTemplateField.aspx` ページの分離コードクラスに書式指定メソッドを追加します。 前のチュートリアルで説明したように、テンプレートからアクセスできるようにするには、このメソッドを `protected` または `public` としてマークする*必要があり*ます。

[!code-csharp[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample4.cs)]

このメソッドは、入力パラメーター (`discontinued`) を確認し、`true`の場合は "YES" を返します。それ以外の場合は "NO" を返します。

> [!NOTE]
> 前のチュートリアルで検証した書式設定メソッドでは、`NULL` s を含む可能性のあるデータフィールドを渡していたため、`EmployeesRow`の `HiredDate` プロパティにアクセスする前に、従業員の `HiredDate` プロパティ値にデータベース `NULL` 値があるかどうかを確認する必要がありました。 ここでは、このようなチェックは必要ありません。 `Discontinued` 列にはデータベース `NULL` 値が割り当てられないためです。 さらに、このメソッドは、`ProductsRow` のインスタンスまたは `object`型のパラメーターを受け入れるのではなく、ブール型の入力パラメーターを受け取ることができます。

この書式指定メソッドが完了すると、TemplateField の `ItemTemplate`から呼び出すだけです。 TemplateField を作成するには、`Discontinued` BoundField を削除し、新しい TemplateField を追加するか、または `Discontinued` BoundField を TemplateField に変換します。 次に、宣言型マークアップビューで、TemplateField を編集して、`DisplayDiscontinuedAsYESorNO` メソッドを呼び出し、現在の `ProductRow` インスタンスの `Discontinued` プロパティの値を渡して、ItemTemplate だけが含まれるようにします。 これには、`Eval` メソッドを使用してアクセスできます。 具体的には、TemplateField のマークアップは次のようになります。

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample5.aspx)]

これにより、DetailsView をレンダリングするときに `DisplayDiscontinuedAsYESorNO` メソッドが呼び出され、`ProductRow` インスタンスの `Discontinued` 値が渡されます。 `Eval` メソッドは型 `object`の値を返しますが、`DisplayDiscontinuedAsYESorNO` メソッドは `bool`型の入力パラメーターを必要とするため、`Eval` メソッドの戻り値を `bool`にキャストします。 `DisplayDiscontinuedAsYESorNO` メソッドは、受け取った値に応じて "YES" または "NO" を返します。 返される値は、この DetailsView 行に表示される値です (図10を参照)。

[![YES または NO の値が廃止された行に表示されるようになりました](using-templatefields-in-the-detailsview-control-cs/_static/image29.png)](using-templatefields-in-the-detailsview-control-cs/_static/image28.png)

**図 10**: [はい] または [廃止された行に値が表示されない] ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-detailsview-control-cs/_static/image30.png)されます)

## <a name="summary"></a>要約

DetailsView コントロールの TemplateField を使用すると、他のフィールドコントロールで使用できるデータよりも高い柔軟性が得られ、次のような状況に適しています。

- 複数のデータフィールドを1つの GridView 列に表示する必要がある
- データは、プレーンテキストではなく Web コントロールを使用して表現することをお勧めします。
- 出力は、メタデータの表示やデータの再フォーマットなど、基になるデータによって異なります。

TemplateFields では、DetailsView の基になるデータをレンダリングする際の柔軟性が高くなりますが、各フィールドが HTML `<table>`の行としてレンダリングされるため、DetailsView の出力では引き続きビットの boxy が使用されます。

FormView コントロールを利用すると、表示される出力をより柔軟に構成できます。 FormView にはフィールドは含まれていませんが、一連のテンプレート (`ItemTemplate`、`EditItemTemplate`、`HeaderTemplate`など) だけではありません。 次のチュートリアルでは、FormView を使用して、レンダリングされたレイアウトをさらに細かく制御する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は Dan Jagers でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](using-templatefields-in-the-gridview-control-cs.md)
> [次へ](using-the-formview-s-templates-cs.md)
