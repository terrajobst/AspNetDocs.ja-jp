---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: GridView にボタンを追加して対応さC#せる () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、テンプレートと GridView コントロールまたは DetailsView コントロールのフィールドの両方にカスタムボタンを追加する方法について説明します。 特に、...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5c87386e4fe2c53b39162071689f2522dcc6c7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78442420"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>GridView にボタンを追加し、応答する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe)または[PDF のダウンロード](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> このチュートリアルでは、テンプレートと GridView コントロールまたは DetailsView コントロールのフィールドの両方にカスタムボタンを追加する方法について説明します。 特に、ユーザーがサプライヤーを通じてページを作成できるようにする FormView を持つインターフェイスを構築します。

## <a name="introduction"></a>はじめに

レポートデータへの読み取り専用アクセスは多くのレポートシナリオに含まれていますが、レポートでは、表示されるデータに基づいてアクションを実行する機能が含まれていることは珍しくありません。 通常、この操作を行うには、レポートに表示される各レコードと共に Button、LinkButton、または ImageButton Web コントロールを追加する必要があります。これは、クリックすると、ポストバックが発生し、いくつかのサーバー側コードが呼び出されます。 レコードごとにデータを編集および削除することが、最も一般的な例です。 実際、[データの挿入、更新、削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)について説明したように、編集と削除は、GridView、DetailsView、および FormView コントロールが、1行のコードを記述しなくても、このような機能をサポートできるという点でよく見られます。

[編集] ボタンと [削除] ボタンに加えて、GridView、DetailsView、および FormView コントロールには、ボタン、リンクボタン、または ImageButtons を含めることができます。このボタンは、クリックすると、カスタムのサーバー側ロジックを実行します。 このチュートリアルでは、テンプレートと GridView コントロールまたは DetailsView コントロールのフィールドの両方にカスタムボタンを追加する方法について説明します。 特に、ユーザーがサプライヤーを通じてページを作成できるようにする FormView を持つインターフェイスを構築します。 特定の仕入先について、FormView には、サプライヤーに関する情報とボタン Web コントロールが表示されます。このボタンをクリックすると、関連付けられているすべての製品が廃止済みとしてマークされます。 また、GridView は、選択された業者によって提供される製品を一覧表示します。各行には、[価格] ボタンと [割引価格] ボタンが表示されます。このボタンをクリックすると、製品の `UnitPrice` が10% 上がります (図1を参照)。

[FormView と GridView の両方にカスタムアクションを実行するボタンが含まれている ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**図 1**: FormView と GridView の両方にカスタムアクションを実行するボタンが含まれている ([クリックしてフルサイズのイメージを表示する](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png))

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>手順 1: Button チュートリアル Web ページの追加

カスタムボタンを追加する方法については、まず、このチュートリアルで必要となる web サイトプロジェクトの ASP.NET ページを作成してみましょう。 まず、`CustomButtons`という名前の新しいフォルダーを追加します。 次に、次の2つの ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `CustomButtons.aspx`

![カスタムボタンに関連するチュートリアルの ASP.NET ページを追加する](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**図 2**: カスタムボタンに関連するチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`CustomButtons` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 そのため、ソリューションエクスプローラーからページのデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**図 3**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png)されます)

最後に、`Web.sitemap` ファイルにエントリとしてページを追加します。 具体的には、ページングと並べ替え `<siteMapNode>`の後に、次のマークアップを追加します。

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、チュートリアルの編集、挿入、および削除を行うための項目が含まれています。

![サイトマップにカスタムボタンチュートリアルのエントリが含まれるようになりました。](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**図 4**: サイトマップにカスタムボタンチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>手順 2: 仕入先を一覧表示する FormView を追加する

ここでは、サプライヤーを一覧表示する FormView を追加して、このチュートリアルを開始してみましょう。 概要で説明したように、この FormView を使用すると、サプライヤーによって提供される製品を GridView で表示することができます。 また、この FormView にはボタンが含まれています。このボタンをクリックすると、すべての仕入先の製品が廃止済みとしてマークされます。 FormView にカスタムボタンを追加することに関心がある前に、まず FormView を作成して、仕入先の情報が表示されるようにしましょう。

まず、`CustomButtons` フォルダーの [`CustomButtons.aspx`] ページを開きます。 FormView を [ツールボックス] からデザイナーにドラッグし、[`ID`] プロパティを [`Suppliers`] に設定して、FormView をページに追加します。 FormView のスマートタグから、`SuppliersDataSource`という名前の新しい ObjectDataSource を作成することを選択します。

[SuppliersDataSource という名前の新しい ObjectDataSource を作成 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**図 5**: `SuppliersDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png)される)

`SuppliersBLL` クラスの `GetSuppliers()` メソッドからクエリを行うように、この新しい ObjectDataSource を構成します (図6を参照)。 この FormView では supplier 情報を更新するためのインターフェイスが提供されないため、[更新] タブのドロップダウンリストから [(なし)] オプションを選択します。

[SuppliersBLL Class s GetSuppliers () メソッドを使用するようにデータソースを構成 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**図 6**: `SuppliersBLL` クラスの `GetSuppliers()` メソッドを使用するようにデータソースを構成する ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png)されます)

ObjectDataSource を構成すると、Visual Studio によって、FormView の `InsertItemTemplate`、`EditItemTemplate`、および `ItemTemplate` が生成されます。 `InsertItemTemplate` と `EditItemTemplate` を削除し、仕入先の会社名と電話番号だけを表示するように `ItemTemplate` を変更します。 最後に、[ページングを有効にする] チェックボックスをオンにして、FormView のページングサポートをオンにします (または、その `AllowPaging` プロパティを `True`に設定します)。 これらの変更が完了すると、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

図7は、ブラウザーを使用して表示するときの CustomButtons .aspx ページを示しています。

[FormView に ![現在選択されている業者からの CompanyName フィールドと Phone フィールドが一覧表示されます](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**図 7**: FormView には、現在選択されている業者の `CompanyName` および `Phone` のフィールドが一覧表示されます ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png)されます)

## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>手順 3: 選択した仕入先の製品を一覧表示する GridView の追加

FormView のテンプレートに [すべての製品の中止] ボタンを追加する前に、まず、選択した業者によって提供される製品を一覧表示する FormView の下に GridView を追加してみましょう。 これを行うには、GridView をページに追加し、その `ID` プロパティを `SuppliersProducts`に設定して、`SuppliersProductsDataSource`という名前の新しい ObjectDataSource を追加します。

[SuppliersProductsDataSource という名前の新しい ObjectDataSource を作成 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**図 8**: `SuppliersProductsDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png)される)

この ObjectDataSource を構成して、製品の Bll クラスの `GetProductsBySupplierID(supplierID)` メソッドを使用します (図9を参照)。 この GridView では、製品の価格を調整できますが、GridView の組み込みの編集機能または削除機能は使用されません。 そのため、ObjectDataSource の UPDATE、INSERT、DELETE の各タブでは、ドロップダウンリストを [(なし)] に設定できます。

[製品の Bll クラス s Get$ By仕入先 (仕入先) メソッドを使用するようにデータソースを構成 ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**図 9**: `ProductsBLL` クラスの `GetProductsBySupplierID(supplierID)` メソッドを使用するようにデータソースを構成する ([クリックしてフルサイズのイメージを表示する](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))

`GetProductsBySupplierID(supplierID)` メソッドは入力パラメーターを受け取るため、ObjectDataSource ウィザードでは、このパラメーター値のソースを要求するメッセージが表示されます。 FormView から `SupplierID` 値を渡すには、[パラメーターソース] ドロップダウンリストを [制御] に設定し、[ControlID] ドロップダウンリストを `Suppliers` (手順2で作成した FormView の ID) に設定します。

[![は、仕入先の FormView コントロールから、仕入先のパラメーターを取得する必要があることを示します。](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**図 10**: *`supplierID`* パラメーターが `Suppliers` FormView コントロールから取得される必要があることを示します ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png)されます)

ObjectDataSource ウィザードを完了すると、GridView には、各製品のデータフィールドの BoundField または CheckBoxField が含まれます。 ここで、`ProductName` と `UnitPrice` BoundFields を `Discontinued` CheckBoxField と共に表示するようにしてみましょう。さらに、テキストが通貨として書式設定されるように `UnitPrice` BoundField を書式設定してみましょう。 GridView と `SuppliersProductsDataSource` ObjectDataSource の宣言型マークアップは、次のマークアップのようになります。

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

この時点で、このチュートリアルではマスター/詳細レポートを表示します。ユーザーは、上部にある FormView からサプライヤーを選択し、下部にある GridView を通じて、その供給業者によって提供される製品を表示できます。 図11は、FormView から東京 Traders 社のサプライヤーを選択するときのこのページのスクリーンショットを示しています。

[選択した仕入先の製品が GridView に表示さ ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**図 11**: 選択した仕入先の製品が GridView に表示される ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png)されます)

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>手順 4: Supplier および BLL メソッドを作成して業者のすべての製品を中止する

FormView にボタンを追加する前に、クリックすると、すべての仕入先の製品が停止します。最初に、このアクションを実行する DAL と BLL の両方にメソッドを追加する必要があります。 特に、このメソッドには `DiscontinueAllProductsForSupplier(supplierID)`という名前が付けられます。 FormView のボタンをクリックすると、ビジネスロジック層でこのメソッドが呼び出され、選択した業者の `SupplierID`が渡されます。次に、BLL は対応するデータアクセス層メソッドにコールダウンします。これにより、指定した仕入先の製品を中断するデータベースに `UPDATE` ステートメントが発行されます。

前のチュートリアルで行ったように、まず、DAL メソッドを作成し、次に BLL メソッドを作成し、最後に ASP.NET ページに機能を実装します。 `App_Code/DAL` フォルダーの `Northwind.xsd` 型指定されたデータセットを開き、`ProductsTableAdapter` に新しいメソッドを追加します (`ProductsTableAdapter` を右クリックし、[クエリの追加] を選択します)。 これにより、TableAdapter クエリの構成ウィザードが表示されます。このウィザードでは、新しいメソッドを追加するプロセスについて説明します。 まず、DAL メソッドがアドホック SQL ステートメントを使用することを示します。

[アドホック SQL ステートメントを使用して DAL メソッドを作成 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**図 12**: アドホック SQL ステートメントを使用して DAL メソッドを作成[する (クリックすると、フルサイズのイメージが表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png)されます)

次に、ウィザードによって、作成するクエリの種類を入力するように求められます。 `DiscontinueAllProductsForSupplier(supplierID)` メソッドでは `Products` データベーステーブルを更新する必要があるため、`Discontinued` フィールドを1に設定し、指定した *`supplierID`* によって提供されるすべての製品について、データを更新するクエリを作成する必要があります。

[更新クエリの種類を選択 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**図 13**: 更新クエリの種類を選択[する (クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png)されます)

次のウィザード画面には、TableAdapter の既存の `UPDATE` ステートメントが用意されており、`Products` DataTable に定義されている各フィールドを更新します。 このクエリテキストを次のステートメントに置き換えます。

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

このクエリを入力して [次へ] をクリックすると、ウィザードの最後の画面が表示され、新しいメソッドの名前が `DiscontinueAllProductsForSupplier`に使用されます。 [完了] ボタンをクリックしてウィザードを完了します。 データセットデザイナーに戻ると、`DiscontinueAllProductsForSupplier(@SupplierID)`という名前の `ProductsTableAdapter` に新しいメソッドが表示されます。

[新しい DAL メソッド DiscontinueAllProductsForSupplier に名前を ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**図 14**: 新しい DAL メソッドに名前を指定[する `DiscontinueAllProductsForSupplier` (クリックしてフルサイズのイメージを表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))

データアクセス層で `DiscontinueAllProductsForSupplier(supplierID)` メソッドを作成した後、次のタスクでは、ビジネスロジック層で `DiscontinueAllProductsForSupplier(supplierID)` メソッドを作成します。 これを行うには、`ProductsBLL` クラスファイルを開き、次のように追加します。

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

このメソッドは、指定された *`supplierID`* パラメーター値を渡して、DAL 内の `DiscontinueAllProductsForSupplier(supplierID)` メソッドを単に呼び出します。 特定の状況で仕入先の製品を廃止することのみが許可されたビジネスルールがある場合は、そのルールを BLL に実装する必要があります。

> [!NOTE]
> `ProductsBLL` クラスの `UpdateProduct` のオーバーロードとは異なり、`DiscontinueAllProductsForSupplier(supplierID)` メソッドシグネチャには `DataObjectMethodAttribute` 属性 (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`) は含まれません。 これにより、[更新] タブの ObjectDataSource のデータソース構成ウィザードのドロップダウンリストの `DiscontinueAllProductsForSupplier(supplierID)` 方法ができません。ASP.NET のページでイベントハンドラーから `DiscontinueAllProductsForSupplier(supplierID)` メソッドを直接呼び出すため、この属性は省略しました。

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>手順 5: FormView に [すべての製品を中止] ボタンを追加する

BLL と DAL の `DiscontinueAllProductsForSupplier(supplierID)` メソッドを完了すると、選択した業者のすべての製品を中止する機能を追加する最後の手順として、FormView の `ItemTemplate`にボタン Web コントロールを追加します。 仕入先の電話番号の下にボタンテキストを追加して、すべての製品と `DiscontinueAllProductsForSupplier`の `ID` プロパティ値を中止してみましょう。 このボタン Web コントロールをデザイナーから追加するには、FormView のスマートタグの [テンプレートの編集] リンクをクリックするか (図15を参照)、または宣言型の構文を直接使用します。

[[すべての製品を中止] ボタン Web コントロールを FormView s ItemTemplate に追加 ![には](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**図 15**: [すべての製品を中止] ボタン Web コントロールを FormView の `ItemTemplate` に追加する ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png)されます)

ページにアクセスしているユーザーがボタンをクリックすると、ポストバック ensues と FormView の[`ItemCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx)が発生します。 このボタンがクリックされたときの応答でカスタムコードを実行するには、このイベントのイベントハンドラーを作成します。 ただし、FormView 内*でボタン、* LinkButton、または ImageButton Web コントロールがクリックされるたびに、`ItemCommand` イベントが発生することを理解してください。 つまり、ユーザーが FormView 内のあるページから別のページに移動すると、`ItemCommand` イベントが発生します。挿入、更新、または削除をサポートする FormView で、ユーザーが [新規]、[編集]、または [削除] をクリックしたときにも同じことが言えます。

`ItemCommand` はどのボタンがクリックされたかに関係なく起動されるため、イベントハンドラーでは、[すべての製品を中止] ボタンがクリックされたかどうか、または他のボタンであるかどうかを確認する方法が必要になります。 これを実現するには、ボタン Web コントロールの `CommandName` プロパティを特定の値に設定します。 このボタンをクリックすると、この `CommandName` 値が `ItemCommand` イベントハンドラーに渡され、[すべての製品を中止] ボタンがクリックされたかどうかを確認できるようになります。 [すべての製品を中止] ボタンの `CommandName` プロパティを DiscontinueProducts に設定します。

最後に、クライアント側の [確認] ダイアログボックスを使用して、ユーザーが選択した業者の製品を本当に停止することを確認します。 チュートリアル「[削除時のクライアント側の確認を追加する](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md)」で説明したように、これは少しの JavaScript で実現できます。 特に、ボタン Web コントロールの OnClientClick プロパティを `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');` に設定します。

これらの変更を行った後、FormView の宣言構文は次のようになります。

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

次に、FormView の `ItemCommand` イベントのイベントハンドラーを作成します。 このイベントハンドラーでは、最初に [すべての製品を中止] ボタンがクリックされたかどうかを確認する必要があります。 そのような場合は、`ProductsBLL` クラスのインスタンスを作成し、その `DiscontinueAllProductsForSupplier(supplierID)` メソッドを呼び出して、選択した FormView の `SupplierID` を渡します。

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

FormView の[`SelectedValue` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)を使用して、formview で現在選択されている業者の `SupplierID` にアクセスできることに注意してください。 `SelectedValue` プロパティは、FormView に表示されるレコードの最初のデータキー値を返します。 FormView の[`DataKeyNames` プロパティ](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)は、データキー値の取得元のデータフィールドを示します。これは、手順 2. で ObjectDataSource を FormView にバインドするときに、Visual Studio によって自動的に `SupplierID` するように設定されています。

`ItemCommand` イベントハンドラーが作成されたら、しばらく時間を取ってページをテストします。 Cooperativa de Quesos ' ラスベガス ' のサプライヤー (FormView の5番目のサプライヤー) に移動します。 このサプライヤーは、Queso Cabrales と Queso Manの両方の製品を提供しています。どちらも廃止され*ていません*。

Cooperativa de Quesos ' ラスベガスがビジネスを終了し、その製品を廃止することを想像してください。 [すべての製品を中止] ボタンをクリックします。 これにより、[クライアント側の確認] ダイアログボックスが表示されます (図16を参照)。

[![Cooperativa de Quesos のラスベガスが2つのアクティブな製品を提供する](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**図 16**: Cooperativa De Quesos のラスベガスで2つのアクティブな製品が提供される ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png)される)

[クライアント側の確認] ダイアログボックスで [OK] をクリックすると、フォームの送信が続行され、FormView の `ItemCommand` イベントが発生するポストバックが発生します。 次に、作成したイベントハンドラーが実行され、`DiscontinueAllProductsForSupplier(supplierID)` メソッドが呼び出され、Queso Cabrales と Queso Manの両方の製品が中止されます。

GridView のビューステートを無効にした場合、GridView はすべてのポストバックの基になるデータストアに再バインドされるため、この2つの製品が廃止されたことを反映してすぐに更新されます (図17を参照)。 ただし、GridView でビューステートが無効になっていない場合は、この変更を行った後、データを GridView に手動で再バインドする必要があります。 これを実現するには、`DiscontinueAllProductsForSupplier(supplierID)` メソッドを呼び出した直後に GridView の `DataBind()` メソッドを呼び出す必要があります。

[[すべての製品を中止] ボタンをクリックした後 ![、仕入先の製品がそれに応じて更新されます。](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**図 17**: [すべての製品を中止] ボタンをクリックすると、仕入先の製品がそれに応じて更新されます ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png)されます)

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>手順 6: 製品の価格を調整するためのビジネスロジック層での UpdateProduct オーバーロードの作成

FormView の [すべての製品を中止] ボタンと同様に、GridView で製品の価格を増減するボタンを追加するには、最初に適切なデータアクセス層とビジネスロジック層のメソッドを追加する必要があります。 DAL の1つの製品行を更新するメソッドが既にあるため、BLL の `UpdateProduct` メソッドに新しいオーバーロードを作成することによって、そのような機能を提供できます。

過去の `UpdateProduct` のオーバーロードは、一部の製品フィールドをスカラー入力値として取得し、指定された製品のフィールドだけを更新しました。 このオーバーロードでは、この標準とは若干異なります。代わりに、製品の `ProductID` と、`UnitPrice` の調整に使用する割合 (新しい、調整された `UnitPrice` 自体に渡すのではなく) を渡します。 この方法では、現在の製品の `UnitPrice`を決定する必要がないため、ASP.NET page 分離コードクラスで記述する必要があるコードが簡略化されます。

このチュートリアルの `UpdateProduct` のオーバーロードを次に示します。

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

このオーバーロードは、DAL の `GetProductByProductID(productID)` メソッドを使用して、指定された製品に関する情報を取得します。 次に、製品の `UnitPrice` にデータベース `NULL` 値が割り当てられているかどうかを確認します。 その場合、価格は変更されません。 ただし、`NULL` 以外の `UnitPrice` 値がある場合、メソッドは、指定されたパーセント (`unitPriceAdjustmentPercent`) で製品の `UnitPrice` を更新します。

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>手順 7: GridView に [拡大] ボタンと [縮小] ボタンを追加する

GridView (および DetailsView) は、両方ともフィールドのコレクションで構成されています。 BoundFields、CheckBoxFields、および TemplateFields に加えて、ASP.NET には ButtonField が含まれています。これは、その名前が示すとおり、各行のボタン、LinkButton、または ImageButton を持つ列として表示されます。 FormView と同様に、GridView ページングボタン内の*いずれか*のボタンをクリックする、ボタンの編集または削除、並べ替えボタンなどを行うと、ポストバックが発生し、gridview の[`RowCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)が発生します。

ButtonField には、`CommandName` プロパティの各ボタンに指定された値を割り当てる `CommandName` プロパティがあります。 FormView と同様に、`CommandName` 値は、クリックされたボタンを判断するために `RowCommand` イベントハンドラーによって使用されます。

GridView に2つの新しい ButtonFields を追加します。1つはボタンテキスト価格 + 10%、もう1つはテキスト価格で10% です。 これらの ButtonFields を追加するには、GridView のスマートタグから [列の編集] リンクをクリックし、左上の一覧から Buttonfields フィールドの種類を選択して、[追加] ボタンをクリックします。

![GridView に2つの ButtonFields を追加する](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**図 18**: GridView に2つの buttonfields を追加する

2つの ButtonFields を移動して、最初の2つの GridView フィールドとして表示されるようにします。 次に、これら2つの ButtonFields の `Text` プロパティを Price + 10% および Price-10% に設定し、`CommandName` プロパティを IncreasePrice と DecreasePrice にそれぞれ設定します。 既定では、ButtonField はボタンの列をリンクボタンとしてレンダリングします。 ただし、これは、ButtonField の[`ButtonType` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)を使用して変更できます。 これらの2つの ButtonFields を通常のプッシュボタンとしてレンダリングしてみましょう。したがって、`ButtonType` プロパティを `Button`に設定します。 図19は、これらの変更が加えられた後の [フィールド] ダイアログボックスを示しています。次に、GridView の宣言型マークアップを示します。

![ButtonFields Text、CommandName、およびです (buttontype の各プロパティの構成](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**図 19**: buttonfields `Text`、`CommandName`、および `ButtonType` の各プロパティを構成する

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

これらの ButtonFields を作成したら、最後の手順として、GridView の `RowCommand` イベントのイベントハンドラーを作成します。 このイベントハンドラーは、Price + 10% または Price-10% のボタンがクリックされたことが原因で発生した場合、によって、ボタンがクリックされた行の `ProductID` を判断し、`ProductsBLL` クラスの `UpdateProduct` メソッドを呼び出して、`ProductID`と共に適切な `UnitPrice` 比率の調整を渡す必要があります。 次のコードでは、これらのタスクを実行します。

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

Price + 10% または Price-10% のボタンがクリックされた行の `ProductID` を確認するには、GridView の `DataKeys` コレクションを参照する必要があります。 このコレクションは、各 GridView 行の `DataKeyNames` プロパティに指定されているフィールドの値を保持します。 ObjectDataSource を GridView にバインドするときに、GridView の `DataKeyNames` プロパティが Visual Studio によって ProductID に設定されているため、`DataKeys(rowIndex).Value` 指定された*rowIndex*の `ProductID` が提供されます。

ButtonField は、`e.CommandArgument` パラメーターを通じてボタンがクリックされた行の*rowIndex*を自動的に渡します。 そのため、Price + 10% または Price-10% のボタンをクリックした行の `ProductID` を確認するには、次のように使用します: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`。

[すべての製品を中止] ボタンと同様に、GridView のビューステートを無効にした場合、GridView はすべてのポストバックの基になるデータストアに再バインドされます。そのため、クリックしたときに発生した価格の変化を反映するように、直ちに更新されます。いずれかのボタン。 ただし、GridView でビューステートが無効になっていない場合は、この変更を行った後、データを GridView に手動で再バインドする必要があります。 これを実現するには、`UpdateProduct` メソッドを呼び出した直後に GridView の `DataBind()` メソッドを呼び出す必要があります。

図20は、おばあちゃん友野 's Homestead によって提供される製品を表示するときのページを示しています。 図21は、おばあちゃんの Boysenberry 拡散に対して Price + 10% ボタンを2回クリックした後の結果を示しています。 Northwoods Cranberry ソースの場合は、1回の価格-10% ボタンをクリックします。

[GridView に Price + 10% と Price-10% のボタンが含まれている ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**図 20**: GridView には、price + 10% および price-10% のボタンが含まれています ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png)されます)

[1番目と3番目の製品の価格は、[価格 + 10%] ボタンと [Price-10%] ボタンによって更新されてい ![](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**図 21**: 1 番目と3番目の製品の価格が価格 + 10% と料金10% のボタンで更新されました ([クリックすると、フルサイズの画像が表示](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png)されます)

> [!NOTE]
> GridView (および DetailsView) には、TemplateFields にボタン、リンクボタン、または ImageButtons を追加することもできます。 BoundField の場合と同様に、これらのボタンをクリックするとポストバックが実行され、GridView の `RowCommand` イベントが発生します。 ただし、TemplateField にボタンを追加する場合、ボタンの `CommandArgument` は、ButtonFields を使用する場合と同様に、行のインデックスに自動的に設定されません。 `RowCommand` イベントハンドラー内でクリックされたボタンの行インデックスを調べる必要がある場合は、次のようなコードを使用して、TemplateField 内の宣言構文でボタンの `CommandArgument` プロパティを手動で設定する必要があります。  
> [https://login.microsoftonline.com/consumers/](`<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`)

## <a name="summary"></a>まとめ

GridView、DetailsView、および FormView コントロールには、ボタン、リンクボタン、または ImageButtons を含めることができます。 このようなボタンをクリックすると、ポストバックが発生し、FormView および DetailsView コントロールと GridView の `RowCommand` イベントで `ItemCommand` イベントが発生します。 これらのデータ Web コントロールには、レコードの削除や編集など、コマンドに関連する一般的な操作を処理するための機能が組み込まれています。 ただし、ボタンをクリックすると、独自のカスタムコードを実行して応答することもできます。

これを実現するには、`ItemCommand` イベントまたは `RowCommand` イベントのイベントハンドラーを作成する必要があります。 このイベントハンドラーでは、最初に受信 `CommandName` 値を確認して、クリックされたボタンを特定し、適切なカスタムアクションを実行します。 このチュートリアルでは、ボタンと ButtonFields を使用して、指定された業者のすべての製品を中止する方法、または特定の製品の価格を10% 増減する方法について説明しました。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [Next](adding-and-responding-to-buttons-to-a-gridview-vb.md)
