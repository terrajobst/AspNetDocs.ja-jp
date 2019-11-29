---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
title: SqlDataSource コントロールを使用してデータにクエリを実行する (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、ObjectDataSource コントロールを使用して、プレゼンテーション層とデータアクセス層を完全に分離しています。 次の教えるで始まる...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: b12f752d-3502-40a4-b695-fc7b7d08cfd3
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 199ddb46e877c3a0937672d33241a240660684da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606017"
---
# <a name="querying-data-with-the-sqldatasource-control-vb"></a>SqlDataSource コントロールでデータにクエリを実行する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_VB.exe)または[PDF のダウンロード](querying-data-with-the-sqldatasource-control-vb/_static/datatutorial47vb1.pdf)

> 前のチュートリアルでは、ObjectDataSource コントロールを使用して、プレゼンテーション層とデータアクセス層を完全に分離しています。 このチュートリアルでは、プレゼンテーションとデータアクセスの厳密な分離を必要としない単純なアプリケーションに対して、SqlDataSource コントロールを使用する方法について説明します。

## <a name="introduction"></a>はじめに

これまでに説明したすべてのチュートリアルでは、プレゼンテーション、ビジネスロジック、およびデータアクセス層で構成される階層型アーキテクチャを使用してきました。 データアクセス層 (DAL) は、1つ目のチュートリアル ([データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)) とビジネスロジック層 ([ビジネスロジック層の作成](../introduction/creating-a-business-logic-layer-vb.md)) で作成されました。 「ObjectDataSource チュートリアル[を使用してデータを表示](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)する」から、ASP.NET 2.0 s new ObjectDataSource コントロールを使用して、プレゼンテーション層のアーキテクチャとの宣言によるインターフェイスを作成する方法を説明しました。

これまでのすべてのチュートリアルでは、アーキテクチャを使用してデータを処理してきましたが、ASP.NET ページから直接データベースデータにアクセスし、挿入、更新、削除することもできます。 これにより、特定のデータベースクエリとビジネスロジックが web ページに直接配置されます。 大規模または複雑なアプリケーションの場合、階層化されたアーキテクチャの設計、実装、および使用は、アプリケーションの成功、更新、および保守性を実現するために非常に重要です。 ただし、非常に単純な1回限りのアプリケーションを作成する場合、堅牢なアーキテクチャの開発は不要になることがあります。

ASP.NET 2.0 には、 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)、および[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)という5つの組み込みデータソースコントロールが用意されています。 SqlDataSource を使用すると、リレーショナルデータベース (Microsoft SQL Server、Microsoft Access、Oracle、MySQL など) から直接データにアクセスして変更を行うことができます。 このチュートリアルと次の3つのチュートリアルでは、SqlDataSource コントロールを操作する方法、データベースデータのクエリとフィルター処理の方法、および SqlDataSource を使用してデータを挿入、更新、および削除する方法について説明します。

![ASP.NET 2.0 には、5つの組み込みデータソースコントロールが含まれています](querying-data-with-the-sqldatasource-control-vb/_static/image1.gif)

**図 1**: ASP.NET 2.0 には、5つの組み込みデータソースコントロールが含まれています。

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>ObjectDataSource と SqlDataSource の比較

概念的には、ObjectDataSource と SqlDataSource の両方のコントロールが単にデータのプロキシになります。 「 [Objectdatasource を使用したデータの表示](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)」で説明したように、objectdatasource には、データを提供するオブジェクトの種類を示すプロパティと、基になるオブジェクトの種類からデータを選択、挿入、更新、および削除するために呼び出すメソッドがあります。 ObjectDataSource のプロパティが構成されたら、GridView、DetailsView、DataList などのデータ Web コントロールをコントロールにバインドできます。その際、ObjectDataSource s `Select()`、`Insert()`、`Delete()`、および `Update()` の各メソッドを使用して、基になるアーキテクチャと対話します。

SqlDataSource は同じ機能を提供しますが、オブジェクトライブラリではなくリレーショナルデータベースに対して動作します。 SqlDataSource を使用する場合は、データベース接続文字列と、データの挿入、更新、削除、および取得を実行するアドホック SQL クエリまたはストアドプロシージャを指定する必要があります。 SqlDataSource s `Select()`、`Insert()`、`Update()`、および `Delete()` メソッドを呼び出すと、指定されたデータベースに接続し、適切な SQL クエリを発行します。 次の図に示すように、これらのメソッドは、データベースへの接続、クエリの発行、および結果の取得の grunt を実行します。

![SqlDataSource は、データベースへのプロキシとして機能します。](querying-data-with-the-sqldatasource-control-vb/_static/image2.gif)

**図 2**: SqlDataSource はデータベースへのプロキシとして機能する

> [!NOTE]
> このチュートリアルでは、データベースからデータを取得することに重点を置いて説明します。 「 [Sqldatasource Control を使用したデータの挿入、更新、および削除](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)」チュートリアルでは、挿入、更新、および削除をサポートするように sqldatasource を構成する方法について説明します。

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource コントロールと AccessDataSource コントロール

SqlDataSource コントロールに加えて、ASP.NET 2.0 には AccessDataSource コントロールも含まれています。 これらの2つの異なるコントロールは、多くの開発者にとって ASP.NET 2.0 を使用することをお勧めします。これは、AccessDataSource コントロールが、Microsoft SQL Server でのみ動作するように設計された SqlDataSource コントロールを使用して、Microsoft Access でのみ動作するように設計さ AccessDataSource は、特に Microsoft Access で動作するように設計されていますが、SqlDataSource コントロールは、.NET を介してアクセスできる*任意*のリレーショナルデータベースで動作します。 これには、Microsoft SQL Server、Microsoft Access、Oracle、Informix、MySQL、PostgreSQL など、他の多くの OleDb または ODBC に準拠したデータストアが含まれます。

AccessDataSource と SqlDataSource コントロールの唯一の違いは、データベース接続情報を指定する方法です。 AccessDataSource コントロールには、Access データベースファイルへのファイルパスのみが必要です。 一方、SqlDataSource には、完全な接続文字列が必要です。

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>手順 1: SqlDataSource Web ページの作成

SqlDataSource コントロールを使用してデータベースデータを直接操作する方法を確認する前に、まず、このチュートリアルで必要な ASP.NET ページを web サイトプロジェクトに作成し、次の3つについて説明します。 まず、`SqlDataSource`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する](querying-data-with-the-sqldatasource-control-vb/_static/image3.gif)

**図 3**: SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`SqlDataSource` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](querying-data-with-the-sqldatasource-control-vb/_static/image5.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image4.gif)

**図 4**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](querying-data-with-the-sqldatasource-control-vb/_static/image6.gif)されます)

最後に、これらの4つのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、DataList および Repeater `<siteMapNode>`にカスタムボタンを追加した後に、次のマークアップを追加します。

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample1.sql)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、チュートリアルの編集、挿入、および削除を行うための項目が含まれています。

![サイトマップに、SqlDataSource チュートリアルのエントリが含まれるようになりました。](querying-data-with-the-sqldatasource-control-vb/_static/image7.gif)

**図 5**: サイトマップに SqlDataSource チュートリアルのエントリが含まれるようになった

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>手順 2: SqlDataSource コントロールの追加と構成

まず、`SqlDataSource` フォルダーの [`Querying.aspx`] ページを開いてデザインビューに切り替えます。 [ツールボックス] から [SqlDataSource] コントロールをデザイナーにドラッグし、その `ID` を [`ProductsDataSource`] に設定します。 ObjectDataSource と同様に、SqlDataSource はレンダリングされた出力を生成しないため、デザインサーフェイスに灰色のボックスとして表示されます。 SqlDataSource を構成するには、SqlDataSource s スマートタグから [データソースの構成] リンクをクリックします。

![SqlDataSource s スマートタグから [データソースの構成] リンクをクリックします。](querying-data-with-the-sqldatasource-control-vb/_static/image8.gif)

**図 6**: SqlDataSource s スマートタグから [データソースの構成] リンクをクリックする

これにより、[SqlDataSource control s データソースの構成] ウィザードが起動します。 ウィザードの手順は ObjectDataSource コントロールとは異なりますが、最終的な目的は、データソースを介してデータを取得、挿入、更新、および削除する方法の詳細を提供することと同じです。 SqlDataSource の場合は、使用する基になるデータベースを指定し、アドホック SQL ステートメントまたはストアドプロシージャを提供します。

ウィザードの最初のステップでは、データベースの入力を求められます。 ドロップダウンリストには、web アプリケーションの `App_Data` フォルダーにあるデータベースと、サーバーエクスプローラーの [データ接続] ノードに追加されたデータベースが表示されます。 `App_Data` フォルダー内の `NORTHWIND.MDF` データベースの接続文字列は、プロジェクトの `Web.config` ファイルに既に追加されているため、ドロップダウンリストには、その接続文字列への参照、`NORTHWINDConnectionString`が含まれています。 ドロップダウンリストからこの項目を選択し、[次へ] をクリックします。

![ドロップダウンリストから NORTHWINDConnectionString を選択します。](querying-data-with-the-sqldatasource-control-vb/_static/image9.gif)

**図 7**: ドロップダウンリストから `NORTHWINDConnectionString` を選択する

データベースを選択すると、ウィザードによって、データを返すクエリが要求されます。 返されるテーブルまたはビューの列を指定するか、カスタム SQL ステートメントを入力するか、ストアドプロシージャを指定できます。 このオプションは、[カスタム SQL ステートメントまたはストアドプロシージャの指定] と [テーブルまたはビューのオプション] ボタンからの列の指定によって切り替えることができます。

> [!NOTE]
> 最初の例では、[テーブルまたはビューから列を指定] オプションを使用します。 このチュートリアルの後半でウィザードに戻り、[カスタム SQL ステートメントまたはストアドプロシージャの指定] オプションを調べます。

図8は、[テーブルまたはビューから列を指定] オプションボタンが選択されている場合の [Select ステートメントの構成] 画面を示しています。 ドロップダウンリストには、Northwind データベースのテーブルとビューのセットが含まれています。選択したテーブルまたはビュー s 列が下のチェックボックスの一覧に表示されます。 この例では、を使用して、`Products` テーブルから `ProductID`、`ProductName`、および `UnitPrice` の各列を返します。 図8に示すように、これらのオプションを選択すると、結果として得られる SQL ステートメント `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`がウィザードに表示されます。

![Products テーブルからデータを返す](querying-data-with-the-sqldatasource-control-vb/_static/image10.gif)

**図 8**: `Products` テーブルからデータを返す

`Products` テーブルから `ProductID`、`ProductName`、および `UnitPrice` 列を返すようにウィザードを構成したら、[次へ] をクリックします。 この最後の画面では、前の手順で構成したクエリの結果を調べることができます。 [クエリのテスト] ボタンをクリックすると、構成済みの `SELECT` ステートメントが実行され、結果がグリッドに表示されます。

![[クエリのテスト] ボタンをクリックして、選択したクエリを確認します。](querying-data-with-the-sqldatasource-control-vb/_static/image11.gif)

**図 9**: [クエリのテスト] ボタンをクリックして `SELECT` クエリを確認する

ウィザードを完了するには、[完了] をクリックします。

ObjectDataSource の場合と同様に、SqlDataSource s ウィザードでは、コントロールのプロパティ、つまり[`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx)と[`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx)のプロパティに値が割り当てられるだけです。 ウィザードを完了すると、SqlDataSource コントロール s の宣言型マークアップは次のようになります。

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample2.aspx)]

`ConnectionString` プロパティは、データベースに接続する方法に関する情報を提供します。 このプロパティには、ハードコーディングされた完全な接続文字列値を割り当てることも、`Web.config`の接続文字列を指定することもできます。 Web.config の接続文字列値を参照するには、`<%$ expressionPrefix:expressionValue %>`構文を使用します。 通常、*式のプレフィックス*は ConnectionStrings で、*式の値*は `Web.config` [`<connectionStrings>` セクション](https://msdn.microsoft.com/library/bf7sd233.aspx)の接続文字列の名前です。 ただし、構文を使用して、リソースファイルから `<appSettings>` の要素やコンテンツを参照することができます。 この構文の詳細については、「 [ASP.NET 式の概要](https://msdn.microsoft.com/library/d5bd1tad.aspx)」を参照してください。

`SelectCommand` プロパティは、データを返すために実行するアドホック SQL ステートメントまたはストアドプロシージャを指定します。

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>手順 3: データ Web コントロールを追加し、SqlDataSource にバインドする

SqlDataSource が構成されると、GridView や DetailsView などのデータ Web コントロールにバインドできます。 このチュートリアルでは、を使用して GridView のデータを表示します。 [ツールボックス] から、GridView をページにドラッグして `ProductsDataSource` SqlDataSource にバインドします。これを行うには、GridView のスマートタグのドロップダウンリストからデータソースを選択します。

[GridView を追加して SqlDataSource コントロールにバインド ![には](querying-data-with-the-sqldatasource-control-vb/_static/image13.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image12.gif)

**図 10**: GridView を追加して SqlDataSource コントロールにバインドする ([クリックすると、フルサイズの画像が表示](querying-data-with-the-sqldatasource-control-vb/_static/image14.gif)されます)

GridView s スマートタグのドロップダウンリストから SqlDataSource コントロールを選択すると、データソースコントロールによって返される各列の GridView に BoundField または CheckBoxField が自動的に追加されます。 SqlDataSource は `ProductID`、`ProductName`、`UnitPrice` の3つのデータベース列を返すため、GridView には3つのフィールドがあります。

GridView の3つの連結フィールドを構成してみましょう。 `ProductName` field s `HeaderText` プロパティを Product Name に、`UnitPrice` フィールドを Price に変更します。 また、`UnitPrice` フィールドを通貨として書式設定します。 これらの変更を行った後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample3.aspx)]

ブラウザーを使用してこのページにアクセスします。 図11に示すように、GridView には、各製品の `ProductID`、`ProductName`、および `UnitPrice` 値が表示されます。

[GridView に ![各製品の ProductID、ProductName、および UnitPrice の値が表示されます](querying-data-with-the-sqldatasource-control-vb/_static/image16.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image15.gif)

**図 11**: GridView には、各製品の `ProductID`、`ProductName`、および `UnitPrice` の値が表示されます ([クリックすると、フルサイズの画像が表示](querying-data-with-the-sqldatasource-control-vb/_static/image17.gif)されます)

ページにアクセスすると、GridView はそのデータソースコントロール s `Select()` メソッドを呼び出します。 ObjectDataSource コントロールを使用していた場合、これは `ProductsBLL` クラス s `GetProducts()` メソッドと呼ばれます。 ただし、SqlDataSource を使用すると、`Select()` メソッドは、指定されたデータベースへの接続を確立し、`SelectCommand` (この例では`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`) を発行します。 SqlDataSource はその結果を返します。 GridView は、返された各データベースレコードに対して、GridView 内に行を作成します。

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>組み込みのデータ Web コントロール機能と SqlDataSource コントロール

一般に、データ Web コントロールに固有の機能 (ページング、並べ替え、編集、削除、挿入など) はデータ Web コントロールに固有であり、使用されるデータソースコントロールには依存しません。 つまり、GridView は、組み込みのページング、並べ替え、編集、および削除が ObjectDataSource または SqlDataSource にバインドされているかどうかを利用できます。 ただし、特定のデータ Web コントロール機能は、使用されているデータソースコントロールまたはデータソースコントロールの構成に依存しています。

たとえば、[大量のデータを効率的にページング](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)するチュートリアルでは、既定では、データ Web コントロールネイティブのページングロジックによって基になるデータソースから*すべて*のレコードが返されます。その後、現在のページインデックスとページごとに表示されるレコードの数に応じて、適切なレコードのサブセットのみが表示されます。 このモデルは、十分に大きな結果セットを使用してページングする場合、非常に非効率的です。 幸い、ObjectDataSource はカスタムページングをサポートするように構成できます。これにより、表示するレコードの正確なサブセットのみが返されます。 ただし、SqlDataSource コントロールには、カスタムページングを実装するためのプロパティがありません。

ページングと並べ替えを行う別のはらみが SqlDataSource で発生します。 既定では、SqlDataSource から返されるデータは、GridView を使用してページングまたは並べ替えを行うことができます。 これを示すには、`Querying.aspx` の GridView s スマートタグで [ページングを有効にし、並べ替えオプションを有効にする] をオンにして、これが想定どおりに動作することを確認します。

SqlDataSource は、緩い型のデータセットにデータベースデータを取得するため、並べ替えとページングが機能します。 クエリによって返されるレコードの合計数は、ページングを実装するために必要な要素として、データセットから確かめるすることができます。 さらに、データセットの結果は DataView を使用して並べ替えることができます。 これらの機能は、GridView がページングまたは並べ替えデータを要求するときに、SqlDataSource によって自動的に使用されます。

SqlDataSource は、その[`DataSourceMode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)を `DataSet` (既定) から `DataReader`に変更することによって、データセットではなく DataReader を返すように構成できます。 Datareader を使用する場合は、DataReader を想定している既存のコードに SqlDataSource s の結果を渡すと、状況によって好ましい場合があります。 さらに、Datareader はデータセットよりもはるかに単純なオブジェクトであるため、パフォーマンスが向上します。 ただし、この変更を行った場合、SqlDataSource ではクエリによって返されるレコード数を確認できず、返されたデータを並べ替えるための手法も用意されていないため、データ Web コントロールは並べ替えもページもできません。

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>手順 4: カスタム SQL ステートメントまたはストアドプロシージャの使用

SqlDataSource コントロールを構成する場合、データを返すために使用されるクエリは、カスタム SQL ステートメントまたはストアドプロシージャとして、または既存のテーブルまたはビューの列として、次の2つの方法のいずれかで指定できます。 手順2では、`Products` テーブルから列を選択します。 では、カスタム SQL ステートメントを使用する方法を見てみましょう。

別の GridView コントロールを `Querying.aspx` ページに追加し、スマートタグのドロップダウンリストから新しいデータソースを作成することを選択します。 次に、データがデータベースからプルされることを示します。これにより、新しい SqlDataSource コントロールが作成されます。 コントロールに `ProductsWithCategoryInfoDataSource`という名前を指定します。

![「製品とカテゴリのインフォデータソース」という名前の新しい SqlDataSource コントロールを作成します。](querying-data-with-the-sqldatasource-control-vb/_static/image18.gif)

**図 12**: `ProductsWithCategoryInfoDataSource` という名前の新しい SqlDataSource コントロールを作成する

次の画面では、データベースを指定するように求められます。 図7に戻ってきたように、ドロップダウンリストから `NORTHWINDConnectionString` を選択し、[次へ] をクリックします。 [Select ステートメントの構成] 画面で、[カスタム SQL ステートメントまたはストアドプロシージャを指定します] オプションを選択し、[次へ] をクリックします。 [カスタムステートメントまたはストアドプロシージャの定義] 画面が表示され、[選択]、[更新]、[挿入]、および [削除] というラベルの付いたタブが表示されます。 各タブで、テキストボックスにカスタム SQL ステートメントを入力するか、ドロップダウンリストからストアドプロシージャを選択できます。 このチュートリアルでは、カスタム SQL ステートメントの入力について説明します。次のチュートリアルでは、ストアドプロシージャを使用する例を紹介します。

![カスタム SQL ステートメントを入力するか、ストアドプロシージャを選択します。](querying-data-with-the-sqldatasource-control-vb/_static/image19.gif)

**図 13**: カスタム SQL ステートメントを入力するか、ストアドプロシージャを選択する

カスタム SQL ステートメントは、手動でテキストボックスに入力することも、[クエリビルダー] ボタンをクリックしてグラフィカルに作成することもできます。 `JOIN` テーブルから製品 `CategoryName` を取得するには、次のクエリを使用して、クエリビルダーまたはテキストボックスから、次のクエリを使用して、`Products` テーブルの `ProductID` と `ProductName` のフィールドを返します。

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample4.sql)]

![クエリは、を使用してグラフィカルに作成できクエリビルダー](querying-data-with-the-sqldatasource-control-vb/_static/image20.gif)

**図 14**: を使用してクエリをグラフィカルに作成する方法クエリビルダー

クエリを指定したら、[次へ] をクリックして [クエリのテスト] 画面に進みます。 [完了] をクリックして、SqlDataSource wizard を完了します。

ウィザードを完了すると、GridView に3つの連結されたフィールドが追加され、クエリから返された `ProductID`、`ProductName`、および `CategoryName` 列が表示され、次の宣言型マークアップが生成されます。

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample5.aspx)]

[GridView に ![、各製品の ID、名前、および関連付けられているカテゴリ名が表示されます。](querying-data-with-the-sqldatasource-control-vb/_static/image22.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image21.gif)

**図 15**: GridView には、各製品の ID、名前、および関連付けられているカテゴリ名が表示されます ([クリックすると、フルサイズの画像が表示](querying-data-with-the-sqldatasource-control-vb/_static/image23.gif)されます)

## <a name="summary"></a>要約

このチュートリアルでは、SqlDataSource コントロールを使用してデータのクエリと表示を行う方法について説明しました。 ObjectDataSource と同様に、SqlDataSource はプロキシとして機能し、データにアクセスするための宣言型のアプローチを提供します。 このプロパティは、接続先のデータベースと実行する SQL `SELECT` クエリを指定します。これらは、プロパティウィンドウまたはデータソースの構成ウィザードを使用して指定できます。

このチュートリアルで調べた `SELECT` クエリの例では、指定されたクエリのすべてのレコードが返されました。 ただし、SqlDataSource コントロールには、値がプログラムによって割り当てられるか、または指定されたソースから自動的にプルされるパラメーターを含む `WHERE` 句を含めることができます。 パラメーター化されたクエリを作成して使用する方法については、次のチュートリアルで説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [リレーショナルデータベースデータへのアクセス](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource コントロールの概要](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET クイックスタートチュートリアル: SqlDataSource コントロール](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 要素](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [データベース接続文字列のリファレンス](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、スーザン、Bernadette Leigh、David 藤巻 u でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
> [次へ](using-parameterized-queries-with-the-sqldatasource-vb.md)
