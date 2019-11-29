---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
title: ビジネスロジック層を作成する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、データ交換の仲介者として機能するビジネスロジック層 (BLL) にビジネスルールを一元化する方法について説明します。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 142e5181-29ce-4bb9-907b-2a0becf7928b
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 2ee4789ea9567b7bcd70eb63695e0b1d73076dc2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572617"
---
# <a name="creating-a-business-logic-layer-vb"></a>ビジネス ロジック層を作成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_2_VB.exe)または[PDF のダウンロード](creating-a-business-logic-layer-vb/_static/datatutorial02vb1.pdf)

> このチュートリアルでは、プレゼンテーション層と DAL 間のデータ交換の仲介役として機能するビジネスロジック層 (BLL) にビジネスルールを一元化する方法について説明します。

## <a name="introduction"></a>はじめに

[最初のチュートリアル](creating-a-data-access-layer-vb.md)で作成したデータアクセス層 (DAL) は、データアクセスロジックをプレゼンテーションロジックから明確に分離します。 ただし、DAL では、データアクセスの詳細がプレゼンテーション層から明確に分離されますが、適用されるビジネスルールは適用されません。 たとえば、アプリケーションの場合、`Discontinued` フィールドが1に設定されているときは `Products` テーブルの `CategoryID` または `SupplierID` フィールドを変更しないようにするか、勤続ルールを適用して、従業員が雇用されたユーザーによって従業員が管理される状況を禁止することができます。 もう1つの一般的なシナリオは、特定のロールのユーザーのみが製品を削除したり、`UnitPrice` 値を変更したりできるということです。

このチュートリアルでは、これらのビジネスルールを、プレゼンテーション層と DAL 間のデータ交換の仲介役として機能するビジネスロジック層 (BLL) に集約する方法について説明します。 実際のアプリケーションでは、BLL を別のクラスライブラリプロジェクトとして実装する必要があります。ただし、これらのチュートリアルでは、プロジェクトの構造を簡略化するために、BLL を `App_Code` フォルダー内の一連のクラスとして実装します。 図1は、プレゼンテーション層、BLL、および DAL 間のアーキテクチャの関係を示しています。

![BLL は、プレゼンテーション層とデータアクセス層を分離し、ビジネスルールを適用します。](creating-a-business-logic-layer-vb/_static/image1.png)

**図 1**: BLL によって、プレゼンテーション層とデータアクセス層が分離され、ビジネスルールが適用される

[ビジネスロジック](http://en.wikipedia.org/wiki/Business_logic)を実装するために個別のクラスを作成するのではなく、部分クラスを使用して、このロジックを型指定されたデータセットに直接配置することもできます。 型指定されたデータセットの作成と拡張の例については、最初のチュートリアルを参照してください。

## <a name="step-1-creating-the-bll-classes"></a>手順 1: BLL クラスの作成

BLL は、DAL 内の各 TableAdapter 用に1つずつ、4つのクラスで構成されます。これらの BLL クラスにはそれぞれ、適切なビジネスルールを適用して、DAL 内のそれぞれの TableAdapter から取得、挿入、更新、および削除するためのメソッドが用意されています。

DAL および BLL に関連するクラスをより明確に分離するには、`App_Code` フォルダー、`DAL` および `BLL`に2つのサブフォルダーを作成します。 ソリューションエクスプローラーの `App_Code` フォルダーを右クリックし、[新しいフォルダー] を選択します。 これらの2つのフォルダーを作成したら、最初のチュートリアルで作成した型指定されたデータセットを `DAL` サブフォルダーに移動します。

次に、4つの BLL クラスファイルを `BLL` サブフォルダーに作成します。 これを行うには、[`BLL`] サブフォルダーを右クリックし、[新しい項目の追加] をクリックして、[クラス] テンプレートを選択します。 `ProductsBLL`、`CategoriesBLL`、`SuppliersBLL`、および `EmployeesBLL`の4つのクラスに名前を指定します。

![App_Code フォルダーに4つの新しいクラスを追加する](creating-a-business-logic-layer-vb/_static/image2.png)

**図 2**: `App_Code` フォルダーに4つの新しいクラスを追加する

次に、各クラスにメソッドを追加して、最初のチュートリアルで Tableadapter 用に定義されたメソッドをラップするだけです。 現時点では、これらのメソッドは、DAL に直接を呼び出します。必要なビジネスロジックを追加するには、後でを返します。

> [!NOTE]
> Visual Studio Standard Edition 以上を使用している場合 (つまり、Visual Web Developer を使用して*いない*場合)、必要に応じて[クラスデザイナー](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)を使用してクラスを視覚的にデザインできます。 Visual Studio のこの新機能の詳細については、[クラスデザイナーのブログ](https://blogs.msdn.com/classdesigner/default.aspx)を参照してください。

`ProductsBLL` クラスでは、合計7つのメソッドを追加する必要があります。

- すべての製品を返す `GetProducts()`
- 指定された製品 ID を持つ製品を返す `GetProductByProductID(productID)`
- 指定されたカテゴリのすべての製品を返す `GetProductsByCategoryID(categoryID)`
- 指定された業者からすべての製品を返す `GetProductsBySupplier(supplierID)`
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` は、渡された値を使用して新しい製品をデータベースに挿入します。新しく挿入されたレコードの `ProductID` 値を返します。
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` は、渡された値を使用してデータベース内の既存の製品を更新します。1行だけ更新された場合は `True` を返します。それ以外の場合は `False`
- 指定された製品をデータベースから削除 `DeleteProduct(productID)`

製品 Bll

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample1.vb)]

単にデータ `GetProducts`、`GetProductByProductID`、`GetProductsByCategoryID`、および `GetProductBySuppliersID` を返すメソッドは、単に DAL にコールダウンするだけで非常に簡単です。 一部のシナリオでは、このレベルで実装する必要があるビジネスルール (現在ログオンしているユーザーに基づく承認規則や、ユーザーが所属するロールなど) がある場合は、これらのメソッドをそのままにします。 これらのメソッドでは、BLL はプロキシとしてのみ機能し、プレゼンテーション層はデータアクセス層から基になるデータにアクセスします。

`AddProduct` メソッドと `UpdateProduct` メソッドは、両方ともパラメーターとしてさまざまな product フィールドの値を受け取り、新しい製品を追加したり、既存の製品を更新したりします。 `Product` テーブルの列の多くは `NULL` の値 (`CategoryID`、`SupplierID`、および `UnitPrice`を受け取ることができるため、いくつかの列に名前を付けることができます。これらの列にマップする `AddProduct` と `UpdateProduct` の入力パラメーターは、 [null 許容型](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)を使用します。 Null 許容型は .NET 2.0 の新機能であり、値型を `Nothing`する必要があるかどうかを示す手法を提供します。 さらに詳しい情報については、 [Paul Vick](http://www.panopticoncentral.net/)のブログで、 [null 許容型と VB の事実](http://www.panopticoncentral.net/archive/2004/06/04/1180.aspx)と、 [null 許容](https://msdn.microsoft.com/library/b3h38hb0%28VS.80%29.aspx)の構造体に関する技術ドキュメントを参照してください。

この3つのメソッドはいずれも、行が挿入、更新、または削除されたかどうかを示すブール値を返します。これは、操作によって影響を受ける行がない可能性があるためです。 たとえば、ページ開発者が、存在しない製品の `ProductID` を渡す `DeleteProduct` を呼び出すと、データベースに対して発行された `DELETE` ステートメントは影響を受けないため、`DeleteProduct` メソッドは `False`を返します。

新しい製品を追加したり、既存の製品を更新したりするときには、`ProductsRow` インスタンスを使用するのではなく、新しいまたは変更された製品のフィールド値をスカラーの一覧として取得することに注意してください。 `ProductsRow` クラスは、既定のパラメーターなしのコンストラクターを持たない ADO.NET `DataRow` クラスから派生するため、この方法が選択されました。 新しい `ProductsRow` インスタンスを作成するには、まず `ProductsDataTable` インスタンスを作成し、その `NewProductRow()` メソッド (`AddProduct`で実行) を呼び出す必要があります。 この欠点は、ObjectDataSource を使用して製品を挿入および更新するときに、そのようになります。 つまり、ObjectDataSource は入力パラメーターのインスタンスの作成を試みます。 BLL メソッドが `ProductsRow` インスタンスを必要とする場合、ObjectDataSource は1つのインスタンスを作成しようとしますが、既定のパラメーターなしのコンストラクターがないため失敗します。 この問題の詳細については、次の2つの ASP.NET フォーラムの投稿を参照してください。[厳密に型指定されたデータセットを使用した Objectdatasources の更新](https://forums.asp.net/1098630/ShowPost.aspx)と、 [ObjectDataSource と厳密に型指定されたデータセットに関する問題](https://forums.asp.net/1048212/ShowPost.aspx)。

次に、`AddProduct` と `UpdateProduct`の両方で、コードは `ProductsRow` インスタンスを作成し、渡されただけの値を設定します。 DataRow の DataColumns に値を代入すると、さまざまなフィールドレベルの検証チェックが発生する可能性があります。 したがって、渡された値を DataRow に手動で配置することで、BLL メソッドに渡されるデータの有効性を確保することができます。 残念ながら、Visual Studio によって生成される厳密に型指定された DataRow クラスでは、null 許容型は使用されません。 代わりに、DataRow 内の特定の DataColumn が `NULL` データベース値に対応する必要があることを示すには、`SetColumnNameNull()` メソッドを使用する必要があります。

`UpdateProduct`、最初に製品を読み込み、`GetProductByProductID(productID)`を使用して更新します。 これはデータベースへの不要なトリップのように思えるかもしれませんが、オプティミスティック同時実行制御について説明する今後のチュートリアルでは、この余分な旅行に役立ちます。 オプティミスティック同時実行制御は、同じデータに対して同時に作業している2人のユーザーが、誤って別の変更を上書きしないようにするための手法です。 レコード全体を取得することにより、DataRow の列のサブセットのみを変更する更新メソッドを作成しやすくなります。 `SuppliersBLL` クラスを探索すると、このような例が表示されます。

最後に、`ProductsBLL` クラスには、 [DataObject 属性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx)が適用されていることに注意してください (ファイルの先頭付近にある class ステートメントの直前にある `[System.ComponentModel.DataObject]` 構文)。メソッドには[DataObjectMethodAttribute 属性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)があります。 `DataObject` 属性は、クラスを[ObjectDataSource コントロール](https://msdn.microsoft.com/library/9a4kyhcx.aspx)へのバインドに適したオブジェクトとしてマークしますが、`DataObjectMethodAttribute` はメソッドの目的を示します。 今後のチュートリアルで説明するように、ASP.NET 2.0 の ObjectDataSource を使用すると、クラスのデータに簡単に宣言できます。 ObjectDataSource のウィザードで、使用可能なクラスの一覧をフィルター処理してバインドするには、既定では `DataObjects` としてマークされたクラスのみがウィザードのドロップダウンリストに表示されます。 `ProductsBLL` クラスはこれらの属性がなくても機能しますが、これらを追加すると、ObjectDataSource のウィザードでの操作が簡単になります。

## <a name="adding-the-other-classes"></a>その他のクラスの追加

`ProductsBLL` クラスが完成したら、カテゴリ、仕入先、および従業員を操作するためのクラスを追加する必要があります。 前の例の概念を使用して、次のクラスとメソッドを作成します。

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

注目すべき1つの方法は、`SuppliersBLL` クラスの `UpdateSupplierAddress` メソッドです。 このメソッドは、業者のアドレス情報だけを更新するためのインターフェイスを提供します。 内部的には、このメソッドは、指定された `supplierID` (`GetSupplierBySupplierID`を使用) の `SupplierDataRow` オブジェクトを読み取り、そのアドレス関連のプロパティを設定して、`SupplierDataTable`の `Update` メソッドにを呼び出します。 `UpdateSupplierAddress` メソッドは次のとおりです。

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample2.vb)]

BLL クラスの完全な実装については、この記事のダウンロードを参照してください。

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>手順 2: BLL クラスを使用して型指定されたデータセットにアクセスする

最初のチュートリアルでは、型指定されたデータセットをプログラムで直接操作する例を紹介しましたが、BLL クラスを追加すると、代わりに BLL に対してプレゼンテーション層が機能する必要があります。 最初のチュートリアルの `AllProducts.aspx` 例では、次のコードに示すように、`ProductsTableAdapter` を使用して製品の一覧を GridView にバインドしました。

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample3.vb)]

新しい BLL クラスを使用するには、変更する必要があるのは、単に `ProductsTableAdapter` オブジェクトを `ProductBLL` オブジェクトに置き換えるだけです。

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample4.vb)]

BLL クラスは、ObjectDataSource を使用して (型指定されたデータセットと同様に) 宣言によってアクセスすることもできます。 ObjectDataSource については、次のチュートリアルで詳しく説明します。

[製品の一覧が GridView に表示される ![](creating-a-business-logic-layer-vb/_static/image4.png)](creating-a-business-logic-layer-vb/_static/image3.png)

**図 3**: 製品の一覧が GridView に表示される ([クリックすると、フルサイズの画像が表示](creating-a-business-logic-layer-vb/_static/image5.png)されます)

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>手順 3: DataRow クラスへのフィールドレベルの検証の追加

フィールドレベルの検証は、挿入または更新時のビジネスオブジェクトのプロパティ値に関連するチェックです。 製品のフィールドレベルの検証規則には、次のようなものがあります。

- `ProductName` フィールドは40文字以下でなければなりません
- `QuantityPerUnit` フィールドの長さは20文字以下でなければなりません
- `ProductID`、`ProductName`、および `Discontinued` フィールドが必要ですが、他のすべてのフィールドは省略可能です。
- `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、および `ReorderLevel` の各フィールドには0以上の値を指定する必要があります

これらのルールは、データベースレベルで表すことができます。 `ProductName` フィールドと `QuantityPerUnit` フィールドの文字数の制限は `Products` テーブルの列のデータ型によってキャプチャされます (`nvarchar(40)` と `nvarchar(20)`それぞれ)。 データベーステーブル列で `NULL` が許可されている場合、フィールドが必須であり、省略可能であるかどうか。 0以上の値だけが `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、または `ReorderLevel` の列になるように、4つの[check 制約](https://msdn.microsoft.com/library/ms188258.aspx)が存在します。

これらの規則は、データベースで適用するだけでなく、データセットレベルでも適用する必要があります。 実際には、データテーブルの DataColumns のセットごとに、フィールドの長さと値が必須かどうか、または省略可能かどうかが既にキャプチャされています。 自動的に入力された既存のフィールドレベルの検証を表示するには、データセットデザイナーにアクセスし、いずれかの Datatable からフィールドを選択して、プロパティウィンドウにアクセスします。 図4に示すように、`ProductsDataTable` の `QuantityPerUnit` DataColumn の最大長は20文字で、`NULL` 値が許可されています。 `ProductsDataRow`の `QuantityPerUnit` プロパティを20文字より長い文字列値に設定しようとすると、`ArgumentException` がスローされます。

[DataColumn が ![基本的なフィールドレベルの検証を提供する](creating-a-business-logic-layer-vb/_static/image7.png)](creating-a-business-logic-layer-vb/_static/image6.png)

**図 4**: DataColumn は基本的なフィールドレベルの検証を提供します ([クリックすると、フルサイズの画像が表示](creating-a-business-logic-layer-vb/_static/image8.png)されます)

残念ながら、プロパティウィンドウを通じて `UnitPrice` 値が0以上である必要があるなど、境界チェックを指定することはできません。 この種類のフィールドレベルの検証を提供するには、DataTable の[Columnchanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx)イベントのイベントハンドラーを作成する必要があります。 [前のチュートリアル](creating-a-data-access-layer-vb.md)で説明したように、型指定されたデータセットによって作成されるデータセット、datatable、および DataRow オブジェクトは、部分クラスを使用して拡張できます。 この手法を使用すると、`ProductsDataTable` クラスの `ColumnChanging` イベントハンドラーを作成できます。 まず、`ProductsDataTable.ColumnChanging.vb`という名前の `App_Code` フォルダーにクラスを作成します。

[App_Code フォルダーに新しいクラスを追加 ![には](creating-a-business-logic-layer-vb/_static/image10.png)](creating-a-business-logic-layer-vb/_static/image9.png)

**図 5**: `App_Code` フォルダーに新しいクラスを追加する ([クリックすると、フルサイズの画像が表示](creating-a-business-logic-layer-vb/_static/image11.png)されます)

次に、`UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、および `ReorderLevel` 列の値が0以上であることを確認する `ColumnChanging` イベントのイベントハンドラーを作成します。 このような列が範囲外の場合は、`ArgumentException`をスローします。

製品 Datatable. ColumnChanging .vb

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample5.vb)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>手順 4: BLL のクラスにカスタムビジネスルールを追加する

フィールドレベルの検証に加えて、次のように、1つの列レベルでは表現できないさまざまなエンティティまたは概念を含む高度なカスタムビジネスルールが存在する場合があります。

- 製品が廃止された場合、その `UnitPrice` を更新することはできません
- 従業員の居住国は、管理者の居住国と同じである必要があります。
- 供給業者によって提供される唯一の製品である場合、製品を廃止することはできません。

BLL クラスには、アプリケーションのビジネスルールに準拠していることを確認するためのチェックが含まれている必要があります。 これらのチェックは、適用するメソッドに直接追加できます。

ビジネスルールによって、特定の供給業者からの唯一の製品である製品を廃止済みとしてマークできなかったとします。 つまり、製品*x*が supplier *Y*から購入した唯一の製品である場合、 *x*を廃止済みとしてマークできませんでした。ただし、supplier *Y*で*は、a*、 *B*、および*C*という3つの製品が提供されている場合、これらのいずれかを "廃止" としてマークできます。 しかし、ビジネスルールと一般的な意味は常に揃っていません。

`UpdateProducts` 方法でこのビジネスルールを適用するには、まず、`Discontinued` が `True` に設定されているかどうかを確認し、その場合は `GetProductsBySupplierID` を呼び出して、この製品の供給業者から購入した製品の数を確認します。 この業者から購入した製品が1つだけの場合は、`ApplicationException`がスローされます。

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample6.vb)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>プレゼンテーション層での検証エラーへの対応

プレゼンテーション層から BLL を呼び出すときに、発生する可能性のある例外を処理するか、ASP.NET にバブルアップさせるかを決定できます (これにより、`HttpApplication`の `Error` イベントが発生します)。 プログラムを使用して BLL を操作するときに例外を処理するには、 [Try...Catch](https://msdn.microsoft.com/library/fk6t46tz%28VS.80%29.aspx)ブロック。次に例を示します。

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample7.vb)]

今後のチュートリアルで説明するように、データ Web コントロールを使用してデータを挿入、更新、または削除するときに、BLL からバブルアップする例外の処理は、`Try...Catch` ブロックでコードをラップする必要があるのではなく、イベントハンドラーで直接処理できます。

## <a name="summary"></a>要約

適切に設計されたアプリケーションは、それぞれが特定のロールをカプセル化する別個の層に作られています。 この記事シリーズの最初のチュートリアルでは、型指定されたデータセットを使用してデータアクセス層を作成しました。このチュートリアルでは、アプリケーションの `App_Code` フォルダーにある一連のクラスとしてビジネスロジック層を構築し、DAL を呼び出します。 BLL は、アプリケーションのフィールドレベルおよびビジネスレベルのロジックを実装しています。 このチュートリアルで行ったように、別の BLL を作成するだけでなく、部分クラスを使用して Tableadapter のメソッドを拡張することもできます。 ただし、この方法を使用しても、既存のメソッドをオーバーライドすることはできません。また、この記事で説明した方法と同様に、DAL と BLL を分離することもできません。

DAL と BLL が完成したら、プレゼンテーション層から始めることができます。 次の[チュートリアル](master-pages-and-site-navigation-vb.md)では、データアクセスのトピックから簡単な迂回を作成し、チュートリアル全体で使用する一貫性のあるページレイアウトを定義します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Liz Shulok、Patterson が、Carlos Santos、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](creating-a-data-access-layer-vb.md)
> [次へ](master-pages-and-site-navigation-vb.md)
