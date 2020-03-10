---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: 2つの DropDownLists を使用したマスター/詳細フィルター処理 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、マスター/詳細リレーションシップを展開して3番目のレイヤーを追加し、2つの DropDownList コントロールを使用して目的の親を選択します。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 166d6a7664a326361dc2a3f115eddb988cd39d20
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424294"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>2 つの DropDownList でマスター/詳細をフィルター処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe)または[PDF のダウンロード](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> このチュートリアルでは、マスター/詳細リレーションシップを展開して3番目のレイヤーを追加します。2つの DropDownList コントロールを使用して、目的の親レコードと祖父母レコードを選択します。

## <a name="introduction"></a>はじめに

前の[チュートリアル](master-detail-filtering-with-a-dropdownlist-vb.md)では、カテゴリが設定された1つの DropDownList と、選択したカテゴリに属する製品を示す GridView を使用して、単純なマスター/詳細レポートを表示する方法を説明しました。 このレポートパターンは、一対多のリレーションシップを持つレコードを表示する場合に適しています。また、複数の一対多リレーションシップを含むシナリオで機能するように簡単に拡張できます。 たとえば、注文入力システムには、顧客、注文、および注文品目に対応するテーブルがあります。 特定の顧客には、注文ごとに複数の注文が含まれている場合があります。 このようなデータは、2つの DropDownLists と GridView を使用してユーザーに提示できます。 最初の DropDownList には、データベース内の顧客ごとに、2番目の内容が選択した顧客によって配置された注文であるというリストアイテムがあります。 GridView では、選択した順序で行項目が一覧表示されます。

Northwind データベースには、`Customers`、`Orders`、および `Order Details` の各テーブルに、正規の顧客/注文/注文の詳細情報が含まれていますが、これらのテーブルはアーキテクチャではキャプチャされません。 それでも、2つの依存する DropDownLists を使用して説明することはできます。 最初の DropDownList にカテゴリと、選択したカテゴリに属する2番目の製品が一覧表示されます。 次に、選択した製品の詳細が表示されます。

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>手順 1: カテゴリの作成と設定 DropDownList

最初の目標は、カテゴリを一覧表示する DropDownList を追加することです。 これらの手順の詳細については、前のチュートリアルで詳しく説明しましたが、ここでは完全を期すためにまとめました。

`Filtering` フォルダーの [`MasterDetailsDetails.aspx`] ページを開き、DropDownList をページに追加します。その `ID` プロパティを [`Categories`] に設定し、そのスマートタグの [データソースの構成] リンクをクリックします。 データソース構成ウィザードから、新しいデータソースの追加を選択します。

[DropDownList の新しいデータソースを追加 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**図 1**: DropDownList の新しいデータソースを追加する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png)されます)

新しいデータソースは、当然、ObjectDataSource である必要があります。 この新しい ObjectDataSource `CategoriesDataSource` という名前を指定し、`CategoriesBLL` オブジェクトの `GetCategories()` メソッドを呼び出すようにします。

[カテゴリ Bll クラスの使用を選択 ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**図 2**: `CategoriesBLL` クラスの使用を選択する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png))

[GetCategories () メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**図 3**: `GetCategories()` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png))

ObjectDataSource を構成した後も、`Categories` DropDownList に表示するデータソースフィールドを指定し、リストアイテムの値として構成する必要があるデータソースフィールドを指定する必要があります。 `CategoryName` フィールドを表示として設定し、各リスト項目の値として `CategoryID` します。

[DropDownList で [区分項目] フィールドを表示し、値として CategoryID を使用する ![ます。](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**図 4**: DropDownList に `CategoryName` フィールドが表示され、`CategoryID` を値として使用する ([クリックしてフルサイズの画像を表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png))

この時点で、`Categories` テーブルのレコードが設定された DropDownList コントロール (`Categories`) があります。 ユーザーが DropDownList から新しいカテゴリを選択すると、手順 2. で作成しようとしている製品の DropDownList を更新するためにポストバックが発生します。 そのため、`categories` DropDownList のスマートタグから [AutoPostBack を有効にする] オプションをオンにします。

[カテゴリの DropDownList に対して AutoPostBack を有効に ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**図 5**: `Categories` DropDownList の AutoPostBack を有効[にする (クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>手順 2: 選択したカテゴリの製品を2番目の DropDownList に表示する

`Categories` DropDownList が完了したら、次の手順では、選択したカテゴリに属する製品の DropDownList を表示します。 これを行うには、`ProductsByCategory`という名前のページに別の DropDownList を追加します。 `Categories` DropDownList と同様に、`ProductsByCategoryDataSource`という名前の `ProductsByCategory` DropDownList の新しい ObjectDataSource を作成します。

[製品 Bycategory の DropDownList の新しいデータソースを追加 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**図 6**: `ProductsByCategory` DropDownList の新しいデータソースを追加する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png)されます)

[新しい ObjectDataSource という名前の新しい ![を作成します。](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**図 7**: `ProductsByCategoryDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png)される)

`ProductsByCategory` DropDownList は選択されたカテゴリに属する製品のみを表示する必要があるため、ObjectDataSource は `ProductsBLL` オブジェクトから `GetProductsByCategoryID(categoryID)` メソッドを呼び出します。

[製品の Bll クラスの使用を選択 ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**図 8**: `ProductsBLL` クラスの使用を選択する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png))

[Get$ Bycategoryid (categoryID) メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**図 9**: `GetProductsByCategoryID(categoryID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png))

ウィザードの最後の手順では、 *`categoryID`* パラメーターの値を指定する必要があります。 このパラメーターを `Categories` DropDownList から選択した項目に割り当てます。

[カテゴリの DropDownList から categoryID パラメーター値をプル ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**図 10**: `Categories` DropDownList から *`categoryID`* パラメーターの値を取得[する (クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png))

ObjectDataSource が構成されていれば、DropDownList の項目の表示と値に使用されるデータソースフィールドを指定するだけです。 [`ProductName`] フィールドを表示し、[`ProductID`] フィールドを値として使用します。

[DropDownList の ListItems のテキストと値のプロパティに使用されるデータソースフィールドを指定 ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**図 11**: DropDownList の `ListItem` s ' `Text` と `Value` プロパティに使用されるデータソースフィールドを指定[する (クリックしてフルサイズの画像を表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png))

ObjectDataSource と `ProductsByCategory` DropDownList が構成されている場合、ページには2つの DropDownLists が表示されます。1つ目はすべてのカテゴリを一覧表示し、2番目のリストは選択したカテゴリに属する製品を一覧表示します。 ユーザーが最初の DropDownList から新しいカテゴリを選択すると、ポストバックは議論され、2番目の DropDownList は再バインドされ、新しく選択されたカテゴリに属する製品が表示されます。 図12および13は、ブラウザーで表示したときに `MasterDetailsDetails.aspx` の動作を示しています。

[![最初にページにアクセスしたときに、飲み物のカテゴリが選択されます。](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**図 12**: 最初にページにアクセスしたときに飲み物のカテゴリが選択されている ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png)されます)

[別のカテゴリを選択 ![と、新しいカテゴリの製品が表示されます](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**図 13**: 別のカテゴリを選択すると、新しいカテゴリの製品が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png)されます)

現在 `productsByCategory` DropDownList は、変更された場合、ポストバックを発生*させません*。 ただし、選択した製品の詳細を表示するために DetailsView を追加した後に、ポストバックが発生するようにします (手順 3)。 そのため、`productsByCategory` DropDownList のスマートタグから [AutoPostBack を有効にする] チェックボックスをオンにします。

[製品 Bycategory の DropDownList の AutoPostBack 機能を有効 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**図 14**: `productsByCategory` DropDownList の AutoPostBack 機能を有効にする ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>手順 3: DetailsView を使用して選択した製品の詳細を表示する

最後の手順は、選択した製品の詳細を DetailsView で表示することです。 これを行うには、DetailsView をページに追加し、その `ID` プロパティを `ProductDetails`に設定して、新しい ObjectDataSource を作成します。 この ObjectDataSource を構成して、 *`productID`* パラメーターの値に対して `ProductsByCategory` DropDownList の選択された値を使用して、`ProductsBLL` クラスの `GetProductByProductID(productID)` メソッドからデータをプルします。

[製品の Bll クラスの使用を選択 ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**図 15**: `ProductsBLL` クラスの使用を選択する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png))

[GetProductByProductID (productID) メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**図 16**: `GetProductByProductID(productID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png))

[製品 Bycategory の DropDownList から productID パラメーター値をプル ![には](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**図 17**: `ProductsByCategory` DropDownList から *`productID`* パラメーター値を取得する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png)されます)

`ProductDetails` DetailsView で使用可能なフィールドを表示するように選択できます。 `ProductID`、`SupplierID`、および `CategoryID` フィールドを削除し、残りのフィールドの並べ替えと書式設定を行いました。 さらに、DetailsView の `Height` と `Width` プロパティをクリアし、指定されたサイズに制限されるのではなく、データを最適に表示するために必要な幅まで DetailsView を拡張できるようにしました。 完全なマークアップが以下に表示されます。

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

ブラウザーで `MasterDetailsDetails.aspx` のページを試してみましょう。 一見すると、すべてが必要に応じて動作しているように見えるかもしれませんが、微妙な問題があります。 新しいカテゴリを選択すると `ProductsByCategory` DropDownList は選択されたカテゴリの製品を含むように更新されますが、`ProductDetails` DetailsView は以前の製品情報を表示し続けます。 選択したカテゴリに対して別の製品を選択すると、DetailsView が更新されます。 さらに、十分にテストした場合は、新しいカテゴリ (`Categories` DropDownList からの飲み物の選択、Condiments、Confections など) を選択すると、他のすべてのカテゴリの選択によって `ProductDetails` の DetailsView が更新されることがわかります。

この問題をを具体化ために、特定の例を見てみましょう。 ページに初めてアクセスすると、飲み物カテゴリが選択され、関連する製品が `ProductsByCategory` DropDownList に読み込まれます。 Chai は選択された製品で、図18に示すように、`ProductDetails` の DetailsView にその詳細が表示されます。

[選択した製品の詳細が DetailsView に表示される ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**図 18**: 選択した製品の詳細が DetailsView に表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png)されます)

カテゴリの選択を飲み物から Condiments に変更すると、ポストバックが発生し、それに応じて `ProductsByCategory` DropDownList が更新されますが、DetailsView には、Chai の詳細が表示されます。

[以前に選択した製品の詳細が表示され ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**図 19**: 以前に選択された製品の詳細が表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png)されます)

一覧から新しい製品を選択すると、必要に応じて DetailsView が更新されます。 製品を変更した後で新しいカテゴリを選択しても、DetailsView は再更新されません。 ただし、新しいカテゴリを選択して新しい製品を選択するのではなく、DetailsView が更新されます。 ここでは、世界中で何が起こっているのでしょうか。

問題は、ページのライフサイクルのタイミングの問題です。 ページが要求されるたびに、レンダリングとしていくつかの手順を実行します。 これらの手順のいずれかで、ObjectDataSource コントロールは `SelectParameters` 値が変更されているかどうかを確認します。 その場合、ObjectDataSource にバインドされているデータ Web コントロールは、表示を更新する必要があることを認識しています。 たとえば、新しいカテゴリが選択されている場合、`ProductsByCategoryDataSource` ObjectDataSource はそのパラメーター値が変更されたことを検出し、`ProductsByCategory` DropDownList がそれ自体を再バインドして、選択されたカテゴリの製品を取得します。

この状況で発生する問題は、変更されたパラメーターの ObjectDataSources ソースチェックが、関連付けられたデータ Web コントロールの再バインドの*前に*発生することを示す、ページのライフサイクルのポイントです。 したがって、新しいカテゴリを選択すると `ProductsByCategoryDataSource` ObjectDataSource によって、パラメーターの値の変更が検出されます。 ただし、`ProductDetails` DetailsView で使用される ObjectDataSource は、`ProductsByCategory` DropDownList がまだ再バインドされていないため、このような変更はメモしていません。 その後、ライフサイクルの `ProductsByCategory` DropDownList を ObjectDataSource に再バインドし、新しく選択したカテゴリの製品を取得します。 `ProductsByCategory` DropDownList の値が変更されましたが、`ProductDetails` DetailsView の ObjectDataSource のパラメーター値のチェックが既に完了しています。そのため、DetailsView は前の結果を表示します。 この相互作用は、図20に示されています。

[ProductDetails DetailsView の ObjectDataSource が変更されたかどうかを確認した後に、Productbycategory の DropDownList 値の変更を ![します](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**図 20**: `ProductDetails` DetailsView の ObjectDataSource の ObjectDataSource によって変更がチェックされた後の `ProductsByCategory` DropDownList 値の変更 ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png)されます)

これを解決するには、`ProductsByCategory` DropDownList がバインドされた後に `ProductDetails` DetailsView を明示的に再バインドする必要があります。 これは、`ProductsByCategory` DropDownList の `DataBound` イベントが発生したときに `ProductDetails` DetailsView の `DataBind()` メソッドを呼び出すことによって実現できます。 次のイベントハンドラーコードを `MasterDetailsDetails.aspx` ページの分離コードクラスに追加します (イベントハンドラーを追加する方法の詳細については、「[ObjectDataSource のパラメーター値をプログラムで設定](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)する」を参照してください)。

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

`ProductDetails` DetailsView の `DataBind()` メソッドのこの明示的な呼び出しが追加されると、このチュートリアルは想定どおりに動作します。 図21は、この変更が以前の問題を解決した方法を示しています。

[Productbycategory の DropDownList のデータバインドイベントが発生したときに、ProductDetails の DetailsView が明示的に更新さ ![](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**図 21**: `ProductsByCategory` DropDownList の `DataBound` イベントが発生したときに `ProductDetails` DetailsView が明示的に更新される ([クリックしてフルサイズの画像を表示する](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png))

## <a name="summary"></a>まとめ

DropDownList はマスター/詳細レポートの理想的なユーザーインターフェイス要素として機能し、マスターレコードと詳細レコードの間に一対多のリレーションシップが存在します。 前のチュートリアルでは、1つの DropDownList を使用して、選択したカテゴリによって表示される製品をフィルター処理する方法を説明しました。 このチュートリアルでは、製品の GridView を DropDownList に置き換え、DetailsView を使用して選択した製品の詳細を表示しました。 このチュートリアルで説明する概念は、顧客、注文、注文品目など、複数の一対多リレーションシップを含むデータモデルに簡単に拡張できます。 一般に、一対多のリレーションシップでは、"one" エンティティごとに DropDownList をいつでも追加できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-filtering-with-a-dropdownlist-vb.md)
> [次へ](master-detail-filtering-across-two-pages-vb.md)
