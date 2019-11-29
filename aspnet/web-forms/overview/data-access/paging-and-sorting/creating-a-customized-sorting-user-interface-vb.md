---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
title: カスタマイズされた並べ替えユーザーインターフェイスを作成する (VB) |Microsoft Docs
author: rick-anderson
description: 並べ替えられたデータの長い一覧を表示する場合は、区切り行を導入することによって関連データをグループ化すると非常に便利です。 このチュートリアルでは、次の方法について説明します。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: f3897a74-cc6a-4032-8f68-465f155e296a
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 66127630560141cd795beb15f525a7fba85f3993
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607347"
---
# <a name="creating-a-customized-sorting-user-interface-vb"></a>カスタマイズされた並べ替えユーザー インターフェイスを作成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_VB.exe)または[PDF のダウンロード](creating-a-customized-sorting-user-interface-vb/_static/datatutorial27vb1.pdf)

> 並べ替えられたデータの長い一覧を表示する場合は、区切り行を導入することによって関連データをグループ化すると非常に便利です。 このチュートリアルでは、このような並べ替えユーザーインターフェイスを作成する方法について説明します。

## <a name="introduction"></a>はじめに

並べ替えられた列に異なる値がいくつか存在する場合、並べ替えられたデータの長い一覧を表示すると、エンドユーザーは、正確な境界がどこにあるかを正確に区別することが困難になる可能性があります。 たとえば、データベースには81製品がありますが、カテゴリの選択肢は9つだけです (8 つの一意のカテゴリと `NULL` オプション)。 シーフードカテゴリに分類されている製品を調べることに関心のあるユーザーの場合を考えてみます。 1つの GridView 内の*すべて*の製品を一覧表示するページから、ユーザーは結果をカテゴリ別に並べ替えることができます。これにより、すべてのシーフード製品がまとめてグループ化されます。 カテゴリ別に並べ替えた後、ユーザーはリストを確認する必要があります。ここでは、シーフード製品の開始と終了を検索します。 結果はカテゴリ名のアルファベット順に並べ替えられるため、シーフード製品を見つけるのは困難ですが、グリッド内の項目の一覧を厳密にスキャンする必要があります。

並べ替えられたグループ間の境界を強調表示するために、多くの web サイトでは、そのようなグループ間に区切り記号を追加するユーザーインターフェイスを採用しています。 図1に示すような区切り記号を使用すると、特定のグループをすばやく検索し、その境界を識別したり、データ内に存在する別のグループを確認したりすることができます。

[各カテゴリグループを明確に識別 ![](creating-a-customized-sorting-user-interface-vb/_static/image2.png)](creating-a-customized-sorting-user-interface-vb/_static/image1.png)

**図 1**: 各カテゴリグループが明確に識別される ([クリックすると、フルサイズの画像が表示](creating-a-customized-sorting-user-interface-vb/_static/image3.png)されます)

このチュートリアルでは、このような並べ替えユーザーインターフェイスを作成する方法について説明します。

## <a name="step-1-creating-a-standard-sortable-gridview"></a>手順 1: 標準の並べ替え可能な GridView の作成

拡張並べ替えインターフェイスを提供するように GridView を拡張する方法については、まず、製品を一覧表示する、標準の並べ替え可能な GridView を作成してみましょう。 まず、`PagingAndSorting` フォルダーの [`CustomSortingUI.aspx`] ページを開きます。 GridView をページに追加し、その `ID` プロパティを `ProductList`に設定して、新しい ObjectDataSource にバインドします。 `ProductsBLL` クラス s `GetProducts()` メソッドを使用してレコードを選択するように ObjectDataSource を構成します。

次に、`ProductName`、`CategoryName`、`SupplierName`、および `UnitPrice` BoundFields と、廃止された CheckBoxField のみが含まれるように、GridView を構成します。 最後に、gridview のスマートタグの [並べ替えを有効にする] チェックボックスをオンにして、並べ替えをサポートするように GridView を構成します (または、`AllowSorting` プロパティを `true`に設定します)。 これらを [`CustomSortingUI.aspx`] ページに追加すると、宣言型のマークアップは次のようになります。

[!code-aspx[Main](creating-a-customized-sorting-user-interface-vb/samples/sample1.aspx)]

ブラウザーでこの時点までの進行状況を確認してください。 図2は、データがアルファベット順にカテゴリ別に並べ替えられている場合の、並べ替え可能な GridView を示しています。

[並べ替え可能な GridView のデータがカテゴリ別に並べ替えら ![](creating-a-customized-sorting-user-interface-vb/_static/image5.png)](creating-a-customized-sorting-user-interface-vb/_static/image4.png)

**図 2**: 並べ替え可能な GridView のデータがカテゴリ別に並べ替えられている ([クリックすると、フルサイズの画像が表示](creating-a-customized-sorting-user-interface-vb/_static/image6.png)されます)

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>手順 2: 区切り行を追加するための手法を調べる

汎用の並べ替え可能な GridView を完了すると、すべての一意の並べ替えられたグループの前に、GridView の区切り行を追加できるようになります。 しかし、このような行を GridView に挿入するにはどうすればよいでしょうか。 基本的に、GridView の行を反復処理し、並べ替えられた列の値の間の相違点を判断して、適切な区切り行を追加する必要があります。 この問題について考えてみると、ソリューションが GridView s `RowDataBound` イベントハンドラーのどこかにあることが自然であるように見えます。 「[データに基づくカスタム書式](../custom-formatting/custom-formatting-based-upon-data-vb.md)設定」のチュートリアルで説明したように、このイベントハンドラーは、行のデータに基づいて行レベルの書式設定を適用するときによく使用されます。 ただし、このイベントハンドラーからプログラムを使用して行を GridView に追加することはできないので、ここでは `RowDataBound` イベントハンドラーはソリューションではありません。 実際には、GridView の `Rows` コレクションは読み取り専用です。

GridView に行を追加するには、次の3つの選択肢があります。

- これらのメタデータ区切り行を、GridView にバインドされている実際のデータに追加します。
- GridView がデータにバインドされたら、追加の `TableRow` インスタンスを GridView s コントロールコレクションに追加します。
- GridView コントロールを拡張するカスタムサーバーコントロールを作成し、GridView の構造を構築するためのメソッドをオーバーライドします。

多くの web ページまたは複数の web サイトでこの機能が必要な場合は、カスタムサーバーコントロールを作成することをお勧めします。 ただし、かなりのコードが必要になり、GridView の内部動作の深さを徹底的に調査する必要があります。 このため、このチュートリアルではこのオプションについては検討しません。

その他の2つのオプションでは、GridView にバインドされている実際のデータに区切り行を追加し、バインドされた後に GridView のコントロールコレクションを操作して、問題を別の方法で攻撃し、議論を行います。

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>GridView にバインドされているデータに行を追加する

GridView がデータソースにバインドされると、データソースによって返されるレコードごとに `GridViewRow` が作成されます。 そのため、GridView にバインドする前に区切り記号レコードをデータソースに追加することによって、必要な区切り記号を挿入できます。 図3は、この概念を示しています。

![1つの手法では、データソースに区切り行を追加します。](creating-a-customized-sorting-user-interface-vb/_static/image7.png)

**図 3**: データソースに区切り行を追加する方法の1つ

区切り記号レコードという用語は、特別な区切り記号がないため、引用符で使用します。代わりに、データソース内の特定のレコードが通常のデータ行ではなく区切り記号として機能することを、何らかのフラグを付ける必要があります。 この例では、`ProductRows`で構成されている GridView に `ProductsDataTable` インスタンスをバインドします。 `CategoryID` プロパティを `-1` に設定して、レコードを区切り行としてフラグを設定することがあります (このような値は通常は存在できません)。

この手法を利用するには、次の手順を実行する必要があります。

1. GridView にバインドするデータをプログラムで取得する (`ProductsDataTable` インスタンス)
2. GridView の `SortExpression` と `SortDirection` のプロパティに基づいてデータを並べ替えます。
3. `ProductsDataTable`内の `ProductsRows` を反復処理して、並べ替えられた列の相違点を探します。
4. 各グループの境界で、`ProductsRow` インスタンスの区切り記号レコードを DataTable に挿入します。これには、`CategoryID` が `-1` に設定されているか (または、レコードを区切り記号レコードとしてマークするために決定された任意の指定) が含まれます。
5. 区切り行を挿入した後、プログラムによってデータを GridView にバインドします。

これらの5つの手順に加えて、GridView s `RowDataBound` イベントのイベントハンドラーも提供する必要があります。 ここでは、各 `DataRow` をチェックし、`CategoryID` 設定が `-1`れている区切り行であるかどうかを確認します。 その場合は、その書式設定や、セルに表示されるテキストを調整することをお勧めします。

並べ替えグループの境界を挿入するためにこの手法を使用する場合は、前に説明した以上の作業が必要になります。これは、GridView の `Sorting` イベントのイベントハンドラーを提供し、`SortExpression` と `SortDirection` の値を追跡する必要があるためです。

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>データバインドされた後の GridView s コントロールコレクションの操作

GridView にバインドする前にデータをメッセージングするのではなく、データが GridView にバインドされ*た後*に区切り行を追加できます。 データバインディングのプロセスは、GridView のコントロール階層を構築します。これは実際には、単に行のコレクションで構成される `Table` インスタンスであり、それぞれがセルのコレクションで構成されます。 具体的には、GridView のコントロールコレクションには、ルートの `Table` オブジェクト、GridView にバインドされている `DataSource` 内の各レコードの `GridViewRow` (`TableRow` クラスから派生した)、および `TableCell` 内の各データフィールドの各 `GridViewRow` インスタンス内の `DataSource`オブジェクトが含まれています。

各並べ替えグループの間に区切り記号を追加するには、作成されたコントロール階層を直接操作します。 ページがレンダリングされる時点までに、GridView のコントロール階層が最後に作成されたことを確信できます。 したがって、この方法は `Page` クラス s `Render` メソッドよりも優先されます。その時点で、必要な区切り行を含むように GridView の最後のコントロール階層が更新されます。 図4に、このプロセスを示します。

[別の手法を ![して、GridView のコントロール階層を操作します。](creating-a-customized-sorting-user-interface-vb/_static/image9.png)](creating-a-customized-sorting-user-interface-vb/_static/image8.png)

**図 4**: 別の方法で GridView のコントロール階層を操作する ([クリックすると、フルサイズのイメージが表示](creating-a-customized-sorting-user-interface-vb/_static/image10.png)されます)

このチュートリアルでは、この後者の方法を使用して、ユーザーエクスペリエンスの並べ替えをカスタマイズします。

> [!NOTE]
> このチュートリアルで説明するコードは、 [Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s ブログエントリに記載されている例に基づいており、 [GridView の並べ替えグループ化を使用してビットを再生](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)しています。

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>手順 3: GridView のコントロール階層に区切り行を追加する

GridView のコントロール階層が作成され、最後にそのページにアクセスするときに作成された後に、区切り行を追加するだけなので、ページライフサイクルの最後にこの追加を実行しますが、実際の GridView co) 階層が HTML にレンダリングされました。 これを実現できる最新のポイントは、`Page` クラス s `Render` イベントです。このイベントは、次のメソッドシグネチャを使用して、分離コードクラスでオーバーライドできます。

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample2.vb)]

`Page` クラス s original `Render` メソッドが呼び出されると `base.Render(writer)` ページ内の各コントロールがレンダリングされ、コントロール階層に基づいてマークアップが生成されます。 したがって、ページが表示されるように `base.Render(writer)`を呼び出す必要があります。また、`base.Render(writer)`を呼び出す前に GridView の s コントロール階層を操作して、表示される前に区切り行が GridView s コントロール階層に追加されている必要があります。

並べ替えグループヘッダーを挿入するには、まず、ユーザーがデータの並べ替えを要求したことを確認する必要があります。 既定では、GridView のコンテンツは並べ替えられないため、グループの並べ替えヘッダーを入力する必要はありません。

> [!NOTE]
> ページが最初に読み込まれるときに、GridView を特定の列で並べ替えるには、最初のページにアクセスしたときに GridView s `Sort` メソッドを呼び出します (以降のポストバックでは使用しません)。 これを実現するには、`if (!Page.IsPostBack)` 条件に含まれる `Page_Load` イベントハンドラーにこの呼び出しを追加します。 `Sort` 方法の詳細については、「[レポートデータのページングと並べ替え](paging-and-sorting-report-data-vb.md)」チュートリアルの情報を参照してください。

データが並べ替えられていることを前提として、次のタスクでは、データの並べ替えに使用された列を特定し、その列の値の相違点を検索する行をスキャンします。 次のコードでは、データが並べ替えられていることを確認し、データの並べ替えに使用されている列を見つけます。

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample3.vb)]

GridView がまだ並べ替えられていない場合は、GridView の `SortExpression` プロパティが設定されていません。 このため、このプロパティに値がある場合にのみ、区切り行を追加します。 その場合は、次に、データの並べ替えに使用された列のインデックスを決定する必要があります。 これは、GridView s `Columns` コレクションをループ処理し、`SortExpression` プロパティが GridView s `SortExpression` プロパティと等しい列を検索することで実現されます。 列 s インデックスに加えて、区切り行を表示するときに使用される `HeaderText` プロパティも取得します。

データの並べ替えに使用する列のインデックスを使用して、最後の手順として、GridView の行を列挙します。 行ごとに、並べ替えられた列の値が前の行の並べ替えられた列の値と異なるかどうかを判断する必要があります。 その場合は、新しい `GridViewRow` インスタンスをコントロール階層に挿入する必要があります。 これは、次のコードを使用して行います。

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample4.vb)]

このコードは、GridView のコントロール階層のルートにある `Table` オブジェクトをプログラムによって参照し、`lastValue`という名前の文字列変数を作成することによって開始します。 `lastValue` は、現在の行の並べ替えられた列の値と前の行の値を比較するために使用します。 次に、GridView s `Rows` コレクションが列挙され、行ごとに、並べ替えられた列の値が `currentValue` 変数に格納されます。

> [!NOTE]
> 特定の行の並べ替え済みの列の値を確認するには、セル s `Text` プロパティを使用します。 これは、BoundFields では適切に機能しますが、TemplateFields や CheckBoxFields などには適していません。 ここでは、後で代替 GridView フィールドを考慮する方法について説明します。

その後、`currentValue` と `lastValue` の変数が比較されます。 異なる場合は、コントロール階層に新しい区切り行を追加する必要があります。 これを行うには、`Table` オブジェクト s `Rows` コレクション内の `GridViewRow` のインデックスを調べ、新しい `GridViewRow` と `TableCell` インスタンスを作成してから、`TableCell` と `GridViewRow` をコントロール階層に追加します。

区切り行 s `TableCell` は、GridView の幅全体にまたがるように書式設定されており、`SortHeaderRowStyle` CSS クラスを使用して書式設定されています。また、並べ替えグループ名 (Category など) と group s 値 (飲料など) の両方が表示されるように `Text` プロパティを持っていることに注意してください。 最後に、`lastValue` が `currentValue`の値に更新されます。

並べ替えグループヘッダー行の書式を設定するために使用される CSS クラス `SortHeaderRowStyle` `Styles.css` ファイルで指定する必要があります。 好きなスタイル設定を自由に使用できます。ここでは、次のものを使用しました。

[!code-css[Main](creating-a-customized-sorting-user-interface-vb/samples/sample5.css)]

現在のコードでは、並べ替えインターフェイスは、任意の BoundField によって並べ替えを行うときに並べ替えグループヘッダーを追加します (図5を参照してください。これは、業者による並べ替え時のスクリーンショットを示しています)。 ただし、他のフィールドの種類 (CheckBoxField や TemplateField など) で並べ替える場合は、並べ替えグループのヘッダーが見つかりません (図6を参照)。

[並べ替えインターフェイスに、BoundFields による並べ替え時の並べ替えグループヘッダーが含まれる ![](creating-a-customized-sorting-user-interface-vb/_static/image12.png)](creating-a-customized-sorting-user-interface-vb/_static/image11.png)

**図 5**: 並べ替えインターフェイスには、boundfields によって並べ替えを行うときの並べ替えグループヘッダーが含まれます ([クリックしてフルサイズのイメージを表示](creating-a-customized-sorting-user-interface-vb/_static/image13.png)します)

[CheckBoxField の並べ替え時に並べ替えグループヘッダーがない ![](creating-a-customized-sorting-user-interface-vb/_static/image15.png)](creating-a-customized-sorting-user-interface-vb/_static/image14.png)

**図 6**: CheckBoxField の並べ替え時に並べ替えグループのヘッダーが表示されない ([クリックしてフルサイズの画像を表示する](creating-a-customized-sorting-user-interface-vb/_static/image16.png))

CheckBoxField での並べ替え時に並べ替えグループヘッダーがない理由は、現在、コードでは `TableCell` s `Text` プロパティのみを使用して、行ごとに並べ替えられた列の値を決定しているためです。 CheckBoxFields の場合、`TableCell` s `Text` プロパティは空の文字列です。代わりに、この値は、`TableCell` s `Controls` コレクション内に存在する CheckBox Web コントロールで使用できます。

BoundFields 以外のフィールド型を処理するには、`currentValue` 変数が割り当てられているコードを拡張して、`TableCell` s `Controls` コレクションにチェックボックスがあるかどうかを確認する必要があります。 `currentValue = gvr.Cells(sortColumnIndex).Text`を使用する代わりに、このコードを次のコードに置き換えます。

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample6.vb)]

このコードは、現在の行に対して並べ替えられた列 `TableCell` を調べて、`Controls` コレクションにコントロールがあるかどうかを確認します。 が存在し、最初のコントロールがチェックボックスの場合は、CheckBox s `Checked` プロパティに応じて、`currentValue` 変数が Yes または No に設定されます。 それ以外の場合、値は `TableCell` s `Text` プロパティから取得されます。 このロジックをレプリケートして、GridView に存在する可能性のある TemplateFields の並べ替えを処理することができます。

上記のコードを追加すると、廃止された CheckBoxField (図7を参照) によって並べ替えを行うときに、並べ替えグループのヘッダーが表示されるようになりました。

[CheckBoxField の並べ替え時に並べ替えグループのヘッダーが表示されるように ![](creating-a-customized-sorting-user-interface-vb/_static/image18.png)](creating-a-customized-sorting-user-interface-vb/_static/image17.png)

**図 7**: CheckBoxField の並べ替え時に並べ替えグループのヘッダーが表示される ([クリックしてフルサイズのイメージを表示する](creating-a-customized-sorting-user-interface-vb/_static/image19.png))

> [!NOTE]
> `NULL` データベースの値が `CategoryID`、`SupplierID`、または `UnitPrice` フィールドに含まれている製品がある場合、既定では、これらの値は GridView で空の文字列として表示されます。つまり、`NULL` 値を持つ製品の区切り行 s テキストは Category として読み取られます (つまり、category: 飲料ではなく、category の後に名前 ここに表示される値を使用する場合は、BoundFields [`NullDisplayText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx)に表示するテキストを設定するか、`currentValue` を separator 行 s `Text` プロパティに割り当てるときに、Render メソッドに条件付きステートメントを追加できます。

## <a name="summary"></a>要約

GridView には、並べ替えインターフェイスをカスタマイズするための多くの組み込みオプションは含まれていません。 ただし、低レベルのコードでは、GridView のコントロール階層を微調整して、よりカスタマイズされたインターフェイスを作成することができます。 このチュートリアルでは、並べ替え可能な GridView の並べ替えグループの区切り行を追加する方法を説明しました。これにより、個別のグループとそれらのグループの境界を簡単に識別できます。 カスタマイズされた並べ替えインターフェイスのその他の例については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/) s[の ASP.NET 2.0 GridView の並べ替えのヒントと秘訣](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx)に関するブログ記事をご覧ください。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](sorting-custom-paged-data-vb.md)
