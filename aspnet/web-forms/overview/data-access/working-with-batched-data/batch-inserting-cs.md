---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
title: バッチ挿入 (C#) |Microsoft Docs
author: rick-anderson
description: 1回の操作で複数のデータベースレコードを挿入する方法について説明します。 ユーザーインターフェイスレイヤーでは、GridView を拡張して、ユーザーが複数の n...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: cf025e08-48fc-4385-b176-8610aa7b5565
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
msc.type: authoredcontent
ms.openlocfilehash: 5dc4d0b6ac9bf3aa2baa54fe9f5d4149494e47d2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584764"
---
# <a name="batch-inserting-c"></a>一括挿入 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_CS.zip)または[PDF のダウンロード](batch-inserting-cs/_static/datatutorial66cs1.pdf)

> 1回の操作で複数のデータベースレコードを挿入する方法について説明します。 ユーザーインターフェイスレイヤーでは、GridView を拡張して、ユーザーが複数の新しいレコードを入力できるようにします。 データアクセス層では、トランザクション内で複数の挿入操作をラップして、すべての挿入が成功するか、すべての挿入がロールバックされるようにします。

## <a name="introduction"></a>はじめに

[バッチ更新](batch-updating-cs.md)のチュートリアルでは、GridView コントロールをカスタマイズして、複数のレコードが編集可能であるインターフェイスを表示する方法について説明しました。 ページにアクセスするユーザーは一連の変更を行い、ボタンを1回クリックするだけでバッチ更新を実行できます。 ユーザーが一般的に1つの移動で多くのレコードを更新する場合、このようなインターフェイスでは、[データの挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)について最初に調査した既定の行ごとの編集機能と比較して、多数のクリックとキーボードからマウスのコンテキストスイッチを保存できます。

この概念は、レコードを追加するときにも適用できます。 ここでは、Northwind Traders で、特定のカテゴリの製品が多数含まれているサプライヤーから出荷を受け取ることが多いとします。 例として、東京 Traders から6つの異なる紅茶とコーヒー製品の出荷を受けているとします。 ユーザーが DetailsView コントロールを使用して6つの製品を一度に1つずつ入力した場合、同じ値の多くを繰り返し選択する必要があります。同じカテゴリ (飲み物)、同じ業者 (東京 Traders)、および同じ廃止された値を選択する必要があります (False)、および注文の値 (0) に同じ単位が指定されています。 この反復的なデータ入力は、時間のかかるだけでなく、エラーが発生しやすくなります。

少し作業をして、ユーザーが仕入先とカテゴリを1回選択し、一連の製品名と単価を入力し、ボタンをクリックして新しい製品をデータベースに追加できるようにする、バッチ挿入インターフェイスを作成できます (図1を参照)。 各製品が追加されると、その `ProductName` および `UnitPrice` のデータフィールドにはテキストボックスに入力された値が割り当てられ、その `CategoryID` 値と `SupplierID` 値にはフォームの上部にある DropDownLists の値が割り当てられます。 `Discontinued` と `UnitsOnOrder` の値は、それぞれ `false` と0のハードコーディングされた値に設定されます。

[バッチ挿入インターフェイスの ![](batch-inserting-cs/_static/image2.png)](batch-inserting-cs/_static/image1.png)

**図 1**: バッチ挿入インターフェイス ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image3.png)されます)

このチュートリアルでは、図1に示すバッチ挿入インターフェイスを実装するページを作成します。 前の2つのチュートリアルと同様に、アトミック性を確保するために、トランザクションのスコープ内に挿入をラップします。 始めましょう!

## <a name="step-1-creating-the-display-interface"></a>手順 1: 表示インターフェイスを作成する

このチュートリアルは、表示領域と挿入領域という2つの領域に分割された1つのページで構成されます。 この手順で作成する display インターフェイスには、GridView の製品が表示され、[Process Product] (製品出荷のプロセス) というボタンが表示されます。 このボタンをクリックすると、図1に示すように、表示インターフェイスが挿入インターフェイスに置き換えられます。 [出荷からの製品の追加] または [キャンセル] ボタンをクリックすると、表示インターフェイスが戻ります。 ここでは、手順 2. で挿入インターフェイスを作成します。

2つのインターフェイスを持つページを作成するときに、そのうちの1つだけが一度に表示される場合、通常、各インターフェイスは、他のコントロールのコンテナーとして機能する[パネル Web コントロール](http://www.w3schools.com/aspnet/control_panel.asp)内に配置されます。 したがって、このページでは、インターフェイスごとに2つのパネルコントロールが表示されます。

まず、`BatchData` フォルダーの [`BatchInsert.aspx`] ページを開き、パネルをツールボックスからデザイナーにドラッグします (図2を参照)。 [Panel s `ID`] プロパティを `DisplayInterface`に設定します。 パネルをデザイナーに追加すると、`Height` プロパティと `Width` プロパティがそれぞれ50px と125px に設定されます。 これらのプロパティ値をプロパティウィンドウから削除します。

[パネルをツールボックスからデザイナーにドラッグ ![](batch-inserting-cs/_static/image5.png)](batch-inserting-cs/_static/image4.png)

**図 2**: パネルをツールボックスからデザイナーにドラッグする ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image6.png)されます)

次に、ボタンと GridView コントロールをパネルにドラッグします。 ボタン s `ID` プロパティを `ProcessShipment` に設定し、その `Text` プロパティを製品出荷を処理するように設定します。 GridView s `ID` プロパティを `ProductsGrid` に設定し、そのスマートタグから `ProductsDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLL` クラス s `GetProducts` メソッドからデータをプルするように ObjectDataSource を構成します。 この GridView はデータの表示にのみ使用されるため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。 [完了] をクリックして、データソースの構成ウィザードを完了します。

[製品の Bll クラス s GetProducts メソッドから返されたデータを表示 ![](batch-inserting-cs/_static/image8.png)](batch-inserting-cs/_static/image7.png)

**図 3**: `ProductsBLL` クラス s `GetProducts` メソッドから返されたデータを表示[する (クリックしてフルサイズの画像を表示する](batch-inserting-cs/_static/image9.png))

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](batch-inserting-cs/_static/image11.png)](batch-inserting-cs/_static/image10.png)

**図 4**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズのイメージを表示する](batch-inserting-cs/_static/image12.png))

ObjectDataSource ウィザードを完了すると、Visual Studio によって、BoundFields と product データフィールドの CheckBoxField が追加されます。 `ProductName`、`CategoryName`、`SupplierName`、`UnitPrice`、および `Discontinued` のフィールド以外はすべて削除します。 美しいカスタマイズを自由に行うことができます。 ここでは、`UnitPrice` フィールドを通貨値として書式設定し、フィールドを並べ替え、いくつかのフィールドの名前を `HeaderText` 値に変更することにしました。 また、gridview のスマートタグの [ページングを有効にし、並べ替えを有効にする] チェックボックスをオンにして、ページングと並べ替えのサポートを含むように GridView を構成します。

パネル、ボタン、GridView、ObjectDataSource の各コントロールを追加し、GridView のフィールドをカスタマイズすると、ページ s の宣言型マークアップは次のようになります。

[!code-aspx[Main](batch-inserting-cs/samples/sample1.aspx)]

ボタンと GridView のマークアップは、開始タグと終了タグの `<asp:Panel>` 内に表示されることに注意してください。 これらのコントロールは `DisplayInterface` パネル内にあるため、Panel s `Visible` プロパティを `false`に設定するだけで非表示にすることができます。 手順3では、ボタンクリックに応じてパネルの `Visible` プロパティをプログラムによって変更し、もう一方のインターフェイスを非表示にします。

ブラウザーで進行状況を確認してください。 図5に示すように、一度に10製品を一覧表示する GridView の上に、[Process Product 出荷] ボタンが表示されます。

[GridView によって製品が一覧表示され、並べ替えとページングの機能が提供さ ![](batch-inserting-cs/_static/image14.png)](batch-inserting-cs/_static/image13.png)

**図 5**: GridView に製品が一覧表示され、並べ替えとページングの機能が提供される ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image15.png)されます)

## <a name="step-2-creating-the-inserting-interface"></a>手順 2: 挿入インターフェイスの作成

Display インターフェイスが完成したら、挿入インターフェイスを作成する準備ができました。 このチュートリアルでは、1つの仕入先とカテゴリの値を要求する挿入インターフェイスを作成し、ユーザーが最大5つの製品名と単価の値を入力できるようにします。 このインターフェイスを使用すると、ユーザーは、同じカテゴリおよび仕入先を共有し、一意の製品名と価格を持つ5つの新しい製品に1つを追加できます。

まず、パネルをツールボックスからデザイナーにドラッグして、既存の `DisplayInterface` パネルの下に配置します。 新しく追加したこのパネルの [`ID`] プロパティを `InsertingInterface` に設定し、その `Visible` プロパティを [`false`] に設定します。 手順 3. で `true` に `InsertingInterface` Panel s `Visible` プロパティを設定するコードを追加します。 また、パネル s `Height` をオフにし、プロパティ値 `Width` します。

次に、図1に戻された挿入インターフェイスを作成する必要があります。 このインターフェイスは、さまざまな HTML 手法を使用して作成できますが、非常に簡単な方法として、4列の7行のテーブルを使用します。

> [!NOTE]
> HTML `<table>` 要素のマークアップを入力するときに、ソースビューを使用します。 Visual Studio には `<table>` 要素をデザイナーから追加するためのツールが用意されていますが、デザイナーでは、`style` 設定の unasked をマークアップに挿入する必要がありすぎないように見えます。 `<table>` マークアップを作成したら、通常はデザイナーに戻り、Web コントロールを追加し、そのプロパティを設定します。 事前に定義された列と行を含むテーブルを作成する場合は、[テーブル web コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx)ではなく静的な HTML を使用することをお勧めします。これは、テーブル web コントロール内に配置された web コントロールには `FindControl("controlID")` パターンを使用してのみアクセスできるためです。 ただし、テーブル web コントロールはプログラムによって構築できるため、動的にサイズ変更されたテーブル (行または列がデータベースまたはユーザー指定の条件に基づいているテーブル) にはテーブル Web コントロールを使用します。

`InsertingInterface` パネルの `<asp:Panel>` タグ内に次のマークアップを入力します。

[!code-html[Main](batch-inserting-cs/samples/sample2.html)]

この `<table>` マークアップには、まだ Web コントロールが含まれていません。これらを一時的に追加します。 各 `<tr>` 要素には、特定の CSS クラス設定が含まれていることに注意してください。これは、supplier リストと category DropDownLists が移動するヘッダー行の `BatchInsertHeaderRow` です。[出荷から製品を追加] および [キャンセル] ボタンが表示されるフッター行の `BatchInsertFooterRow`とは、product および unit price TextBox コントロールを含む行の `BatchInsertRow` と `BatchInsertAlternatingRow` の値を交互に表示します。 このチュートリアルで使用している GridView および DetailsView コントロールと同様の外観を挿入インターフェイスに与えるために、対応する CSS クラスを `Styles.css` ファイルに作成しました。 これらの CSS クラスを次に示します。

[!code-css[Main](batch-inserting-cs/samples/sample3.css)]

このマークアップを入力したら、デザインビューに戻ります。 図6に示すように、この `<table>` はデザイナーに4列の7行のテーブルとして表示されます。

[挿入インターフェイスは、4列の7行のテーブルで構成されて ![ます。](batch-inserting-cs/_static/image17.png)](batch-inserting-cs/_static/image16.png)

**図 6**: 挿入インターフェイスは、4列の7行のテーブルで構成されています ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image18.png)されます)

挿入インターフェイスに Web コントロールを追加する準備ができました。 ツールボックスから2つの DropDownLists をテーブル内の適切なセルにドラッグして、仕入先とカテゴリに1つずつドラッグします。

Supplier DropDownList `ID` プロパティを `Suppliers` に設定し、`SuppliersDataSource`という名前の新しい ObjectDataSource にバインドします。 新しい ObjectDataSource を `SuppliersBLL` クラス s `GetSuppliers` メソッドからデータを取得するように構成し、[更新] タブのドロップダウンリストを [(なし)] に設定します。 [完了] をクリックしてウィザードを終了します。

[SuppliersBLL Class s GetSuppliers メソッドを使用するように ObjectDataSource を構成 ![には](batch-inserting-cs/_static/image20.png)](batch-inserting-cs/_static/image19.png)

**図 7**: `SuppliersBLL` クラス s `GetSuppliers` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](batch-inserting-cs/_static/image21.png))

`Suppliers` DropDownList で `CompanyName` データフィールドを表示し、`SupplierID` データフィールドを `ListItem` s 値として使用します。

[![CompanyName データフィールドを表示し、値として [仕入先] を使用します。](batch-inserting-cs/_static/image23.png)](batch-inserting-cs/_static/image22.png)

**図 8**: `CompanyName` データフィールドを表示し、値として `SupplierID` を使用する ([クリックしてフルサイズの画像を表示する](batch-inserting-cs/_static/image24.png))

2番目の DropDownList `Categories` という名前を付け、`CategoriesDataSource`という名前の新しい ObjectDataSource にバインドします。 `CategoriesBLL` クラス s `GetCategories` メソッドを使用するように `CategoriesDataSource` ObjectDataSource を構成します。[更新] タブと [削除] タブのドロップダウンリストを (なし) に設定し、[完了] をクリックしてウィザードを完了します。 最後に、DropDownList に `CategoryName` データフィールドを表示させると共に、`CategoryID` を値として使用します。

これら2つの DropDownLists を追加し、適切に構成された ObjectDataSources ソースにバインドした後、画面は図9のようになります。

[ヘッダー行に [仕入先] と [カテゴリ] の DropDownLists が含まれるように ![](batch-inserting-cs/_static/image26.png)](batch-inserting-cs/_static/image25.png)

**図 9**: ヘッダー行に `Suppliers` と `Categories` の Dropdownlists が含まれるようになりました ([クリックしてフルサイズの画像を表示](batch-inserting-cs/_static/image27.png))

ここで、新しい製品の名前と価格を収集するためのテキストボックスを作成する必要があります。 5つの製品名と価格行のそれぞれについて、[ツールボックス] から [TextBox] コントロールをデザイナーにドラッグします。 テキストボックスの `ID` プロパティを `ProductName1`、`UnitPrice1`、`ProductName2`、`UnitPrice2`、`ProductName3`、`UnitPrice3`などに設定します。

各単価テキストボックスの後に CompareValidator を追加し、`ControlToValidate` プロパティを適切な `ID`に設定します。 また、`Operator` プロパティを `GreaterThanEqual`、`ValueToCompare` 0、および `Type` を `Currency`に設定します。 これらの設定は、入力された場合、価格が0以上の有効な通貨値であることを保証するように CompareValidator に指示します。 `Text` プロパティを \*に設定し、`ErrorMessage` には0以上の値を指定する必要があります。 また、通貨記号は省略してください。

> [!NOTE]
> `Products` データベーステーブルの `ProductName` フィールドで `NULL` 値が許可されていない場合でも、挿入インターフェイスには RequiredFieldValidator コントロールは含まれません。 これは、ユーザーが最大5つの製品を入力できるようにするためです。 たとえば、ユーザーが最初の3行の製品名と単価を入力し、最後の2行を空白のままにしている場合は、3つの新しい製品をシステムに追加するだけです。 ただし `ProductName` が必要であるため、対応する製品名の値が指定されているかどうかをプログラムによって確認する必要があります。 このチェックについては、手順 4. で説明します。

ユーザーの入力を検証するときに、値に通貨記号が含まれている場合、CompareValidator は無効なデータを報告します。 価格を入力するときに通貨記号を省略するようユーザーに指示する視覚的な合図として使用するために、各単価のテキストボックスの前に $ を追加します。

最後に、[`InsertingInterface`] パネルに [ValidationSummary] コントロールを追加し、`ShowMessageBox` プロパティを `true` に設定し、その `ShowSummary` プロパティを `false`に設定します。 これらの設定を使用すると、ユーザーが無効な単価の値を入力すると、問題のあるテキストボックスコントロールの横にアスタリスクが表示され、前に指定したエラーメッセージを表示するクライアント側のメッセージボックスが表示されます。

この時点で、画面は図10のようになります。

[挿入インターフェイスに製品名と価格のテキストボックスが含まれるようになった ![](batch-inserting-cs/_static/image29.png)](batch-inserting-cs/_static/image28.png)

**図 10**: 挿入インターフェイスに製品名と価格のテキストボックスが含まれるようになりました ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image30.png)されます)

次に、[出荷からの製品の追加] ボタンと [キャンセル] ボタンをフッター行に追加する必要があります。 ツールボックスから2つのボタンコントロールを挿入インターフェイスのフッターにドラッグし、ボタン `ID` プロパティを `CancelButton` `AddProducts` に設定し、プロパティを `Text` して、出荷から製品を追加したり、キャンセルしたりします。 さらに、`CancelButton` コントロール s `CausesValidation` プロパティを `false`に設定します。

最後に、2つのインターフェイスのステータスメッセージを表示する Label Web コントロールを追加する必要があります。 たとえば、ユーザーが製品の新しい出荷物を正常に追加した場合、表示インターフェイスに戻り、確認メッセージを表示します。 ただし、ユーザーが新しい製品の価格を指定し、製品名を残した場合は、`ProductName` フィールドが必須であるため、警告メッセージを表示する必要があります。 このメッセージは、両方のインターフェイスに表示する必要があるため、パネルの外側にあるページの上部に配置します。

[ツールボックス] から、デザイナーのページの上部にラベル Web コントロールをドラッグします。 `ID` プロパティを `StatusLabel`に設定し、`Text` プロパティをオフにして、`Visible` および `EnableViewState` のプロパティを `false`に設定します。 前のチュートリアルで見たように、[`EnableViewState`] プロパティを `false` に設定すると、ラベル s のプロパティ値をプログラムで変更し、後続のポストバック時に自動的に既定値に戻すことができます。 これにより、後続のポストバックで表示されなくなったユーザー操作に応答してステータスメッセージを表示するコードが簡単になります。 最後に、`StatusLabel` コントロール s `CssClass` プロパティを [警告] に設定します。これは、大きい、斜体、太字、赤のフォントでテキストを表示する、`Styles.css` で定義されている CSS クラスの名前です。

図11は、ラベルが追加および構成された後の Visual Studio デザイナーを示しています。

[StatusLabel コントロールを2つのパネルコントロールの上に配置 ![には](batch-inserting-cs/_static/image32.png)](batch-inserting-cs/_static/image31.png)

**図 11**: `StatusLabel` コントロールを2つのパネルコントロールの上[に配置する (クリックしてフルサイズのイメージを表示する](batch-inserting-cs/_static/image33.png))

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>手順 3: 表示インターフェイスと挿入インターフェイスの切り替え

この時点で、表示および挿入インターフェイスのマークアップが完了しましたが、次の2つのタスクが残っています。

- 表示インターフェイスと挿入インターフェイスの切り替え
- 出荷時の製品をデータベースに追加する

現在、表示インターフェイスは表示されていますが、挿入インターフェイスが非表示になっています。 これは、`DisplayInterface` Panel s `Visible` プロパティが `true` (既定値) に設定され、`InsertingInterface` Panel s `Visible` プロパティが `false`に設定されているためです。 2つのインターフェイスを切り替えるには、各コントロールの `Visible` プロパティ値を切り替えるだけです。

[Product 出荷の処理] ボタンがクリックされたときに、表示インターフェイスから挿入インターフェイスに移動します。 したがって、次のコードを含むこのボタン `Click` イベントのイベントハンドラーを作成します。

[!code-csharp[Main](batch-inserting-cs/samples/sample4.cs)]

このコードは、`DisplayInterface` パネルを非表示にして、`InsertingInterface` パネルを表示するだけです。

次に、挿入インターフェイスの [出荷からの製品の追加] および [キャンセル] ボタンコントロールのイベントハンドラーを作成します。 これらのボタンのいずれかをクリックすると、表示インターフェイスに戻す必要があります。 `ReturnToDisplayInterface`を呼び出すために、すぐに追加するメソッドである `Click` イベントハンドラーを作成します。 `ReturnToDisplayInterface` メソッドでは、[`InsertingInterface`] パネルを非表示にして `DisplayInterface` パネルを表示するだけでなく、Web コントロールを編集前の状態に戻す必要があります。 これには、DropDownLists `SelectedIndex` プロパティを0に設定し、TextBox コントロールの `Text` プロパティをクリアする作業が含まれます。

> [!NOTE]
> 表示インターフェイスに戻る前に、コントロールを編集前の状態に戻していない場合はどうなるかを検討してください。 ユーザーは、[製品出荷プロセス] ボタンをクリックし、出荷の製品を入力して、[出荷時の製品の追加] をクリックすることがあります。 これにより、製品が追加され、ユーザーが表示インターフェイスに返されます。 この時点で、ユーザーは別の出荷を追加することが必要になる場合があります。 [製品出荷の処理] ボタンをクリックすると、挿入インターフェイスに戻りますが、DropDownList の選択とテキストボックスの値には、前の値が設定されたままになります。

[!code-csharp[Main](batch-inserting-cs/samples/sample5.cs)]

どちらの `Click` イベントハンドラーも `ReturnToDisplayInterface` メソッドを呼び出しますが、手順 4. で [出荷から製品を追加] `Click` イベントハンドラーに戻り、製品を保存するコードを追加します。 `ReturnToDisplayInterface` は、`Suppliers` と `Categories` の DropDownLists を最初のオプションに返すことから始まります。 2つの定数 `firstControlID` および `lastControlID`、挿入インターフェイスの製品名と単価のテキストボックスに名前を付けるために使用される開始および終了の制御インデックス値をマークし、テキストボックスコントロールの `Text` プロパティを空の文字列に設定する `for` ループの境界内で使用されます。 最後に、挿入インターフェイスが非表示になり、表示インターフェイスが表示されるように、パネル `Visible` のプロパティがリセットされます。

ブラウザーでこのページをテストしてみましょう。 最初にページにアクセスしたときに、図5に示すように表示インターフェイスが表示されます。 [プロセスの製品出荷] ボタンをクリックします。 ページがポストバックされ、図12に示すように挿入インターフェイスが表示されるようになります。 [出荷からの製品の追加] または [キャンセル] ボタンのいずれかをクリックすると、表示インターフェイスに戻ります。

> [!NOTE]
> 挿入インターフェイスを表示しているときに、[単価] テキストボックスで CompareValidators をテストしてみましょう。 [出荷から商品を追加] ボタンをクリックすると、無効な通貨値または価格が0未満の値を持つクライアント側のメッセージボックス警告が表示されます。

[[プロセスの製品出荷] ボタンをクリックした後に挿入インターフェイスが表示される ![](batch-inserting-cs/_static/image35.png)](batch-inserting-cs/_static/image34.png)

**図 12**: [製品出荷プロセス] ボタンをクリックすると、[挿入] インターフェイスが表示されます ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image36.png)されます)

## <a name="step-4-adding-the-products"></a>手順 4: 製品を追加する

このチュートリアルでは、[出荷から製品を追加] ボタン `Click` イベントハンドラーで製品をデータベースに保存するだけです。 これを行うには、`ProductsDataTable` を作成し、提供された各製品名に対して `ProductsRow` インスタンスを追加します。 これらの `ProductsRow` が追加されたら、`ProductsDataTable`で渡される `ProductsBLL` クラス s `UpdateWithTransaction` メソッドを呼び出します。 「[トランザクション内のデータベースの変更のラップ](wrapping-database-modifications-within-a-transaction-cs.md)」チュートリアルで作成した `UpdateWithTransaction` メソッドが、`ProductsDataTable` を `ProductsTableAdapter` s `UpdateWithTransaction` メソッドに渡すことを思い出してください。 そこから、ADO.NET トランザクションが開始され、データテーブルに追加された各 `ProductsRow` について、TableAdapter が `INSERT` ステートメントをデータベースに発行します。 すべての製品がエラーなしで追加されると、トランザクションはコミットされ、それ以外の場合はロールバックされます。

また、[出荷時の製品の追加] ボタン `Click` イベントハンドラーのコードでは、いくつかのエラーチェックも実行する必要があります。 挿入インターフェイスで使用されている RequiredFieldValidators がないため、ユーザーは製品の価格を入力しても名前を省略できます。 製品名は必須であるため、このような条件が上ば、ユーザーに警告し、挿入を続行する必要がありません。 `Click` イベントハンドラーの完全なコードは次のとおりです。

[!code-csharp[Main](batch-inserting-cs/samples/sample6.cs)]

イベントハンドラーは、`Page.IsValid` プロパティが `true`の値を返すことを保証することによって開始されます。 `false`が返された場合、1つ以上の CompareValidators が無効なデータを報告していることを意味します。このような場合は、入力した製品を挿入しようとしないか、または、ユーザーが入力した単価の値を `ProductsRow` s `UnitPrice` プロパティに割り当てようとしたときに例外が発生します。

次に、新しい `ProductsDataTable` インスタンスを作成します (`products`)。 `for` ループは、製品名と単価のテキストボックスを反復処理するために使用され、`Text` のプロパティは `productName` と `unitPrice`のローカル変数に読み込まれます。 ユーザーが、対応する製品名ではなく単価の値を入力した場合、単価を指定すると、`StatusLabel` にメッセージが表示されます。製品の名前も含めて、イベントハンドラーを終了する必要があります。

製品名が指定されている場合は、`ProductsDataTable` s `NewProductsRow` メソッドを使用して新しい `ProductsRow` インスタンスが作成されます。 この新しい `ProductsRow` instance s `ProductName` プロパティは、[現在の製品名] テキストボックスに設定されますが、`SupplierID` プロパティと `CategoryID` プロパティは、[挿入] interface s ヘッダーの DropDownLists の `SelectedValue` プロパティに割り当てられます。 ユーザーが製品の価格の値を入力した場合は、`ProductsRow` instance s `UnitPrice` プロパティに割り当てられます。それ以外の場合、プロパティは未割り当てのままになり、データベース内の `UnitPrice` の `NULL` 値になります。 最後に、`Discontinued` と `UnitsOnOrder` の各プロパティは、ハードコーディングされた値 `false` と0にそれぞれ割り当てられます。

`ProductsRow` インスタンスにプロパティが割り当てられると、`ProductsDataTable`に追加されます。

`for` ループが完了したら、製品が追加されているかどうかを確認します。 すべてのユーザーが製品名または価格を入力する前に、[出荷から製品を追加] をクリックしている可能性があります。 `ProductsDataTable`に少なくとも1つの製品がある場合は、`ProductsBLL` クラス s `UpdateWithTransaction` メソッドが呼び出されます。 次に、新しく追加した製品が表示インターフェイスに表示されるように、データが `ProductsGrid` GridView に再バインドされます。 `StatusLabel` が更新され、確認メッセージが表示され、`ReturnToDisplayInterface` が呼び出され、挿入インターフェイスが非表示になり、表示インターフェイスが表示されます。

商品が入力されていない場合、挿入インターフェイスは表示されたままですが、"製品が追加されていません。 テキストボックスに製品名と単価を入力してください。

図 s 13、14、および15は、挿入と表示のインターフェイスが動作していることを示しています。 図13では、ユーザーは、対応する製品名を指定せずに単価の値を入力しました。 図14は、3つの新しい製品が正常に追加された後の表示インターフェイスを示しています。図15は、新しく追加された2つの製品を GridView に示しています (3 番目の製品は前のページにあります)。

[単価を入力するときに製品名が必要 ![](batch-inserting-cs/_static/image38.png)](batch-inserting-cs/_static/image37.png)

**図 13**: 単価を入力するときに製品名が必要である ([クリックしてフルサイズの画像を表示する](batch-inserting-cs/_static/image39.png))

[![業者に対して3つの新しい Veggies が追加されました。](batch-inserting-cs/_static/image41.png)](batch-inserting-cs/_static/image40.png)

**図 14**: Supplier i s の新しい Veggies が3つ追加されました ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image42.png)されます)

[新しい製品が GridView の最後のページにある ![](batch-inserting-cs/_static/image44.png)](batch-inserting-cs/_static/image43.png)

**図 15**: GridView の最後のページに新しい製品があります ([クリックすると、フルサイズの画像が表示](batch-inserting-cs/_static/image45.png)されます)。

> [!NOTE]
> このチュートリアルで使用するバッチ挿入ロジックでは、トランザクションのスコープ内で挿入をラップします。 これを確認するには、データベースレベルのエラーを意図的に導入します。 たとえば、新しい `ProductsRow` インスタンスの `CategoryID` プロパティを `Categories` DropDownList で選択されている値に割り当てるのではなく、`i * 5`などの値に割り当てます。 ここで `i` はループインデクサーで、1 ~ 5 の範囲の値を持ちます。 したがって、バッチ挿入に2つ以上の製品を追加する場合、最初の製品には有効な `CategoryID` 値 (5) が設定されますが、それ以降の製品では、`Categories` テーブルの値 `CategoryID` に一致しない値が `CategoryID` されます。 実質的には、最初の `INSERT` は成功しますが、それ以降は外部キー制約違反で失敗します。 バッチ挿入はアトミックであるため、最初の `INSERT` がロールバックされ、バッチ挿入プロセスが開始される前にデータベースがその状態に戻ります。

## <a name="summary"></a>要約

このチュートリアルと前の2つのチュートリアルでは、データのバッチの更新、削除、および挿入を可能にするインターフェイスを作成しました。トランザクションを使用する場合は、[トランザクション内でデータベースをラップ](wrapping-database-modifications-within-a-transaction-cs.md)することで、データアクセス層に追加しました。 特定のシナリオでは、このようなバッチ処理のユーザーインターフェイスを使用すると、基になるデータの整合性を維持しながら、クリック、ポストバック、キーボードからマウスへのコンテキストスイッチの数を減らすことで、エンドユーザーの効率を大幅に向上させることができます。

このチュートリアルでは、バッチ処理されたデータの使用方法について説明します。 次の一連のチュートリアルでは、TableAdapter のメソッドでのストアドプロシージャの使用、DAL での接続とコマンドレベルの設定の構成、接続文字列の暗号化など、高度なデータアクセス層のさまざまなシナリオについて説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow と S ren Jacob Lauritsen でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](batch-deleting-cs.md)
> [次へ](wrapping-database-modifications-within-a-transaction-vb.md)
