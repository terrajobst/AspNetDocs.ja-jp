---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: カスタムデータベース駆動型サイトマッププロバイダーを構築する (VB) |Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 の既定のサイトマッププロバイダーは、静的な XML ファイルからそのデータを取得します。 XML ベースのプロバイダーは、多くの小規模および中程度の siz に適しています。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 78051696bd75e1d574f55b1c5d5891fe67c3030d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481612"
---
# <a name="building-a-custom-database-driven-site-map-provider-vb"></a>カスタム データベース駆動型サイト マップ プロバイダーを構築する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip)または[PDF のダウンロード](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2.0 の既定のサイトマッププロバイダーは、静的な XML ファイルからそのデータを取得します。 XML ベースのプロバイダーは、多くの小規模および中規模の Web サイトに適していますが、大規模な Web アプリケーションには、より動的なサイトマップが必要です。 このチュートリアルでは、ビジネスロジック層からデータを取得し、さらにデータベースからデータを取得するカスタムサイトマッププロバイダーを構築します。

## <a name="introduction"></a>はじめに

ASP.NET 2.0 s サイトマップ機能を使用すると、ページ開発者は、XML ファイルなどの一部の永続メディアで web アプリケーション s サイトマップを定義できます。 定義が完了すると、 [`System.Web` 名前空間](https://msdn.microsoft.com/library/system.web.aspx)の[`SiteMap` クラス](https://msdn.microsoft.com/library/system.web.sitemap.aspx)、または SiteMapPath、Menu、TreeView コントロールなどのさまざまなナビゲーション Web コントロールを使用して、プログラムによってサイトマップデータにアクセスできます。 サイトマップシステムでは[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)を使用して、さまざまなサイトマップのシリアル化の実装を作成し、web アプリケーションに接続することができます。 ASP.NET 2.0 に付属する既定のサイトマッププロバイダーは、サイトマップ構造を XML ファイルに保持します。 [マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)チュートリアルに戻り、この構造を含む `Web.sitemap` という名前のファイルを作成し、新しいチュートリアルセクションごとにその XML を更新しました。

既定の XML ベースのサイトマッププロバイダーは、サイトマップの構造が非常に静的な場合 (これらのチュートリアルの場合など) に適しています。 ただし、多くのシナリオでは、より動的なサイトマップが必要です。 図1に示すサイトマップを考えてみます。ここで、各カテゴリと製品は、web サイトの構造のセクションとして表示されます。 このサイトマップでは、ルートノードに対応する web ページにアクセスすると、すべてのカテゴリが一覧表示されます。特定のカテゴリの web ページにアクセスすると、カテゴリの製品が一覧表示され、特定の製品の web ページを表示すると、その製品の詳細が表示されます。

[カテゴリと製品の ![サイトマップの構造を構成する](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**図 1**: カテゴリと製品は、サイトマップの構造を構成します ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png)されます)

このカテゴリと製品ベースの構造は `Web.sitemap` ファイルにハードコーディングされている可能性がありますが、カテゴリまたは製品が追加、削除、または名前変更されるたびに、ファイルを更新する必要があります。 そのため、データベースから構造を取得した場合や、理想的にはアプリケーションのアーキテクチャのビジネスロジック層からサイトマップのメンテナンスが大幅に簡素化されます。 これにより、製品とカテゴリが追加、名前変更、または削除されたときに、これらの変更を反映するためにサイトマップが自動的に更新されます。

ASP.NET 2.0 s サイトマップのシリアル化はプロバイダーモデルの上に構築されているため、データベースやアーキテクチャなどの代替データストアからデータを取得する独自のカスタムサイトマッププロバイダーを作成できます。 このチュートリアルでは、BLL からデータを取得するカスタムプロバイダーを作成します。 始めましょう!

> [!NOTE]
> このチュートリアルで作成したカスタムサイトマッププロバイダーは、アプリケーションのアーキテクチャとデータモデルに密結合されています。 [SQL Server にサイトマップを格納](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)する Jeff Prosise と、記事[を待機している SQL サイトマッププロバイダーが](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)、SQL Server にサイトマップデータを格納するための一般化されたアプローチを検討しています。

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>手順 1: カスタムサイトマッププロバイダー Web ページの作成

カスタムサイトマッププロバイダーの作成を開始する前に、まず、このチュートリアルで必要な ASP.NET ページを追加してみましょう。 まず、`SiteMapProvider`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

また、`App_Code` フォルダーに `CustomProviders` サブフォルダーを追加します。

![サイトマッププロバイダー関連のチュートリアルの ASP.NET ページを追加する](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**図 2**: サイトマッププロバイダー関連のチュートリアルの ASP.NET ページを追加する

このセクションにはチュートリアルが1つしかないため、セクションのチュートリアルの一覧を表示する `Default.aspx` は必要ありません。 代わりに、`Default.aspx` によって GridView コントロールにカテゴリが表示されます。 これについては、手順 2. で説明します。

次に、`Web.sitemap` を更新して、`Default.aspx` ページへの参照を含めます。 具体的には、キャッシュ `<siteMapNode>`の後に、次のマークアップを追加します。

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、唯一のサイトマッププロバイダーのチュートリアルの項目が含まれるようになりました。

![サイトマップに、サイトマッププロバイダーのチュートリアルのエントリが含まれるようになりました。](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**図 3**: サイトマップにサイトマッププロバイダーのチュートリアルのエントリが含まれるようになりました。

このチュートリアルの主な目的は、カスタムのサイトマッププロバイダーを作成し、そのプロバイダーを使用するように web アプリケーションを構成することです。 特に、図1に示すように、各カテゴリと製品のノードと共にルートノードを含むサイトマップを返すプロバイダーを作成します。 一般に、サイトマップ内の各ノードは URL を指定できます。 サイトマップの場合、ルートノードの URL は `~/SiteMapProvider/Default.aspx`になります。これにより、データベース内のすべてのカテゴリが一覧表示されます。 サイトマップ内の各カテゴリノードには、`~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`を指す URL があります。これにより、指定された*categoryID*内のすべての製品が一覧表示されます。 最後に、各製品サイトマップノードが `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`をポイントし、特定の製品の詳細が表示されます。

開始するには、`Default.aspx`、`ProductsByCategory.aspx`、および `ProductDetails.aspx` の各ページを作成する必要があります。 これらのページは、それぞれ手順2、3、および4で完了します。 このチュートリアルの推力はサイトマッププロバイダーに関するものであり、過去のチュートリアルではこれらの種類の複数ページのマスター/詳細レポートの作成について説明しているため、手順 2. ~ 4. を実行します。 複数のページにまたがるマスター/詳細レポートの作成に関するリフレッシャーが必要な場合は、「 [2 ページのマスター/詳細のフィルター処理](../masterdetail/master-detail-filtering-across-two-pages-vb.md)」チュートリアルを参照してください。

## <a name="step-2-displaying-a-list-of-categories"></a>手順 2: カテゴリの一覧を表示する

`SiteMapProvider` フォルダーの [`Default.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグし、`ID` を [`Categories`] に設定します。 GridView s スマートタグから、`CategoriesDataSource` という名前の新しい ObjectDataSource にバインドし、`CategoriesBLL` クラス s `GetCategories` メソッドを使用してデータを取得するように構成します。 この GridView はカテゴリを表示するだけで、データ変更機能を提供しないため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[GetCategories メソッドを使用してカテゴリを返すように ObjectDataSource を構成 ![には](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**図 4**: `GetCategories` メソッドを使用してカテゴリを返すように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png))

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**図 5**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png))

データソースの構成ウィザードを完了すると、Visual Studio によって `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`、および `BrochurePath`の BoundField が追加されます。 GridView を編集して、`CategoryName` および `Description` BoundFields のみが含まれるようにし、`CategoryName` BoundField s `HeaderText` プロパティを Category に更新します。

次に、ハイパーリンクフィールドを追加して、一番左のフィールドになるように配置します。 `DataNavigateUrlFields` プロパティを `CategoryID` に設定し、`DataNavigateUrlFormatString` プロパティを `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`に設定します。 製品を表示するには、`Text` プロパティを設定します。

![カテゴリ GridView にハイパーリンクフィールドを追加する](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**図 6**: `Categories` GridView にハイパーリンクフィールドを追加する

ObjectDataSource を作成し、GridView のフィールドをカスタマイズした後、2つのコントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

図7は、ブラウザーを使用して表示する場合の `Default.aspx` を示しています。 Category s View Products リンクをクリックすると、手順3で作成する `ProductsByCategory.aspx?CategoryID=categoryID`に移動します。

[各カテゴリが ![ビュー製品のリンクと共に一覧表示されます。](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**図 7**: 各カテゴリは、[製品の表示] リンクと共に表示されます ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png)されます)

## <a name="step-3-listing-the-selected-category-s-products"></a>手順 3: 選択したカテゴリの製品を一覧表示する

[`ProductsByCategory.aspx`] ページを開き、GridView を追加して `ProductsByCategory`名前を付けます。 そのスマートタグから、GridView を `ProductsByCategoryDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを使用するように ObjectDataSource を構成し、[更新]、[挿入]、[削除] の各タブで、ドロップダウンリストを [(なし)] に設定します。

[製品の Bll クラス s Get$ Bycategoryid (categoryID) メソッドを使用 ![](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**図 8**: `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを使用する ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png))

データソースの構成ウィザードの最後の手順では、 *categoryID*のパラメーターソースを入力するように求められます。 この情報は、クエリ文字列フィールド `CategoryID`経由で渡されるため、図9に示すように、ドロップダウンリストから QueryString を選択し、QueryStringField テキストボックスに「CategoryID」と入力します。 [完了] をクリックしてウィザードを終了します。

[categoryID パラメーターに CategoryID フィールドを使用 ![](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**図 9**: *categoryID*パラメーターに `CategoryID` Querystring フィールドを使用する ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png)されます)

ウィザードを完了すると、Visual Studio によって、対応する BoundFields と CheckBoxField が製品データフィールドの GridView に追加されます。 `ProductName`、`UnitPrice`、および `SupplierName` BoundFields 以外はすべて削除します。 これら3つの連結されたフィールド `HeaderText` プロパティをカスタマイズして、それぞれ製品、価格、および供給業者を読み取ります。 `UnitPrice` BoundField を通貨として書式設定します。

次に、ハイパーリンクフィールドを追加し、左端の位置に移動します。 `Text` プロパティを [詳細を表示]、[`DataNavigateUrlFields`] プロパティを `ProductID`に、`DataNavigateUrlFormatString` プロパティを `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`に設定します。

![ProductDetails を指す [ビューの詳細ハイパーリンク] フィールドを追加します。](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**図 10**: `ProductDetails.aspx` を指し示すビューの詳細ハイパーリンクフィールドを追加する

これらのカスタマイズを行った後、GridView および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

ブラウザーを使用した `Default.aspx` の表示に戻り、飲み物の [Products] \ (製品の表示 \) リンクをクリックします。 これにより、飲料カテゴリに属する Northwind データベース内の製品の名前、価格、および仕入先が `ProductsByCategory.aspx?CategoryID=1`表示されます (図11を参照)。 このページをさらに拡張して、カテゴリリストページ (`Default.aspx`) にユーザーを返すリンクや、選択したカテゴリの名前と説明を表示する DetailsView または FormView コントロールを追加することもできます。

[飲み物の名前、価格、および仕入先が表示され ![](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**図 11**: 飲み物の名前、価格、および仕入先が表示される ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png)されます)

## <a name="step-4-showing-a-product-s-details"></a>手順 4: 製品の詳細を表示する

最後のページ `ProductDetails.aspx`には、選択した製品の詳細が表示されます。 `ProductDetails.aspx` を開き、[ツールボックス] から [DetailsView] をデザイナーにドラッグします。 [DetailsView s `ID`] プロパティを `ProductInfo` に設定し、`Height` と `Width` プロパティの値をクリアします。 スマートタグから、DetailsView を `ProductDataSource`という名前の新しい ObjectDataSource にバインドし、ObjectDataSource を構成して `ProductsBLL` クラス s `GetProductByProductID(productID)` メソッドからデータをプルします。 手順 2. と 3. で作成した前の web ページと同様に、[更新]、[挿入]、および [削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[GetProductByProductID (productID) メソッドを使用するように ObjectDataSource を構成 ![には](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**図 12**: `GetProductByProductID(productID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))

データソースの構成ウィザードの最後の手順では、 *productID*パラメーターのソースが要求されます。 このデータにはクエリ文字列フィールド `ProductID`が含まれているため、ドロップダウンリストを QueryString に設定し、QueryStringField テキストボックスを ProductID に設定します。 最後に、[完了] をクリックしてウィザードを完了します。

[productid パラメーターを構成して、ProductID パラメーターフィールドから値を取得 ![](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**図 13**: *productID*パラメーターを `ProductID` Querystring フィールドから値をプルするように構成する ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))

データソースの構成ウィザードを完了すると、Visual Studio によって、対応する BoundFields と CheckBoxField が製品データフィールドの DetailsView に作成されます。 `ProductID`、`SupplierID`、および `CategoryID` BoundFields を削除し、必要に応じて残りのフィールドを構成します。 いくつかの美しい構成を行った後、その DetailsView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

このページをテストするには、`Default.aspx` に戻り、[飲料] カテゴリの [製品の表示] をクリックします。 飲み物製品の一覧から、Chai 紅茶の [Details] \ (詳細の表示 \) リンクをクリックします。 これにより、`ProductDetails.aspx?ProductID=1`に移動します。これには、Chai 茶の詳細が表示されます (図14を参照)。

[![Chai 茶 s 仕入先、カテゴリ、価格などの情報が表示されます](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**図 14**: Chai ティー s の仕入先、カテゴリ、価格、およびその他の情報が表示されます ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png)されます)

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>手順 5: サイトマッププロバイダーの内部動作を理解する

サイトマップは、web サーバーのメモリ内で、階層を形成する `SiteMapNode` インスタンスのコレクションとして表されます。 ルートは1つだけである必要があります。ルート以外のすべてのノードには1つの親ノードが必要であり、すべてのノードが任意の数の子を持つことができます。 各 `SiteMapNode` オブジェクトは、web サイトの構造内のセクションを表します。これらのセクションには、通常、対応する web ページがあります。 その結果、 [`SiteMapNode` クラス](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)には `Title`、`Url`、および `Description`のようなプロパティがあり、`SiteMapNode` が表すセクションの情報を提供します。 また、階層内の各 `SiteMapNode` を一意に識別する `Key` プロパティと、この階層 `ChildNodes`、`ParentNode`、`NextSibling`、`PreviousSibling`などを確立するために使用されるプロパティもあります。

図15は、図1の一般的なサイトマップ構造を示していますが、実装の詳細については詳細に説明しています。

[各 SiteMapNode には、Title、Url、Key などのプロパティがあります。 ![](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**図 15**: 各 `SiteMapNode` には `Title`、`Url`、`Key`などのプロパティがあります ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif)されます)。

サイトマップには、 [`System.Web` 名前空間](https://msdn.microsoft.com/library/system.web.aspx)の[`SiteMap` クラス](https://msdn.microsoft.com/library/system.web.sitemap.aspx)を使用してアクセスできます。 このクラスの `RootNode` プロパティは、サイトマップのルート `SiteMapNode` インスタンスを返します。`CurrentNode` は、現在要求されているページの URL と一致する `Url` プロパティを持つ `SiteMapNode` を返します。 このクラスは、ASP.NET 2.0 s ナビゲーション Web コントロールによって内部的に使用されます。

`SiteMap` クラスのプロパティにアクセスするときは、サイトマップ構造を永続メディアからメモリにシリアル化する必要があります。 ただし、サイトマップのシリアル化ロジックは `SiteMap` クラスにハードコーディングされません。 代わりに、実行時に、`SiteMap` クラスによって、シリアル化に使用するサイトマップ*プロバイダー*が決定されます。 既定では、 [`XmlSiteMapProvider` クラス](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)が使用されます。これにより、適切に書式設定された XML ファイルからサイトマップの構造が読み取られます。 ただし、少しの作業で、独自のカスタムサイトマッププロバイダーを作成できます。

すべてのサイトマッププロバイダーは、 [`SiteMapProvider` クラス](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)から派生する必要があります。このクラスには、サイトマッププロバイダーに必要な必須のメソッドとプロパティが含まれていますが、実装の詳細の多くは省略されています。 2つ目のクラス[`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)は、`SiteMapProvider` クラスを拡張し、必要な機能をより堅牢に実装しています。 内部的には、`StaticSiteMapProvider` はサイトマップの `SiteMapNode` インスタンスを `Hashtable` に格納し、`RemoveNode(siteMapNode),` を内部 `Clear()` に追加および削除する `AddNode(child, parent)`、`SiteMapNode`、`Hashtable`などのメソッドを提供します。 `XmlSiteMapProvider` は、`StaticSiteMapProvider` から派生しています。

`StaticSiteMapProvider`を拡張するカスタムのサイトマッププロバイダーを作成する場合は、 [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx)と[`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)の2つの抽象メソッドをオーバーライドする必要があります。 `BuildSiteMap`は、その名前が示すとおり、は、永続ストレージからサイトマップ構造を読み込み、メモリに構築する役割を担います。 `GetRootNodeCore` は、サイトマップ内のルートノードを返します。

Web アプリケーションでサイトマッププロバイダーを使用する前に、アプリケーションの構成に登録する必要があります。 既定では、`XmlSiteMapProvider` クラスは `AspNetXmlSiteMapProvider`名前を使用して登録されます。 追加のサイトマッププロバイダーを登録するには、`Web.config`に次のマークアップを追加します。

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*名前*の値は、ユーザーが判読できる名前をプロバイダーに割り当てますが、*型*はサイトマッププロバイダーの完全修飾型名を指定します。 ここでは、カスタムのサイトマッププロバイダーを作成した後、手順 7. で*名前*と*型*の値の具体的な値について説明します。

サイトマッププロバイダークラスは、`SiteMap` クラスから初めてアクセスしたときにインスタンス化され、web アプリケーションの有効期間中はメモリに残ります。 サイトマッププロバイダーのインスタンスは、同時に複数の web サイトの訪問者から呼び出される可能性があるため、プロバイダーのメソッドが*スレッドセーフ*であることが不可欠です。

パフォーマンスとスケーラビリティ上の理由から、`BuildSiteMap` メソッドが呼び出されるたびに再作成するのではなく、メモリ内のサイトマップ構造をキャッシュし、このキャッシュされた構造体を返すことが重要です。 ページで使用されているナビゲーションコントロールとサイトマップ構造の深さによっては、`BuildSiteMap` が1ページあたりの要求ごとに複数回呼び出されることがあります。 どのような場合でも、サイトマップ構造を `BuildSiteMap` にキャッシュしない場合は、起動するたびに、アーキテクチャから製品とカテゴリの情報を再取得する必要があります (これにより、データベースに対するクエリが実行されます)。 前のキャッシュのチュートリアルで説明したように、キャッシュされたデータは古くなる可能性があります。 これに対処するには、時間または SQL キャッシュの依存関係ベースの expiries を使用できます。

> [!NOTE]
> サイトマッププロバイダーは、必要に応じて[`Initialize` メソッド](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)をオーバーライドできます。 `Initialize` は、サイトマッププロバイダーが最初にインスタンス化され、次のように `<add>` 要素の `Web.config` でプロバイダーに割り当てられたカスタム属性が渡されたときに呼び出されます。 `<add name="name" type="type" customAttribute="value" />`です。 これは、ページ開発者がプロバイダーのコードを変更しなくても、さまざまなサイトマッププロバイダーに関連する設定を指定できるようにする場合に便利です。 たとえば、アーキテクチャではなくデータベースからカテゴリと製品データを直接読み取る場合、プロバイダーのコードでハードコーディングされた値を使用するのではなく、`Web.config` でデータベース接続文字列を指定することができます。 手順6でビルドするカスタムサイトマッププロバイダーは、この `Initialize` メソッドをオーバーライドしません。 `Initialize` メソッドの使用例については、SQL Server の記事に記載されている[Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) [のサイトマップの格納](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)に関するページを参照してください。

## <a name="step-6-creating-the-custom-site-map-provider"></a>手順 6: カスタムサイトマッププロバイダーを作成する

Northwind データベースのカテゴリと製品からサイトマップを構築するカスタムサイトマッププロバイダーを作成するには、`StaticSiteMapProvider`を拡張するクラスを作成する必要があります。 手順 1. では、`App_Code` フォルダーに `CustomProviders` フォルダーを追加するように求められました。 `NorthwindSiteMapProvider`という名前の新しいクラスをこのフォルダーに追加します。 以下のコードを `NorthwindSiteMapProvider` クラスに追加します。

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

まず、このクラス `BuildSiteMap` メソッドを調べてみましょう。このメソッドは、 [`lock` ステートメント](https://msdn.microsoft.com/library/c5kehkcz.aspx)から始まります。 `lock` ステートメントでは、一度に1つのスレッドだけを入力できます。これにより、そのコードへのアクセスがシリアル化され、2つの同時実行スレッドが1つの生まれたをステップ実行できなくなります。

クラスレベル `SiteMapNode` 変数 `root` は、サイトマップ構造をキャッシュするために使用されます。 サイトマップを初めて作成する場合、または基になるデータが変更された後に初めて構成する場合は、`root` が `Nothing` され、サイトマップ構造が構築されます。 このメソッドが次回呼び出されるときに、`root` が `Nothing`されないように、構築プロセス中に、サイトマップのルートノードが `root` に割り当てられます。 そのため、`root` が `Nothing` ない限り、サイトマップ構造は、再作成することなく、呼び出し元に返されます。

ルートが `Nothing`場合は、製品とカテゴリの情報からサイトマップ構造が作成されます。 サイトマップを作成するには、`SiteMapNode` インスタンスを作成し、`StaticSiteMapProvider` クラス s `AddNode` メソッドの呼び出しを使用して階層を形成します。 `AddNode` によって内部のブックキーピングが実行され、`Hashtable`に複数の `SiteMapNode` インスタンスが格納されます。 階層の構築を始める前に、まず、`Clear` メソッドを呼び出します。これにより、内部 `Hashtable`から要素が消去されます。 次に、`ProductsBLL` クラス s `GetProducts` メソッドと、結果として得られる `ProductsDataTable` がローカル変数に格納されます。

サイトマップの構築は、ルートノードを作成し、それを `root`に割り当てることから始まります。 ここで使用する[`SiteMapNode` s コンストラクター](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx)とこの `BuildSiteMap` 全体のオーバーロードには、次の情報が渡されます。

- サイトマッププロバイダー (`Me`) への参照。
- `SiteMapNode` s `Key`。 この必須値は、`SiteMapNode`ごとに一意である必要があります。
- `SiteMapNode` s `Url`。 `Url` は省略可能ですが、指定する場合、`SiteMapNode` s `Url` 値はそれぞれ一意である必要があります。
- `SiteMapNode` s `Title`。これは必須です。

`AddNode(root)` メソッド呼び出しは、ルートとしてサイトマップに `SiteMapNode` `root` を追加します。 次に、`ProductsDataTable` 内の各 `ProductRow` が列挙されます。 現在の product s カテゴリの `SiteMapNode` が既に存在する場合は、そのカテゴリが参照されます。 それ以外の場合は、`AddNode(categoryNode, root)` メソッド呼び出しによって、カテゴリの新しい `SiteMapNode` が作成され、`SiteMapNode``root` の子として追加されます。 適切なカテゴリ `SiteMapNode` ノードが見つかったか作成されると、現在の製品に対して `SiteMapNode` が作成され、`AddNode(productNode, categoryNode)`経由で `SiteMapNode` カテゴリの子として追加されます。 Product `SiteMapNode` s `Url` プロパティに `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`が割り当てられている間、category `SiteMapNode` `Url` プロパティ値は `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID` ます。

> [!NOTE]
> `CategoryID` に対してデータベース `NULL` 値を持つ製品は、`Title` プロパティが None に設定され、`Url` プロパティが空の文字列に設定されているカテゴリ `SiteMapNode` の下にグループ化されます。 `Url` を空の文字列に設定することにしました。これは、`ProductBLL` クラス s `GetProductsByCategory(categoryID)` メソッドには、現在 `NULL` `CategoryID` 値を持つ製品だけを返す機能がないためです。 また、ナビゲーションコントロールが、`Url` プロパティの値が不足している `SiteMapNode` をどのように表示するかを説明します。 このチュートリアルを拡張して、None `SiteMapNode` s `Url` プロパティが `ProductsByCategory.aspx`を指すようにすることをお勧めしますが、`NULL` `CategoryID` 値を持つ製品のみが表示されるようにしています。

サイトマップを構築した後、任意のオブジェクトが、`AggregateCacheDependency` オブジェクトを介して `Categories` テーブルと `Products` テーブルに対する SQL キャッシュの依存関係を使用して、データキャッシュに追加されます。 *Sql キャッシュ*の依存関係を使用して、前のチュートリアルで sql キャッシュの依存関係を使用する方法について説明します。 ただし、カスタムのサイトマッププロバイダーでは、データキャッシュ s `Insert` メソッドのオーバーロードを使用します。 このオーバーロードは、最後の入力パラメーターとしてを受け入れます。このデリゲートは、オブジェクトがキャッシュから削除されたときに呼び出されます。 具体的には、`NorthwindSiteMapProvider` クラスで定義されている `OnSiteMapChanged` メソッドを指す新しい[`CacheItemRemovedCallback` デリゲート](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx)を渡します。

> [!NOTE]
> サイトマップのメモリ内表現は、クラスレベルの変数 `root`によってキャッシュされます。 カスタムサイトマッププロバイダークラスのインスタンスは1つだけであり、そのインスタンスは web アプリケーションのすべてのスレッド間で共有されるため、このクラス変数はキャッシュとして機能します。 `BuildSiteMap` メソッドはデータキャッシュも使用しますが、`Categories` または `Products` テーブル内の基になるデータベースデータが変更されたときに通知を受信する手段としてのみ使用します。 データキャッシュに格納される値は、現在の日付と時刻のみであることに注意してください。 実際のサイトマップデータはデータキャッシュに格納され*ません*。

`BuildSiteMap` メソッドは、サイトマップのルートノードを返すことによって完了します。

残りのメソッドは非常に簡単です。 `GetRootNodeCore` は、ルートノードを返します。 `BuildSiteMap` はルートを返すため、`GetRootNodeCore` は単に `BuildSiteMap` s 戻り値を返します。 `OnSiteMapChanged` メソッドは、キャッシュ項目が削除されたときに `root` を `Nothing` に戻します。 ルートを `Nothing`に設定し直すと、次に `BuildSiteMap` が呼び出されたときに、サイトマップ構造が再構築されます。 最後に、このような値が存在する場合、`CachedDate` プロパティは、データキャッシュに格納されている日付と時刻の値を返します。 このプロパティは、サイトマップデータが最後にキャッシュされた日時を確認するために、ページ開発者が使用できます。

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>手順 7:`NorthwindSiteMapProvider` を登録する

手順6で作成した `NorthwindSiteMapProvider` サイトマッププロバイダーを web アプリケーションで使用するには、`Web.config`の `<siteMap>` セクションに登録する必要があります。 具体的には、`Web.config`の `<system.web>` 要素内に次のマークアップを追加します。

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

このマークアップは2つの処理を行います。まず、組み込みの `AspNetXmlSiteMapProvider` が既定のサイトマッププロバイダーであることを示します。次に、手順 6. で作成したカスタムサイトマッププロバイダーを、Northwind という名前で登録します。

> [!NOTE]
> アプリケーションの `App_Code` フォルダーに配置されているサイトマッププロバイダーの場合、`type` 属性の値は単にクラス名になります。 または、カスタムのサイトマッププロバイダーが、web アプリケーション s の `/Bin` ディレクトリに配置されたコンパイル済みアセンブリと共に、別のクラスライブラリプロジェクトに作成されている場合もあります。 この場合、`type` 属性値は*名前空間*になります。*ClassName*、 *AssemblyName* 。

`Web.config`を更新した後、ブラウザーでチュートリアルのページを表示してみてください。 左側のナビゲーションインターフェイスには、`Web.sitemap`で定義されているセクションとチュートリアルがまだ表示されていることに注意してください。 これは、`AspNetXmlSiteMapProvider` が既定のプロバイダーとして残されているためです。 `NorthwindSiteMapProvider`を使用するナビゲーションユーザーインターフェイス要素を作成するには、Northwind サイトマッププロバイダーを使用する必要があることを明示的に指定する必要があります。 手順8でこれを実現する方法について説明します。

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>手順 8: カスタムサイトマッププロバイダーを使用してサイトマップ情報を表示する

`Web.config`にカスタムサイトマッププロバイダーを作成して登録すると、`SiteMapProvider` フォルダー内の `Default.aspx`、`ProductsByCategory.aspx`、および `ProductDetails.aspx` の各ページにナビゲーションコントロールを追加できるようになります。 まず、[`Default.aspx`] ページを開いて、[ツールボックス] からデザイナーに `SiteMapPath` をドラッグします。 SiteMapPath コントロールは、ツールボックスのナビゲーションセクションにあります。

[SiteMapPath を default.aspx に追加 ![には](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**図 16**: `Default.aspx` に SiteMapPath を追加する ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif)される)

SiteMapPath コントロールは、サイトマップ内の現在のページの場所を示す階層リンクを表示します。 マスターページ*とサイトナビゲーション*のチュートリアルで、マスターページの一番上に SiteMapPath を追加しました。

ブラウザーを使用してこのページを表示します。 図16で追加した SiteMapPath は、既定のサイトマッププロバイダーを使用して、`Web.sitemap`からデータをプルします。 そのため、階層リンクは、右上隅の階層リンクと同じように、サイトマップをカスタマイズするホーム &gt; を表示します。

[階層リンクが既定のサイトマッププロバイダーを使用する ![](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**図 17**: 階層リンクで既定のサイトマッププロバイダーが使用される ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif)されます)

図16で SiteMapPath を追加するには、手順6で作成したカスタムサイトマッププロバイダーを使用し、その[`SiteMapProvider` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx)を Northwind に設定します。この名前は `Web.config`で `NorthwindSiteMapProvider` に割り当てられています。 残念ながら、デザイナーは引き続き既定のサイトマッププロバイダーを使用しますが、このプロパティを変更した後でブラウザーを使用してページにアクセスすると、階層リンクでカスタムサイトマッププロバイダーが使用されていることがわかります。

[![階層リンクがカスタムサイトマッププロバイダー NorthwindSiteMapProvider を使用するようになりました。](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**図 18**: 階層リンクがカスタムサイトマッププロバイダー `NorthwindSiteMapProvider` を使用するようになりました ([クリックしてフルサイズのイメージを表示](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))

SiteMapPath コントロールは、`ProductsByCategory.aspx` ページと `ProductDetails.aspx` ページにより機能の高いユーザーインターフェイスを表示します。 これらのページに SiteMapPath を追加し、両方の `SiteMapProvider` プロパティを Northwind に設定します。 [飲料] の [Products の表示] リンクを `Default.aspx` クリックし、[Chai 茶] の [詳細の表示] リンクをクリックします。 図19に示すように、階層リンクには、現在のサイトマップセクション (Chai 紅茶) とその先祖 (飲み物およびすべてのカテゴリ) が含まれます。

[![階層リンクがカスタムサイトマッププロバイダー NorthwindSiteMapProvider を使用するようになりました。](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**図 19**: 階層リンクがカスタムサイトマッププロバイダー `NorthwindSiteMapProvider` を使用するようになりました ([クリックしてフルサイズのイメージを表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))

他のナビゲーションユーザーインターフェイス要素は、メニューや TreeView コントロールなど、SiteMapPath に加えて使用できます。 このチュートリアルのダウンロードの `Default.aspx`、`ProductsByCategory.aspx`、および `ProductDetails.aspx` ページ (たとえば、すべてのメニューコントロールが含まれます (図20を参照)。 ASP.NET 2.0 のナビゲーションコントロールとサイトマップシステムの詳細については、 [ASP.NET 2.0 クイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/)の「 [ASP.NET 2.0 s サイトナビゲーション機能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)とサイト[ナビゲーションコントロールの使用](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx)」を参照してください。

[メニューコントロールの ![カテゴリと製品の一覧を表示する](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**図 20**: メニューコントロールにカテゴリと製品の一覧が表示される ([クリックすると、フルサイズの画像が表示](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif)されます)

このチュートリアルで既に説明したように、サイトマップ構造には、`SiteMap` クラスを使用してプログラムからアクセスできます。 次のコードは、既定のプロバイダーのルート `SiteMapNode` を返します。

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

`AspNetXmlSiteMapProvider` はアプリケーションの既定のプロバイダーであるため、上記のコードは `Web.sitemap`で定義されているルートノードを返します。 既定以外のサイトマッププロバイダーを参照するには、次のように `SiteMap` クラス s [`Providers` プロパティ](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx)を使用します。

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

ここで、 *name*はカスタムサイトマッププロバイダー (web アプリケーションの場合は Northwind) の名前です。

サイトマッププロバイダーに固有のメンバーにアクセスするには、`SiteMap.Providers["name"]` を使用してプロバイダーインスタンスを取得し、それを適切な型にキャストします。 たとえば、ASP.NET ページで `NorthwindSiteMapProvider` s `CachedDate` プロパティを表示するには、次のコードを使用します。

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> SQL キャッシュ依存関係機能を必ずテストしてください。 `Default.aspx`、`ProductsByCategory.aspx`、および `ProductDetails.aspx` ページにアクセスした後、[編集]、[挿入]、[削除] セクションのいずれかのチュートリアルにアクセスし、カテゴリまたは製品の名前を編集します。 次に、`SiteMapProvider` フォルダー内のいずれかのページに戻ります。 基になるデータベースへの変更を記録するためにポーリングメカニズムに十分な時間が経過していると仮定した場合、新しい製品名またはカテゴリ名を表示するようにサイトマップを更新する必要があります。

## <a name="summary"></a>まとめ

ASP.NET 2.0 s サイトマップ機能には、`SiteMap` クラス、多数の組み込みナビゲーション Web コントロール、および XML ファイルに保存されているサイトマップ情報を期待する既定のサイトマッププロバイダーが含まれています。 データベース、アプリケーションのアーキテクチャ、リモート Web サービスなど、他のソースからのサイトマップ情報を使用するには、カスタムのサイトマッププロバイダーを作成する必要があります。 これには、`SiteMapProvider` クラスから直接的または間接的に派生するクラスを作成する必要があります。

このチュートリアルでは、製品のサイトマップとアプリケーションアーキテクチャからカリングされるカテゴリ情報を基にした、カスタムのサイトマッププロバイダーを作成する方法を説明しました。 プロバイダーは `StaticSiteMapProvider` クラスと低下を拡張し、データを取得し、サイトマップ階層を構築し、結果の構造をクラスレベルの変数にキャッシュする `BuildSiteMap` メソッドを作成しました。 基になる `Categories` または `Products` データが変更されたときに、キャッシュされた構造体を無効にするために、コールバック関数と共に SQL キャッシュの依存関係を使用しました。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- SQL Server と、[待機していた SQL サイトマッププロバイダー](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) [にサイトマップを格納](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)しています
- [ASP.NET 2.0 s プロバイダーモデルの概要](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [プロバイダーツールキット](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [ASP.NET 2.0 s サイトナビゲーション機能の確認](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Dave Gardner、Zack Jones、Teresa Murphy、Bernadette Leigh でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](building-a-custom-database-driven-site-map-provider-cs.md)
