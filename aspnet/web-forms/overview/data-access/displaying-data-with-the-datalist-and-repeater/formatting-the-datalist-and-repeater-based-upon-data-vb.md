---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
title: データに基づいて DataList と Repeater を書式設定する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、次のように書式設定関数を使用して、DataList コントロールと Repeater コントロールの外観を書式設定する方法の例について説明します。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: e2f401ae-37bb-4b19-aa97-d6b385d40f88
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: c9b60e4dacd992962942034e84c01cb82e039c81
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508096"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-vb"></a>データに基づいて DataList と Repeater を書式設定する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_VB.exe)または[PDF のダウンロード](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/datatutorial30vb1.pdf)

> このチュートリアルでは、テンプレート内で書式設定関数を使用するか、データバインドイベントを処理することによって、DataList コントロールと Repeater コントロールの外観を書式設定する方法の例について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルで見たように、DataList には、外観に影響を与えるさまざまなスタイル関連のプロパティが用意されています。 特に、既定の CSS クラスを DataList s `HeaderStyle`、`ItemStyle`、`AlternatingItemStyle`、および `SelectedItemStyle` プロパティに割り当てる方法について説明しました。 これらの4つのプロパティに加えて、DataList には、`Font`、`ForeColor`、`BackColor`、`BorderWidth`など、いくつかのスタイル関連プロパティがいくつか含まれています。 Repeater コントロールにスタイル関連のプロパティが含まれていません。 このようなスタイル設定は、Repeater s テンプレートのマークアップ内で直接行う必要があります。

しかし、多くの場合、データを書式設定する方法は、データ自体によって異なります。 たとえば、製品を一覧表示する場合は、製品情報を薄い灰色のフォントの色で表示することができます。または、`UnitsInStock` 値がゼロの場合に強調表示することもできます。 前のチュートリアルで見たように、GridView、DetailsView、および FormView には、データに基づいて外観を書式設定するための2つの方法が用意されています。

- **`DataBound` イベントは**、適切な `DataBound` イベントのイベントハンドラーを作成します。これは、データが各項目にバインドされた後に発生します (GridView の場合は `RowDataBound` イベント、DataList と Repeater の場合は `ItemDataBound` イベント)。 このイベントハンドラーでは、バインドされたデータのみを調べて、書式設定の決定を行うことができます。 この手法は、「[データに基づくカスタム書式](../custom-formatting/custom-formatting-based-upon-data-vb.md)設定」チュートリアルで確認しています。
- **テンプレートの関数の書式設定**DetailsView コントロールまたは GridView コントロールで templatefields を使用する場合、または FormView コントロールでテンプレートを使用する場合、書式設定関数を ASP.NET ページの分離コードクラス、ビジネスロジック層、または web アプリケーションからアクセスできるその他のクラスライブラリに追加できます。 この書式設定関数は任意の数の入力パラメーターを受け取ることができますが、テンプレートに表示する HTML を返す必要があります。 書式設定関数は、 [GridView コントロールチュートリアルの「Templatetemplatefields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 」で最初に検証されました。

これらの両方の書式設定手法は、DataList コントロールと Repeater コントロールで使用できます。 このチュートリアルでは、両方のコントロールに対して両方の手法を使用する例について説明します。

## <a name="using-theitemdataboundevent-handler"></a>`ItemDataBound`イベントハンドラーの使用

データソースコントロールから、またはプログラムによってコントロール s `DataSource` プロパティにデータを割り当て、その `DataBind()` メソッドを呼び出すことによって、データが DataList にバインドされている場合、DataList s `DataBinding` イベントが発生し、データソースが列挙され、各データレコードが DataList にバインドされます。 DataList は、データソース内の各レコードについて、現在のレコードにバインドされる[`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx)オブジェクトを作成します。 この処理中、DataList は次の2つのイベントを発生させます。

- `DataListItem` が作成された後に起動 **`ItemCreated`**
- **`ItemDataBound`** は、現在のレコードが `DataListItem` にバインドされた後に発生します

次の手順では、DataList コントロールのデータバインディングプロセスの概要を示します。

1. DataList s [`DataBinding` イベント](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx)が発生します。
2. データは DataList にバインドされます。  
  
   データソース内の各レコードについて 

    1. `DataListItem` オブジェクトを作成する
    2. [`ItemCreated` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)を起動します
    3. レコードを `DataListItem` にバインドする
    4. [`ItemDataBound` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)を起動します
    5. `Items` コレクションに `DataListItem` を追加します。

Repeater コントロールにデータをバインドする場合、同じ一連の手順を実行します。 唯一の違いは、`DataListItem` インスタンスが作成されるのではなく、リピータが[`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s を使用することです。

> [!NOTE]
> ずる賢い reader は、DataList と Repeater がデータにバインドされている場合と、GridView がデータにバインドされている場合に発生する一連の手順がわずかに異常であると認識している可能性があります。 データバインディングプロセスの末尾で、GridView によって `DataBound` イベントが発生します。ただし、このようなイベントは、DataList と Repeater の両方のコントロールにはありません。 これは、以前レベルのイベントハンドラーパターンが共通になる前に、DataList コントロールと Repeater コントロールが ASP.NET 1.x タイムフレームで作成されたためです。

GridView の場合と同様に、データに基づいて書式を設定するためのオプションの1つとして、`ItemDataBound` イベントのイベントハンドラーを作成する方法があります。 このイベントハンドラーは、`DataListItem` または `RepeaterItem` にバインドされたばかりのデータを検査し、必要に応じてコントロールの書式設定に影響を与えます。

DataList コントロールでは、標準の `Font`、`ForeColor`、`BackColor`、`CssClass`などを含む `DataListItem` s スタイル関連のプロパティを使用して、項目全体の書式設定の変更を実装できます。 DataList s テンプレート内の特定の Web コントロールの書式設定に影響を与えるには、プログラムを使用して、Web コントロールのスタイルにアクセスして変更する必要があります。 データのチュートリアルに*基づくカスタム書式*設定でこれを実現する方法について説明しました。 Repeater コントロールと同様に、`RepeaterItem` クラスにはスタイル関連のプロパティがありません。したがって、`ItemDataBound` イベントハンドラーの `RepeaterItem` に加えられたスタイル関連のすべての変更は、プログラムによってテンプレート内の Web コントロールにアクセスして更新する必要があります。

DataList と Repeater の `ItemDataBound` の書式設定手法は事実上同じであるため、この例では DataList の使用に焦点を当てます。

## <a name="step-1-displaying-product-information-in-the-datalist"></a>手順 1: DataList で製品情報を表示する

書式設定について心配する前に、まず、DataList を使用して製品情報を表示するページを作成してみましょう。 前の[チュートリアル](displaying-data-with-the-datalist-and-repeater-controls-vb.md)では、各製品の名前、カテゴリ、仕入先、数量/ユニット、価格を表示 `ItemTemplate` を持つ DataList を作成しました。 このチュートリアルでは、この機能を繰り返してみましょう。 これを実現するには、DataList とその ObjectDataSource をゼロから再作成するか、前のチュートリアルで作成したページ (`Basics.aspx`) からこれらのコントロールをコピーして、このチュートリアルのページ (`Formatting.aspx`) に貼り付けます。

DataList および ObjectDataSource 機能を `Basics.aspx` から `Formatting.aspx`にレプリケートしたら、DataList s `ID` プロパティを `DataList1` からよりわかりやすい `ItemDataBoundFormattingExample`に変更します。 次に、ブラウザーで DataList を表示します。 図1に示すように、各製品の書式設定の違いは、背景色が交互に表示されることだけです。

[DataList コントロールに製品が一覧表示され ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image1.png)

**図 1**: 製品が DataList コントロールに一覧表示される ([クリックしてフルサイズの画像を表示する](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image3.png))

このチュートリアルでは、$20.00 より小さい価格の製品については、名前と単価の両方が黄色で強調表示されるように DataList を設定します。

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>手順 2: プログラムによる ItemDataBound バインドイベントハンドラーのデータの値の決定

$20.00 未満の価格の製品でのみカスタム書式が適用されるため、各製品の価格を決定できる必要があります。 Datalist にデータをバインドすると、DataList はデータソース内のレコードを列挙し、各レコードについて `DataListItem` インスタンスを作成して、データソースレコードを `DataListItem`にバインドします。 特定のレコード s データが現在の `DataListItem` オブジェクトにバインドされると、DataList s `ItemDataBound` イベントが発生します。 このイベントのイベントハンドラーを作成して、現在の `DataListItem` のデータ値を検査し、それらの値に基づいて書式設定の変更を行うことができます。

DataList の `ItemDataBound` イベントを作成し、次のコードを追加します。

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample1.vb)]

DataList s `ItemDataBound` イベントハンドラーの背後にある概念とセマンティクスは、「*データに基づくカスタム書式*設定」チュートリアルの GridView s `RowDataBound` イベントハンドラーで使用されているものと同じですが、構文は若干異なります。 `ItemDataBound` イベントが発生すると、データにバインドされた `DataListItem` は、`e.Row`(GridView s `RowDataBound` イベントハンドラーと同様に) `e.Item` 経由で対応するイベントハンドラーに渡されます。 Datalist s `ItemDataBound` イベントハンドラーは、ヘッダー行、フッター行、および区切り行を含む、DataList に追加され*た各行に対して*発生します。 ただし、製品情報はデータ行にのみバインドされます。 そのため、`ItemDataBound` イベントを使用して DataList にバインドされたデータを検査する場合は、まずデータ項目を操作していることを確認する必要があります。 これは、[次の 8](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx)つの値のいずれかを持つ `DataListItem` s [`ItemType` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)を確認することで実現できます。

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

`Item` と `AlternatingItem``DataListItem` s の両方が、DataList s データ項目を行います。 `Item` または `AlternatingItem`を操作していると仮定すると、現在の `DataListItem`にバインドされている実際の `ProductsRow` インスタンスにアクセスします。 `DataListItem` s [`DataItem` プロパティ](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx)には、`DataRowView` オブジェクトへの参照が含まれています。このオブジェクトの `Row` プロパティは、実際の `ProductsRow` オブジェクトへの参照を提供します。

次に、`ProductsRow` instance s `UnitPrice` プロパティを確認します。 Products テーブルの `UnitPrice` フィールドでは `NULL` 値が許可されているため、`UnitPrice` プロパティにアクセスする前に、まず、`IsUnitPriceNull()` メソッドを使用して `NULL` 値があるかどうかを確認する必要があります。 `UnitPrice` 値が `NULL`ていない場合は、が $20.00 未満かどうかを確認します。 実際に $20.00 未満の場合は、カスタム書式設定を適用する必要があります。

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>手順 3: 製品名と価格を強調表示する

製品の価格が $20.00 未満であることを確認したら、その名前と価格を強調表示します。 これを実現するには、最初に製品の名前と価格を表示する `ItemTemplate` のラベルコントロールをプログラムで参照する必要があります。 次に、黄色の背景を表示する必要があります。 この書式設定情報は、ラベル `BackColor` プロパティ (`LabelID.BackColor = Color.Yellow`) を直接変更することで適用できます。ただし、すべての表示に関連する問題は、カスケードスタイルシートを通じて表現するのが理想的です。 実際には、`Styles.css` - `AffordablePriceEmphasis`で定義されている、必要な書式設定を提供するスタイルシートが既に用意されています。このスタイルは、「*データに基づくカスタム書式*設定」のチュートリアルで作成し、説明しました。

書式設定を適用するには、次のコードに示すように、2つのラベル Web コントロール `CssClass` プロパティを `AffordablePriceEmphasis`に設定するだけです。

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample2.vb)]

`ItemDataBound` イベントハンドラーが完了したら、ブラウザーで `Formatting.aspx` のページに戻ります。 図2に示すように、$20.00 の価格の製品には、名前と価格の両方が強調表示されています。

[$20.00 未満の製品が強調表示されている ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image4.png)

**図 2**: $20.00 未満の製品が強調表示されている ([クリックすると、フルサイズの画像が表示](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image6.png)されます)

> [!NOTE]
> DataList は HTML `<table>`として表示されるため、その `DataListItem` インスタンスには、特定のスタイルを項目全体に適用するように設定できるスタイル関連のプロパティがあります。 たとえば、価格が $20.00 未満の場合に、項目*全体*を黄色で強調表示するには、ラベルを参照したコードを置き換えて、その `CssClass` プロパティを次のコード行に設定し `e.Item.CssClass = "AffordablePriceEmphasis"` ます (図3を参照)。

Repeater コントロールを構成する `RepeaterItem` s は、このようなスタイルレベルのプロパティを提供しません。 したがって、カスタム書式設定をリピータに適用するには、図2のように、Repeater テンプレート内の Web コントロールにスタイルプロパティを適用する必要があります。

[$20.00 未満の製品の製品項目全体が強調表示さ ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image7.png)

**図 3**: $20.00 未満の製品の製品項目全体が強調表示されている ([クリックすると、フルサイズの画像が表示](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image9.png)されます)

## <a name="using-formatting-functions-from-within-the-template"></a>テンプレート内からの書式設定関数の使用

*「Gridview コントロールでの TemplateFields の使用*」チュートリアルでは、gridview TemplateField 内で書式設定関数を使用して、gridview の行にバインドされたデータに基づいてカスタム書式を適用する方法を説明しました。 書式設定関数は、テンプレートから呼び出すことができ、その代わりに生成される HTML を返すメソッドです。 書式設定関数は、ASP.NET ページの分離コードクラス内に存在することも、`App_Code` フォルダー内のクラスファイルまたは別のクラスライブラリプロジェクトに格納することもできます。 ASP.NET page s 分離コードクラスから書式設定関数を移動することは、複数の ASP.NET ページまたは他の ASP.NET web アプリケーションで同じ書式指定関数を使用する予定がある場合に最適です。

書式設定関数を示すために、の製品情報には、製品名の横にある [廃止] というテキストが含まれています。 また、が $20.00 未満の場合、価格は黄色で強調表示されます (`ItemDataBound` イベントハンドラーの例で行ったように)。価格が $20.00 以上の場合は、に実際の価格は表示されませんが、その代わりに、というテキストを入力してください。 図4は、これらの書式ルールが適用された製品一覧のスクリーンショットを示しています。

[高額な製品の場合、価格はテキストで置き換えられます。価格の見積もりについては、をお問い合わせください ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image10.png)

**図 4**: 高価な製品の場合、価格はテキストで置き換えられます。価格見積もりについては、をお問い合わせください ([クリックすると、フルサイズの画像が表示](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image12.png)されます)

## <a name="step-1-create-the-formatting-functions"></a>手順 1: 書式設定関数を作成する

この例では、2つの書式関数が必要です。1つは製品名とテキスト [廃止] を表示し、必要に応じて、強調表示された価格を $20.00 未満の場合は、テキストの場合はを、それ以外の場合はを呼び出します。 では、ASP.NET ページの分離コードクラスでこれらの関数を作成し、`DisplayProductNameAndDiscontinuedStatus` して `DisplayPrice`という名前を指定します。 どちらの方法でも、HTML を文字列として表示する必要があります。また、ASP.NET ページ s 宣言構文部分から呼び出すには、両方のメソッドが `Protected` (または `Public`) とマークされている必要があります。 これらの2つのメソッドのコードは次のとおりです。

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample3.vb)]

`DisplayProductNameAndDiscontinuedStatus` メソッドは、`productName` の値と `discontinued` のデータフィールドをスカラー値として受け入れます。一方、`DisplayPrice` メソッドは `ProductsRow` のスカラー値ではなく `unitPrice` インスタンスを受け入れます。 どちらの方法も使用できます。ただし、書式設定関数が、データベース `NULL` 値 (`ProductName` `UnitPrice`など) を含むことができるスカラー値を使用している場合、`Discontinued` または `NULL` 値を許可していない場合は、これらのスカラー入力を処理する際に特別な注意を払う必要があります。

具体的には、入力パラメーターは `Object` 型である必要があります。これは、受信値が、予期されるデータ型ではなく `DBNull` インスタンスである可能性があるためです。 さらに、受信した値がデータベース `NULL` 値であるかどうかを確認するためのチェックを行う必要があります。 つまり、`DisplayPrice` 方法では、スカラー値として価格を受け入れる必要がある場合、次のコードを使用する必要があります。

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample4.vb)]

`unitPrice` 入力パラメーターの型が `Object` であり、`unitPrice` が `DBNull` かどうかを確認するために条件付きステートメントが変更されていることに注意してください。 さらに、`unitPrice` 入力パラメーターは `Object`として渡されるため、10進値にキャストする必要があります。

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>手順 2: DataList s ItemTemplate からの書式設定関数の呼び出し

ASP.NET ページの分離コードクラスに追加された書式関数を使用すると、これらの書式設定関数を DataList s `ItemTemplate`から呼び出すだけで済みます。 テンプレートから書式設定関数を呼び出すには、関数呼び出しを databinding 構文内に配置します。

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample5.aspx)]

DataList s `ItemTemplate` `ProductNameLabel` Label Web コントロールは、`Text` プロパティに `<%# Eval("ProductName") %>`の結果を割り当てることによって、製品名を現在表示しています。 名前とテキスト [廃止] を表示するには、必要に応じて、代わりに `Text` プロパティを `DisplayProductNameAndDiscontinuedStatus` メソッドの値に割り当てるように宣言構文を更新します。 その場合は、`Eval("columnName")` 構文を使用して、製品名と廃止された値を渡す必要があります。 `Eval` は `Object`型の値を返しますが、`DisplayProductNameAndDiscontinuedStatus` メソッドには `String` および `Boolean`型の入力パラメーターが必要です。したがって、`Eval` メソッドによって返される値は、次のように、予期される入力パラメーターの型にキャストする必要があります。

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample6.aspx)]

価格を表示するには、単に `UnitPriceLabel` Label s `Text` プロパティを `DisplayPrice` メソッドによって返される値に設定します。これは、製品の名前と [廃止] のテキストを表示する場合と同様です。 ただし、`UnitPrice` をスカラー入力パラメーターとして渡すのではなく、`ProductsRow` インスタンス全体を渡します。

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample7.aspx)]

書式設定関数の呼び出しを実行し、ブラウザーで進行状況を表示します。 画面は図5のようになります。これには、「廃止された」というテキストを含む廃止された製品が含まれています。また、これらの製品の料金は $20.00 を超えています。価格については、「」を参照してください。

[高額な製品の場合、価格はテキストで置き換えられます。価格の見積もりについては、をお問い合わせください ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image13.png)

**図 5**: 高価な製品の場合、価格はテキストで置き換えられます。価格見積もりについては、をお問い合わせください ([クリックすると、フルサイズの画像が表示](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image15.png)されます)

## <a name="summary"></a>まとめ

データに基づいて DataList または Repeater コントロールの内容を書式設定するには、次の2つの方法を使用します。 最初の方法では、`ItemDataBound` イベントのイベントハンドラーを作成します。これは、データソース内の各レコードが新しい `DataListItem` または `RepeaterItem`にバインドされるときに発生します。 `ItemDataBound` イベントハンドラーでは、現在の項目のデータを確認してから、書式設定をテンプレートの内容に適用したり、`DataListItem` の場合は項目全体に適用したりすることができます。

または、書式設定関数を使用してカスタム書式設定を実現できます。 書式設定関数は、その代わりに生成する HTML を返す DataList または Repeater s テンプレートから呼び出すことができるメソッドです。 多くの場合、書式設定関数によって返される HTML は、現在の項目にバインドされている値によって決定されます。 これらの値は、スカラー値として、または項目にバインドされるオブジェクト全体 (`ProductsRow` インスタンスなど) に渡すことによって、書式指定関数に渡すことができます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Yaakov Ellis、Randy/Liz Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
> [次へ](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
