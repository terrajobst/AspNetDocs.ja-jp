---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: 2つのページにわたるマスター/C#詳細のフィルター処理 () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各 supplier 行には、ビューが含まれています...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: ccb3bfa5f215ba6e65b8a10b40041d5c2896c7e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620412"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>2 つのページでマスター/詳細をフィルター処理する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe)または[PDF のダウンロード](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各仕入先の行には、[製品の表示] リンクが含まれています。このリンクをクリックすると、選択した業者の製品が一覧表示された別のページに移動します。

## <a name="introduction"></a>はじめに

前の2つのチュートリアルでは、DropDownLists を使用して "マスター" レコードを表示する[1 つの web ページでマスター/詳細レポート](master-detail-filtering-with-a-dropdownlist-cs.md)を表示する方法、および "詳細" を表示するための[GridView または DetailsView コントロール](master-detail-filtering-with-two-dropdownlists-cs.md)について説明しました。 マスター/詳細レポートに使用されるもう1つの一般的なパターンは、1つの web ページにマスターレコードを作成し、その詳細を別の web ページに表示することです。 フォーラムの web サイト ( [ASP.NET フォーラム](https://forums.asp.net/)など) は、このパターンを実践するための好例です。 ASP.NET フォーラムは、さまざまなフォーラムはじめに、Web フォーム、データ表示コントロールなどで構成されています。 各フォーラムは多くのスレッドで構成されており、各スレッドは多数の投稿で構成されています。 ASP.NET フォーラムのホームページに、フォーラムが表示されます。 フォーラムをクリックすると、そのフォーラムのスレッドが一覧表示される `ShowForum.aspx` ページに whisks ます。 同様に、スレッドをクリックすると `ShowPost.aspx`に移動し、クリックされたスレッドの投稿が表示されます。

このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各仕入先の行には、[製品の表示] リンクが含まれています。このリンクをクリックすると、選択した業者の製品が一覧表示された別のページに移動します。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>手順 1:`SupplierListMaster.aspx`ページと`ProductsForSupplierDetails.aspx`ページを`Filtering`フォルダーに追加する

3番目のチュートリアルでページレイアウトを定義すると、`BasicReporting`、`Filtering`、および `CustomFormatting` フォルダーに多数の "starter" ページが追加されました。 ただし、その時点でこのチュートリアルのスタートページを追加していません。そのため、`SupplierListMaster.aspx` と `ProductsForSupplierDetails.aspx`の2つの新しいページを `Filtering` フォルダーに追加してみましょう。 `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` には、選択した業者の製品が表示されますが、"マスター" レコード (業者) が一覧表示されます。

これら2つの新しいページを作成する場合は、`Site.master` マスターページに関連付ける必要があります。

![SupplierListMaster および ProductsForSupplierDetails ページをフィルター処理フォルダーに追加します。](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**図 1**: `SupplierListMaster.aspx` ページと `ProductsForSupplierDetails.aspx` ページを `Filtering` フォルダーに追加する

また、新しいページをプロジェクトに追加するときは、必ずサイトマップファイルを更新してください (`Web.sitemap`)。 このチュートリアルでは、次の XML コンテンツをフィルター処理する `<siteMapNode>` 要素の子として使用して、`SupplierListMaster.aspx` ページをサイトマップに追加するだけです。

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> K を使用して新しい ASP.NET ページを追加するときに、サイトマップファイルの更新プロセスを自動化でき[ます。 Scott Allen](http://odetocode.com/Blogs/scott/)の無料の Visual Studio[サイトマップマクロ](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)です。

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>手順 2:`SupplierListMaster.aspx` での業者の一覧の表示

`SupplierListMaster.aspx` と `ProductsForSupplierDetails.aspx` のページが作成されたので、次の手順は `SupplierListMaster.aspx`でサプライヤーの GridView を作成することです。 GridView をページに追加し、新しい ObjectDataSource にバインドします。 この ObjectDataSource では、`SuppliersBLL` クラスの `GetSuppliers()` メソッドを使用して、すべての業者を返す必要があります。

[SuppliersBLL クラスを選択 ![には](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**図 2**: `SuppliersBLL` クラスを選択[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image4.png)されます)

[GetSuppliers () メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**図 3**: `GetSuppliers()` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image7.png))

クリックすると、ユーザーが選択した行の `SupplierID` 値をクエリ文字列を使用して渡す `ProductsForSupplierDetails.aspx` するために、各 GridView 行に「Products」というタイトルのリンクを含める必要があります。 たとえば、ユーザーが東京 Traders 業者の [Products の表示] リンクをクリックした場合 (`SupplierID` 値は 4)、`ProductsForSupplierDetails.aspx?SupplierID=4`に送信する必要があります。

これを行うには、GridView に hyperlink[フィールド](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx)を追加します。これにより、各 gridview 行にハイパーリンクが追加されます。 まず、GridView のスマートタグから [列の編集] リンクをクリックします。 次に、左上の一覧から [ハイパーリンク] フィールドを選択し、[追加] をクリックして、GridView のフィールドリストにハイパーリンクフィールドを含めます。

[GridView にハイパーリンクフィールドを追加 ![には](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**図 4**: GridView にハイパーリンクフィールドを追加する ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-cs/_static/image10.png)されます)

ハイパーリンクフィールドは、各 GridView 行のリンクに同じテキストまたは URL 値を使用するように構成できます。また、各行にバインドされたデータ値に基づいてこれらの値を指定することもできます。 すべての行に対して静的な値を指定するには、ハイパーリンクフィールドの `Text` または `NavigateUrl` プロパティを使用します。 すべての行でリンクテキストを同じにするため、ハイパーリンクフィールドの `Text` プロパティを設定して、製品を表示します。

[ハイパーリンクフィールドの Text プロパティを設定して製品を表示 ![には](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**図 5**: ハイパーリンクフィールドの `Text` プロパティを設定して製品を表示する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image13.png)されます)

GridView 行にバインドされている基になるデータに基づいてテキストまたは URL の値を設定するには、`DataTextField` または `DataNavigateUrlFields` のプロパティで、テキストまたは URL の値を取得するデータフィールドを指定します。 `DataTextField` は、1つのデータフィールドにのみ設定できます。ただし `DataNavigateUrlFields`は、データフィールドのコンマ区切りの一覧に設定できます。 多くの場合、現在の行のデータフィールド値といくつかの静的マークアップの組み合わせに基づいて、テキストまたは URL を指定する必要があります。 このチュートリアルでは、たとえば、ハイパーリンクフィールドのリンクの URL を `ProductsForSupplierDetails.aspx?SupplierID=supplierID`にする必要があります。 *`supplierID`* は各 GridView の行の `SupplierID` 値です。 ここでは、静的な値とデータドリブン値の両方が必要であることに注意してください。リンクの URL の `ProductsForSupplierDetails.aspx?SupplierID=` 部分は静的であるのに対し、 *`supplierID`* 部分はそれぞれの行独自の `SupplierID` 値であるため、データドリブンです。

静的な値とデータドリブン値の組み合わせを示すには、`DataTextFormatString` プロパティと `DataNavigateUrlFormatString` プロパティを使用します。 これらのプロパティでは、必要に応じて静的なマークアップを入力し、[`DataTextField`] または [`DataNavigateUrlFields`] プロパティで指定したフィールドの値を表示するマーカー `{0}` を使用します。 `DataNavigateUrlFields` プロパティに複数のフィールドが指定されている場合は、最初のフィールド値を挿入する場所に `{0}` を使用し、2番目のフィールド値を `{1}` します。

このチュートリアルにこれを適用するには、`DataNavigateUrlFields` プロパティを `SupplierID`に設定する必要があります。これは、行ごとにカスタマイズする必要がある値を持つデータフィールドと、`ProductsForSupplierDetails.aspx?SupplierID={0}`する `DataNavigateUrlFormatString` プロパティであるためです。

[[ハイパーリンク] フィールドを構成して、仕入先に基づく適切なリンク URL を含める ![](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**図 6**: `SupplierID` に基づく適切なリンク URL を含めるようにハイパーリンクフィールドを構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image16.png))

ハイパーリンクフィールドを追加した後は、GridView のフィールドのカスタマイズと順序変更を自由に行うことができます。 次のマークアップは、いくつかの細かいフィールドレベルのカスタマイズを行った後の GridView を示しています。

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

ブラウザーで `SupplierListMaster.aspx` ページを表示してみましょう。 図7に示すように、現在のページには、[製品の表示] リンクを含むすべての仕入先が表示されています。 [製品の表示] リンクをクリックすると、`ProductsForSupplierDetails.aspx`に移動し、クエリ文字列で業者の `SupplierID` を渡します。

[各 Supplier 行に ![ビュー製品のリンクが含まれています](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**図 7**: 各仕入先の行に [製品の表示] リンクが含まれている ([クリックしてフルサイズの画像を表示する](master-detail-filtering-across-two-pages-cs/_static/image19.png))

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>手順 3:`ProductsForSupplierDetails.aspx` で仕入先の製品を一覧表示する

この時点で、`SupplierListMaster.aspx` ページが `ProductsForSupplierDetails.aspx`にユーザーを送信し、選択した業者の `SupplierID` を querystring に渡します。 チュートリアルの最後の手順は、クエリ文字列を使用して渡された `SupplierID` と等しい `SupplierID` を持つ `ProductsForSupplierDetails.aspx` の GridView に製品を表示することです。 これを行うには、GridView を `ProductsForSupplierDetails.aspx` ページに追加します。そのためには、`ProductsBLL` クラスから `GetProductsBySupplierID(supplierID)` メソッドを呼び出す `ProductsBySupplierDataSource` という名前の新しい ObjectDataSource コントロールを使用します。

[ProductsBySupplierDataSource という名前の新しい ObjectDataSource を追加 ![には](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**図 8**: `ProductsBySupplierDataSource` という名前の新しい ObjectDataSource を追加[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image22.png)される)

[製品の Bll クラスを選択 ![には](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**図 9**: `ProductsBLL` クラスを選択[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image25.png)されます)

[ObjectDataSource が Get$ By仕入先 (仕入先) メソッドを呼び出す ![](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**図 10**: ObjectDataSource で `GetProductsBySupplierID(supplierID)` メソッドを呼び出す ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image28.png))

データソースの構成ウィザードの最後の手順では、`GetProductsBySupplierID(supplierID)` メソッドの *`supplierID`* パラメーターのソースを指定するように求められます。 Querystring 値を使用するには、パラメーターソースを QueryString に設定し、QueryStringField テキストボックス (`SupplierID`) で使用する querystring 値の名前を入力します。

[仕入先のパラメーター値を仕入先のクエリ文字列の値から設定 ![](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**図 11**: `SupplierID` Querystring 値から *`supplierID`* パラメーター値を設定する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image31.png))

必要な作業は以上です。 図12は、`SupplierListMaster.aspx`から [東京 Traders] リンクをクリックしてアクセスしたときの `ProductsForSupplierDetails.aspx` ページを示しています。

[東京 Traders 社によって提供される製品が ![表示されます。](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**図 12**: 東京 Traders が提供する製品が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image34.png)されます)

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>`ProductsForSupplierDetails.aspx` での仕入先情報の表示

図12に示すように、[`ProductsForSupplierDetails.aspx`] ページには、クエリ文字列に指定された `SupplierID` によって提供される製品の一覧が表示されます。 ただし、このページに直接送信されたユーザーは、図12に東京 Traders 社の製品が表示されていることはわかりません。 この問題を解決するには、このページでサプライヤー情報を表示することもできます。

まず、products GridView の上に FormView を追加します。 `SuppliersBLL` クラスの `GetSupplierBySupplierID(supplierID)` メソッドを呼び出す `SuppliersDataSource` という名前の新しい ObjectDataSource コントロールを作成します。

[SuppliersBLL クラスを選択 ![には](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**図 13**: `SuppliersBLL` クラスを選択[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image37.png)されます)

[![ObjectDataSource Invoke GetSupplierBySupplierID (仕入先) メソッド](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**図 14**: ObjectDataSource で `GetSupplierBySupplierID(supplierID)` メソッドを呼び出す ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image40.png))

`ProductsBySupplierDataSource`と同様に、 *`supplierID`* パラメーターに `SupplierID` querystring 値の値が割り当てられている必要があります。

[仕入先のパラメーター値を仕入先のクエリ文字列の値から設定 ![](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**図 15**: `SupplierID` Querystring 値から *`supplierID`* パラメーター値を設定する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-across-two-pages-cs/_static/image43.png))

デザインビューで FormView を ObjectDataSource にバインドすると、Visual Studio は、ObjectDataSource によって返される各データフィールドに対して、ラベルとテキストボックス Web コントロールを含む FormView の `ItemTemplate`、`InsertItemTemplate`、および `EditItemTemplate` を自動的に作成します。 仕入先情報を表示するだけなので、`InsertItemTemplate` と `EditItemTemplate`を削除してもかまいません。 次に、ItemTemplate を編集して、仕入先の会社名を `<h3>` 要素に、住所、市区町村、国、電話番号を会社名の下に表示するようにします。 または、FormView の `DataSourceID` を手動で設定し、「ObjectDataSource を使用した[データの表示](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)」のチュートリアルで説明したように、`ItemTemplate` マークアップを作成することもできます。

これらの編集の後、FormView の宣言型マークアップは次のようになります。

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

図16は、上記で説明した業者情報が含まれていた後の `ProductsForSupplierDetails.aspx` ページのスクリーンショットを示しています。

[製品の一覧に ![業者に関する概要が記載されています。](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**図 16**: 製品の一覧には、業者に関する概要が含まれています ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image46.png)されます)

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>`ProductsForSupplierDetails.aspx`UI の最後のタッチを適用する

このレポートのユーザーエクスペリエンスを向上させるために、`ProductsForSupplierDetails.aspx` のページに対していくつかの追加機能が用意されています。 現在、ユーザーが `ProductsForSupplierDetails.aspx` ページからサプライヤーの一覧に戻ることができる唯一の方法は、ブラウザーの [戻る] ボタンをクリックすることです。 `SupplierListMaster.aspx`に戻るハイパーリンクコントロールを `ProductsForSupplierDetails.aspx` ページに追加して、ユーザーがマスターリストに戻るための別の方法を提供してみましょう。

[![ハイパーリンクコントロールを追加して、ユーザーを SupplierListMaster に戻します。](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**図 17**: ハイパーリンクコントロールを追加してユーザーを `SupplierListMaster.aspx` に戻す ([クリックしてフルサイズの画像を表示する](master-detail-filtering-across-two-pages-cs/_static/image49.png))

製品が存在しない業者の [製品の表示] リンクをクリックすると、`ProductsForSupplierDetails.aspx` の `ProductsBySupplierDataSource` ObjectDataSource では結果が返されません。 ObjectDataSource にバインドされている GridView では、ユーザーのブラウザーのページに空白の領域が生じるマークアップはレンダリングされません。 選択した業者に関連付けられている製品がないことをユーザーにより明確に伝えるために、GridView の `EmptyDataText` プロパティを、このような状況が発生したときに表示するメッセージに設定できます。 このプロパティを "この供給業者によって提供される製品はありません" に設定しました。

既定では、Northwinds データベースのすべての仕入先は、少なくとも1つの製品を提供します。 ただし、このチュートリアルでは、supplier Escargots Nouveaux が製品に関連付けられないように、`Products` テーブルを手動で変更しました。 図18は、この変更が行われた後の Escargots Nouveaux の詳細ページを示しています。

[![ユーザーには、業者が製品を提供していないことが通知されます。](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**図 18**: 業者が製品を提供していないことがユーザーに通知される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-cs/_static/image52.png)されます)

## <a name="summary"></a>要約

マスター/詳細レポートでは、マスターレコードと詳細レコードの両方を1ページに表示できますが、多くの web サイトでは、2つの web ページに分割されています。 このチュートリアルでは、このようなマスター/詳細レポートを実装する方法について説明しました。これには、"マスター" web ページの GridView にサプライヤーを一覧表示し、[詳細] ページに一覧表示されている関連製品を表示します。 マスター web ページの各 supplier 行には、行の `SupplierID` 値に従って渡された詳細ページへのリンクが含まれていました。 このような行固有のリンクは、GridView の [ハイパーリンク] フィールドを使用して簡単に追加できます。

詳細ページで、`ProductsBLL` クラスの `GetProductsBySupplierID(supplierID)` メソッドを呼び出すことによって、指定された業者のこれらの製品を取得しました。 *`supplierID`* パラメーター値は、querystring をパラメーターソースとして使用して宣言的に指定されました。 また、FormView を使用して詳細ページでサプライヤーの詳細を表示する方法についても説明しました。

[次のチュートリアル](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)では、マスター/詳細レポートについて説明します。 GridView で製品の一覧を表示する方法について説明します。各行には [選択] ボタンがあります。 [選択] ボタンをクリックすると、同じページの DetailsView コントロールにその製品の詳細が表示されます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-filtering-with-two-dropdownlists-cs.md)
> [次へ](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
