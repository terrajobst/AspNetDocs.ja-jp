---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: ObjectDataSource を使用したデータの表示 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、このコントロールを使用して ObjectDataSource コントロールを見ていきます。前のチュートリアルで作成した BLL から取得したデータを havi なしでバインドできます...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 754188352cbfb08e610027f5b7890a32bd88ae26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483052"
---
# <a name="displaying-data-with-the-objectdatasource-vb"></a>ObjectDataSource でデータを表示する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe)または[PDF のダウンロード](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> このチュートリアルでは、このコントロールを使用して ObjectDataSource コントロールを見ていきます。前のチュートリアルで作成した BLL から取得したデータをバインドするには、コード行を記述する必要はありません。

## <a name="introduction"></a>はじめに

アプリケーションアーキテクチャと web サイトページレイアウトが完成したら、さまざまな一般的なデータおよびレポート関連タスクを実行する方法を確認できます。 前のチュートリアルでは、DAL から ASP.NET ページのデータ Web コントロールにプログラムによってデータをバインドする方法を説明しました。 この構文では、データ Web コントロールの `DataSource` プロパティを表示するデータに割り当ててから、コントロールの `DataBind()` メソッドを呼び出すことが、ASP.NET 1.x アプリケーションで使用されていたパターンでした。この構文は、2.0 アプリケーションで引き続き使用できます。 ただし、ASP.NET 2.0 の新しいデータソースコントロールには、データを操作するための宣言的な方法が用意されています。 これらのコントロールを使用すると、コード行を記述しなくても、前のチュートリアルで作成した BLL から取得したデータをバインドできます。

ASP.NET 2.0 には、5つの組み込みデータソースコントロール[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)、および[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)が付属していますが、必要に応じて独自の[カスタムデータソースコントロール](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)を作成することもできます。 チュートリアルアプリケーションのアーキテクチャを開発したため、BLL クラスに対して ObjectDataSource を使用します。

![ASP.NET 2.0 には、5つの組み込みデータソースコントロールが含まれています](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**図 1**: ASP.NET 2.0 には、5つの組み込みデータソースコントロールが含まれています。

ObjectDataSource は、他のオブジェクトを操作するためのプロキシとして機能します。 ObjectDataSource を構成するには、この基になるオブジェクトを指定し、そのメソッドを ObjectDataSource の `Select`、`Insert`、`Update`、および `Delete` メソッドにどのようにマップするかを指定します。 この基になるオブジェクトを指定し、メソッドを ObjectDataSource のにマップした後、ObjectDataSource をデータ Web コントロールにバインドできます。 ASP.NET には、GridView、DetailsView、RadioButtonList、DropDownList など、多くのデータ Web コントロールが付属しています。 ページのライフサイクル中に、データ Web コントロールは、バインドされているデータにアクセスする必要がある場合があります。これは、ObjectDataSource の `Select` メソッドを呼び出すことによって実現します。データ Web コントロールが挿入、更新、または削除をサポートしている場合は、ObjectDataSource の `Insert`、`Update`、または `Delete` メソッドに対して呼び出しを行うことができます。 これらの呼び出しは、次の図に示すように、ObjectDataSource によって適切な基になるオブジェクトのメソッドにルーティングされます。

[ObjectDataSource をプロキシとして機能させる ![](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**図 2**: ObjectDataSource はプロキシとして機能します ([クリックすると、フルサイズのイメージが表示](displaying-data-with-the-objectdatasource-vb/_static/image4.png)されます)

ObjectDataSource を使用すると、データの挿入、更新、または削除のためのメソッドを呼び出すことができますが、データを返すだけで済みます。今後のチュートリアルでは、データを変更する ObjectDataSource およびデータ Web コントロールの使用方法について説明します。

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>手順 1: ObjectDataSource コントロールの追加と構成

まず、`BasicReporting` フォルダーの [`SimpleDisplay.aspx`] ページを開き、[デザインビュー] に切り替えて、[ツールボックス] から [ObjectDataSource] コントロールをページのデザイン画面にドラッグします。 ObjectDataSource は、マークアップを生成しないため、デザインサーフェイスに灰色のボックスとして表示されます。単に、指定されたオブジェクトからメソッドを呼び出すことによってデータにアクセスします。 ObjectDataSource によって返されるデータは、GridView、DetailsView、FormView などのデータ Web コントロールによって表示できます。

> [!NOTE]
> または、最初にデータ Web コントロールをページに追加してから、そのスマートタグから、ドロップダウンリストから [新しいデータソースの &lt;&gt;] オプションを選択します。

ObjectDataSource の基になるオブジェクトと、そのオブジェクトのメソッドが ObjectDataSource のにどのように対応付けられるかを指定するには、ObjectDataSource のスマートタグから [データソースの構成] リンクをクリックします。

[![スマートタグから [データソースの構成] リンクをクリックします。](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**図 3**: スマートタグから [データソースの構成] リンクをクリック[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image7.png)されます)

これにより、データソースの構成ウィザードが起動します。 最初に、ObjectDataSource が使用するオブジェクトを指定する必要があります。 [データコンポーネントのみを表示する] チェックボックスがオンになっている場合、この画面のドロップダウンリストには、`DataObject` 属性で修飾されたオブジェクトのみが表示されます。 現在の一覧には、型指定されたデータセットの Tableadapter と、前のチュートリアルで作成した BLL クラスが含まれています。 `DataObject` 属性をビジネスロジックレイヤークラスに追加し忘れた場合、この一覧には表示されません。 その場合は、[データコンポーネントのみを表示する] チェックボックスをオフにしてすべてのオブジェクトを表示します。これには、BLL クラスが含まれている必要があります。これには、型指定されたデータセット内の他のクラスと共に Datatable、Datarow などが含まれます。

この最初の画面で、ドロップダウンリストから `ProductsBLL` クラスを選択し、[次へ] をクリックします。

[ObjectDataSource コントロールで使用するオブジェクトを指定 ![には](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**図 4**: ObjectDataSource コントロールで使用するオブジェクトを指定する ([クリックしてフルサイズのイメージを表示する](displaying-data-with-the-objectdatasource-vb/_static/image10.png))

ウィザードの次の画面では、ObjectDataSource が呼び出すメソッドを選択するよう求められます。 ドロップダウンリストには、前の画面で選択したオブジェクトのデータを返すメソッドが一覧表示されます。 ここでは、`GetProductByProductID`、`GetProducts`、`GetProductsByCategoryID`、および `GetProductsBySupplierID`について説明します。 ドロップダウンリストから `GetProducts` メソッドを選択し、[完了] をクリックします (前のチュートリアルで示したように、`ProductBLL`のメソッドに `DataObjectMethodAttribute` を追加した場合は、このオプションが既定で選択されます)。

[![[選択] タブからデータを返す方法を選択します。](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**図 5**: [選択] タブからデータを返す方法を選択[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image13.png)されます)

## <a name="configure-the-objectdatasource-manually"></a>ObjectDataSource を手動で構成する

ObjectDataSource のデータソース構成ウィザードでは、使用するオブジェクトを簡単に指定し、オブジェクトのメソッドを関連付けることができます。 ただし、プロパティウィンドウを使用するか、または宣言マークアップ内で直接、プロパティを使用して ObjectDataSource を構成できます。 単に、`TypeName` プロパティを、使用する基になるオブジェクトの型に設定し、データを取得するときに呼び出すメソッドの `SelectMethod` に設定します。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

データソースの構成ウィザードを使用する場合でも、ObjectDataSource を手動で構成する必要がある場合があります。これは、ウィザードが開発者が作成したクラスのみを一覧表示するためです。 ObjectDataSource を[メンバーシップクラス](https://msdn.microsoft.com/library/system.web.security.membership.aspx)などの .NET Framework のクラスにバインドする場合、ユーザーアカウント情報にアクセスする場合、または[ディレクトリクラス](https://msdn.microsoft.com/library/system.io.directory.aspx)を使用してファイルシステム情報を操作する場合は、objectdatasource のプロパティを手動で設定する必要があります。

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>手順 2: データ Web コントロールを追加して ObjectDataSource にバインドする

ObjectDataSource がページに追加され、構成されたら、データ Web コントロールをページに追加して、ObjectDataSource の `Select` メソッドによって返されたデータを表示する準備ができました。 任意のデータ Web コントロールを ObjectDataSource にバインドできます。GridView、DetailsView、FormView に ObjectDataSource のデータを表示する方法を見てみましょう。

## <a name="binding-a-gridview-to-the-objectdatasource"></a>GridView を ObjectDataSource にバインドする

ツールボックスから `SimpleDisplay.aspx`のデザインサーフェイスに GridView コントロールを追加します。 GridView のスマートタグから、手順1で追加した ObjectDataSource コントロールを選択します。 これにより、ObjectDataSource の `Select` メソッド (つまり、Products DataTable によって定義されるプロパティ) からのデータによって返される各プロパティに対して、GridView に BoundField が自動的に作成されます。

[GridView がページに追加され、ObjectDataSource にバインドされて ![](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**図 6**: GridView がページに追加され、ObjectDataSource にバインドされている ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image16.png)されます)

その後、スマートタグの [列の編集] オプションをクリックして、GridView の BoundFields をカスタマイズ、再配置、または削除できます。

[[列の編集] ダイアログボックスを使用して GridView の BoundFields を管理 ![には](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**図 7**: [列の編集] ダイアログボックスを使用して GridView の boundfields を管理[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image19.png)されます)

GridView の BoundFields を変更し、`ProductID`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitsInStock`、`UnitsOnOrder`、および `ReorderLevel` BoundFields を削除します。 左下の一覧から BoundField を選択し、[削除] ボタン (赤い X) をクリックして削除します。 次に、boundfields を再配置して、`CategoryName` と `SupplierName` BoundFields が `UnitPrice` BoundField の前になるようにします。そのためには、これらの連結フィールドを選択し、上矢印をクリックします。 残りの BoundFields の `HeaderText` プロパティを `Products`、`Category`、`Supplier`、および `Price`にそれぞれ設定します。 次に、BoundField の `HtmlEncode` プロパティを False に設定し、その `DataFormatString` プロパティを `{0:c}`に設定して、`Price` BoundField を通貨として書式設定します。 最後に、`ItemStyle`/`HorizontalAlign` プロパティを使用して、`Price` を右揃えにし、[`Discontinued`] チェックボックスを中央に配置します。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

[GridView の BoundFields がカスタマイズされている ![](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**図 8**: GridView の Boundfields がカスタマイズされている ([クリックしてフルサイズのイメージを表示する](displaying-data-with-the-objectdatasource-vb/_static/image22.png))

## <a name="using-themes-for-a-consistent-look"></a>テーマを一貫した外観で使用する

これらのチュートリアルでは、可能な限り外部ファイルで定義されているカスケードスタイルシートを使用するのではなく、コントロールレベルのスタイル設定をすべて削除することに努めています。 `Styles.css` ファイルには、これらのチュートリアルで使用するデータ Web コントロールの外観を指定するために使用する必要がある、`DataWebControlStyle`、`HeaderStyle`、`RowStyle`、および `AlternatingRowStyle` の CSS クラスが含まれています。 これを実現するには、GridView の `CssClass` プロパティを `DataWebControlStyle`に設定し、その `HeaderStyle`、`RowStyle`、および `AlternatingRowStyle` プロパティの `CssClass` プロパティを適宜設定します。

これらの `CssClass` プロパティを Web コントロールで設定する場合は、チュートリアルに追加したすべてのデータ Web コントロールに対して、これらのプロパティ値を明示的に設定する必要があります。 より管理しやすい方法は、テーマを使用して GridView、DetailsView、FormView コントロールの既定の CSS 関連プロパティを定義することです。 テーマとは、コントロールレベルのプロパティ設定、画像、および CSS クラスのコレクションであり、一般的なルックアンドフィールを適用するためにサイト全体のページに適用できます。

このテーマには、イメージや CSS ファイルは含まれません (web アプリケーションのルートフォルダーで定義されているように、スタイルシート `Styles.css` そのままにしておきます)。ただし、2つのスキンが含まれます。 スキンは、Web コントロールの既定のプロパティを定義するファイルです。 具体的には、GridView コントロールと DetailsView コントロールのスキンファイルがあり、既定の `CssClass`関連のプロパティを示しています。

まず、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択して、`GridView.skin` という名前のプロジェクトに新しいスキンファイルを追加します。

[GridView という名前のスキンファイルを追加 ![には](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**図 9**: `GridView.skin` という名前のスキンファイルを追加[する (クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image25.png)される)

スキンファイルは、`App_Themes` フォルダーにあるテーマに配置する必要があります。 このようなフォルダーをまだ持っていないため、Visual Studio では、最初のスキンを追加するときに、このフォルダーを作成するように提供します。 [はい] をクリックして `App_Theme` フォルダーを作成し、そこに新しい `GridView.skin` ファイルを配置します。

[![Visual Studio で App_Theme フォルダーを作成できるようにする](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**図 10**: Visual Studio で `App_Theme` フォルダーを作成できるよう[にする (クリックしてフルサイズのイメージを表示する](displaying-data-with-the-objectdatasource-vb/_static/image28.png))

これにより、GridView という名前の `App_Themes` フォルダーに、スキンファイル `GridView.skin`を含む新しいテーマが作成されます。

![GridView テーマが App_Theme フォルダーに追加されました](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**図 11**: GridView テーマが `App_Theme` フォルダーに追加されている

GridView テーマの名前を DataWebControls に変更します (`App_Theme` フォルダー内の GridView フォルダーを右クリックし、[名前の変更] を選択します)。 次に、`GridView.skin` ファイルに次のマークアップを入力します。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

これにより、DataWebControls テーマを使用する任意のページ内のすべての GridView の `CssClass`関連プロパティの既定のプロパティが定義されます。 この DetailsView に別のスキンを追加してみましょう。これは、すぐに使用するデータ Web コントロールです。 `DetailsView.skin` という名前の DataWebControls テーマに新しいスキンを追加し、次のマークアップを追加します。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

テーマを定義したら、最後の手順として、テーマを ASP.NET ページに適用します。 テーマは、ページごとに、または web サイト内のすべてのページに適用できます。 このテーマを web サイトのすべてのページで使用してみましょう。 これを実現するには、次のマークアップを `Web.config`の `<system.web>` セクションに追加します。

[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

これですべて完了です。 `styleSheetTheme` 設定は、テーマで指定されたプロパティが、コントロールレベルで指定されたプロパティをオーバーライドし*ない*ようにすることを示します。 テーマ設定でコントロールの設定を優先するように指定するには、`styleSheetTheme`の代わりに `theme` 属性を使用します。残念ながら、Visual Studio のデザインビューにテーマの設定は表示されません。 テーマとスキンの詳細については、 [「ASP.NET theme And スキンの概要」と「](https://msdn.microsoft.com/library/ykzx33wh.aspx) [テーマを使用したサーバー側のスタイル](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)」を参照してください。テーマを使用するようにページを構成する方法の詳細については、「[方法: ASP.NET テーマを適用](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx)する」を参照してください。

[GridView に ![製品の名前、カテゴリ、仕入先、価格、および廃止された情報が表示されます。](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**図 12**: GridView には、製品名、カテゴリ、仕入先、価格、および廃止された情報が表示されます ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image32.png)されます)

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>DetailsView で一度に1つのレコードを表示する

GridView には、バインド先のデータソースコントロールによって返されるレコードごとに1行のデータが表示されます。 ただし、1つのレコードだけを表示したい場合や、一度に1つのレコードだけを表示する場合があります。 [DetailsView コントロール](https://msdn.microsoft.com/library/s3w1w7t4.aspx)には、この機能が用意されており、2つの列を含む HTML `<table>` としてレンダリングされ、コントロールにバインドされている列またはプロパティごとに1行が表示されます。 この DetailsView は、1つのレコードが90度回転した GridView と考えることができます。

まず、`SimpleDisplay.aspx`の GridView の*上*に DetailsView コントロールを追加します。 次に、GridView と同じ ObjectDataSource コントロールにバインドします。 GridView の場合と同様に、ObjectDataSource の `Select` メソッドによって返されるオブジェクトの各プロパティの DetailsView に BoundField が追加されます。 唯一の違いは、DetailsView の BoundFields が垂直方向ではなく水平方向にレイアウトされる点です。

[DetailsView をページに追加して ObjectDataSource にバインド ![には](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**図 13**: DetailsView をページに追加して ObjectDataSource にバインドする ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image35.png)されます)

GridView の場合と同様に、DetailsView の BoundFields を微調整して、ObjectDataSource によって返されるデータをよりカスタマイズした表示を提供できます。 図14は、BoundFields と `CssClass` プロパティが GridView の例と似たように構成された後の DetailsView を示しています。

[DetailsView に1つのレコードが表示される ![](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**図 14**: DetailsView に1つのレコードが表示される ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image38.png)されます)

DetailsView には、データソースから返された最初のレコードのみが表示されることに注意してください。 ユーザーがすべてのレコードを1つずつステップ実行できるようにするには、DetailsView のページングを有効にする必要があります。 これを行うには、Visual Studio に戻り、DetailsView のスマートタグの [ページングを有効にする] チェックボックスをオンにします。

[DetailsView コントロールでページングを有効に ![には](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**図 15**: DetailsView コントロールでページングを有効にする ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image41.png)されます)

[ページングが有効になっている ![、DetailsView を使用すると、ユーザーは任意の製品を表示できます。](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**図 16**: ページングが有効になっている場合、DetailsView を使用すると、ユーザーは任意の製品を表示できます ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image44.png)されます)。

ページングの詳細については、今後のチュートリアルで説明します。

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>一度に1つのレコードを表示するためのより柔軟なレイアウト

DetailsView は、ObjectDataSource から返された各レコードを表示する方法において非常に厳密です。 データのより柔軟なビューが必要になる場合があります。 たとえば、製品名、カテゴリ、仕入先、価格、および廃止された情報をそれぞれ別の行に表示するのではなく、`<h4>` の見出しに製品名と価格を表示し、名前と価格の下にカテゴリおよび仕入先の情報を小さいフォントサイズで表示することをお勧めします。 また、値の横にプロパティ名 (製品、カテゴリなど) が表示されない場合もあります。

[FormView コントロール](https://msdn.microsoft.com/library/fyf1dk77.aspx)は、このレベルのカスタマイズを提供します。 FormView では、(GridView や DetailsView と同様に) フィールドを使用するのではなく、Web コントロール、静的な HTML、および[databinding の構文](http://www.15seconds.com/issue/040630.htm)を組み合わせて使用できるテンプレートを使用します。 ASP.NET 1.x の Repeater コントロールに慣れている場合は、FormView を1つのレコードを表示するためのリピータと見なすことができます。

FormView コントロールを `SimpleDisplay.aspx` ページのデザインサーフェイスに追加します。 最初に、FormView はグレーのブロックとして表示され、少なくともコントロールの `ItemTemplate`を提供する必要があることを通知します。

[FormView に ItemTemplate を含める必要がある ![](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**図 17**: FormView に `ItemTemplate` が含まれている必要があります ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image47.png)されます)

Formview のスマートタグを使用すると、FormView を直接データソースコントロールにバインドできます。これにより、ObjectDataSource コントロールの `InsertMethod` および `UpdateMethod` プロパティが設定されている場合に、`EditItemTemplate` と `InsertItemTemplate`と共に、既定の `ItemTemplate` が自動的に作成されます。 ただし、この例では、データを FormView にバインドし、その `ItemTemplate` を手動で指定してみましょう。 まず、FormView の `DataSourceID` プロパティを ObjectDataSource コントロールの `ID` に設定し、`ObjectDataSource1`します。 次に、`ItemTemplate` を作成します。これにより、製品の名前と価格が `<h4>` 要素に表示され、カテゴリと出荷業者の名前が小さいフォントサイズで表示されるようになります。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]

[最初の製品 (Chai) がカスタム形式で表示される ![](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**図 18**: 最初の製品 (Chai) がカスタム形式で表示される ([クリックすると、フルサイズの画像が表示](displaying-data-with-the-objectdatasource-vb/_static/image50.png)されます)

`<%# Eval(propertyName) %>` は、データバインド構文です。 `Eval` メソッドは、FormView コントロールにバインドされている現在のオブジェクトについて、指定されたプロパティの値を返します。 データバインドの入出力の詳細については、Alex Homer の記事「 [ASP.NET 2.0 の簡略化および拡張されたデータバインディング構文」](http://www.15seconds.com/issue/040630.htm)を参照してください。

DetailsView と同様に、FormView は、ObjectDataSource から返された最初のレコードのみを表示します。 FormView でページングを有効にすると、ユーザーが一度に1つずつ製品をステップ実行できるようになります。

## <a name="summary"></a>まとめ

ビジネスロジックレイヤーからのデータへのアクセスと表示は、ASP.NET 2.0 の ObjectDataSource コントロールによってコード行を記述しなくても実現できます。 ObjectDataSource は、クラスの指定されたメソッドを呼び出し、結果を返します。 これらの結果は、ObjectDataSource にバインドされているデータ Web コントロールに表示できます。 このチュートリアルでは、GridView、DetailsView、および FormView コントロールを ObjectDataSource にバインドする方法について説明しました。

ここまでは、ObjectDataSource を使用してパラメーターのないメソッドを呼び出す方法について説明しましたが、`ProductBLL` クラスの `GetProductsByCategoryID(categoryID)`などの入力パラメーターを必要とするメソッドを呼び出す場合はどうでしょうか。 1つ以上のパラメーターを受け取るメソッドを呼び出すには、これらのパラメーターの値を指定するように ObjectDataSource を構成する必要があります。 これを実現する方法については、[次のチュートリアル](declarative-parameters-vb.md)で説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [独自のデータソースコントロールを作成する](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2.0 の GridView の例](https://msdn.microsoft.com/library/aa479339.aspx)
- [ASP.NET 2.0 での簡略化および拡張されたデータバインディング構文](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0 のテーマ](http://www.odetocode.com/Articles/423.aspx)
- [テーマを使用したサーバー側のスタイル](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [方法: プログラムによって ASP.NET テーマを適用する](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [次へ](declarative-parameters-vb.md)
