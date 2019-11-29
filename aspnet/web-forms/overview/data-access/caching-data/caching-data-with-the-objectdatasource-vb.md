---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: ObjectDataSource (VB) を使用したデータのキャッシュMicrosoft Docs
author: rick-anderson
description: キャッシュは、低速で高速な Web アプリケーションの違いを意味します。 このチュートリアルでは、ASP.NET でのキャッシュの詳細について説明します。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 16f20d9a0f4f677073174d680418b278dba40b07
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74612227"
---
# <a name="caching-data-with-the-objectdatasource-vb"></a>ObjectDataSource でデータをキャッシュする (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe)または[PDF のダウンロード](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> キャッシュは、低速で高速な Web アプリケーションの違いを意味します。 このチュートリアルでは、ASP.NET でのキャッシュの詳細について説明します。 キャッシュの主要な概念と、ObjectDataSource コントロールを介してプレゼンテーション層にキャッシュを適用する方法について説明します。

## <a name="introduction"></a>はじめに

コンピューターサイエンスでは、*キャッシュ*とは、アクセスしやすくなる場所にデータまたは情報を格納するのにコストがかかる情報を取得するプロセスです。 データドリブンアプリケーションでは、大規模で複雑なクエリは、通常、アプリケーションの実行時間の大部分を消費します。 このようなアプリケーションのパフォーマンスは、多くの場合、負荷の高いデータベースクエリの結果をアプリケーションのメモリに格納することで改善できます。

ASP.NET 2.0 には、さまざまなキャッシュオプションが用意されています。 *出力キャッシュ*を使用して、web ページまたはユーザーコントロールに表示されるマークアップ全体をキャッシュできます。 ObjectDataSource および SqlDataSource コントロールはキャッシュ機能も提供しているため、コントロールレベルでデータをキャッシュできます。 および ASP.NET s*データキャッシュ*は、ページ開発者がオブジェクトをプログラムによってキャッシュできるようにする、豊富なキャッシュ API を提供します。 このチュートリアルと次の3つのチュートリアルでは、ObjectDataSource のキャッシュ機能とデータキャッシュを使用して検証します。 また、起動時にアプリケーション全体のデータをキャッシュする方法と、SQL キャッシュの依存関係を使用してキャッシュされたデータを最新の状態に保つ方法についても説明します。 これらのチュートリアルでは、出力キャッシュについては説明しません。 出力キャッシュの詳細については、「 [ASP.NET 2.0 の出力キャッシュ](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)」を参照してください。

キャッシュは、データアクセス層からプレゼンテーション層まで、アーキテクチャ内の任意の場所で適用できます。 このチュートリアルでは、ObjectDataSource コントロールを介してプレゼンテーション層にキャッシュを適用する方法について説明します。 次のチュートリアルでは、ビジネスロジック層のキャッシュデータについて説明します。

## <a name="key-caching-concepts"></a>キーキャッシュの概念

キャッシュを使用すると、アプリケーションのパフォーマンスとスケーラビリティを大幅に向上させることができます。データを生成して、より効率的にアクセスできる場所に格納することによって、アプリケーションの全体的なパフォーマンスとスケーラビリティを向上させることができます。 キャッシュは、実際の基になるデータのコピーだけを保持しているため、基になるデータが変更された場合、古くなったり、*古く*なったりする可能性があります。 これに対処するために、ページ開発者は、次のいずれかを使用して、キャッシュ項目がキャッシュから*削除*される条件を示すことができます。

- **時間ベースの条件**キャッシュに項目を追加することができます。 たとえば、ページ開発者は、60秒という期間を示すことができます。 絶対期間では、キャッシュされた項目は、アクセスされた頻度に関係なく、キャッシュに追加された後、60秒間削除されます。 スライディング継続時間では、キャッシュされた項目は最後のアクセスから60秒後に削除されます。
- **依存関係ベースの条件**キャッシュに追加されたときに、依存関係を項目に関連付けることができます。 項目の依存関係が変更されると、項目はキャッシュから削除されます。 依存関係には、ファイル、別のキャッシュ項目、またはその2つの組み合わせを使用できます。 ASP.NET 2.0 では、SQL キャッシュの依存関係も許可されます。これにより、開発者は項目をキャッシュに追加し、基になるデータベースデータが変更されたときに削除することができます。 Sql キャッシュの依存関係については、後の[「](using-sql-cache-dependencies-vb.md) sql キャッシュの依存関係」のチュートリアルで確認します。

指定された削除条件に関係なく、キャッシュ内の項目は、時間ベースまたは依存関係ベースの条件が満たされる前に*清掃*されることがあります。 キャッシュが容量に達した場合は、既存の項目を削除してから、新しい項目を追加する必要があります。 その結果、プログラムを使用してキャッシュされたデータを操作するときは、キャッシュされたデータが存在しないと常に想定することが重要です。 次のチュートリアルでは、プログラムによってキャッシュからデータにアクセスするときに使用するパターンについて説明します。*アーキテクチャでのデータのキャッシュ*に関する記事をご覧ください。

キャッシュは、アプリケーションのパフォーマンスを向上させる経済的な手段を提供します。 ASP.NET の記事では、[秋山 Smith](http://aspadvice.com/blogs/ssmith/)示されるとして、次のよう[な手法とベストプラクティス](https://msdn.microsoft.com/library/aa478965.aspx)をご紹介します。

キャッシュを使用すると、時間と分析を頻繁に行うことなく、十分なパフォーマンスを得ることができます。 メモリは安価であるため、コードまたはデータベースの最適化を試みる1日または1週間ではなく、30秒間の出力をキャッシュすることによって、必要なパフォーマンスを得ることができます。キャッシュソリューション (30 秒前のデータが ok であることを前提としています) とに移動します。 最終的には、設計が悪いと、アプリケーションを正しく設計する必要があります。 しかし、現在、十分なパフォーマンスを発揮する必要がある場合は、キャッシュが優れた [アプローチ] であるため、後でアプリケーションをリファクタリングする時間を確保できます。

キャッシュを使用すると、ほどのパフォーマンスを向上させることができますが、リアルタイムで頻繁に更新されるデータを使用するアプリケーションや、間もなく期限切れになる古いデータを使用できない場合など、すべての状況で適用することはできません。 しかし、ほとんどのアプリケーションでは、キャッシュを使用する必要があります。 ASP.NET 2.0 でのキャッシュの背景については、 [ASP.NET 2.0 のクイックスタートチュートリアル](https://quickstarts.asp.net/QuickStartv20/aspnet/)の[パフォーマンスのキャッシュ](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx)に関するセクションを参照してください。

## <a name="step-1-creating-the-caching-web-pages"></a>手順 1: キャッシュ Web ページの作成

ObjectDataSource のキャッシュ機能の探索を開始する前に、まず、このチュートリアルに必要な ASP.NET ページを web サイトプロジェクトに作成し、次の3つについて説明します。 まず、`Caching`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![キャッシュ関連のチュートリアルの ASP.NET ページを追加する](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**図 1**: キャッシュ関連のチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`Caching` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[![図 2: default.aspx に SectionLevelTutorialListing ユーザーコントロールを追加する](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**図 2**: 図 2: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](caching-data-with-the-objectdatasource-vb/_static/image4.png)されます)

最後に、これらのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、バイナリデータ `<siteMapNode>`の操作後に、次のマークアップを追加します。

[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、キャッシュのチュートリアルの項目が含まれるようになりました。

![サイトマップにキャッシュチュートリアルのエントリが含まれるようになりました。](caching-data-with-the-objectdatasource-vb/_static/image5.png)

**図 3**: サイトマップにキャッシュチュートリアルのエントリが含まれるようになった

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>手順 2: Web ページに製品の一覧を表示する

このチュートリアルでは、ObjectDataSource コントロール s に組み込まれているキャッシュ機能の使用方法について説明します。 ただし、これらの機能を確認する前に、最初にページを使用する必要があります。 GridView を使用して `ProductsBLL` クラスから ObjectDataSource によって取得された製品情報を一覧表示する web ページを作成します。

まず、`Caching` フォルダーの [`ObjectDataSource.aspx`] ページを開きます。 GridView をツールボックスからデザイナーにドラッグし、その `ID` プロパティを `Products`に設定します。そのスマートタグから、`ProductsDataSource`という名前の新しい ObjectDataSource コントロールにバインドします。 `ProductsBLL` クラスで動作するように ObjectDataSource を構成します。

[製品の Bll クラスを使用するように ObjectDataSource を構成 ![には](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**図 4**: `ProductsBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](caching-data-with-the-objectdatasource-vb/_static/image8.png))

このページでは、編集可能な GridView を作成して、ObjectDataSource でキャッシュされたデータが GridView のインターフェイスを通じて変更された場合の動作を確認できるようにします。 [選択] タブのドロップダウンリストを既定値の `GetProducts()`のままにします。ただし、[更新] タブで選択した項目を、`productName`、`unitPrice`、および `productID` を入力パラメーターとして受け取る `UpdateProduct` のオーバーロードに変更します。

[[更新] タブのドロップダウンリストを適切な UpdateProduct オーバーロードに設定 ![](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**図 5**: [更新] タブのドロップダウンリストを適切な `UpdateProduct` オーバーロードに設定する ([クリックすると、フルサイズの画像が表示](caching-data-with-the-objectdatasource-vb/_static/image11.png)されます)

最後に、[挿入] タブと [削除] タブのドロップダウンリストを (なし) に設定し、[完了] をクリックします。 データソースの構成ウィザードの完了時に、Visual Studio は ObjectDataSource s `OldValuesParameterFormatString` プロパティを `original_{0}`に設定します。 [「データの挿入、更新、削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)」のチュートリアルで説明したように、このプロパティは、宣言構文から削除するか、既定値の `{0}`に戻す必要があります。これにより、更新ワークフローはエラーなしで続行されます。

さらに、ウィザードの完了時に、Visual Studio によって各製品データフィールドの GridView にフィールドが追加されます。 `ProductName`、`CategoryName`、および `UnitPrice` BoundFields 以外はすべて削除します。 次に、それぞれの BoundFields の `HeaderText` プロパティを、それぞれ Product、Category、および Price に更新します。 `ProductName` フィールドが必要であるため、BoundField を TemplateField に変換し、`EditItemTemplate`に RequiredFieldValidator を追加します。 同様に、`UnitPrice` BoundField を TemplateField に変換し、CompareValidator を追加して、ユーザーが入力した値が0以上の有効な通貨値であることを確認します。 これらの変更に加えて、`UnitPrice` 値を右揃えにしたり、読み取り専用インターフェイスと編集インターフェイスで `UnitPrice` テキストの書式設定を指定したりするなど、美しい変更を自由に実行できます。

Gridview s スマートタグの [編集を有効にする] チェックボックスをオンにして、GridView を編集可能にします。 また、[ページングを有効にし、並べ替えを有効にする] チェックボックスをオンにします。

> [!NOTE]
> GridView の編集インターフェイスをカスタマイズする方法を確認する必要がありますか。 その場合は、[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)に関するチュートリアルを参照してください。

[編集、並べ替え、およびページングのために GridView サポートを有効にする ![](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**図 6**: 編集、並べ替え、ページングのために GridView のサポートを有効にする ([クリックしてフルサイズのイメージを表示する](caching-data-with-the-objectdatasource-vb/_static/image14.png))

これらの GridView を変更した後、GridView および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

図7に示すように、編集可能な GridView には、データベース内の各製品の名前、カテゴリ、および価格が表示されます。 ページの機能をテストして、結果の並べ替え、ページの表示、レコードの編集を行います。

[各製品の名前、カテゴリ、価格が、並べ替え可能で、ページング可能で編集可能な GridView に表示さ ![](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**図 7**: 各製品の名前、カテゴリ、価格は、並べ替え可能で、ページング可能な編集可能な GridView に一覧表示されます ([クリックすると、フルサイズの画像が表示](caching-data-with-the-objectdatasource-vb/_static/image17.png)されます)

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>手順 3: ObjectDataSource がデータを要求していることを調べる

`Products` GridView は、`ProductsDataSource` ObjectDataSource の `Select` メソッドを呼び出すことによって、表示するデータを取得します。 この ObjectDataSource は、ビジネスロジック層 s `ProductsBLL` クラスのインスタンスを作成し、その `GetProducts()` メソッドを呼び出します。このメソッドは、データアクセス層 s `ProductsTableAdapter` s `GetProducts()` メソッドを呼び出します。 DAL メソッドは Northwind データベースに接続し、構成された `SELECT` クエリを発行します。 このデータは DAL に返され、`NorthwindDataTable`でパッケージ化されます。 DataTable オブジェクトが BLL に返され、それが ObjectDataSource に返されます。これにより、GridView にそれが返されます。 次に、GridView は DataTable 内の各 `DataRow` に対して `GridViewRow` オブジェクトを作成します。各 `GridViewRow` は、最終的にクライアントに返され、ビジターのブラウザーに表示される HTML にレンダリングされます。

この一連のイベントは、GridView が基になるデータにバインドする必要があるたびに発生します。 これは、ページが最初にアクセスされたとき、データの1ページから別のページに移動したとき、GridView を並べ替えるとき、または組み込みの編集または削除インターフェイスを使用して GridView のデータを変更したときに発生します。 GridView のビューステートが無効になっている場合は、すべてのポストバックに加えて、GridView も再バインドされます。 GridView は、その `DataBind()` メソッドを呼び出すことによって、そのデータに明示的に再バインドすることもできます。

データベースからデータを取得する頻度を十分に把握するために、データが再取得されるタイミングを示すメッセージを表示します。 `ODSEvents`という名前の GridView の上にラベル Web コントロールを追加します。 `Text` プロパティをクリアし、その `EnableViewState` プロパティを `False`に設定します。 ラベルの下にボタン Web コントロールを追加し、その `Text` プロパティを [ポストバック] に設定します。

[GridView の上のページにラベルとボタンを追加 ![には](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**図 8**: GridView の上のページにラベルとボタンを追加する ([クリックすると、フルサイズの画像が表示](caching-data-with-the-objectdatasource-vb/_static/image20.png)されます)

データアクセスワークフロー中に、ObjectDataSource s `Selecting` イベントは、基になるオブジェクトが作成され、構成されたメソッドが呼び出される前に発生します。 このイベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

ObjectDataSource がデータのアーキテクチャに要求を行うたびに、ラベルには [イベントが発生しました] というテキストが表示されます。

ブラウザーでこのページを参照してください。 ページが最初に表示されたときに、[イベントが発生しました] というテキストが表示されます。 [ポストバック] ボタンをクリックすると、テキストが表示されなくなります (GridView の `EnableViewState` プロパティが `True`、既定値に設定されていることを前提としています)。 これは、ポストバック時に GridView がビューステートから再構築されるため、データの ObjectDataSource には変わりません。 ただし、データの並べ替え、ページング、または編集を行うと、GridView がそのデータソースに再バインドされるため、[イベントが発生しました] というテキストが再び表示されます。

[GridView がそのデータソースに再バインドされるたびに、[イベントが発生しました] を選択すると ![](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**図 9**: GridView がそのデータソースに再バインドしている場合は、[イベントが発生しました] が表示されます ([クリックすると、フルサイズの画像が表示](caching-data-with-the-objectdatasource-vb/_static/image23.png)されます)

[ポストバックボタンをクリック ![と、GridView がビューステートから再構築されます。](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**図 10**: [ポストバック] ボタンをクリックすると、GridView がビューステートから再構築されます ([クリックすると、フルサイズのイメージが表示](caching-data-with-the-objectdatasource-vb/_static/image26.png)されます)

データがページングまたは並べ替えられるたびに、データベースのデータを取得することは無駄に見えるかもしれません。 結局のところ、既定のページングを使用しているため、ObjectDataSource は最初のページを表示するときにすべてのレコードを取得しました。 GridView で並べ替えとページングのサポートが提供されていない場合でも、任意のユーザーがページに最初にアクセスしたとき (ビューステートが無効になっている場合は、すべてのポストバックで)、データベースからデータを取得する必要があります。 ただし、GridView がすべてのユーザーに対して同じデータを表示している場合、これらの追加のデータベース要求は不要です。 `GetProducts()` メソッドから返された結果をキャッシュして、それらのキャッシュされた結果に GridView をバインドしないのはなぜですか。

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>手順 4: ObjectDataSource を使用してデータをキャッシュする

いくつかのプロパティを設定するだけで、取得したデータを ASP.NET データキャッシュに自動的にキャッシュするように ObjectDataSource を構成できます。 次の一覧は、ObjectDataSource のキャッシュ関連のプロパティをまとめたものです。

- キャッシュを有効にするには、 [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx)を `True` に設定する必要があります。 既定値は、 `False`です。
- [Cacheduration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx)データがキャッシュされる時間の長さ (秒単位)。 既定値は 0 です。 ObjectDataSource は、`EnableCaching` が `True`、`CacheDuration` がゼロより大きい値に設定されている場合にのみデータをキャッシュします。
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx)は、`Absolute` または `Sliding`に設定できます。 `Absolute`した場合、ObjectDataSource は取得したデータを `CacheDuration` 秒間キャッシュします。`Sliding`した場合、データは、`CacheDuration` 秒間アクセスされていない場合にのみ有効期限が切れます。 既定値は、 `Absolute`です。
- [Cachekeydependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx)このプロパティを使用して、ObjectDataSource のキャッシュエントリと既存のキャッシュ依存関係を関連付けます。 ObjectDataSource s データエントリは、関連付けられた `CacheKeyDependency`を期限切れにすることで、キャッシュから早期に削除できます。 このプロパティは、SQL キャッシュの依存関係を ObjectDataSource のキャッシュと関連付けるために最も一般的に使用されます。これについては、後で[Sql キャッシュの依存関係](using-sql-cache-dependencies-vb.md)のチュートリアルを使用して説明します。

では、`ProductsDataSource` ObjectDataSource を構成して、データを30秒間、絶対スケールにキャッシュします。 ObjectDataSource s `EnableCaching` プロパティを `True` に設定し、その `CacheDuration` プロパティを30に設定します。 `CacheExpirationPolicy` プロパティは、既定の `Absolute`に設定したままにします。

[データを30秒間キャッシュするように ObjectDataSource を構成 ![には](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**図 11**: データを30秒間キャッシュするように ObjectDataSource を構成する ([クリックすると、フルサイズのイメージが表示](caching-data-with-the-objectdatasource-vb/_static/image29.png)されます)

変更を保存し、ブラウザーでこのページを再閲覧します。 最初にページにアクセスしたときに選択したイベントが表示されます。これは、データがキャッシュ内にないためです。 ただし、ポストバックボタンのクリック、並べ替え、ページング、または [編集] ボタンまたは [キャンセル] ボタンのクリックによってトリガーされる後続のポストバックでは、選択したイベントが発生したテキストは表示*されません* これは、ObjectDataSource が基になるオブジェクトからデータを取得するときにのみ、`Selecting` イベントが発生するためです。データがデータキャッシュからプルされた場合、`Selecting` イベントは発生しません。

30秒後に、データがキャッシュから削除されます。 ObjectDataSource s `Insert`、`Update`、または `Delete` メソッドが呼び出されると、データもキャッシュから削除されます。 その結果、30秒が経過するか、[更新] ボタンがクリックされた後、[編集] または [キャンセル] ボタンをクリックすると、ObjectDataSource によって基になるオブジェクトからデータが取得され、`Selecting` イベントが発生したときに選択したイベントが表示されます。 返された結果は、データキャッシュに戻されます。

> [!NOTE]
> ObjectDataSource がキャッシュされたデータを使用していると予想される場合でも、[イベントが発生したテキストを頻繁に選択する] が表示される場合は、メモリの制約が原因である可能性があります。 空きメモリが不足している場合は、ObjectDataSource によってキャッシュに追加されたデータが清掃されている可能性があります。 ObjectDataSource が正しくデータをキャッシュしていないように見える場合、またはデータを散発的にキャッシュするだけの場合は、一部のアプリケーションを閉じてメモリを解放し、もう一度やり直してください。

図12は、ObjectDataSource s キャッシュワークフローを示しています。 選択したイベントが画面に表示されたときに、データがキャッシュに含まれておらず、基になるオブジェクトから取得する必要があることが原因です。 ただし、このテキストが存在しない場合は、データがキャッシュから利用可能であったことになります。 キャッシュからデータが返されるときに、基になるオブジェクトへの呼び出しはなく、そのため、データベースクエリは実行されません。

![ObjectDataSource は、データキャッシュからデータを格納して取得します。](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**図 12**: ObjectDataSource によってデータキャッシュからデータが格納および取得される

各 ASP.NET アプリケーションには、すべてのページと訪問者で共有される独自のデータキャッシュインスタンスがあります。 つまり、ObjectDataSource によってデータキャッシュに格納されるデータは、そのページにアクセスするすべてのユーザー間でも共有されます。 これを確認するには、ブラウザーで [`ObjectDataSource.aspx`] ページを開きます。 ページに初めてアクセスしたときに、選択したイベントが発生します (以前のテストによってキャッシュに追加されたデータが削除されたことを前提としています)。 2番目のブラウザーインスタンスを開き、最初のブラウザーインスタンスの URL をコピーして、2番目のブラウザーインスタンスに貼り付けます。 2番目のブラウザーインスタンスでは、最初と同じキャッシュデータを使用しているので、選択したイベントが表示されません。

取得したデータをキャッシュに挿入すると、ObjectDataSource では、次のようなキャッシュキー値が使用されます。 `CacheDuration` と `CacheExpirationPolicy` のプロパティ値です。ObjectDataSource によって使用されている、基になるビジネスオブジェクトの型。この型は、 [`TypeName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx)(この例では`ProductsBLL`) を使用して指定されます。`SelectMethod` プロパティの値、および `SelectParameters` コレクション内のパラメーターの名前と値。[カスタムページング](../paging-and-sorting/paging-and-sorting-report-data-vb.md)を実装するときに使用される、`StartRowIndex` プロパティと `MaximumRows` プロパティの値。

これらのプロパティの組み合わせとしてキャッシュキー値を構築すると、これらの値が変更されるときに、一意のキャッシュエントリが確保されます。 たとえば、過去のチュートリアルでは、指定されたカテゴリのすべての製品を返す `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)`の使用について説明しました。 1人のユーザーがページにアクセスして飲料を表示する場合があります。飲み物は `CategoryID` が1です。 `SelectParameters` 値に関係なく、ObjectDataSource によって結果がキャッシュされた場合、飲料製品がキャッシュ内にあるときに condiments を表示するために別のユーザーがページに戻ると、condiments ではなく、キャッシュされた飲料製品が表示されます。 `SelectParameters`の値を含むこれらのプロパティによってキャッシュキーを変更することで、ObjectDataSource は飲み物と condiments 用に個別のキャッシュエントリを保持します。

## <a name="stale-data-concerns"></a>古いデータの問題

`Insert`、`Update`、または `Delete` メソッドのいずれかが呼び出されると、ObjectDataSource はキャッシュから項目を自動的に見つけします。 これにより、ページを介してデータが変更されたときにキャッシュエントリがクリアされるため、古いデータを保護できます。 ただし、キャッシュを使用して古いデータを表示することもできます。 最も単純なケースでは、データがデータベース内で直接変更されていることが原因である可能性があります。 データベース管理者は、データベース内の一部のレコードを変更するスクリプトを実行しただけです。

このシナリオは、より微妙な方法で展開することもできます。 ObjectDataSource は、データ変更メソッドの1つが呼び出されたときにキャッシュからその項目を見つけしますが、削除されるキャッシュ項目は、ObjectDataSource の特定のプロパティ値の組み合わせ (`CacheDuration`、`TypeName`、`SelectMethod`など) を対象としています。 異なる `SelectMethods` または `SelectParameters`を使用する2つの ObjectDataSources ソースがあり、同じデータを更新できる場合は、1つの ObjectDataSource によって行が更新され、それ自体のキャッシュエントリが無効になりますが、2番目の ObjectDataSource の対応する行は、キャッシュされたから引き続き提供されます。 この機能を使用するためのページを作成することをお勧めします。 キャッシュを使用する ObjectDataSource からデータをプルし、`ProductsBLL` クラス s `GetProducts()` メソッドからデータを取得するように構成されている、編集可能な GridView を表示するページを作成します。 別の編集可能な GridView と ObjectDataSource をこのページ (または別のページ) に追加しますが、この2番目の ObjectDataSource では `GetProductsByCategoryID(categoryID)` メソッドを使用します。 2つの ObjectDataSources ソース `SelectMethod` プロパティが異なるため、それぞれに独自のキャッシュ値があります。 1つのグリッドで製品を編集した場合、次に他のグリッドにデータをバインドすると (ページングや並べ替えなどによって)、そのデータはキャッシュされた古いデータに対して機能し、他のグリッドからの変更は反映されません。

つまり、古いデータの可能性がある場合は時間ベースの expiries のみを使用し、データの鮮度が重要なシナリオでは短い expiries を使用します。 古いデータを使用できない場合は、済ませるをキャッシュするか、SQL キャッシュの依存関係を使用します (キャッシュし直すデータベースデータであることを前提としています)。 SQL キャッシュの依存関係については、今後のチュートリアルで説明します。

## <a name="summary"></a>要約

このチュートリアルでは、ObjectDataSource s の組み込みのキャッシュ機能について説明しました。 いくつかのプロパティを設定するだけで、指定された `SelectMethod` から返された結果を ASP.NET データキャッシュにキャッシュするように ObjectDataSource に指示できます。 `CacheDuration` と `CacheExpirationPolicy` のプロパティは、項目がキャッシュされている期間と、その項目が絶対有効期限またはスライド式有効期限であるかどうかを示します。 `CacheKeyDependency` プロパティは、すべての ObjectDataSource キャッシュエントリと既存のキャッシュ依存関係を関連付けます。 これは、時間ベースの有効期限が切れる前にキャッシュから ObjectDataSource s エントリを削除するために使用でき、通常は SQL キャッシュの依存関係で使用されます。

ObjectDataSource は単にその値をデータキャッシュにキャッシュするだけであるため、ObjectDataSource の組み込み機能をプログラムによってレプリケートできます。 ObjectDataSource はこの機能をすぐに使用できるようにするため、プレゼンテーション層では意味がありませんが、アーキテクチャの別のレイヤーにキャッシュ機能を実装することができます。 これを行うには、ObjectDataSource で使用されているのと同じロジックを繰り返す必要があります。 この後のチュートリアルでは、アーキテクチャ内からデータキャッシュをプログラムで操作する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET キャッシュ: 手法とベストプラクティス](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework アプリケーション用のキャッシュアーキテクチャガイド](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2.0 での出力キャッシュ](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](using-sql-cache-dependencies-cs.md)
> [次へ](caching-data-in-the-architecture-vb.md)
