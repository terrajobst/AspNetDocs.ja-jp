---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: DropDownList を使用したマスター/詳細フィルター処理 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、DropDownLists を使用して ' master ' レコードを表示する1つの web ページでマスター/詳細レポートを表示する方法について説明します。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 537f8e76bc0cbfa759a014b63ae5f68b5d3ca64d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491086"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>DropDownList でマスター/詳細をフィルター処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe)または[PDF のダウンロード](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> このチュートリアルでは、DropDownLists を使用して "マスター" レコードを表示する1つの web ページでマスター/詳細レポートを表示する方法と、"詳細" を表示するための DataList を説明します。

## <a name="introduction"></a>はじめに

最初に DropDownList チュートリアルを使用して以前の[マスター/詳細フィルター](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)の GridView を使用して作成したマスター/詳細レポートは、"マスター" レコードのセットを表示することから始まります。 その後、ユーザーはマスターレコードのいずれかにドリルダウンして、マスターレコードの "詳細" を表示できます。 マスター/詳細レポートは、一対多のリレーションシップを視覚化するための最適な選択肢であり、特に多数の列を含むテーブルから詳細情報を表示するために適しています。 前のチュートリアルでは、GridView および DetailsView コントロールを使用してマスター/詳細レポートを実装する方法を説明しました。 このチュートリアルと次の2つのチュートリアルでは、これらの概念を再検討しますが、代わりに DataList コントロールと Repeater コントロールの使用に焦点を当てます。

このチュートリアルでは、DropDownList を使用して "マスター" レコードを格納し、DataList に "details" レコードを表示する方法について説明します。

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>手順 1: マスター/詳細チュートリアル Web ページの追加

このチュートリアルを開始する前に、まず、このチュートリアルに必要なフォルダーと ASP.NET のページを追加し、次の2つのページで、DataList および Repeater コントロールを使用してマスター/詳細レポートを処理してみましょう。 まず、`DataListRepeaterFiltering`という名前のプロジェクトに新しいフォルダーを作成します。 次に、次の5つの ASP.NET ページをこのフォルダーに追加します。マスターページ `Site.master`を使用するようにすべてのページを構成します。

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![DatASP.NET Strepeaterfiltering フォルダーを作成し、チュートリアルのページを追加します。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**図 1**: `DataListRepeaterFiltering` フォルダーを作成し、チュートリアル ASP.NET ページを追加する

次に、[`Default.aspx`] ページを開き、`SectionLevelTutorialListing.ascx` ユーザーコントロールを `UserControls` フォルダーからデザイン画面にドラッグします。 このユーザーコントロールは、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)チュートリアルで作成したもので、サイトマップを列挙し、現在のセクションのチュートリアルを箇条書きの一覧に表示します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png)されます)

作成するマスター/詳細のチュートリアルを箇条書きに表示するには、サイトマップに追加する必要があります。 `Web.sitemap` ファイルを開き、「DataList と Repeater を使用したデータの表示」の後に、次のマークアップを追加します。

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]

![新しい ASP.NET ページを含めるようにサイトマップを更新する](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**図 3**: 新しい ASP.NET ページを含めるようにサイトマップを更新する

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>手順 2: DropDownList でカテゴリを表示する

マスター/詳細レポートには、選択したリストアイテムの製品が DataList のページに表示されるように、DropDownList にカテゴリが一覧表示されます。 最初のタスクであるのは、カテゴリを DropDownList に表示することです。 まず、`DataListRepeaterFiltering` フォルダーの [`FilterByDropDownList.aspx`] ページを開いて、[ツールボックス] から [DropDownList] をページデザイナーにドラッグします。 次に、DropDownList の `ID` プロパティを `Categories`に設定します。 DropDownList のスマートタグから [データソースの選択] リンクをクリックし、`CategoriesDataSource`という名前の新しい ObjectDataSource を作成します。

[新しい ObjectDataSource という名前の新しい名前のデータソースを追加 ![には](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**図 4**: `CategoriesDataSource` という名前の新しい ObjectDataSource を追加[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png)される)

`CategoriesBLL` クラスの `GetCategories()` メソッドを呼び出すように、新しい ObjectDataSource を構成します。 ObjectDataSource を構成した後も、DropDownList に表示するデータソースフィールドを指定し、各リスト項目の値として関連付ける必要があるデータソースフィールドを指定する必要があります。 `CategoryName` フィールドを表示として使用し、各リスト項目の値として `CategoryID` します。

[DropDownList で [区分項目] フィールドを表示し、値として CategoryID を使用する ![ます。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**図 5**: DropDownList に `CategoryName` フィールドが表示され、`CategoryID` を値として使用する ([クリックしてフルサイズの画像を表示する](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))

この時点で、`Categories` テーブルのレコードが設定された DropDownList コントロールがあります (すべての操作は約6秒で完了しました)。 図6は、ブラウザーを通じて表示されたときの進行状況を示しています。

[ドロップダウンリスト ![現在のカテゴリを一覧表示します。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**図 6**: ドロップダウンリストに現在のカテゴリが表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png)されます)

## <a name="step-2-adding-the-products-datalist"></a>手順 2: 製品の DataList を追加する

マスター/詳細レポートの最後の手順は、選択したカテゴリに関連付けられている製品を一覧表示することです。 これを実現するには、DataList をページに追加し、`ProductsByCategoryDataSource`という名前の新しい ObjectDataSource を作成します。 `ProductsByCategoryDataSource` コントロールが、`ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドからデータを取得するようにします。 このマスター/詳細レポートは読み取り専用であるため、[挿入]、[更新]、および [削除] の各タブで [(なし)] オプションを選択します。

[Get製品 Bycategoryid (categoryID) メソッドを選択 ![には](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**図 7**: `GetProductsByCategoryID(categoryID)` メソッドを選択[する (クリックしてフルサイズのイメージを表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))

[次へ] をクリックすると、ObjectDataSource ウィザードによって、`GetProductsByCategoryID(categoryID)` メソッドの *`categoryID`* パラメーターの値のソースが要求されます。 選択した `categories` DropDownList 項目の値を使用するには、パラメーターソースを制御するように設定し、ControlID を `Categories`に設定します。

[categoryID パラメーターをカテゴリの DropDownList の値に設定 ![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**図 8**: *`categoryID`* パラメーターを `Categories` DropDownList の値に設定する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、各データフィールドの名前と値を表示する DataList の `ItemTemplate` が自動的に生成されます。 ここでは、DataList を拡張して、製品の名前、カテゴリ、仕入先、数量/単位、価格だけでなく、各項目の間に `<hr>` 要素を挿入する `SeparatorTemplate` を表示する `ItemTemplate` を使用するようにします。 ここでは、「 [DataList コントロールと Repeater コントロールでデータを表示](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md)する」チュートリアルの例の `ItemTemplate` を使用しますが、視覚的に魅力のあるテンプレートマークアップを自由に使用できます。

これらの変更を行った後、DataList とその ObjectDataSource のマークアップは次のようになります。

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

ブラウザーで進行状況を確認してみてください。 最初にページにアクセスすると、選択したカテゴリ (飲料) に属するこれらの製品が表示されます (図9を参照)。 DropDownList を変更してもデータは更新されません。 これは、DataList を更新するためにポストバックが発生する必要があるためです。 これを実現するには、DropDownList の `AutoPostBack` プロパティを `true` に設定するか、ボタン Web コントロールをページに追加します。 このチュートリアルでは、DropDownList の `AutoPostBack` プロパティを `true`に設定することを選択しました。

図9と10は、マスター/詳細レポートの動作を示しています。

[ページに初めてアクセスしたときに、飲料製品が表示される ![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**図 9**: 最初にページにアクセスしたときに、飲み物の製品が表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png)されます)

[新しい製品 ([生成]) を選択する ![自動的にポストバックが発生し、DataList が更新されます。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**図 10**: 新しい製品 ([生成]) を選択すると自動的にポストバックが発生し、DataList が更新されます ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png)されます)

## <a name="adding-a----choose-a-category----list-item"></a>"--カテゴリの選択--" リスト項目を追加する

最初に [`FilterByDropDownList.aspx`] ページにアクセスしたときに、[カテゴリ] の [DropDownList] の最初のリスト項目 (飲料) が既定で選択され、[DataList] の飲料製品が表示されます。 DropDownList チュートリアルを使用した*マスター/詳細フィルター処理*で、既定で選択された dropdownlist に "--Category--" オプションを追加しました。選択すると、データベース内の*すべて*の製品が表示されます。 このようなアプローチは、GridView で製品を一覧表示するときに管理しやすくなりました。これは、各製品の行が画面の実際のサイズを小さくするためです。 ただし、DataList では、各製品の情報が画面のチャンクを大幅に消費します。 引き続き "--Category を選択する--" オプションを追加して、既定で選択します。ただし、選択したすべての製品を表示するのではなく、製品が表示されないように構成します。

新しいリストアイテムを DropDownList に追加するには、プロパティウィンドウにアクセスし、`Items` プロパティの省略記号をクリックします。 `Text` "--Category--" と `Value` `0`を持つ新しいリスト項目を追加します。

![追加](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**図 11**: "--カテゴリを選択する--" リスト項目を追加する

または、次のマークアップを DropDownList に追加して、リスト項目を追加することもできます。

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

さらに、DropDownList コントロールの `AppendDataBoundItems` を `true` に設定する必要があります。これは `false` (既定) に設定されている場合、カテゴリが ObjectDataSource から DropDownList にバインドされると、手動で追加したリスト項目が上書きされるためです。

![AppendDataBoundItems プロパティを True に設定します。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**図 12**: `AppendDataBoundItems` プロパティを True に設定する

"--カテゴリの選択--" リスト項目の値 `0` を選択した理由は、システムには値が `0`であるカテゴリが存在しないため、"--カテゴリの選択--" リスト項目が選択されたときに製品レコードが返されないためです。 これを確認するには、ブラウザーを使用してページにアクセスします。 図13に示されているように、最初にページを表示すると、"--カテゴリを選択--" リスト項目が選択され、製品が表示されません。

[![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**図 13**: "--カテゴリの選択--" リスト項目が選択されている場合、製品は表示されません ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png)されます)

[--カテゴリの選択--] オプションを選択したときに*すべて*の製品を表示する場合は、代わりに値 `-1` を使用します。 ずる賢い reader は、DropDownList チュートリアルを使用し*てマスター/詳細フィルター処理*を行ったことを思い出して、`-1` の *`categoryID`* 値が渡された場合に、すべての製品レコードが返されるように `ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドを更新しました。

## <a name="summary"></a>まとめ

階層的に関連するデータを表示する場合は、多くの場合、マスター/詳細レポートを使用してデータを表示することができます。この場合、ユーザーは階層の最上位からデータのつい man を開始し、詳細にドリルダウンできます。 このチュートリアルでは、選択したカテゴリの製品を示す単純なマスター/詳細レポートを作成する方法を説明しました。 これを実現するには、選択したカテゴリに属する製品のカテゴリの一覧に DropDownList を使用します。

次のチュートリアルでは、2ページでマスターレコードと詳細レコードを分離する方法について説明します。 最初のページには、"マスター" レコードの一覧と、詳細を表示するためのリンクが表示されます。 リンクをクリックすると、ユーザーが2番目のページに whisk、選択したマスターレコードの詳細が表示されます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Randy になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [次へ](master-detail-filtering-acess-two-pages-datalist-vb.md)
