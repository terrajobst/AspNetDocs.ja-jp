---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
title: DataList または Repeater コントロールでのデータの並べ替え (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、DataList と Repeater に並べ替えサポートを含める方法と、データを格納できる DataList または Repeater を構築する方法について説明します。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 97c13898-0741-45f9-b3fa-7540ab1679e6
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 81e07bec8569b9ee987dfaa84dec9eec95a2692f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465256"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-vb"></a>DataList または Repeater コントロールのデータを並べ替える (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_VB.exe)または[PDF のダウンロード](sorting-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial45vb1.pdf)

> このチュートリアルでは、DataList と Repeater に並べ替えサポートを含める方法と、データのページングと並べ替えが可能な DataList または Repeater を構築する方法について説明します。

## <a name="introduction"></a>はじめに

前の[チュートリアル](paging-report-data-in-a-datalist-or-repeater-control-vb.md)では、DataList にページングサポートを追加する方法を説明しています。 `PagedDataSource` オブジェクトを返す `ProductsBLL` クラス (`GetProductsAsPagedDataSource`) に新しいメソッドを作成しました。 Datalist または repeater にバインドされている場合、DataList または Repeater は、要求されたデータのページだけを表示します。 この手法は、組み込みの既定のページング機能を提供するために GridView、DetailsView、FormView コントロールによって内部的に使用されるものと似ています。

GridView には、ページングをサポートするだけでなく、すぐに使える並べ替えサポートも含まれています。 DataList も Repeater も、組み込みの並べ替え機能を提供しません。ただし、部分的なコードを使用して並べ替え機能を追加することもできます。 このチュートリアルでは、DataList と Repeater に並べ替えサポートを含める方法と、データのページングと並べ替えが可能な DataList または Repeater を構築する方法について説明します。

## <a name="a-review-of-sorting"></a>並べ替えのレビュー

「[レポートデータのページングと並べ替え](../paging-and-sorting/paging-and-sorting-report-data-vb.md)」チュートリアルで説明したように、GridView コントロールには、すぐに使用できる並べ替えサポートが用意されています。 各 GridView フィールドに関連付けられた `SortExpression`を持つことができます。これは、データの並べ替えに使用するデータフィールドを示します。 GridView の `AllowSorting` プロパティが `true`に設定されている場合、`SortExpression` プロパティ値を持つ各 GridView フィールドのヘッダーは LinkButton として表示されます。 ユーザーが特定の GridView フィールド s ヘッダーをクリックすると、ポストバックが発生し、クリックされたフィールド s `SortExpression`に従ってデータが並べ替えられます。

GridView コントロールには、データの並べ替えに使用される GridView フィールドの `SortExpression` を格納する `SortExpression` プロパティもあります。 また、`SortDirection` プロパティは、データを昇順または降順で並べ替えるかどうかを示します (ユーザーが特定の GridView フィールド s ヘッダーリンクを連続して2回クリックした場合、並べ替え順序が切り替わります)。

GridView がデータソースコントロールにバインドされている場合、その `SortExpression` を渡し、プロパティをデータソースコントロールに `SortDirection` します。 データソースコントロールはデータを取得し、指定された `SortExpression` および `SortDirection` プロパティに従ってデータを並べ替えます。 データを並べ替えると、データソースコントロールによってデータが GridView に返されます。

DataList または Repeater コントロールを使用してこの機能をレプリケートするには、次の操作を行う必要があります。

- 並べ替えインターフェイスを作成する
- 並べ替えの基準となるデータフィールドと、昇順と降順のどちらで並べ替えるかを忘れないでください。
- 特定のデータフィールドでデータを並べ替えるように ObjectDataSource に指示します。

ここでは、手順3と4の3つのタスクについて説明します。 ここでは、DataList または Repeater でページングと並べ替えの両方のサポートを含める方法について説明します。

## <a name="step-2-displaying-the-products-in-a-repeater"></a>手順 2: リピータでの製品の表示

並べ替えに関連する機能の実装について心配する前に、まずリピータコントロールに製品を一覧表示してみましょう。 まず、`PagingSortingDataListRepeater` フォルダーの [`Sorting.aspx`] ページを開きます。 Repeater コントロールを web ページに追加し、その `ID` プロパティを `SortableProducts`に設定します。 Repeater s スマートタグから `ProductsDataSource` という名前の新しい ObjectDataSource を作成し、`ProductsBLL` クラス s `GetProducts()` メソッドからデータを取得するように構成します。 [挿入]、[更新]、および [削除] の各タブのドロップダウンリストから [(なし)] オプションを選択します。

[ObjectDataSource を作成 ![、GetProductsAsPagedDataSource () メソッドを使用するように構成します。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**図 1**: ObjectDataSource を作成し、`GetProductsAsPagedDataSource()` メソッドを使用するように構成する ([クリックしてフルサイズのイメージを表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image3.png))

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)

**図 2**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズの画像を表示する](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image6.png))

DataList とは異なり、Visual Studio では、データソースにバインドした後、Repeater コントロールの `ItemTemplate` が自動的に作成されません。 さらに、この `ItemTemplate` を宣言的に追加する必要があります。これは、Repeater コントロール s スマートタグに、DataList s で見つかった [テンプレートの編集] オプションがないためです。 ここでは、製品名、供給業者、カテゴリを表示する前のチュートリアルと同じ `ItemTemplate` を使用します。

`ItemTemplate`を追加した後、リピータおよび ObjectDataSource の宣言マークアップは次のようになります。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample1.aspx)]

図3は、ブラウザーを使用して表示するときのこのページを示しています。

[各製品の名前、供給業者、およびカテゴリが ![表示されます。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**図 3**: 各製品の名前、供給業者、カテゴリが表示されます ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image9.png)されます)

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>手順 3: データの並べ替えを ObjectDataSource に指示する

リピータに表示されるデータを並べ替えるには、データの並べ替えに使用する並べ替え式を ObjectDataSource に通知する必要があります。 ObjectDataSource によってデータが取得される前に、まず[`Selecting` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)が発生します。これにより、並べ替え式を指定できるようになります。 `Selecting` イベントハンドラーに[`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)型のオブジェクトが渡されます。このオブジェクトには、 [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)型の[`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx)という名前のプロパティがあります。 `DataSourceSelectArguments` クラスは、データのコンシューマーからデータソースコントロールにデータ関連の要求を渡すように設計されており、 [`SortExpression` のプロパティ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)が含まれています。

並べ替え情報を ASP.NET ページから ObjectDataSource に渡すには、`Selecting` イベントのイベントハンドラーを作成し、次のコードを使用します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

*SortExpression*値には、データの並べ替えに使用するデータフィールドの名前 (ProductName など) を割り当てる必要があります。 並べ替えの方向に関連するプロパティはありません。そのため、データを降順に並べ替える場合は、 *sortExpression*値 (ProductName desc など) に文字列 DESC を追加します。

*SortExpression*に対してハードコーディングされた別の値を試し、ブラウザーで結果をテストしてみましょう。 図4に示すように、ProductName DESC を*sortExpression*として使用する場合、製品は名前の逆順でアルファベット順に並べ替えられます。

[製品の名前をアルファベットの逆順で並べ替える ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**図 4**: 製品はアルファベットの逆順で名前順に並べ替えられます ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image12.png)されます)

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>手順 4: 並べ替えインターフェイスを作成し、並べ替え式と方向を記憶する

GridView で並べ替えのサポートを有効にすると、並べ替え可能な各フィールドのヘッダーテキストが LinkButton に変換され、クリックすると、それに応じてデータが並べ替えられます。 このような並べ替えインターフェイスは、データが列に適切に配置されている GridView に適しています。 ただし、DataList コントロールと Repeater コントロールでは、別の並べ替えインターフェイスが必要です。 データの一覧に対する一般的な並べ替えインターフェイス (データのグリッドではなく) は、データの並べ替えに使用するフィールドを示すドロップダウンリストです。 このチュートリアルでは、このようなインターフェイスを実装します。

`SortableProducts` リピータの上に DropDownList Web コントロールを追加し、その `ID` プロパティを `SortBy`に設定します。 プロパティウィンドウから、`Items` プロパティの省略記号をクリックして、ListItem コレクションエディターを表示します。 `ProductName`、`CategoryName`、および `SupplierName` の各フィールドでデータを並べ替えるには `ListItem` s を追加します。 また、製品を名前で逆順にアルファベット順に並べ替える `ListItem` も追加します。

`ListItem` `Text` のプロパティを任意の値 (Name など) に設定できますが、`Value` プロパティはデータフィールドの名前 (ProductName など) に設定する必要があります。 結果を降順に並べ替えるには、ProductName DESC のように、データフィールド名に文字列 DESC を追加します。

![並べ替え可能な各データフィールドの ListItem を追加する](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**図 5**: 並べ替え可能な各データフィールドの `ListItem` を追加する

最後に、DropDownList の右側にボタン Web コントロールを追加します。 `ID` を `RefreshRepeater` に設定し、その `Text` プロパティを更新します。

`ListItem` s を作成して [更新] ボタンを追加すると、DropDownList とボタンの宣言構文は次のようになります。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

並べ替えの DropDownList が完了したら、次に ObjectDataSource s `Selecting` イベントハンドラーを更新して、ハードコーディングされた並べ替え式ではなく、選択した `SortBy``ListItem` s `Value` プロパティを使用するようにする必要があります。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample4.vb)]

この時点で、最初にページにアクセスしたときに、製品は最初に `ProductName` データフィールドによって並べ替えられます。これは、`SortBy` `ListItem` 既定で選択されているためです (図6を参照)。 [カテゴリ] や [更新] をクリックするなど、別の並べ替えオプションを選択すると、図7に示すように、ポストバックが発生し、カテゴリ名によってデータが再並べ替えされます。

[製品が最初に名前順に並べ替えられた ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)

**図 6**: 製品は最初に名前で並べ替えられます ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)されます)

[製品がカテゴリ別に並べ替えられた ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)

**図 7**: 製品がカテゴリ別に並べ替えられるようになりました ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)されます)

> [!NOTE]
> [最新の情報に更新] ボタンをクリックすると、Repeater のビューステートが無効になっているため、データが自動的に並べ替えられます。これにより、リピータは、すべてのポストバック時にそのデータソースに再バインドされます。 リピータのビューステートを有効にしたままにした場合、並べ替えのドロップダウンリストを変更しても、並べ替え順序に影響はありません。 これを解決するには、Refresh Button s `Click` イベントのイベントハンドラーを作成し、repeater をそのデータソースに再バインドします (Repeater s `DataBind()` メソッドを呼び出します)。

## <a name="remembering-the-sort-expression-and-direction"></a>並べ替え式と方向の記憶

並べ替えられていない関連のポストバックが発生する可能性があるページで、並べ替え可能な DataList または Repeater を作成する場合は、並べ替え式と方向をポストバック間で記録する必要があります。 たとえば、このチュートリアルでリピータを更新して、各製品に [削除] ボタンを追加したとします。 ユーザーが [削除] ボタンをクリックしたときに、選択した製品を削除するコードをいくつか実行し、そのデータを Repeater に再バインドします。 ポストバック間で並べ替えの詳細が保持されていない場合、画面に表示されるデータは元の並べ替え順序に戻ります。

このチュートリアルでは、DropDownList は並べ替え式と方向をビューステートに暗黙的に保存します。 別の並べ替えインターフェイスを使用していた場合、たとえば、さまざまな並べ替えオプションを提供する LinkButtons では、ポストバック間で並べ替え順序を記憶する必要があります。 これを実現するには、並べ替えパラメーターをページのビューステートに格納します。そのためには、querystring に sort パラメーターを含めるか、他の状態の永続化手法を使用します。

このチュートリアルの今後の例では、ページ s ビューステートに並べ替えの詳細を保持する方法を紹介します。

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>手順 5: 既定のページングを使用する DataList に並べ替えサポートを追加する

前の[チュートリアル](paging-report-data-in-a-datalist-or-repeater-control-vb.md)では、DataList を使用して既定のページングを実装する方法について説明します。 では、この前の例を拡張して、ページングされたデータを並べ替える機能を追加してみましょう。 まず、`PagingSortingDataListRepeater` フォルダーの `SortingWithDefaultPaging.aspx` と `Paging.aspx` のページを開きます。 [`Paging.aspx`] ページで、[ソース] ボタンをクリックして、ページの宣言型マークアップを表示します。 選択したテキストをコピーし (図8を参照)、`<asp:Content>` タグ間の `SortingWithDefaultPaging.aspx` の宣言型マークアップに貼り付けます。

[![、&lt;asp: Content&gt; Tags から SortingWithDefaultPaging に宣言マークアップをレプリケートします。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)

**図 8**: `Paging.aspx` から `SortingWithDefaultPaging.aspx` に `<asp:Content>` タグの宣言マークアップをレプリケートする ([クリックしてフルサイズのイメージを表示する](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image22.png))

宣言型マークアップをコピーしたら、`Paging.aspx` ページの分離コードクラスのメソッドとプロパティを `SortingWithDefaultPaging.aspx`の分離コードクラスにコピーします。 次に、ブラウザーで `SortingWithDefaultPaging.aspx` ページを表示します。 `Paging.aspx`と同じ機能と外観が表示されます。

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>既定のページングと並べ替え方法を含むように、製品の Bll を強化する

前のチュートリアルでは、`PagedDataSource` オブジェクトを返す `ProductsBLL` クラスの `GetProductsAsPagedDataSource(pageIndex, pageSize)` メソッドを作成しました。 この `PagedDataSource` オブジェクトには、(BLL s `GetProducts()` メソッドを使用して)*すべて*の製品が格納されていますが、DataList にバインドされている場合は、指定した*pageIndex*および*pageSize*入力パラメーターに対応するレコードのみが表示されます。

このチュートリアルの前半では、ObjectDataSource s `Selecting` イベントハンドラーから並べ替え式を指定して、並べ替えサポートを追加しました。 これは、ObjectDataSource が、`GetProducts()` メソッドによって返される `ProductsDataTable` のように、並べ替え可能なオブジェクトを返す場合に適しています。 ただし、`GetProductsAsPagedDataSource` メソッドによって返された `PagedDataSource` オブジェクトは、内部データソースの並べ替えをサポートしていません。 代わりに、`GetProducts()` メソッドから返された結果を `PagedDataSource`に配置する*前*に並べ替える必要があります。

これを実現するには、`ProductsBLL` クラスで新しいメソッドを作成し、`GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`します。 `GetProducts()` メソッドによって返される `ProductsDataTable` を並べ替えるには、既定の `DataTableView`の `Sort` プロパティを指定します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`GetProductsSortedAsPagedDataSource` メソッドは、前のチュートリアルで作成した `GetProductsAsPagedDataSource` メソッドとはわずかに異なります。 特に、`GetProductsSortedAsPagedDataSource` は追加の入力パラメーター `sortExpression` を受け取り、この値を `ProductDataTable` s `DefaultView`の `Sort` プロパティに割り当てます。 数行のコードでは、`PagedDataSource` object s DataSource に `ProductDataTable` s `DefaultView`が割り当てられています。

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>GetProductsSortedAsPagedDataSource メソッドを呼び出し、SortExpression 入力パラメーターの値を指定します。

`GetProductsSortedAsPagedDataSource` メソッドが完了したら、次の手順として、このパラメーターの値を指定します。 `SortingWithDefaultPaging.aspx` の ObjectDataSource は、現在、`GetProductsAsPagedDataSource` メソッドを呼び出すように構成されており、2つの入力パラメーターを、`SelectParameters` コレクションで指定されている2つの `QueryStringParameters`を介して渡します。 これらの2つの `QueryStringParameters` は、`GetProductsAsPagedDataSource` メソッドの*pageIndex*および*pageSize*パラメーターのソースが、`pageIndex` と `pageSize`のクエリ文字列フィールドから取得されることを示します。

新しい `GetProductsSortedAsPagedDataSource` メソッドを呼び出すように、ObjectDataSource s `SelectMethod` プロパティを更新します。 次に、新しい `QueryStringParameter` を追加して、クエリ文字列フィールド `sortExpression`から*sortExpression*入力パラメーターにアクセスできるようにします。 `QueryStringParameter` s `DefaultValue` を ProductName に設定します。

これらの変更を行った後、ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample6.aspx)]

この時点で、`SortingWithDefaultPaging.aspx` ページは結果を製品名でアルファベット順に並べ替えます (図9を参照)。 これは、既定では、ProductName の値が `GetProductsSortedAsPagedDataSource` method s *sortExpression*パラメーターとして渡されるためです。

[![既定では、結果は ProductName 別に並べ替えられます。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)

**図 9**: 既定では、結果は `ProductName` 順に並べ替えられます ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)されます)

`SortingWithDefaultPaging.aspx?sortExpression=CategoryName` などの `sortExpression` querystring フィールドを手動で追加すると、指定した `sortExpression`によって結果が並べ替えられます。 ただし、この `sortExpression` パラメーターは、データの別のページに移動するときに、querystring には含まれません。 実際には、[次へ] または [最後のページ] ボタンをクリックすると `Paging.aspx`に戻ります。 さらに、現在、並べ替えインターフェイスはありません。 ユーザーがページングされたデータの並べ替え順序を変更する唯一の方法は、クエリ文字列を直接操作することです。

## <a name="creating-the-sorting-interface"></a>並べ替えインターフェイスの作成

まず、`RedirectUser` メソッドを更新して、ユーザーを `Paging.aspx`ではなく `SortingWithDefaultPaging.aspx` に送信し、`sortExpression` の値を querystring に含める必要があります。 また、`SortExpression` プロパティという名前の読み取り専用のページレベルを追加する必要があります。 このプロパティは、前のチュートリアルで作成した `PageIndex` や `PageSize` プロパティと同様に、`sortExpression` querystring フィールドが存在する場合はその値を返し、それ以外の場合は既定値 (ProductName) を返します。

現在、`RedirectUser` メソッドでは、表示するページのインデックスを1つの入力パラメーターだけを受け取ることができます。 ただし、クエリ文字列に指定されている以外の並べ替え式を使用して、データの特定のページにユーザーをリダイレクトすることが必要になる場合があります。 ここでは、このページの並べ替えインターフェイスを作成します。これには、指定された列によってデータを並べ替えるための一連のボタン Web コントロールが含まれます。 これらのボタンのいずれかをクリックすると、適切な並べ替え式の値を渡してユーザーをリダイレクトすることになります。 この機能を提供するには、`RedirectUser` メソッドの2つのバージョンを作成します。 1つ目はページインデックスだけを表示し、2つ目はページインデックスと並べ替え式を受け入れます。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

このチュートリアルの最初の例では、DropDownList を使用して並べ替えインターフェイスを作成しました。 この例では、`ProductName`によって並べ替えを行うために、DataList 1 の上に配置された3つのボタン Web コントロールを使用します。1つは `CategoryName`用で、もう1つは `SupplierName`用です。 3つのボタン Web コントロールを追加し、`ID` プロパティと `Text` プロパティを適切に設定します。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample8.aspx)]

次に、それぞれの `Click` イベントハンドラーを作成します。 イベントハンドラーは、`RedirectUser` メソッドを呼び出し、適切な並べ替え式を使用してユーザーを最初のページに返す必要があります。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

最初にページにアクセスしたときに、製品名でデータがアルファベット順に並べ替えられます (図9を参照)。 [次へ] ボタンをクリックしてデータの2ページ目に進み、[カテゴリで並べ替え] ボタンをクリックします。 これにより、データの最初のページにカテゴリ名で並べ替えられます (図10を参照)。 同様に、[仕入先で並べ替え] ボタンをクリックすると、データの最初のページから、仕入先別にデータが並べ替えられます。 並べ替えの選択は、データがページングされるときに記憶されます。 図11では、カテゴリ別に並べ替えた後、データの13番目のページに進むとページが表示されます。

[製品がカテゴリ別に並べ替えられて ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)

**図 10**: 製品がカテゴリ別に並べ替えられている ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image28.png)されます)

[データのページング時に並べ替え式が記憶される ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image29.png)

**図 11**: データをページングするときに並べ替え式が記憶される ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image31.png)されます)

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>手順 6: リピータのレコードを使用したカスタムページング

DataList の例では、非効率的な既定のページング手法を使用して、手順5ページでデータを調べています。 大量のデータをページングする場合は、カスタムページングを使用する必要があります。 [大量のデータを効率的にページング](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)し、カスタムページング[データを並べ替える](../paging-and-sorting/sorting-custom-paged-data-vb.md)チュートリアルでは、カスタムページングを利用し、カスタムページングデータを並べ替えるために、BLL 内の既定のページングとカスタムページングの違いを調べました。 具体的には、次の2つのチュートリアルでは、`ProductsBLL` クラスに次の3つのメソッドを追加しました。

- `GetProductsPaged(startRowIndex, maximumRows)` は、 *Startrowindex*から始まり、 *maximumrows*を超えないレコードの特定のサブセットを返します。
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` は、指定された*sortExpression*入力パラメーターによって並べ替えられた特定のレコードのサブセットを返します。
- `TotalNumberOfProducts()` `Products` データベーステーブル内のレコードの合計数を示します。

これらのメソッドを使用すると、DataList または Repeater コントロールを使用してデータを効率的にページおよび並べ替えできます。 これを説明するために、まず、カスタムページングをサポートする Repeater コントロールを作成します。次に、並べ替え機能を追加します。

`PagingSortingDataListRepeater` フォルダーの [`SortingWithCustomPaging.aspx`] ページを開き、Repeater をページに追加します。その `ID` プロパティを [`Products`] に設定します。 Repeater s スマートタグから、`ProductsDataSource`という名前の新しい ObjectDataSource を作成します。 `ProductsBLL` クラス s `GetProductsPaged` メソッドからデータを選択するように構成します。

[Productbll クラス s GetProductsPaged 切れメソッドを使用するように ObjectDataSource を構成 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image32.png)

**図 12**: `ProductsBLL` クラス s `GetProductsPaged` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image34.png))

[更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定し、[次へ] ボタンをクリックします。 データソースの構成ウィザードによって、`GetProductsPaged` method s *Startrowindex*および*maximumrows*入力パラメーターのソースの入力が求められるようになりました。 実際には、これらの入力パラメーターは無視されます。 代わりに、このチュートリアルの最初のデモで*sortExpression*を指定したのと同じように、ObjectDataSource s `Selecting` イベントハンドラーの `Arguments` プロパティを通じて*Startrowindex*と*maximumrows*の値が渡されます。 このため、ウィザードの [ソース] ドロップダウンリストは [なし] のままにしておきます。

[[パラメーターのソース] を [なし] のままにし ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image35.png)

**図 13**: パラメーターソースを None に設定したままにする ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image37.png)されます)

> [!NOTE]
> ObjectDataSource s `EnablePaging` プロパティを `true`*に設定しないでください。* これにより、ObjectDataSource では、独自の*Startrowindex*パラメーターと*maximumrows*パラメーターが、`SelectMethod` の既存のパラメーターリストに自動的に追加されます。 `EnablePaging` プロパティは、GridView、DetailsView、または FormView コントロールにカスタムページングデータをバインドする場合に便利です。これは、これらのコントロールは、`EnablePaging` プロパティが `true`場合にのみ使用できる ObjectDataSource からの特定の動作を想定しているためです。 DataList と Repeater のページングサポートを手動で追加する必要があるため、このプロパティは `false` (既定) に設定したままにします。 ASP.NET ページ内で必要な機能を直接焼き付けるします。

最後に、製品名、カテゴリ、および供給業者が表示されるように、リピータの `ItemTemplate` を定義します。 これらの変更が完了すると、Repeater および ObjectDataSource の宣言構文は次のようになります。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample10.aspx)]

ブラウザーでページにアクセスして、レコードが返されないことを確認します。 これは、 *Startrowindex*および*maximumrows*パラメーター値をまだ指定していないためです。したがって、値0は両方に渡されます。 これらの値を指定するには、ObjectDataSource s `Selecting` イベントのイベントハンドラーを作成し、これらのパラメーター値をプログラムによって、0および5のハードコーディングされた値に設定します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample11.vb)]

この変更により、ブラウザーで表示したときに、最初の5つの製品がページに表示されます。

[最初の5つのレコードが表示される ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image38.png)

**図 14**: 最初の5つのレコードが表示される ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image40.png)されます)

> [!NOTE]
> 図14に記載されている製品は、効率的なカスタムページングクエリを実行する `GetProductsPaged` ストアドプロシージャが `ProductName`によって結果を並べ替えるため、製品名で並べ替えられています。

ユーザーがページをステップ実行できるようにするには、開始行インデックスと最大行数を追跡し、ポストバック全体でこれらの値を記憶しておく必要があります。 既定のページングの例では、querystring フィールドを使用してこれらの値を保持していました。このデモでは、この情報をページ s ビューステートに保持します。 次の2つのプロパティを作成します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample12.vb)]

次に、選択したイベントハンドラーのコードを更新します。これにより、0と5のハードコーディングされた値の代わりに、`StartRowIndex` と `MaximumRows` のプロパティが使用されるようになります。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample13.vb)]

この時点で、ページには最初の5つのレコードのみが表示されます。 ただし、これらのプロパティが設定されていれば、ページングインターフェイスを作成する準備が整います。

## <a name="adding-the-paging-interface"></a>ページングインターフェイスの追加

では、既定のページングの例で使用されている最初、前、次の最後のページングインターフェイスと同じものを使用します。これには、表示されているデータページと合計ページ数を表示するラベル Web コントロールが含まれます。 Repeater の下に、4つのボタンの Web コントロールとラベルを追加します。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample14.aspx)]

次に、4つのボタンの `Click` イベントハンドラーを作成します。 これらのボタンのいずれかをクリックすると、`StartRowIndex` を更新して、データをリピータに再バインドする必要があります。 [最初]、[前へ]、[次へ] の各ボタンのコードは単純ですが、最後のボタンの場合、最後のページのデータの先頭行のインデックスはどのように決定しますか。 このインデックスを計算し、次のボタンと最後のボタンを有効にする必要があるかどうかを判断できるようにするには、合計でページングされているレコードの数を把握しておく必要があります。 これは、`ProductsBLL` クラス s `TotalNumberOfProducts()` メソッドを呼び出すことによって判断できます。 `TotalNumberOfProducts()` メソッドの結果を返す `TotalRowCount` という名前の読み取り専用のページレベルのプロパティを作成します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample15.vb)]

このプロパティを使用して、最後のページの開始行インデックスを決定できるようになりました。 具体的には、`TotalRowCount`-1 を `MaximumRows`で除算し、`MaximumRows`を乗算した結果の整数が返されます。 次に、4つのページングインターフェイスボタンの `Click` イベントハンドラーを記述できるようになりました。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample16.vb)]

最後に、データの最初のページを表示するときにページングインターフェイスの最初のボタンと前のボタンを無効にし、最後のページを表示するときに [次へ] と [最後] のボタンを無効にする必要があります。 これを実現するには、ObjectDataSource s `Selecting` イベントハンドラーに次のコードを追加します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample17.vb)]

これらの `Click` イベントハンドラーを追加し、現在の開始行インデックスに基づいてページングインターフェイス要素を有効または無効にするコードを追加した後、ブラウザーでページをテストします。 図15に示すように、最初にページにアクセスしたときに、最初のボタンと前のボタンが無効になります。 [次へ] をクリックすると、データの2ページ目が表示され、[最後] をクリックすると最終ページが表示されます (図16と17を参照)。 データの最後のページを表示すると、[次へ] と [最後] の両方のボタンが無効になります。

[製品の最初のページを表示しているときに、前のボタンと最後のボタンが無効に ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image41.png)

**図 15**: 製品の最初のページを表示するときに、前のボタンと最後のボタンが無効になる ([クリックしてフルサイズの画像を表示する](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image43.png))

[![製品の2番目のページが表示されます。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image44.png)

**図 16**: 製品の2番目のページが表示される ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image46.png)されます)

[最後の ![クリックすると、最後のデータページが表示されます](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image47.png)

**図 17**: [最後[へ] をクリックする](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image49.png)と、データの最終ページが表示されます (クリックすると、フルサイズの画像が表示されます)

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>手順 7: カスタムのページリピータを使用した並べ替えサポートの追加

カスタムページングが実装されたので、並べ替えサポートを追加する準備ができました。 `ProductsBLL` クラス s `GetProductsPagedAndSorted` メソッドには `GetProductsPaged`と同じ*Startrowindex*および*maximumrows*入力パラメーターがありますが、追加の*sortExpression*入力パラメーターが許可されています。 `SortingWithCustomPaging.aspx`から `GetProductsPagedAndSorted` メソッドを使用するには、次の手順を実行する必要があります。

1. ObjectDataSource s `SelectMethod` プロパティを `GetProductsPaged` から `GetProductsPagedAndSorted`に変更します。
2. *SortExpression* `Parameter` オブジェクトを ObjectDataSource s `SelectParameters` コレクションに追加します。
3. ページ s ビューステートを通じてポストバック間で値を永続化する、ページレベルのプライベート `SortExpression` プロパティを作成します。
4. ObjectDataSource s `Selecting` イベントハンドラーを更新して、ObjectDataSource s *sortExpression*パラメーターにページレベル `SortExpression` プロパティの値を割り当てます。
5. 並べ替えインターフェイスを作成します。

最初に、ObjectDataSource s `SelectMethod` プロパティを更新し、 *sortExpression* `Parameter`を追加します。 *SortExpression* `Parameter` s `Type` プロパティが `String`に設定されていることを確認します。 これらの最初の2つのタスクを完了すると、ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample18.aspx)]

次に、値がビューステートにシリアル化されるページレベルの `SortExpression` プロパティが必要です。 並べ替え式の値が設定されていない場合は、ProductName を既定値として使用します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample19.vb)]

ObjectDataSource によって `GetProductsPagedAndSorted` メソッドが呼び出される前に、 *sortExpression* `Parameter` を `SortExpression` プロパティの値に設定する必要があります。 `Selecting` イベントハンドラーで、次のコード行を追加します。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample20.vb)]

残りのことは、並べ替えインターフェイスを実装することだけです。 最後の例で行ったように、では、ユーザーが製品名、カテゴリ、または業者別に結果を並べ替えられるようにする3つのボタン Web コントロールを使用して、並べ替えインターフェイスを実装しています。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample21.aspx)]

これら3つのボタンコントロールの `Click` イベントハンドラーを作成します。 イベントハンドラーで、`StartRowIndex` を0にリセットし、`SortExpression` を適切な値に設定して、データをリピータに再バインドします。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample22.vb)]

これで完了です。 カスタムページングと並べ替えを実装するための手順はいくつかありましたが、これらの手順は、既定のページングに必要な手順とよく似ていました。 図18に、カテゴリ別に並べ替えられたデータの最後のページを表示する場合の製品を示します。

[データの最後のページ ![カテゴリ別に並べ替えられて表示されます。](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image50.png)

**図 18**: データの最後のページがカテゴリ別に並べ替えられて表示される ([クリックすると、フルサイズの画像が表示](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image52.png)されます)

> [!NOTE]
> 前の例では、supplier SupplierName による並べ替えが並べ替え式として使用されていました。 ただし、カスタムページング実装の場合は、CompanyName を使用する必要があります。 これは、カスタムページング `GetProductsPagedAndSorted` を実装するストアドプロシージャが `ROW_NUMBER()` キーワードに並べ替え式を渡す場合、`ROW_NUMBER()` キーワードには別名ではなく実際の列名が必要であるためです。 そのため、並べ替え式の `SELECT` クエリ (`SupplierName`) で使用される別名ではなく、`CompanyName` (`Suppliers` テーブルの列名) を使用する必要があります。

## <a name="summary"></a>まとめ

DataList も Repeater も、組み込みの並べ替えサポートを提供していませんが、コードとカスタムの並べ替えインターフェイスを使用して、そのような機能を追加することができます。 並べ替えを実装するときにページングではなく、ObjectDataSource s `Select` メソッドに渡される `DataSourceSelectArguments` オブジェクトを使用して並べ替え式を指定できます。 この `DataSourceSelectArguments` オブジェクト s `SortExpression` プロパティは、ObjectDataSource s `Selecting` イベントハンドラーで割り当てることができます。

既にページングがサポートされている DataList または Repeater に並べ替え機能を追加するには、並べ替え式を受け取るメソッドを含むようにビジネスロジックレイヤーをカスタマイズするのが最も簡単な方法です。 この情報は、ObjectDataSource s `SelectParameters`のパラメーターを通じて渡すことができます。

このチュートリアルでは、DataList コントロールと Repeater コントロールを使用したページングと並べ替えの検査を完了します。 次の最後のチュートリアルでは、カスタムのユーザーが開始した機能を項目ごとに提供するために、DataList および Repeater のテンプレートにボタン Web コントロールを追加する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は David, u です。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
