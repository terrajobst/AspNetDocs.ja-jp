---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: DataList または Repeater コントロールのレポートデータのページングC#() |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、自動ページングまたは並べ替えをサポートしているのではなく、DataList または Repeater にページングサポートを追加する方法についても説明してい,...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 16686c7e41926698c0da9c60d3cf26e858f5daca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78503260"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>DataList または Repeater コントロールのレポート データをページングする (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe)または[PDF のダウンロード](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> このチュートリアルでは、自動ページングまたは並べ替えをサポートしているのではなく、DataList または Repeater にページングサポートを追加する方法についても説明します。

## <a name="introduction"></a>はじめに

ページングと並べ替えは、オンラインアプリケーションにデータを表示するときの2つの非常に一般的な機能です。 たとえば、オンライン書店で ASP.NET books を検索する場合、このような書籍は多数存在する可能性がありますが、検索結果を一覧表示するレポートでは、1ページあたり10件の一致のみが一覧表示されます。 さらに、結果はタイトル、価格、ページ数、作成者名などで並べ替えることができます。 「[レポートデータのページングと並べ替え](../paging-and-sorting/paging-and-sorting-report-data-cs.md)」のチュートリアルで説明したように、GridView、DetailsView、および FormView コントロールには、チェックボックスの目盛りで有効にできる組み込みのページングサポートが用意されています。 GridView には、並べ替えのサポートも含まれています。

残念ながら、自動ページングや並べ替えはサポートされていません。 このチュートリアルでは、DataList または Repeater にページングサポートを追加する方法について説明します。 ページングインターフェイスを手動で作成し、適切なレコードページを表示し、ポストバック間でアクセスされているページを記憶しておく必要があります。 この処理には GridView、DetailsView、または FormView よりも時間とコードが必要ですが、DataList と Repeater では、より柔軟なページングとデータ表示インターフェイスを使用できます。

> [!NOTE]
> このチュートリアルでは、ページングのみを中心に説明します。 次のチュートリアルでは、並べ替え機能の追加に注目します。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>手順 1: ページングと並べ替えのチュートリアル Web ページの追加

このチュートリアルを開始する前に、まず、このチュートリアルに必要な ASP.NET ページと次のページを追加してみましょう。 まず、`PagingSortingDataListRepeater`という名前のプロジェクトに新しいフォルダーを作成します。 次に、次の5つの ASP.NET ページをこのフォルダーに追加します。マスターページ `Site.master`を使用するようにすべてのページを構成します。

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![PagingSortingDataListRepeater フォルダーを作成し、チュートリアル ASP.NET ページを追加します。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**図 1**: `PagingSortingDataListRepeater` フォルダーを作成し、チュートリアル ASP.NET ページを追加する

次に、[`Default.aspx`] ページを開き、`SectionLevelTutorialListing.ascx` ユーザーコントロールを `UserControls` フォルダーからデザイン画面にドラッグします。 このユーザーコントロールは、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-cs.md)チュートリアルで作成したもので、サイトマップを列挙し、現在のセクションに記載されているチュートリアルを箇条書きの一覧に表示します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)されます)

箇条書きの一覧に、作成するページングと並べ替えのチュートリアルが表示されるようにするには、サイトマップに追加する必要があります。 `Web.sitemap` ファイルを開き、DataList サイトマップノードマークアップを使用して編集および削除の後に、次のマークアップを追加します。

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]

![新しい ASP.NET ページを含めるようにサイトマップを更新する](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**図 3**: 新しい ASP.NET ページを含めるようにサイトマップを更新する

## <a name="a-review-of-paging"></a>ページングのレビュー

前のチュートリアルでは、GridView、DetailsView、および FormView コントロールのデータをページ表示する方法を説明しました。 これら3つのコントロールは、*既定のページング*と呼ばれる単純な形式のページングを提供します。これは、control s スマートタグの [ページングを有効にする] オプションをオンにするだけで実装できます。 既定のページングでは、最初のページにアクセスしたときにデータのページが要求されるたびに、またはユーザーが別のデータページに移動したときに、GridView、DetailsView、または FormView コントロールが ObjectDataSource からの*すべて*のデータを再要求します。 次に、要求されたページインデックスとページごとに表示するレコードの数を指定して、表示する特定のレコードのセットを切り取ります。 既定のページングについては、「[レポートデータのページングと並べ替え](../paging-and-sorting/paging-and-sorting-report-data-cs.md)」のチュートリアルで説明しました。

既定のページングでは各ページのすべてのレコードが再要求されるため、十分に大量のデータをページングする場合は実用的ではありません。 たとえば、ページサイズが10の5万レコードのページングを考えてみます。 ユーザーが新しいページに移動するたびに、10個のレコードが1つしか表示されない場合でも、すべての5万レコードをデータベースから取得する必要があります。

*カスタムページング*は、要求されたページに表示するレコードの正確なサブセットのみを取得することで、既定のページングのパフォーマンスの問題を解決します。 カスタムページングを実装する場合は、正しいレコードセットだけを効率的に返す SQL クエリを記述する必要があります。 このようなクエリを作成する方法については、「[大量のデータを使用](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)した効率的なページング」チュートリアルで SQL Server 2005 s new [`ROW_NUMBER()` キーワード](http://www.4guysfromrolla.com/webtech/010406-1.shtml)を使用して作成する方法について説明しました。

DataList または Repeater コントロールに既定のページングを実装するには、 [`PagedDataSource` クラス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx)を、内容がページングされている `ProductsDataTable` のラッパーとして使用できます。 `PagedDataSource` クラスには、任意の列挙可能なオブジェクトに割り当てることができる `DataSource` プロパティと、1ページあたりのレコード数と現在のページインデックスを示す[`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx)および[`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx)プロパティがあります。 これらのプロパティを設定した後は、任意のデータ Web コントロールのデータソースとして `PagedDataSource` を使用できます。 列挙された `PagedDataSource`は、`PageSize` および `CurrentPageIndex` プロパティに基づいて、内部 `DataSource` のレコードの適切なサブセットのみを返します。 図4は、`PagedDataSource` クラスの機能を示しています。

![PagedDataSource は、ページング可能なインターフェイスを使用して列挙可能なオブジェクトをラップします。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**図 4**: `PagedDataSource` は、ページング可能なインターフェイスを使用して列挙可能なオブジェクトをラップする

`PagedDataSource` オブジェクトは、ビジネスロジック層から直接作成して構成し、ObjectDataSource を介して DataList または Repeater にバインドするか、ASP.NET ページの分離コードクラスで直接作成して構成することができます。 後者の方法を使用する場合は、ObjectDataSource を使用して済ませるする必要があります。代わりに、ページングされたデータを DataList または Repeater にプログラムでバインドします。

`PagedDataSource` オブジェクトには、カスタムページングをサポートするプロパティもあります。 ただし、カスタムページングには `PagedDataSource` を使用しないようにすることができます。これは、表示する正確なレコードを返すカスタムページング用にデザインされた `ProductsBLL` クラスに既に BLL メソッドがあるためです。

このチュートリアルでは、適切に構成された `PagedDataSource` オブジェクトを返す `ProductsBLL` クラスに新しいメソッドを追加することによって、DataList に既定のページングを実装する方法について説明します。 次のチュートリアルでは、カスタムページングの使用方法について説明します。

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>手順 2: ビジネスロジック層に既定のページングメソッドを追加する

現在、`ProductsBLL` クラスには、すべての製品情報 `GetProducts()` を返すメソッドと、開始インデックス `GetProductsPaged(startRowIndex, maximumRows)`で製品の特定のサブセットを返すためのメソッドがあります。 既定のページングでは、GridView、DetailsView、FormView コントロールはすべて、`GetProducts()` メソッドを使用してすべての製品を取得しますが、内部的に `PagedDataSource` を使用して、レコードの正しいサブセットのみを表示します。 DataList コントロールと Repeater コントロールを使用してこの機能をレプリケートするには、この動作を模倣する新しいメソッドを BLL に作成します。

2つの整数入力パラメーターを受け取る `GetProductsAsPagedDataSource` という名前の `ProductsBLL` クラスにメソッドを追加します。

- 表示するページのインデックスを `pageIndex` し、0でインデックスを作成します。
- ページごとに表示するレコードの数 `pageSize` ます。

`GetProductsAsPagedDataSource` は、`GetProducts()`から*すべて*のレコードを取得することによって開始されます。 次に、`PagedDataSource` オブジェクトを作成し、その `CurrentPageIndex` と `PageSize` プロパティを、渡された `pageIndex` と `pageSize` パラメーターの値に設定します。 メソッドは、この構成された `PagedDataSource`を返すことによって終了します。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>手順 3: 既定のページングを使用して DataList に製品情報を表示する

`ProductsBLL` クラスに `GetProductsAsPagedDataSource` メソッドを追加して、既定のページングを提供する DataList または Repeater を作成できるようになりました。 まず、`PagingSortingDataListRepeater` フォルダーの [`Paging.aspx`] ページを開き、DataList をツールボックスからデザイナーにドラッグして、DataList s `ID` プロパティを `ProductsDefaultPaging`に設定します。 DataList s スマートタグから `ProductsDefaultPagingDataSource` という名前の新しい ObjectDataSource を作成し、`GetProductsAsPagedDataSource` メソッドを使用してデータを取得するように構成します。

[ObjectDataSource を作成 ![、GetProductsAsPagedDataSource () メソッドを使用するように構成します。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**図 5**: ObjectDataSource を作成し、`GetProductsAsPagedDataSource` `()` メソッドを使用するように構成する ([クリックしてフルサイズのイメージを表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png)する)

[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**図 6**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズの画像を表示する](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))

`GetProductsAsPagedDataSource` メソッドでは2つの入力パラメーターが必要であるため、これらのパラメーター値のソースを要求するプロンプトが表示されます。

ページインデックスとページサイズの値は、ポストバック間で記録する必要があります。 ビューステートに格納したり、クエリ文字列に永続化したり、セッション変数に格納したり、他の方法を使用して記憶したりすることができます。 このチュートリアルでは、querystring を使用します。これには、データの特定のページにブックマークを設定することができるという利点があります。

特に、`pageIndex` パラメーターと `pageSize` パラメーターには、クエリ文字列フィールドの pageIndex と pageSize をそれぞれ使用します (図7を参照)。 ユーザーが最初にこのページにアクセスしたときに querystring 値が表示されないため、これらのパラメーターの既定値を設定してください。 `pageIndex`には、既定値を 0 (データの最初のページが表示されます) に設定し、`pageSize` s の既定値を4に設定します。

[![、pageIndex および pageSize パラメーターのソースとしてクエリ文字列を使用します。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**図 7**: `pageIndex` および `pageSize` パラメーターのソースとしてクエリ文字列を使用する ([クリックしてフルサイズのイメージを表示する](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png))

ObjectDataSource を構成すると、Visual Studio によって DataList の `ItemTemplate` が自動的に作成されます。 製品の名前、カテゴリ、および業者のみが表示されるように `ItemTemplate` をカスタマイズします。 また、DataList s `RepeatColumns` プロパティを2に、`Width` を100% に設定し、`ItemStyle` s `Width` を50% に設定します。 これらの幅の設定では、2つの列に対して同じ間隔が使用されます。

これらの変更を行った後、DataList および ObjectDataSource s マークアップは次のようになります。

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> このチュートリアルでは、更新または削除の機能を実行していないので、表示されるページサイズを減らすために、DataList s ビューステートを無効にすることができます。

ブラウザーを使用して最初にこのページにアクセスしたときに、`pageIndex` も `pageSize` のクエリ文字列パラメーターも指定されていません。 そのため、既定値の0と4が使用されます。 図8に示すように、これにより、最初の4つの製品を表示する DataList が生成されます。

[最初の4つの製品が一覧表示され ![](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**図 8**: 最初の4つの製品が一覧表示されます ([クリックすると、フルサイズの画像が表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)されます)

ページングインターフェイスを使用しない場合、ユーザーがデータの2ページ目に移動するための簡単な方法はありません。 ここでは、手順 4. でページングインターフェイスを作成します。 現時点では、ページングは、クエリ文字列のページング条件を直接指定することによってのみ実現できます。 たとえば、2番目のページを表示するには、ブラウザーのアドレスバーの URL を `Paging.aspx` から `Paging.aspx?pageIndex=2` に変更し、Enter キーを押します。 これにより、データの2ページ目が表示されます (図9を参照)。

[![データの2ページ目が表示されます。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**図 9**: データの2番目のページが表示される ([クリックすると、フルサイズの画像が表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)されます)

## <a name="step-4-creating-the-paging-interface"></a>手順 4: ページングインターフェイスを作成する

実装できるさまざまなページングインターフェイスがあります。 GridView、DetailsView、および FormView コントロールは、次の4つの異なるインターフェイスを使用して選択できます。

- **次に、前**のユーザーは、一度に1ページずつ移動できます。
- 次**に**、[次へ] ボタンと [戻る] ボタンに加えて、このインターフェイスには、最初または最後のページに移動するための最初と最後のボタンが含まれています。
- **[数値]** ページングインターフェイス内のページ番号を一覧表示し、ユーザーが特定のページにすばやく移動できるようにします。
- 数値のページ番号に加えて、**最初**または最後のページに移動するためのボタンが含まれています。

DataList と Repeater では、ページングインターフェイスを決定し、実装する責任があります。 これには、ページで必要な Web コントロールを作成し、特定のページングインターフェイスボタンがクリックされたときに要求されたページを表示する作業が含まれます。 また、特定のページングインターフェイスコントロールを無効にする必要がある場合もあります。 たとえば、Next、Previous、First、Last の各インターフェイスを使用してデータの最初のページを表示すると、最初のボタンと前のボタンの両方が無効になります。

このチュートリアルでは、を使用して、Next、Previous、First、Last の各インターフェイスを使用します。 4つのボタン Web コントロールをページに追加し、その `ID` を `FirstPage`、`PrevPage`、`NextPage`、`LastPage`に設定します。 `Text` のプロパティを &lt;&lt; First、&lt; Prev、Next &gt;、および Last &gt;&gt; に設定します。

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

次に、これらの各ボタンの `Click` イベントハンドラーを作成します。 この時点で、要求されたページを表示するために必要なコードを追加します。

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>ページングされているレコードの合計数を記憶する

選択したページングインターフェイスに関係なく、ページングされているレコードの合計数を計算して記憶する必要があります。 合計行数 (ページサイズと共に) によって、ページングされるデータの合計ページ数が決まります。これにより、どのページングインターフェイスコントロールが追加または有効になるかが決まります。 次に作成する、最初の、最後のインターフェイスでは、ページ数は2つの方法で使用されます。

- 最後のページを表示しているかどうかを判断するために、[次へ] と [最後] のボタンは無効になっています。
- ユーザーが最後のボタンをクリックした場合、最後のページに whisk する必要があります。インデックスはページカウントよりも1小さい値です。

ページ数は、合計行数がページサイズで割った値として計算されます。 たとえば、ページごとに4つのレコードを含む79レコードをページングする場合、ページ数は 20 (79/4 の切り上げ) になります。 数値ページングインターフェイスを使用している場合、この情報によって、表示する数値ページボタンの数が通知されます。ページングインターフェイスに次のボタンまたは最後のボタンが含まれている場合は、ページ数を使用して、次のボタンまたは最後のボタンをいつ無効にするかを決定します。

ページングインターフェイスに最後のボタンが含まれている場合は、最後のボタンをクリックしたときに最後のページインデックスを決定できるように、ポストバック間でページングされるレコードの合計数を記憶する必要があります。 これを容易にするには、ASP.NET ページの分離コードクラスで `TotalRowCount` プロパティを作成し、その値をビューステートに永続化します。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

`TotalRowCount`に加えて、ページインデックス、ページサイズ、およびページ数に簡単にアクセスできるように、読み取り専用のページレベルのプロパティを作成するのに1分かかります。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>ページングされているレコードの合計数を確認する

ObjectDataSource s `Select()` メソッドから返された `PagedDataSource` オブジェクトは、それらのサブセットだけが DataList に表示される場合でも、*すべて*の製品レコードに含まれます。 `PagedDataSource` s [`Count` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx)は、DataList に表示される項目の数のみを返します。[`DataSourceCount` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx)は、`PagedDataSource`内の項目の合計数を返します。 したがって、ASP.NET page s `TotalRowCount` プロパティ `PagedDataSource` s `DataSourceCount` プロパティの値を割り当てる必要があります。

これを実現するには、ObjectDataSource s `Selected` イベントのイベントハンドラーを作成します。 `Selected` イベントハンドラーでは、ObjectDataSource s `Select()` メソッドの戻り値 (この場合は `PagedDataSource`) にアクセスできます。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>要求されたデータページの表示

ユーザーがページングインターフェイスのボタンのいずれかをクリックすると、要求されたデータページを表示する必要があります。 ページングパラメーターはクエリ文字列を介して指定されるため、要求されたデータページを表示するには `Response.Redirect(url)` 使用して、ユーザーのブラウザーが `Paging.aspx` ページに適切なページングパラメーターを再要求します。 たとえば、データの2ページ目を表示するには、ユーザーを `Paging.aspx?pageIndex=1`にリダイレクトします。

これを容易にするには、ユーザーを `Paging.aspx?pageIndex=sendUserToPageIndex`にリダイレクトする `RedirectUser(sendUserToPageIndex)` メソッドを作成します。 次に、4つのボタン `Click` イベントハンドラーからこのメソッドを呼び出します。 `FirstPage` `Click` イベントハンドラーで `RedirectUser(0)`を呼び出して、最初のページに送信します。`PrevPage` `Click` イベントハンドラーで、ページインデックスとして `PageIndex - 1` を使用します。などなど。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

`Click` イベントハンドラーが完了したら、ボタンをクリックすることで、DataList s レコードをページングできます。 試してみてください。

## <a name="disabling-paging-interface-controls"></a>無効化 (ページングインターフェイスコントロールを)

現在、4つのボタンはすべて、表示されているページに関係なく有効になっています。 ただし、データの最初のページを表示するときに、最初のボタンと前のボタンを無効にし、最後のページを表示するときに [次へ] と [最後] のボタンを無効にする必要があります。 ObjectDataSource s `Select()` メソッドによって返される `PagedDataSource` オブジェクトには、データの最初または最後のページを表示しているかどうかを確認するために確認できるプロパティ[`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx)および[`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx)があります。

ObjectDataSource s `Selected` イベントハンドラーに次のを追加します。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

この追加により、最初のページを表示しているときに、最初のボタンと前のボタンが無効になります。最後のページを表示すると、[次へ] ボタンと [最後のボタン] は無効になります。

現在表示しているページと合計ページ数をユーザーに通知して、ページングインターフェイスを完成させます。 ページにラベル Web コントロールを追加し、その `ID` プロパティを `CurrentPageNumber`に設定します。 ObjectDataSource s 選択イベントハンドラーで `Text` プロパティを設定します。これにより、現在表示されているページ (`PageIndex + 1`) と総ページ数 (`PageCount`) が含まれるようになります。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

図10に、最初にアクセスしたときの `Paging.aspx` を示します。 Querystring は空であるため、DataList は既定で最初の4つの製品を表示します。最初のボタンと前のボタンは無効になっています。 [次へ] をクリックすると、次の4つのレコードが表示されます (図11を参照)。1つ目と前のボタンが有効になります。

[データの最初のページが表示される ![](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**図 10**: データの最初のページが表示される ([クリックすると、フルサイズの画像が表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)されます)

[![データの2ページ目が表示されます。](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**図 11**: データの2番目のページが表示される ([クリックすると、フルサイズの画像が表示](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)されます)

> [!NOTE]
> ページングインターフェイスをさらに拡張するには、ユーザーがページごとに表示するページ数を指定できるようにします。 たとえば、"5"、"10"、"25"、"50"、"すべて" のようなページサイズオプションを追加できます。 ページサイズを選択するときは、ユーザーを `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`にリダイレクトする必要があります。 この拡張機能の実装は、リーダーの演習として行っています。

## <a name="using-custom-paging"></a>カスタムページングの使用

DataList ページは、非効率的な既定のページング手法を使用してデータを処理します。 大量のデータをページングする場合は、カスタムページングを使用する必要があります。 実装の詳細は若干異なりますが、DataList でのカスタムページングの実装の背後にある概念は、既定のページングの場合と同じです。 カスタムページングを使用する場合は、`ProductBLL` クラス s `GetProductsPaged` メソッド (`GetProductsAsPagedDataSource`ではなく) を使用します。 「[大量のデータを使用](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)した効率的なページング」で説明されているように、`GetProductsPaged` には、開始行インデックスと返される最大行数を渡す必要があります。 これらのパラメーターは、既定のページングで使用される `pageIndex` や `pageSize` パラメーターと同様に、querystring を使用して管理できます。

カスタムページングを使用した `PagedDataSource` はないため、ページングされるレコードの合計数と、データの最初または最後のページを表示するかどうかを決定するために、代替手法を使用する必要があります。 `ProductsBLL` クラスの `TotalNumberOfProducts()` メソッドは、ページングされている製品の合計数を返します。 データの最初のページが表示されているかどうかを調べるには、開始行のインデックスが0の場合は、最初のページが表示されていることを確認します。 先頭行のインデックスと返される最大行数が、ページングされているレコードの合計数以上の場合、最後のページが表示されます。

カスタムページングの実装については、次のチュートリアルでさらに詳しく説明します。

## <a name="summary"></a>まとめ

DataList も Repeater も、GridView、DetailsView、FormView コントロールで検出されたインボックスページングサポートを提供しませんが、このような機能は最小限の労力で追加できます。 既定のページングを実装する最も簡単な方法は、`PagedDataSource` 内で製品セット全体をラップし、その `PagedDataSource` を DataList または Repeater にバインドすることです。 このチュートリアルでは、`PagedDataSource`を返すために、`ProductsBLL` クラスに `GetProductsAsPagedDataSource` メソッドを追加しました。 `ProductsBLL` クラスには、カスタムページング `GetProductsPaged` と `TotalNumberOfProducts`に必要なメソッドが既に含まれています。

既定のページングのために、カスタムページングまたは `PagedDataSource` 内のすべてのレコードについて表示する正確なレコードセットを取得すると共に、ページングインターフェイスを手動で追加する必要もあります。 このチュートリアルでは、4つのボタン Web コントロールを使用して、Next、Previous、First、Last の各インターフェイスを作成しました。 また、現在のページ番号と合計ページ数を表示するラベルコントロールも追加されました。

次のチュートリアルでは、DataList と Repeater に並べ替えサポートを追加する方法について説明します。 また、ページングと並べ替えの両方が可能な DataList を作成する方法についても説明します (既定のページングとカスタムページングを使用した例を参照)。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Liz Shulok、Ken p Isa、および Bernadette Leigh でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](sorting-data-in-a-datalist-or-repeater-control-cs.md)
