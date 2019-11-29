---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: レポートデータのページングと並べ替えC#() |Microsoft Docs
author: rick-anderson
description: ページングと並べ替えは、オンラインアプリケーションにデータを表示するときの2つの非常に一般的な機能です。 このチュートリアルでは、並べ替えの追加と...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 2f77040316dadc218b8183e52628dc0cfe3b35a1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587007"
---
# <a name="paging-and-sorting-report-data-c"></a>レポート データのページングと並べ替え (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe)または[PDF のダウンロード](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> ページングと並べ替えは、オンラインアプリケーションにデータを表示するときの2つの非常に一般的な機能です。 このチュートリアルでは、レポートに並べ替えとページングを追加する方法について最初に説明します。これは今後のチュートリアルで作成します。

## <a name="introduction"></a>はじめに

ページングと並べ替えは、オンラインアプリケーションにデータを表示するときの2つの非常に一般的な機能です。 たとえば、オンライン書店で ASP.NET books を検索する場合、このような書籍は多数存在する可能性がありますが、検索結果を一覧表示するレポートでは、1ページあたり10件の一致のみが一覧表示されます。 さらに、結果はタイトル、価格、ページ数、作成者名などで並べ替えることができます。 過去23のチュートリアルでは、データの追加、編集、削除を行うことができるインターフェイスを含むさまざまなレポートを作成する方法を確認しましたが、データの並べ替え方法については説明しませんでした。また、DetailsView と FormView を使用したページングの例のみを説明しました。制限.

このチュートリアルでは、レポートに並べ替えとページングを追加する方法について説明します。これは、いくつかのチェックボックスをオンにするだけで実現できます。 残念ながら、この単純な実装には欠点があるため、並べ替えインターフェイスは必要になることがあり、ページングルーチンは大きな結果セットを効率的にページングするようには設計されていません。 今後のチュートリアルでは、すぐに使えるページングと並べ替えソリューションの制限を克服する方法について説明します。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>手順 1: ページングと並べ替えのチュートリアル Web ページの追加

このチュートリアルを開始する前に、このチュートリアルに必要な ASP.NET ページを追加し、次の3つについて説明します。 まず、`PagingAndSorting`という名前のプロジェクトに新しいフォルダーを作成します。 次に、次の5つの ASP.NET ページをこのフォルダーに追加します。マスターページ `Site.master`を使用するようにすべてのページを構成します。

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![PagingAndSorting フォルダーを作成し、チュートリアル ASP.NET ページを追加します。](paging-and-sorting-report-data-cs/_static/image1.png)

**図 1**: PagingAndSorting フォルダーを作成し、チュートリアル ASP.NET ページを追加する

次に、[`Default.aspx`] ページを開き、`SectionLevelTutorialListing.ascx` ユーザーコントロールを `UserControls` フォルダーからデザイン画面にドラッグします。 このユーザーコントロールは、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-cs.md)チュートリアルで作成したもので、サイトマップを列挙し、現在のセクションに記載されているチュートリアルを箇条書きの一覧に表示します。

![Default.aspx に SectionLevelTutorialListing ユーザーコントロールを追加します。](paging-and-sorting-report-data-cs/_static/image2.png)

**図 2**: Default.aspx に SectionLevelTutorialListing ユーザーコントロールを追加する

箇条書きの一覧に、作成するページングと並べ替えのチュートリアルが表示されるようにするには、サイトマップに追加する必要があります。 `Web.sitemap` ファイルを開き、サイトマップノードマークアップの編集、挿入、および削除の後に、次のマークアップを追加します。

[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]

![新しい ASP.NET ページを含めるようにサイトマップを更新する](paging-and-sorting-report-data-cs/_static/image3.png)

**図 3**: 新しい ASP.NET ページを含めるようにサイトマップを更新する

## <a name="step-2-displaying-product-information-in-a-gridview"></a>手順 2: GridView で製品情報を表示する

ページングと並べ替えの機能を実際に実装する前に、まずは、製品情報を一覧表示する、並べ替え不可能な標準の非ページ GridView を作成してみましょう。 このチュートリアルシリーズの前に何度も実行していたので、これらの手順は理解しておく必要があります。 まず、[`SimplePagingSorting.aspx`] ページを開き、[ツールボックス] から GridView コントロールをデザイナーにドラッグして、`ID` プロパティを `Products`に設定します。 次に、製品の `GetProducts()` メソッドを使用してすべての製品情報を返す新しい ObjectDataSource を作成します。

![GetProducts () メソッドを使用して、すべての製品に関する情報を取得します。](paging-and-sorting-report-data-cs/_static/image4.png)

**図 4**: getproducts () メソッドを使用してすべての製品に関する情報を取得する

このレポートは読み取り専用のレポートであるため、ObjectDataSource s `Insert()`、`Update()`、または `Delete()` メソッドを対応する `ProductsBLL` メソッドにマップする必要はありません。そのため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストから [(なし)] を選択します。

![[更新]、[挿入]、[削除] の各タブのドロップダウンリストで [(なし)] オプションを選択します。](paging-and-sorting-report-data-cs/_static/image5.png)

**図 5**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストで [(なし)] オプションを選択する

次に、を使用して、製品名、仕入先、カテゴリ、価格、および廃止された状態のみが表示されるように、GridView のフィールドをカスタマイズします。 さらに、`HeaderText` のプロパティを調整したり、価格を通貨として書式設定するなど、フィールドレベルの書式設定を自由に変更することもできます。 これらの変更が完了すると、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

図6は、ブラウザーを通じて表示されたときの進行状況を示しています。 このページには、すべての製品が1つの画面に表示され、各製品の名前、カテゴリ、仕入先、価格、および廃止された状態が表示されていることに注意してください。

[各製品 ![一覧表示されます。](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**図 6**: 各製品が一覧表示されます ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image8.png)されます)

## <a name="step-3-adding-paging-support"></a>手順 3: ページングサポートを追加する

*すべて*の製品を1つの画面に一覧表示すると、ユーザーがデータをつい man するための情報が過負荷になる可能性があります。 結果をさらに管理しやすくするために、データを小さなページに分割し、ユーザーが一度に1ページずつデータをステップ実行できるようにします。 これを行うには、GridView s スマートタグから [ページングを有効にする] チェックボックスをオンにします (これにより、GridView s [`AllowPaging` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)が `true`に設定されます)。

[[ページングを有効にする] チェックボックスをオンにして、ページングサポートを追加 ![](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**図 7**: [ページングを有効にする] チェックボックスをオンにしてページングサポートを追加する ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image11.png)されます)

ページングを有効にすると、ページごとに表示されるレコードの数が制限され、*ページングインターフェイス*が GridView に追加されます。 図7に示す既定のページングインターフェイスは一連のページ番号であり、ユーザーはデータの1ページから別のページにすばやく移動できます。 このページングインターフェイスは、前のチュートリアルでは、DetailsView コントロールと FormView コントロールにページングサポートを追加するときに見たように、見慣れているはずです。

DetailsView コントロールと FormView コントロールは、どちらもページごとに1つのレコードのみを表示します。 ただし、GridView は、 [`PageSize` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)を調べて、1ページあたりに表示するレコード数を決定します (このプロパティの既定値は 10)。

この GridView、DetailsView、FormView s ページングインターフェイスは、次のプロパティを使用してカスタマイズできます。

- `PagerStyle` ページングインターフェイスのスタイル情報を示します。`BackColor`、`ForeColor`、`CssClass`、`HorizontalAlign`などの設定を指定できます。
- `PagerSettings` には、ページングインターフェイスの機能をカスタマイズできる傾斜 y プロパティが含まれています。ページングインターフェイスに表示される数値ページ番号の最大数 (既定値は 10) を `PageButtonCount` します。[`Mode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)は、ページングインターフェイスの動作を指定し、次のように設定できます。 

    - `NextPrevious` [次へ] ボタンと [前へ] ボタンが表示され、ユーザーは一度に1ページずつ移動または移動できます。
    - `NextPreviousFirstLast` [次へ] ボタンと [戻る] ボタンに加えて、最初と最後のボタンも含まれています。これにより、ユーザーはデータの最初または最後のページにすばやく移動できます。
    - `Numeric` には一連のページ番号が表示され、ユーザーはすぐに任意のページに移動できます。
    - ページ番号に加えて `NumericFirstLast` には、最初と最後のボタンが含まれており、ユーザーはすぐにデータの最初または最後のページに移動できます。最初/最後のボタンは、すべての数値のページ番号が一致しない場合にのみ表示されます。

さらに、GridView、DetailsView、および FormView には、`PageIndex` プロパティと `PageCount` プロパティが用意されています。これらのプロパティは、表示されている現在のページと、データページの合計数を示します。 `PageIndex` プロパティのインデックスは0から始まります。これは、データの最初のページを表示するときに `PageIndex` が0になることを意味します。 一方、`PageCount`は1からカウントを開始します。つまり、`PageIndex` は0から `PageCount - 1`までの値に制限されます。

GridView のページングインターフェイスの既定の外観を改善するために、しばらく時間がかかります。 具体的には、のページングインターフェイスを明るい灰色の背景で右に並べます。 GridView の `PagerStyle` プロパティを使用してこれらのプロパティを直接設定するのではなく、`PagerRowStyle` という名前の `Styles.css` に CSS クラスを作成し、このテーマを使用して `PagerStyle` s `CssClass` プロパティを割り当てます。 まず `Styles.css` を開き、次の CSS クラス定義を追加します。

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

次に、`App_Themes` フォルダー内の `DataWebControls` フォルダーにある `GridView.skin` ファイルを開きます。 *マスターページとサイトナビゲーション*のチュートリアルで説明したように、スキンファイルを使用して、Web コントロールの既定のプロパティ値を指定できます。 したがって、では、既存の設定が拡張され、`PagerStyle` s `CssClass` プロパティの設定が `PagerRowStyle`に追加されます。 また、ページングインターフェイスを構成して、`NumericFirstLast` ページングインターフェイスを使用して最大5つの数値ページボタンを表示するようにします。

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>ユーザーエクスペリエンスのページング

図8は、GridView の [ページングを有効にする] チェックボックスがオンになった後にブラウザーでアクセスしたときの web ページを示しています。また、`PagerStyle` と `PagerSettings` の構成が `GridView.skin` ファイルによって行われています。 表示されるのは10個のレコードのみであり、ページングインターフェイスは、データの最初のページを表示していることを示します。

[ページングが有効になっている ![は、レコードのサブセットのみが一度に表示されます。](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**図 8**: ページングが有効になっている場合は、レコードのサブセットのみが一度に表示されます ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image14.png)されます)

ページングインターフェイス内のいずれかのページ番号をクリックすると、ポストバック ensues とページが再読み込みされ、要求されたページ s レコードが表示されます。 図9は、データの最終ページを表示した後の結果を示しています。 最後のページには1つのレコードしかないことに注意してください。これは、合計で81のレコードが存在するためです。その結果、ページごとに10個のレコードが含まれ、1つのページには単一行のレコードが含まれます。

[ページ番号をクリック ![と、ポストバックが発生し、レコードの適切なサブセットが表示されます。](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**図 9**: ページ番号をクリックするとポストバックが発生し、レコードの適切なサブセットが表示されます ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image17.png)されます)

## <a name="paging-s-server-side-workflow"></a>サーバー側のワークフローのページング

エンドユーザーがページングインターフェイスのボタンをクリックすると、ポストバック ensues と次のサーバー側ワークフローが開始されます。

1. GridView s (または DetailsView または FormView) `PageIndexChanging` イベントが発生します
2. ObjectDataSource は、BLL からの*すべて*のデータを再要求します。gridview の `PageIndex` と `PageSize` プロパティ値を使用して、GridView に表示する必要のある BLL から返されるレコードを決定します。
3. GridView s `PageIndexChanged` イベントが発生します

手順 2. で、ObjectDataSource はデータソースからのすべてのデータを再要求します。 この形式のページングは、一般に*既定のページング*と呼ばれます。これは、`AllowPaging` プロパティを `true`に設定するときに既定で使用されるページング動作です。 既定のページングを使用すると、データ Web コントロールネイティブは、データの各ページのすべてのレコードを取得します。ただし、実際には、ブラウザーに送信された HTML にレコードのサブセットのみがレンダリングされます。 データベースデータが BLL または ObjectDataSource によってキャッシュされていない限り、既定のページングは、十分に大きな結果セットまたは多数の同時実行ユーザーを持つ web アプリケーションに対して動作不能ます。

次のチュートリアルでは、*カスタムページング*を実装する方法について説明します。 カスタムページングを使用すると、要求されたデータページに必要なレコードの正確なセットだけを取得するように ObjectDataSource に指示できます。 ご想像のとおり、カスタムページングを使用すると、大きな結果セットを使用したページングの効率が大幅に向上します。

> [!NOTE]
> 既定のページングは、大量の結果セットをページングする場合や、多数の同時ユーザーがいるサイトの場合には適していませんが、カスタムページングではより多くの変更と実装が必要であり、チェックボックスをチェックするだけではありません (既定では)。ページング)。 そのため、小規模、低トラフィックの web サイト、または比較的小さな結果セットをページングする場合に、既定のページングが最適な選択肢となる可能性があります。これは、より簡単かつ迅速に実装できるためです。

たとえば、データベースで100を超える製品を使用しないことがわかっている場合は、カスタムページングによって利用できるパフォーマンスの低下は、実装に必要な労力によって相殺される可能性があります。 しかし、1日に数千から数十の製品がある場合、カスタムページングを実装しても、アプリケーションのスケーラビリティが大幅に阻害*され*ます。

## <a name="step-4-customizing-the-paging-experience"></a>手順 4: ページングエクスペリエンスのカスタマイズ

データ Web コントロールには、ユーザーのページングエクスペリエンスを向上させるために使用できる多数のプロパティが用意されています。 たとえば、`PageCount` プロパティは、表示されているページの合計数を示します。一方、`PageIndex` プロパティは、現在アクセスしているページを示します。また、ユーザーを特定のページにすばやく移動するように設定できます。 これらのプロパティを使用してユーザーのページングエクスペリエンスを向上させる方法を説明するために、では、現在アクセスしているページをユーザーに通知するラベル Web コントロールをページに追加します。また、DropDownList コントロールを使用して、特定のページにすばやく移動できるようにします.

まず、ラベル Web コントロールをページに追加し、その `ID` プロパティを `PagingInformation`に設定して、その `Text` プロパティをクリアします。 次に、GridView s `DataBound` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

このイベントハンドラーは、`PagingInformation` Label s `Text` プロパティを、現在 `Products.PageIndex + 1` アクセスしているページをユーザーに通知するメッセージに割り当てます。これにより、`Products.PageIndex` は0からインデックスが作成される `Products.PageCount` ので、`PageIndex` プロパティに1が追加されます。 `PageIndexChanged` イベントハンドラーではなく、`DataBound` イベントハンドラーで [この `Text` ラベルを割り当てる] プロパティを選択しました。これは、データが GridView にバインドされるたびに `DataBound` イベントが発生するのに対して、`PageIndexChanged` イベントハンドラーはページインデックスが変更された場合にのみ発生するためです。 最初のページに移動したときに GridView が最初のページでデータバインドされた場合、`PageIndexChanging` イベントは発生しません (`DataBound` イベントによって発生します)。

この追加により、ユーザーがアクセスしているページと、そのデータの合計ページ数を示すメッセージが表示されるようになりました。

[現在のページ番号と合計ページ数を ![](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**図 10**: 現在のページ数とページ数の合計が表示される ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image20.png)されます)

ラベルコントロールに加えて、現在表示されているページを使用して GridView 内のページ番号を一覧表示する DropDownList コントロールも追加します。 ここでの考え方は、ユーザーが DropDownList から新しいページインデックスを選択するだけで、現在のページから別のページにすばやく移動できることです。 まず、DropDownList をデザイナーに追加し、その `ID` プロパティを `PageList` に設定して、そのスマートタグから [AutoPostBack を有効にする] オプションをオンにします。

次に、`DataBound` イベントハンドラーに戻り、次のコードを追加します。

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

このコードでは、まず `PageList` DropDownList の項目をクリアします。 このような場合、ページ数が変更されることはありませんが、他のユーザーが同時にシステムを使用して、`Products` テーブルのレコードを追加または削除する可能性があります。 このような挿入や削除によって、データのページ数が変更される可能性があります。

次に、ページ番号を再度作成し、現在の GridView にマップされているものを既定で選択 `PageIndex` する必要があります。 これを行うには、0から `PageCount - 1`へのループを行い、各反復に新しい `ListItem` を追加し、現在の反復インデックスが GridView s `PageIndex` プロパティに等しい場合はその `Selected` プロパティを true に設定します。

最後に、DropDownList `SelectedIndexChanged` イベントのイベントハンドラーを作成する必要があります。これは、ユーザーが一覧から別の項目を選択するたびに起動されます。 このイベントハンドラーを作成するには、デザイナーで DropDownList をダブルクリックし、次のコードを追加します。

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

図11に示すように、GridView の `PageIndex` プロパティを変更するだけで、データが GridView に再バインドされます。 GridView s `DataBound` イベントハンドラーで、適切な DropDownList `ListItem` が選択されています。

[[ページ 6] ドロップダウンリスト項目を選択すると、ユーザーは6ページ目に自動的に移動 ![](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**図 11**: ページ6のドロップダウンリスト項目を選択したときに、ユーザーが6番目のページに自動的に移動する ([クリックしてフルサイズの画像を表示する](paging-and-sorting-report-data-cs/_static/image23.png))

## <a name="step-5-adding-bi-directional-sorting-support"></a>手順 5: 双方向の並べ替えサポートを追加する

双方向の並べ替えサポートの追加は、ページングサポートを追加するだけで簡単に行うことができます。 GridView s スマートタグ (GridView s [`AllowSorting` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)を `true`に設定する) の [並べ替えを有効にする] オプションをオンにします。 これにより、GridView のフィールドの各ヘッダーがリンクボタンとして表示され、クリックするとポストバックが発生し、クリックされた列によって並べ替えられたデータが昇順で返されます。 同じヘッダー LinkButton をクリックすると、データが降順に並べ替えられます。

> [!NOTE]
> 型指定されたデータセットではなくカスタムデータアクセス層を使用している場合は、GridView s スマートタグに [並べ替えを有効にする] オプションがない可能性があります。 並べ替えをネイティブにサポートするデータソースにバインドされている GridViews でのみ、このチェックボックスを使用できます。 ADO.NET DataTable には、指定された条件を使用して DataTable s Datarow を並べ替える `Sort` メソッドが用意されているため、型指定されたデータセットは、すぐに使用できる並べ替えをサポートします。

DAL が並べ替えをネイティブにサポートするオブジェクトを返さない場合は、ObjectDataSource を構成して、並べ替え情報をビジネスロジックレイヤーに渡す必要があります。これにより、データを並べ替えるか、DAL によってデータを並べ替えることができます。 今後のチュートリアルでは、ビジネスロジックとデータアクセス層でデータを並べ替える方法について説明します。

[LinkButtons 並べ替え] ボタンは HTML ハイパーリンクとして表示されます。現在の色 (未処理リンクの場合は青、アクセスしたリンクの場合はダーク赤色) が、ヘッダー行の背景色と競合します。 代わりに、アクセスされたかどうかに関係なく、すべてのヘッダー行のリンクが白で表示されます。 これを行うには、次のを `Styles.css` クラスに追加します。

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

この構文は、HeaderStyle クラスを使用する要素内にこれらのハイパーリンクを表示するときに、ホワイトテキストを使用することを示します。

この CSS を追加した後、ブラウザーを使用してページにアクセスすると、画面は図12のようになります。 特に、図12は、Price field s ヘッダーリンクがクリックされた後の結果を示しています。

[結果が UnitPrice で昇順に並べ替えられた ![](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**図 12**: 結果が UnitPrice の昇順で並べ替えられている ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image26.png)されます)

## <a name="examining-the-sorting-workflow"></a>並べ替えワークフローを調べています

すべての GridView フィールド BoundField、CheckBoxField、TemplateField などには、そのフィールドの [並べ替えヘッダー] リンクがクリックされたときにデータを並べ替えるために使用する式を示す `SortExpression` のプロパティがあります。 GridView には、`SortExpression` プロパティもあります。 並べ替えヘッダー LinkButton がクリックされると、GridView によってそのフィールドの `SortExpression` 値が `SortExpression` プロパティに割り当てられます。 次に、データは ObjectDataSource から再取得され、GridView s `SortExpression` プロパティに従って並べ替えられます。 次の一覧では、エンドユーザーが GridView でデータを並べ替えるときに発生する一連の手順について詳しく説明します。

1. GridView の[並べ替えイベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)が発生しました
2. GridView s [`SortExpression` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)は、並べ替えヘッダー LinkButton がクリックされたフィールドの `SortExpression` に設定されます。
3. ObjectDataSource は、BLL からすべてのデータを再取得した後、GridView s を使用してデータを並べ替え `SortExpression`
4. GridView s `PageIndex` プロパティは0にリセットされます。つまり、ユーザーがデータの最初のページに戻るとき (ページングのサポートが実装されていることを前提としています)、
5. GridView s [`Sorted` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)が発生します

既定のページングの場合と同様に、既定の並べ替えオプションでは、BLL から*すべて*のレコードが再取得されます。 ページングを行わずに並べ替えを使用する場合、または既定のページングでの並べ替えを使用する場合、このパフォーマンスの低下を回避する方法はありません (データベースデータをキャッシュすることもありません)。 ただし、今後のチュートリアルで説明しているように、カスタムページングを使用するときにデータを効率的に並べ替えることができます。

GridView のスマートタグのドロップダウンリストを使用して ObjectDataSource を GridView にバインドすると、各 GridView フィールドには、`ProductsRow` クラスのデータフィールドの名前に割り当てられた `SortExpression` プロパティが自動的に設定されます。 たとえば、次の宣言型マークアップに示すように、`ProductName` BoundField s `SortExpression` は `ProductName`に設定されます。

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

フィールドを構成して、その `SortExpression` プロパティをクリアする (空の文字列に割り当てる) ことによって、並べ替えられないようにすることができます。 これを説明するために、お客様が製品を価格で並べ替えないようにしたいと考えています。 `UnitPrice` BoundField s `SortExpression` プロパティは、宣言型マークアップから、または [フィールド] ダイアログボックス (GridView s スマートタグの [列の編集] リンクをクリックするとアクセスできます) から削除できます。

![結果は、UnitPrice の昇順で並べ替えられています。](paging-and-sorting-report-data-cs/_static/image27.png)

**図 13**: 結果が UnitPrice の昇順で並べ替えられている

`SortExpression` プロパティが `UnitPrice` BoundField に対して削除されると、ヘッダーはリンクとしてではなくテキストとして表示されるため、ユーザーはデータを価格で並べ替えることができません。

[SortExpression プロパティを削除することにより、ユーザーは商品を価格で並べ替えることができなくなります。 ![](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**図 14**: SortExpression プロパティを削除すると、ユーザーは製品を価格で並べ替えることができなくなります ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image30.png)されます)

## <a name="programmatically-sorting-the-gridview"></a>プログラムによる GridView の並べ替え

Gridview s [`Sort` メソッド](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)を使用して、gridview の内容をプログラムによって並べ替えることもできます。 `SortExpression` 値を渡すだけで、 [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` または `Descending`) と共に並べ替えられ、GridView のデータが再並べ替えされます。

`UnitPrice` による並べ替えを無効にした理由は、お客様が最低価格の製品のみを購入するという懸念があることを想像してください。 しかし、コストの高い製品を購入できるようにすることをお勧めします。そのため、製品を価格で並べ替えることができますが、最もコストの高い価格のみを使用できます。

これを実現するには、ボタン Web コントロールをページに追加し、その `ID` プロパティを `SortPriceDescending`に設定し、その `Text` プロパティを Price で並べ替えます。 次に、デザイナーのボタンコントロールをダブルクリックして、ボタン s `Click` イベントのイベントハンドラーを作成します。 このイベントハンドラーに次のコードを追加します。

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

このボタンをクリックすると、製品が価格で並べ替えられた最初のページにユーザーが返されます。料金は最も高く、コストが最も低くなります (図15を参照)。

[このボタンをクリック ![と、最もコストの高い製品から順に製品が順序付けされます。](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**図 15**: ボタンをクリックすると、最もコストの高い製品から最もコストが高くなります ([クリックすると、フルサイズの画像が表示](paging-and-sorting-report-data-cs/_static/image33.png)されます)

## <a name="summary"></a>要約

このチュートリアルでは、既定のページングと並べ替えの機能を実装する方法について説明しました。どちらもチェックボックスをオンにするのと同じくらい簡単でした。 ユーザーがデータを並べ替えたり、ページを上したりすると、同様のワークフローは次のようになります。

1. ポストバック ensues
2. データ Web コントロール s レベルのイベントが発生します (`PageIndexChanging` または `Sorting`)
3. すべてのデータが ObjectDataSource によって再取得されます。
4. データ Web コントロール s レベルのイベントが発生しました (`PageIndexChanged` または `Sorted`)

基本的なページングと並べ替えを実装するのは簡単ですが、より効率的なカスタムページングを利用したり、ページングまたは並べ替えインターフェイスをさらに強化したりするには、より多くの労力を用いる必要があります。 今後のチュートリアルでは、これらのトピックについて説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [次へ](efficiently-paging-through-large-amounts-of-data-cs.md)
