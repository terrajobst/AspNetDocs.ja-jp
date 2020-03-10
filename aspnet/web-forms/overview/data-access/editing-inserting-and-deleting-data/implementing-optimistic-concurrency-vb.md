---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb
title: オプティミスティック同時実行制御の実装 (VB) |Microsoft Docs
author: rick-anderson
description: 複数のユーザーがデータを編集できるようにする web アプリケーションの場合、2人のユーザーが同時に同じデータを編集するというリスクがあります。 この tutori では、
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2646968c-2826-4418-b1d0-62610ed177e3
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb
msc.type: authoredcontent
ms.openlocfilehash: 28c39fe2a290cc3a5b093fdd09de341630606137
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78492364"
---
# <a name="implementing-optimistic-concurrency-vb"></a>オプティミスティック同時実行制御を実装する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_VB.exe)または[PDF のダウンロード](implementing-optimistic-concurrency-vb/_static/datatutorial21vb1.pdf)

> 複数のユーザーがデータを編集できるようにする web アプリケーションの場合、2人のユーザーが同時に同じデータを編集するというリスクがあります。 このチュートリアルでは、オプティミスティック同時実行制御を実装して、このリスクを処理します。

## <a name="introduction"></a>はじめに

データの表示のみを許可する web アプリケーションの場合、またはデータを変更できる1人のユーザーのみを含む web アプリケーションの場合、2人のユーザーが別の変更を誤って上書きしても、脅威は発生しません。 複数のユーザーがデータを更新または削除できるようにする web アプリケーションの場合、1人のユーザーが別の同時実行ユーザーと競合する可能性があります。 同時実行ポリシーが設定されていない場合、2人のユーザーが同時に1つのレコードを編集すると、その変更をコミットしたユーザーは、最初に行った変更を上書きします。

たとえば、Jisun と Sam という2人のユーザーがアプリケーションのページにアクセスし、その後、ユーザーが GridView コントロールを使用して製品を更新および削除できるとします。 両方とも、GridView の [編集] ボタンをクリックします。 Jisun は製品名を "Chai 紅茶" に変更し、[更新] ボタンをクリックします。 結果として、データベースに送信される `UPDATE` ステートメントがあります。これにより、*すべて*の製品の更新可能フィールドが設定されます (Jisun によって1つのフィールドが更新された場合でも、`ProductName`)。 この時点で、この特定の製品について、データベースの値は "Chai 紅茶"、カテゴリ飲み物、業者の特別な液体などです。 ただし、Sam の画面の GridView でも、編集可能な GridView 行の製品名は "Chai" として表示されます。 Jisun の変更がコミットされてから数秒後に、Sam はカテゴリを Condiments に更新し、[更新] をクリックします。 これにより、製品名を "Chai" に設定する `UPDATE` ステートメントがデータベースに送信され、対応する飲料カテゴリ ID に `CategoryID` ます。 製品名に対する jisun の変更が上書きされました。 図1に、この一連のイベントをグラフィカルに示します。

[2人のユーザーが同時にレコードを更新したときに、1人のユーザーの変更によって他のユーザーが上書きされる可能性がある ![](implementing-optimistic-concurrency-vb/_static/image2.png)](implementing-optimistic-concurrency-vb/_static/image1.png)

**図 1**: 2 人のユーザーが同時にレコードを更新する場合、1人のユーザーの変更によって他のが上書きされる可能性があります ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image3.png)されます)。

同様に、2人のユーザーが1ページにアクセスしたときに、あるユーザーが別のユーザーによって削除されたレコードを更新しようとしている場合があります。 または、ユーザーがページを読み込んだときに、[削除] ボタンをクリックしたときに、別のユーザーがそのレコードの内容を変更した可能性があります。

次の3つの[同時実行制御](http://en.wikipedia.org/wiki/Concurrency_control)戦略を使用できます。

- **何もしない**-同時実行ユーザーが同じレコードを変更している場合は、最後のコミットを優先します (既定の動作)。
- [**オプティミスティック同時実行制御**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)-現時点で同時実行の競合が発生する可能性はありますが、そのような競合が発生することはほとんどありません。そのため、競合が発生した場合は、別のユーザーが同じデータを変更したため、変更を保存できないことをユーザーに通知するだけです。
- **ペシミスティック同時実行制御**-同時実行の競合が一般的であり、ユーザーが別のユーザーの同時アクティビティによって変更が保存されていないということを許容できないことを想定しています。そのため、1人のユーザーがレコードの更新を開始したときに、そのレコードをロックして、ユーザーが変更をコミットするまで他のユーザーがそのレコードを編集または削除できないようにします。

これまでに説明したすべてのチュートリアルでは、既定の同時実行の解決方法を使用していました。つまり、最後の書き込みを勝ちにします。 このチュートリアルでは、オプティミスティック同時実行制御を実装する方法について説明します。

> [!NOTE]
> このチュートリアルシリーズでは、ペシミスティック同時実行の例については説明しません。 ペシミスティック同時実行制御はほとんど使用されません。このようなロックが適切に放棄されていないと、他のユーザーがデータを更新できなくなる可能性があるためです。 たとえば、ユーザーが編集のためにレコードをロックしてから、ロックを解除する前にその日のままにした場合、元のユーザーが戻って更新を完了するまで、他のユーザーはそのレコードを更新できません。 したがって、ペシミスティック同時実行制御が使用されている場合は、通常、タイムアウトが発生すると、ロックがキャンセルされます。 チケット販売 web サイトでは、ユーザーが注文プロセスを完了している間に特定の座席をロックします。これは、ペシミスティック同時実行制御の一例です。

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>手順 1: オプティミスティック同時実行制御の実装方法を確認する

オプティミスティック同時実行制御は、更新または削除するレコードの値が、更新または削除処理の開始時と同じ値であることを保証することによって機能します。 たとえば、編集可能な GridView で [編集] ボタンをクリックすると、レコードの値がデータベースから読み取られ、テキストボックスやその他の Web コントロールに表示されます。 これらの元の値は、GridView によって保存されます。 その後、ユーザーが変更を行って [更新] ボタンをクリックすると、元の値と新しい値がビジネスロジック層に送信され、その後、データアクセス層に移動します。 データアクセス層は、ユーザーが編集を開始した元の値がデータベース内の値と同じである場合にのみレコードを更新する SQL ステートメントを発行する必要があります。 図2は、この一連のイベントを示しています。

[更新または削除を成功させるには、元の値が現在のデータベースの値と同じである必要があり ![](implementing-optimistic-concurrency-vb/_static/image5.png)](implementing-optimistic-concurrency-vb/_static/image4.png)

**図 2**: 更新または削除を成功させるには、元の値が現在のデータベースの値と同じである必要があります ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image6.png)されます)。

オプティミスティック同時実行制御の実装にはさまざまな方法があります (いくつかのオプションについては、「 [Bromberg](http://peterbromberg.net/)の[オプティミスティック同時実行制御のロジック](http://www.eggheadcafe.com/articles/20050719.asp)」を参照してください)。 ADO.NET 型指定されたデータセットは、チェックボックスの目盛りだけを使用して構成できる1つの実装を提供します。 型指定されたデータセット内の TableAdapter に対してオプティミスティック同時実行制御を有効にすると、TableAdapter の `UPDATE` と `DELETE` ステートメントが強化され、`WHERE` 句の元の値のすべての比較が含まれます。 次の `UPDATE` ステートメントでは、現在のデータベース値が GridView のレコードを更新するときに最初に取得された値と等しい場合にのみ、製品の名前と価格を更新します。 `@ProductName` パラメーターと `@UnitPrice` パラメーターには、ユーザーが入力した新しい値が含まれます。一方、`@original_ProductName` と `@original_UnitPrice` には、[編集] ボタンをクリックしたときに GridView に最初に読み込まれた値が含まれます。

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample1.sql)]

> [!NOTE]
> この `UPDATE` ステートメントは、読みやすくするために簡略化されています。 実際には、`UnitPrice` に `NULL` を含めることができ、`NULL = NULL` が常に False を返すかどうかを確認するために、`WHERE` 句の `UnitPrice` チェックインがさらに複雑になります (代わりに `IS NULL`を使用する必要があります)。

別の基になる `UPDATE` ステートメントを使用するだけでなく、オプティミスティック同時実行制御を使用するように TableAdapter を構成すると、その DB ダイレクトメソッドの署名も変更されます。 最初のチュートリアル「[*データアクセス層の作成*](../introduction/creating-a-data-access-layer-cs.md)」では、DB ダイレクトメソッドは、厳密に型指定された DataRow または DataTable インスタンスではなく、入力パラメーターとしてスカラー値のリストを受け取るものでした。 オプティミスティック同時実行制御を使用する場合、DB direct `Update()` および `Delete()` メソッドには、元の値の入力パラメーターも含まれます。 さらに、バッチ更新パターンを使用するための BLL 内のコード (スカラー値ではなく Datarow と Datatable を受け入れる `Update()` メソッドオーバーロード) も変更する必要があります。

既存の DAL の Tableadapter を拡張してオプティミスティック同時実行制御を使用するのではなく (このためには、BLL の変更が必要になります)、代わりに `NorthwindOptimisticConcurrency`という名前の新しい型のデータセットを作成します。ここで、オプティミスティック同時実行制御を使用する `Products` TableAdapter を追加します。 その後、オプティミスティック同時実行制御 DAL をサポートするための適切な変更を含む `ProductsOptimisticConcurrencyBLL` ビジネスロジック層クラスを作成します。 この基礎を説明すると、ASP.NET ページを作成する準備が整います。

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>手順 2: オプティミスティック同時実行制御をサポートするデータアクセス層の作成

新しい型指定されたデータセットを作成するには、`App_Code` フォルダー内の `DAL` フォルダーを右クリックし、`NorthwindOptimisticConcurrency`という名前の新しいデータセットを追加します。 最初のチュートリアルで説明したように、これを行うと、新しい TableAdapter が型指定されたデータセットに追加され、TableAdapter 構成ウィザードが自動的に起動します。 最初の画面では、`Web.config`の `NORTHWNDConnectionString` 設定を使用して、同じ Northwind データベースに接続するためのデータベースを指定するように求められます。

[同じ Northwind データベースに接続 ![には](implementing-optimistic-concurrency-vb/_static/image8.png)](implementing-optimistic-concurrency-vb/_static/image7.png)

**図 3**: 同じ Northwind データベースに接続する ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image9.png)されます)

次に、アドホック SQL ステートメント、新しいストアドプロシージャ、または既存のストアドプロシージャを使用して、データのクエリを実行する方法を確認するメッセージが表示されます。 元の DAL でアドホック SQL クエリを使用したため、ここでもこのオプションを使用します。

[アドホック SQL ステートメントを使用して取得するデータを指定 ![には](implementing-optimistic-concurrency-vb/_static/image11.png)](implementing-optimistic-concurrency-vb/_static/image10.png)

**図 4**: アドホック SQL ステートメントを使用して取得するデータを指定する ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image12.png)されます)

次の画面で、製品情報を取得するために使用する SQL クエリを入力します。 元の DAL の `Products` TableAdapter に使用したものとまったく同じ SQL クエリを使用します。これにより、製品の供給元とカテゴリ名と共にすべての `Product` 列が返されます。

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample2.sql)]

[元の DAL の Products TableAdapter と同じ SQL クエリを使用 ![](implementing-optimistic-concurrency-vb/_static/image14.png)](implementing-optimistic-concurrency-vb/_static/image13.png)

**図 5**: 元の DAL の `Products` TableAdapter で同じ SQL クエリを使用する ([クリックしてフルサイズのイメージを表示する](implementing-optimistic-concurrency-vb/_static/image15.png))

次の画面に進む前に、[詳細オプション] ボタンをクリックします。 この TableAdapter でオプティミスティック同時実行制御を使用するには、[オプティミスティック同時実行制御を使用する] チェックボックスをオンにします。

[オプティミスティック同時実行制御を有効にするには &quot;[オプティミスティック同時実行制御を使用する]&quot; チェックボックスをオンに ![](implementing-optimistic-concurrency-vb/_static/image17.png)](implementing-optimistic-concurrency-vb/_static/image16.png)

**図 6**: [オプティミスティック同時実行制御を使用する] チェックボックスをオンにしてオプティミスティック同時実行制御を有効にする ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image18.png)されます)

最後に、TableAdapter が DataTable にデータを格納し、DataTable を返すデータアクセスパターンを使用する必要があることを示します。また、DB ダイレクトメソッドを作成する必要があることを示します。 元の DAL で使用した名前付け規則を反映するように、GetData から GetProducts に DataTable パターンを返すのメソッド名を変更します。

[TableAdapter がすべてのデータアクセスパターンを利用 ![](implementing-optimistic-concurrency-vb/_static/image20.png)](implementing-optimistic-concurrency-vb/_static/image19.png)

**図 7**: TableAdapter ですべてのデータアクセスパターンを使用[する (クリックしてフルサイズのイメージを表示する](implementing-optimistic-concurrency-vb/_static/image21.png))

ウィザードを完了すると、データセットデザイナーには、厳密に型指定された `Products` DataTable と TableAdapter が含まれます。 DataTable の名前を `Products` から `ProductsOptimisticConcurrency`に変更します。これを行うには、DataTable のタイトルバーを右クリックし、コンテキストメニューから [名前の変更] を選択します。

[DataTable と TableAdapter が型指定されたデータセットに追加された ![](implementing-optimistic-concurrency-vb/_static/image23.png)](implementing-optimistic-concurrency-vb/_static/image22.png)

**図 8**: DataTable と TableAdapter が型指定されたデータセットに追加された ([クリックすると、フルサイズのイメージが表示](implementing-optimistic-concurrency-vb/_static/image24.png)されます)

(オプティミスティック同時実行制御を使用する) `ProductsOptimisticConcurrency` TableAdapter と Products TableAdapter () の間の `UPDATE` と `DELETE` クエリの相違点を確認するには、TableAdapter をクリックし、プロパティウィンドウにアクセスします。 `DeleteCommand` プロパティと `UpdateCommand` プロパティの `CommandText` サブプロパティで、DAL の更新または削除に関連するメソッドが呼び出されたときにデータベースに送信される実際の SQL 構文を確認できます。 `ProductsOptimisticConcurrency` TableAdapter の場合、使用される `DELETE` ステートメントは次のとおりです。

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample3.sql)]

しかし、元の DAL の製品 TableAdapter の `DELETE` ステートメントははるかに簡単です。

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample4.sql)]

ご覧のように、オプティミスティック同時実行制御を使用する TableAdapter の `DELETE` ステートメントの `WHERE` 句には、`Product` テーブルの既存の列値と、GridView (または DetailsView または FormView) が最後に設定された時点での元の値との比較が含まれます。 `ProductID`、`ProductName`、および `Discontinued` 以外のすべてのフィールドは `NULL` 値を持つことができるため、`NULL` 句の `WHERE` 値を正しく比較するために、追加のパラメーターとチェックが含まれています。

このチュートリアルでは、オプティミスティック同時実行制御が有効なデータセットに Datatable を追加することはありません。 ASP.NET ページでは、製品情報の更新と削除のみが提供されるためです。 ただし、`ProductsOptimisticConcurrency` TableAdapter に `GetProductByProductID(productID)` メソッドを追加する必要もあります。

これを行うには、TableAdapter のタイトルバー (`Fill` と `GetProducts` メソッド名の上の領域) を右クリックし、コンテキストメニューから [クエリの追加] を選択します。 これにより、TableAdapter クエリの構成ウィザードが起動します。 TableAdapter の初期構成と同様に、アドホック SQL ステートメントを使用して `GetProductByProductID(productID)` メソッドを作成することを選択します (図4を参照)。 `GetProductByProductID(productID)` メソッドは特定の製品に関する情報を返すため、このクエリは、行を返す `SELECT` のクエリ型であることを示します。

[![クエリの種類を &quot;としてマークすると、行が返され&quot;](implementing-optimistic-concurrency-vb/_static/image26.png)](implementing-optimistic-concurrency-vb/_static/image25.png)

**図 9**: クエリの種類を "行を返す`SELECT`" としてマーク[する (クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image27.png)されます)

次の画面で、TableAdapter の既定のクエリが事前に読み込まれている、使用する SQL クエリを入力するように求められます。 図10に示すように、`WHERE ProductID = @ProductID`句を含めるように既存のクエリを拡張します。

[特定の製品レコードを返すために、事前に読み込まれたクエリに WHERE 句を追加 ![](implementing-optimistic-concurrency-vb/_static/image29.png)](implementing-optimistic-concurrency-vb/_static/image28.png)

**図 10**: 事前に読み込まれたクエリに `WHERE` 句を追加して特定の製品レコードを返す ([クリックしてフルサイズの画像を表示する](implementing-optimistic-concurrency-vb/_static/image30.png))

最後に、生成されたメソッド名を `FillByProductID` に変更し、`GetProductByProductID`します。

[メソッドの名前を FillByProductID および GetProductByProductID に変更 ![には](implementing-optimistic-concurrency-vb/_static/image32.png)](implementing-optimistic-concurrency-vb/_static/image31.png)

**図 11**: `FillByProductID` と `GetProductByProductID` にメソッドの名前を変更する ([クリックしてフルサイズのイメージを表示する](implementing-optimistic-concurrency-vb/_static/image33.png))

このウィザードが完了すると、TableAdapter には、データを取得するための2つのメソッドが含まれるようになりました。 `GetProducts()`では、*すべて*の製品が返されます。および `GetProductByProductID(productID)`。指定した製品が返されます。

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>手順 3: オプティミスティック同時実行対応 DAL のビジネスロジック層の作成

既存の `ProductsBLL` クラスには、batch update と DB direct の両方のパターンを使用する例が含まれています。 `AddProduct` メソッドと `UpdateProduct` のオーバーロードでは、どちらもバッチ更新パターンを使用し、`ProductRow` インスタンスを TableAdapter の Update メソッドに渡します。 一方、`DeleteProduct` メソッドでは、TableAdapter の `Delete(productID)` メソッドを呼び出すことによって、DB direct パターンが使用されます。

新しい `ProductsOptimisticConcurrency` TableAdapter では、DB ダイレクトメソッドで、元の値も渡す必要があります。 たとえば、`Delete` メソッドでは、10個の入力パラメーター (元の `ProductID`、`ProductName`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`、`Discontinued`) が必要になります。 これらの追加の入力パラメーターの値は、データベースに送信される `DELETE` ステートメントの `WHERE` 句で使用されます。データベースの現在の値が元の値に対応している場合にのみ、指定したレコードが削除されます。

バッチ更新パターンで使用される TableAdapter の `Update` メソッドのメソッドシグネチャは変更されていませんが、元の値と新しい値を記録するために必要なコードにはがあります。 そのため、オプティミスティック同時実行対応の DAL を既存の `ProductsBLL` クラスと共に使用するのではなく、新しい DAL を操作するための新しいビジネスロジックレイヤークラスを作成してみましょう。

`ProductsOptimisticConcurrencyBLL` という名前のクラスを `App_Code` フォルダー内の `BLL` フォルダーに追加します。

![ProductsOptimisticConcurrencyBLL クラスを [BLL] フォルダーに追加します。](implementing-optimistic-concurrency-vb/_static/image34.png)

**図 12**: [BLL] フォルダーに `ProductsOptimisticConcurrencyBLL` クラスを追加する

次に、`ProductsOptimisticConcurrencyBLL` クラスに次のコードを追加します。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample5.vb)]

Using `NorthwindOptimisticConcurrencyTableAdapters` ステートメントは、クラス宣言の先頭より上にあることに注意してください。 `NorthwindOptimisticConcurrencyTableAdapters` 名前空間には、DAL のメソッドを提供する `ProductsOptimisticConcurrencyTableAdapter` クラスが含まれています。 また、クラス宣言の前に、`System.ComponentModel.DataObject` 属性があります。これにより、Visual Studio は、ObjectDataSource ウィザードのドロップダウンリストにこのクラスを含めるように指示します。

`ProductsOptimisticConcurrencyBLL`の `Adapter` プロパティを使用すると、`ProductsOptimisticConcurrencyTableAdapter` クラスのインスタンスにすばやくアクセスでき、元の BLL クラス (`ProductsBLL`、`CategoriesBLL`など) で使用されるパターンに従います。 最後に、`GetProducts()` メソッドは、DAL の `GetProducts()` メソッドに単にを呼び出し、データベース内の各製品レコードの `ProductsOptimisticConcurrencyRow` インスタンスが設定された `ProductsOptimisticConcurrencyDataTable` オブジェクトを返します。

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>オプティミスティック同時実行制御による DB Direct パターンを使用した製品の削除

オプティミスティック同時実行制御を使用する DAL に対して DB direct パターンを使用する場合は、メソッドに新しい値と元の値を渡す必要があります。 削除の場合、新しい値は存在しないため、元の値のみを渡す必要があります。 BLL では、元のすべてのパラメーターを入力パラメーターとして受け入れる必要があります。 `ProductsOptimisticConcurrencyBLL` クラスの `DeleteProduct` メソッドで、DB ダイレクトメソッドを使用してみましょう。 つまり、次のコードに示すように、このメソッドは10個の製品データフィールドをすべて入力パラメーターとして取得し、それらを DAL に渡す必要があります。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample6.vb)]

元の値-GridView (または DetailsView または FormView) に最後に読み込まれた値と、ユーザーが [削除] ボタンをクリックしたときにデータベースの値が異なる場合、`WHERE` 句はデータベースレコードと一致せず、影響を受けるレコードはありません。 したがって、TableAdapter の `Delete` メソッドは `0` を返し、BLL の `DeleteProduct` メソッドは `false`を返します。

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>オプティミスティック同時実行制御によるバッチ更新パターンを使用した製品の更新

前述のように、TableAdapter のバッチ更新パターンの `Update` メソッドは、オプティミスティック同時実行制御が使用されているかどうかに関係なく、同じメソッドシグネチャを持ちます。 つまり、`Update` メソッドには、DataRow、Datarow の配列、DataTable、または型指定されたデータセットが必要です。 元の値を指定するための追加の入力パラメーターはありません。 これが可能なのは、DataTable が DataRow の元の値および変更された値を追跡しているためです。 DAL によって `UPDATE` ステートメントが発行されると、`@original_ColumnName` パラメーターに DataRow の元の値が設定されます。一方、`@ColumnName` のパラメーターには、DataRow の変更後の値が設定されます。

(元の非オプティミスティック同時実行制御 DAL を使用する) `ProductsBLL` クラスでは、バッチ更新パターンを使用して製品情報を更新すると、コードで次の一連のイベントが実行されます。

1. TableAdapter の `GetProductByProductID(productID)` 方法を使用して、現在のデータベースの製品情報を `ProductRow` インスタンスに読み取ります。
2. 手順 1. の `ProductRow` インスタンスに新しい値を割り当てます。
3. TableAdapter の `Update` メソッドを呼び出し、`ProductRow` インスタンスを渡します。

ただし、この一連の手順ではオプティミスティック同時実行制御が正しくサポートされません。これは、手順 1. で設定された `ProductRow` がデータベースから直接設定されることを意味します。つまり、DataRow によって使用される元の値は、データベースに現在存在する値であり、編集プロセスの開始時に GridView にバインドされた 代わりに、オプティミスティック同時実行制御を有効にした DAL を使用する場合は、次の手順を使用するように `UpdateProduct` メソッドのオーバーロードを変更する必要があります。

1. TableAdapter の `GetProductByProductID(productID)` 方法を使用して、現在のデータベースの製品情報を `ProductsOptimisticConcurrencyRow` インスタンスに読み取ります。
2. 手順 1. の `ProductsOptimisticConcurrencyRow` インスタンスに*元*の値を割り当てます。
3. `ProductsOptimisticConcurrencyRow` インスタンスの `AcceptChanges()` メソッドを呼び出します。これにより、現在の値が "original" であることが DataRow に指示されます。
4. *新しい*値を `ProductsOptimisticConcurrencyRow` インスタンスに割り当てます。
5. TableAdapter の `Update` メソッドを呼び出し、`ProductsOptimisticConcurrencyRow` インスタンスを渡します。

手順1では、指定された製品レコードの現在のすべてのデータベース値を読み取ります。 この手順は、*すべて*の product 列を更新する `UpdateProduct` のオーバーロードには不要です (これらの値は手順2で上書きされます) が、列の値のサブセットのみが入力パラメーターとして渡されるオーバーロードには不可欠です。 元の値が `ProductsOptimisticConcurrencyRow` インスタンスに割り当てられると、`AcceptChanges()` メソッドが呼び出されます。これにより、現在の DataRow 値が `UPDATE` ステートメントの `@original_ColumnName` パラメーターで使用される元の値としてマークされます。 次に、新しいパラメーター値が `ProductsOptimisticConcurrencyRow` に割り当てられ、最後に `Update` メソッドが呼び出され、DataRow に渡されます。

次のコードは、すべての製品データフィールドを入力パラメーターとして受け入れる `UpdateProduct` オーバーロードを示しています。 ここには記載されていませんが、このチュートリアルのダウンロードに含まれている `ProductsOptimisticConcurrencyBLL` クラスには、入力パラメーターとして製品名と価格だけを受け入れる `UpdateProduct` のオーバーロードも含まれています。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample7.vb)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>手順 4: 元の値と新しい値を ASP.NET ページから BLL メソッドに渡す

DAL と BLL が完成したら、システムに組み込まれたオプティミスティック同時実行制御ロジックを利用できる ASP.NET ページを作成します。 具体的には、データ Web コントロール (GridView、DetailsView、または FormView) は元の値を記憶する必要があり、ObjectDataSource は両方の値のセットをビジネスロジック層に渡す必要があります。 さらに、同時実行違反を適切に処理するように、ASP.NET ページを構成する必要があります。

まず、`EditInsertDelete` フォルダーの [`OptimisticConcurrency.aspx`] ページを開き、GridView をデザイナーに追加します。その `ID` プロパティを `ProductsGrid`に設定します。 GridView のスマートタグから、`ProductsOptimisticConcurrencyDataSource`という名前の新しい ObjectDataSource を作成することを選択します。 この ObjectDataSource はオプティミスティック同時実行制御をサポートする DAL を使用するようにするため、`ProductsOptimisticConcurrencyBLL` オブジェクトを使用するように構成します。

[ObjectDataSource が ProductsOptimisticConcurrencyBLL オブジェクトを使用している ![](implementing-optimistic-concurrency-vb/_static/image36.png)](implementing-optimistic-concurrency-vb/_static/image35.png)

**図 13**: ObjectDataSource で `ProductsOptimisticConcurrencyBLL` オブジェクトを使用する ([クリックしてフルサイズの画像を表示する](implementing-optimistic-concurrency-vb/_static/image37.png))

ウィザードのドロップダウンリストから `GetProducts`、`UpdateProduct`、および `DeleteProduct` メソッドを選択します。 UpdateProduct メソッドの場合は、すべての製品のデータフィールドを受け入れるオーバーロードを使用します。

## <a name="configuring-the-objectdatasource-controls-properties"></a>ObjectDataSource コントロールのプロパティの構成

ウィザードを完了すると、ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample8.aspx)]

ご覧のように、`DeleteParameters` コレクションには、`ProductsOptimisticConcurrencyBLL` クラスの `DeleteProduct` メソッドに含まれる10個の入力パラメーターそれぞれの `Parameter` インスタンスが含まれています。 同様に、`UpdateParameters` コレクションには `UpdateProduct`内の各入力パラメーターの `Parameter` インスタンスが含まれています。

データ変更を伴う前のチュートリアルでは、この時点で ObjectDataSource の `OldValuesParameterFormatString` プロパティを削除しました。このプロパティは、BLL メソッドが、新しい値と共に古い (または元の) 値を渡すことを想定していることを示すためです。 さらに、このプロパティ値は、元の値の入力パラメーター名を示します。 元の値を BLL に渡すため、このプロパティ*は削除しないでください。*

> [!NOTE]
> `OldValuesParameterFormatString` プロパティの値は、元の値を期待する BLL 内の入力パラメーター名にマップされる必要があります。 これらのパラメーターには `original_productName`、`original_supplierID`などの名前を付けたので、`OldValuesParameterFormatString` プロパティの値を `original_{0}`として残しておくことができます。 ただし、BLL メソッドの入力パラメーターに `old_productName`、`old_supplierID`などの名前が付いている場合は、`OldValuesParameterFormatString` プロパティを `old_{0}`に更新する必要があります。

ObjectDataSource が元の値を BLL メソッドに正しく渡すために必要な最後のプロパティ設定が1つあります。 ObjectDataSource には、次[の2つの値のいずれか](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx)に割り当てることができる[ConflictDetection プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx)があります。

- `OverwriteChanges`-既定値。は、元の値を BLL メソッドの元の入力パラメーターに送信しません。
- `CompareAllValues`-元の値を BLL メソッドに送信します。オプティミスティック同時実行制御を使用する場合にこのオプションを選択します

`ConflictDetection` プロパティを `CompareAllValues`に設定します。

## <a name="configuring-the-gridviews-properties-and-fields"></a>GridView のプロパティとフィールドの構成

ObjectDataSource のプロパティが適切に構成されているので、GridView の設定に注目してみましょう。 まず、GridView で編集と削除がサポートされるようにするため、[編集を有効にする] チェックボックスをオンにして、GridView のスマートタグから [削除] チェックボックスをオンにします。 これにより、`ShowEditButton` と `ShowDeleteButton` の両方が `true`に設定されている CommandField が追加されます。

`ProductsOptimisticConcurrencyDataSource` ObjectDataSource にバインドされている場合、GridView には、各製品のデータフィールドのフィールドが含まれます。 このような GridView は編集できますが、ユーザーエクスペリエンスは任意ですが、許容されます。 `CategoryID` および `SupplierID` BoundFields がテキストボックスとして表示され、ユーザーは適切なカテゴリとサプライヤーを ID 番号として入力する必要があります。 数値フィールドの書式が設定されていないため、製品名が指定されていること、および単価、在庫数、在庫数、および並べ替えレベルの値が適切な数値であることを確認するための検証コントロールはありません。0にします。

「*編集および挿入インターフェイスへの検証コントロールの追加*」と「*データ変更インターフェイスのカスタマイズ*」で説明したように、ユーザーインターフェイスは、Boundfields を templatefields に置き換えることによってカスタマイズできます。 この GridView と編集インターフェイスは、次の方法で変更しました。

- `ProductID`、`SupplierName`、および `CategoryName` BoundFields が削除されました。
- `ProductName` BoundField を TemplateField に変換し、RequiredFieldValidation コントロールを追加しました。
- `CategoryID` および `SupplierID` BoundFields を TemplateFields に変換し、テキストボックスではなく DropDownLists を使用するように編集インターフェイスを調整しました。 これらの TemplateFields ' `ItemTemplates`には、`CategoryName` と `SupplierName` のデータフィールドが表示されます。
- `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、および `ReorderLevel` BoundFields を TemplateFields に変換し、CompareValidator コントロールを追加しました。

前のチュートリアルでこれらのタスクを実行する方法については既に説明したので、ここでは最後の宣言型の構文を一覧表示し、実装を実際のままにします。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample9.aspx)]

ここでは、完全に動作する例を示しています。 ただし、いくつかの微妙な問題が発生します。 また、同時実行違反が発生した場合にユーザーに警告するインターフェイスも必要です。

> [!NOTE]
> データ Web コントロールが元の値を ObjectDataSource に正しく渡す (その後、BLL に渡される) ためには、GridView の `EnableViewState` プロパティが `true` (既定値) に設定されていることが重要です。 ビューステートを無効にすると、元の値がポストバック時に失われます。

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>正しい元の値を ObjectDataSource に渡す

GridView の構成方法にはいくつかの問題があります。 Objectdatasource の `ConflictDetection` プロパティが `CompareAllValues` (そのまま) に設定されている場合、objectdatasource の `Update()` または `Delete()` メソッドが GridView (または DetailsView または FormView) によって呼び出されると、ObjectDataSource は GridView の元の値を適切な `Parameter` インスタンスにコピーしようとします。 このプロセスをグラフィカルに表示するには、図2を参照してください。

具体的には、gridview の元の値には、データが GridView にバインドされるたびに、双方向のデータバインドステートメントの値が割り当てられます。 したがって、必要な元の値はすべて双方向のデータバインディングを使用してキャプチャされ、変換可能な形式で提供されることが不可欠です。

これが重要な理由を確認するには、ブラウザーでページにアクセスしてください。 必要に応じて、GridView は、左端の列の [編集] ボタンと [削除] ボタンを使用して各製品を一覧表示します。

[GridView に製品が一覧表示さ ![](implementing-optimistic-concurrency-vb/_static/image39.png)](implementing-optimistic-concurrency-vb/_static/image38.png)

**図 14**: GridView に製品が表示されている ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image40.png)されます)

任意の製品の [削除] ボタンをクリックすると、`FormatException` がスローされます。

[FormatException で製品の結果を削除しようとして ![](implementing-optimistic-concurrency-vb/_static/image42.png)](implementing-optimistic-concurrency-vb/_static/image41.png)

**図 15**: `FormatException` で製品の結果を削除しようとしています ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image43.png)されます)

`FormatException` は、ObjectDataSource が元の `UnitPrice` 値を読み取ろうとしたときに発生します。 `ItemTemplate` の `UnitPrice` は通貨 (`<%# Bind("UnitPrice", "{0:C}") %>`) として書式設定されているため、$19.95 のような通貨記号が含まれています。 `FormatException` は、ObjectDataSource がこの文字列を `decimal`に変換しようとしたときに発生します。 この問題を回避するために、いくつかのオプションがあります。

- `ItemTemplate`から通貨の書式を削除します。 つまり、`<%# Bind("UnitPrice", "{0:C}") %>`を使用するのではなく、単に `<%# Bind("UnitPrice") %>`を使用します。 この欠点は、価格がフォーマットされていないことです。
- `ItemTemplate`で通貨として書式設定された `UnitPrice` を表示しますが、`Eval` キーワードを使用してこれを行います。 `Eval` は一方向のデータバインディングを実行することを思い出してください。 その場合でも、元の値に `UnitPrice` 値を指定する必要があるため、`ItemTemplate`では双方向の databinding ステートメントが必要になりますが、`Visible` プロパティが `false`に設定されている Label Web コントロールに配置できます。 ItemTemplate では、次のマークアップを使用できます。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample10.aspx)]

- `<%# Bind("UnitPrice") %>`を使用して、`ItemTemplate`から通貨の書式を削除します。 GridView の `RowDataBound` イベントハンドラーで、`UnitPrice` 値が表示されている Label Web コントロールにプログラムによってアクセスし、その `Text` プロパティを書式設定されたバージョンに設定します。
- `UnitPrice` は通貨形式のままにします。 GridView の `RowDeleting` イベントハンドラーで、`Decimal.Parse`を使用して、既存の元の `UnitPrice` の値 ($19.95) を実際の10進値に置き換えます。 ASP.NET ページのチュートリアルでは、 [*BLL と DAL レベルの例外の処理*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)に関する `RowUpdating` のイベントハンドラーに似たものを実現する方法を説明しました。

この例では、2番目の方法を使用して、`Text` プロパティが、書式設定されていない `UnitPrice` 値にバインドされた双方向データである非表示のラベル Web コントロールを追加します。

この問題を解決したら、任意の製品の [削除] ボタンをもう一度クリックします。 今回は、ObjectDataSource が BLL の `UpdateProduct` メソッドを呼び出そうとしたときに、`InvalidOperationException` を取得します。

[![ObjectDataSource は、送信しようとしている入力パラメーターを持つメソッドを見つけることができません](implementing-optimistic-concurrency-vb/_static/image45.png)](implementing-optimistic-concurrency-vb/_static/image44.png)

**図 16**: ObjectDataSource は、送信する入力パラメーターを持つメソッドを見つけることができません ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image46.png)されます)

例外のメッセージを見ると、ObjectDataSource では、`original_CategoryName` と `original_SupplierName` 入力パラメーターを含む BLL `DeleteProduct` メソッドを呼び出す必要があることがわかります。 これは、`CategoryID` と `SupplierID` TemplateFields の `ItemTemplate` には、現在、`CategoryName` および `SupplierName` データフィールドを持つ双方向のバインドステートメントが含まれているためです。 代わりに、`CategoryID` と `SupplierID` のデータフィールドを含む `Bind` ステートメントを含める必要があります。 これを行うには、既存の Bind ステートメントを `Eval` のステートメントに置き換え、次に示すように、双方向のデータバインディングを使用して、`Text` プロパティが `CategoryID` と `SupplierID` のデータフィールドにバインドされている非表示のラベルコントロールを追加します。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample11.aspx)]

これらの変更により、製品情報を正常に削除および編集できるようになりました。 手順 5. では、同時実行違反が検出されていることを確認する方法について説明します。 ここでは、いくつかのレコードを更新して削除し、1人のユーザーの更新と削除が想定どおりに動作することを確認するために数分かかります。

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>手順 5: オプティミスティック同時実行制御のテスト

(データが無条件に上書きされるのではなく) 同時実行違反が検出されていることを確認するには、このページで2つのブラウザーウィンドウを開く必要があります。 両方のブラウザーインスタンスで、[Chai] の [編集] ボタンをクリックします。 次に、いずれかのブラウザーで、名前を "Chai 紅茶" に変更し、[更新] をクリックします。 更新は正常に完了し、GridView が新しい製品名として "Chai 紅茶" を使用して、編集前の状態に戻ります。

ただし、他のブラウザーウィンドウインスタンスでは、[製品名] テキストボックスには引き続き "Chai" と表示されます。 この2番目のブラウザーウィンドウで、`UnitPrice` を `25.00`に更新します。 オプティミスティック同時実行制御がサポートされていない場合、2番目のブラウザーインスタンスで [更新] をクリックすると、製品名が "Chai" に変更され、最初のブラウザーインスタンスによって行われた変更が上書きされます。 ただし、オプティミスティック同時実行制御を使用した場合、2番目のブラウザーインスタンスの [更新] ボタンをクリックすると、 [system.data.dbconcurrencyexception](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)が発生します。

[![同時実行違反が検出されると、System.data.dbconcurrencyexception がスローされます。](implementing-optimistic-concurrency-vb/_static/image48.png)](implementing-optimistic-concurrency-vb/_static/image47.png)

**図 17**: 同時実行違反が検出されると `DBConcurrencyException` がスローされます ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image49.png)されます)

`DBConcurrencyException` は、DAL のバッチ更新パターンが使用されている場合にのみスローされます。 DB direct パターンでは、例外は発生しません。これは、影響を受けた行がないことを示しているだけです。 これを説明するために、両方のブラウザーインスタンスの GridView を編集前の状態に戻します。 次に、最初のブラウザーインスタンスで、[編集] ボタンをクリックし、製品名を "Chai 紅茶" から "Chai" に変更し、[更新] をクリックします。 2番目のブラウザーウィンドウで、[Chai] の [削除] ボタンをクリックします。

[削除] をクリックすると、ページがポストバックされ、GridView が ObjectDataSource の `Delete()` メソッドを呼び出し、ObjectDataSource が `ProductsOptimisticConcurrencyBLL` クラスの `DeleteProduct` メソッドに戻り、元の値が渡されます。 2番目のブラウザーインスタンスの元の `ProductName` 値は "Chai 紅茶" で、データベース内の現在の `ProductName` 値と一致しません。 したがって、データベースに対して発行された `DELETE` ステートメントは、`WHERE` 句が満たすレコードがないため、0行に影響します。 `DeleteProduct` メソッドは `false` を返し、ObjectDataSource のデータは GridView に再バインドされます。

エンドユーザーの観点からは、2番目のブラウザーウィンドウで [Chai 茶] の [削除] ボタンをクリックすると、画面が点滅します。その後、製品はまだ存在しますが、"Chai" (最初のブラウザーによって行われた製品名の変更) として表示されます。インスタンス)。 ユーザーが [削除] ボタンをもう一度クリックした場合、GridView の元の `ProductName` 値 ("Chai") がデータベースの値と一致するため、削除は成功します。

どちらの場合も、ユーザーエクスペリエンスは理想的なものになります。 バッチ更新パターンを使用する場合、`DBConcurrencyException` 例外の詳細をユーザーに表示しないことは明らかです。 また、DB direct パターンを使用する場合の動作は、ユーザーコマンドが失敗したときに多少わかりにくいことがありますが、その理由について正確に示す情報はありませんでした。

この2つの問題を解決するには、ページにラベル Web コントロールを作成し、更新または削除が失敗した理由を説明します。 バッチ更新パターンでは、GridView のポストレベルイベントハンドラーで `DBConcurrencyException` 例外が発生したかどうかを判断し、必要に応じて警告ラベルを表示できます。 DB ダイレクトメソッドでは、BLL メソッドの戻り値 (1 つの行が影響を受けた場合は `true`、それ以外の場合は `false`) を確認し、必要に応じて情報メッセージを表示できます。

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>手順 6: 情報メッセージを追加し、同時実行違反の発生時に表示する

同時実行違反が発生した場合の動作は、DAL のバッチ更新または DB ダイレクトパターンが使用されたかどうかによって異なります。 このチュートリアルでは、両方のパターンを使用します。更新に使用するバッチ更新パターンと、削除に使用する DB direct パターンを使用します。 まず、データを削除または更新しようとしたときに同時実行違反が発生したことを説明する2つのラベル Web コントロールをページに追加してみましょう。 ラベルコントロールの `Visible` と `EnableViewState` プロパティを `false`に設定します。これにより、各ページにアクセスしたときに、その `Visible` プロパティがプログラムによって `true`に設定されている場合を除いて、各ページのアクセスで非表示になります。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample12.aspx)]

`Visible`、`EnabledViewState`、および `Text` プロパティの設定に加えて、`CssClass` プロパティも `Warning`に設定しました。これにより、ラベルが大きい、赤、斜体、太字のフォントで表示されます。 この CSS `Warning` クラスは、*挿入、更新、および削除*の各チュートリアルに関連付けられているイベントを調べることで、定義され、スタイルに追加されました。

これらのラベルを追加すると、Visual Studio のデザイナーは図18のようになります。

[2つのラベルコントロールがページに追加され ![](implementing-optimistic-concurrency-vb/_static/image51.png)](implementing-optimistic-concurrency-vb/_static/image50.png)

**図 18**: ページに2つのラベルコントロールが追加されました ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-vb/_static/image52.png)されます)

これらのラベルの Web コントロールを使用して、同時実行違反が発生したことを判断する方法を調べる準備ができました。その時点で、適切なラベルの `Visible` プロパティを `true`に設定して、情報メッセージを表示することができます。

## <a name="handling-concurrency-violations-when-updating"></a>更新時の同時実行違反の処理

まず、バッチ更新パターンを使用するときに、同時実行違反を処理する方法を見てみましょう。 バッチ更新パターンによるこのような違反によって `DBConcurrencyException` 例外がスローされるため、更新プロセス中に `DBConcurrencyException` 例外が発生したかどうかを確認するコードを ASP.NET ページに追加する必要があります。 その場合は、ユーザーがレコードの編集を開始してから [更新] ボタンをクリックしたときとの間で、他のユーザーが同じデータを変更したため、変更が保存されていないことを示すメッセージがユーザーに表示されます。

ASP.NET ページのチュートリアルでは、 *BLL と DAL レベルの例外の処理*について説明しましたが、このような例外は、データ Web コントロールの post レベルのイベントハンドラーで検出および抑制することができます。 そのため、`DBConcurrencyException` 例外がスローされたかどうかを確認する GridView の `RowUpdated` イベントのイベントハンドラーを作成する必要があります。 このイベントハンドラーには、次のイベントハンドラーコードに示すように、更新プロセス中に発生した例外への参照が渡されます。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample13.vb)]

`DBConcurrencyException` 例外が発生すると、このイベントハンドラーによって `UpdateConflictMessage` Label コントロールが表示され、例外が処理されたことが示されます。 このコードを配置すると、レコードの更新時に同時実行違反が発生した場合、ユーザーの変更は失われます。これは、ユーザーが同時に別のユーザーの変更を上書きしたためです。 特に、GridView は編集前の状態に戻り、現在のデータベースデータにバインドされます。 これにより、以前は表示されていなかった他のユーザーの変更で GridView 行が更新されます。 さらに、`UpdateConflictMessage` ラベルコントロールは、発生したことをユーザーに説明します。 この一連のイベントについては、図19で詳しく説明します。

[同時実行違反の発生時にユーザーの更新が失われる ![](implementing-optimistic-concurrency-vb/_static/image54.png)](implementing-optimistic-concurrency-vb/_static/image53.png)

**図 19**: 同時実行違反が発生したときにユーザーの更新が失われる ([クリックしてフルサイズの画像を表示する](implementing-optimistic-concurrency-vb/_static/image55.png))

> [!NOTE]
> または、GridView を編集前の状態に戻すのではなく、渡された `GridViewUpdatedEventArgs` オブジェクトの `KeepInEditMode` プロパティを true に設定して、GridView を編集中の状態にしておくこともできます。 ただし、この方法を使用する場合は、(`DataBind()` メソッドを呼び出して) GridView にデータを再バインドし、他のユーザーの値が編集インターフェイスに読み込まれるようにする必要があります。 このチュートリアルでダウンロードできるコードは、コメントアウトされた `RowUpdated` のイベントハンドラーに、次の2行のコードが含まれています。これらのコード行をコメント解除するだけで、同時実行違反の後に GridView を編集モードのままにすることができます。

## <a name="responding-to-concurrency-violations-when-deleting"></a>同時実行違反への応答 (削除時)

DB direct パターンでは、同時実行違反の発生時に例外は発生しません。 代わりに、WHERE 句がどのレコードとも一致しないため、データベースステートメントは単にレコードに影響しません。 BLL で作成されたすべてのデータ変更メソッドは、正確に1つのレコードに影響を与えたかどうかを示すブール値を返すように設計されています。 そのため、レコードの削除時に同時実行違反が発生したかどうかを判断するには、BLL の `DeleteProduct` メソッドの戻り値を確認します。

BLL メソッドの戻り値は、ObjectDataSource のポストレベルのイベントハンドラーで、イベントハンドラーに渡された `ObjectDataSourceStatusEventArgs` オブジェクトの `ReturnValue` プロパティを使用して調べることができます。 `DeleteProduct` メソッドから戻り値を決定することに関心があるため、ObjectDataSource の `Deleted` イベント用のイベントハンドラーを作成する必要があります。 `ReturnValue` プロパティは `object` 型であり、例外が発生した場合に `null` できます。また、メソッドは、値を返す前に中断されています。 したがって、最初に `ReturnValue` プロパティが `null` ではなく、ブール値であることを確認する必要があります。 このチェックに合格すると、`ReturnValue` が `false`場合は、`DeleteConflictMessage` Label コントロールが表示されます。 これは、次のコードを使用して実現できます。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample14.vb)]

同時実行違反が発生した場合、ユーザーの削除要求は取り消されます。 GridView が更新され、ユーザーがページを読み込んだときと [削除] ボタンをクリックしたときの間で、そのレコードに対して発生した変更が表示されます。 このような違反が発生した場合は、`DeleteConflictMessage` ラベルが表示され、何が起こったかがわかります (図20を参照)。

[同時実行違反の発生時にユーザーの削除が取り消さ ![](implementing-optimistic-concurrency-vb/_static/image57.png)](implementing-optimistic-concurrency-vb/_static/image56.png)

**図 20**: 同時実行違反が発生したときにユーザーの削除が取り消される ([クリックしてフルサイズのイメージを表示する](implementing-optimistic-concurrency-vb/_static/image58.png))

## <a name="summary"></a>まとめ

同時実行ユーザーが複数のデータを更新または削除できるようにするすべてのアプリケーションには、同時実行違反の可能性があります。 このような違反が考慮されていない場合、2人のユーザーが前回の書き込みで取得した同じデータを同時に更新すると、他のユーザーの変更が上書きされます。 また、開発者はオプティミスティックまたはペシミスティック同時実行制御を実装できます。 オプティミスティック同時実行制御では、同時実行違反が頻繁に発生しないことを前提としています。また、単に、同時実行違反を構成する update または delete コマンドを禁止します ペシミスティック同時実行制御は、同時実行違反が頻繁に発生することを前提としており、1人のユーザーの update コマンドまたは delete コマンドを拒否するだけでは許容できません。 ペシミスティック同時実行制御では、レコードを更新することによって、ロックされている間に他のユーザーがレコードを変更または削除できないようにします。

.NET の型指定されたデータセットは、オプティミスティック同時実行制御をサポートするための機能を提供します。 特に、データベースに対して発行された `UPDATE` および `DELETE` ステートメントには、テーブルのすべての列が含まれているので、レコードの現在のデータが、更新または削除の実行時にユーザーが持っていた元のデータと一致する場合にのみ、更新または削除が行われます。 DAL がオプティミスティック同時実行制御をサポートするように構成されたら、BLL メソッドを更新する必要があります。 また、BLL にコールダウンする ASP.NET ページを構成して、ObjectDataSource がデータ Web コントロールから元の値を取得し、BLL に渡すようにする必要があります。

このチュートリアルで説明したように、ASP.NET web アプリケーションにオプティミスティック同時実行制御を実装するには、DAL を更新して、ASP.NET ページにサポートを追加する必要があります。 この追加の作業が時間と労力を費やすかどうかは、アプリケーションによって異なります。 同時実行ユーザーがデータを更新していない場合、または更新しようとしているデータが相互に異なる場合は、同時実行制御が重要な問題にはなりません。 ただし、サイトの複数のユーザーが同じデータを使用している場合、同時実行制御を使用すると、1人のユーザーの更新や削除によって他のが誤って上書きされるのを防ぐことができます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](customizing-the-data-modification-interface-vb.md)
> [次へ](adding-client-side-confirmation-when-deleting-vb.md)
