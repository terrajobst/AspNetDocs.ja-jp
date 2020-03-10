---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: GridView のフッターから新しいレコードを挿入する (VB) |Microsoft Docs
author: rick-anderson
description: GridView コントロールには、新しいデータレコードを挿入するための組み込みのサポートが用意されていませんが、このチュートリアルでは、GridView を拡張して...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 67ef370a90bc843f5c2da80bb43c8ef8de216b51
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78477412"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>GridView のフッターから新しいレコードを挿入する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe)または[PDF のダウンロード](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> GridView コントロールは、新しいデータレコードを挿入するための組み込みサポートを提供していませんが、このチュートリアルでは、挿入インターフェイスを含めるように GridView を拡張する方法について説明します。

## <a name="introduction"></a>はじめに

[「データの挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)」のチュートリアルで説明したように、GridView、DetailsView、および FormView Web コントロールには、組み込みのデータ変更機能が含まれています。 宣言型のデータソースコントロールで使用する場合、これら3つの Web コントロールをすばやく簡単に構成して、データを変更したり、コードを1行も記述しなくてもかまいません。 残念ながら、DetailsView コントロールと FormView コントロールのみが、組み込みの挿入、編集、および削除機能を提供しています。 GridView は、編集および削除のサポートのみを提供します。 ただし、1つのカギ線のグリースでは、挿入インターフェイスを含めるように GridView を拡張できます。

GridView に挿入機能を追加する際には、新しいレコードを追加する方法を決定し、挿入インターフェイスを作成し、新しいレコードを挿入するコードを記述する必要があります。 このチュートリアルでは、GridView のフッター行に挿入インターフェイスを追加する方法について説明します (図1を参照)。 各列のフッターセルには、適切なデータコレクションユーザーインターフェイス要素 (製品名のテキストボックス、業者の DropDownList など) が含まれます。 また、[追加] ボタンの列も必要です。クリックすると、フッター行に指定された値を使用して、ポストバックが発生し、`Products` テーブルに新しいレコードが挿入されます。

[フッター行に ![新しい製品を追加するためのインターフェイスが用意されています。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**図 1**: フッター行は、新しい製品を追加するためのインターフェイスを提供します ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png)されます)

## <a name="step-1-displaying-product-information-in-a-gridview"></a>手順 1: GridView で製品情報を表示する

GridView s フッターでの挿入インターフェイスの作成については、まず、データベース内の製品を一覧表示するページへの GridView の追加について説明します。 まず、`EnhancedGridView` フォルダーの [`InsertThroughFooter.aspx`] ページを開き、GridView をツールボックスからデザイナーにドラッグします。 GridView の `ID` プロパティを `Products`に設定します。 次に、GridView s スマートタグを使用して、`ProductsDataSource`という名前の新しい ObjectDataSource にバインドします。

[![新しい ObjectDataSource Datasource を作成する](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**図 2**: `ProductsDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png)される)

`ProductsBLL` クラス s `GetProducts()` メソッドを使用して製品情報を取得するように ObjectDataSource を構成します。 このチュートリアルでは、を使用して挿入機能を追加するだけで、編集や削除について心配することはありません。 そのため、[挿入] タブのドロップダウンリストが `AddProduct()` に設定されていること、および [更新] タブと [削除] タブのドロップダウンリストが [(なし)] に設定されていることを確認してください。

[AddProduct メソッドを ObjectDataSource s Insert () メソッドにマップ ![には](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**図 3**: `AddProduct` メソッドを ObjectDataSource s `Insert()` メソッドにマップする ([クリックしてフルサイズのイメージを表示する](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png))

[[更新] タブと [タブの削除] ドロップダウンリストを [(なし)] に設定 ![](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**図 4**: [更新] タブと [タブの削除] ドロップダウンリストを [(なし)] に設定する ([クリックしてフルサイズのイメージを表示する](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))

ObjectDataSource s のデータソース構成ウィザードを完了すると、対応する各データフィールドの GridView にフィールドが自動的に追加されます。 ここでは、Visual Studio によって追加されたすべてのフィールドをそのまま使用します。 このチュートリアルの後の方で、新しいレコードを追加するときに値を指定する必要のないフィールドをいくつか削除します。

データベースには80製品が含まれているため、ユーザーは新しいレコードを追加するために、web ページの一番下までスクロールする必要があります。 そのため、を使用すると、挿入インターフェイスをより見やすく、アクセスしやすくすることができます。 ページングを有効にするには、GridView のスマートタグから [ページングを有効にする] チェックボックスをオンにします。

この時点で、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]

[すべての製品データフィールドがページングされた GridView に表示される ![](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**図 5**: すべての製品データフィールドがページングされた GridView に表示される ([クリックしてフルサイズの画像を表示する](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png))

## <a name="step-2-adding-a-footer-row"></a>手順 2: フッター行の追加

GridView には、ヘッダー行とデータ行と共に、フッター行が含まれています。 ヘッダーとフッターの行は、GridView の[`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx)と[`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx)プロパティの値に応じて表示されます。 フッター行を表示するには、単に `ShowFooter` プロパティを `True`に設定します。 図6に示すように、`ShowFooter` プロパティを `True` に設定すると、グリッドにフッター行が追加されます。

[フッター行を表示 ![には、ShowFooter を True に設定します。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**図 6**: フッター行を表示するには `ShowFooter` を `True` に設定します ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png)されます)

フッター行の背景色が濃い赤になっていることに注意してください。 これは、DataWebControls テーマが作成され、 [ObjectDataSource チュートリアルでデータを表示するとき](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)にすべてのページに適用されるためです。 具体的には、`GridView.skin` ファイルによって、`FooterStyle` CSS クラスを使用するように `FooterStyle` プロパティが構成されます。 `FooterStyle` クラスは、`Styles.css` で次のように定義されています。

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> 前のチュートリアルでは、GridView のフッター行を使用しました。 必要に応じて、「 [GridView のフッターチュートリアル」の概要情報を表示](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)して、リフレッシャーを参照してください。

`ShowFooter` プロパティを `True`に設定した後、出力をブラウザーに表示します。 現在、フッター行にはテキストまたは Web コントロールは含まれていません。 手順3では、適切な挿入インターフェイスが含まれるように、各 GridView フィールドのフッターを変更します。

[![、空のフッター行がページングインターフェイスコントロールの上に表示されます。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**図 7**: ページングインターフェイスコントロールの上に空のフッター行が表示される ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png)されます)

## <a name="step-3-customizing-the-footer-row"></a>手順 3: フッター行のカスタマイズ

[Gridview コントロールチュートリアルの「Using TemplateFields」 (templatefields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)または CheckBoxFields ではなく) templatefields を使用して特定の GridView 列の表示を大幅にカスタマイズする方法について説明しました。[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)については、「templatefields を使用して GridView の編集インターフェイスをカスタマイズする」を参照してください。 TemplateField は、特定の種類の行に使用されるマークアップ、Web コントロール、およびデータバインディング構文の組み合わせを定義する多数のテンプレートで構成されていることを思い出してください。 たとえば、`ItemTemplate`では、読み取り専用の行に使用するテンプレートを指定し、`EditItemTemplate` は編集可能な行のテンプレートを定義します。

TemplateField には、`ItemTemplate` と `EditItemTemplate`と共に、フッター行の内容を指定する `FooterTemplate` も含まれています。 そのため、各フィールドに必要な Web コントロールを `FooterTemplate`に追加できます。 開始するには、GridView のすべてのフィールドを TemplateFields に変換します。 これを行うには、GridView のスマートタグの [列の編集] リンクをクリックし、左下隅にある各フィールドを選択して、[このフィールドを TemplateField に変換する] リンクをクリックします。

![各フィールドを TemplateField に変換します。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**図 8**: 各フィールドを TemplateField に変換する

[このフィールドを TemplateField に変換] をクリックすると、現在のフィールドの種類が同等の TemplateField に変わります。 たとえば、各 BoundField は、対応するデータフィールドを表示するラベルを含む `ItemTemplate` の TemplateField と、データフィールドをテキストボックスに表示する `EditItemTemplate` に置き換えられます。 `ProductName` BoundField は、次の TemplateField マークアップに変換されました。

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

同様に、`Discontinued` CheckBoxField は、`ItemTemplate` と `EditItemTemplate` に CheckBox Web コントロールが含まれている TemplateField に変換されています (`ItemTemplate` のチェックボックスが無効になっています)。 読み取り専用 `ProductID` BoundField は、`ItemTemplate` と `EditItemTemplate`の両方でラベルコントロールを持つ TemplateField に変換されました。 つまり、既存の GridView フィールドを TemplateField に変換することは、既存のフィールドの機能を失うことなく、よりカスタマイズ可能な TemplateField に簡単に切り替えることができます。

この GridView では編集がサポートされていないため、各 TemplateField から `EditItemTemplate` を削除して、`ItemTemplate`だけを残しておきます。 この操作を行った後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

各 GridView フィールドが TemplateField に変換されたので、各 `FooterTemplate`フィールドに適切な挿入インターフェイスを入力できます。 一部のフィールドには、挿入インターフェイス (`ProductID`など) がありません。他のユーザーは、新しい製品の情報を収集するために使用される Web コントロールによって異なります。

編集インターフェイスを作成するには、GridView のスマートタグから [テンプレートの編集] リンクを選択します。 次に、ドロップダウンリストから適切なフィールド s `FooterTemplate` を選択し、ツールボックスから適切なコントロールをデザイナーにドラッグします。

[各フィールドのフッターテンプレートに適切な挿入インターフェイスを追加 ![](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**図 9**: 各フィールド `FooterTemplate` に適切な挿入インターフェイスを追加する ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png)されます)

次の箇条書きリストは、追加する挿入インターフェイスを指定して、GridView フィールドを列挙しています。

- `ProductID` なし。
- テキストボックスを追加 `ProductName`、その `ID` を `NewProductName`に設定します。 RequiredFieldValidator コントロールも追加して、ユーザーが新しい製品名の値を入力するようにします。
- `SupplierID` なし。
- `CategoryID` なし。
- テキストボックスを追加 `QuantityPerUnit`、その `ID` を `NewQuantityPerUnit`に設定します。
- `UnitPrice` `NewUnitPrice` という名前のテキストボックスと、入力した値が0以上の通貨値であることを確認する CompareValidator を追加します。
- `ID` が `NewUnitsInStock`に設定されているテキストボックスを使用 `UnitsInStock` ます。 入力した値が0以上の整数値であることを保証する CompareValidator を含めます。
- `ID` が `NewUnitsOnOrder`に設定されているテキストボックスを使用 `UnitsOnOrder` ます。 入力した値が0以上の整数値であることを保証する CompareValidator を含めます。
- `ID` が `NewReorderLevel`に設定されているテキストボックスを使用 `ReorderLevel` ます。 入力した値が0以上の整数値であることを保証する CompareValidator を含めます。
- チェックボックスを追加 `Discontinued`、その `ID` を `NewDiscontinued`に設定します。
- DropDownList を追加 `CategoryName`、その `ID` を `NewCategoryID`に設定します。 これを `CategoriesDataSource` という名前の新しい ObjectDataSource にバインドし、`CategoriesBLL` クラス s `GetCategories()` メソッドを使用するように構成します。 `CategoryID` データフィールドを値として使用して、DropDownList `ListItem` s に `CategoryName` データフィールドが表示されるようにします。
- DropDownList を追加 `SupplierName`、その `ID` を `NewSupplierID`に設定します。 これを `SuppliersDataSource` という名前の新しい ObjectDataSource にバインドし、`SuppliersBLL` クラス s `GetSuppliers()` メソッドを使用するように構成します。 `SupplierID` データフィールドを値として使用して、DropDownList `ListItem` s に `CompanyName` データフィールドが表示されるようにします。

各検証コントロールについて、`ForeColor` プロパティをオフにして、既定の赤の代わりに `FooterStyle` CSS クラス s の前景色が使用されるようにします。 また、`ErrorMessage` プロパティを使用して詳細な説明を行いますが、`Text` プロパティにはアスタリスクを設定します。 検証コントロールのテキストによって挿入インターフェイスが2行に折り返されないようにするには、検証コントロールを使用する各 `FooterTemplate` のに対して、`FooterStyle` s `Wrap` プロパティを false に設定します。 最後に、GridView の下に ValidationSummary コントロールを追加し、その `ShowMessageBox` プロパティを `True` に設定し、その `ShowSummary` プロパティを `False`に設定します。

新しい製品を追加する場合は、`CategoryID` と `SupplierID`を提供する必要があります。 この情報は、[`CategoryName`] フィールドと [`SupplierName`] フィールドのフッターセルにある [DropDownLists] によってキャプチャされます。 ここでは、これらのフィールドを `CategoryID` および `SupplierID` TemplateFields ではなく使用することを選択しました。これは、grid のデータ行では、ユーザーが ID 値ではなく、カテゴリ名と仕入先名を表示することに興味を持つ可能性が高いためです。 `CategoryID` と `SupplierID` の値は現在、`CategoryName` と `SupplierName` field の挿入インターフェイスでキャプチャされているため、GridView から `CategoryID` および `SupplierID` TemplateFields を削除できます。

同様に、`ProductID` は新しい製品を追加するときには使用されないため、`ProductID` TemplateField も削除できます。 ただし、では、グリッド内の `ProductID` フィールドをそのままにしておきます。 挿入インターフェイスを構成するテキストボックス、DropDownLists、Checkbox、および validation コントロールに加えて、[追加] ボタンも必要になります。このボタンは、クリックすると、新しい製品をデータベースに追加するロジックを実行します。 手順 4. で、`ProductID` TemplateField s `FooterTemplate`の [挿入] インターフェイスに [追加] ボタンを含めます。

さまざまな GridView フィールドの外観を向上させることができます。 たとえば、`UnitPrice` 値を通貨として書式設定し、`UnitsInStock`、`UnitsOnOrder`、および `ReorderLevel` の各フィールドを右揃えにして、TemplateFields の `HeaderText` 値を更新することができます。

`FooterTemplate` s にインターフェイスを挿入し、`SupplierID`、および `CategoryID` TemplateFields を削除した後、TemplateFields を書式設定して配置することでグリッドの外観を改善した後、GridView の宣言型のマークアップは次のようになります。

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

ブラウザーで表示すると、GridView のフッター行に、完成した挿入インターフェイスが含まれるようになりました (図10を参照)。 この時点で、挿入インターフェイスには、ユーザーが新しい製品のデータを入力し、データベースに新しいレコードを挿入することを示す手段が含まれていません。 また、フッターに入力したデータが `Products` データベースの新しいレコードに変換される方法についても説明します。 手順4では、[追加] ボタンを挿入インターフェイスに含める方法と、ポストバック時にコードをクリックしたときにコードを実行する方法について説明します。 手順5は、フッターのデータを使用して新しいレコードを挿入する方法を示しています。

[GridView フッターに ![新しいレコードを追加するためのインターフェイスが用意されています。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**図 10**: GridView フッターは、新しいレコードを追加するためのインターフェイスを提供します ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png)されます)

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>手順 4: 挿入インターフェイスに [追加] ボタンを含める

挿入インターフェイスのどこかに [追加] ボタンを含める必要があります。これは、フッター行の挿入インターフェイスには、現在、ユーザーが新しい製品情報の入力を完了したことを示す手段がないためです。 これは既存の `FooterTemplate` のいずれかに配置できます。または、この目的のために新しい列をグリッドに追加することもできます。 このチュートリアルでは、`ProductID` TemplateField s `FooterTemplate`に [追加] ボタンを配置します。

デザイナーで、GridView s スマートタグの [テンプレートの編集] リンクをクリックし、ドロップダウンリストから `ProductID` フィールド s `FooterTemplate` を選択します。 図11に示すように、テンプレートにボタン Web コントロール (または LinkButton または ImageButton) を追加し、その ID を `AddProduct`、挿入する `CommandName`、`Text` プロパティを追加します。

[ProductID TemplateField s フッターテンプレートに [追加] ボタンを配置 ![には](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**図 11**: `ProductID` TemplateField s `FooterTemplate` に [追加] ボタンを配置[する (クリックしてフルサイズの画像を表示する](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png))

[追加] ボタンをクリックした後、ブラウザーでページをテストします。 挿入インターフェイスに無効なデータが含まれている [追加] ボタンをクリックすると、ポストバックは短いサーキットになり、ValidationSummary コントロールは無効なデータを示します (図12を参照)。 適切なデータを入力したら、[追加] ボタンをクリックするとポストバックが発生します。 ただし、レコードはデータベースに追加されません。 実際に挿入を実行するには、少しコードを記述する必要があります。

[挿入インターフェイスに無効なデータが含まれている場合は、[Add] ボタン s ポストバック ![Short サーキット](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**図 12**: 挿入インターフェイスに無効なデータが含まれている場合は、[Add] ボタン s ポストバックが短いサーキット ([クリックすると、フルサイズの画像が表示](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png)されます)

> [!NOTE]
> 挿入インターフェイスの検証コントロールが検証グループに割り当てられませんでした。 これは、挿入インターフェイスがページ上の検証コントロールの唯一のセットである限り、問題なく動作します。 ただし、ページに他の検証コントロール (grid s 編集インターフェイスの検証コントロールなど) がある場合、[挿入インターフェイス] プロパティと [ボタンの追加] `ValidationGroup` プロパティの検証コントロールには、これらのコントロールを特定の検証グループに関連付けるために同じ値を割り当てる必要があります。 ページ上の検証コントロールとボタンを検証グループにパーティション分割する方法の詳細については[、「解説 The Validation controls in ASP.NET 2.0」](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)を参照してください。

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>手順 5:`Products`テーブルに新しいレコードを挿入する

GridView の組み込み編集機能を使用すると、更新プログラムの実行に必要なすべての作業が GridView によって自動的に処理されます。 特に、[更新] ボタンをクリックすると、編集インターフェイスから入力した値が ObjectDataSource s `UpdateParameters` コレクションのパラメーターにコピーされ、ObjectDataSource s `Update()` メソッドを呼び出すことで更新が開始されます。 GridView は挿入用のこのような組み込み機能を提供しないため、ObjectDataSource s `Insert()` メソッドを呼び出し、挿入インターフェイスから ObjectDataSource s `InsertParameters` コレクションに値をコピーするコードを実装する必要があります。

この挿入ロジックは、[追加] ボタンをクリックした後に実行する必要があります。 Gridview でのボタンの[追加と応答](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md)に関するチュートリアルで説明したように、Gridview のボタン、LinkButton、または ImageButton がクリックされると、gridview s `RowCommand` イベントがポストバック時に発生します。 このイベントは、ボタン、LinkButton、または ImageButton が、フッター行の [追加] ボタンなどの明示的に追加されたか、GridView によって自動的に追加されたか ([並べ替えを有効にする] が選択されている場合は、各列の上部にあるリンクボタンなど) を示します。[ページングを有効にする] が選択されているときのページングインターフェイスのリンクボタン。

したがって、[追加] ボタンをクリックしたユーザーに応答するには、GridView s `RowCommand` イベントのイベントハンドラーを作成する必要があります。 このイベントは、GridView*の Button、* LinkButton、または ImageButton がクリックされるたびに発生するため、イベントハンドラーに渡された `CommandName` プロパティが [追加] ボタン (Insert) の `CommandName` 値にマップされている場合にのみ、挿入ロジックを続行することが重要です。 さらに、検証コントロールが有効なデータを報告している場合にのみ処理を続行する必要もあります。 これに対応するには、次のコードを使用して、`RowCommand` イベントのイベントハンドラーを作成します。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> イベントハンドラーによって `Page.IsValid` プロパティがチェックされるのはなぜですか。 結局のところ、挿入インターフェイスに無効なデータが指定されている場合、ポストバックは抑制されますか。 この想定は、ユーザーが JavaScript を無効にしていない場合、またはクライアント側の検証ロジックを回避する手順を実行している場合に適しています。 つまり、クライアント側の検証に厳密に依存しないようにする必要があります。データを操作する前に、サーバー側の有効性チェックを常に実行する必要があります。

手順 1. では、`Insert()` メソッドが `ProductsBLL` クラス s `AddProduct` メソッドにマップされるように `ProductsDataSource` ObjectDataSource を作成しました。 新しいレコードを `Products` テーブルに挿入するには、単に ObjectDataSource s `Insert()` メソッドを呼び出します。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

`Insert()` メソッドが呼び出されたので、次は、挿入インターフェイスから `ProductsBLL` クラス s `AddProduct` メソッドに渡されるパラメーターに値をコピーします。 [挿入、更新、および削除のチュートリアルに関連するイベントの](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)確認については、ObjectDataSource s `Inserting` イベントを使用して行うことができます。 `Inserting` イベントでは、`Products` GridView s フッター行からコントロールをプログラムによって参照し、その値を `e.InputParameters` コレクションに割り当てる必要があります。 ユーザーが `ReorderLevel` テキストボックスを空白のままにするなどの値を省略した場合は、データベースに挿入される値を `NULL`するように指定する必要があります。 `AddProducts` メソッドは null 許容型データベースフィールドの null 許容型を受け入れるため、ユーザー入力が省略されている場合は、null 許容型を使用し、その値を `Nothing` に設定するだけです。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

`Inserting` イベントハンドラーが完了したので、GridView s フッター行を使用して `Products` データベーステーブルに新しいレコードを追加できます。 新しい製品をいくつか追加してみましょう。

## <a name="enhancing-and-customizing-the-add-operation"></a>追加操作の拡張とカスタマイズ

現時点では、[追加] ボタンをクリックすると、データベーステーブルに新しいレコードが追加されますが、レコードが正常に追加されたことを示す視覚的なフィードバックは提供されません。 理想的には、ラベル Web コントロールまたはクライアント側の警告ボックスは、挿入が正常に完了したことをユーザーに通知します。 この作業をリーダーの演習として残しておきます。

このチュートリアルで使用する GridView では、表示されている製品に並べ替え順序は適用されません。また、エンドユーザーはデータを並べ替えることもできません。 その結果、レコードは、データベース内の主キーフィールドによって並べ替えられます。 新しいレコードには、最後のレコードよりも大きい `ProductID` 値があるため、新しい製品が追加されるたびに、グリッドの最後に追加されます。 そのため、新しいレコードを追加した後に、GridView の最後のページにユーザーを自動的に送信することができます。 これを行うには、データを GridView にバインドした後、最後のページにユーザーを送信する必要があることを示すために、`RowCommand` イベントハンドラーで `ProductsDataSource.Insert()` の呼び出しの後に次のコード行を追加します。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` は、最初は `False`の値が割り当てられるページレベルのブール型変数です。 GridView s `DataBound` イベントハンドラーで `SendUserToLastPage` が false の場合、`PageIndex` プロパティが更新され、最後のページにユーザーが送信されます。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

`DataBound` イベントハンドラーで `PageIndex` プロパティが設定されている理由は (`RowCommand` イベントハンドラーではありません)、`RowCommand` イベントハンドラーが起動すると、新しいレコードが `Products` データベーステーブルに追加されていないためです。 したがって、`RowCommand` イベントハンドラーでは、最後のページインデックス (`PageCount - 1`) は、新しい製品が追加さ*れる前*の最後のページインデックスを表します。 追加される製品の大部分については、新しい製品を追加した後の最後のページインデックスは同じです。 ただし、追加された製品によって新しいページインデックスが作成された場合、`RowCommand` イベントハンドラーの `PageIndex` を誤って更新すると、新しい最後のページインデックスではなく、最後のページ (新しい製品を追加する前の最後のページインデックス) に移動します。 新しい製品が追加され、データがグリッドに再バインドされた後に `DataBound` イベントハンドラーが呼び出されるため、`PageIndex` プロパティを設定することによって、正しい最後のページインデックスを取得することがわかっています。

最後に、このチュートリアルで使用する GridView は、新しい製品を追加するために収集する必要があるフィールドの数が多いため、非常に広範囲にわたります。 この幅により、DetailsView s の垂直レイアウトが優先される場合があります。 少なくとも入力を収集することで、GridView の全体の幅を減らすことができます。 新しい製品を追加するときに、`UnitsOnOrder`、`UnitsInStock`、および `ReorderLevel` フィールドを収集する必要はないかもしれません。この場合、これらのフィールドは GridView から削除される可能性があります。

収集されるデータを調整するには、次の2つの方法のいずれかを使用します。

- `UnitsOnOrder`、`UnitsInStock`、および `ReorderLevel` の各フィールドの値を必要とする `AddProduct` メソッドを引き続き使用します。 `Inserting` イベントハンドラーで、挿入インターフェイスから削除されたこれらの入力に使用する、ハードコーディングされた既定値を指定します。
- `UnitsOnOrder`、`UnitsInStock`、および `ReorderLevel` の各フィールドの入力を受け付けない、`ProductsBLL` クラスの `AddProduct` メソッドの新しいオーバーロードを作成します。 次に、[ASP.NET] ページで、この新しいオーバーロードを使用するように ObjectDataSource を構成します。

どちらのオプションも同様に機能します。 これまでのチュートリアルでは、後者のオプションを使用して、`ProductsBLL` クラス s `UpdateProduct` メソッドに対して複数のオーバーロードを作成しました。

## <a name="summary"></a>まとめ

GridView には、DetailsView と FormView に含まれる組み込みの挿入機能がありませんが、挿入インターフェイスをフッター行に追加することができます。 GridView にフッター行を表示するには、単に `ShowFooter` プロパティを `True`に設定します。 フィールドを TemplateField に変換し、挿入インターフェイスを `FooterTemplate`に追加することで、フィールドごとにフッター行の内容をカスタマイズできます。 このチュートリアルで説明したように、`FooterTemplate` には、ボタン、テキストボックス、DropDownLists、チェックボックス、データドリブン Web コントロール (DropDownLists など) を設定するためのデータソースコントロール、および検証コントロールを含めることができます。 ユーザー入力を収集するためのコントロールと共に、Add Button、LinkButton、または ImageButton が必要です。

[追加] ボタンがクリックされると、ObjectDataSource s `Insert()` メソッドが呼び出され、挿入ワークフローが開始されます。 次に、ObjectDataSource は、構成された挿入メソッド (このチュートリアルでは `ProductsBLL` クラス s `AddProduct` メソッド) を呼び出します。 挿入メソッドを呼び出す前に、GridView の `InsertParameters` コレクションに対して、GridView s インターフェイスから値をコピーする必要があります。 これは、ObjectDataSource s `Inserting` イベントハンドラーの挿入インターフェイス Web コントロールをプログラムで参照することによって実現できます。

このチュートリアルでは、GridView の外観を拡張する方法について説明します。 次の一連のチュートリアルでは、画像、Pdf、Word 文書などのバイナリデータを操作する方法と、データ Web コントロールについて説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Bernadette Leigh でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](adding-a-gridview-column-of-checkboxes-vb.md)
