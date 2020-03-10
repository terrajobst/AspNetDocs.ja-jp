---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
title: バッチ更新 (VB) |Microsoft Docs
author: rick-anderson
description: 1回の操作で複数のデータベースレコードを更新する方法について説明します。 ユーザーインターフェイスレイヤーでは、各行が編集可能な GridView をビルドします。 データ...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: d191a204-d7ea-458d-b81c-0b9049ecb55f
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
msc.type: authoredcontent
ms.openlocfilehash: f0bb83b17585876dd6d28a5893a223cce15da31d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501310"
---
# <a name="batch-updating-vb"></a>一括更新 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_VB.zip)または[PDF のダウンロード](batch-updating-vb/_static/datatutorial64vb1.pdf)

> 1回の操作で複数のデータベースレコードを更新する方法について説明します。 ユーザーインターフェイスレイヤーでは、各行が編集可能な GridView をビルドします。 データアクセス層では、1つのトランザクション内に複数の更新操作をラップして、すべての更新が成功するか、すべての更新がロールバックされるようにします。

## <a name="introduction"></a>はじめに

前の[チュートリアル](wrapping-database-modifications-within-a-transaction-vb.md)では、データアクセス層を拡張して、データベーストランザクションのサポートを追加する方法を説明しました。 データベーストランザクションは、一連のデータ変更ステートメントが1つのアトミック操作として扱われることを保証します。これにより、すべての変更が失敗するか、すべてが成功します。 この低レベルの DAL 機能を使用して、バッチデータ変更インターフェイスを作成する準備ができました。

このチュートリアルでは、各行を編集できる GridView をビルドします (図1を参照)。 各行は編集インターフェイスにレンダリングされるため、[編集]、[更新]、および [キャンセル] の各ボタンの列は必要ありません。 このページには、2つの [Update Products] ボタンがあります。このボタンをクリックすると、GridView 行が列挙され、データベースが更新されます。

[GridView の各行が編集可能 ![](batch-updating-vb/_static/image1.gif)](batch-updating-vb/_static/image1.png)

**図 1**: GridView の各行が編集可能である ([クリックしてフルサイズの画像を表示する](batch-updating-vb/_static/image2.png))

始めましょう!

> [!NOTE]
> [バッチ更新の実行](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)に関するチュートリアルでは、DataList コントロールを使用してバッチ編集インターフェイスを作成しました。 このチュートリアルは、GridView を使用しているでの前のチュートリアルとは異なり、バッチ更新はトランザクションのスコープ内で実行されます。 このチュートリアルを完了すると、前のチュートリアルに戻って、前のチュートリアルで追加したデータベーストランザクション関連の機能を使用するように更新することをお勧めします。

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>すべての GridView 行を編集できるようにするための手順を確認しています

[「データの挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)」で説明したように、GridView は、基になるデータを行単位で編集するための組み込みサポートを提供します。 内部的には、GridView は、 [`EditIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)を使用して編集可能な行を示します。 GridView はデータソースにバインドされているため、各行のインデックスが `EditIndex`の値と等しいかどうかを確認します。 その場合、その行のフィールドは編集インターフェイスを使用して表示されます。 BoundFields の場合、編集インターフェイスは、BoundField s `DataField` プロパティによって指定されたデータフィールドの値が `Text` プロパティに割り当てられている TextBox です。 TemplateFields の場合、`ItemTemplate`の代わりに `EditItemTemplate` が使用されます。

ユーザーが行 s の [編集] ボタンをクリックしたときに、編集ワークフローが開始されることを思い出してください。 これにより、ポストバックが発生し、GridView s `EditIndex` プロパティがクリックされた行 s インデックスに設定され、データがグリッドに再バインドされます。 行 s の [キャンセル] ボタンがクリックされると、ポストバック時に、データをグリッドに再バインドする前に `EditIndex` が `-1` の値に設定されます。 GridView の行はゼロでインデックス作成を開始するため、`EditIndex` を `-1` に設定すると、GridView が読み取り専用モードで表示されます。

`EditIndex` プロパティは行ごとの編集に適していますが、バッチ編集用には設計されていません。 GridView 全体を編集できるようにするには、編集インターフェイスを使用して各行を表示する必要があります。 これを実現する最も簡単な方法は、`ItemTemplate`で定義されている編集インターフェイスを使用して、編集可能な各フィールドが TemplateField として実装されている場所を作成することです。

次のいくつかの手順で、完全に編集可能な GridView を作成します。 手順 1. では、まず GridView とその ObjectDataSource を作成し、その BoundFields と CheckBoxField を TemplateFields に変換します。 手順 2. と 3. で、編集インターフェイスを TemplateFields `EditItemTemplate` s から `ItemTemplate` s に移動します。

## <a name="step-1-displaying-product-information"></a>手順 1: 製品情報の表示

行が編集可能な GridView を作成することを心配する前に、まず製品情報を表示してみましょう。 `BatchData` フォルダーの [`BatchUpdate.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグします。 GridView の `ID` を `ProductsGrid` に設定し、そのスマートタグから、`ProductsDataSource`という名前の新しい ObjectDataSource にバインドするように選択します。 `ProductsBLL` クラス s `GetProducts` メソッドからデータを取得するように ObjectDataSource を構成します。

[製品の Bll クラスを使用するように ObjectDataSource を構成 ![には](batch-updating-vb/_static/image2.gif)](batch-updating-vb/_static/image3.png)

**図 2**: `ProductsBLL` クラスを使用するように ObjectDataSource を構成する ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image4.png)されます)

[GetProducts メソッドを使用して製品データを取得 ![には](batch-updating-vb/_static/image3.gif)](batch-updating-vb/_static/image5.png)

**図 3**: `GetProducts` メソッドを使用して製品データを取得[する (クリックしてフルサイズの画像を表示する](batch-updating-vb/_static/image6.png))

GridView と同様に、ObjectDataSource の変更機能は行単位で動作するように設計されています。 一連のレコードを更新するには、データをバッチ処理して BLL に渡す、ASP.NET ページの分離コードクラスに少しコードを記述する必要があります。 そのため、ObjectDataSource s UPDATE、INSERT、および DELETE の各タブのドロップダウンリストを (None) に設定します。 [完了] をクリックしてウィザードを終了します。

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](batch-updating-vb/_static/image4.gif)](batch-updating-vb/_static/image7.png)

**図 4**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズのイメージを表示する](batch-updating-vb/_static/image8.png))

データソースの構成ウィザードを完了すると、ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](batch-updating-vb/samples/sample1.aspx)]

データソースの構成ウィザードを完了すると、Visual Studio によって、GridView の product データフィールドの連結フィールドと CheckBoxField が作成されます。 このチュートリアルでは、を使用して、製品の名前、カテゴリ、価格、および廃止された状態を表示および編集できるようにします。 `ProductName`、`CategoryName`、`UnitPrice`、`Discontinued` の各フィールドを除くすべてのフィールドを削除し、最初の3つのフィールドの `HeaderText` プロパティの名前をそれぞれ Product、Category、および Price に変更します。 最後に、GridView s スマートタグの [ページングを有効にし、並べ替えを有効にする] チェックボックスをオンにします。

この時点で、GridView には、3つの連結されたフィールド (`ProductName`、`CategoryName`、および `UnitPrice`) と CheckBoxField (`Discontinued`) があります。 これらの4つのフィールドを TemplateFields に変換してから、編集インターフェイスを TemplateField s `EditItemTemplate` から `ItemTemplate`に移動する必要があります。

> [!NOTE]
> 「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)」チュートリアルの templatefields の作成とカスタマイズについて説明します。 ここでは、BoundFields と CheckBoxField を TemplateFields に変換し、その `ItemTemplate` で編集インターフェイスを定義する手順について説明しますが、行き詰まった場合やリフレッシャーが必要な場合は、前のチュートリアルを参照してください。

GridView s スマートタグから [列の編集] リンクをクリックして、[フィールド] ダイアログボックスを開きます。 次に、各フィールドを選択し、[このフィールドを TemplateField に変換する] リンクをクリックします。

![既存の BoundFields と CheckBoxField を TemplateFields に変換します。](batch-updating-vb/_static/image5.gif)

**図 5**: 既存の boundfields と CheckBoxField を Templatefields に変換する

各フィールドが TemplateField になったので、編集インターフェイスを `EditItemTemplate` s から `ItemTemplate` s に移動する準備ができました。

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>手順 2:`ProductName`、`UnitPrice`、および`Discontinued`の編集インターフェイスの作成

`ProductName`、`UnitPrice`、および `Discontinued` 編集インターフェイスの作成は、この手順のトピックです。各インターフェイスは TemplateField s `EditItemTemplate`で既に定義されているため、非常に簡単です。 `CategoryName` 編集インターフェイスを作成することは、該当するカテゴリの DropDownList を作成する必要があるため、少し複雑になります。 この `CategoryName` 編集インターフェイスについては、手順 3. で説明します。

では、`ProductName` TemplateField から始めましょう。 GridView s スマートタグから [Edit Templates] リンクをクリックし、`ProductName` TemplateField s `EditItemTemplate`にドリルダウンします。 テキストボックスを選択し、クリップボードにコピーして、`ProductName` TemplateField s `ItemTemplate`に貼り付けます。 TextBox s `ID` プロパティを `ProductName`に変更します。

次に、`ItemTemplate` に RequiredFieldValidator を追加して、ユーザーが各製品名に値を提供するようにします。 `ControlToValidate` プロパティを ProductName に設定し、`ErrorMessage` プロパティに製品の名前を指定する必要があります。 \*する `Text` プロパティ。 これらを `ItemTemplate`に追加すると、画面は図6のようになります。

[![ProductName TemplateField にテキストボックスと RequiredFieldValidator が含まれるようになりました。](batch-updating-vb/_static/image6.gif)](batch-updating-vb/_static/image9.png)

**図 6**: `ProductName` TemplateField にテキストボックスと RequiredFieldValidator が含まれるようになりました ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image10.png)されます)

`UnitPrice` 編集インターフェイスの場合は、まず `EditItemTemplate` から `ItemTemplate`にテキストボックスをコピーします。 次に、テキストボックスの前に $ を置き、その `ID` プロパティを UnitPrice に、その `Columns` プロパティを8に設定します。

また、CompareValidator を `UnitPrice` s `ItemTemplate` に追加して、ユーザーが入力した値が $0.00 以上の有効な通貨値であることを確認します。 [バリデーター s `ControlToValidate`] プロパティを [UnitPrice] に、[`ErrorMessage`] プロパティを [UnitPrice] に設定し、有効な通貨値を入力する必要があります。 通貨記号を省略し、その `Text` プロパティを \*に、`Type` プロパティを `Currency`に、その `Operator` プロパティを0に、その `GreaterThanEqual`プロパティを0にします。`ValueToCompare`

[入力した価格が負でない通貨値であることを確認するために CompareValidator を追加 ![ます。](batch-updating-vb/_static/image7.gif)](batch-updating-vb/_static/image11.png)

**図 7**: 入力した価格が負でない通貨値であることを確認するために CompareValidator を追加する ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image12.png)されます)

`Discontinued` TemplateField の場合、`ItemTemplate`で既に定義されているチェックボックスを使用できます。 単純に `ID` を "廃止" に設定し、その `Enabled` プロパティを `True`に設定します。

## <a name="step-3-creating-thecategorynameediting-interface"></a>手順 3:`CategoryName`編集インターフェイスを作成する

`CategoryName` TemplateField s `EditItemTemplate` の編集インターフェイスには、`CategoryName` データフィールドの値を表示するテキストボックスが含まれています。 これを、使用可能なカテゴリを一覧表示する DropDownList に置き換える必要があります。

> [!NOTE]
> 「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)」チュートリアルでは、テキストボックスではなく DropDownList を含めるようにテンプレートをカスタマイズする方法について詳しく説明します。 手順は完了しましたが、tersely に表示されます。 カテゴリ DropDownList の作成と構成の詳細については、「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)」チュートリアルを参照してください。

[DropDownList] をツールボックスから `CategoryName` TemplateField s `ItemTemplate`にドラッグし、その `ID` を `Categories`に設定します。 この時点では、通常、新しい ObjectDataSource を作成して、そのスマートタグを使用して DropDownLists s データソースを定義します。 ただし、`ItemTemplate`内に ObjectDataSource が追加されるため、各 GridView 行に対して ObjectDataSource インスタンスが作成されます。 代わりに、によって、GridView の TemplateFields フィールド以外に ObjectDataSource が作成されます。 テンプレートの編集を終了し、ObjectDataSource をツールボックスから `ProductsDataSource` ObjectDataSource の下のデザイナーにドラッグします。 新しい ObjectDataSource `CategoriesDataSource` という名前を設定し、`CategoriesBLL` クラス s `GetCategories` メソッドを使用するように構成します。

[カテゴリ Bll クラスを使用するように ObjectDataSource を構成 ![には](batch-updating-vb/_static/image8.gif)](batch-updating-vb/_static/image13.png)

**図 8**: `CategoriesBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](batch-updating-vb/_static/image14.png))

[GetCategories メソッドを使用してカテゴリデータを取得 ![には](batch-updating-vb/_static/image9.gif)](batch-updating-vb/_static/image15.png)

**図 9**: `GetCategories` メソッドを使用してカテゴリデータを取得[する (クリックしてフルサイズの画像を表示する](batch-updating-vb/_static/image16.png))

この ObjectDataSource はデータを取得するためにのみ使用されるため、[更新] タブと [削除] タブのドロップダウンリストを [(なし)] に設定します。 [完了] をクリックしてウィザードを終了します。

[[更新] タブと [削除] タブのドロップダウンリストを [(なし)] に設定 ![ます。](batch-updating-vb/_static/image10.gif)](batch-updating-vb/_static/image17.png)

**図 10**: [更新] タブと [削除] タブのドロップダウンリストを (なし) に設定する ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image18.png)されます)

ウィザードを完了すると、`CategoriesDataSource` s 宣言マークアップは次のようになります。

[!code-aspx[Main](batch-updating-vb/samples/sample2.aspx)]

`CategoriesDataSource` 作成して構成した状態で `CategoryName` TemplateField s `ItemTemplate` に戻り、DropDownList s スマートタグから [データソースの選択] リンクをクリックします。 データソース構成ウィザードで、最初のドロップダウンリストから [`CategoriesDataSource`] オプションを選択し、値として表示と `CategoryID` に `CategoryName` 使用することを選択します。

[DropDownList をカテゴリデータソースにバインド ![には](batch-updating-vb/_static/image11.gif)](batch-updating-vb/_static/image19.png)

**図 11**: DropDownList を `CategoriesDataSource` にバインドする ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image20.png)されます)

この時点で、`Categories` DropDownList はすべてのカテゴリを一覧表示しますが、GridView 行にバインドされている製品の適切なカテゴリはまだ自動的に選択されていません。 これを実現するには、`Categories` DropDownList s `SelectedValue` を製品の `CategoryID` 値に設定する必要があります。 「DropDownList s」スマートタグから [データバインディングの編集] リンクをクリックし、図12に示すように、`SelectedValue` プロパティを `CategoryID` データフィールドに関連付けます。

![Product s CategoryID 値を DropDownList s SelectedValue プロパティにバインドします。](batch-updating-vb/_static/image12.gif)

**図 12**: `CategoryID` 値を DropDownList s `SelectedValue` プロパティにバインドする

最後に1つの問題が残っています。製品に `CategoryID` 値が指定されていない場合、`SelectedValue` の databinding ステートメントで例外が発生します。 これは、DropDownList にカテゴリの項目のみが含まれており、`CategoryID`の `NULL` データベース値を持つ製品のオプションが提供されていないためです。 これを解決するには、DropDownList s `AppendDataBoundItems` プロパティを `True` に設定し、新しい項目を DropDownList に追加します。これにより、宣言構文の `Value` プロパティを省略します。 つまり、`Categories` DropDownList s の宣言構文は次のようになります。

[!code-aspx[Main](batch-updating-vb/samples/sample3.aspx)]

`Value` 属性が明示的に空の文字列に設定されている `<asp:ListItem Value="">` を選択する方法に注意してください。 `NULL` のケースを処理するためにこの追加の DropDownList 項目が必要な理由と、`Value` プロパティを空の文字列に割り当てる理由について詳しく説明するために、「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)」チュートリアルを参照してください。

> [!NOTE]
> ここでは、パフォーマンスとスケーラビリティに関する潜在的な問題について説明します。 各行には、データソースとして `CategoriesDataSource` を使用する DropDownList があるため、`CategoriesBLL` class s `GetCategories` メソッドは、ページへのアクセスごとに*n*回呼び出されます。ここで、 *n*は GridView の行数です。 これらの*n* `GetCategories` を呼び出すと、データベースに対して*n 個*のクエリが発生します。 このデータベースへの影響は、要求ごとのキャッシュ、または SQL キャッシュの依存関係または非常に短い時間ベースの有効期限を使用してキャッシュレイヤーを介して返されたカテゴリをキャッシュすることによって軽減できます。 要求ごとのキャッシュオプションの詳細については、「[要求ごとのキャッシュストアの`HttpContext.Items`](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)」を参照してください。

## <a name="step-4-completing-the-editing-interface"></a>手順 4: 編集インターフェイスを完了する

進行状況を表示するために、GridView のテンプレートにいくつかの変更を加えました。 ブラウザーで進行状況を確認してください。 図13に示すように、各行は、セルの編集インターフェイスを含む `ItemTemplate`を使用してレンダリングされます。

[各 GridView 行が編集可能 ![](batch-updating-vb/_static/image13.gif)](batch-updating-vb/_static/image21.png)

**図 13**: 各 GridView 行が編集可能である ([クリックしてフルサイズの画像を表示する](batch-updating-vb/_static/image22.png))

この時点では、いくつかの軽微な書式設定の問題が発生します。 まず、`UnitPrice` 値には4つの小数点が含まれていることに注意してください。 この問題を解決するには、`UnitPrice` TemplateField s `ItemTemplate` に戻り、TextBox s のスマートタグから [自動接続の編集] リンクをクリックします。 次に、`Text` プロパティを数値として書式設定するように指定します。

![テキストプロパティを数値として書式設定する](batch-updating-vb/_static/image14.gif)

**図 14**: `Text` のプロパティを数値として書式設定する

次に、[`Discontinued`] 列のチェックボックスを中央に配置します (左揃えではなく)。 GridView s スマートタグから [列の編集] をクリックし、左下隅のフィールドの一覧から `Discontinued` TemplateField を選択します。 図15に示すように、`ItemStyle` にドリルダウンし、`HorizontalAlign` プロパティを Center に設定します。

![[中止] チェックボックスを中央にする](batch-updating-vb/_static/image15.gif)

**図 15**: `Discontinued` チェックボックスを中央に配置する

次に、ValidationSummary コントロールをページに追加し、その `ShowMessageBox` プロパティを `True` に設定し、その `ShowSummary` プロパティを `False`に設定します。 また、ボタン Web コントロールも追加します。このボタンをクリックすると、ユーザーの変更が更新されます。 具体的には、2つのボタン Web コントロール (GridView の上に1つ、その下に1つ) を追加し、両方のコントロールに `Text` プロパティを設定して製品を更新します。

GridView の編集インターフェイスは TemplateFields `ItemTemplate` s で定義されているため、`EditItemTemplate` のは不要であり、削除される可能性があります。

上記の書式変更を説明し、ボタンコントロールを追加し、不要な `EditItemTemplate` を削除すると、ページ s の宣言構文は次のようになります。

[!code-aspx[Main](batch-updating-vb/samples/sample4.aspx)]

図16は、ボタン Web コントロールが追加され、書式が変更された後にブラウザーで表示するときに、このページを示しています。

[ページに2つの [更新製品] ボタンが追加され ![](batch-updating-vb/_static/image16.gif)](batch-updating-vb/_static/image23.png)

**図 16**: ページに2つの [製品の更新] ボタンが追加されました ([クリックすると、フルサイズの画像が表示](batch-updating-vb/_static/image24.png)されます)

## <a name="step-5-updating-the-products"></a>手順 5: 製品を更新する

ユーザーがこのページにアクセスすると、変更が加えられ、2つの [製品の更新] ボタンのいずれかをクリックします。 その時点で、行ごとにユーザーが入力した値を `ProductsDataTable` インスタンスに保存してから、その `ProductsDataTable` インスタンスを DAL の `UpdateWithTransaction` メソッドに渡す BLL メソッドに渡す必要があります。 [前のチュートリアル](wrapping-database-modifications-within-a-transaction-vb.md)で作成した `UpdateWithTransaction` メソッドを使用すると、変更のバッチがアトミック操作として更新されるようになります。

`BatchUpdate.aspx.vb` に `BatchUpdate` という名前のメソッドを作成し、次のコードを追加します。

[!code-vb[Main](batch-updating-vb/samples/sample5.vb)]

このメソッドは、まず、BLL s `GetProducts` メソッドの呼び出しを使用して、すべての製品を `ProductsDataTable` に戻します。 次に、`ProductGrid` GridView s [`Rows` コレクション](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)を列挙します。 `Rows` コレクションには、GridView に表示される各行の[`GridViewRow` インスタンス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx)が含まれています。 1ページあたり最大10行を表示しているため、GridView の `Rows` コレクションに含まれる項目数は10個までです。

行ごとに、`ProductID` が `DataKeys` コレクションからグラブされ、適切な `ProductsRow` が `ProductsDataTable`から選択されます。 4つの TemplateField 入力コントロールがプログラムによって参照され、その値が `ProductsRow` インスタンスのプロパティに割り当てられます。 各 GridView 行 s の値を使用して `ProductsDataTable`を更新した後は、前のチュートリアルで説明したように、BLL の `UpdateWithTransaction` メソッドに渡されます。このメソッドは、単に DAL s `UpdateWithTransaction` メソッドを呼び出します。

このチュートリアルで使用するバッチ更新アルゴリズムでは、製品の情報が変更されているかどうかに関係なく、GridView の行に対応する `ProductsDataTable` の各行を更新します。 このようなブラインド更新は、通常はパフォーマンス上の問題ではありませんが、データベーステーブルへの変更を監査すると、余分なレコードが生じる可能性があります。 [バッチ更新の実行](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)に関するチュートリアルでは、DataList を使用してバッチ更新インターフェイスを探索し、ユーザーが実際に変更したレコードのみを更新するコードを追加しました。 必要に応じて、[バッチ更新を実行](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)する方法を自由に使用して、このチュートリアルのコードを更新してください。

> [!NOTE]
> データソースをそのスマートタグを使用して GridView にバインドすると、Visual Studio によって、データソースの主キー値が GridView s `DataKeyNames` プロパティに自動的に割り当てられます。 手順 1. で説明したように、gridview s スマートタグを介して ObjectDataSource を GridView にバインドしなかった場合は、`DataKeys` コレクションを使用して各行の `ProductID` 値にアクセスするために、GridView の `DataKeyNames` プロパティを ProductID に手動で設定する必要があります。

`BatchUpdate` で使用されるコードは、BLL の `UpdateProduct` メソッドで使用されるコードと似ていますが、`UpdateProduct` メソッドでは、アーキテクチャから取得される `ProductRow` インスタンスは1つだけであるという主な違いがあります。 `ProductRow` のプロパティを割り当てるコードは、全体的なパターンと同じように、`BatchUpdate`の `For Each` ループ内のコードと `UpdateProducts` メソッドとの間で同じです。

このチュートリアルを完了するには、[製品の更新] ボタンのいずれかをクリックしたときに、`BatchUpdate` メソッドを呼び出す必要があります。 これらの2つのボタンコントロールの `Click` イベントのイベントハンドラーを作成し、イベントハンドラーに次のコードを追加します。

[!code-vb[Main](batch-updating-vb/samples/sample6.vb)]

最初に、`BatchUpdate`に対して呼び出しが行われます。 次に、 [`ClientScript` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.clientscript(VS.80).aspx)を使用して、製品が更新されたことを読み取るメッセージボックスを表示する JavaScript を挿入します。

このコードをテストするには、少し時間を取ってください。 ブラウザーを使用して `BatchUpdate.aspx` にアクセスし、いくつかの行を編集して、[更新製品] ボタンのいずれかをクリックします。 入力検証エラーがないと仮定すると、製品が更新されたことを読み取るメッセージボックスが表示されます。 更新の原子性を検証するには、`UnitPrice` 値1234.56 を禁止するランダム `CHECK` 制約を追加することを検討してください。 次に、`BatchUpdate.aspx`から複数のレコードを編集し、製品の `UnitPrice` 値の1つを禁止値 (1234.56) に設定します。 そのバッチ操作を元の値にロールバックしたときに、他の変更と共に [製品の更新] をクリックすると、エラーが発生します。

## <a name="an-alternativebatchupdatemethod"></a>代替の`BatchUpdate`方法

ここで説明した `BatchUpdate` 方法では、BLL `GetProducts` メソッドから*すべて*の製品を取得し、GridView に表示されるレコードのみを更新します。 この方法は、GridView がページングを使用しない場合に最適ですが、その場合は、数百、数千、数十の製品が存在する可能性がありますが、GridView には10行しかありません。 このような場合、データベースからすべての製品を取得するのは、そのうちの10を変更することだけです。

このような状況では、代わりに次の `BatchUpdateAlternate` メソッドを使用することを検討してください。

[!code-vb[Main](batch-updating-vb/samples/sample7.vb)]

`BatchMethodAlternate` は、`products`という名前の新しい空の `ProductsDataTable` を作成することから始めます。 次に、GridView s `Rows` コレクションをステップ実行します。行ごとに、BLL s `GetProductByProductID(productID)` メソッドを使用して特定の製品情報を取得します。 取得した `ProductsRow` インスタンスのプロパティは `BatchUpdate`と同じ方法で更新されますが、行を更新すると、DataTable s [`ImportRow(DataRow)` メソッド](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)を使用して `products` `ProductsDataTable` にインポートされます。

`For Each` ループが完了すると、`products` には GridView 内の行ごとに1つの `ProductsRow` インスタンスが含まれます。 各 `ProductsRow` インスタンスは (更新ではなく) `products` に追加されているため、無条件に `UpdateWithTransaction` メソッドに渡すと、`ProductsTableAdapter` は各レコードをデータベースに挿入しようとします。 代わりに、これらの各行が変更されている (追加されていない) ことを指定する必要があります。

これを行うには、`UpdateProductsWithTransaction`という名前の BLL に新しいメソッドを追加します。 次に示す `UpdateProductsWithTransaction`は、`ProductsDataTable` 内の各 `ProductsRow` インスタンスの `RowState` を `Modified` に設定し、その `ProductsDataTable` を DAL の `UpdateWithTransaction` メソッドに渡します。

[!code-vb[Main](batch-updating-vb/samples/sample8.vb)]

## <a name="summary"></a>まとめ

GridView には、行単位の編集機能が組み込まれていますが、完全に編集可能なインターフェイスの作成はサポートされていません。 このチュートリアルで説明したように、このようなインターフェイスは可能ですが、多少の作業が必要です。 すべての行が編集可能な GridView を作成するには、GridView s フィールドを TemplateFields に変換し、`ItemTemplate` 内で編集インターフェイスを定義する必要があります。 また、GridView とは別に、すべての型のボタン Web コントロールをページに追加する必要があります。 イベントハンドラー `Click` これらのボタンは、GridView の `Rows` コレクションを列挙し、変更を `ProductsDataTable`に格納して、更新された情報を適切な BLL メソッドに渡す必要があります。

次のチュートリアルでは、batch を削除するためのインターフェイスを作成する方法について説明します。 具体的には、各 GridView 行にチェックボックスが含まれており、[すべての型を更新] ボタンの代わりに、[選択した行の削除] ボタンがあります。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy と David になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](wrapping-database-modifications-within-a-transaction-vb.md)
> [次へ](batch-deleting-vb.md)
