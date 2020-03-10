---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: FormView のテンプレートを使用する (VB) |Microsoft Docs
author: rick-anderson
description: DetailsView とは異なり、FormView はフィールドで構成されていません。 代わりに、FormView がテンプレートを使用して表示されます。 このチュートリアルでは、「F...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: cafe47cf5766bb14503852ec6e9f305d1e6d426f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426580"
---
# <a name="using-the-formviews-templates-vb"></a>FormView のテンプレートの使用 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe)または[PDF のダウンロード](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> DetailsView とは異なり、FormView はフィールドで構成されていません。 代わりに、FormView がテンプレートを使用して表示されます。 このチュートリアルでは、FormView コントロールを使用してデータをより厳密に表示する方法について説明します。

## <a name="introduction"></a>はじめに

最後の2つのチュートリアルでは、TemplateFields を使用して GridView および DetailsView コントロールの出力をカスタマイズする方法を説明しました。 TemplateFields を使用すると、特定のフィールドの内容を高度にカスタマイズすることができますが、最終的には、GridView と DetailsView の両方にグリッド形式の外観が設定されます。 多くのシナリオでは、グリッドに似たレイアウトが理想的ですが、より滑らかで低い表示が必要になる場合もあります。 1つのレコードを表示する場合は、FormView コントロールを使用して、このような流体レイアウトを行うことができます。

DetailsView とは異なり、FormView はフィールドで構成されていません。 FormView に BoundField または TemplateField を追加することはできません。 代わりに、FormView がテンプレートを使用して表示されます。 FormView は、1つの TemplateField を含む DetailsView コントロールと考えることができます。 FormView は、次のテンプレートをサポートしています。

- FormView に表示される特定のレコードを表示するために使用 `ItemTemplate`
- 省略可能なヘッダー行を指定するために使用 `HeaderTemplate`
- オプションのフッター行を指定するために使用 `FooterTemplate`
- `EmptyDataTemplate` FormView の `DataSource` にレコードがない場合は、コントロールのマークアップを表示するために、`ItemTemplate` の代わりに `EmptyDataTemplate` が使用されます。
- ページングが有効になっている FormViews のページングインターフェイスをカスタマイズするために `PagerTemplate` を使用できます。
- `EditItemTemplate` / `InsertItemTemplate`、そのような機能をサポートする FormViews の編集インターフェイスをカスタマイズしたり、インターフェイスを挿入したりするために使用されます。

このチュートリアルでは、FormView コントロールを使用して、より厳密でない製品の表示を表示します。 FormView の `ItemTemplate` では、name、category、supplier などのフィールドを持つのではなく、ヘッダー要素と `<table>` の組み合わせを使用してこれらの値が表示されます (図1を参照)。

[DetailsView に表示されるグリッドに似たレイアウトから FormView が分割さ ![](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**図 1**: FormView は、DetailsView に表示されるグリッドに似たレイアウトから分割します ([クリックすると、フルサイズの画像が表示](using-the-formview-s-templates-vb/_static/image3.png)されます)。

## <a name="step-1-binding-the-data-to-the-formview"></a>手順 1: データを FormView にバインドする

[`FormView.aspx`] ページを開き、[ツールボックス] から FormView をデザイナーにドラッグします。 最初に FormView を追加すると、`ItemTemplate` が必要であることを示す灰色のボックスが表示されます。

[![ItemTemplate が指定されるまで、FormView をデザイナーでレンダリングできません。](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**図 2**: `ItemTemplate` が指定されるまで、FormView をデザイナーでレンダリングできない ([クリックしてフルサイズのイメージを表示](using-the-formview-s-templates-vb/_static/image6.png))

`ItemTemplate` は、(宣言構文を使用して) 手動で作成することも、デザイナーを使用してデータソースコントロールに FormView をバインドすることによって自動作成することもできます。 この自動作成 `ItemTemplate` には、各フィールドの名前と、`Text` プロパティがフィールドの値にバインドされているラベルコントロールを一覧表示する HTML が含まれています。 この方法では、データソースコントロールによって返される各データフィールドの入力コントロールが入力された `InsertItemTemplate` と `EditItemTemplate`も自動作成されます。

テンプレートを自動作成する場合は、FormView のスマートタグから、`ProductsBLL` クラスの `GetProducts()` メソッドを呼び出す新しい ObjectDataSource コントロールを追加します。 これにより、`ItemTemplate`、`InsertItemTemplate`、および `EditItemTemplate`を含む FormView が作成されます。 編集または挿入をサポートする FormView を作成する必要がないため、ソースビューから `InsertItemTemplate` と `EditItemTemplate` を削除します。 次に、`ItemTemplate` 内のマークアップをオフにして、正常に動作するようにクリーンなスレートを作成します。

`ItemTemplate` を手動で作成する場合は、ObjectDataSource をツールボックスからデザイナーにドラッグして、ObjectDataSource を追加して構成できます。 ただし、FormView のデータソースをデザイナーから設定しないでください。 代わりに、ソースビューにアクセスし、FormView の `DataSourceID` プロパティを ObjectDataSource の `ID` 値に手動で設定します。 次に、`ItemTemplate`を手動で追加します。

どの方法を採用するかにかかわらず、この時点で、FormView の宣言型のマークアップは次のようになります。

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

FormView のスマートタグの [ページングを有効にする] チェックボックスをオンにします。これにより、`AllowPaging="True"` の属性が FormView の宣言構文に追加されます。 また、`EnableViewState` プロパティを False に設定します。

## <a name="step-2-defining-theitemtemplates-markup"></a>手順 2:`ItemTemplate`のマークアップの定義

FormView が ObjectDataSource コントロールにバインドされ、ページングをサポートするように構成されている状態で、`ItemTemplate`のコンテンツを指定する準備ができました。 このチュートリアルでは、製品名を `<h3>` 見出しに表示してみましょう。 その後、HTML `<table>` を使用して、4列のテーブルに残りの製品プロパティを表示します。ここでは、1番目と3番目の列にプロパティ名が一覧表示され、2番目と4番目の列の値が一覧表示されます。

このマークアップは、デザイナーの FormView のテンプレート編集インターフェイスを通じて入力するか、宣言構文を使用して手動で入力できます。 テンプレートを使用する場合は、通常、宣言型の構文を直接操作する方が簡単ですが、最も使い慣れた手法を自由に使用できます。

次のマークアップは、`ItemTemplate`の構造が完了した後の FormView 宣言マークアップを示しています。

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

たとえば、データバインド構文 `<%# Eval("ProductName") %>`が、テンプレートの出力に直接挿入されることがわかります。 つまり、ラベルコントロールの `Text` プロパティに割り当てる必要はありません。 たとえば、`<h3><%# Eval("ProductName") %></h3>`を使用して `<h3>` 要素に `ProductName` 値が表示されているとします。この場合、製品の Chai は `<h3>Chai</h3>`として表示されます。

`ProductPropertyLabel` および `ProductPropertyValue` の CSS クラスは、`<table>`内の製品プロパティの名前と値のスタイルを指定するために使用されます。 これらの CSS クラスは `Styles.css` で定義されており、プロパティ名が太字で右に配置され、プロパティ値に右余白が追加されます。

FormView で使用できる CheckBoxFields がないため、`Discontinued` 値をチェックボックスとして表示するには、独自の CheckBox コントロールを追加する必要があります。 `Enabled` プロパティが False に設定されており、読み取り専用になっています。チェックボックスの `Checked` プロパティは `Discontinued` データフィールドの値にバインドされています。

`ItemTemplate` 完了すると、製品情報がより滑らかな方法で表示されます。 最後のチュートリアルの DetailsView 出力 (図 3) と、このチュートリアルの FormView によって生成される出力を比較します (図 4)。

[固定の DetailsView 出力を ![する](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**図 3**: 固定の DetailsView 出力 ([クリックすると、フルサイズの画像が表示](using-the-formview-s-templates-vb/_static/image9.png)されます)

[流体 FormView 出力の ![](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**図 4**: 流体の FormView 出力 ([クリックすると、フルサイズの画像が表示](using-the-formview-s-templates-vb/_static/image12.png)されます)

## <a name="summary"></a>まとめ

GridView コントロールと DetailsView コントロールの出力は TemplateFields を使用してカスタマイズできますが、どちらもデータをグリッドのような boxy 形式で表示します。 1つのレコードをより固定されていないレイアウトで表示する必要がある場合は、FormView が最適な選択肢です。 DetailsView と同様に、FormView は `DataSource`から1つのレコードを表示しますが、DetailsView とは異なり、テンプレートだけで構成されており、フィールドはサポートされていません。

このチュートリアルで説明したように、FormView では、1つのレコードを表示するときに、より柔軟なレイアウトを使用できます。 今後のチュートリアルでは、DataList コントロールと Repeater コントロールについて説明します。このコントロールは、フォームビューと同じレベルの柔軟性を提供しますが、複数のレコード (GridView など) を表示できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は E.R. でした Gilmore. 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](using-templatefields-in-the-detailsview-control-vb.md)
> [次へ](displaying-summary-information-in-the-gridview-s-footer-vb.md)
