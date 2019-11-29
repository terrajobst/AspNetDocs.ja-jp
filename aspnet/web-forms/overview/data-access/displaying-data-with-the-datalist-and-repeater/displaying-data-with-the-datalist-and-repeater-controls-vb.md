---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: DataList コントロールと Repeater コントロールを使用したデータの表示 (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、GridView コントロールを使用してデータを表示しました。 このチュートリアルでは、次のような一般的なレポートパターンの構築について説明します。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 4e7aaa1701da67aec61505b64a835ef41031bb13
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74613991"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>DataList および Repeater コントロールでデータを表示する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe)または[PDF のダウンロード](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> 前のチュートリアルでは、GridView コントロールを使用してデータを表示しました。 このチュートリアルでは、DataList コントロールと Repeater コントロールを使用した一般的なレポートパターンの構築について説明します。これらのコントロールを使用してデータを表示する方法の基本について説明します。

## <a name="introduction"></a>はじめに

過去28チュートリアルのすべての例で、データソースから複数のレコードを表示する必要がある場合は、GridView コントロールを利用しています。 GridView は、データソース内のレコードごとに1行のデータを表示し、レコード s のデータフィールドを列に表示します。 GridView によって、データの表示、ページ間での並べ替え、編集、および削除のためのスナップが作成されますが、その外観はビット boxy になります。 さらに、GridView の構造を担当するマークアップには、各レコードのテーブル行 (`<tr>`) と各フィールドのテーブルセル (`<td>`) を含む HTML `<table>` が含まれています。

複数のレコードを表示するときに、外観と表示マークアップのカスタマイズの度合いを高めるために、ASP.NET 2.0 には DataList コントロールと Repeater コントロールが用意されています (どちらも ASP.NET バージョン1.x でも使用できました)。 DataList コントロールと Repeater コントロールは、BoundFields、CheckBoxFields、ButtonFields などではなく、テンプレートを使用してコンテンツをレンダリングします。 GridView と同様に、DataList は HTML `<table>`として表示されますが、複数のデータソースレコードを1つのテーブル行に表示することができます。 一方、リピータは、明示的に指定したものとは別のマークアップをレンダリングしません。これは、生成されたマークアップを正確に制御する必要がある場合に最適な候補です。

次の3つ以上のチュートリアルでは、DataList コントロールと Repeater コントロールを使用した一般的なレポートパターンの構築について説明します。これらのコントロールテンプレートを使用してデータを表示する方法については、「」を参照してください。 これらのコントロールの書式を設定する方法、データソースレコードのレイアウトを変更する方法、一般的なマスター/詳細のシナリオ、データを編集および削除する方法、レコードをページに表示する方法などについて説明します。

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>手順 1: DataList および Repeater チュートリアル Web ページの追加

このチュートリアルを開始する前に、まず、このチュートリアルで必要な ASP.NET ページを追加し、次のいくつかのチュートリアルで DataList と Repeater を使用したデータの表示について説明します。 まず、`DataListRepeaterBasics`という名前のプロジェクトに新しいフォルダーを作成します。 次に、次の5つの ASP.NET ページをこのフォルダーに追加します。マスターページ `Site.master`を使用するようにすべてのページを構成します。

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![DatASP.NET Strepeater基本フォルダーを作成し、チュートリアルのページを追加します。](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**図 1**: `DataListRepeaterBasics` フォルダーを作成し、チュートリアル ASP.NET ページを追加する

`Default.aspx` ページを開き、[`UserControls`] フォルダーから `SectionLevelTutorialListing.ascx` ユーザーコントロールをデザイン画面にドラッグします。 このユーザーコントロールは、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)チュートリアルで作成したもので、サイトマップを列挙し、現在のセクションのチュートリアルを箇条書きの一覧に表示します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png)されます)

箇条書きの一覧に、作成する DataList と Repeater のチュートリアルが表示されるようにするには、サイトマップに追加する必要があります。 [カスタムボタンの追加] サイトマップノードマークアップの後に、`Web.sitemap` ファイルを開き、次のマークアップを追加します。

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]

![新しい ASP.NET ページを含めるようにサイトマップを更新する](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**図 3**: 新しい ASP.NET ページを含めるようにサイトマップを更新する

## <a name="step-2-displaying-product-information-with-the-datalist"></a>手順 2: DataList を使用して製品情報を表示する

FormView と同様に、DataList コントロールは表示される出力は、BoundFields や CheckBoxFields などではなく、テンプレートによって異なります。 FormView とは異なり、DataList は、1つのビューではなくレコードのセットを表示するように設計されています。 このチュートリアルでは、製品情報を DataList にバインドする方法について説明します。 まず、`DataListRepeaterBasics` フォルダーの [`Basics.aspx`] ページを開きます。 次に、DataList をツールボックスからデザイナーにドラッグします。 図4に示すように、DataList s テンプレートを指定する前に、デザイナーに灰色のボックスとして表示されます。

[DataList をツールボックスからデザイナーにドラッグ ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**図 4**: DataList をツールボックスからデザイナーにドラッグする ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png)されます)

DataList s スマートタグから新しい ObjectDataSource を追加し、`ProductsBLL` クラス s `GetProducts` メソッドを使用するように構成します。 このチュートリアルで読み取り専用の DataList を作成するため、ウィザードの [挿入]、[更新]、および [削除] の各タブで、ドロップダウンリストを [(なし)] に設定します。

[新しい ObjectDataSource を作成することを選択 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**図 5**: 新しい ObjectDataSource を作成することを選択する ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png)される)

[製品の Bll クラスを使用するように ObjectDataSource を構成 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**図 6**: `ProductsBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))

[GetProducts メソッドを使用してすべての製品に関する情報を取得 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**図 7**: `GetProducts` メソッドを使用してすべての製品に関する情報を取得[する (クリックしてフルサイズの画像を表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))

ObjectDataSource を構成し、そのスマートタグによって DataList に関連付けると、Visual Studio によって、データソースから返された各データフィールドの名前と値を表示する `ItemTemplate` が DataList に自動的に作成されます (以下のマークアップを参照)。 この既定の `ItemTemplate` 外観は、デザイナーを使用してデータソースを FormView にバインドするときに自動的に作成されるテンプレートと同じです。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> FormView s スマートタグを使用してデータソースを FormView コントロールにバインドするときに、Visual Studio によって `ItemTemplate`、`InsertItemTemplate`、および `EditItemTemplate`が作成されたことを思い出してください。 ただし、DataList では、`ItemTemplate` だけが作成されます。 これは、DataList には、FormView によって提供される組み込みの編集および挿入のサポートが含まれていないためです。 DataList には編集および削除に関連するイベントが含まれており、編集および削除のサポートは少しのコードを使用して追加できますが、FormView と同様にすぐに使用できる単純なサポートはありません。 この後のチュートリアルでは、DataList を使用して編集および削除のサポートを追加する方法について説明します。

このテンプレートの外観を改善するために、しばらく時間を取ってください。 では、すべてのデータフィールドを表示するのではなく、製品名、供給業者、カテゴリ、数量/単位、および単価を表示するだけです。 さらに、`<h4>` 見出しに名前を表示し、見出しの下の `<table>` を使用して残りのフィールドをレイアウトします。

これらの変更を行うには、DataList s スマートタグからデザイナーのテンプレート編集機能を使用するか、[テンプレートの編集] リンクをクリックします。または、ページ s 宣言構文を使用して手動でテンプレートを変更することもできます。 デザイナーで [テンプレートの編集] オプションを使用した場合、結果のマークアップは次のマークアップと正確に一致しない可能性がありますが、ブラウザーで表示すると、図8に示すスクリーンショットと非常によく似ています。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> 上の例では、`Text` プロパティに databinding 構文の値が割り当てられている Label Web コントロールを使用しています。 または、ラベルを完全に省略して、データバインディング構文だけを入力することもできます。 つまり、`<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` 使用するのではなく、宣言型の構文 `<%# Eval("CategoryName") %>`を使用することもできます。

ただし、ラベル Web コントロールに残しておくと、2つの利点があります。 まず、次のチュートリアルで説明するように、データに基づいてデータを書式設定するための簡単な方法を提供します。 2つ目の方法として、デザイナーの [テンプレートの編集] オプションには、Web コントロールの外部に表示される宣言型のデータバインディング構文が表示されません。 テンプレートの編集インターフェイスは、静的マークアップおよび Web コントロールの操作を容易にするように設計されています。また、Web コントロールのスマートタグからアクセスできる [データバインドの編集] ダイアログボックスを使用してデータバインディングを実行することを前提としています。

そのため、DataList を使用する場合は、デザイナーを使用してテンプレートを編集するオプションが用意されています。 Label Web コントロールを使用して、テンプレートの編集インターフェイスからコンテンツにアクセスできるようにします。 後で説明するように、Repeater では、テンプレートの内容がソースビューから編集されている必要があります。 そのため、Repeater テンプレートを作成するときに、プログラムロジックに基づいてデータバインドテキストの外観を書式設定する必要があることがわかっている場合を除き、多くの場合、ラベル Web コントロールを省略します。

[各製品の出力は、DataList s ItemTemplate を使用してレンダリングされ ![](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**図 8**: 各製品の出力は、DataList s `ItemTemplate` を使用してレンダリングされます ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png)されます)

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>手順 3: DataList の外観を改善する

GridView と同様に、DataList には、`Font`、`ForeColor`、`BackColor`、`CssClass`、`ItemStyle`、`AlternatingItemStyle`、`SelectedItemStyle`など、さまざまなスタイル関連のプロパティが用意されています。 GridView および DetailsView コントロールを使用する場合、`DataWebControls` テーマでスキンファイルを作成しました。このテーマでは、これら2つのコントロールの `CssClass` プロパティと、いくつかのサブプロパティ (`RowStyle`、`HeaderStyle`など) の `CssClass` プロパティが事前に定義されています。 DataList と同じ操作を行います。

「 [ObjectDataSource チュートリアルを使用したデータの表示](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)」で説明したように、スキンファイルは Web コントロールの既定の外観に関連するプロパティを指定します。テーマとは、web サイトの特定のルックアンドフィールを定義するスキン、CSS、イメージ、および JavaScript ファイルのコレクションです。 「 *ObjectDataSource チュートリアルを使用したデータの表示*」では、現在、2つのスキンファイル `GridView.skin` と `DetailsView.skin`を持つ `DataWebControls` テーマ (`App_Themes` フォルダー内のフォルダーとして実装されています) を作成しました。 3番目のスキンファイルを追加して、DataList の定義済みのスタイル設定を指定します。

スキンファイルを追加するには、[`App_Themes/DataWebControls`] フォルダーを右クリックし、[新しい項目の追加] を選択して、一覧から [スキンファイル] オプションを選択します。 そのファイルに `DataList.skin` という名前を付けます。

[![、DataList という名前の新しいスキンファイルを作成します。](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**図 9**: `DataList.skin` という名前の新しいスキンファイルを作成[する (クリックしてフルサイズのイメージを表示する](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))

`DataList.skin` ファイルには、次のマークアップを使用します。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

これらの設定は、GridView および DetailsView コントロールで使用されたのと同じ CSS クラスを適切な DataList プロパティに割り当てます。 ここで使用されている CSS クラス `DataWebControlStyle`、`AlternatingRowStyle`、`RowStyle`などは、`Styles.css` ファイルで定義され、前のチュートリアルで追加されています。

このスキンファイルを追加すると、デザイナーで DataList の外観が更新されます (新しいスキンファイルの効果を表示するには、デザイナービューを更新する必要がある場合があります。 [表示] メニューの [最新の状態に更新] をクリックします)。 図10に示すように、交互の製品ごとに薄いピンクの背景色があります。

[![、DataList という名前の新しいスキンファイルを作成します。](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**図 10**: `DataList.skin` という名前の新しいスキンファイルを作成[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png)される)

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>手順 4: DataList のその他のテンプレートを調べる

DataList では、`ItemTemplate`だけでなく、次の6つのオプションテンプレートもサポートしています。

- `HeaderTemplate` 指定した場合、出力にヘッダー行を追加し、この行を表示するために使用されます。
- 交互の項目を表示するために使用 `AlternatingItemTemplate`
- 選択した項目を表示するために使用 `SelectedItemTemplate` ます。選択されたアイテムは、インデックスが DataList s [`SelectedIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)に対応するアイテムです
- 編集中の項目を表示するために使用 `EditItemTemplate`
- `SeparatorTemplate` 指定した場合、各項目の間に区切り記号を追加し、この区切り記号を表示するために使用されます。
- `FooterTemplate`-指定すると、出力にフッター行が追加され、この行を表示するために使用されます。

`HeaderTemplate` または `FooterTemplate`を指定すると、DataList によって、表示される出力にヘッダー行またはフッター行が追加されます。 GridView のヘッダー行とフッター行と同様に、DataList のヘッダーとフッターはデータにバインドされません。 したがって、バインドされたデータにアクセスしようとする `HeaderTemplate` または `FooterTemplate` のデータバインド構文では、空の文字列が返されます。

> [!NOTE]
> 「 [Gridview s フッターで概要情報を表示](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)する」のチュートリアルで説明したように、ヘッダー行とフッター行ではデータバインド構文がサポートされていませんが、データ固有の情報は、gridview s `RowDataBound` イベントハンドラーからこれらの行に直接挿入できます。 この手法を使用すると、コントロールにバインドされたデータから、実行中の合計やその他の情報を計算したり、その情報をフッターに割り当てたりすることができます。 この概念は、DataList コントロールと Repeater コントロールにも適用できます。唯一の違いは、DataList と Repeater では、(`RowDataBound` イベントではなく) `ItemDataBound` イベントのイベントハンドラーを作成することです。

この例では、にタイトルの製品情報が表示されています。その結果、`<h3>` 見出しになります。 これを実現するには、適切なマークアップを含む `HeaderTemplate` を追加します。 デザイナーからこの操作を行うには、DataList s スマートタグの [テンプレートの編集] リンクをクリックし、ドロップダウンリストからヘッダーテンプレートを選択します。次に、[スタイル] ドロップダウンリストから [見出し 3] オプションを選択した後にテキストを入力します (図11を参照)。

[System.windows.controls.headereditemscontrol.headertemplate をテキストの製品情報と共に追加 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**図 11**: 製品情報をテキストと共に `HeaderTemplate` を追加[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png)されます)

または、`<asp:DataList>` タグ内に次のマークアップを入力することによって、宣言的に追加することもできます。

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

各製品の一覧の間にスペースを追加するには、各セクションの間に行を含む `SeparatorTemplate` を追加します。 水平ルールタグ (`<hr>`) は、このような区分線を追加します。 次のマークアップを含むように `SeparatorTemplate` を作成します。

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> `HeaderTemplate` や `FooterTemplates`と同様に、`SeparatorTemplate` はデータソースのどのレコードにもバインドされていないため、DataList にバインドされているデータソースレコードに直接アクセスすることはできません。

この追加を行った後、ブラウザーを使用してページを表示すると、図12のようになります。 ヘッダー行と各製品リストの間の行に注意してください。

[DataList に ![、各製品リストの間にヘッダー行と水平ルールが含まれています。](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**図 12**: DataList には、各製品リストの間にヘッダー行と水平ルールが含まれています ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png)されます)

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>手順 5: Repeater コントロールを使用して特定のマークアップをレンダリングする

図12の DataList の例にアクセスしているときにブラウザーからビューまたはソースを作成すると、datalist は、DataList にバインドされている各項目に対して1つのテーブルセル (`<td>`) を含むテーブル行 (`<tr>`) を含む HTML `<table>` を生成することがわかります。 実際、この出力は、1つの TemplateField を使用して GridView から生成されるものと同じです。 今後のチュートリアルで説明するように、DataList では出力をさらにカスタマイズできます。これにより、テーブル行ごとに複数のデータソースレコードを表示できるようになります。

ただし、HTML `<table>`を出力したくない場合はどうすればよいでしょうか。 データ Web コントロールによって生成されるマークアップを合計し、完全に制御するには、Repeater コントロールを使用する必要があります。 DataList と同様に、Repeater はテンプレートに基づいて構築されます。 ただし、リピータは次の5つのテンプレートのみを提供します。

- `HeaderTemplate` 指定した場合は、指定したマークアップを項目の前に追加します。
- 項目のレンダリングに使用 `ItemTemplate`
- `AlternatingItemTemplate` 指定した場合は、交互の項目を表示するために使用されます
- `SeparatorTemplate` 指定した場合、各項目の間に指定したマークアップを追加します。
- `FooterTemplate`-指定した場合、指定したマークアップを項目の後に追加します。

ASP.NET 1.x では、Repeater コントロールは、データがデータソースから取得された箇条書きリストを表示するためによく使用されていました。 このような場合、`HeaderTemplate` と `FooterTemplates` にはそれぞれ開始タグと `<ul>` 終了タグがそれぞれ含まれますが、`ItemTemplate` には、データバインディング構文を持つ `<li>` 要素が含まれます。 このアプローチは、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)チュートリアルの2つの例で説明したように、ASP.NET 2.0 でも使用できます。

- `Site.master` マスターページでは、リピータを使用して、最上位サイトマップの内容 (基本的なレポート、フィルター処理、カスタマイズされた書式設定など) の箇条書きリストを表示しました。入れ子になった別のリピータが、最上位のセクションの子セクションを表示するために使用されました
- `SectionLevelTutorialListing.ascx`では、Repeater を使用して、現在のサイトマップセクションの子セクションの箇条書きリストを表示しました。

> [!NOTE]
> ASP.NET 2.0 では、簡単な箇条書きリストを表示するためにデータソースコントロールにバインドできる新しい[BulletedList コントロール](https://msdn.microsoft.com/library/ms228101.aspx)が導入されています。 BulletedList コントロールでは、リストに関連する HTML を指定する必要はありません。代わりに、各リスト項目のテキストとして表示するデータフィールドを指定するだけです。

リピータは、すべてのデータのキャッチ Web コントロールとして機能します。 必要なマークアップを生成する既存のコントロールがない場合は、Repeater コントロールを使用できます。 リピータの使用方法を示すために、「」では、手順 2. で作成した製品情報 DataList の上に表示されるカテゴリの一覧を示します。 特に、1行の HTML `<table>` にカテゴリを表示し、各カテゴリをテーブルの列として表示します。

これを実現するには、まず、ツールボックスから Repeater コントロールを、製品情報 DataList の上にあるデザイナーにドラッグします。 DataList と同様に、Repeater は、テンプレートが定義されるまで、最初はグレーのボックスとして表示されます。

[Repeater をデザイナーに追加 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**図 13**: Repeater をデザイナーに追加する ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png)されます)

Repeater s スマートタグには、[データソースの選択] というオプションが1つだけあります。 新しい ObjectDataSource を作成し、`CategoriesBLL` クラス s `GetCategories` メソッドを使用するように構成することを選択します。

[新しい ObjectDataSource を作成 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**図 14**: 新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png)される)

[カテゴリ Bll クラスを使用するように ObjectDataSource を構成 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**図 15**: `CategoriesBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))

[GetCategories メソッドを使用してすべてのカテゴリに関する情報を取得 ![には](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**図 16**: `GetCategories` メソッドを使用してすべてのカテゴリに関する情報を取得[する (クリックしてフルサイズのイメージを表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))

DataList とは異なり、Visual Studio では、データソースにバインドした後、リピータの ItemTemplate が自動的に作成されることはありません。 さらに、Repeater テンプレートはデザイナーを使用して構成することはできず、宣言によって指定する必要があります。

各カテゴリの列を含む1行の `<table>` としてカテゴリを表示するには、次のようなマークアップを生成するために Repeater が必要です。

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

`<td>Category X</td>` テキストは繰り返す部分であるため、Repeater s ItemTemplate に表示されます。 `<table><tr>` の前に表示されるマークアップは、終了マークアップ `</tr></table>` `HeaderTemplate` に配置され、`FooterTemplate`に配置されます。 これらのテンプレート設定を入力するには、左下隅にある [ソース] ボタンをクリックし、次の構文を入力して、ASP.NET ページの宣言部分に移動します。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

リピータは、テンプレートによって指定された正確なマークアップを出力しますが、それだけではありません。 図17は、ブラウザーを通じて表示されるときのリピータの出力を示しています。

[1行の HTML &lt;テーブルを ![&gt; 各カテゴリを個別の列に一覧表示します。](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**図 17**: 1 行の HTML `<table>` 個別の列に各カテゴリが一覧表示される ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png)されます)

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>手順 6: リピータの外観を改善する

リピータはそのテンプレートによって指定されたマークアップを正確に出力するため、リピータにスタイル関連のプロパティがないということは意外なことではありません。 リピータによって生成されるコンテンツの外観を変更するには、必要な HTML または CSS のコンテンツをリピータテンプレートに直接手動で追加する必要があります。

この例では、DataList 内の交互の行と同様に、カテゴリ列に代替背景色を設定します。 これを実現するには、次のように、`ItemTemplate` と `AlternatingItemTemplate` のテンプレートを使用して、各リピータ項目と `AlternatingRowStyle` CSS クラスに `RowStyle` CSS クラスを割り当てる必要があります。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

また、は、Product Categories というテキストを使用して、出力にヘッダー行を追加します。 生成された `<table>` が構成される列の数がわからないため、すべての列にまたがることが保証されているヘッダー行を生成する最も簡単な方法は、 *2 つ*の `<table>` を使用することです。 最初の `<table>` には、ヘッダー行の2つの行と、システム内の各カテゴリの列を持つ2番目の単一行 `<table>` を格納する行が含まれます。 つまり、次のマークアップを出力します。

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

次の `HeaderTemplate` と `FooterTemplate` により、目的のマークアップが生成されます。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

図18は、これらの変更が加えられた後のリピータを示しています。

[カテゴリ列を背景色で代替 ![し、ヘッダー行を含める](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**図 18**: カテゴリの列が背景色で交互に表示され、ヘッダー行が含まれる ([クリックしてフルサイズの画像を表示する](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))

## <a name="summary"></a>要約

GridView コントロールを使用すると、データの表示、編集、削除、並べ替え、およびページの表示を簡単に行うことができますが、外観は非常に簡単です。 外観を詳細に制御するには、DataList または Repeater コントロールのいずれかに切り替える必要があります。 これらのコントロールはどちらも、BoundFields、CheckBoxFields などではなく、テンプレートを使用してレコードのセットを表示します。

DataList は HTML `<table>` として表示されます。既定では、1つの TemplateField を持つ GridView と同じように、各データソースレコードが1つのテーブル行に表示されます。 ただし、後のチュートリアルで説明するように、DataList ではテーブルの行ごとに複数のレコードを表示することが許可されています。 一方、リピータは、テンプレートで指定されたマークアップを厳密に出力します。追加のマークアップは追加されないため、一般的には、`<table>` (箇条書きなど) 以外の HTML 要素にデータを表示するために使用されます。

DataList と Repeater では、レンダリングされる出力がより柔軟になりますが、GridView には組み込まれている機能の多くがありません。 今後のチュートリアルでは、これらの機能のいくつかを使用する手間を省きながら、いくつかの機能を使用して戻すことができます。ただし、GridView の代わりに DataList または Repeater を使用すると、これらの機能を実装しなくても使用できる機能が制限されることに注意してください。精通.

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Yaakov Ellis、Liz Shulok、Randy、および Stacy 公園でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](nested-data-web-controls-cs.md)
> [次へ](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
