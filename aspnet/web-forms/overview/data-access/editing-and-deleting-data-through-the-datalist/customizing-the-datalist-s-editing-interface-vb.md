---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
title: DataList の編集インターフェイスをカスタマイズする (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、リストとチェックボックスを含む、DataList 用の豊富な編集インターフェイスを作成します。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 718628e2-224c-455f-b33a-a41efd48d5a0
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: adee419764cff2f39ee16962080c24b52553aa14
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637473"
---
# <a name="customizing-the-datalists-editing-interface-vb"></a>DataList の編集インターフェイスをカスタマイズする (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_VB.exe)または[PDF のダウンロード](customizing-the-datalist-s-editing-interface-vb/_static/datatutorial40vb1.pdf)

> このチュートリアルでは、リストとチェックボックスを含む、DataList 用の豊富な編集インターフェイスを作成します。

## <a name="introduction"></a>はじめに

DataList s `EditItemTemplate` のマークアップおよび Web コントロールは、その編集可能なインターフェイスを定義します。 これまでに確認したすべての編集可能な DataList の例では、編集可能なインターフェイスがテキストボックス Web コントロールで構成されています。 前の[チュートリアル](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)では、検証コントロールを追加して、編集時のユーザーエクスペリエンスを改善しました。

`EditItemTemplate` をさらに展開して、テキストボックス以外の Web コントロール (DropDownLists、RadioButtonLists、カレンダーなど) を含めることができます。 テキストボックスと同様に、編集インターフェイスをカスタマイズして他の Web コントロールを含める場合は、次の手順を実行します。

1. `EditItemTemplate`に Web コントロールを追加します。
2. 対応するデータフィールドの値を適切なプロパティに割り当てるには、databinding 構文を使用します。
3. `UpdateCommand` イベントハンドラーで、プログラムを使用して Web コントロールの値にアクセスし、適切な BLL メソッドに渡します。

このチュートリアルでは、リストとチェックボックスを含む、DataList 用の豊富な編集インターフェイスを作成します。 具体的には、製品情報を一覧表示し、製品名、供給業者、カテゴリ、および廃止された状態を更新することを許可する DataList を作成します (図1を参照)。

[編集インターフェイスには、テキストボックス、2つのドロップリスト、およびチェックボックスが含まれて ![ます。](customizing-the-datalist-s-editing-interface-vb/_static/image2.png)](customizing-the-datalist-s-editing-interface-vb/_static/image1.png)

**図 1**: 編集インターフェイスには、テキストボックス、2つのドロップリスト、およびチェックボックスがあります ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image3.png)されます)

## <a name="step-1-displaying-product-information"></a>手順 1: 製品情報の表示

DataList s 編集可能なインターフェイスを作成する前に、まず読み取り専用のインターフェイスを構築する必要があります。 まず、`EditDeleteDataList` フォルダーから [`CustomizedUI.aspx`] ページを開き、デザイナーからページに DataList を追加して、その `ID` プロパティを `Products`に設定します。 DataList s スマートタグから、新しい ObjectDataSource を作成します。 この新しい ObjectDataSource `ProductsDataSource` という名前を設定し、`ProductsBLL` クラス s `GetProducts` メソッドからデータを取得するように構成します。 前の編集可能な DataList チュートリアルと同様に、ビジネスロジックレイヤーに直接移動して、編集した製品の情報を更新します。 それに応じて、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![](customizing-the-datalist-s-editing-interface-vb/_static/image5.png)](customizing-the-datalist-s-editing-interface-vb/_static/image4.png)

**図 2**: [更新]、[挿入]、[削除] の各ドロップダウンリストを [(なし)] に設定します ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image6.png)されます)

ObjectDataSource を構成すると、Visual Studio によって、返される各データフィールドの名前と値を一覧表示する、DataList の既定の `ItemTemplate` が作成されます。 `ItemTemplate` を変更して、`<h4>` 要素内の製品名とカテゴリ名、仕入先名、価格、および廃止状態が一覧表示されるようにします。 さらに、[Edit] \ (編集 \) ボタンを追加して、`CommandName` プロパティが [編集] に設定されていることを確認します。 `ItemTemplate` の宣言型マークアップは次のとおりです。

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

上記のマークアップは、製品名の &lt;h4&gt; 見出しと、残りのフィールドの4列 `<table>` を使用して、製品情報をレイアウトします。 `Styles.css`で定義されている `ProductPropertyLabel` および `ProductPropertyValue` CSS クラスについては、前のチュートリアルで説明しました。 図3は、ブラウザーを使用して表示したときの進行状況を示しています。

[各製品の名前、供給業者、カテゴリ、廃止された状態、および価格を ![](customizing-the-datalist-s-editing-interface-vb/_static/image8.png)](customizing-the-datalist-s-editing-interface-vb/_static/image7.png)

**図 3**: 各製品の名前、仕入先、カテゴリ、廃止された状態、および価格が表示されます ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image9.png)されます)

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>手順 2: 編集インターフェイスに Web コントロールを追加する

カスタマイズされた DataList 編集インターフェイスを構築するための最初の手順は、必要な Web コントロールを `EditItemTemplate`に追加することです。 具体的には、カテゴリの DropDownList、業者の別の DropDownList、および廃止された状態のチェックボックスが必要です。 この例では、製品の価格は編集できないため、ラベル Web コントロールを使用して引き続き表示できます。

編集インターフェイスをカスタマイズするには、DataList s スマートタグの [テンプレートの編集] リンクをクリックし、ドロップダウンリストから [`EditItemTemplate`] オプションを選択します。 DropDownList を `EditItemTemplate` に追加し、その `ID` を `Categories`に設定します。

[カテゴリの DropDownList を追加 ![には](customizing-the-datalist-s-editing-interface-vb/_static/image11.png)](customizing-the-datalist-s-editing-interface-vb/_static/image10.png)

**図 4**: カテゴリの DropDownList を追加する ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image12.png)されます)

次に、DropDownList のスマートタグから [データソースの選択] オプションを選択し、`CategoriesDataSource`という名前の新しい ObjectDataSource を作成します。 この ObjectDataSource を `CategoriesBLL` クラス s `GetCategories()` メソッドを使用するように構成します (図5を参照)。 次に、DropDownList データソース構成ウィザードによって、各 `ListItem` s `Text` と `Value` プロパティに使用するデータフィールドを入力するよう求められます。 DropDownList に `CategoryName` データフィールドを表示し、図6に示すように `CategoryID` を値として使用します。

[新しい ObjectDataSource という名前の新しい名前のデータソースを作成 ![には](customizing-the-datalist-s-editing-interface-vb/_static/image14.png)](customizing-the-datalist-s-editing-interface-vb/_static/image13.png)

**図 5**: `CategoriesDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image15.png)される)

[DropDownList の表示フィールドと値フィールドを構成 ![には](customizing-the-datalist-s-editing-interface-vb/_static/image17.png)](customizing-the-datalist-s-editing-interface-vb/_static/image16.png)

**図 6**: DropDownList の表示フィールドと値フィールドを構成[する (クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image18.png)されます)

この一連の手順を繰り返して、サプライヤーの DropDownList を作成します。 この DropDownList の `ID` を `Suppliers` に設定し、ObjectDataSource `SuppliersDataSource`に名前を指定します。

2つの DropDownLists を追加した後、[生産中止] 状態のチェックボックスと製品名のテキストボックスを追加します。 チェックボックスとテキストボックスの `ID` をそれぞれ `Discontinued` と `ProductName`に設定します。 RequiredFieldValidator を追加して、ユーザーが製品名の値を確実に提供できるようにします。

最後に、[更新] ボタンと [キャンセル] ボタンを追加します。 これらの2つのボタンについては、`CommandName` プロパティをそれぞれ Update および Cancel に設定する必要があることに注意してください。

編集インターフェイスは自由に配置できます。 次の宣言型の構文とスクリーンショットに示すように、読み取り専用インターフェイスから同じ4列の `<table>` レイアウトを使用することを選択しました。

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample2.aspx)]

[編集インターフェイスが読み取り専用インターフェイスのようにレイアウトされて ![](customizing-the-datalist-s-editing-interface-vb/_static/image20.png)](customizing-the-datalist-s-editing-interface-vb/_static/image19.png)

**図 7**: 編集インターフェイスが読み取り専用インターフェイスのようにレイアウトされている ([クリックしてフルサイズのイメージを表示する](customizing-the-datalist-s-editing-interface-vb/_static/image21.png))

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>手順 3: EditCommand および CancelCommand イベントハンドラーの作成

現時点では、`EditItemTemplate` にはデータバインド構文がありません (ただし、`ItemTemplate`から逐語的にコピーされた `UnitPriceLabel`は除きます)。 ここでは、データバインド構文を一時的に追加しますが、まず、DataList s `EditCommand` イベントと `CancelCommand` イベントのイベントハンドラーを作成します。 `EditCommand` イベントハンドラーの役割は、[編集] ボタンがクリックされた DataList 項目の編集インターフェイスを表示することです。一方、`CancelCommand` のジョブは、DataList を編集前の状態に戻します。

これらの2つのイベントハンドラーを作成し、次のコードを使用します。

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample3.vb)]

これらの2つのイベントハンドラーが配置されている状態で、[編集] ボタンをクリックすると編集インターフェイスが表示され、[キャンセル] ボタンをクリックすると、編集した項目が読み取り専用モードに戻ります。 図8は、Chef Anton s Gumbo ミックスに対して [編集] ボタンがクリックされた後の DataList を示しています。 これまでに、編集インターフェイスにデータバインド構文を追加していたので、[`ProductName`] ボックスは空白になり、[`Discontinued`] チェックボックスがオフになっています。また、`Categories` と `Suppliers` DropDownLists から選択された最初の項目が選択されています。

[[編集] ボタンをクリック ![と、編集インターフェイスが表示されます。](customizing-the-datalist-s-editing-interface-vb/_static/image23.png)](customizing-the-datalist-s-editing-interface-vb/_static/image22.png)

**図 8**: [編集] ボタンをクリックすると編集インターフェイスが表示される ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image24.png)されます)

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>手順 4: 編集インターフェイスに DataBinding 構文を追加する

編集インターフェイスに現在の製品の値が表示されるようにするには、データフィールドの値を適切な Web コントロールの値に割り当てるためにデータバインド構文を使用する必要があります。 データバインド構文は、[テンプレートの編集] 画面に移動し、Web コントロールのスマートタグから [データバインディングの編集] リンクを選択すると、デザイナーを使用して適用できます。 または、データバインディング構文を宣言型マークアップに直接追加することもできます。

`ProductName` のデータフィールドの値を `ProductName` TextBox s `Text` プロパティに、`CategoryID` および `SupplierID` のデータフィールドの値を `Categories` および `Suppliers` の DropDownLists `SelectedValue` プロパティに、`Discontinued` data フィールドの値を `Discontinued` CheckBox s `Checked` プロパティに割り当てます。 デザイナーまたは宣言型マークアップを使用してこれらの変更を行った後、ブラウザーを使用してページを再度参照し、Chef Anton s Gumbo ミックスの [編集] ボタンをクリックします。 図9に示すように、databinding 構文では、TextBox、DropDownLists、および CheckBox に現在の値が追加されています。

[[編集] ボタンをクリック ![と、編集インターフェイスが表示されます。](customizing-the-datalist-s-editing-interface-vb/_static/image26.png)](customizing-the-datalist-s-editing-interface-vb/_static/image25.png)

**図 9**: [編集] ボタンをクリックすると編集インターフェイスが表示される ([クリックしてフルサイズの画像を表示する](customizing-the-datalist-s-editing-interface-vb/_static/image27.png))

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>手順 5: UpdateCommand イベントハンドラーでのユーザーの変更の保存

ユーザーが製品を編集して [更新] ボタンをクリックすると、ポストバックが発生し、DataList s `UpdateCommand` イベントが発生します。 イベントハンドラーでは、`EditItemTemplate` 内の Web コントロールから値を読み取って、BLL とインターフェイスを使用してデータベース内の製品を更新する必要があります。 前のチュートリアルで見たように、更新された製品の `ProductID` には、`DataKeys` コレクションからアクセスできます。 ユーザーが入力したフィールドにアクセスするには、次のコードに示すように、プログラムによって `FindControl("controlID")`を使用して Web コントロールを参照します。

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample4.vb)]

このコードでは、まず、`Page.IsValid` プロパティを調べて、ページ上のすべての検証コントロールが有効であることを確認します。 `Page.IsValid` が `True`場合は、編集した製品の `ProductID` 値が `DataKeys` コレクションから読み取られ、`EditItemTemplate` 内のデータ入力 Web コントロールがプログラムによって参照されます。 次に、これらの Web コントロールからの値が、適切な `UpdateProduct` オーバーロードに渡される変数に読み込まれます。 データを更新すると、DataList が編集前の状態に戻ります。

> [!NOTE]
> ここでは、 [BLL と DAL レベルの例外処理](handling-bll-and-dal-level-exceptions-vb.md)のチュートリアルで追加した例外処理ロジックを省略し、コードとこの例を中心にしています。 練習として、このチュートリアルを完了した後で、この機能を追加します。

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>手順 6: NULL の CategoryID および仕入先の値を処理する

Northwind データベースでは、`Products` テーブル s `CategoryID` および `SupplierID` 列に `NULL` 値を使用できます。 ただし、編集インターフェイスには現在 `NULL` 値が格納できません。 `CategoryID` または `SupplierID` 列のいずれかに `NULL` 値が含まれている製品を編集しようとすると `ArgumentOutOfRangeException`、"Categories" には SelectedValue があります。これ*は、項目の一覧に存在しないため無効*です。 また、現在、製品のカテゴリまたは供給業者の値を`NULL` 以外の値から `NULL` に変更することはできません。

Category および supplier DropDownLists の `NULL` 値をサポートするには、追加の `ListItem`を追加する必要があります。 この `ListItem`の `Text` 値として (None) を使用することを選択しましたが、必要に応じて別の値 (空の文字列など) に変更することもできます。 最後に、DropDownLists `AppendDataBoundItems` を `True`に設定することを忘れないでください。忘れた場合は、DropDownList にバインドされているカテゴリおよびサプライヤーが、静的に追加された `ListItem`を上書きします。

これらの変更を行った後、次のように、リスト内の `EditItemTemplate` のマークアップが表示されます。

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> 静的 `ListItem` s は、デザイナーを使用して DropDownList に追加することも、宣言型の構文を使用して直接追加することもできます。 データベース `NULL` 値を表す DropDownList 項目を追加する場合は、宣言型の構文を使用して `ListItem` を追加してください。 デザイナーで `ListItem` コレクションエディターを使用した場合、生成された宣言構文では、空の文字列を割り当てたときに、`Value` 設定を完全に省略して、`<asp:ListItem>(None)</asp:ListItem>`のような宣言型のマークアップを作成します。 これは無害に見えるかもしれませんが、不足している `Value` では、DropDownList で `Text` プロパティ値が代わりに使用されます。 つまり、この `NULL` `ListItem` を選択した場合、値 (None) が product data フィールド (このチュートリアルでは`CategoryID` または `SupplierID`) に割り当てられます。これにより、例外が発生します。 `Value=""`を明示的に設定することによって、`NULL` `ListItem` を選択したときに、`NULL` 値が product data フィールドに割り当てられます。

ブラウザーで進行状況を確認してください。 製品を編集するときに、`Categories` と `Suppliers` の DropDownLists の両方に、DropDownList の先頭に [(なし)] オプションがあることに注意してください。

[カテゴリおよび仕入先のドロップダウンリストに [(なし)] オプションが含まれている ![](customizing-the-datalist-s-editing-interface-vb/_static/image29.png)](customizing-the-datalist-s-editing-interface-vb/_static/image28.png)

**図 10**: `Categories` と `Suppliers` の dropdownlists には (None) オプションがあります ([クリックすると、フルサイズの画像が表示](customizing-the-datalist-s-editing-interface-vb/_static/image30.png)されます)

[(なし)] オプションをデータベース `NULL` 値として保存するには、`UpdateCommand` イベントハンドラーに戻る必要があります。 `categoryIDValue` および `supplierIDValue` 変数を null 許容の整数に変更し、DropDownList `SelectedValue` が空の文字列でない場合にのみ `Nothing` 以外の値を割り当てます。

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample6.vb)]

この変更により、`NULL` データベース値に対応するいずれかのドロップダウンリストからユーザーが [(なし)] オプションを選択した場合、`Nothing` の値が `UpdateProduct` BLL メソッドに渡されます。

## <a name="summary"></a>要約

このチュートリアルでは、3つの異なる入力 Web コントロール (TextBox)、2つの DropDownLists、および検証コントロールと共にチェックボックスを含む、より複雑な DataList 編集インターフェイスを作成する方法を説明しました。 編集インターフェイスを構築する場合、使用されている Web コントロールに関係なく、手順は同じです。まず、DataList s `EditItemTemplate`に Web コントロールを追加します。適切な Web コントロールプロパティを使用して、対応するデータフィールドの値を割り当てるには、databinding 構文を使用します。また、`UpdateCommand` イベントハンドラーでは、プログラムによって Web コントロールとそのプロパティにアクセスし、その値を BLL に渡します。

編集インターフェイスを作成するときに、テキストボックスだけで構成されているか、異なる Web コントロールのコレクションで構成されているかにかかわらず、データベース `NULL` の値を正しく処理するようにしてください。 `NULL` s をアカウンティングする場合は、編集インターフェイスに既存の `NULL` 値を正しく表示するだけでなく、値を `NULL`としてマークするための手段も提供する必要があります。 DataLists の DropDownLists の場合、これは通常、`Value` プロパティが明示的に空の文字列 (`Value=""`) に設定されている静的 `ListItem` を追加し、`NULL``ListItem` が選択されているかどうかを判断するために `UpdateCommand` イベントハンドラーにビットコードを追加することを意味します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Patterson が、David 氏 u、および Randy のようなものです。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
