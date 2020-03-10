---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: DataList コントロール (C#) を使用して行ごとに複数のレコードを表示するMicrosoft Docs
author: rick-anderson
description: この短いチュートリアルでは、[RepeatColumns] プロパティと [Repeatcolumns] プロパティを使用して、DataList のレイアウトをカスタマイズする方法について説明します。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3280a7b5f28207d3e640a6480f47869ce19692bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481108"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>DataList コントロールで複数のレコードを行ごとに表示する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe)または[PDF のダウンロード](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> この短いチュートリアルでは、[RepeatColumns] プロパティと [Repeatcolumns] プロパティを使用して、DataList のレイアウトをカスタマイズする方法について説明します。

## <a name="introduction"></a>はじめに

これまでの2つのチュートリアルで見た DataList の例では、各レコードをデータソースから1列の HTML `<table>`の行として表示しています。 これは既定の DataList 動作ですが、データソースアイテムが複数列の複数行テーブルに分散されるように、DataList 表示をカスタマイズするのは非常に簡単です。 さらに、すべてのデータソースアイテムを1行の複数列の DataList に表示することもできます。

DataList s レイアウトは、`RepeatColumns` と `RepeatDirection` プロパティを使用してカスタマイズできます。これらのプロパティはそれぞれ、表示される列の数と、それらの項目が垂直方向または水平方向のどちらでレイアウトされるかを示します。 図1は、3つの列を含むテーブルに製品情報を表示する DataList を示しています。

[DataList によって行ごとに3つの製品が表示される ![](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**図 1**: DataList は行ごとに3つの製品を表示します ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png)されます)

行ごとに複数のデータソース項目を表示することにより、DataList は水平画面領域をより効果的に利用できます。 この短いチュートリアルでは、これら2つの DataList プロパティについて説明します。

## <a name="step-1-displaying-product-information-in-a-datalist"></a>手順 1: DataList で製品情報を表示する

`RepeatColumns` と `RepeatDirection` のプロパティを確認する前に、まず、標準の単一列のテーブルレイアウトを使用して製品情報を一覧表示する DataList をページに作成します。 この例では、次のマークアップを使用して、製品の名前、カテゴリ、価格を表示します。

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

前の例でデータを DataList にバインドする方法について説明しましたので、これらの手順を迅速に進めていきます。 まず、`DataListRepeaterBasics` フォルダーの [`RepeatColumnAndDirection.aspx`] ページを開き、[ツールボックス] から [DataList] をデザイナーにドラッグします。 DataList s スマートタグから新しい ObjectDataSource を作成し、そのデータを `ProductsBLL` クラスの `GetProducts` メソッドからプルするように構成します。 [ウィザード] の [挿入]、[更新]、および [削除] の各タブで [(なし)] オプションを選択します。

新しい ObjectDataSource を作成して DataList にバインドすると、Visual Studio によって、各製品データフィールドの名前と値を表示する `ItemTemplate` が自動的に作成されます。 宣言マークアップまたは DataList s スマートタグの [テンプレートの編集] オプションを使用して、上に示したマークアップを使用するように `ItemTemplate` を直接調整します。これにより、*製品名*、*カテゴリ名*、*価格*テキストは、適切なデータバインディング構文を使用して、`Text` プロパティに値を割り当てるラベルコントロールに置き換えられます。 `ItemTemplate`を更新すると、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

`UnitPrice`の `Eval` databinding 構文に書式指定子が含まれており、返された値が通貨として書式設定されていることに注意してください `Eval("UnitPrice", "{0:C}").`

ブラウザーでページにアクセスします。 図2に示すように、DataList は製品の単一列の複数行のテーブルとして表示されます。

[![既定では、DataList は単一列の複数行のテーブルとして表示されます。](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**図 2**: 既定では、DataList は単一列の複数行のテーブルとして表示されます ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png)されます)

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>手順 2: DataList s レイアウト方向の変更

DataList の既定の動作では、単一列の複数行のテーブルで項目を垂直方向にレイアウトしますが、この動作は DataList s [`RepeatDirection` プロパティ](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)を使用して簡単に変更できます。 `RepeatDirection` プロパティは、`Horizontal` または `Vertical` (既定値) の2つの値のいずれかを受け取ることができます。

DataList は、`RepeatDirection` プロパティを `Vertical` から `Horizontal`に変更することにより、そのレコードを1つの行に表示し、データソースアイテムごとに1つの列を作成します。 この効果を示すには、デザイナーで DataList をクリックし、プロパティウィンドウの `RepeatDirection` プロパティを `Vertical` から `Horizontal`に変更します。 この操作を行うと、デザイナーによって DataList s レイアウトが調整され、単一行、複数列のインターフェイスが作成されます (図3を参照)。

[RepeatDirection プロパティを ![して、DataList の項目がどのようにレイアウトされるかを決定します。](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**図 3**: `RepeatDirection` プロパティは、DataList の項目のレイアウトを決定します ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png)されます)

少量のデータを表示する場合は、単一行の複数列のテーブルが、画面の不動産を最大化するのに最適な方法である可能性があります。 ただし、大量のデータについては、1つの行に多数の列が必要になります。これにより、画面に収まりきらないアイテムが右側にプッシュされます。 図4は、1行の DataList で表示される場合の製品を示しています。 多くの製品 (80 を超える) があるため、ユーザーは各製品に関する情報を表示するために、右端までスクロールする必要があります。

[データソースが十分に大きい場合は、1つの列の DataList で水平スクロールが必要になることが ![](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**図 4**: 十分に大規模なデータソースの場合は、1つの列の DataList で水平スクロールが必要になります ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png)されます)

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>手順 3: 複数列の複数行のテーブルにデータを表示する

複数列の複数行の DataList を作成するには、 [`RepeatColumns` プロパティ](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx)を、表示する列の数に設定する必要があります。 既定では、`RepeatColumns` プロパティは0に設定されています。これにより、DataList では、`RepeatDirection` プロパティの値に応じて、すべての項目が1つの行または列に表示されます。

この例では、テーブル行ごとに3つの製品を表示します。 したがって、`RepeatColumns` プロパティを3に設定します。 この変更を行った後、ブラウザーで結果を表示してみてください。 図5に示すように、製品は3列の複数行のテーブルに一覧表示されています。

[行ごとに3つの製品 ![表示されます](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**図 5**: 行ごとに3つの製品が表示される ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png)されます)

`RepeatDirection` プロパティは、DataList の項目がどのようにレイアウトされるかに影響します。図5は、`RepeatDirection` プロパティが `Horizontal`に設定された結果を示しています。 最初の3つの製品である Chai、変更履歴、Aniseed シロップが左から右、上から下にレイアウトされていることに注意してください。 次の3つの製品 (Chef Anton s Cajun Seasoning 以降) は、最初の3つの下にある行に表示されます。 ただし、`RepeatDirection` プロパティを `Vertical`に変更すると、図6に示すように、これらの製品が上から下、左から右にレイアウトされます。

[ここで ![、製品は垂直方向にレイアウトされます。](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**図 6**: ここでは、製品が縦方向にレイアウトされています ([クリックすると、フルサイズの画像が表示](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png)されます)

結果のテーブルに表示される行数は、DataList にバインドされている合計レコード数によって異なります。 正確には、データソースアイテムの合計数が `RepeatColumns` プロパティ値で割った値になります。 現在、`Products` テーブルには3で割り切れる84製品があるため、28行あります。 データソース内の項目数と `RepeatColumns` プロパティ値が割り切れない場合、最後の行または列には空白のセルが含まれます。 `RepeatDirection` が `Vertical`に設定されている場合、最後の列には空のセルが含まれます。`RepeatDirection` が `Horizontal`の場合、最後の行には空のセルが含まれます。

## <a name="summary"></a>まとめ

既定では、DataList は単一列の複数行のテーブルに項目を一覧表示します。これは、1つの TemplateField を持つ GridView のレイアウトを模倣します。 この既定のレイアウトは許容されますが、行ごとに複数のデータソース項目を表示することで、画面の不動産を最大化できます。 これを実現するには、DataList s `RepeatColumns` プロパティを行ごとに表示する列数に設定するだけです。 さらに、[DataList s `RepeatDirection`] プロパティを使用して、複数列の複数行のテーブルの内容を、左から右、上から下、または上下左右の左から右にレイアウトするかどうかを指定できます。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは John 加藤 u でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [次へ](nested-data-web-controls-cs.md)
