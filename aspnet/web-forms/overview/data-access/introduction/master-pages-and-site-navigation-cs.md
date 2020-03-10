---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: マスターページとサイトナビゲーション (C#) |Microsoft Docs
author: rick-anderson
description: ユーザーフレンドリな web サイトの一般的な特性の1つは、一貫性のあるサイト全体のページレイアウトとナビゲーションスキームを持つことです。 このチュートリアルでは、
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: e1ddd43524a61ff2e012171eba1a8dc8efbf8f1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426304"
---
# <a name="master-pages-and-site-navigation-c"></a>マスター ページとサイト ナビゲーション (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe)または[PDF のダウンロード](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> ユーザーフレンドリな web サイトの一般的な特性の1つは、一貫性のあるサイト全体のページレイアウトとナビゲーションスキームを持つことです。 このチュートリアルでは、簡単に更新できるすべてのページで一貫したルックアンドフィールを作成する方法について説明します。

## <a name="introduction"></a>はじめに

ユーザーフレンドリな web サイトの一般的な特性の1つは、一貫性のあるサイト全体のページレイアウトとナビゲーションスキームを持つことです。 ASP.NET 2.0 には、サイト全体のページレイアウトとナビゲーションスキームの実装を大幅に簡略化する2つの新機能が導入されています。マスターページとサイトナビゲーションです。 マスターページを使用すると、開発者は、指定された編集可能な領域を使用してサイト全体のテンプレートを作成できます。 このテンプレートは、サイト内の ASP.NET ページに適用できます。 このような ASP.NET ページは、マスターページの指定された編集可能な領域に対してのみコンテンツを提供する必要がありますマスターページ内の他のすべてのマークアップは、マスターページを使用するすべての ASP.NET ページで同一です。 このモデルを使用すると、開発者はサイト全体のページレイアウトを定義して一元管理できます。これにより、簡単に更新できるすべてのページに一貫したルックアンドフィールを作成することができます。

[サイトナビゲーションシステム](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)には、ページ開発者がサイトマップを定義するためのメカニズムと、そのサイトマップ用の API をプログラムで照会するためのメカニズムが用意されています。 新しいナビゲーション Web では、メニュー、TreeView、および SiteMapPath を制御して、サイトマップの全体または一部を共通のナビゲーションユーザーインターフェイス要素に簡単にレンダリングできるようにします。 既定のサイトナビゲーションプロバイダーを使用します。つまり、サイトマップは XML 形式のファイルで定義されます。

これらの概念を説明し、チュートリアルの web サイトをより使いやすくするために、このレッスンでは、サイト全体のページレイアウトの定義、サイトマップの実装、およびナビゲーション UI の追加について説明します。 このチュートリアルを終了すると、チュートリアル web ページを構築するための洗練された web サイトの設計が完成します。

[このチュートリアルの最終結果を ![する](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**図 1**: このチュートリアルの最終結果 ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image3.png)されます)

## <a name="step-1-creating-the-master-page"></a>手順 1: マスターページの作成

最初の手順では、サイトのマスターページを作成します。 現在、web サイトは、型指定されたデータセット (`Northwind.xsd`、`App_Code` フォルダー内)、BLL クラス (`ProductsBLL.cs`、`CategoriesBLL.cs`など)、すべて `App_Code` フォルダー内のデータベース、データベース (`NORTHWND.MDF`フォルダー内)、構成ファイル (`App_Data`)、および CSS スタイルシートファイル (`Web.config`) で構成されています。`Styles.css` これらのページとファイルは、最初の2つのチュートリアルの DAL と BLL の使用をデモンストレーションしています。これらの例については、今後のチュートリアルでさらに詳しく説明します。

![プロジェクト内のファイル](master-pages-and-site-navigation-cs/_static/image4.png)

**図 2**: プロジェクト内のファイル

マスターページを作成するには、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 次に、テンプレートの一覧からマスターページの種類を選択し、`Site.master`という名前を入力します。

[新しいマスターページを Web サイトに追加 ![には](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**図 3**: web サイトに新しいマスターページを追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image7.png)されます)

ここでは、マスターページでサイト全体のページレイアウトを定義します。 デザインビューを使用して、必要なレイアウトや Web コントロールを追加したり、手動でソースビューにマークアップを手動で追加したりすることができます。 マスターページでは、外部ファイル `Style.css`で定義されている CSS 設定を使用して、配置とスタイルに[カスケードスタイルシート](http://www.w3schools.com/css/default.asp)を使用します。 次に示すマークアップからはわかりませんが、CSS 規則は、ナビゲーション `<div>`の内容が、左側に表示されるように絶対配置され、200ピクセルの固定幅であるように定義されています。

サイト. master

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

マスターページでは、静的ページレイアウトと、マスターページを使用する ASP.NET ページで編集できる領域の両方が定義されています。 これらのコンテンツ編集可能な領域は、ContentPlaceHolder コントロールによって示されます。これは、コンテンツ `<div>`内で確認できます。 マスターページには1つの ContentPlaceHolder (`MainContent`) がありますが、マスターページには複数の ContentPlaceHolders がある場合があります。

上で入力したマークアップで、デザインビューに切り替えると、マスターページのレイアウトが表示されます。 このマスターページを使用するすべての ASP.NET ページでは、この uniform layout が使用され、`MainContent` 領域のマークアップを指定することができます。

[デザインビューで表示したときにマスターページを ![する](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**図 4**: デザインビューで表示したときのマスターページ ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image10.png)されます)

## <a name="step-2-adding-a-homepage-to-the-website"></a>手順 2: Web サイトへのホームページの追加

マスターページが定義されているので、web サイトの ASP.NET ページを追加する準備ができました。 まず、web サイトのホームページ `Default.aspx`を追加しましょう。 ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 [テンプレート] ボックスの一覧から [Web フォーム] オプションを選択し、ファイルに `Default.aspx`という名前を指定します。 また、[マスターページの選択] チェックボックスをオンにします。

[新しい Web フォームを追加 ![には、[マスターページの選択] チェックボックスをオンにします。](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**図 5**: [マスターページの選択] チェックボックスをオンにして新しい Web フォームを追加[する (クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image13.png)されます)

[OK] ボタンをクリックすると、この新しい ASP.NET ページで使用するマスターページを選択するように求められます。 プロジェクトには複数のマスターページを含めることができますが、1つしかありません。

[この ASP.NET ページで使用するマスターページを選択 ![](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**図 6**: この ASP.NET ページで使用するマスターページを選択します ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image16.png)されます)

マスターページを選択すると、新しい ASP.NET ページには次のマークアップが含まれます。

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

`@Page` ディレクティブには、使用されるマスターページファイルへの参照 (`MasterPageFile="~/Site.master"`) があります。また、ASP.NET ページのマークアップには、マスターページで定義されている各 ContentPlaceHolder コントロールのコンテンツコントロールが含まれています。また、コントロールの `ContentPlaceHolderID` によって、コンテンツコントロールが特定の ContentPlaceHolder にマッピングされます。 コンテンツコントロールは、対応する ContentPlaceHolder に表示するマークアップを配置する場所です。 `@Page` ディレクティブの `Title` 属性を Home に設定し、いくつかのウェルカムコンテンツをコンテンツコントロールに追加します。

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

`@Page` ディレクティブの `Title` 属性を使用すると、マスターページで `<title>` 要素が定義されている場合でも、ASP.NET ページからページのタイトルを設定できます。 `Page.Title`を使用して、プログラムでタイトルを設定することもできます。 また、マスターページのスタイルシート (`Style.css`など) への参照が自動的に更新され、ASP.NET ページがマスターページを基準とするディレクトリに関係なく、ASP.NET ページで動作するようになっていることに注意してください。

デザインビューに切り替えると、ブラウザーでページがどのように表示されるかを確認できます。 ASP.NET ページのデザインビューでは、編集可能なコンテンツのみが編集可能な領域であることに注意してください。マスターページで定義されている非 ContentPlaceHolder マークアップはグレーで表示されます。

[ASP.NET ページのデザインビューには、編集可能な領域と編集不可能な領域の両方が表示され ![](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**図 7**: [ASP.NET] ページのデザインビューには、編集可能な領域と編集できない領域の両方が表示されます ([クリックすると、フルサイズのイメージが表示](master-pages-and-site-navigation-cs/_static/image19.png)されます)

ブラウザーが `Default.aspx` ページにアクセスすると、ASP.NET エンジンはページのマスターページの内容と ASP を自動的にマージします。ネットワークのコンテンツ。マージされたコンテンツを、要求側のブラウザーに送信される最終的な HTML にレンダリングします。 マスターページのコンテンツが更新されると、このマスターページを使用するすべての ASP.NET ページのコンテンツは、次回要求されたときに新しいマスターページコンテンツに再マージされます。 つまり、マスターページモデルでは、1つのページレイアウトテンプレート (マスターページ) を定義し、その変更内容をサイト全体に直ちに反映させることができます。

## <a name="adding-additional-aspnet-pages-to-the-website"></a>Web サイトへの ASP.NET ページの追加

ここでは、さまざまなレポートのデモを最終的に保持する ASP.NET page スタブをサイトに追加します。 合計で35のデモが行われるため、すべてのスタブページを作成するのではなく、最初の数を作成するだけです。 デモには多くのカテゴリがあるため、デモをより適切に管理するには、カテゴリのフォルダーを追加します。 ここでは、次の3つのフォルダーを追加します。

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

最後に、図8のソリューションエクスプローラーに示すように、新しいファイルを追加します。 各ファイルを追加するときは、必ず [マスターページの選択] チェックボックスをオンにしてください。

![次のファイルを追加します。](master-pages-and-site-navigation-cs/_static/image20.png)

**図 8**: 次のファイルを追加する

## <a name="step-2-creating-a-site-map"></a>手順 2: サイトマップの作成

いくつかのページで構成される web サイトを管理する際の課題の1つは、サイト間を移動するための簡単な方法を提供することです。 まず、サイトのナビゲーション構造を定義する必要があります。 次に、この構造体を、メニューや階層リンクなどのナビゲート可能なユーザーインターフェイス要素に変換する必要があります。 最後に、新しいページがサイトに追加され、既存のページが削除されたときに、このプロセス全体を維持し、更新する必要があります。 ASP.NET 2.0 より前の開発者は、サイトのナビゲーション構造を作成し、それを維持し、移動可能なユーザーインターフェイス要素に変換するための独自の作業を行っていました。 ただし、ASP.NET 2.0 では、開発者は非常に柔軟な組み込みサイトナビゲーションシステムを利用できます。

ASP.NET 2.0 サイトナビゲーションシステムは、開発者がサイトマップを定義し、プログラムによる API を使用してこの情報にアクセスするための手段を提供します。 ASP.NET には、サイトマップデータが特定の方法でフォーマットされた XML ファイルに格納されることを想定したサイトマッププロバイダーが付属しています。 ただし、サイトナビゲーションシステムは[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)に基づいて構築されているため、サイトマップ情報をシリアル化する別の方法をサポートするように拡張することができます。 Jeff Prosise の記事では、サイトマップを SQL Server データベースに格納するサイトマッププロバイダーを作成する方法に[ついて説明してい](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)ます。別の方法として[、ファイルシステムの構造に基づいてサイトマッププロバイダーを](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)作成することもできます。

ただし、このチュートリアルでは、ASP.NET 2.0 に付属している既定のサイトマッププロバイダーを使用します。 サイトマップを作成するには、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] をクリックして、[サイトマップ] オプションを選択します。 名前を `Web.sitemap` のままにして、[追加] ボタンをクリックします。

[プロジェクトにサイトマップを追加 ![には](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**図 9**: サイトマップをプロジェクトに追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image23.png)される)

サイトマップファイルは XML ファイルです。 Visual Studio では、サイトマップ構造に IntelliSense が用意されていることに注意してください。 サイトマップファイルには、`<siteMap>` ノードがルートノードとして含まれている必要があります。このノードには、正確に1つの `<siteMapNode>` 子要素を含める必要があります。 最初の `<siteMapNode>` 要素には、任意の数の子孫 `<siteMapNode>` 要素を含めることができます。

ファイルシステムの構造を模倣するようにサイトマップを定義します。 つまり、次のように、3つの各フォルダーの `<siteMapNode>` 要素と、それらのフォルダー内の各 ASP.NET ページの子 `<siteMapNode>` 要素を追加します。

Web.sitemap

[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

サイトマップでは、web サイトのナビゲーション構造を定義します。これは、サイトのさまざまなセクションを説明する階層です。 `Web.sitemap` 内の各 `<siteMapNode>` 要素は、サイトのナビゲーション構造のセクションを表します。

[サイトマップが階層ナビゲーション構造を表す ![](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**図 10**: サイトマップが階層ナビゲーション構造を表す ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image26.png)されます)

ASP.NET は、.NET Framework の[SiteMap クラス](https://msdn.microsoft.com/library/system.web.sitemap.aspx)を介して、サイトマップの構造を公開します。 このクラスには、ユーザーが現在アクセスしているセクションに関する情報を返す `CurrentNode` プロパティがあります。`RootNode` プロパティは、サイトマップのルート (microsoft のサイトマップ内) を返します。 `CurrentNode` と `RootNode` の両方のプロパティは、サイトマップ階層をウォークできるようにする、`ParentNode`、`ChildNodes`、`NextSibling`、`PreviousSibling`などのプロパティを持つ[SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)インスタンスを返します。

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>手順 3: サイトマップに基づいてメニューを表示する

ASP.NET 2.0 のデータへのアクセスは、ASP.NET 1.x などのプログラムによって、または新しい[データソースコントロール](https://msdn.microsoft.com/library/ms227679.aspx)を介して宣言によって行うことができます。 データソースコントロールには、リレーショナルデータベースデータへのアクセス、ObjectDataSource コントロール、クラスからのデータアクセス用など、いくつかの組み込みデータソースコントロールがあります。 独自の[カスタムデータソースコントロール](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)を作成することもできます。

データソースコントロールは、ASP.NET ページと基になるデータの間のプロキシとして機能します。 データソースコントロールが取得したデータを表示するには、通常、別の Web コントロールをページに追加し、それをデータソースコントロールにバインドします。 Web コントロールをデータソースコントロールにバインドするには、単に Web コントロールの `DataSourceID` プロパティをデータソースコントロールの `ID` プロパティの値に設定します。

サイトマップのデータの操作を支援するために、ASP.NET には SiteMapDataSource コントロールが含まれています。これにより、Web コントロールを Web サイトのサイトマップにバインドすることができます。 2つの Web コントロール TreeView と Menu は、一般的にナビゲーションユーザーインターフェイスを提供するために使用されます。 この2つのコントロールのいずれかにサイトマップデータをバインドするには、SiteMapDataSource プロパティがそれに応じて設定されている TreeView または Menu `DataSourceID` コントロールと共にをページに追加するだけです。 たとえば、次のマークアップを使用して、マスターページにメニューコントロールを追加できます。

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

出力される HTML をより細かく制御するには、次のように、SiteMapDataSource コントロールを Repeater コントロールにバインドします。

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

SiteMapDataSource コントロールは、一度に1レベルずつサイトマップ階層を返します。これは、ルートサイトマップノード (サイトマップのホーム)、次のレベル (基本的なレポート、フィルター処理、カスタマイズされた書式設定など) から始まります。 SiteMapDataSource をリピータにバインドする場合は、返された最初のレベルを列挙し、その1番目のレベルの各 `SiteMapNode` インスタンスの `ItemTemplate` をインスタンス化します。 `SiteMapNode`の特定のプロパティにアクセスするには、`Eval(propertyName)`を使用できます。これは、各 `SiteMapNode`の `Url` とハイパーリンクコントロールの `Title` プロパティを取得する方法です。

上記のリピータの例では、次のマークアップが表示されます。

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

これらのサイトマップノード (基本的なレポート、フィルター処理、およびカスタマイズされた書式設定) は、最初のレベルではなく、表示されるサイトマップの*2 番目*のレベルを構成します。 これは、SiteMapDataSource の `ShowStartingNode` プロパティが False に設定され、SiteMapDataSource がルートサイトマップノードをバイパスし、代わりに、サイトマップ階層の2番目のレベルを返すことによって開始されるためです。

基本的なレポート作成、レポートのフィルター処理、カスタマイズされた書式設定 `SiteMapNode` の子を表示するには、最初のリピータの `ItemTemplate`に別のリピータを追加します。 この2番目のリピータは、次のように `SiteMapNode` インスタンスの `ChildNodes` プロパティにバインドされます。

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

これらの2つのリピータは、次のマークアップを生成します (簡略化のため、一部のマークアップは削除されています)。

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

[Rachel Andrew](http://www.rachelandrew.co.uk/)の書籍から選択された css スタイルを使用して[、css anthology 書籍: 101 重要なヒント、秘訣、&amp; ハッキング](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance)、`<ul>` 要素と `<li>` 要素には、マークアップによって次のビジュアル出力が生成されるようにスタイルが指定されています。

![2つのリピータといくつかの CSS から構成されるメニュー](master-pages-and-site-navigation-cs/_static/image27.png)

**図 11**: 2 つのリピータといくつかの CSS から構成されるメニュー

このメニューは、マスターページにあり、`Web.sitemap`で定義されているサイトマップにバインドされています。つまり、サイトマップに対する変更は、`Site.master` マスターページを使用するすべてのページに直ちに反映されます。

## <a name="disabling-viewstate"></a>ViewState の無効化

すべての ASP.NET コントロールは、必要に応じて状態を[ビューステート](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)に永続化することができます。これは、レンダリングされた HTML の非表示フォームフィールドとしてシリアル化されます。 ビューステートは、データ Web コントロールにバインドされたデータなど、ポストバック間でプログラムによって変更された状態を記憶するために、コントロールによって使用されます。 ビューステートでは、ポストバック間で情報を記憶することが許可されますが、クライアントに送信する必要があるマークアップのサイズが増加し、厳密に監視されていない場合は、ページのサイズが極端に大きくなる可能性があります。 データ Web コントロール (特に、GridView) は、ページに多数の追加のマークアップを追加する場合に特によく知られています。 このような増加は、ブロードバンドまたはイントラネットのユーザーにとってはごくわずかである場合がありますが、ダイヤルアップユーザーのためにラウンドトリップに数秒を追加することができます。

ビューステートの影響を確認するには、ブラウザーのページにアクセスし、web ページによって送信されたソースを表示します (Internet Explorer で、[表示] メニューに移動し、[ソース] オプションを選択します)。 ページ[トレース](https://msdn.microsoft.com/library/sfbfw58f.aspx)をオンにして、ページ上の各コントロールによって使用されるビューステートの割り当てを確認することもできます。 ビューステート情報は `__VIEWSTATE`という名前の非表示フィールドにシリアル化されます。このフィールドは、開始 `<form>` タグの直後にある `<div>` 要素にあります。 ビューステートは、使用されている Web フォームがある場合にのみ保存されます。ASP.NET ページの宣言構文に `<form runat="server">` が含まれていない場合は、表示されているマークアップに `__VIEWSTATE` の非表示フォームフィールドはありません。

マスターページによって生成される `__VIEWSTATE` フォームフィールドは、ページの生成されたマークアップに約1800バイトを追加します。 SiteMapDataSource コントロールの内容がビューステートに保持されるため、この余分な膨張は、主に Repeater コントロールによって発生します。 余分な1800バイトは、多くのフィールドとレコードを含む GridView を使用する場合に、多くのフィールドとレコードを含む GridView を使用すると、swell が10以上の割合で簡単に表示されない可能性があります。

`EnableViewState` プロパティを `false`に設定すると、ビューステートをページレベルまたはコントロールレベルで無効にして、表示されるマークアップのサイズを小さくすることができます。 データ web コントロールのビューステートは、ポストバック間でデータ Web コントロールにバインドされたデータを保持するため、データ Web コントロールのビューステートを無効にするときは、データを各ポストバックごとにバインドする必要があります。 ASP.NET バージョン1.x では、この責任はページ開発者のショルダーにあります。ただし、ASP.NET 2.0 では、必要に応じて、データ Web コントロールが各ポストバックのデータソースコントロールに再バインドされます。

ページのビューステートを小さくするには、Repeater コントロールの `EnableViewState` プロパティを `false`に設定します。 これは、デザイナーのプロパティウィンドウを使用するか、ソースビューで宣言によって行うことができます。 この変更を行った後、リピータの宣言型マークアップは次のようになります。

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

この変更が完了すると、ページのレンダリングされたビューステートのサイズが52バイトに縮小し、ビューステートサイズが97% 節約されます。 このシリーズのチュートリアルでは、表示されるマークアップのサイズを小さくするために、既定でデータ Web コントロールのビューステートを無効にします。 例の大部分では、`EnableViewState` プロパティは `false` に設定され、言及せずに完了します。 データ Web コントロールが期待される機能を提供するために、ビューステートが有効になっている必要があるシナリオでは、表示状態のみを説明します。

## <a name="step-4-adding-breadcrumb-navigation"></a>手順 4: 階層リンクナビゲーションを追加する

マスターページを完成させるには、各ページに階層リンクナビゲーション UI 要素を追加してみましょう。 階層リンクは、サイト階層内の現在の位置をユーザーにすばやく表示します。 ASP.NET 2.0 で階層リンクを追加するのは、ページに SiteMapPath コントロールを追加するだけです。コードは必要ありません。

サイトでは、次のコントロールをヘッダー `<div>`に追加します。

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

階層リンクには、ユーザーがサイトマップ階層内でアクセスしている現在のページと、そのサイトマップノードの "先祖" が表示されます。これは、ルート (サイトマップ内のホーム) までです。

![階層リンクには、現在のページとその先祖がサイトマップ階層に表示されます。](master-pages-and-site-navigation-cs/_static/image28.png)

**図 12**: 階層リンクに、現在のページとその先祖がサイトマップ階層に表示される

## <a name="step-5-adding-the-default-page-for-each-section"></a>手順 5: 各セクションの既定のページを追加する

このサイトのチュートリアルは、各カテゴリのフォルダーと、そのフォルダー内の ASP.NET ページとしての対応するチュートリアルによって、さまざまなカテゴリに分類されています。 また、各フォルダーには `Default.aspx` ページが含まれています。 この既定のページでは、現在のセクションのすべてのチュートリアルを表示してみましょう。 つまり、`BasicReporting` フォルダーの `Default.aspx` には、`SimpleDisplay.aspx`、`DeclarativeParams.aspx`、`ProgrammaticParams.aspx`へのリンクがあります。 ここでも、`SiteMap` クラスとデータ Web コントロールを使用して、`Web.sitemap`で定義されているサイトマップに基づいてこの情報を表示できます。

リピータを使用して順序なしのリストをもう一度表示してみましょう。今度は、チュートリアルのタイトルと説明を表示します。 これを実現するためのマークアップとコードは `Default.aspx` ページごとに繰り返す必要があるため、[ユーザーコントロール](https://msdn.microsoft.com/library/y6wb1a0e.aspx)にこの UI ロジックをカプセル化することができます。 Web サイトに `UserControls` という名前のフォルダーを作成し、`SectionLevelTutorialListing.ascx`という種類の Web ユーザーコントロールの新しい項目を追加して、次のマークアップを追加します。

[UserControls フォルダーに新しい Web ユーザーコントロールを追加 ![には](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**図 13**: `UserControls` フォルダーに新しい Web ユーザーコントロールを追加する ([クリックしてフルサイズのイメージを表示する](master-pages-and-site-navigation-cs/_static/image31.png))

SectionLevelTutorialListing.ascx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs

[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

前のリピータの例では、`SiteMap` データを、宣言によってリピータにバインドしました。ただし、`SectionLevelTutorialListing` ユーザーコントロールはプログラムによって行われます。 `Page_Load` イベントハンドラーでは、このページの URL がサイトマップ内のノードにマップされていることを確認するためのチェックが行われます。 このユーザーコントロールが、対応する `<siteMapNode>` エントリのないページで使用されている場合、`SiteMap.CurrentNode` は `null` を返し、データはリピータにバインドされません。 `CurrentNode`があると仮定した場合、その `ChildNodes` コレクションをリピータにバインドします。 各セクションの [`Default.aspx`] ページがそのセクション内のすべてのチュートリアルの親ノードになるようにサイトマップが設定されているため、次のスクリーンショットに示すように、このコードには、すべてのセクションのチュートリアルのリンクと説明が表示されます。

このリピータが作成されたら、各フォルダーの `Default.aspx` ページを開き、デザインビューに移動します。次に、ソリューションエクスプローラーから、チュートリアルリストを表示するデザイン画面にユーザーコントロールをドラッグします。

[ユーザーコントロールが default.aspx に追加され ![](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**図 14**: ユーザーコントロールが `Default.aspx` に追加されました ([クリックしてフルサイズの画像を表示](master-pages-and-site-navigation-cs/_static/image34.png))

[基本的なレポートのチュートリアルが記載されて ![](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**図 15**: 基本的なレポートのチュートリアルが一覧表示されます ([クリックすると、フルサイズの画像が表示](master-pages-and-site-navigation-cs/_static/image37.png)されます)

## <a name="summary"></a>まとめ

サイトマップが定義され、マスターページが完成したので、データ関連のチュートリアルのページレイアウトとナビゲーションスキームが一貫しています。 サイトに追加するページの数に関係なく、サイト全体のページレイアウトまたはサイトナビゲーション情報の更新は、この情報が集中管理されているため、短時間で簡単なプロセスです。 具体的には、ページレイアウト情報は `Site.master` マスターページと `Web.sitemap`のサイトマップで定義されています。 このサイト全体のページレイアウトとナビゲーション機構を実現するため*にコードを*記述する必要はありませんでした。 Visual Studio では完全な WYSIWYG デザイナーサポートを維持しています。

データアクセス層とビジネスロジック層を完成させ、一貫性のあるページレイアウトとサイトナビゲーションを定義したら、一般的なレポートパターンの調査を開始できます。 [次](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)の3つのチュートリアルでは、GridView、DetailsView、および FormView コントロールの BLL から取得したデータを表示する基本的なレポートタスクについて説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET マスターページの概要](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2.0 のマスターページ](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 のデザインテンプレート](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET サイトナビゲーションの概要](https://msdn.microsoft.com/library/e468hxky.aspx)
- [ASP.NET 2.0 のサイトナビゲーションを調べる](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 サイトナビゲーション機能](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [ASP.NET ビューステートについて](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [方法: ASP.NET ページのトレースを有効にする](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET ユーザーコントロール](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Liz Shulok、Patterson が、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](creating-a-business-logic-layer-cs.md)
> [次へ](creating-a-data-access-layer-vb.md)
