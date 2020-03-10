---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
title: バッチ更新の実行C#() |Microsoft Docs
author: rick-anderson
description: 完全に編集可能な DataList を作成する方法について説明します。すべての項目が編集モードであり、値を保存するには、[すべて更新] ボタンをクリックします。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 57743ca7-5695-4e07-aed1-44b297f245a9
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
msc.type: authoredcontent
ms.openlocfilehash: cde12a4d24555216adc49dd02818901278932eaa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480046"
---
# <a name="performing-batch-updates-c"></a>バッチ更新を実行する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_CS.exe)または[PDF のダウンロード](performing-batch-updates-cs/_static/datatutorial37cs1.pdf)

> すべての項目が編集モードで、ページの [すべて更新] ボタンをクリックして値を保存できる、完全に編集可能な DataList を作成する方法について説明します。

## <a name="introduction"></a>はじめに

前の[チュートリアル](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)では、項目レベルの DataList を作成する方法を説明しています。 標準の編集可能な GridView と同様に、DataList の各項目には [編集] ボタンが含まれています。このボタンをクリックすると、項目が編集可能になります。 この項目レベルの編集は、ときどき更新されるデータに対しては有効ですが、特定のユースケースシナリオでは、ユーザーが多くのレコードを編集する必要があります。 ユーザーが多数のレコードを編集する必要があり、[編集] をクリックし、変更を加えて、それぞれの [更新] をクリックする必要がある場合は、クリックすると、その生産性が低下する可能性があります。 このような状況では、完全に編集可能な DataList を指定することをお勧めします。これは、*すべて*の項目が編集モードであり、ページ上の [すべて更新] ボタンをクリックして値を編集できる、というものです (図1を参照)。

[完全に編集可能な DataList の各項目を変更できる ![](performing-batch-updates-cs/_static/image2.png)](performing-batch-updates-cs/_static/image1.png)

**図 1**: 完全に編集可能な DataList の各項目を変更することができます ([クリックすると、フルサイズのイメージが表示](performing-batch-updates-cs/_static/image3.png)されます)

このチュートリアルでは、ユーザーが完全に編集可能な DataList を使用して仕入先の住所情報を更新できるようにする方法について説明します。

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>手順 1: DataList s ItemTemplate で編集可能なユーザーインターフェイスを作成する

前のチュートリアルでは、標準の項目レベルの編集可能な DataList を作成し、次の2つのテンプレートを使用しています。

- `ItemTemplate` には、読み取り専用のユーザーインターフェイス (各製品の名前と価格を表示するためのラベル Web コントロール) が含まれています。
- `EditItemTemplate` には、編集モードのユーザーインターフェイスが含まれています (2 つの TextBox Web コントロール)。

DataList s `EditItemIndex` プロパティは、`EditItemTemplate`を使用して表示される `DataListItem` (存在する場合) を決定します。 特に、`ItemIndex` 値が DataList s `EditItemIndex` プロパティと一致する `DataListItem` は、`EditItemTemplate`を使用して表示されます。 このモデルは、一度に1つの項目しか編集できない場合に適していますが、完全に編集可能な DataList を作成するときには区別されません。

完全に編集可能な DataList の場合は、*すべて*の `DataListItem` が編集可能なインターフェイスを使用して表示されます。 これを実現する最も簡単な方法は、`ItemTemplate`で編集可能なインターフェイスを定義することです。 仕入先の住所情報を変更するために、編集可能なインターフェイスには業者名がテキストとして含まれており、住所、市区町村、および国の値のテキストボックスが表示されます。

まず、`BatchUpdate.aspx` ページを開き、DataList コントロールを追加して、その `ID` プロパティを `Suppliers`に設定します。 DataList s スマートタグから、`SuppliersDataSource`という名前の新しい ObjectDataSource コントロールを追加することを選択します。

[SuppliersDataSource という名前の新しい ObjectDataSource を作成 ![には](performing-batch-updates-cs/_static/image5.png)](performing-batch-updates-cs/_static/image4.png)

**図 2**: `SuppliersDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](performing-batch-updates-cs/_static/image6.png)される)

`SuppliersBLL` クラス s `GetSuppliers()` メソッドを使用してデータを取得するように ObjectDataSource を構成します (図3を参照)。 前のチュートリアルと同様に、ObjectDataSource を通じて supplier 情報を更新するのではなく、ビジネスロジックレイヤーを直接操作します。 そのため、[更新] タブで、ドロップダウンリストを [(なし)] に設定します (図4を参照)。

[GetSuppliers () メソッドを使用して業者情報を取得 ![には](performing-batch-updates-cs/_static/image8.png)](performing-batch-updates-cs/_static/image7.png)

**図 3**: `GetSuppliers()` メソッドを使用して業者情報を取得[する (クリックしてフルサイズのイメージを表示](performing-batch-updates-cs/_static/image9.png))

[[更新] タブで、ドロップダウンリストを [(なし)] に設定 ![ます。](performing-batch-updates-cs/_static/image11.png)](performing-batch-updates-cs/_static/image10.png)

**図 4**: [更新] タブでドロップダウンリストを (なし) に設定する ([クリックすると、フルサイズの画像が表示](performing-batch-updates-cs/_static/image12.png)されます)

ウィザードを完了すると、Visual Studio によって自動的に DataList s `ItemTemplate` が生成され、データソースから返された各データフィールドがラベル Web コントロールに表示されます。 代わりに編集インターフェイスを提供するように、このテンプレートを変更する必要があります。 `ItemTemplate` は、デザイナーを使用して、DataList s スマートタグの [テンプレートの編集] オプションを使用してカスタマイズすることも、宣言型の構文から直接カスタマイズすることもできます。

業者の名前をテキストとして表示する編集インターフェイスを作成しますが、仕入先の住所、市区町村、国の値のテキストボックスが含まれています。 これらの変更を行った後、ページの宣言構文は次のようになります。

[!code-aspx[Main](performing-batch-updates-cs/samples/sample1.aspx)]

> [!NOTE]
> 前のチュートリアルと同様に、このチュートリアルの DataList ではビューステートが有効になっている必要があります。

`ItemTemplate` は、2つの新しい CSS クラスを使用しています。 `SupplierPropertyLabel` と `SupplierPropertyValue`は、`Styles.css` クラスに追加され、`ProductPropertyLabel` および `ProductPropertyValue` CSS クラスと同じスタイル設定を使用するように構成されています。

[!code-css[Main](performing-batch-updates-cs/samples/sample2.css)]

これらの変更を行った後、ブラウザーを使用してこのページにアクセスします。 図5に示すように、各 DataList 項目は、仕入先名をテキストとして表示し、テキストボックスを使用して住所、市区町村、および国を表示します。

[DataList 内の各サプライヤーが編集可能で ![](performing-batch-updates-cs/_static/image14.png)](performing-batch-updates-cs/_static/image13.png)

**図 5**: DataList の各仕入先は編集可能です ([クリックすると、フルサイズの画像が表示](performing-batch-updates-cs/_static/image15.png)されます)

## <a name="step-2-adding-an-update-all-button"></a>手順 2: [すべて更新] ボタンを追加する

図5の各仕入先には、住所、市区町村、および国のフィールドがテキストボックスに表示されていますが、現在は [更新] ボタンがありません。 アイテムごとに更新ボタンを使用するのではなく、完全に編集可能な DataLists を使用すると、通常、ページの [すべて更新] ボタンがあります。このボタンをクリックすると、DataList 内の*すべて*のレコードが更新されます。 このチュートリアルでは、2つの [すべての更新] ボタン (ページの上部と下部に1つ) を追加します (いずれかのボタンをクリックしても同じ効果が得られます)。

まず、DataList の上に Button Web コントロールを追加し、その `ID` プロパティを `UpdateAll1`に設定します。 次に、DataList の下に2番目のボタン Web コントロールを追加し、その `ID` を `UpdateAll2`に設定します。 2つのボタンの `Text` プロパティを [すべて更新] に設定します。 最後に、両方のボタン `Click` イベントのイベントハンドラーを作成します。 各イベントハンドラーで更新ロジックを複製するのではなく、を3番目のメソッド (`UpdateAllSupplierAddresses`) にリファクタリングし、この3番目のメソッドを呼び出すだけでイベントハンドラーを使用します。

[!code-csharp[Main](performing-batch-updates-cs/samples/sample3.cs)]

図6は、[すべて更新] ボタンが追加された後のページを示しています。

[![2 つの更新プログラムのすべてのボタンがページに追加されました](performing-batch-updates-cs/_static/image17.png)](performing-batch-updates-cs/_static/image16.png)

**図 6**: [すべての更新] ボタンがページに追加されました ([クリックすると、フルサイズの画像が表示](performing-batch-updates-cs/_static/image18.png)されます)

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>手順 3: すべての仕入先の住所情報を更新する

すべての DataList 項目で編集インターフェイスを表示し、[すべて更新] ボタンを追加すると、残っているのはバッチ更新を実行するコードを記述することだけです。 具体的には、DataList s 項目をループ処理し、それぞれに対して `SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドを呼び出す必要があります。

DataList を設定する `DataListItem` インスタンスのコレクションには、DataList s [`Items` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)を使用してアクセスできます。 `DataListItem`への参照を使用して、次のコードに示すように、`DataKeys` コレクションから対応する `SupplierID` を取得し、プログラムによって `ItemTemplate` 内の TextBox Web コントロールを参照することができます。

[!code-csharp[Main](performing-batch-updates-cs/samples/sample4.cs)]

[すべて更新] ボタンのいずれかをクリックすると、`UpdateAllSupplierAddresses` メソッドは、`Suppliers` DataList 内の各 `DataListItem` を反復処理し、対応する値を渡して `SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドを呼び出します。 住所、都市、または国のパスに対して入力されていない値は、(空白の文字列ではなく) `UpdateSupplierAddress` する `Nothing` の値です。これにより、基になるレコードのフィールドに対してデータベース `NULL` が生成されます。

> [!NOTE]
> 拡張機能として、バッチ更新の実行後に確認メッセージが表示されるページに、ステータスラベル Web コントロールを追加することができます。

## <a name="updating-only-those-addresses-that-have-been-modified"></a>変更されたアドレスのみを更新する

このチュートリアルで使用するバッチ更新アルゴリズムでは、そのアドレス情報が変更されているかどうかにかかわらず、DataList 内の*すべて*の業者に対して `UpdateSupplierAddress` メソッドを呼び出します。 このようなブラインド更新は、通常はパフォーマンス上の問題ではありませんが、データベーステーブルへの変更を監査すると、余分なレコードが生じる可能性があります。 たとえば、トリガーを使用して、すべての `UPDATE` を `Suppliers` テーブルに記録する場合は、ユーザーが [すべて更新] ボタンをクリックするたびに、ユーザーが変更を行ったかどうかに関係なく、システム内の各業者に対して新しい監査レコードが作成されます。

ADO.NET DataTable および DataAdapter クラスはバッチ更新をサポートするように設計されており、変更、削除、および新しいレコードだけがデータベース通信になります。 DataTable 内の各行には、行が DataTable に追加されているか、削除されたか、変更されたか、または変更されていないかを示す[`RowState` プロパティ](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)があります。 DataTable に最初に値が設定されると、すべての行が未変更としてマークされます。 いずれかの行の列の値を変更すると、行が変更済みとしてマークされます。

`SuppliersBLL` クラスでは、最初に単一の仕入先レコードを `SuppliersDataTable` に読み取り、次のコードを使用して、`Address`、`City`、および `Country` 列の値を設定することによって、指定された仕入先のアドレス情報を更新します。

[!code-csharp[Main](performing-batch-updates-cs/samples/sample5.cs)]

このコードネイティブは、値が変更されたかどうかに関係なく、渡されたアドレス、市区町村、国の値を `SuppliersDataTable` 内の `SuppliersRow` に割り当てます。 これらの変更により、`SuppliersRow` s `RowState` プロパティが変更済みとしてマークされます。 データアクセス層 s `Update` メソッドが呼び出されると、`SupplierRow` が変更されていることが確認されるため、データベースに `UPDATE` コマンドが送信されます。

ただし、このメソッドにコードを追加して、渡された address、city、および country の値が `SuppliersRow` s の既存の値と異なる場合にのみ割り当てるようにしたとします。 住所、市区町村、および国が既存のデータと同じ場合、変更は行われず、`SupplierRow` s `RowState` は変更なしとしてマークされたままになります。 結果として、DAL `Update` メソッドが呼び出されたときに、`SuppliersRow` が変更されていないため、データベースの呼び出しは行われません。

この変更を適用するには、渡されたアドレス、市区町村、国の値を無条件に割り当てるステートメントを次のコードに置き換えます。

[!code-csharp[Main](performing-batch-updates-cs/samples/sample6.cs)]

このコードを追加すると、DAL の `Update` メソッドは、アドレス関連の値が変更されたレコードだけを対象として `UPDATE` ステートメントをデータベースに送信します。

または、渡されたアドレスフィールドとデータベースデータの間に違いがあるかどうかを追跡し、存在しない場合は、単に DAL s `Update` メソッドの呼び出しをバイパスすることもできます。 この方法は、DB ダイレクトメソッドを使用した場合に適しています。これは、データベースの呼び出しが実際に必要かどうかを判断するために `RowState` を確認できる `SuppliersRow` インスタンスが DB ダイレクトメソッドに渡されないためです。

> [!NOTE]
> `UpdateSupplierAddress` メソッドが呼び出されるたびに、データベースに対して呼び出しが行われ、更新されたレコードに関する情報が取得されます。 次に、データが変更された場合、テーブル行を更新するための別のデータベース呼び出しが行われます。 このワークフローを最適化するには、`BatchUpdate.aspx` ページの*すべて*の変更を含む `EmployeesDataTable` インスタンスを受け入れる `UpdateSupplierAddress` メソッドのオーバーロードを作成します。 次に、データベースを1回呼び出して、`Suppliers` テーブルからすべてのレコードを取得することができます。 その後、2つの結果セットを列挙し、変更が発生したレコードのみを更新できます。

## <a name="summary"></a>まとめ

このチュートリアルでは、完全に編集可能な DataList を作成し、ユーザーが複数のサプライヤーのアドレス情報をすばやく変更できるようにする方法を説明しました。 このチュートリアルでは、まず、DataList s アドレス、市区町村、および国の値に対して、編集インターフェイスの TextBox Web コントロールを `ItemTemplate`します。 次に、DataList の上と下に [すべて更新] ボタンを追加しました。 ユーザーが自分の変更を行って [すべて更新] ボタンをクリックすると、`DataListItem` s が列挙され、`SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドの呼び出しが行われます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Zack Jones と Ken による Isa です。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)
> [次へ](handling-bll-and-dal-level-exceptions-cs.md)
