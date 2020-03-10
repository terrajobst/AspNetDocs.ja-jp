---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: データ変更インターフェイスをカスタマイズする (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、標準の TextBox コントロールと CheckBox コントロールを代替の ati... に置き換えることにより、編集可能な GridView のインターフェイスをカスタマイズする方法について説明します。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479254"
---
# <a name="customizing-the-data-modification-interface-vb"></a>データ変更インターフェイスをカスタマイズする (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe)または[PDF のダウンロード](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> このチュートリアルでは、標準の TextBox コントロールと CheckBox コントロールを別の入力 Web コントロールに置き換えることによって、編集可能な GridView のインターフェイスをカスタマイズする方法について説明します。

## <a name="introduction"></a>はじめに

GridView および DetailsView コントロールで使用される BoundFields と CheckBoxFields は、読み取り専用、編集可能、および挿入可能なインターフェイスをレンダリングする機能により、データの変更プロセスを簡略化します。 これらのインターフェイスは、追加の宣言マークアップやコードを追加しなくてもレンダリングできます。 ただし、BoundField と CheckBoxField のインターフェイスには、実際のシナリオで必要になることが多いカスタマイズはありません。 GridView または DetailsView で編集可能または挿入可能なインターフェイスをカスタマイズするには、代わりに TemplateField を使用する必要があります。

前の[チュートリアル](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)では、検証 Web コントロールを追加してデータ変更インターフェイスをカスタマイズする方法を説明しました。 このチュートリアルでは、実際のデータコレクション Web コントロールをカスタマイズする方法について説明します。その際、BoundField と CheckBoxField の標準の TextBox コントロールと CheckBox コントロールを別の入力 Web コントロールに置き換えます。 特に、製品名、カテゴリ、サプライヤー、および廃止状態を更新できるようにする編集可能な GridView をビルドします。 特定の行を編集するときに、category フィールドと supplier フィールドが DropDownLists として表示されます。これには、選択可能なカテゴリとサプライヤーのセットが含まれます。 さらに、CheckBoxField の既定のチェックボックスを、"Active" と "廃止" の2つのオプションを提供する RadioButtonList コントロールに置き換えます。

[GridView の編集インターフェイスに DropDownLists と Radiobutton が含まれる ![](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**図 1**: GridView の編集インターフェイスには、dropdownlists と Radiobutton が含まれています ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image3.png)されます)

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>手順 1: 適切な`UpdateProduct`オーバーロードの作成

このチュートリアルでは、製品の名前、カテゴリ、サプライヤー、および廃止状態の編集を許可する編集可能な GridView をビルドします。 このため、4つの製品値と `ProductID`を含む5つの入力パラメーターを受け入れる `UpdateProduct` オーバーロードが必要です。 以前のオーバーロードと同様に、次のようになります。

1. データベースから、指定した `ProductID`の製品情報を取得します。
2. `ProductName`、`CategoryID`、`SupplierID`、および `Discontinued` の各フィールドを更新します。
3. TableAdapter の `Update()` 方法を使用して、更新要求を DAL に送信します。

簡潔にするために、この特定のオーバーロードについては、成果物が廃止とマークされていることを保証するビジネスルールチェックを省略しましたが、供給業者が提供する唯一の製品ではありません。 自由に追加してください。または、理想的にはロジックを別のメソッドにリファクタリングしてください。

次のコードは、`ProductsBLL` クラスの新しい `UpdateProduct` オーバーロードを示しています。

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>手順 2: 編集可能な GridView を編集する

`UpdateProduct` のオーバーロードを追加したので、編集可能な GridView を作成できます。 `EditInsertDelete` フォルダーの [`CustomizedUI.aspx`] ページを開き、GridView コントロールをデザイナーに追加します。 次に、GridView のスマートタグから新しい ObjectDataSource を作成します。 `ProductBLL` クラスの `GetProducts()` メソッドを使用して製品情報を取得し、先ほど作成した `UpdateProduct` のオーバーロードを使用して製品データを更新するように ObjectDataSource を構成します。 [挿入] タブと [削除] タブで、ドロップダウンリストから [(なし)] を選択します。

[作成したばかりの UpdateProduct オーバーロードを使用するように ObjectDataSource を構成 ![](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**図 2**: 作成した `UpdateProduct` のオーバーロードを使用するように ObjectDataSource を構成する ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image6.png)されます)

データ変更のチュートリアルで説明したように、Visual Studio によって作成された ObjectDataSource の宣言型の構文では、`OldValuesParameterFormatString` プロパティが `original_{0}`に割り当てられます。 もちろん、これはビジネスロジック層では機能しません。メソッドでは、元の `ProductID` 値が渡されるとは限りません。 このため、前のチュートリアルで行ったように、このプロパティの割り当てを宣言構文から削除するか、またはこのプロパティの値を `{0}`に設定します。

この変更後、ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

`OldValuesParameterFormatString` プロパティが削除され、`UpdateProduct` のオーバーロードで想定される各入力パラメーターの `UpdateParameters` コレクションに `Parameter` があることに注意してください。

ObjectDataSource は、製品値のサブセットのみを更新するように構成されていますが、現在のところ、*すべて*の product フィールドが GridView に表示されています。 GridView を編集して、次のようにします。

- これには、`ProductName`、`SupplierName`、`CategoryName` BoundFields、および `Discontinued` CheckBoxField のみが含まれます。
- `Discontinued` CheckBoxField の前 (左側) に表示される `CategoryName` および `SupplierName` のフィールド
- `CategoryName` および `SupplierName` BoundFields ' `HeaderText` プロパティは、それぞれ "Category" と "Supplier" に設定されています。
- 編集サポートが有効になっています (GridView のスマートタグの [編集を有効にする] チェックボックスをオンにしてください)

これらの変更が完了すると、デザイナーは図3のようになります。これは、次に示す GridView の宣言構文と似ています。

[GridView から不要なフィールドを削除 ![には](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**図 3**: GridView から不要なフィールドを削除[する (クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image9.png)されます)

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

この時点で、GridView の読み取り専用動作は完了です。 データを表示すると、各製品が GridView の行としてレンダリングされ、製品名、カテゴリ、仕入先、および廃止された状態が表示されます。

[GridView の読み取り専用インターフェイスが完了 ![](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**図 4**: GridView の読み取り専用インターフェイスが完了しました ([クリックすると、フルサイズのイメージが表示](customizing-the-data-modification-interface-vb/_static/image12.png)されます)

> [!NOTE]
> [「データの挿入、更新、削除の概要](an-overview-of-inserting-updating-and-deleting-data-cs.md)」で説明したように、GridView のビューステートが有効になっていることが非常に重要です (既定の動作)。 GridView s `EnableViewState` プロパティを `false`に設定すると、同時実行ユーザーが誤ってレコードを削除または編集する危険性があります。 「警告: 詳細については[、編集または削除をサポートし、ビューステートが無効になっている ASP.NET 2.0 GridViews/DetailsView/formviews での同時実行の問題](http://scottonwriting.net/sowblog/posts/10054.aspx)」を参照してください。

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>手順 3: カテゴリおよびサプライヤー編集インターフェイスに DropDownList を使用する

`ProductsRow` オブジェクトには、`CategoryID`、`CategoryName`、`SupplierID`、および `SupplierName` の各プロパティが含まれていることを思い出してください。これらのプロパティは、`Products` データベーステーブルの実際の外部キー ID 値と、`Name` テーブルと `Categories` テーブルの対応する `Suppliers` 値を提供します。 `ProductRow`の `CategoryID` と `SupplierID` は両方とも読み取りと書き込みが可能ですが、`CategoryName` および `SupplierName` のプロパティは読み取り専用としてマークされています。

`CategoryName` および `SupplierName` プロパティの読み取り専用の状態により、対応する BoundFields の `ReadOnly` プロパティが `True`に設定されています。これにより、行の編集時にこれらの値が変更されるのを防ぐことができます。 `ReadOnly` プロパティを `False`に設定し、編集中に `CategoryName` および `SupplierName` BoundFields をテキストボックスとして表示することもできますが、このような方法では、`UpdateProduct` と `CategoryName` 入力を受け取る `SupplierName` のオーバーロードがないため、ユーザーが製品を更新しようとしたときに例外が発生します。 実際には、次の2つの理由により、このようなオーバーロードを作成する必要はありません。

- `Products` テーブルには、`SupplierName` または `CategoryName` のフィールドはありませんが、`SupplierID` および `CategoryID`ます。 そのため、メソッドには、参照テーブルの値ではなく、これらの特定の ID 値を渡す必要があります。
- 業者またはカテゴリの名前を入力するようユーザーに要求することは、ユーザーが使用可能なカテゴリとサプライヤー、および正しい綴りを知る必要があるため、理想的ではありません。

"仕入先" フィールドと "カテゴリ" フィールドには、"読み取り専用モード" の場合 (現時点では)、カテゴリと仕入先の名前が表示され、編集時には適用可能なオプションのドロップダウンリストが表示されます。 ドロップダウンリストを使用すると、エンドユーザーは、どのカテゴリやサプライヤーを選択できるかをすばやく確認して、より簡単に選択できるようにすることができます。

この動作を実現するには、`SupplierName` および `CategoryName` BoundFields を、`ItemTemplate` が `SupplierName` と `CategoryName` の値を出力し、使用可能なカテゴリとサプライヤーを一覧表示するために DropDownList コントロールを使用する TemplateFields に変換する必要があります。`EditItemTemplate`

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>`Categories`と`Suppliers`の DropDownLists を追加する

まず、GridView のスマートタグから [列の編集] リンクをクリックして、`SupplierName` と `CategoryName` BoundFields を TemplateFields に変換します。左下の一覧から BoundField を選択します。[このフィールドを TemplateField に変換する] リンクをクリックします。 変換プロセスでは、次の宣言構文に示すように、`ItemTemplate` と `EditItemTemplate`の両方を含む TemplateField が作成されます。

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

BoundField は読み取り専用としてマークされているため、`ItemTemplate` と `EditItemTemplate` には、`Text` プロパティが適用可能なデータフィールド (上記の構文では`CategoryName`) にバインドされているラベル Web コントロールが含まれています。 `EditItemTemplate`を変更して、ラベル Web コントロールを DropDownList コントロールに置き換える必要があります。

前のチュートリアルで見たように、テンプレートはデザイナーを使用して編集することも、宣言型の構文から直接編集することもできます。 デザイナーを使用して編集するには、GridView のスマートタグの [テンプレートの編集] リンクをクリックし、カテゴリフィールドの `EditItemTemplate`を操作するように選択します。 Label Web コントロールを削除し、dropdownlist コントロールに置き換えます。 DropDownList の ID プロパティを `Categories`に設定します。

[TexBox を ![削除して、EditItemTemplate に DropDownList を追加します。](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**図 5**: texbox を取り外して、`EditItemTemplate` に DropDownList を追加する ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image15.png)されます)

次に、使用可能なカテゴリで DropDownList にデータを入力する必要があります。 DropDownList のスマートタグから [データソースの選択] リンクをクリックし、`CategoriesDataSource`という名前の新しい ObjectDataSource を作成することを選択します。

[カテゴリデータソースという名前の新しい ObjectDataSource コントロールを作成 ![には](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**図 6**: `CategoriesDataSource` という名前の新しい ObjectDataSource コントロールを作成[する (クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image18.png)される)

この ObjectDataSource がすべてのカテゴリを返すようにするには、`CategoriesBLL` クラスの `GetCategories()` メソッドにバインドします。

[ObjectDataSource をカテゴリ Bll の GetCategories () メソッドにバインド ![](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**図 7**: `CategoriesBLL`の `GetCategories()` メソッドに ObjectDataSource をバインドする ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image21.png)されます)

最後に、DropDownList の設定を構成して、`CategoryName` フィールドが、値として使用される `CategoryID` フィールドと共に各 DropDownList `ListItem` に表示されるようにします。

[[区分項目] フィールドが表示され、CategoryID が値として使用されている ![](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**図 8**: `CategoryName` フィールドが表示され、`CategoryID` が値として使用されている ([クリックしてフルサイズの画像を表示する](customizing-the-data-modification-interface-vb/_static/image24.png))

これらの変更を加えた後、`CategoryName` TemplateField の `EditItemTemplate` の宣言型マークアップには、DropDownList と ObjectDataSource の両方が含まれます。

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> `EditItemTemplate` の DropDownList では、ビューステートが有効になっている必要があります。 まもなく、DropDownList の宣言構文にデータバインド構文を追加し、`Eval()` のようなデータバインドコマンドを追加します。 `Bind()` は、ビューステートが有効になっているコントロールでのみ表示できます。

次の手順を繰り返して、`SupplierName` TemplateField の `EditItemTemplate`に `Suppliers` という名前の DropDownList を追加します。 これには、DropDownList を `EditItemTemplate` に追加し、別の ObjectDataSource を作成する操作が含まれます。 ただし、`Suppliers` DropDownList の ObjectDataSource は、`SuppliersBLL` クラスの `GetSuppliers()` メソッドを呼び出すように構成されている必要があります。 さらに、DropDownList `Suppliers` を構成して `CompanyName` フィールドを表示し、`SupplierID` フィールドを `ListItem` s の値として使用します。

DropDownLists を2つの `EditItemTemplate` s に追加した後、ブラウザーでページを読み込み、Chef Anton の Cajun Seasoning 製品の [編集] ボタンをクリックします。 図9に示すように、製品のカテゴリと供給業者の列はドロップダウンリストとして表示され、使用可能なカテゴリおよび仕入先を選択できます。 ただし、両方のドロップダウンリストの*最初*の項目が既定で選択されていることに注意してください (カテゴリの飲み物とサプライヤーとしての風変わりな液体)。ただし、Chef Anton の Cajun Seasoning は、新しい Orleans Cajun Delights によって提供される Condiment です。

[既定では、ドロップダウンリストの最初の項目が選択されて ![](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**図 9**: 既定では、ドロップダウンリストの最初の項目が選択されています ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image27.png)されます)

さらに、[更新] をクリックすると、製品の `CategoryID` と `SupplierID` の値が `NULL`に設定されていることがわかります。 これらの望ましくない動作はどちらも、`EditItemTemplate` s の DropDownLists が基になる製品データのデータフィールドにバインドされていないために発生します。

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>`CategoryID`と`SupplierID`のデータフィールドへの DropDownLists のバインド

編集した製品の [カテゴリ] ドロップダウンリストと [仕入先] ボックスの一覧を適切な値に設定し、[更新] をクリックしたときにこれらの値を BLL の `UpdateProduct` メソッドに送り返すようにするには、`SelectedValue` のプロパティを、双方向のデータバインディングを使用して `CategoryID` および `SupplierID` データフィールドにバインドする必要があります `Categories` DropDownList でこれを実現するには、宣言構文に `SelectedValue='<%# Bind("CategoryID") %>'` を直接追加します。

または、デザイナーでテンプレートを編集し、DropDownList のスマートタグから [リンクの編集] リンクをクリックして、DropDownList の連結を設定することもできます。 次に、双方向のデータバインディングを使用して、`SelectedValue` プロパティが `CategoryID` フィールドにバインドされていることを示します (図10を参照)。 `SupplierID` データフィールドを `Suppliers` DropDownList にバインドするには、宣言またはデザイナーのいずれかのプロセスを繰り返します。

[双方向のデータバインディングを使用して、CategoryID を DropDownList の SelectedValue プロパティにバインド ![](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**図 10**: 双方向のデータバインディングを使用して、DropDownList の `SelectedValue` プロパティに `CategoryID` をバインドする ([クリックしてフルサイズのイメージを表示する](customizing-the-data-modification-interface-vb/_static/image30.png))

2つの DropDownLists の `SelectedValue` プロパティにバインドが適用されると、編集された製品の category 列と supplier 列には、既定で現在の製品の値が設定されます。 [更新] をクリックすると、選択したドロップダウンリスト項目の `CategoryID` と `SupplierID` の値が `UpdateProduct` メソッドに渡されます。 図11に、データバインドステートメントが追加された後のチュートリアルを示します。Chef Anton's Cajun Seasoning の選択したドロップダウンリスト項目が正しく Condiment、新しい Orleans Cajun Delights になっていることに注意してください。

[編集した製品の現在のカテゴリと仕入先の値が既定で選択されている ![](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**図 11**: 編集した製品の現在のカテゴリと仕入先の値が既定で選択されている ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image33.png)されます)

## <a name="handlingnullvalues"></a>`NULL`値の処理

`Products` テーブルの `CategoryID` 列と `SupplierID` 列は `NULL`できますが、`EditItemTemplate` 内の DropDownLists には、`NULL` 値を表すリスト項目が含まれていません。 これには、次の2つの影響があります。

- ユーザーは、インターフェイスを使用して、製品のカテゴリまたはサプライヤーを非`NULL` 値から `NULL` に変更することはできません
- 製品に `NULL` `CategoryID` または `SupplierID`がある場合、[編集] ボタンをクリックすると例外が発生します。 これは、`Bind()` ステートメントで `CategoryID` (または `SupplierID`) によって返される `NULL` 値が DropDownList の値にマップされないためです (DropDownList は、その `SelectedValue` プロパティがリスト項目のコレクションに*ない*値に設定されている場合に例外をスローします)。

`NULL` の `CategoryID` と `SupplierID` 値をサポートするには、`NULL` 値を表すために、各 DropDownList に別の `ListItem` を追加する必要があります。 DropDownList チュートリアルを[使用したマスター/詳細フィルター](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)では、追加の `ListItem` をデータバインドに追加する方法を説明しました。これには、dropdownlist の `AppendDataBoundItems` プロパティを `True` に設定し、追加の `ListItem`を手動で追加する必要があります。 前のチュートリアルでは、`-1`の `Value` を持つ `ListItem` を追加しました。 ただし、ASP.NET のデータバインドロジックによって、空の文字列が `NULL` 値に自動的に変換され、その逆も行われます。 したがって、このチュートリアルでは、`ListItem`の `Value` を空の文字列にする必要があります。

最初に、DropDownLists ' `AppendDataBoundItems` プロパティの両方を `True`に設定します。 次に、次の `<asp:ListItem>` 要素を各 DropDownList に追加して、`NULL` `ListItem` を追加します。これにより、宣言型のマークアップは次のようになります。

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

この `ListItem`のテキスト値として "(なし)" を使用することを選択しましたが、必要に応じて、これを空の文字列に変更することもできます。

> [!NOTE]
> 「DropDownList チュートリアルを*使用したマスター/詳細のフィルター処理*」で説明したように、`ListItem` s はデザイナーを使用して dropdownlist に追加できます。そのためには、プロパティウィンドウの dropdownlist の `Items` プロパティ (`ListItem` コレクションエディターが表示されます) をクリックします。 ただし、このチュートリアルの `NULL` `ListItem` は、宣言型の構文を使用して追加するようにしてください。 `ListItem` コレクションエディターを使用する場合、生成された宣言構文は、空の文字列を割り当てたときに、`Value` 設定を完全に省略して、`<asp:ListItem>(None)</asp:ListItem>`のような宣言型のマークアップを作成します。 これは無害に見えるかもしれませんが、missing 値を指定すると、DropDownList で `Text` プロパティ値が代わりに使用されます。 つまり、この `NULL` `ListItem` を選択すると、値 "(なし)" が `CategoryID`に割り当てられ、例外が発生します。 `Value=""`を明示的に設定することにより、`NULL` `ListItem` を選択したときに `NULL` 値が `CategoryID` に割り当てられます。

仕入先の DropDownList についても、これらの手順を繰り返します。

この追加の `ListItem`により、図12に示すように、編集インターフェイスは、製品の `CategoryID` と `SupplierID` のフィールドに `NULL` 値を割り当てることができるようになりました。

[[(なし)] を選択して、製品のカテゴリまたは仕入先に NULL 値を割り当てる ![ます。](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**図 12**: [(なし)] を選択して、製品のカテゴリまたは業者の `NULL` 値を割り当てる ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image36.png)される)

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>手順 4: 提供終了ステータスの Radiobutton を使用する

現在、製品の `Discontinued` データフィールドは CheckBoxField を使用して表現されています。これは、読み取り専用の行に対して無効なチェックボックスを表示し、編集されている行に対して [有効] チェックボックスを表示します。 このユーザーインターフェイスは多くの場合に適していますが、TemplateField を使用して必要に応じてカスタマイズすることもできます。 このチュートリアルでは、CheckBoxField を、ユーザーが製品の `Discontinued` 値を指定できる2つのオプション "Active" と "" を使用して、RadioButtonList コントロールを使用する TemplateField に変更してみましょう。

まず、`Discontinued` CheckBoxField を TemplateField に変換します。これにより、`ItemTemplate` と `EditItemTemplate`を持つ TemplateField が作成されます。 両方のテンプレートには、`Discontinued` データフィールドにバインドされた `Checked` プロパティを持つチェックボックスがありますが、`ItemTemplate`のチェックボックスの `Enabled` プロパティが `False`に設定されている2つの間の唯一の違いです。

`ItemTemplate` と `EditItemTemplate` の両方のチェックボックスを RadioButtonList コントロールに置き換え、両方の RadioButtonLists ' `ID` プロパティを `DiscontinuedChoice`に設定します。 次に、RadioButtonLists に2つのラジオボタンがあることを示します。1つは "Active" で、値が "False" で、もう1つは "" というラベルが付いています。 これを実現するには、宣言構文を使用して直接 `<asp:ListItem>` 要素を入力するか、デザイナーから `ListItem` コレクションエディターを使用します。 図13は、2つのオプションボタンオプションが指定された後の `ListItem` コレクションエディターを示しています。

[RadioButtonList にアクティブおよび廃止されたオプションを追加 ![には](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**図 13**: アクティブおよび廃止されたオプションを RadioButtonList に追加する ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image39.png)されます)

`ItemTemplate` の RadioButtonList は編集できないため、`Enabled` プロパティを `False`に設定し、`Enabled` プロパティを `True` の RadioButtonList の `EditItemTemplate`(既定値) のままにします。 これにより、編集されていない行のオプションボタンが読み取り専用になりますが、編集された行の RadioButton 値をユーザーが変更できるようになります。

また、製品の `Discontinued` データフィールドに基づいて適切なオプションボタンが選択されるように、RadioButtonList コントロールの `SelectedValue` プロパティを割り当てる必要もあります。 このチュートリアルで既に説明した DropDownLists と同様に、このデータバインド構文は、宣言型マークアップに直接追加することも、RadioButtonLists ' スマートタグの [データバインディングの編集] リンクを使用して追加することもできます。

2つの RadioButtonLists を追加して構成すると、`Discontinued` TemplateField の宣言型マークアップは次のようになります。

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

これらの変更により、`Discontinued` 列はチェックボックスの一覧からオプションボタンペアのリストに変換されました (図14を参照)。 製品を編集するときに、適切なラジオボタンが選択され、[その他] オプションボタンを選択して [更新] をクリックすると、製品の提供終了ステータスを更新できます。

[![廃止されたチェックボックスがラジオボタンのペアに置き換えられました](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**図 14**: 廃止されたチェックボックスがオプションボタンのペアに置き換えられました ([クリックすると、フルサイズの画像が表示](customizing-the-data-modification-interface-vb/_static/image42.png)されます)

> [!NOTE]
> `Products` データベースの `Discontinued` 列には `NULL` 値を設定できないため、インターフェイスでの `NULL` 情報のキャプチャについて心配する必要はありません。 ただし、`Discontinued` 列に `NULL` 値が含まれている可能性がある場合は、category および supplier DropDownLists と同じように、3番目のオプションボタンを一覧に追加し、その `Value` を空の文字列 (`Value=""`) に設定します。

## <a name="summary"></a>まとめ

BoundField と CheckBoxField は、読み取り専用、編集、および挿入の各インターフェイスを自動的に表示しますが、カスタマイズする機能はありません。 ただし、多くの場合、(前のチュートリアルで説明したように) 検証コントロールを追加したり、(このチュートリアルで説明したように) データコレクションユーザーインターフェイスをカスタマイズしたりして、編集または挿入インターフェイスをカスタマイズする必要があります。 TemplateField を使用してインターフェイスをカスタマイズするには、次の手順を実行します。

1. TemplateField を追加するか、既存の BoundField または CheckBoxField を TemplateField に変換します。
2. 必要に応じてインターフェイスを拡張します。
3. 双方向のデータバインディングを使用して、新しく追加した Web コントロールに適切なデータフィールドをバインドします。

組み込みの ASP.NET Web コントロールを使用するだけでなく、カスタム、コンパイル済みサーバーコントロール、およびユーザーコントロールを使用して、TemplateField のテンプレートをカスタマイズすることもできます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [次へ](implementing-optimistic-concurrency-vb.md)
