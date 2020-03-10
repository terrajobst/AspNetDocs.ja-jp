---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: DataTable 列を追加する (VB) |Microsoft Docs
author: rick-anderson
description: TableAdapter ウィザードを使用して型指定されたデータセットを作成する場合、対応する DataTable には、メインデータベースクエリによって返される列が含まれます。 しかし、
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: 3a55f8bc4d3508387927ca81674073a001867de7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78429100"
---
# <a name="adding-additional-datatable-columns-vb"></a>その他の DataTable 列を追加する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip)または[PDF のダウンロード](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> TableAdapter ウィザードを使用して型指定されたデータセットを作成する場合、対応する DataTable には、メインデータベースクエリによって返される列が含まれます。 ただし、DataTable に追加の列を含める必要がある場合もあります。 このチュートリアルでは、追加の DataTable 列が必要な場合に、ストアドプロシージャを推奨する理由について説明します。

## <a name="introduction"></a>はじめに

型指定されたデータセットに TableAdapter を追加する場合、対応する DataTable s スキーマは TableAdapter のメインクエリによって決定されます。 たとえば、メインクエリからデータフィールド*a*、 *b*、および*c*が返される場合、DataTable には、a、 *b*、および*c*という3つ*の*対応する列があります。TableAdapter には、メインのクエリに加えて、いくつかのパラメーターに基づいてデータのサブセットを返す追加のクエリを含めることができます。 たとえば、すべての製品に関する情報を返す `ProductsTableAdapter` s メインクエリに加えて、指定されたパラメーターに基づいて特定の製品情報を返す `GetProductsByCategoryID(categoryID)` や `GetProductByProductID(productID)`などのメソッドも含まれています。

DataTable s スキーマが TableAdapter s メインクエリを反映するモデルは、すべての TableAdapter のメソッドが、メインクエリで指定されたデータフィールドと同じかそれよりも少数のデータフィールドを返す場合に適しています。 TableAdapter メソッドが追加のデータフィールドを返す必要がある場合は、それに応じて DataTable s スキーマを展開する必要があります。 [「詳細を含むマスターレコードの箇条書きリストを使用したマスター/詳細](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)」では、メイン `NumberOfProducts`クエリに定義されている `CategoryID`、`CategoryName`、および `Description` のデータフィールドを返す `CategoriesTableAdapter` にメソッドを追加し、各カテゴリに関連付けられている製品の数を報告する追加のデータフィールドを追加しました。 この新しいメソッドから `NumberOfProducts` データフィールドの値を取得するために、`CategoriesDataTable` に新しい列を手動で追加しました。

[ファイルのアップロード](../working-with-binary-files/uploading-files-vb.md)に関するチュートリアルで説明したように、アドホック SQL ステートメントを使用し、データフィールドがメインクエリと正確に一致しないメソッドがある tableadapter を使用して、細心の注意を払う必要があります。 TableAdapter 構成ウィザードを再実行すると、すべての TableAdapter のメソッドが更新され、データフィールドの一覧がメインクエリと一致するようになります。 その結果、列リストがカスタマイズされたすべてのメソッドは、メインクエリの列リストに戻り、予想されるデータを返しません。 この問題は、ストアドプロシージャを使用する場合には発生しません。

このチュートリアルでは、DataTable s スキーマを拡張して列を追加する方法について説明します。 このチュートリアルでは、アドホック SQL ステートメントを使用するときの TableAdapter の高まるにより、ストアドプロシージャを使用します。 ストアドプロシージャを使用するように TableAdapter を構成する方法の詳細については、「型指定された[データセットの tableadapter 用に新しいストアドプロシージャを作成](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)する」および[「型指定](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)されたデータセットの tableadapter のチュートリアル」を参照してください。

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>手順 1:`ProductsDataTable` に`PriceQuartile`列を追加する

「*型指定されたデータセットの tableadapter 用の新しいストアドプロシージャの作成*」チュートリアルでは、`NorthwindWithSprocs`という名前の型指定されたデータセットを作成しました。 現在、このデータセットには、`ProductsDataTable` と `EmployeesDataTable`の2つの Datatable が含まれています。 `ProductsTableAdapter` には、次の3つの方法があります。

- `GetProducts`-`Products` テーブルからすべてのレコードを返すメインクエリ
- `GetProductsByCategoryID(categoryID)`-指定された*categoryID*を持つすべての製品を返します。
- `GetProductByProductID(productID)`-指定された*productID*を持つ特定の製品を返します。

メインクエリと2つの追加のメソッドはすべて、同じデータフィールドのセットを返します。つまり、`Products` テーブルのすべての列が返されます。 相関サブクエリが存在しないか、`Categories` または `Suppliers` テーブルから関連データをプルして `JOIN`。 したがって、`ProductsDataTable` には、`Products` テーブル内の各フィールドに対応する列があります。

このチュートリアルでは、を使用して、すべての製品を返す `GetProductsWithPriceQuartile` という名前の `ProductsTableAdapter` にメソッドを追加します。 標準の製品データフィールドに加えて、`GetProductsWithPriceQuartile` には、製品の価格がどの四分の値に分類されるかを示す `PriceQuartile` データフィールドも含まれます。 たとえば、価格が最も高価な25% の製品には `PriceQuartile` の値1が割り当てられ、下位25% に価格が設定されている製品の値は4になります。 ただし、この情報を返すストアドプロシージャを作成することを心配する前に、まず、`ProductsDataTable` を更新して、`GetProductsWithPriceQuartile` メソッドが使用されたときに `PriceQuartile` の結果を保持する列を含める必要があります。

`NorthwindWithSprocs` データセットを開き、`ProductsDataTable`を右クリックします。 コンテキストメニューの [追加] をクリックし、[列] を選択します。

[製品の Datatable に新しい列を追加 ![には](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**図 1**: `ProductsDataTable` に新しい列を追加する ([クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image3.png)されます)

これにより、`System.String`型の Column1 という名前の DataTable に新しい列が追加されます。 この列の名前を PriceQuartile に、その型を `System.Int32` に更新する必要があります。これは、1 ~ 4 の数値を保持するために使用されるためです。 `ProductsDataTable` で新しく追加された列を選択し、プロパティウィンドウの [`Name`] プロパティを [PriceQuartile] に設定し、[`DataType`] プロパティを [`System.Int32`] に設定します。

[新しい列の Name プロパティと DataType プロパティを設定 ![には](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**図 2**: 新しい列の `Name` と `DataType` プロパティの設定 ([クリックしてフルサイズの画像を表示](adding-additional-datatable-columns-vb/_static/image6.png))

図2に示すように、設定できる追加のプロパティがあります。たとえば、列の値が一意である必要があるかどうか、列が自動インクリメント列であるかどうか、データベース `NULL` 値が許可されているかどうかなどです。 これらの値は既定値のままにしておきます。

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>手順 2:`GetProductsWithPriceQuartile`メソッドの作成

`PriceQuartile` 列を含むように `ProductsDataTable` が更新されたので、`GetProductsWithPriceQuartile` メソッドを作成する準備が整いました。 まず、TableAdapter を右クリックし、コンテキストメニューから [クエリの追加] を選択します。 これにより、TableAdapter クエリの構成ウィザードが起動します。このウィザードでは、アドホック SQL ステートメントと新規または既存のストアドプロシージャのどちらを使用するかを確認するメッセージが最初に表示されます。 価格の四分位データを返すストアドプロシージャはまだありません。そのため、では、TableAdapter によってこのストアドプロシージャを作成することが許可されています。 [新しいストアドプロシージャの作成] オプションを選択し、[次へ] をクリックします。

[![、TableAdapter ウィザードでストアドプロシージャを作成するように指示します。](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**図 3**: TableAdapter ウィザードを使用して、ストアドプロシージャを作成するように指示する ([クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image9.png)されます)

図4に示されている後続の画面では、ウィザードによって、追加するクエリの種類が表示されます。 `GetProductsWithPriceQuartile` メソッドは `Products` テーブルからすべての列とレコードを返すため、[行を返す] オプションを選択し、[次へ] をクリックします。

[クエリが複数行を返す SELECT ステートメントになる ![](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**図 4**: クエリは複数の行を返す `SELECT` ステートメントです ([クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image12.png)されます)

次に、`SELECT` クエリを入力するように求められます。 ウィザードに次のクエリを入力します。

[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

上記のクエリでは、SQL Server 2005 s new [`NTILE` 関数](https://msdn.microsoft.com/library/ms175126.aspx)を使用して、結果を4つのグループに分割しています。このグループは、`UnitPrice` 値によって降順に並べ替えられています。

残念ながら、クエリビルダーでは、`OVER` キーワードを解析する方法がわからず、上記のクエリの解析時にエラーが表示されます。 そのため、クエリビルダーを使用せずに、ウィザードのテキストボックスに上記のクエリを直接入力します。

> [!NOTE]
> NTILE および SQL Server 2005 s その他の順位付け関数の詳細については、 [SQL Server 2005 オンラインブック](https://msdn.microsoft.com/library/ms189798.aspx)の「 [Microsoft SQL Server 2005 を使用](http://www.4guysfromrolla.com/webtech/010406-1.shtml)して順位付けされた結果を返す」および「[順位付け関数」](https://msdn.microsoft.com/library/ms189798.aspx)を参照してください。

`SELECT` クエリを入力して [次へ] をクリックすると、ウィザードによって作成されるストアドプロシージャの名前を入力するように求められます。 新しいストアドプロシージャに `Products_SelectWithPriceQuartile` という名前を指定し、[次へ] をクリックします。

[ストアドプロシージャの名前を ![Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**図 5**: ストアドプロシージャの名前を `Products_SelectWithPriceQuartile`[にする (クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image15.png)されます)

最後に、TableAdapter メソッドに名前を指定するように求められます。 [DataTable にデータを格納し、DataTable を返す] チェックボックスをオンのままにして、メソッドの名前を `FillWithPriceQuartile` と `GetProductsWithPriceQuartile`にします。

[TableAdapter のメソッドに名前を ![、[完了] をクリックします。](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**図 6**: TableAdapter のメソッドに名前を指定し、[完了][をクリックする (クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image18.png)されます)

`SELECT` のクエリを指定し、ストアドプロシージャと TableAdapter メソッドをと共に使用して、[完了] をクリックしてウィザードを完了します。 この時点で、`OVER` SQL コンストラクトまたはステートメントがサポートされていないことを示す警告がウィザードから表示されることがあります。 これらの警告は無視してかまいません。

ウィザードが完了したら、TableAdapter に `FillWithPriceQuartile` メソッドと `GetProductsWithPriceQuartile` メソッドを含め、データベースに `Products_SelectWithPriceQuartile`という名前のストアドプロシージャを含める必要があります。 この新しいメソッドが TableAdapter に実際に含まれていること、およびストアドプロシージャがデータベースに正しく追加されていることを確認します。 データベースをチェックするときに、ストアドプロシージャが表示されない場合は、[ストアドプロシージャ] フォルダーを右クリックして [最新の状態に更新] をクリックします。

![新しいメソッドが TableAdapter に追加されたことを確認する](adding-additional-datatable-columns-vb/_static/image19.png)

**図 7**: 新しいメソッドが TableAdapter に追加されたことを確認する

[![データベースに Products_SelectWithPriceQuartile ストアドプロシージャが含まれていることを確認する](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**図 8**: データベースに `Products_SelectWithPriceQuartile` ストアドプロシージャが含まれていることを確認[する (クリックしてフルサイズの画像を表示する](adding-additional-datatable-columns-vb/_static/image22.png))

> [!NOTE]
> アドホック SQL ステートメントの代わりにストアドプロシージャを使用する利点の1つは、TableAdapter 構成ウィザードを再実行しても、[ストアドプロシージャ] 列の一覧が変更されないことです。 これを確認するには、TableAdapter を右クリックし、コンテキストメニューから [構成] オプションを選択してウィザードを起動し、[完了] をクリックして完了します。 次に、データベースにアクセスし、`Products_SelectWithPriceQuartile` ストアドプロシージャを表示します。 列リストが変更されていないことに注意してください。 アドホック SQL ステートメントを使用していたので、TableAdapter 構成ウィザードを再実行すると、メインクエリ列リストに一致するようにこのクエリの列リストが元に戻され、`GetProductsWithPriceQuartile` メソッドによって使用されるクエリから NTILE ステートメントが削除されます。

データアクセス層 s `GetProductsWithPriceQuartile` メソッドが呼び出されると、TableAdapter は `Products_SelectWithPriceQuartile` ストアドプロシージャを実行し、返された各レコードの `ProductsDataTable` に行を追加します。 ストアドプロシージャによって返されるデータフィールドは、`ProductsDataTable` s 列にマップされます。 ストアドプロシージャから返される `PriceQuartile` データフィールドがあるため、その値は `ProductsDataTable` s `PriceQuartile` 列に割り当てられます。

クエリによって `PriceQuartile` データフィールドが返されない TableAdapter メソッドの場合、`PriceQuartile` 列の値はその `DefaultValue` プロパティによって指定された値になります。 図2に示すように、この値は `DBNull`(既定) に設定されています。 別の既定値を使用する場合は、`DefaultValue` プロパティを適宜設定します。 列 `DataType` (つまり、`PriceQuartile` 列の `System.Int32`) によって `DefaultValue` 値が有効であることを確認してください。

この時点で、DataTable に列を追加するために必要な手順を実行しました。 この追加列が想定どおりに動作することを確認するには、ASP.NET ページを作成して、各製品の名前、価格、および価格の四分の1を表示します。 ただし、その前に、最初にビジネスロジックレイヤーを更新して、DAL の `GetProductsWithPriceQuartile` メソッドを呼び出すメソッドを含める必要があります。 次に、手順 3. で [BLL] を更新してから、手順4で ASP.NET ページを作成します。

## <a name="step-3-augmenting-the-business-logic-layer"></a>手順 3: ビジネスロジック層を補強する

プレゼンテーション層から新しい `GetProductsWithPriceQuartile` メソッドを使用する前に、まず、対応するメソッドを BLL に追加する必要があります。 `ProductsBLLWithSprocs` クラスファイルを開き、次のコードを追加します。

[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

`ProductsBLLWithSprocs`の他のデータ取得メソッドと同様に、`GetProductsWithPriceQuartile` メソッドは単に、対応する `GetProductsWithPriceQuartile` メソッドを呼び出し、その結果を返します。

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>手順 4: ASP.NET Web ページで価格の四分の情報を表示する

BLL の追加が完了したら、各製品の価格の ASP.NET を示すページを作成します。 `AdvancedDAL` フォルダーの [`AddingColumns.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグし、`ID` プロパティを [`Products`] に設定します。 GridView s スマートタグから、`ProductsDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLLWithSprocs` クラス s `GetProductsWithPriceQuartile` メソッドを使用するように ObjectDataSource を構成します。 これは読み取り専用であるため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[製品 Bllwithsproc クラスを使用するように ObjectDataSource を構成 ![には](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**図 9**: `ProductsBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](adding-additional-datatable-columns-vb/_static/image25.png))

[GetProductsWithPriceQuartile メソッドから製品情報を取得 ![には](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**図 10**: `GetProductsWithPriceQuartile` メソッドから製品情報[を取得する (クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image28.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、メソッドによって返される各データフィールドの GridView に BoundField または CheckBoxField が自動的に追加されます。 これらのデータフィールドの1つは `PriceQuartile`です。これは、手順 1. で `ProductsDataTable` に追加した列です。

GridView のフィールドを編集し、`ProductName`、`UnitPrice`、および `PriceQuartile` BoundFields 以外はすべて削除します。 `UnitPrice` BoundField を構成して、その値を通貨として書式設定し、`UnitPrice` と `PriceQuartile` BoundFields をそれぞれ右および中央揃えに設定します。 最後に、残りの BoundFields `HeaderText` プロパティを、それぞれ製品、価格、価格の4分の4に更新します。 また、GridView s スマートタグの [並べ替えを有効にする] チェックボックスをオンにします。

これらの変更を加えた後、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

図11は、ブラウザーを使用してアクセスしたときのこのページを示しています。 初期状態では、各製品に適切な `PriceQuartile` 値が割り当てられ、製品の価格が降順で並べ替えられていることに注意してください。 もちろん、このデータは他の条件で並べ替えることができます。価格の四分の列の値は、価格に関して製品のランク付けを反映しています (図12を参照)。

[製品が価格順に並べられている ![](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**図 11**: 製品が価格順に並べられている ([クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image31.png)されます)

[製品が名前順に並んでいる ![](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**図 12**: 製品は名前順に並んでいます ([クリックすると、フルサイズの画像が表示](adding-additional-datatable-columns-vb/_static/image34.png)されます)

> [!NOTE]
> 数行のコードを使用して、`PriceQuartile` 値に基づいて製品の行を色分けするように GridView を拡張することができます。 これらの製品については、最初の4分の1番目の四分位に色を設定します。 この機能を追加することをお勧めします。 GridView の書式設定に関するリフレッシャーが必要な場合は、「[データに基づくカスタム書式](../custom-formatting/custom-formatting-based-upon-data-vb.md)設定」チュートリアルを参照してください。

## <a name="an-alternative-approach---creating-another-tableadapter"></a>別の方法-別の TableAdapter の作成

このチュートリアルで説明したように、メインクエリでスペルが指定されていないデータフィールドを返す TableAdapter にメソッドを追加する場合、対応する列を DataTable に追加できます。 ただし、このような方法は、異なるデータフィールドを返す TableAdapter 内のメソッドの数が少ない場合や、それらの代替データフィールドがメインクエリによって大きく変化しない場合にのみ適しています。

列を DataTable に追加するのではなく、別のデータフィールドを返す最初の TableAdapter のメソッドを含むデータセットに別の TableAdapter を追加することができます。 このチュートリアルでは、`ProductsDataTable` (`GetProductsWithPriceQuartile` メソッドによってのみ使用されます) に `PriceQuartile` 列を追加するのではなく、`Products_SelectWithPriceQuartile` ストアドプロシージャをメインクエリとして使用した `ProductsWithPriceQuartileTableAdapter` という名前のデータセットに、追加の TableAdapter を追加することができます。 価格の ASP.NET に製品情報を取得するために必要なページには、`ProductsWithPriceQuartileTableAdapter`が使用されていますが、`ProductsTableAdapter`の使用を継続できませんでした。

新しい TableAdapter を追加することにより、Datatable は untarnished を維持し、その列には TableAdapter のメソッドによって返されるデータフィールドが正確に反映されます。 ただし、追加の Tableadapter によって、反復的なタスクと機能が導入される場合があります。 たとえば、`PriceQuartile` 列を表示するこれらの ASP.NET ページにも、挿入、更新、および削除のサポートが必要な場合、`ProductsWithPriceQuartileTableAdapter` には、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティが正しく構成されている必要があります。 これらのプロパティは `ProductsTableAdapter` をミラー化しますが、この構成では追加の手順が導入されます。 さらに、データベースに対して製品を更新、削除、または追加するには、`ProductsTableAdapter` と `ProductsWithPriceQuartileTableAdapter` のクラスを使用する2つの方法があります。

このチュートリアルのダウンロードには、この代替アプローチを示す `ProductsWithPriceQuartileTableAdapter` クラスが `NorthwindWithSprocs` データセットに含まれています。

## <a name="summary"></a>まとめ

ほとんどのシナリオでは、TableAdapter 内のすべてのメソッドは同じデータフィールドのセットを返しますが、特定のメソッドまたは2が追加のフィールドを返す必要がある場合もあります。 たとえば、マスター[レコードの箇条書きリストを使用した、詳細データを含むマスターレコードの一覧を使用したマスター/詳細](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)のチュートリアルでは、`CategoriesTableAdapter` にメソッドを追加しました。このメソッドは、メインクエリ s のデータフィールドに加えて、各カテゴリに関連付けられている製品の数を報告する `NumberOfProducts` フィールドを返しました。 このチュートリアルでは、メインのクエリ s データフィールドに加えて、`PriceQuartile` フィールドを返す `ProductsTableAdapter` にメソッドを追加する方法を説明しました。 TableAdapter のメソッドによって返された追加のデータフィールドを取得するには、対応する列を DataTable に追加する必要があります。

DataTable に列を手動で追加する予定の場合は、TableAdapter でストアドプロシージャを使用することをお勧めします。 TableAdapter がアドホック SQL ステートメントを使用する場合、TableAdapter 構成ウィザードを実行するたびに、すべてのメソッドのデータフィールドリストがメインクエリによって返されるデータフィールドに戻されます。 この問題は、ストアドプロシージャには適用されません。そのため、このチュートリアルでは、この問題を使用することをお勧めします。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Randy/Jacky Goor、Bernadette Leigh、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](updating-the-tableadapter-to-use-joins-vb.md)
> [次へ](working-with-computed-columns-vb.md)
