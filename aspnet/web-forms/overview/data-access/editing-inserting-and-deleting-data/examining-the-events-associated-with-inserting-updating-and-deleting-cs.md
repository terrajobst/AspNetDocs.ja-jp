---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: 挿入、更新、および削除に関連付けられてC#いるイベントを調べる () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ASP.NET データ Web コントロールの挿入、更新、または削除操作の前後に発生するイベントを使用します。 W...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: a8c1388b73524a8bb918b67aa265db894c07636f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78493426"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>挿入、更新、削除に関連付けられているイベントを調べる (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe)または[PDF のダウンロード](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> このチュートリアルでは、ASP.NET データ Web コントロールの挿入、更新、または削除操作の前後に発生するイベントを使用します。 また、製品フィールドのサブセットのみを更新するように編集インターフェイスをカスタマイズする方法についても説明します。

## <a name="introduction"></a>はじめに

GridView、DetailsView、または FormView コントロールの組み込みの挿入、編集、または削除機能を使用する場合、エンドユーザーが新しいレコードを追加したり、既存のレコードを更新または削除したりするプロセスを完了すると、さまざまな手順が実行されます。 [前のチュートリアル](an-overview-of-inserting-updating-and-deleting-data-cs.md)で説明したように、GridView で行が編集されると、[編集] ボタンが [Update] ボタンと [Cancel] ボタンに置き換えられ、Boundfields がテキストボックスに変わります。 エンドユーザーがデータを更新して [更新] をクリックすると、次の手順がポストバック時に実行されます。

1. GridView では、ObjectDataSource の `UpdateParameters` が、ユーザーが入力した値と共に、編集されたレコードの一意の識別フィールド (`DataKeyNames` プロパティを介して) に設定されます。
2. GridView は、ObjectDataSource の `Update()` メソッドを呼び出します。このメソッドは、基になるオブジェクト (前のチュートリアルでは`ProductsDAL.UpdateProduct`) の適切なメソッドを呼び出します。
3. 基になるデータ (更新された変更が含まれる) は、GridView に再バインドされます。

この一連の手順では、いくつかのイベントが発生し、必要に応じてカスタムロジックを追加するためのイベントハンドラーを作成できるようになりました。 たとえば、手順1の前に、GridView の `RowUpdating` イベントが発生します。 この時点で、検証エラーが発生した場合に更新要求を取り消すことができます。 `Update()` メソッドが呼び出されると、ObjectDataSource の `Updating` イベントが発生し、`UpdateParameters`の値を追加またはカスタマイズできるようになります。 ObjectDataSource の基になるオブジェクトのメソッドの実行が完了すると、ObjectDataSource の `Updated` イベントが発生します。 `Updated` イベントのイベントハンドラーは、影響を受けた行の数や、例外が発生したかどうかなど、更新操作の詳細を調べることができます。 最後に、手順2の後に、GridView の `RowUpdated` イベントが発生します。このイベントのイベントハンドラーでは、実行した更新操作に関する追加情報を調べることができます。

図1は、GridView を更新するときのこの一連のイベントと手順を示しています。 図1のイベントパターンは、GridView による更新には固有ではありません。 GridView、DetailsView、または FormView からデータを挿入、更新、または削除すると、データ Web コントロールと ObjectDataSource の両方について、同じ順序で precipitates イベントが発生します。

[GridView のデータを更新するときに一連のイベントが発生し ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**図 1**: GridView のデータを更新するときに一連のイベントが発生し、イベントが発生します ([クリックすると、フルサイズのイメージが表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png)されます)

このチュートリアルでは、これらのイベントを使用して、ASP.NET data Web コントロールの組み込みの挿入、更新、および削除機能を拡張します。 また、製品フィールドのサブセットのみを更新するように編集インターフェイスをカスタマイズする方法についても説明します。

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>手順 1: 製品の`ProductName`と`UnitPrice`のフィールドの更新

前のチュートリアルの編集インターフェイスでは、読み取り専用ではない*すべて*の product フィールドを含める必要がありました。 GridView からフィールドを削除する場合 `QuantityPerUnit`-データを更新するときに、データ Web コントロールは ObjectDataSource の `QuantityPerUnit` `UpdateParameters` 値を設定しません。 次に、ObjectDataSource は、`null` 値を `UpdateProduct` ビジネスロジック層 (BLL) メソッドに渡します。これにより、編集されたデータベースレコードの `QuantityPerUnit` 列が `NULL` 値に変更されます。 同様に、`ProductName`などの必須フィールドが編集インターフェイスから削除された場合、更新は失敗し、"*列 ' ProductName ' は null*を許容しません" という例外が表示されます。 この動作が発生する理由は、ObjectDataSource が `ProductsBLL` クラスの `UpdateProduct` メソッドを呼び出すように構成されており、各製品フィールドに入力パラメーターが必要であるためです。 したがって、ObjectDataSource の `UpdateParameters` コレクションには、メソッドの入力パラメーターごとにパラメーターが含まれていました。

エンドユーザーがフィールドのサブセットのみを更新できるデータ Web コントロールを提供する場合は、ObjectDataSource の `Updating` イベントハンドラーで欠落している `UpdateParameters` 値をプログラムによって設定するか、フィールドのサブセットのみを想定する BLL メソッドを作成して呼び出す必要があります。 後者の方法を見てみましょう。

具体的には、編集可能な GridView で `ProductName` および `UnitPrice` のフィールドだけを表示するページを作成します。 この GridView の編集インターフェイスでは、表示されている2つのフィールド、`ProductName` および `UnitPrice`のみを更新できます。 この編集インターフェイスは製品のフィールドのサブセットのみを提供するため、既存の BLL の `UpdateProduct` メソッドを使用する ObjectDataSource を作成する必要があります。また、不足している product フィールド値が `Updating` イベントハンドラーでプログラムによって設定されているか、GridView で定義されたフィールドのサブセットのみを必要とする新しい BLL メソッドを作成する このチュートリアルでは、後者のオプションを使用し、`productName`、`unitPrice`、および `productID`の3つの入力パラメーターだけを受け取る `UpdateProduct` メソッドのオーバーロードを作成します。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

元の `UpdateProduct` メソッドと同様に、このオーバーロードは、指定された `ProductID`の製品がデータベース内に存在するかどうかを確認することから始まります。 そうでない場合は、`false`を返します。これは、製品情報を更新する要求が失敗したことを示します。 それ以外の場合は、既存の製品レコードの `ProductName` と `UnitPrice` フィールドを適宜更新し、TableAdapter の `Update()` メソッドを呼び出して更新をコミットし、`ProductsRow` インスタンスを渡します。

`ProductsBLL` クラスに追加されたことで、簡略化された GridView インターフェイスを作成する準備が整いました。 `EditInsertDelete` フォルダー内の `DataModificationEvents.aspx` を開き、GridView をページに追加します。 新しい ObjectDataSource を作成し、`ProductsBLL` クラスを使用するように構成します。これには、`GetProducts` への `Select()` メソッドマッピングと、`UpdateProduct`、`productName`、および `unitPrice`の入力パラメーターのみを受け取る `productID` オーバーロードへのその `Update()` メソッドのマッピングが含まれます。 図2は、ObjectDataSource の `Update()` メソッドを `ProductsBLL` クラスの新しい `UpdateProduct` メソッドオーバーロードにマッピングするときのデータソースの作成ウィザードを示しています。

[ObjectDataSource の Update () メソッドを新しい UpdateProduct オーバーロードにマップ ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**図 2**: ObjectDataSource の `Update()` メソッドを新しい `UpdateProduct` オーバーロードにマップする ([クリックしてフルサイズのイメージを表示する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png))

この例では最初にデータの編集のみを行う必要がありますが、レコードの挿入や削除を行うことはできません。そのため、[挿入] タブと [削除] タブに移動し、ドロップダウンリストから [(なし)] をクリックして、ObjectDataSource の `Insert()` および `Delete()` メソッドを `ProductsBLL` クラスのメソッドにマップしないことを明示的

[[挿入] タブと [削除] タブのドロップダウンリストから [(なし)] を選択 ![ます。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**図 3**: [挿入] タブと [削除] タブのドロップダウンリストから [(なし)] を選択[する (クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png)されます)

このウィザードを完了したら、GridView のスマートタグから [編集を有効にする] チェックボックスをオンにします。

データソースの作成ウィザードが完了し、GridView にバインドされると、Visual Studio は両方のコントロールに対して宣言構文を作成しました。 ソースビューにアクセスして、次に示す ObjectDataSource の宣言型マークアップを検査します。

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

ObjectDataSource の `Insert()` メソッドと `Delete()` メソッドのマッピングはないため、`InsertParameters` または `DeleteParameters` セクションはありません。 さらに、`Update()` メソッドは、3つの入力パラメーターのみを受け入れる `UpdateProduct` メソッドのオーバーロードにマップされるため、`UpdateParameters` のセクションには `Parameter` インスタンスが3つだけあります。

ObjectDataSource の `OldValuesParameterFormatString` プロパティは `original_{0}`に設定されていることに注意してください。 このプロパティは、データソースの構成ウィザードを使用するときに Visual Studio によって自動的に設定されます。 ただし、BLL メソッドでは元の `ProductID` 値が渡されるとは想定されていないため、このプロパティの割り当てを ObjectDataSource の宣言構文から完全に削除します。

> [!NOTE]
> デザインビューのプロパティウィンドウから `OldValuesParameterFormatString` プロパティ値をクリアするだけの場合、プロパティは宣言構文に存在しますが、空の文字列に設定されます。 宣言構文からプロパティを完全に削除するか、プロパティウィンドウから、値を既定の `{0}`に設定します。

ObjectDataSource には製品名、価格、および ID の `UpdateParameters` がありますが、Visual Studio では、各製品のフィールドの GridView に BoundField または CheckBoxField が追加されています。

[GridView ![、各製品のフィールドの BoundField または CheckBoxField が含まれています。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**図 4**: GridView には、各製品のフィールドの BoundField または CheckBoxField が含まれています ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png)されます)

エンドユーザーが製品を編集して [更新] ボタンをクリックすると、GridView は、読み取り専用ではなかったフィールドを列挙します。 次に、ObjectDataSource の `UpdateParameters` コレクション内の対応するパラメーターの値を、ユーザーが入力した値に設定します。 対応するパラメーターがない場合は、GridView によってコレクションに追加されます。 したがって、GridView ですべての製品のフィールドに対して BoundFields と CheckBoxFields が含まれている場合、objectdatasource の宣言型マークアップで指定されている入力パラメーターは3つだけであるとしても、objectdatasource は、これらすべてのパラメーターを受け取る `UpdateProduct` オーバーロードを呼び出します (図5を参照)。 同様に、`UpdateProduct` のオーバーロードの入力パラメーターに対応しない、非読み取り専用の product フィールドの組み合わせが GridView にある場合は、更新しようとすると例外が発生します。

[GridView によって ![ObjectDataSource の UpdateParameters コレクションにパラメーターが追加されます。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**図 5**: GridView は ObjectDataSource の `UpdateParameters` コレクションにパラメーターを追加します ([クリックすると、フルサイズのイメージが表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png)されます)

ObjectDataSource が製品名、価格、および ID だけを受け取る `UpdateProduct` オーバーロードを呼び出すようにするには、`ProductName` と `UnitPrice`に対してのみ編集可能なフィールドを持つように GridView を制限する必要があります。 これを実現するには、他の BoundFields と CheckBoxFields を削除するか、他のフィールドの `ReadOnly` プロパティを `true`に設定するか、またはその2つの組み合わせを使用します。 このチュートリアルでは、`ProductName` および `UnitPrice` BoundFields を除くすべての GridView フィールドを削除するだけです。その後、GridView の宣言マークアップは次のようになります。

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

`UpdateProduct` のオーバーロードには3つの入力パラメーターが必要ですが、GridView では2つの BoundFields しかありません。 これは、`productID` 入力パラメーターが主キーの値であり、編集された行の `DataKeyNames` プロパティの値を通じて渡されるためです。

GridView を `UpdateProduct` のオーバーロードと共に使用すると、ユーザーは製品の名前と価格だけを編集して、他の製品フィールドを失うことはありません。

[インターフェイスを ![して、製品の名前と価格だけを編集できます。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**図 6**: インターフェイスでは、製品の名前と価格だけを編集できます ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png)されます)

> [!NOTE]
> 前のチュートリアルで説明したように、GridView のビューステートが有効になっていることが非常に重要です (既定の動作)。 GridView s `EnableViewState` プロパティを `false`に設定すると、同時実行ユーザーが誤ってレコードを削除または編集する危険性があります。 「警告: 詳細については[、編集または削除をサポートし、ビューステートが無効になっている ASP.NET 2.0 GridViews/DetailsView/formviews での同時実行の問題](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)」を参照してください。

## <a name="improving-theunitpriceformatting"></a>`UnitPrice`の書式設定の改善

図6に示されている GridView の例は動作しますが、`UnitPrice` フィールドはまったく書式設定されていません。その結果、通貨記号がなく、小数点以下桁数が4桁の価格が表示されます。 編集できない行に通貨書式を適用するには、単に `UnitPrice` BoundField の `DataFormatString` プロパティを `{0:c}` に設定し、その `HtmlEncode` プロパティを `false`に設定します。

[UnitPrice の DataFormatString と HtmlEncode プロパティを適宜設定 ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**図 7**: `UnitPrice`の `DataFormatString` と `HtmlEncode` のプロパティを設定[する (クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png)されます)

この変更により、編集できない行は価格を通貨として書式設定します。ただし、編集された行には、通貨記号を含まない値と小数点以下4桁の値が表示されます。

[![編集できない行が通貨値として書式設定されるようになりました。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**図 8**: 編集できない行が通貨値として書式設定される ([クリックしてフルサイズの画像を表示する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png))

BoundField の `ApplyFormatInEditMode` プロパティを `true` (既定値は `false`) に設定することによって、`DataFormatString` プロパティで指定された書式設定の手順を編集インターフェイスに適用できます。 このプロパティを `true`に設定します。

[![UnitPrice BoundField の ApplyFormatInEditMode プロパティを true に設定します。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**図 9**: `UnitPrice` BoundField の `ApplyFormatInEditMode` プロパティを `true` に設定する ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png)されます)

この変更により、編集された行に表示される `UnitPrice` の値も通貨として書式設定されます。

[編集された行の UnitPrice 値が通貨として書式設定されている ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**図 10**: 編集した行の `UnitPrice` 値が通貨として書式設定される ([クリックしてフルサイズの画像を表示する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png))

ただし、$19.00 などのテキストボックスで通貨記号を使用して製品を更新すると、`FormatException`がスローされます。 GridView がユーザーが指定した値を ObjectDataSource の `UpdateParameters` コレクションに割り当てようとすると、`UnitPrice` 文字列 "$19.00" をパラメーターで必要な `decimal` に変換できません (図11を参照)。 これを解決するには、GridView の `RowUpdating` イベントのイベントハンドラーを作成し、ユーザーが指定した `UnitPrice` を通貨形式の `decimal`として解析することができます。

GridView の `RowUpdating` イベントは、2番目のパラメーターとして、 [GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)型のオブジェクトを受け取ります。これには、ObjectDataSource の `UpdateParameters` コレクションに割り当てる準備ができているユーザー指定の値を保持するプロパティの1つとして、`NewValues` ディクショナリが含まれます。 `NewValues` コレクション内の既存の `UnitPrice` 値は、通貨書式を使用して解析された10進数値で、`RowUpdating` イベントハンドラーの次のコード行で上書きできます。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

ユーザーが `UnitPrice` 値 ("$19.00" など) を指定した場合、この値は[10 進数](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)で計算された10進値で上書きされます。値を通貨として解析します。 これにより、通貨記号、コンマ、小数点などが発生した場合に、10進数が正しく解析され、NumberStyles 名前[空間の](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx)[列挙体](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx)が使用されます。

図11に、ユーザーが指定した `UnitPrice`の通貨記号による問題と、そのような入力を正しく解析するために GridView の `RowUpdating` イベントハンドラーを使用する方法を示します。

[編集された行の UnitPrice 値が通貨として書式設定されている ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**図 11**: 編集した行の `UnitPrice` 値が通貨として書式設定される ([クリックしてフルサイズの画像を表示する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png))

## <a name="step-2-prohibitingnull-unitprices"></a>手順 2:`NULL UnitPrices` を禁止する

データベースは `Products` テーブルの `UnitPrice` 列の値 `NULL` を許可するように構成されていますが、この特定のページにアクセスするユーザーが `NULL` `UnitPrice` 値を指定できないようにすることもできます。 つまり、ユーザーが製品行の編集時に `UnitPrice` 値の入力に失敗した場合は、結果をデータベースに保存するのではなく、このページで、編集したすべての製品に価格を指定する必要があることをユーザーに通知するメッセージを表示します。

GridView の `RowUpdating` イベントハンドラーに渡される `GridViewUpdateEventArgs` オブジェクトには、`Cancel` プロパティが含まれています。このプロパティは `true`に設定されている場合、更新プロセスを終了します。 `RowUpdating` イベントハンドラーを拡張して、`e.Cancel` を `true` に設定し、`NewValues` コレクション内の `UnitPrice` 値が `null`かどうかを説明するメッセージを表示してみましょう。

まず、`MustProvideUnitPriceMessage`という名前のページにラベル Web コントロールを追加します。 このラベルコントロールは、ユーザーが製品の更新時に `UnitPrice` 値を指定できなかった場合に表示されます。 ラベルの `Text` プロパティを「製品の価格を指定する必要があります」に設定します。 また、次の定義で `Warning` という名前の `Styles.css` に新しい CSS クラスを作成しました。

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

最後に、ラベルの `CssClass` プロパティを `Warning`に設定します。 この時点で、デザイナーは、図12に示すように、GridView の上に赤い、太字、斜体、特大のフォントサイズで警告メッセージを表示する必要があります。

[ラベルが GridView の上に追加された ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**図 12**: GridView の上にラベルが追加されました ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png)されます)

既定では、このラベルは非表示になっているため、`Visible` プロパティを `Page_Load` イベントハンドラーで `false` に設定します。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

ユーザーが `UnitPrice`を指定せずに製品を更新しようとした場合は、更新をキャンセルし、警告ラベルを表示します。 GridView の `RowUpdating` イベントハンドラーを次のように拡張します。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

ユーザーが価格を指定せずに製品を保存しようとすると、更新が取り消され、役に立つメッセージが表示されます。 データベース (およびビジネスロジック) では `UnitPrice` `NULL` が許可されますが、この特定の ASP.NET ページは使用できません。

[ユーザーが ![UnitPrice を空白のままにすることはできません](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**図 13**: ユーザーは `UnitPrice` 空白のままにすることはできません ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png)される)

ここまでは、GridView の `RowUpdating` イベントを使用して、ObjectDataSource の `UpdateParameters` コレクションに割り当てられているパラメーター値をプログラムによって変更する方法と、更新プロセスをすべて取り消す方法を説明しました。 これらの概念は、DetailsView コントロールと FormView コントロールに引き継がれ、挿入と削除にも適用されます。

これらのタスクは、`Inserting`、`Updating`、および `Deleting` イベントのイベントハンドラーを通じて ObjectDataSource レベルで実行することもできます。 これらのイベントは、基になるオブジェクトの関連付けられたメソッドが呼び出される前に起動され、入力パラメーターのコレクションを変更するか、操作を完全にキャンセルする機会を提供します。 これら3つのイベントのイベントハンドラーには、 [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx)型のオブジェクトが渡されます。このオブジェクトには、次の2つのプロパティがあります。

- [[キャンセル](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)]。 `true`に設定すると、実行中の操作が取り消されます。
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)。イベントハンドラーが `Inserting`、`Updating`、または `Deleting` イベントのどちらであるかに応じて、`InsertParameters`、`UpdateParameters`、または `DeleteParameters`のコレクションです。

ObjectDataSource レベルでのパラメーター値の使用方法を示すために、ページに DetailsView を含めて、ユーザーが新しい製品を追加できるようにしましょう。 この DetailsView は、新しい製品をデータベースにすばやく追加するためのインターフェイスを提供するために使用されます。 新しい製品を追加するときに一貫性のあるユーザーインターフェイスを維持するには、ユーザーが `ProductName` フィールドと `UnitPrice` フィールドに対してのみ値を入力できるようにします。 既定では、DetailsView の挿入インターフェイスに指定されていない値は、`NULL` データベースの値に設定されます。 ただし、後で説明するように、ObjectDataSource の `Inserting` イベントを使用して異なる既定値を挿入することもできます。

## <a name="step-3-providing-an-interface-to-add-new-products"></a>手順 3: 新しい製品を追加するためのインターフェイスを提供する

ツールボックスから [DetailsView] をドラッグして、GridView の上にあるデザイナーに移動し、`Height` と `Width` のプロパティをオフにして、ページに既に存在する ObjectDataSource にバインドします。 これにより、各製品のフィールドの BoundField または CheckBoxField が追加されます。 この DetailsView を使用して新しい製品を追加する必要があるため、スマートタグから [挿入を有効にする] オプションをオンにする必要があります。ただし、ObjectDataSource の `Insert()` メソッドが `ProductsBLL` クラスのメソッドにマップされていないため、このようなオプションはありません (データソースの構成時にこのマッピングを (None) に設定したことを思い出してください)。図3を参照してください)。

ObjectDataSource を構成するには、スマートタグから [データソースの構成] リンクを選択し、ウィザードを起動します。 最初の画面では、ObjectDataSource がバインドされている基になるオブジェクトを変更できます。`ProductsBLL`に設定したままにします。 次の画面には、ObjectDataSource のメソッドから基になるオブジェクトのへのマッピングが一覧表示されます。 `Insert()` メソッドと `Delete()` メソッドをどのメソッドにもマップしないように明示的に指定しても、[挿入] タブと [削除] タブにアクセスすると、マッピングが表示されます。 これは、`ProductsBLL`の `AddProduct` メソッドと `DeleteProduct` メソッドが `DataObjectMethodAttribute` の属性を使用して、それぞれ `Insert()` および `Delete()`の既定のメソッドであることを示すためです。 そのため、ObjectDataSource ウィザードでは、他の値が明示的に指定されていない限り、ウィザードを実行するたびにこれらの値が選択されます。

`Insert()` メソッドを `AddProduct` メソッドをポイントしたままにして、[削除] タブのドロップダウンリストを [(なし)] に設定します。

[[挿入] タブのドロップダウンリストを AddProduct メソッドに設定 ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**図 14**: [INSERT] タブのドロップダウンリストを `AddProduct` メソッドに設定する ([クリックしてフルサイズの画像を表示する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png))

[![[削除] タブのドロップダウンリストを [(なし)] に設定します。](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**図 15**: [削除] タブのドロップダウンリストを [(なし)] に設定する ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png)されます)

これらの変更を行った後、次に示すように、ObjectDataSource の宣言構文は `InsertParameters` コレクションを含むように展開されます。

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

ウィザードを再実行すると、`OldValuesParameterFormatString` プロパティが戻されました。 このプロパティを既定値 (`{0}`) に設定するか、宣言型の構文から完全に削除することで、このプロパティをクリアします。

ObjectDataSource には挿入機能があり、DetailsView のスマートタグには [挿入を有効にする] チェックボックスが含まれるようになりました。デザイナーに戻り、このオプションをオンにします。 次に、省いと `UnitPrice` と CommandField の2つの連結された `ProductName` フィールドのみを持つように、DetailsView をします。 この時点で、DetailsView の宣言構文は次のようになります。

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

図16は、この時点でブラウザーで表示するときにこのページを示しています。 ご覧のとおり、DetailsView には最初の製品 (Chai) の名前と価格が表示されます。 ただし、必要なのは、ユーザーがデータベースに新しい製品をすばやく追加するための手段を提供する挿入インターフェイスです。

[現在、DetailsView が読み取り専用モードで表示されて ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**図 16**: DetailsView が現在読み取り専用モードで表示されている ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png)されます)

挿入モードで DetailsView を表示するには、`DefaultMode` プロパティを `Inserting`に設定する必要があります。 これにより、最初にアクセスしたときに、挿入モードで DetailsView がレンダリングされ、新しいレコードを挿入した後もそのまま保持されます。 図17に示すように、このような DetailsView は新しいレコードを追加するための簡単なインターフェイスを提供します。

[DetailsView が ![新しい製品をすばやく追加するためのインターフェイスを提供する](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**図 17**: DetailsView は、新しい製品をすばやく追加するためのインターフェイスを提供します ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png)されます)

ユーザーが製品名と価格 (図17のように "Acme 水" や1.99 など) を入力して [挿入] をクリックすると、ポストバック ensues と挿入ワークフローが開始され、データベースに追加される新しい製品レコードがするされます。 DetailsView は挿入インターフェイスを保持し、図18に示すように、新しい製品を含めるために GridView が自動的にデータソースに再バインドされます。

![製品](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**図 18**: 製品 "Acme 水" がデータベースに追加されました。

図18の GridView には表示されませんが、DetailsView インターフェイス `CategoryID`、`SupplierID`、`QuantityPerUnit`などの製品フィールドは、データベースの値 `NULL` 割り当てられます。 これを確認するには、次の手順を実行します。

1. Visual Studio でサーバーエクスプローラーにアクセスする
2. `NORTHWND.MDF` データベースノードの展開
3. `Products` データベーステーブルノードを右クリックします。
4. [テーブルデータの表示] を選択します。

これにより、`Products` テーブル内のすべてのレコードが一覧表示されます。 図19に示すように、`ProductID`、`ProductName`、および `UnitPrice` 以外のすべての新しい製品の列には `NULL` 値が設定されています。

[DetailsView に指定されていない製品フィールドに NULL 値が割り当てられて ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**図 19**: DetailsView に指定されていない Product フィールドに値 `NULL` 割り当てられる ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png)されます)

これらの列値の1つまたは複数に対して、`NULL` 以外の既定値を指定することもできます。これは `NULL` が最適な既定のオプションではないため、またはデータベース列自体が `NULL` を許可しないためです。 これを実現するには、DetailsView の `InputParameters` コレクションのパラメーターの値をプログラムで設定します。 この割り当ては、DetailsView の `ItemInserting` イベントのイベントハンドラー、または ObjectDataSource の `Inserting` イベントに対して行うことができます。 データ Web コントロールレベルでは、事前レベルおよび事後レベルのイベントの使用について既に説明したので、ここでは ObjectDataSource のイベントを使用してみましょう。

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>手順 4:`CategoryID`および`SupplierID`パラメーターへの値の代入

このチュートリアルでは、このインターフェイスを使用して新しい製品を追加するときに、アプリケーションに対して、`CategoryID` と `SupplierID` 値1を割り当てる必要があることを考えてみましょう。 既に説明したように、ObjectDataSource には、データ変更プロセス中に起動される、上位レベルおよびポストレベルのイベントのペアがあります。 `Insert()` メソッドが呼び出されると、ObjectDataSource は最初にその `Inserting` イベントを発生させ、その `Insert()` メソッドが割り当てられているメソッドを呼び出し、最後に `Inserted` イベントを発生させます。 `Inserting` イベントハンドラーは、入力パラメーターを調整したり、操作を完全に取り消したりする最後の機会を与えます。

> [!NOTE]
> 実際のアプリケーションでは、ユーザーにカテゴリとサプライヤーを指定させたり、条件やビジネスロジック (ID 1 を選択するのではなく) に基づいてこの値を選択したりすることが必要になる場合があります。 に関係なく、この例は、ObjectDataSource の事前レベルイベントから入力パラメーターの値をプログラムで設定する方法を示しています。

時間を取って、ObjectDataSource の `Inserting` イベントのイベントハンドラーを作成します。 イベントハンドラーの2番目の入力パラメーターは `ObjectDataSourceMethodEventArgs`型のオブジェクトであることに注意してください。これには、parameters コレクション (`InputParameters`) にアクセスするためのプロパティと、操作をキャンセルするためのプロパティ (`Cancel`) が含まれています。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

この時点で、`InputParameters` プロパティには、DetailsView から割り当てられた値を持つ ObjectDataSource の `InsertParameters` コレクションが含まれています。 これらのパラメーターのいずれかの値を変更するには、単に: `e.InputParameters["paramName"] = value`を使用します。 したがって、`CategoryID` と `SupplierID` を1の値に設定するには、`Inserting` イベントハンドラーを次のように調整します。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

新しい製品 (Acme ソーダなど) を追加すると、新しい製品の `CategoryID` 列と `SupplierID` 列が1に設定されます (図20を参照)。

[新しい製品 ![、CategoryID および仕入先の値が1に設定されました](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**図 20**: 新しい製品の `CategoryID` と `SupplierID` の値が1に設定されました ([クリックすると、フルサイズの画像が表示](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png)されます)

## <a name="summary"></a>まとめ

編集、挿入、および削除のプロセスでは、データ Web コントロールと ObjectDataSource の両方が、いくつかの事前レベルおよび事後レベルのイベントを処理します。 このチュートリアルでは、事前レベルのイベントを確認し、これらを使用して入力パラメーターをカスタマイズする方法、またはデータの変更操作をデータ Web コントロールと ObjectDataSource のイベントの両方から完全にキャンセルする方法について説明しました。 次のチュートリアルでは、投稿レベルのイベントのイベントハンドラーの作成と使用について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Jackie Goor and Liz Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [次へ](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
