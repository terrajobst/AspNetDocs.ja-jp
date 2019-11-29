---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
title: ファイルのアップロード (VB) |Microsoft Docs
author: rick-anderson
description: ユーザーがバイナリファイル (Word や PDF ドキュメントなど) を Web サイトにアップロードして、サーバーのファイルシステムに保存できるようにする方法について説明します。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: f7c00fbd-652c-433d-8ed3-0e5168a4d4df
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0d57ef2f1e8132f19777a7d14e94611c68adcd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615281"
---
# <a name="uploading-files-vb"></a>ファイルのアップロード (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_VB.exe)または[PDF のダウンロード](uploading-files-vb/_static/datatutorial54vb1.pdf)

> ユーザーがバイナリファイル (Word や PDF ドキュメントなど) を Web サイトにアップロードして、サーバーのファイルシステムまたはデータベースに格納できるようにする方法について説明します。

## <a name="introduction"></a>はじめに

これまでに説明したすべてのチュートリアルでは、テキストデータのみが使用されていました。 ただし、多くのアプリケーションには、テキストデータとバイナリデータの両方をキャプチャするデータモデルがあります。 オンラインのサイトでは、ユーザーが自分のプロファイルに関連付けられた画像をアップロードすることができます。 採用 web サイトでは、ユーザーが Microsoft Word または PDF ドキュメントとして resume をアップロードすることができます。

バイナリデータを操作すると、新しい一連の課題が加わります。 バイナリデータをアプリケーションにどのように格納するかを決定する必要があります。 新しいレコードの挿入に使用されるインターフェイスを更新して、ユーザーが自分のコンピューターからファイルをアップロードできるようにする必要があります。また、レコードに関連付けられているバイナリデータをダウンロードする手段を表示または指定するには、追加の手順を実行する必要があります。 このチュートリアルと次の3つのチュートリアルでは、これらの課題をハードルする方法について説明します。 これらのチュートリアルの最後に、すべてのカテゴリに画像と PDF のパンフレットを関連付ける、完全に機能するアプリケーションを構築します。 このチュートリアルでは、バイナリデータを格納するさまざまな手法について説明し、ユーザーが自分のコンピューターからファイルをアップロードし、web サーバーのファイルシステムに保存する方法について説明します。

> [!NOTE]
> アプリケーションのデータモデルの一部であるバイナリデータは、 [BLOB](http://en.wikipedia.org/wiki/Binary_large_object)(バイナリラージオブジェクトの頭字語) と呼ばれることもあります。 これらのチュートリアルでは、用語のバイナリデータを使用することを選択しました。ただし、BLOB という用語は同義です。

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>手順 1: バイナリデータ Web ページの操作を作成する

バイナリデータのサポートの追加に関連する課題の調査を開始する前に、まず、このチュートリアルに必要な ASP.NET ページを web サイトプロジェクトに作成し、次の3つについて説明します。 まず、`BinaryData`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![バイナリデータ関連のチュートリアルの ASP.NET ページを追加する](uploading-files-vb/_static/image1.gif)

**図 1**: バイナリデータ関連のチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`BinaryData` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](uploading-files-vb/_static/image2.gif)](uploading-files-vb/_static/image1.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image2.png)されます)

最後に、これらのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、GridView `<siteMapNode>`を拡張した後に、次のマークアップを追加します。

[!code-xml[Main](uploading-files-vb/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、バイナリデータチュートリアルを使用するための項目が含まれるようになりました。

![サイトマップに、バイナリデータの操作に関するチュートリアルのエントリが含まれるようになりました。](uploading-files-vb/_static/image3.gif)

**図 3**: サイトマップにバイナリデータの使用に関するチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>手順 2: バイナリデータを格納する場所の決定

Application s データモデルに関連付けられているバイナリデータは、web サーバーのファイルシステム上に、データベースに格納されているファイルへの参照が格納されている2か所のいずれかに格納できます。または (図4を参照)。 それぞれの方法には、独自の長所と短所があり、さらに詳細な説明があります。

[バイナリデータは、ファイルシステムに格納することも、データベースに直接格納する ![もできます。](uploading-files-vb/_static/image4.gif)](uploading-files-vb/_static/image3.png)

**図 4**: バイナリデータをファイルシステムに格納することも、データベースに直接格納することもできます ([クリックすると、フルサイズのイメージが表示](uploading-files-vb/_static/image4.png)されます)。

たとえば、Northwind データベースを拡張して、各製品に画像を関連付けるとします。 1つの方法として、これらのイメージファイルを web サーバーのファイルシステムに格納し、`Products` テーブルにパスを記録することができます。 この方法では、`varchar(200)`型の `Products` テーブルに `ImagePath` 列を追加します。 ユーザーが Chai 用に画像をアップロードすると、その画像は `~/Images/Tea.jpg`の web サーバーのファイルシステムに保存される可能性があります。 `~` はアプリケーションの物理パスを表します。 つまり、web サイトが `C:\Websites\Northwind\`物理パスをルートとしている場合、`~/Images/Tea.jpg` は `C:\Websites\Northwind\Images\Tea.jpg`と同じになります。 イメージファイルをアップロードした後、`Products` テーブルの Chai レコードを更新して、その `ImagePath` 列が新しいイメージのパスを参照するようにします。 `~/Images/Tea.jpg` を使用することも、すべての製品イメージをアプリケーションの `Images` フォルダーに配置することにした場合にのみ `Tea.jpg` することもできます。

バイナリデータをファイルシステムに格納する主な利点は次のとおりです。

- **実装が簡単**になりますが、データベース内に直接格納されているバイナリデータの格納と取得には、ファイルシステムを介してデータを操作する場合よりも少し多くのコードが必要になります。 さらに、ユーザーがバイナリデータを表示またはダウンロードするには、そのデータへの URL が表示されている必要があります。 データが web サーバーのファイルシステムに存在する場合、URL は簡単です。 ただし、データがデータベースに格納されている場合は、データベースからデータを取得して返す web ページを作成する必要があります。
- バイナリ**データへの広範なアクセス**。バイナリデータは、データベースからデータをプルできない他のサービスやアプリケーションにアクセスできる必要があります。 たとえば、各製品に関連付けられているイメージをユーザーが[FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)経由で利用できるようにする必要がある場合は、バイナリデータをファイルシステムに格納します。
- **パフォーマンス**バイナリデータがファイルシステムに格納されている場合、データベースサーバーと web サーバー間の要求とネットワークの輻輳は、バイナリデータがデータベース内に直接格納されている場合よりも小さくなります。

バイナリデータをファイルシステムに格納する場合の主な欠点は、データベースからデータを分離することです。 レコードが `Products` テーブルから削除された場合、web サーバーのファイルシステム上の関連ファイルは自動的には削除されません。 ファイルを削除するには、追加のコードを記述する必要があります。そうしないと、ファイルシステムが未使用の孤立したファイルによって乱雑になります。 さらに、データベースをバックアップするときは、関連付けられているバイナリデータのバックアップもファイルシステムに作成する必要があります。 データベースを別のサイトまたはサーバーに移動すると、同様の問題が生じます。

また、`varbinary`型の列を作成することによって、バイナリデータを Microsoft SQL Server 2005 データベースに直接格納することもできます。 他の可変長データ型と同様に、この列に保持できるバイナリデータの最大長を指定できます。 たとえば、最大5000バイトを予約するには、`varbinary(5000)`を使用します。`varbinary(MAX)` では、最大ストレージサイズを 2 GB にすることができます。

バイナリデータをデータベースに直接格納する主な利点は、バイナリデータとデータベースレコードの密結合です。 これにより、バックアップや別のサイトまたはサーバーへのデータベースの移動などのデータベース管理タスクが大幅に簡素化されます。 また、レコードを削除すると、対応するバイナリデータも自動的に削除されます。 バイナリデータをデータベースに格納すると、さらに微妙な利点もあります。 詳細については、「 [ASP.NET 2.0 を使用してデータベースにバイナリファイルを直接格納](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx)する」を参照してください。

> [!NOTE]
> Microsoft SQL Server 2000 以前のバージョンでは、`varbinary` データ型の上限は8000バイトでした。 最大 2 GB のバイナリデータを格納するには、代わりに[`image` データ型](https://msdn.microsoft.com/library/ms187993.aspx)を使用する必要があります。 ただし、SQL Server 2005 に `MAX` を追加すると、`image` データ型は非推奨とされます。 旧バージョンとの互換性のためには引き続きサポートされていますが、マイクロソフトは、今後のバージョンの SQL Server で `image` データ型が削除されることを発表しました。

古いデータモデルを使用している場合は、`image` データ型が表示されることがあります。 Northwind データベースの `Categories` テーブルには、カテゴリのイメージファイルのバイナリデータを格納するために使用できる `Picture` 列があります。 Northwind データベースには、Microsoft Access およびそれ以前のバージョンの SQL Server のルートがあるため、この列のデータ型は `image`です。

このチュートリアルと次の3つの方法では、両方の方法を使用します。 `Categories` テーブルには、カテゴリのイメージのバイナリコンテンツを格納するための `Picture` 列が既に用意されています。 追加の列 `BrochurePath`を追加して、web サーバーのファイルシステム上の PDF へのパスを格納します。これを使用すると、印刷品質と洗練されたカテゴリの概要を提供できます。

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>手順 3:`Categories`テーブルに`BrochurePath`列を追加する

現在、Categories テーブルには、`CategoryID`、`CategoryName`、`Description`、および `Picture`の4つの列しかありません。 これらのフィールドに加えて、カテゴリ s パンフレット (存在する場合) を指す新しいものを追加する必要があります。 この列を追加するには、サーバーエクスプローラーに移動し、テーブルをドリルダウンします。 `Categories` テーブルを右クリックし、[テーブル定義を開く] を選択します (図5を参照)。 サーバーエクスプローラーが表示されない場合は、[表示] メニューの [サーバーエクスプローラー] オプションを選択して起動するか、Ctrl + Alt + S キーを押します。

`BrochurePath` という名前の `Categories` テーブルに新しい `varchar(200)` 列を追加し `NULL` s を許可し、[保存] アイコンをクリックします (または Ctrl + S キーを押します)。

[BrochurePath 列を Categories テーブルに追加 ![には](uploading-files-vb/_static/image5.gif)](uploading-files-vb/_static/image5.png)

**図 5**: `Categories` テーブルに `BrochurePath` 列を追加する ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image6.png)されます)

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>手順 4:`Picture`と`BrochurePath`列を使用するようにアーキテクチャを更新する

現在、データアクセス層 (DAL) の `CategoriesDataTable` には、`CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`という4つの `DataColumn` が定義されています。 [データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)チュートリアルでこの DataTable を設計したので、`CategoriesDataTable` には最初の3つの列のみがありました。`NumberOfProducts` 列は、[詳細な DataList チュートリアルが含まれている、マスターレコードの箇条書きリストを使用してマスター/詳細](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)に追加されました。

「*データアクセス層の作成*」で説明したように、型指定されたデータセット内の datatable はビジネスオブジェクトを構成します。 Tableadapter は、データベースとの通信を行い、ビジネスオブジェクトにクエリ結果を設定します。 `CategoriesDataTable` は、次の3つのデータ取得方法を持つ `CategoriesTableAdapter`によって設定されます。

- `GetCategories()` では、TableAdapter のメインクエリが実行され、`Categories` テーブル内のすべてのレコードの `CategoryID`、`CategoryName`、および `Description` の各フィールドが返されます。 メインクエリは、自動生成される `Insert` および `Update` メソッドによって使用されます。
- `GetCategoryByCategoryID(categoryID)` は、`CategoryID` が*categoryID*と等しいカテゴリの `CategoryID`、`CategoryName`、および `Description` の各フィールドを返します。
- `GetCategoriesAndNumberOfProducts()`-`Categories` テーブル内のすべてのレコードの `CategoryID`、`CategoryName`、および `Description` の各フィールドを返します。 また、サブクエリを使用して、各カテゴリに関連付けられている製品の数を返します。

これらのクエリによって `Categories` table s `Picture` または `BrochurePath` 列が返されないことに注意してください。また、`CategoriesDataTable` は、これらのフィールドに `DataColumn` を提供しません。 Picture プロパティと `BrochurePath` プロパティを操作するには、まずそれらを `CategoriesDataTable` に追加し、次にこれらの列を返すように `CategoriesTableAdapter` クラスを更新する必要があります。

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>`Picture`と`BrochurePath``DataColumn` の追加

まず、これらの2つの列を `CategoriesDataTable`に追加します。 `CategoriesDataTable` s ヘッダーを右クリックし、コンテキストメニューの [追加] をクリックして、[列] オプションを選択します。 これにより、`Column1`という名前の DataTable に新しい `DataColumn` が作成されます。 この列の名前を `Picture`に変更します。 プロパティウィンドウから、`DataColumn` s `DataType` プロパティを `System.Byte[]` に設定します (これはドロップダウンリストのオプションではなく、に入力する必要があります)。

[データ型が system.string [] である DataColumn 名前付き画像を作成 ![には](uploading-files-vb/_static/image6.gif)](uploading-files-vb/_static/image7.png)

**図 6**: `DataType` を `System.Byte[]` する `Picture` という名前の `DataColumn` を作成[する (クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image8.png)されます)

DataTable に別の `DataColumn` を追加し、既定の `DataType` 値 (`System.String`) を使用して `BrochurePath` 名前を付けます。

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>TableAdapter から`Picture`と`BrochurePath`の値を返す

これら2つの `DataColumn` が `CategoriesDataTable`に追加されたので、`CategoriesTableAdapter`を更新する準備ができました。 これらの両方の列の値をメインの TableAdapter クエリに返すこともできますが、これにより `GetCategories()` メソッドが呼び出されるたびにバイナリデータが返されます。 代わりに、を使用して `BrochurePath` を戻し、特定の category s `Picture` 列を返す追加のデータ取得メソッドを作成します。

TableAdapter のメインクエリを更新するには、`CategoriesTableAdapter` s ヘッダーを右クリックし、コンテキストメニューから [構成] オプションを選択します。 これにより、テーブルアダプター構成ウィザードが表示されます。これについては、これまでに説明したいくつかのチュートリアルで説明しました。 クエリを更新して `BrochurePath` を戻し、[完了] をクリックします。

[SELECT ステートメントの列リストを ![更新して、BrochurePath も返すようにします。](uploading-files-vb/_static/image7.gif)](uploading-files-vb/_static/image9.png)

**図 7**: `SELECT` ステートメントの列リストを更新して `BrochurePath` も返す ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image10.png)されます)

TableAdapter にアドホック SQL ステートメントを使用する場合、メインクエリの列リストを更新すると、TableAdapter 内のすべての `SELECT` クエリメソッドの列リストが更新されます。 つまり、`GetCategoryByCategoryID(categoryID)` メソッドが更新され、`BrochurePath` 列が返されることになります。これは、意図したように思われるかもしれません。 ただし、`GetCategoriesAndNumberOfProducts()` メソッドの列リストも更新され、各カテゴリの製品数を返すサブクエリが削除されました。 そのため、このメソッドを `SELECT` クエリに更新する必要があります。 `GetCategoriesAndNumberOfProducts()` メソッドを右クリックし、[構成] を選択して、`SELECT` クエリを元の値に戻します。

[!code-sql[Main](uploading-files-vb/samples/sample2.sql)]

次に、特定のカテゴリの `Picture` 列の値を返す新しい TableAdapter メソッドを作成します。 `CategoriesTableAdapter` s ヘッダーを右クリックし、[クエリの追加] オプションを選択して、TableAdapter クエリの構成ウィザードを起動します。 このウィザードの最初の手順では、アドホック SQL ステートメント、新しいストアドプロシージャ、または既存のストアドプロシージャを使用してデータのクエリを実行するかどうかを確認します。 [SQL ステートメントを使用する] を選択し、[次へ] をクリックします。 ここでは行を返すため、2番目の手順で [SELECT from rows] (行を返す) オプションを選択します。

[![[SQL ステートメントを使用する] オプションを選択する](uploading-files-vb/_static/image8.gif)](uploading-files-vb/_static/image11.png)

**図 8**: [SQL ステートメントを使用する] オプションを選択[する (クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image12.png)されます)

[![クエリは Categories テーブルからレコードを返すので、[行を返す SELECT] を選択します。](uploading-files-vb/_static/image9.gif)](uploading-files-vb/_static/image13.png)

**図 9**: クエリは Categories テーブルからレコードを返すため、[行を返す SELECT] を選択します ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image14.png)されます)

3番目の手順で、次の SQL クエリを入力し、[次へ] をクリックします。

[!code-sql[Main](uploading-files-vb/samples/sample3.sql)]

最後の手順では、新しいメソッドの名前を選択します。 `FillCategoryWithBinaryDataByCategoryID` と `GetCategoryWithBinaryDataByCategoryID` を使用して DataTable にデータを格納し、それぞれ DataTable パターンを返します。 [完了] をクリックしてウィザードを終了します。

[TableAdapter のメソッドの名前を選択 ![には](uploading-files-vb/_static/image10.gif)](uploading-files-vb/_static/image15.png)

**図 10**: TableAdapter のメソッドの名前を選択する ([クリックすると、フルサイズのイメージが表示](uploading-files-vb/_static/image16.png)されます)

> [!NOTE]
> テーブルアダプターのクエリ構成ウィザードを完了すると、新しいコマンドテキストがメインクエリのスキーマとは異なるスキーマを使用してデータを返すことを通知するダイアログボックスが表示される場合があります。 つまり、ウィザードでは、TableAdapter のメインクエリ `GetCategories()` が、先ほど作成したものとは異なるスキーマを返すことに注意してください。 しかし、これが必要なので、このメッセージは無視してかまいません。

また、アドホック SQL ステートメントを使用しているときに、ウィザードを使用して後で TableAdapter のメインクエリを変更する場合は、`GetCategoryWithBinaryDataByCategoryID` method s `SELECT` ステートメント s 列リストが変更され、メインクエリからの列だけが含まれることに注意してください (つまり、クエリから `Picture` 列が削除されます)。 この手順の前の `GetCategoriesAndNumberOfProducts()` 方法と同様に、列リストを手動で更新して `Picture` 列を返す必要があります。

2つの `DataColumn` s を `CategoriesDataTable` に追加し、`GetCategoryWithBinaryDataByCategoryID` メソッドを `CategoriesTableAdapter`に追加すると、型指定されたデータセットデザイナーのこれらのクラスは、図11のスクリーンショットのようになります。

![データセットデザイナーには、新しい列とメソッドが含まれています。](uploading-files-vb/_static/image11.gif)

**図 11**: データセットデザイナーに新しい列とメソッドが含まれる

## <a name="updating-the-business-logic-layer-bll"></a>ビジネスロジック層 (BLL) を更新しています

DAL を更新すると、新しい `CategoriesTableAdapter` メソッドのメソッドを含むように、ビジネスロジック層 (BLL) が拡張されます。 次のメソッドを `CategoriesBLL` クラスに追加します。

[!code-vb[Main](uploading-files-vb/samples/sample4.vb)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>手順 5: クライアントから Web サーバーにファイルをアップロードする

バイナリデータを収集するときは、多くの場合、このデータがエンドユーザーによって提供されます。 この情報を取得するには、ユーザーが自分のコンピューターから web サーバーにファイルをアップロードできる必要があります。 アップロードされたデータは、データモデルと統合する必要があります。これは、ファイルを web サーバーのファイルシステムに保存し、データベース内のファイルへのパスを追加したり、バイナリコンテンツをデータベースに直接書き込んだりすることを意味します。 この手順では、ユーザーが自分のコンピューターからサーバーにファイルをアップロードできるようにする方法について説明します。 次のチュートリアルでは、アップロードしたファイルとデータモデルを統合することに注目します。

ASP.NET 2.0 s new [FileUpload web control](https://msdn.microsoft.com/library/ms227677(VS.80).aspx)は、ユーザーが自分のコンピューターから web サーバーにファイルを送信するためのメカニズムを提供します。 FileUpload コントロールは、`type` 属性が file に設定されている `<input>` 要素としてレンダリングされます。この要素は、ブラウザーが [参照] ボタンを持つテキストボックスとして表示されます。 [参照] ボタンをクリックすると、ユーザーがファイルを選択できるダイアログボックスが表示されます。 フォームがポストバックされると、選択したファイルの内容がポストバックと共に送信されます。 サーバー側では、アップロードされたファイルに関する情報には、FileUpload control s プロパティを使用してアクセスできます。

ファイルのアップロードをデモンストレーションするには、`BinaryData` フォルダーの `FileUpload.aspx` ページを開き、ツールボックス から FileUpload コントロールをデザイナーにドラッグして、コントロール s `ID` プロパティを `UploadTest`に設定します。 次に、ボタン Web コントロールを追加し、その `ID` を設定し `Text` プロパティを `UploadButton` して、選択したファイルをそれぞれアップロードします。 最後に、ボタンの下にラベル Web コントロールを配置し、その `Text` プロパティをオフにして、`ID` プロパティを `UploadDetails`に設定します。

[FileUpload コントロールを ASP.NET ページに追加 ![には](uploading-files-vb/_static/image12.gif)](uploading-files-vb/_static/image17.png)

**図 12**: FileUpload コントロールを ASP.NET ページに追加する ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image18.png)されます)

図13は、ブラウザーを使用して表示するときにこのページを示しています。 [参照] ボタンをクリックすると、[ファイルの選択] ダイアログボックスが表示され、ユーザーは自分のコンピューターからファイルを選択できることに注意してください。 ファイルを選択したら、[選択したファイルのアップロード] ボタンをクリックすると、選択したファイルのバイナリコンテンツを web サーバーに送信するポストバックが発生します。

[ユーザーが自分のコンピューターからサーバーにアップロードするファイルを選択できる ![](uploading-files-vb/_static/image13.gif)](uploading-files-vb/_static/image19.png)

**図 13**: ユーザーは自分のコンピューターからサーバーにアップロードするファイルを選択できます ([クリックすると、フルサイズの画像が表示](uploading-files-vb/_static/image20.png)されます)

ポストバック時には、アップロードされたファイルをファイルシステムに保存することも、バイナリデータをストリーム経由で直接操作することもできます。 この例では、`~/Brochures` フォルダーを作成し、アップロードしたファイルをそこに保存します。 まず、ルートディレクトリのサブフォルダーとして `Brochures` フォルダーをサイトに追加します。 次に、`UploadButton` s `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](uploading-files-vb/samples/sample5.vb)]

FileUpload コントロールには、アップロードされたデータを操作するためのさまざまなプロパティが用意されています。 たとえば、 [`HasFile` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx)は、ファイルがユーザーによってアップロードされたかどうかを示し、 [`FileBytes` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx)は、アップロードされたバイナリデータへのアクセスをバイト配列として提供します。 `Click` イベントハンドラーは、ファイルがアップロードされたことを確認してから開始します。 ファイルがアップロードされている場合、ラベルには、アップロードされたファイルの名前、バイト単位のサイズ、およびそのコンテンツタイプが表示されます。

> [!NOTE]
> ユーザーがファイルをアップロードできるようにするには、`HasFile` プロパティを確認し、`False`の場合は警告を表示するか、代わりに[RequiredFieldValidator コントロール](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx)を使用することができます。

FileUpload s `SaveAs(filePath)` は、アップロードされたファイルを指定したファイル*パス*に保存します。 *filePath*は、*仮想* *パス*(`/Brochures/SomeFile.pdf`) ではなく、*物理パス*(`C:\Websites\Brochures\SomeFile.pdf`) である必要があります。 [`Server.MapPath(virtPath)` メソッド](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx)は、仮想パスを受け取り、対応する物理パスを返します。 ここでは、仮想パスが `~/Brochures/fileName`ます。 *fileName*は、アップロードされたファイルの名前です。 仮想パスと物理パスの詳細および `Server.MapPath`の使用については、「 [using](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 」を参照してください。

`Click` イベントハンドラーが完了したら、ブラウザーでページをテストしてみてください。 [参照] ボタンをクリックしてハードドライブからファイルを選択し、[選択したファイルをアップロードします] ボタンをクリックします。 ポストバックは、選択されたファイルの内容を web サーバーに送信します。その後、ファイルに関する情報が表示され、`~/Brochures` フォルダーに保存されます。 ファイルをアップロードした後、Visual Studio に戻り、ソリューションエクスプローラーの [更新] ボタンをクリックします。 アップロードしたファイルが、~/パンフレットフォルダーに表示されます。

[EvolutionValley ファイルが Web サーバーにアップロードされた ![](uploading-files-vb/_static/image14.gif)](uploading-files-vb/_static/image21.png)

**図 14**: ファイル `EvolutionValley.jpg` が Web サーバーにアップロードされている ([クリックしてフルサイズの画像を表示する](uploading-files-vb/_static/image22.png))

![EvolutionValley が ~/パンフレットフォルダーに保存されました](uploading-files-vb/_static/image15.gif)

**図 15**: `EvolutionValley.jpg` が `~/Brochures` フォルダーに保存された

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>ファイルシステムへのアップロードされたファイルの保存との微妙な違い

Web サーバーのファイルシステムにアップロードするファイルを保存する際には、いくつかの微妙な対処が必要です。 まず、セキュリティの問題があります。 ファイルをファイルシステムに保存するには、ASP.NET ページを実行しているセキュリティコンテキストに書き込み権限が必要です。 ASP.NET Development Web サーバーは、現在のユーザーアカウントのコンテキストで実行されます。 Microsoft インターネットインフォメーションサービス (IIS) を web サーバーとして使用している場合、セキュリティコンテキストは IIS のバージョンとその構成によって異なります。

ファイルをファイルシステムに保存するもう1つの課題は、ファイルの名前付けに関するものです。 現在、このページでは、クライアントコンピューター上のファイルと同じ名前を使用して、アップロードされたすべてのファイルが `~/Brochures` ディレクトリに保存されます。 ユーザー A が `Brochure.pdf`という名前のパンフレットをアップロードすると、ファイルは `~/Brochure/Brochure.pdf`として保存されます。 しかし、それ以降のユーザー B が同じファイル名 (`Brochure.pdf`) を持つ別のパンフレットファイルをアップロードする場合はどうでしょうか。 現在のコードでは、ユーザー A s ファイルはユーザー B がアップロードして上書きされます。

ファイル名の競合を解決するには、いくつかの方法があります。 1つの方法として、同じ名前のファイルが既に存在する場合に、ファイルのアップロードを禁止することができます。 この方法では、ユーザー B が `Brochure.pdf`という名前のファイルをアップロードしようとしても、ファイルは保存されず、ユーザー B がファイルの名前を変更して再試行するように指示するメッセージが表示されます。 別の方法としては、一意のファイル名を使用してファイルを保存する方法があります。これは、[グローバル一意識別子 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)または対応するデータベースレコードの主キー列の値 (アップロードがデータモデルの特定の行に関連付けられていることを前提とします) です。 次のチュートリアルでは、これらのオプションについて詳しく説明します。

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>大量のバイナリデータに関連する課題

これらのチュートリアルでは、キャプチャされるバイナリデータのサイズが適度であることを前提としています。 数 mb 以上の大量のバイナリデータファイルを操作する場合は、これらのチュートリアルの範囲を超えて新しい課題が発生します。 たとえば、既定では、ASP.NET は 4 MB を超えるアップロードを拒否しますが、`Web.config`の[`<httpRuntime>` 要素](https://msdn.microsoft.com/library/e1f13641.aspx)を使用して構成することもできます。 IIS では、独自のファイルアップロードサイズ制限も設けられています。 詳細については、「 [IIS Upload File Size](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) 」を参照してください。 さらに、大きなファイルのアップロードにかかる時間は、ASP.NET が要求を待機する既定の110秒を超える場合があります。 また、大きなファイルを操作するときに発生するメモリとパフォーマンスの問題もあります。

FileUpload コントロールは、大きなファイルのアップロードには実用的ではありません。 ファイルの内容がサーバーにポストされている間、エンドユーザーは、アップロードの進行状況を確認せずに待機を我慢強く必要があります。 これは、数秒でアップロードできる小さなファイルを扱う場合の問題ではありませんが、アップロードに数分かかる可能性のある大きなファイルを処理する場合に問題になることがあります。 大規模なアップロードの処理に適したサードパーティ製のファイルアップロードコントロールがいくつかあります。これらのベンダーの多くは、より洗練されたユーザーエクスペリエンスを提供する進行状況インジケーターと ActiveX アップロードマネージャーを提供しています。

アプリケーションで大きなファイルを処理する必要がある場合は、問題を慎重に調査し、特定のニーズに適したソリューションを見つける必要があります。

## <a name="summary"></a>要約

バイナリデータをキャプチャする必要があるアプリケーションを構築すると、さまざまな課題が生じます。 このチュートリアルでは、最初の2つについて説明します。バイナリデータを格納する場所を決定し、ユーザーが web ページを使用してバイナリコンテンツをアップロードできるようにします。 次の3つのチュートリアルでは、アップロードされたデータをデータベース内のレコードに関連付ける方法と、バイナリデータをテキストデータフィールドと共に表示する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [大きな値のデータ型の使用](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload コントロールのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload サーバーコントロール](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [ファイルのアップロードのダークサイド](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy and Bernadette Leigh でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](updating-and-deleting-existing-binary-data-cs.md)
> [次へ](displaying-binary-data-in-the-data-web-controls-vb.md)
