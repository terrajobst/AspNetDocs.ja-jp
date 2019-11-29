---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: データに基づくカスタム書式設定 (VB) |Microsoft Docs
author: rick-anderson
description: GridView、DetailsView、または FormView の形式を、バインドされたデータに基づいて調整するには、複数の方法があります。 このチュートリアルでは、...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 268dc763ef6954903f721a3015daaf10bf9bccb1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74613047"
---
# <a name="custom-formatting-based-upon-data-vb"></a>データに基づくカスタム書式設定 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe)または[PDF のダウンロード](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> GridView、DetailsView、または FormView の形式を、バインドされたデータに基づいて調整するには、複数の方法があります。 このチュートリアルでは、データバインディングと行のデータバインドのイベントハンドラーを使用して、データバインド形式を実現する方法について説明します。

## <a name="introduction"></a>はじめに

GridView、DetailsView、FormView コントロールの外観は、スタイルに関連する無数のプロパティを使用してカスタマイズできます。 `CssClass`、`Font`、`BorderWidth`、`BorderStyle`、`BorderColor`、`Width`、`Height`などのプロパティは、表示されるコントロールの全般的な外観を決定します。 `HeaderStyle`、`RowStyle`、`AlternatingRowStyle`などのプロパティを使用すると、これらの同じスタイル設定を特定のセクションに適用できます。 同様に、これらのスタイル設定はフィールドレベルで適用できます。

ただし、多くのシナリオでは、書式設定の要件は、表示されるデータの値によって異なります。 たとえば、在庫切れ製品に注目するために、製品情報を一覧表示するレポートでは、`UnitsInStock` フィールドと `UnitsOnOrder` フィールドの両方が0である製品の背景色が黄色に設定されている場合があります。 コストの高い製品を強調表示するには、$75.00 を超える価格を太字のフォントで表示することをお勧めします。

GridView、DetailsView、または FormView の形式を、バインドされたデータに基づいて調整するには、複数の方法があります。 このチュートリアルでは、`DataBound` および `RowDataBound` のイベントハンドラーを使用して、データバインド形式を実現する方法について説明します。 次のチュートリアルでは、別の方法について説明します。

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView コントロールの`DataBound`イベントハンドラーの使用

データソースコントロールから、またはプログラムによってコントロールの `DataSource` プロパティにデータを割り当て、その `DataBind()` メソッドを呼び出すことにより、データが DetailsView にバインドされると、次の一連の手順が実行されます。

1. データ Web コントロールの `DataBinding` イベントが発生します。
2. データは、データ Web コントロールにバインドされます。
3. データ Web コントロールの `DataBound` イベントが発生します。

カスタムロジックは、手順 1. と 3. の直後にイベントハンドラーを使用して挿入できます。 `DataBound` イベントのイベントハンドラーを作成することによって、データ Web コントロールにバインドされているデータをプログラムによって判断し、必要に応じて書式設定を調整することができます。 これを説明するために、製品に関する全般的な情報を一覧表示する DetailsView を作成しますが、$75.00 を超えた場合は、`UnitPrice` 値を***太字の斜体フォント***で表示します。

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>手順 1: DetailsView で製品情報を表示する

`CustomFormatting` フォルダーの [`CustomColors.aspx`] ページを開き、[ツールボックス] から [DetailsView] コントロールをデザイナーにドラッグし、`ID` プロパティの値を [`ExpensiveProductsPriceInBoldItalic`] に設定して、`ProductsBLL` クラスの `GetProducts()` メソッドを呼び出す新しい ObjectDataSource コントロールにバインドします。 これを実現するための詳細な手順については、前のチュートリアルで詳しく説明したので、ここでは簡潔にするために省略してあります。

ObjectDataSource を DetailsView にバインドしたら、すぐにフィールドリストを変更します。 `ProductID`、`SupplierID`、`CategoryID`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`、および `Discontinued` BoundFields を削除し、残りの BoundFields の名前を変更して再フォーマットすることを選択しました。 また、`Width` と `Height` の設定をクリアしました。 DetailsView には1つのレコードのみが表示されるため、エンドユーザーがすべての製品を表示できるようにするには、ページングを有効にする必要があります。 これを行うには、DetailsView のスマートタグの [ページングを有効にする] チェックボックスをオンにします。

[![図 1: DetailsView のスマートタグの [ページングを有効にする] チェックボックスをオンにする](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**図 1**: 図 1: DetailsView のスマートタグの [ページングを有効にする] チェックボックス[をオンにする (クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image3.png)されます)

これらの変更が完了すると、DetailsView マークアップは次のようになります。

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

ブラウザーでこのページをテストしてみましょう。

[DetailsView コントロールに一度に1つの製品が表示される ![](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**図 2**: DetailsView コントロールは一度に1つの製品を表示します ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image6.png)されます)

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>手順 2: プログラムによってデータバインドイベントハンドラーのデータ値を判断する

`UnitPrice` 値が $75.00 を超える製品の太字で斜体のフォントで価格を表示するには、まず、`UnitPrice` の値をプログラムによって判断できるようにする必要があります。 DetailsView の場合、これは `DataBound` イベントハンドラーで実現できます。 イベントハンドラーを作成するには、デザイナーで [DetailsView] をクリックし、プロパティウィンドウに移動します。 F4 キーを押して表示しない場合は、F4 キーを押すか、[表示] メニューに移動して [プロパティウィンドウ] メニューオプションを選択します。 プロパティウィンドウから、稲妻のアイコンをクリックして、DetailsView のイベントの一覧を表示します。 次に、`DataBound` イベントをダブルクリックするか、作成するイベントハンドラーの名前を入力します。

![データバインドイベントのイベントハンドラーを作成する](custom-formatting-based-upon-data-vb/_static/image7.png)

**図 3**: `DataBound` イベントのイベントハンドラーを作成する

> [!NOTE]
> また、ASP.NET ページのコード部分からイベントハンドラーを作成することもできます。 ここには、ページの上部に2つのドロップダウンリストがあります。 左のドロップダウンリストからオブジェクトを選択すると、ハンドラーを作成するイベントが右のドロップダウンリストから選択され、Visual Studio によって適切なイベントハンドラーが自動的に作成されます。

これにより、イベントハンドラーが自動的に作成され、追加されたコード部分に移動します。 この時点で、次のように表示されます。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

DetailsView にバインドされたデータには、`DataItem` プロパティを使用してアクセスできます。 コントロールを厳密に型指定された DataTable にバインドすることを思い出してください。これは、厳密に型指定された DataRow インスタンスのコレクションで構成されています。 DataTable が DetailsView にバインドされると、DataTable の最初の DataRow が DetailsView の `DataItem` プロパティに割り当てられます。 具体的には、`DataItem` プロパティに `DataRowView` オブジェクトが割り当てられます。 `DataRowView`の `Row` プロパティを使用して、基になる DataRow オブジェクト (実際には `ProductsRow` インスタンス) にアクセスできます。 この `ProductsRow` インスタンスを作成した後は、オブジェクトのプロパティ値を調べるだけで、決定を行うことができます。

次のコードは、DetailsView コントロールにバインドされている `UnitPrice` 値が $75.00 より大きいかどうかを確認する方法を示しています。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> `UnitPrice` はデータベースに `NULL` 値を持つことができるため、まず、`ProductsRow`の `UnitPrice` プロパティにアクセスする前に `NULL` 値を処理していないことを確認します。 `NULL` 値がある場合に `UnitPrice` プロパティにアクセスしようとすると、`ProductsRow` オブジェクトが[StrongTypingException 例外](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)をスローするため、このチェックは重要です。

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>手順 3: DetailsView の UnitPrice 値の書式設定

この時点で、DetailsView にバインドされている `UnitPrice` 値の値が $75.00 を超えているかどうかを確認できますが、それに応じて DetailsView の書式をプログラムで調整する方法については、まだ説明していません。 DetailsView 内の行全体の書式を変更するには、プログラムで `DetailsViewID.Rows(index)`を使用して行にアクセスします。特定のセルを変更するには、`DetailsViewID.Rows(index).Cells(index)`を使用します。 行またはセルへの参照を取得したら、そのスタイルに関連するプロパティを設定することによって外観を調整できます。

プログラムによって行にアクセスするには、0から始まる行のインデックスが必要です。 `UnitPrice` 行は、DetailsView の5番目の行になります。これにより、4のインデックスが作成され、`ExpensiveProductsPriceInBoldItalic.Rows(4)`を使用してプログラムからアクセスできるようになります。 この時点で、次のコードを使用して、行のコンテンツ全体を太字で斜体のフォントで表示できます。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

ただし、これにより、ラベル (Price) と値が太字と斜体の*両方*が作成されます。 太字と斜体の値のみを使用する場合は、この書式設定を行の2番目のセルに適用する必要があります。これは、次のようにして実現できます。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

これまでのチュートリアルでは、スタイルシートを使用して、レンダリングされたマークアップとスタイル関連の情報を明確に分離しているため、上記のように特定のスタイルプロパティを設定するのではなく、CSS クラスを使用します。 `Styles.css` スタイルシートを開き、次の定義を使用して `ExpensivePriceEmphasis` という名前の新しい CSS クラスを追加します。

[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

次に、`DataBound` イベントハンドラーで、セルの `CssClass` プロパティを `ExpensivePriceEmphasis`に設定します。 次のコードは、`DataBound` イベントハンドラー全体を示しています。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

Chai を表示するときに、$75.00 未満の料金が表示される場合は、通常のフォントで表示されます (図4を参照)。 ただし、価格が $97.00 の Mishi の Niku を表示する場合、価格は太字で斜体のフォントで表示されます (図5を参照)。

[$75.00 未満の ![価格は通常のフォントで表示されます](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**図 4**: $75.00 未満の価格は通常のフォントで表示されます ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image10.png)されます)

[![高価な製品の価格が太字で斜体のフォントで表示される](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**図 5**: 高価な製品の価格は、太字で斜体のフォントで表示されます ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image13.png)されます)

## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView コントロールの`DataBound`イベントハンドラーの使用

FormView にバインドされている基になるデータを決定する手順は、DetailsView の場合と同じです。 `DataBound` イベントハンドラーを作成し、`DataItem` プロパティをコントロールにバインドされている適切なオブジェクト型にキャストし、続行する方法を決定します。 ただし、FormView と DetailsView は、ユーザーインターフェイスの外観がどのように更新されるかによって異なります。

FormView に BoundFields が含まれていないため、`Rows` コレクションがありません。 代わりに、FormView はテンプレートで構成されています。これには、静的な HTML、Web コントロール、およびデータバインディングの構文の組み合わせを含めることができます。 FormView のスタイルを調整するには、通常、FormView のテンプレート内の1つ以上の Web コントロールのスタイルを調整する必要があります。

これを説明するために、FormView を使用して前の例のように製品を一覧表示しますが、ここでは、在庫の単位が10以下の場合に、株価の単位を赤のフォントで表示します。

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>手順 4: FormView で製品情報を表示する

FormView の下にある `CustomColors.aspx` ページに FormView を追加し、その `ID` プロパティを `LowStockedProductsInRed`に設定します。 前の手順で作成した ObjectDataSource コントロールに FormView をバインドします。 これにより、FormView の `ItemTemplate`、`EditItemTemplate`、および `InsertItemTemplate` が作成されます。 `EditItemTemplate` と `InsertItemTemplate` を削除し、`ProductName` および `UnitsInStock` の値だけを含めるように `ItemTemplate` を簡略化します。各値は、適切な名前を付けたラベルコントロールに含まれます。 前の例の DetailsView と同様に、FormView のスマートタグの [ページングを有効にする] チェックボックスもオンにします。

これらの編集が完了すると、FormView のマークアップは次のようになります。

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

`ItemTemplate` には次のものが含まれることに注意してください。

- **静的 HTML**テキスト "Product:" および "Unit In Stock:" と共に、`<br />` 要素と `<b>` 要素が含まれます。
- **Web**では、`ProductNameLabel` と `UnitsInStockLabel`の2つのラベルコントロールを制御します。
- **Databinding 構文**`<%# Bind("ProductName") %>` と `<%# Bind("UnitsInStock") %>` の構文。これらのフィールドの値をラベルコントロールの `Text` プロパティに割り当てます。

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>手順 5: プログラムによってデータバインドイベントハンドラーのデータ値を判断する

FormView のマークアップが完了したら、次の手順では、`UnitsInStock` 値が10以下であるかどうかをプログラムによって判断します。 これは、DetailsView と同じように FormView とまったく同じ方法で実行されます。 まず、FormView の `DataBound` イベントのイベントハンドラーを作成します。

![データバインドイベントハンドラーを作成する](custom-formatting-based-upon-data-vb/_static/image14.png)

**図 6**: `DataBound` イベントハンドラーを作成する

イベントハンドラーで、FormView の `DataItem` プロパティを `ProductsRow` インスタンスにキャストし、`UnitsInPrice` 値が赤いフォントで表示する必要があるかどうかを判断します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>手順 6: FormView の ItemTemplate で、ユニットの Instocklabel ラベルコントロールの書式を設定する

最後の手順では、表示されている `UnitsInStock` 値を、値が10以下の場合に赤いフォントで書式設定します。 これを実現するには、プログラムを使用して `ItemTemplate` の `UnitsInStockLabel` コントロールにアクセスし、そのテキストが赤で表示されるようにスタイルプロパティを設定する必要があります。 テンプレート内の Web コントロールにアクセスするには、次のように `FindControl("controlID")` メソッドを使用します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

この例では、`ID` 値が `UnitsInStockLabel`であるラベルコントロールにアクセスするため、次のように使用します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

プログラムによる Web コントロールへの参照を取得したら、必要に応じてスタイル関連のプロパティを変更できます。 前の例と同様に、`Styles.css` `LowUnitsInStockEmphasis`という名前の CSS クラスを作成しました。 このスタイルをラベル Web コントロールに適用するには、その `CssClass` プロパティを適宜設定します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> `FindControl("controlID")` を使用して Web コントロールにプログラムでアクセスし、そのスタイルに関連するプロパティを設定するための構文は、DetailsView コントロールまたは GridView コントロールで[Templatefields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx)を使用する場合にも使用できます。 TemplateFields については、次のチュートリアルで確認します。

図7は、`UnitsInStock` 値が10より大きい製品を表示する場合の FormView を示しています。一方、図8の製品の値は10未満です。

[在庫に十分な単位がある製品の ![、カスタム書式設定は適用されません。](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**図 7**: 在庫数が十分に大きい製品の場合、カスタム書式設定は適用されません ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image17.png)されます)

[![値が10以下の製品については、在庫番号の単位が赤で示されます。](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**図 8**: 値が10以下の製品については、在庫番号の単位が赤で示されます ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image20.png)されます)

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>GridView の`RowDataBound`イベントを使用した書式設定

前の手順では、データバインド中に DetailsView と FormView によって進行を制御する一連の手順を確認しています。 これらの手順をもう一度確認してみましょう。

1. データ Web コントロールの `DataBinding` イベントが発生します。
2. データは、データ Web コントロールにバインドされます。
3. データ Web コントロールの `DataBound` イベントが発生します。

この3つの簡単な手順では、1つのレコードのみが表示されるので、DetailsView と FormView で十分です。 GridView の場合は、それにバインドされている*すべて*のレコードが表示されます (1 つ目のレコードではありません)。手順2はもう少し複雑です。

手順 2. では、GridView がデータソースを列挙し、各レコードについて `GridViewRow` インスタンスを作成し、現在のレコードをバインドします。 GridView に追加される `GridViewRow` ごとに、次の2つのイベントが発生します。

- `GridViewRow` が作成された後に起動 **`RowCreated`**
- **`RowDataBound`** は、現在のレコードが `GridViewRow`にバインドされた後に発生します。

GridView の場合、データバインディングは次の一連の手順でより正確に記述されます。

1. GridView の `DataBinding` イベントが発生します。
2. データは GridView にバインドされます。   
  
   データソース内の各レコードについて 

    1. `GridViewRow` オブジェクトを作成する
    2. `RowCreated` イベントを起動します
    3. レコードを `GridViewRow` にバインドする
    4. `RowDataBound` イベントを起動します
    5. `Rows` コレクションに `GridViewRow` を追加します。
3. GridView の `DataBound` イベントが発生します。

GridView の個々のレコードの形式をカスタマイズするには、`RowDataBound` イベントのイベントハンドラーを作成する必要があります。 これを説明するために、`CustomColors.aspx` ページに GridView を追加して、各製品の名前、カテゴリ、価格を一覧表示します。これにより、価格が $10.00 未満の製品が黄色の背景色で強調表示されます。

## <a name="step-7-displaying-product-information-in-a-gridview"></a>手順 7: GridView で製品情報を表示する

前の例の FormView の下に GridView を追加し、その `ID` プロパティを `HighlightCheapProducts`に設定します。 ページ上のすべての製品を返す ObjectDataSource が既にあるため、GridView をそれにバインドします。 最後に、GridView の BoundFields を編集して、製品の名前、カテゴリ、価格だけを含めます。 これらの編集の後、GridView のマークアップは次のようになります。

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

図9に、ブラウザーで表示したときのこのポイントの進行状況を示します。

[GridView に ![、各製品の名前、カテゴリ、価格が表示されます。](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**図 9**: GridView には、各製品の名前、カテゴリ、価格が表示されます ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image23.png)されます)

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>手順 8: RowDataBound バインドイベントハンドラーのデータの値をプログラムで判断する

`ProductsDataTable` が GridView にバインドされると、その `ProductsRow` インスタンスが列挙され、`ProductsRow` ごとに `GridViewRow` が作成されます。 `GridViewRow`の `DataItem` プロパティは、特定の `ProductRow`に割り当てられます。その後、GridView の `RowDataBound` イベントハンドラーが発生します。 GridView にバインドされている各製品の `UnitPrice` 値を特定するには、GridView の `RowDataBound` イベント用のイベントハンドラーを作成する必要があります。 このイベントハンドラーでは、現在の `GridViewRow` の `UnitPrice` 値を調べて、その行に対して書式設定の決定を行うことができます。

このイベントハンドラーは、FormView および DetailsView と同じ一連の手順を使用して作成できます。

![GridView の RowDataBound バインドイベントのイベントハンドラーを作成します。](custom-formatting-based-upon-data-vb/_static/image24.png)

**図 10**: GridView の `RowDataBound` イベントのイベントハンドラーを作成する

この方法でイベントハンドラーを作成すると、ASP.NET ページのコード部分に次のコードが自動的に追加されます。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

`RowDataBound` イベントが発生すると、イベントハンドラーは、`GridViewRowEventArgs`型のオブジェクトである2番目のパラメーターとして渡されます。このオブジェクトには、`Row`という名前のプロパティがあります。 このプロパティは、データバインドされただけの `GridViewRow` への参照を返します。 `GridViewRow` にバインドされている `ProductsRow` インスタンスにアクセスするには、次のように `DataItem` プロパティを使用します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

`RowDataBound` イベントハンドラーを使用する場合は、GridView がさまざまな種類の行で構成され、このイベントが*すべて*の行の種類に対して発生することに注意することが重要です。 `GridViewRow`の型は、`RowType` プロパティによって決定できます。また、次のいずれかの値を使用できます。

- GridView の `DataSource` からレコードにバインドされている行を `DataRow` します。
- GridView の `DataSource` が空の場合に表示される行を `EmptyDataRow` します
- フッター行を `Footer` します。GridView の `ShowFooter` プロパティがに設定されている場合に表示され `True`
- ヘッダー行を `Header` します。GridView の ShowHeader プロパティが `True` (既定値) に設定されている場合に表示されます。
- ページングを実装する GridView の `Pager`、ページングインターフェイスを表示する行
- `Separator` GridView には使用されませんが、DataList コントロールと Repeater コントロールの `RowType` プロパティで使用されます。今後のチュートリアルでは、2つのデータ Web コントロールについて説明します。

`EmptyDataRow`、`Header`、`Footer`、および `Pager` の行は `DataSource` レコードと関連付けられていないため、`Nothing` のプロパティの値は常に `DataItem` になります。 このため、現在の `GridViewRow`の `DataItem` プロパティを操作する前に、まず `DataRow`を処理するようにしてください。 これを行うには、次のように `GridViewRow`の `RowType` プロパティをチェックします。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>手順 9: UnitPrice 値が $10.00 未満の場合に行を黄色で強調表示する

最後の手順では、その行の `UnitPrice` 値が $10.00 未満の場合、プログラムによって `GridViewRow` 全体を強調表示します。 GridView の行またはセルにアクセスするための構文は、特定のセルにアクセスするために `GridViewID.Rows(index).Cells(index)` 行全体にアクセスするための DetailsView `GridViewID.Rows(index)` と同じです。 ただし、`RowDataBound` イベントハンドラーが起動するときに、`GridViewRow` データバインドされたデータは、GridView の `Rows` コレクションにまだ追加されていません。 そのため、Rows コレクションを使用して、`RowDataBound` イベントハンドラーから現在の `GridViewRow` インスタンスにアクセスすることはできません。

`GridViewID.Rows(index)`ではなく、`e.Row`を使用して `RowDataBound` イベントハンドラーで現在の `GridViewRow` インスタンスを参照することができます。 つまり、`RowDataBound` イベントハンドラーから現在の `GridViewRow` インスタンスを強調表示するには、次のように使用します。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

`GridViewRow`の `BackColor` プロパティを直接設定するのではなく、CSS クラスの使用について説明します。 ここでは、背景色を黄色に設定する `AffordablePriceEmphasis` という名前の CSS クラスを作成しました。 完成した `RowDataBound` イベントハンドラーは次のようになります。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]

[最も手頃な価格の製品を黄色で強調表示 ![](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**図 11**: 最も低価格の製品が黄色で強調表示されている ([クリックすると、フルサイズの画像が表示](custom-formatting-based-upon-data-vb/_static/image27.png)されます)

## <a name="summary"></a>要約

このチュートリアルでは、コントロールにバインドされたデータに基づいて GridView、DetailsView、および FormView の書式を設定する方法を説明しました。 これを実現するために、必要に応じて、基になるデータを書式設定の変更と共に調べた `DataBound` イベントまたは `RowDataBound` イベントのイベントハンドラーを作成しました。 DetailsView または FormView にバインドされたデータにアクセスするには、`DataBound` イベントハンドラーの `DataItem` プロパティを使用します。GridView の場合、各 `GridViewRow` インスタンスの `DataItem` プロパティには、その行にバインドされたデータが含まれます。これは、`RowDataBound` イベントハンドラーで使用できます。

プログラムによってデータ Web コントロールの書式設定を調整するための構文は、Web コントロールと書式設定されるデータの表示方法によって異なります。 DetailsView コントロールと GridView コントロールでは、序数インデックスを使用して行とセルにアクセスできます。 テンプレートを使用する FormView では、通常、`FindControl("controlID")` メソッドを使用して、テンプレート内から Web コントロールを検索します。

次のチュートリアルでは、GridView と DetailsView でテンプレートを使用する方法について説明します。 さらに、基になるデータに基づいて書式設定をカスタマイズするための別の方法も紹介します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は E.R. でした Gilmore、Patterson が、Dan Jagers。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [次へ](using-templatefields-in-the-gridview-control-vb.md)
