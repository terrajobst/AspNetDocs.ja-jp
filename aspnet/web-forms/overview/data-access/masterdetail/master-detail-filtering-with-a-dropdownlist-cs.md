---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: DropDownList (C#) を使用したマスター/詳細のフィルター処理Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、DropDownList コントロールのマスターレコードと、GridView で選択したリスト項目の詳細を表示する方法について説明します。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 3ec549f9da7a2b3a021e77827f0039e6ae60b5c5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616069"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>DropDownList でマスター/詳細をフィルター処理する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe)または[PDF のダウンロード](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> このチュートリアルでは、DropDownList コントロールのマスターレコードと、GridView で選択したリスト項目の詳細を表示する方法について説明します。

## <a name="introduction"></a>はじめに

一般的なレポートの種類として、*マスター/詳細レポート*があります。このレポートでは、"マスター" レコードのセットが表示されます。 その後、ユーザーはマスターレコードのいずれかにドリルダウンして、マスターレコードの "詳細" を表示できます。 マスター/詳細レポートは、すべてのカテゴリを表示し、ユーザーが特定のカテゴリを選択し、関連付けられている製品を表示できるようにするレポートなど、1対多のリレーションシップを視覚化するために最適な選択肢です。 さらに、マスター/詳細レポートは、特に多くの列を持つテーブルから詳細情報を表示する場合に便利です。 たとえば、マスター/詳細レポートの "マスター" レベルでは、製品名とデータベース内の製品の単価だけが表示され、特定の製品をドリルダウンすると、追加の製品フィールド (カテゴリ、仕入先、単位あたりの数量など) が表示されます。

マスター/詳細レポートを実装するには、さまざまな方法があります。 このチュートリアルと次の3つのチュートリアルでは、さまざまなマスター/詳細レポートについて説明します。 このチュートリアルでは、 [DropDownList コントロール](https://msdn.microsoft.com/library/dtx91y0z.aspx)のマスターレコードと、GridView で選択したリスト項目の詳細を表示する方法について説明します。 特に、このチュートリアルのマスター/詳細レポートには、カテゴリと製品情報が一覧表示されます。

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>手順 1: DropDownList でカテゴリを表示する

マスター/詳細レポートには、選択したリストアイテムの製品が GridView のページに表示されるように、DropDownList にカテゴリが一覧表示されます。 最初のタスクであるのは、カテゴリを DropDownList に表示することです。 `Filtering` フォルダーの [`FilterByDropDownList.aspx`] ページを開き、[ツールボックス] の DropDownList をページデザイナーにドラッグして、その `ID` プロパティを [`Categories`] に設定します。 次に、DropDownList のスマートタグから [データソースの選択] リンクをクリックします。 データソース構成ウィザードが表示されます。

[DropDownList のデータソースを指定 ![には](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**図 1**: DropDownList のデータソースを指定[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png)されます)

`CategoriesBLL` クラスの `GetCategories()` メソッドを呼び出す `CategoriesDataSource` という名前の新しい ObjectDataSource を追加します。

[新しい ObjectDataSource という名前の新しい名前のデータソースを追加 ![には](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**図 2**: `CategoriesDataSource` という名前の新しい ObjectDataSource を追加[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png)される)

[カテゴリ Bll クラスの使用を選択 ![](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**図 3**: `CategoriesBLL` クラスの使用を選択する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png)されます)

[GetCategories () メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**図 4**: `GetCategories()` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))

ObjectDataSource を構成した後も、DropDownList に表示するデータソースフィールドと、リストアイテムの値として関連付ける必要があるデータソースフィールドを指定する必要があります。 `CategoryName` フィールドを表示として使用し、各リスト項目の値として `CategoryID` します。

[DropDownList で [区分項目] フィールドを表示し、値として CategoryID を使用する ![ます。](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**図 5**: DropDownList に `CategoryName` フィールドが表示され、`CategoryID` を値として使用する ([クリックしてフルサイズの画像を表示する](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))

この時点で、`Categories` テーブルのレコードが設定された DropDownList コントロールがあります (すべての操作は約6秒で完了しました)。 図6は、ブラウザーを通じて表示されたときの進行状況を示しています。

[ドロップダウンリスト ![現在のカテゴリを一覧表示します。](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**図 6**: ドロップダウンリストに現在のカテゴリが表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png)されます)

## <a name="step-2-adding-the-products-gridview"></a>手順 2: 製品の GridView を追加する

マスター/詳細レポートの最後の手順は、選択したカテゴリに関連付けられている製品を一覧表示することです。 これを実現するには、GridView をページに追加し、`productsDataSource`という名前の新しい ObjectDataSource を作成します。 `productsDataSource` コントロールが、`ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドからのデータをカリングするようにします。

[Get製品 Bycategoryid (categoryID) メソッドを選択 ![には](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**図 7**: `GetProductsByCategoryID(categoryID)` メソッドを選択[する (クリックしてフルサイズのイメージを表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))

このメソッドを選択すると、ObjectDataSource ウィザードによって、メソッドの *`categoryID`* パラメーターの値を入力するように求められます。 選択した `categories` DropDownList 項目の値を使用するには、パラメーターソースを制御するように設定し、ControlID を `Categories`に設定します。

[categoryID パラメーターをカテゴリの DropDownList の値に設定 ![](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**図 8**: *`categoryID`* パラメーターを `Categories` DropDownList の値に設定する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png)されます)

ブラウザーで進行状況を確認してみてください。 最初にページにアクセスしたときに、選択したカテゴリ (飲料) に属している製品が表示されます (図9を参照)。 DropDownList を変更してもデータは更新されません。 これは、GridView を更新するためにポストバックが発生する必要があるためです。 これを実現するには、次の2つのオプションがあります (どちらの方法でもコードを記述する必要はありません)。

- **[カテゴリ] [DropDownList の**[AutoPostBack] プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**を [True] に設定します。** (これを行うには、DropDownList のスマートタグの [AutoPostBack を有効にする] オプションをオンにします)。これにより、DropDownList の選択項目がユーザーによって変更されるたびにポストバックがトリガーされます。 このため、ユーザーが DropDownList から新しいカテゴリを選択すると、ポストバックは議論し、新しく選択されたカテゴリの製品で GridView が更新されます。 (これは、このチュートリアルで使用した方法です)。
- **DropDownList の横にボタン Web コントロールを追加します。** `Text` プロパティを更新するように設定します。 この方法では、ユーザーは新しいカテゴリを選択し、ボタンをクリックする必要があります。 このボタンをクリックすると、ポストバックが発生し、GridView が更新されて、選択したカテゴリの製品が一覧表示されます。

図9と10は、マスター/詳細レポートの動作を示しています。

[ページに初めてアクセスしたときに、飲料製品が表示される ![](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**図 9**: 最初にページにアクセスしたときに、飲み物の製品が表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png)されます)

[新しい製品 ([生成]) を選択する ![自動的にポストバックが発生し、GridView が更新されます。](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**図 10**: 新しい製品 ([生成]) を選択すると自動的にポストバックが発生し、GridView が更新されます ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png)されます)

## <a name="adding-a----choose-a-category----list-item"></a>"--カテゴリの選択--" リスト項目を追加する

最初に [`FilterByDropDownList.aspx`] ページにアクセスしたときに、[カテゴリ] [DropDownList の最初のリスト項目 (飲料)] が既定で選択されており、GridView の飲料製品が表示されます。 最初のカテゴリの製品を表示するのではなく、"--カテゴリの選択--" のような DropDownList 項目を選択しておくことをお勧めします。

新しいリストアイテムを DropDownList に追加するには、プロパティウィンドウにアクセスし、`Items` プロパティの省略記号をクリックします。 `Text` "--Category--" と `Value` `-1`を持つ新しいリスト項目を追加します。

[![の追加--カテゴリの選択--リスト項目](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**図 11**: 追加 a--カテゴリの選択--リスト項目 ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png)される)

または、次のマークアップを DropDownList に追加して、リスト項目を追加することもできます。

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

また、`AppendDataBoundItems` が True でない場合は、項目が ObjectDataSource から DropDownList にバインドされると、手動で追加されたリスト項目が上書きされるので、DropDownList コントロールの `AppendDataBoundItems` を True に設定する必要があります。

![AppendDataBoundItems プロパティを True に設定します。](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**図 12**: `AppendDataBoundItems` プロパティを True に設定する

これらの変更が完了すると、最初にページにアクセスしたときに、[--カテゴリを選択--] オプションが選択され、製品は表示されません。

[最初のページの読み込みで ![製品が表示されない](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**図 13**: 初期ページの読み込み時に製品が表示されない ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png)されます)

"--カテゴリの選択--" リスト項目が選択されているために、製品が表示されない理由は、その値が `-1` で、データベースに `-1`の `CategoryID` を持つ製品が存在しないためです。 この動作が必要な場合は、この時点で完了です。 ただし、"--カテゴリの選択--" リスト項目が選択されているときに*すべて*のカテゴリを表示する場合は、`ProductsBLL` クラスに戻り、`GetProductsByCategoryID(categoryID)` メソッドをカスタマイズして、渡された *`categoryID`* パラメーターがゼロ未満の場合に `GetProducts()` メソッドを呼び出すようにします。

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

ここで使用する手法は、[宣言型パラメーター](../basic-reporting/declarative-parameters-cs.md)のチュートリアルですべてのサプライヤーを表示する方法と似ています。この例では、`-1` の値を使用して、`null`ではなくすべてのレコードを取得するように指定しています。 これは、`GetProductsByCategoryID(categoryID)` メソッドの *`categoryID`* パラメーターには、渡された整数値が必要であるのに対し、宣言型パラメーターのチュートリアルでは、文字列入力パラメーターを渡しているためです。

図14は、"--カテゴリの選択--" オプションが選択されている場合の `FilterByDropDownList.aspx` のスクリーンショットを示しています。 ここでは、すべての製品が既定で表示され、ユーザーは特定のカテゴリを選択して表示を絞り込むことができます。

[すべての製品が既定で一覧表示されるように ![](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**図 14**: 既定ですべての製品が表示される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png)されます)

## <a name="summary"></a>要約

階層的に関連するデータを表示する場合は、多くの場合、マスター/詳細レポートを使用してデータを表示することができます。この場合、ユーザーは階層の最上位からデータのつい man を開始し、詳細にドリルダウンできます。 このチュートリアルでは、選択したカテゴリの製品を示す単純なマスター/詳細レポートを作成する方法を説明しました。 これを実現するには、選択したカテゴリに属する製品のカテゴリの一覧の DropDownList と GridView を使用します。

次の[チュートリアル](master-detail-filtering-with-two-dropdownlists-cs.md)では、2つの dropdownlists を使用して、DropDownList インターフェイスを1ステップ進めます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [次へ](master-detail-filtering-with-two-dropdownlists-cs.md)
