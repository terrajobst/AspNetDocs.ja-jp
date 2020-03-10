---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
title: 宣言型パラメーター (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ハードコーディングされた値に設定されたパラメーターを使用して、DetailsView コントロールに表示するデータを選択する方法について説明します。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: dc1234a3-114f-4c9a-8d25-50ca03cc8e8e
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
msc.type: authoredcontent
ms.openlocfilehash: cdc42752fc78d18366af037a81fe4ebe5a1646ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483130"
---
# <a name="declarative-parameters-vb"></a>宣言パラメーター (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_5_VB.exe)または[PDF のダウンロード](declarative-parameters-vb/_static/datatutorial05vb1.pdf)

> このチュートリアルでは、ハードコーディングされた値に設定されたパラメーターを使用して、DetailsView コントロールに表示するデータを選択する方法について説明します。

## <a name="introduction"></a>はじめに

最後の[チュートリアル](displaying-data-with-the-objectdatasource-vb.md)では、`ProductsBLL` クラスから `GetProducts()` メソッドを呼び出した ObjectDataSource コントロールにバインドされた GridView、DetailsView、FormView コントロールを使用してデータを表示する方法について見てきました。 `GetProducts()` メソッドは、Northwind データベースの `Products` テーブルのすべてのレコードを格納する、厳密に型指定された DataTable を返します。 `ProductsBLL` クラスには、`GetProductByProductID(productID)`、`GetProductsByCategoryID(categoryID)`、および `GetProductsBySupplierID(supplierID)`製品のサブセットのみを返すための追加メソッドが含まれています。 これら3つのメソッドは、返された製品情報をフィルター処理する方法を示す入力パラメーターを想定しています。

ObjectDataSource は、入力パラメーターを必要とするメソッドを呼び出すために使用できますが、そのためには、これらのパラメーターの値の取得元となる場所を指定する必要があります。 パラメーター値は、ハードコーディングすることも、クエリ文字列値、セッション変数、ページ上の Web コントロールのプロパティ値など、さまざまな動的ソースから取得することもできます。

このチュートリアルでは、まず、パラメーターをハードコーディングされた値に設定する方法を説明します。 具体的には、特定の製品に関する情報を表示する DetailsView をページに追加する方法について説明します。これには、`ProductID` が5の、Chef Anton の Gumbo Mix が含まれます。 次に、Web コントロールに基づいてパラメーター値を設定する方法について説明します。 具体的には、テキストボックスを使用してユーザーが国に入力できるようにします。その後、ボタンをクリックすると、その国に存在する業者の一覧が表示されます。

## <a name="using-a-hard-coded-parameter-value"></a>ハードコーディングされたパラメーター値の使用

最初の例では、まず、`BasicReporting` フォルダーの `DeclarativeParams.aspx` ページに DetailsView コントロールを追加します。 DetailsView のスマートタグから、ドロップダウンリストから [新しいデータソースの&gt; を &lt;] を選択し、ObjectDataSource を追加することを選択します。

[![ObjectDataSource をページに追加する](declarative-parameters-vb/_static/image2.png)](declarative-parameters-vb/_static/image1.png)

**図 1**: ObjectDataSource をページに追加する ([クリックすると、フルサイズの画像が表示](declarative-parameters-vb/_static/image3.png)されます)

これにより、ObjectDataSource コントロールの [データソースの選択] ウィザードが自動的に開始されます。 ウィザードの最初の画面で `ProductsBLL` クラスを選択します。

[製品の Bll クラスを選択 ![には](declarative-parameters-vb/_static/image5.png)](declarative-parameters-vb/_static/image4.png)

**図 2**: `ProductsBLL` クラスを選択[する (クリックすると、フルサイズの画像が表示](declarative-parameters-vb/_static/image6.png)されます)

特定の製品に関する情報を表示する必要があるため、`GetProductByProductID(productID)` メソッドを使用します。

[GetProductByProductID (productID) メソッドを選択 ![には](declarative-parameters-vb/_static/image8.png)](declarative-parameters-vb/_static/image7.png)

**図 3**: `GetProductByProductID(productID)` メソッドを選択[する (クリックしてフルサイズの画像を表示する](declarative-parameters-vb/_static/image9.png))

選択したメソッドにはパラメーターが含まれているため、ウィザードの画面がもう1つ表示されます。この画面では、パラメーターに使用する値を定義するよう求められています。 左側の一覧には、選択したメソッドのすべてのパラメーターが表示されます。 `GetProductByProductID(productID)` には、`productID`が1つだけあります。 右側で、選択したパラメーターの値を指定できます。 [パラメーターのソース] ボックスの一覧には、パラメーター値に使用できるさまざまなソースが列挙されています。 `productID` パラメーターにはハードコーディングされた値5を指定するので、パラメーター source は None のままにし、DefaultValue テキストボックスに「5」と入力します。

[ハードコードされたパラメーター値5が productID パラメーターに使用される ![](declarative-parameters-vb/_static/image11.png)](declarative-parameters-vb/_static/image10.png)

**図 4**: ハードコーディングされたパラメーター値5が `productID` パラメーターに使用されます ([クリックすると、フルサイズのイメージが表示](declarative-parameters-vb/_static/image12.png)されます)

データソースの構成ウィザードを完了すると、ObjectDataSource コントロールの宣言型マークアップには、`SelectMethod` プロパティで定義されたメソッドに必要な各入力パラメーターの `SelectParameters` コレクション内の `Parameter` オブジェクトが含まれます。 この例で使用しているメソッドでは、1つの入力パラメーターだけが想定されているため、ここにはエントリが1つだけあります。 `parameterID`ます。 `SelectParameters` コレクションには、`System.Web.UI.WebControls` 名前空間の `Parameter` クラスから派生した任意のクラスを含めることができます。 ハードコーディングされたパラメーター値の場合は、基本 `Parameter` クラスが使用されますが、その他のパラメーターソースオプションでは、派生 `Parameter` クラスが使用されます。必要に応じて、独自の[カスタムパラメーター型](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)を作成することもできます。

[!code-aspx[Main](declarative-parameters-vb/samples/sample1.aspx)]

> [!NOTE]
> 自分のコンピューターに従っている場合、この時点で表示される宣言型マークアップには、`InsertMethod`、`UpdateMethod`、および `DeleteMethod` プロパティの値と `DeleteParameters`が含まれている可能性があります。 ObjectDataSource の [データソースの選択] ウィザードでは、挿入、更新、および削除に使用するメソッドが `ProductBLL` から自動的に指定されます。これらのメソッドを明示的にクリアしない限り、上記のマークアップに含まれます。

このページにアクセスすると、データ Web コントロールは ObjectDataSource の `Select` メソッドを呼び出します。このメソッドは、`productID` 入力パラメーターに対してハードコーディングされた値5を使用して、`ProductsBLL` クラスの `GetProductByProductID(productID)` メソッドを呼び出します。 メソッドは、Chef Anton の Gumbo ミックス (製品の `ProductID` 5) に関する情報を含む単一行を含む、厳密に型指定された `ProductDataTable` オブジェクトを返します。

[Chef Anton の Gumbo ミックスに関する ![情報が表示されます](declarative-parameters-vb/_static/image14.png)](declarative-parameters-vb/_static/image13.png)

**図 5**: Chef Anton の Gumbo ミックスに関する情報の表示 ([クリックすると、フルサイズの画像が表示](declarative-parameters-vb/_static/image15.png)されます)

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>パラメーター値を Web コントロールのプロパティ値に設定する

ObjectDataSource のパラメーター値は、ページの Web コントロールの値に基づいて設定することもできます。 これを説明するために、ユーザーによって指定された国に配置されているすべての仕入先を一覧表示する GridView を使用します。 この作業を行うには、ユーザーが国名を入力できるページにテキストボックスを追加します。 このテキストボックスコントロールの `ID` プロパティを `CountryName`に設定します。 また、ボタン Web コントロールも追加します。

[ID CountryName のページにテキストボックスを追加 ![には](declarative-parameters-vb/_static/image17.png)](declarative-parameters-vb/_static/image16.png)

**図 6**: `ID` `CountryName` を含むテキストボックスをページに追加する ([クリックすると、フルサイズの画像が表示](declarative-parameters-vb/_static/image18.png)されます)

次に、GridView をページに追加し、スマートタグから新しい ObjectDataSource を追加することを選択します。 仕入先情報を表示するため、ウィザードの最初の画面から `SuppliersBLL` クラスを選択します。 2番目の画面で、`GetSuppliersByCountry(country)` メソッドを選択します。

[GetSuppliersByCountry (country) メソッドを選択 ![には](declarative-parameters-vb/_static/image20.png)](declarative-parameters-vb/_static/image19.png)

**図 7**: `GetSuppliersByCountry(country)` メソッドを選択[する (クリックしてフルサイズのイメージを表示する](declarative-parameters-vb/_static/image21.png))

`GetSuppliersByCountry(country)` メソッドに入力パラメーターがあるため、ウィザードには、パラメーター値を選択するための最後の画面がもう一度表示されます。 ここでは、パラメーターソースを [制御] に設定します。 これにより、[ControlID] ドロップダウンリストに、ページ上のコントロールの名前が設定されます。一覧から `CountryName` コントロールを選択します。 ページが最初に表示されたときに `CountryName` テキストボックスは空白になるため、結果は返されず、何も表示されません。 既定でいくつかの結果を表示するには、DefaultValue テキストボックスを適宜設定します。

[CountryName コントロール値にパラメーター値を設定 ![には](declarative-parameters-vb/_static/image23.png)](declarative-parameters-vb/_static/image22.png)

**図 8**: パラメーター値を `CountryName` コントロールの値に設定する ([クリックしてフルサイズのイメージを表示する](declarative-parameters-vb/_static/image24.png))

ObjectDataSource の宣言型マークアップは、最初の例とは少し異なり、標準の `Parameter` オブジェクトの代わりに[Controlparameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx)を使用します。 `ControlParameter` には、Web コントロールの `ID` と、パラメーターに使用するプロパティ値 (`PropertyName`) を指定するための追加のプロパティがあります。 データソースの構成ウィザードでは、テキストボックスの場合、パラメーター値に `Text` プロパティを使用することができます。 ただし、Web コントロールから別のプロパティ値を使用する場合は、ここで `PropertyName` 値を変更するか、ウィザードの [詳細プロパティの表示] リンクをクリックします。

[!code-aspx[Main](declarative-parameters-vb/samples/sample2.aspx)]

ページに初めてアクセスしたときに、`CountryName` テキストボックスが空になります。 ObjectDataSource の `Select` メソッドは GridView によってまだ呼び出されていますが、`GetSuppliersByCountry(country)` メソッドに `Nothing` の値が渡されます。 TableAdapter は、`Nothing` をデータベース `NULL` 値 (`DBNull.Value`) に変換しますが、`GetSuppliersByCountry(country)` メソッドによって使用されるクエリは、`NULL` パラメーターに `@CategoryID` 値が指定されている場合に値を返さないように記述されています。 つまり、仕入先は返されません。

ただし、ビジターが1つの国に入力し、[サプライヤーの表示] ボタンをクリックするとポストバックが発生すると、ObjectDataSource の `Select` メソッドが再クエリされ、`country` パラメーターとして TextBox コントロールの `Text` 値が渡されます。

[カナダからの仕入先の ![が表示されます。](declarative-parameters-vb/_static/image26.png)](declarative-parameters-vb/_static/image25.png)

**図 9**: カナダの仕入先が表示されます ([クリックすると、フルサイズの画像が表示](declarative-parameters-vb/_static/image27.png)されます)

## <a name="showing-all-suppliers-by-default"></a>既定ですべての仕入先を表示する

最初にページを表示したときにサプライヤーが表示されないようにするには、最初に*すべて*のサプライヤーを表示し、ユーザーがテキストボックスに国名を入力してリストを省いできるようにします。 テキストボックスが空の場合、`SuppliersBLL` クラスの `GetSuppliersByCountry(country)` メソッドは *`country`* 入力パラメーターの `Nothing` に渡されます。 この `Nothing` 値は、次のクエリの `@Country` パラメーターのデータベース `NULL` 値に変換される DAL の `GetSupplierByCountry(country)` メソッドに渡されます。

[!code-sql[Main](declarative-parameters-vb/samples/sample3.sql)]

式 `Country = NULL` は、`Country` 列に `NULL` 値があるレコードに対しても常に False を返します。したがって、レコードは返されません。

Country テキストボックスが空のときに*すべて*の業者を返すには、BLL の `GetSuppliersByCountry(country)` メソッドを拡張して、country パラメーターが `Nothing` ときに `GetSuppliers()` メソッドを呼び出し、それ以外の場合は DAL の `GetSuppliersByCountry(country)` メソッドを呼び出すことができます。 これにより、国が指定されていない場合はすべての業者が返され、country パラメーターが含まれている場合は、サプライヤーの適切なサブセットが返されます。

`SuppliersBLL` クラスの `GetSuppliersByCountry(country)` メソッドを次のように変更します。

[!code-vb[Main](declarative-parameters-vb/samples/sample4.vb)]

この変更により、[`DeclarativeParams.aspx`] ページには、最初にアクセスしたとき (または `CountryName` テキストボックスが空のとき) にすべての仕入先が表示されます。

[すべての仕入先が既定で表示されるようになりました ![](declarative-parameters-vb/_static/image29.png)](declarative-parameters-vb/_static/image28.png)

**図 10**: すべての仕入先が既定で表示される ([クリックしてフルサイズの画像を表示する](declarative-parameters-vb/_static/image30.png))

## <a name="summary"></a>まとめ

入力パラメーターでメソッドを使用するには、ObjectDataSource の `SelectParameters` コレクションのパラメーターの値を指定する必要があります。 パラメーターの種類によって、さまざまなソースからパラメーター値を取得できます。 既定のパラメーターの型はハードコーディングされた値を使用しますが、単純に (コード行を含めずに) パラメーター値をクエリ文字列、セッション変数、cookie から取得することも、ページ上の Web コントロールからユーザーが入力した値から取得することもできます。

このチュートリアルで見た例では、宣言型パラメーター値の使用方法を説明しました。 ただし、現在の日付と時刻など、利用できないパラメーターソースを使用する必要がある場合や、サイトでメンバーシップを使用している場合は、ビジターのユーザー ID を使用することがあります。 このようなシナリオでは、ObjectDataSource の前にプログラムによってパラメーター値を設定して、基になるオブジェクトのメソッドを呼び出すことができます。 これを実現する方法については、[次のチュートリアル](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)で説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](displaying-data-with-the-objectdatasource-vb.md)
> [次へ](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)
