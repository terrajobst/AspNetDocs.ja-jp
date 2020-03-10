---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: パラメーター化されたクエリをC#SqlDataSource () と共に使用するMicrosoft Docs
author: rick-anderson
description: このチュートリアルでは、SqlDataSource コントロールの概要を説明し、パラメーター化クエリを定義する方法を学習します。 パラメーターは宣言の両方を指定できます...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 241dc8c089d4faa9eb95a63684e8a56756bb302c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78444850"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-c"></a>パラメーター化されたクエリと SqlDataSource を使用する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe)または[PDF のダウンロード](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> このチュートリアルでは、SqlDataSource コントロールの概要を説明し、パラメーター化クエリを定義する方法を学習します。 パラメーターは、宣言とプログラムの両方で指定できます。また、クエリ文字列、セッション状態、その他のコントロールなど、さまざまな場所からプルできます。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、SqlDataSource コントロールを使用してデータベースからデータを直接取得する方法を説明しました。 データソースの構成ウィザードを使用して、データベースを選択し、テーブルまたはビューから返す列を選択します。カスタム SQL ステートメントを入力してください。または、ストアドプロシージャを使用します。 テーブルまたはビューから列を選択するか、カスタム SQL ステートメントを入力するかにかかわらず、SqlDataSource control s `SelectCommand` プロパティには、作成されたアドホック SQL `SELECT` ステートメントが割り当てられます。この `SELECT` ステートメントは、SqlDataSource s `Select()` メソッドが呼び出されたときに実行されます (プログラムによって、またはデータ Web コントロールから自動で)。

前のチュートリアルのデモで使用した SQL `SELECT` ステートメントには、`WHERE` の句がありませんでした。 `SELECT` ステートメントでは、`WHERE` 句を使用して、返される結果を制限できます。 たとえば、$50.00 を超える製品の名前を表示するには、次のクエリを使用します。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

通常、`WHERE` 句で使用される値は、クエリ文字列値、セッション変数、ページ上の Web コントロールからのユーザー入力など、一部の外部ソースによって決定されます。 このような入力は、*パラメーター*を使用して指定するのが理想的です。 Microsoft SQL Server では、次のように `@parameterName`を使用してパラメーターが示されます。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

SqlDataSource は、`SELECT` ステートメントと `INSERT`、`UPDATE`、および `DELETE` ステートメントの両方に対して、パラメーター化クエリをサポートします。 さらに、パラメーター値は、クエリ文字列、セッション状態、ページ上のコントロールなど、さまざまなソースから自動的に取得できます。また、プログラムで割り当てることもできます。 このチュートリアルでは、パラメーター化されたクエリを定義する方法と、パラメーターの値を宣言とプログラムの両方で指定する方法について説明します。

> [!NOTE]
> 前のチュートリアルでは、最初の46チュートリアルの中で選択されていた ObjectDataSource と、概念的な類似性について説明しました。 これらの類似点は、パラメーターにも拡張されます。 ビジネスロジック層のメソッドの入力パラメーターにマップされた ObjectDataSource s パラメーター。 SqlDataSource を使用すると、パラメーターは SQL クエリ内で直接定義されます。 両方のコントロールには、`Select()`、`Insert()`、`Update()`、および `Delete()` メソッドのパラメーターのコレクションがあります。また、これらのパラメーター値は、事前定義されたソース (querystring 値、セッション変数など) から設定することも、プログラムによって割り当てられることもあります。

## <a name="creating-a-parameterized-query"></a>パラメーター クエリの作成

SqlDataSource control s データソース構成ウィザードには、データベースレコードを取得するために実行するコマンドを定義する3つの方法が用意されています。

- 既存のテーブルまたはビューから列を選択することにより、
- カスタム SQL ステートメントを入力することによって、または
- ストアドプロシージャを選択する

既存のテーブルまたはビューから列を選択する場合は、[`WHERE` 句の追加] ダイアログボックスで `WHERE` 句のパラメーターを指定する必要があります。 ただし、カスタム SQL ステートメントを作成する場合は、パラメーターを `WHERE` 句に直接入力できます (各パラメーターを示すには `@parameterName` を使用します)。 [ストアドプロシージャ](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)は1つ以上の SQL ステートメントで構成され、これらのステートメントはパラメーター化できます。 ただし、SQL ステートメントで使用されるパラメーターは、ストアドプロシージャに入力パラメーターとして渡す必要があります。

パラメーター化されたクエリの作成は、SqlDataSource s `SelectCommand` の指定方法によって異なります。そのため、では、3つのアプローチすべてを見ていきましょう。 作業を開始するには、`SqlDataSource` フォルダーの [`ParameterizedQueries.aspx`] ページを開き、[SqlDataSource] コントロールを [ツールボックス] からデザイナーにドラッグし、`ID` を [`Products25BucksAndUnderDataSource`] に設定します。 次に、コントロール s スマートタグから [データソースの構成] リンクをクリックします。 使用するデータベース (`NORTHWINDConnectionString`) を選択し、[次へ] をクリックします。

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>手順 1: テーブルまたはビューから列を選択するときに`WHERE`句を追加する

SqlDataSource コントロールを使用してデータベースから返すデータを選択する場合、データソースの構成ウィザードでは、既存のテーブルまたはビューから返す列を選択するだけで済みます (図1を参照)。 これにより、SQL `SELECT` ステートメントが自動的に作成されます。このステートメントは、SqlDataSource s `Select()` メソッドが呼び出されたときにデータベースに送信されます。 前のチュートリアルで行ったように、ドロップダウンリストから Products テーブルを選択し、`ProductID`、`ProductName`、および `UnitPrice` 列を確認します。

[テーブルまたはビューから返す列を選択 ![には](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**図 1**: テーブルまたはビューから返す列を選択する ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png)されます)

`SELECT` ステートメントに `WHERE` 句を含めるには、[`WHERE`] ボタンをクリックします。 [`WHERE` 句の追加] ダイアログボックスが表示されます (図2を参照)。 パラメーターを追加して `SELECT` クエリによって返される結果を制限するには、まず、データをフィルター処理する列を選択します。 次に、フィルター処理に使用する演算子 (=、&lt;、&lt;=、&gt;など) を選択します。 最後に、クエリ文字列やセッション状態など、パラメーター s 値のソースを選択します。 パラメーターを構成した後、[追加] ボタンをクリックして `SELECT` クエリに含めます。

この例では、`UnitPrice` 値が $25.00 以下の結果のみを返すようにします。 そのため、[列] ドロップダウンリストから [`UnitPrice`] を選択し、[演算子] ドロップダウンリストから [=] を &lt;ます。 ハードコーディングされたパラメーター値 ($25.00 など) を使用する場合、またはパラメーター値をプログラムによって指定する場合は、[ソース] ボックスの一覧から [なし] を選択します。 次に、ハードコーディングされたパラメーター値をテキストボックス25.00 に入力し、[追加] ボタンをクリックしてプロセスを完了します。

[[WHERE 句の追加] ダイアログボックスから返される結果を制限 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**図 2**: [`WHERE` 句の追加] ダイアログボックスで返される結果を制限[する (クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png)されます)

パラメーターを追加したら、[OK] をクリックして、データソースの構成ウィザードに戻ります。 ウィザードの下部にある `SELECT` ステートメントに、`@UnitPrice`という名前のパラメーターを持つ `WHERE` 句が含まれるようになりました。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> [`WHERE` 句の追加] ダイアログボックスで `WHERE` 句に複数の条件を指定した場合は、ウィザードによって `AND` 演算子と結合されます。 `WHERE` 句 (`WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`など) に `OR` を含める必要がある場合は、[カスタム SQL ステートメント] 画面を使用して `SELECT` ステートメントを作成する必要があります。

SqlDataSource の構成を完了します ([次へ]、[完了] の順にクリック)。次に、SqlDataSource s 宣言型マークアップを調べます。 マークアップには、`<SelectParameters>` コレクションが含まれるようになりました。これにより、`SelectCommand`内のパラメーターのソースが特定されます。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

SqlDataSource s `Select()` メソッドが呼び出されると、データベースに送信される前に、`UnitPrice` パラメーター値 (25.00) が `SelectCommand` 内の `@UnitPrice` パラメーターに適用されます。 結果として、$25.00 以下の製品のみが `Products` テーブルから返されます。 これを確認するには、GridView をページに追加し、このデータソースにバインドしてから、ブラウザーを使用してページを表示します。 図3に示すように、$25.00 以下の製品のみが表示されます。

[![$25.00 以下の製品のみが表示されます](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**図 3**: $25.00 以下の製品のみが表示されます ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png)されます)

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>手順 2: カスタム SQL ステートメントへのパラメーターの追加

カスタム SQL ステートメントを追加する場合は、`WHERE` 句に明示的に入力するか、クエリビルダーのフィルターセルに値を指定します。 これを示すために、には、特定のしきい値未満の価格を持つ GridView の製品のみが表示されます。 まず、`ParameterizedQueries.aspx` ページにテキストボックスを追加して、ユーザーからこのしきい値を収集します。 TextBox s `ID` プロパティを `MaxPrice`に設定します。 ボタン Web コントロールを追加し、一致する製品を表示するように `Text` プロパティを設定します。

次に、GridView をページにドラッグし、そのスマートタグから `ProductsFilteredByPriceDataSource`という名前の新しい SqlDataSource を作成します。 データソースの構成ウィザードで、[カスタム SQL ステートメントまたはストアドプロシージャの指定] 画面に進み (図4を参照)、次のクエリを入力します。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

(手動またはクエリビルダーを使用して) クエリを入力したら、[次へ] をクリックします。

[パラメーター値以下の製品のみを返す ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**図 4**: パラメーター値以下の製品のみを返す (クリックすると、[フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png)されます)

クエリにはパラメーターが含まれているため、ウィザードの次の画面では、パラメーター値のソースを入力するように求められます。 [パラメーターのソース] ボックスの一覧から [コントロール] を選択し、[ControlID] ドロップダウンリストから `MaxPrice` (TextBox コントロール s `ID` 値) を選択します。 ユーザーが `MaxPrice` テキストボックスにテキストを入力していない場合に使用するオプションの既定値を入力することもできます。 時間については、既定値を入力しないでください。

[パラメーターのソースとして MaxPrice TextBox s Text プロパティが使用されて ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**図 5**: `MaxPrice` TextBox s `Text` プロパティがパラメーターソースとして使用されている ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png)されます)

[次へ]、[完了] の順にクリックして、データソースの構成ウィザードを完了します。 GridView、TextBox、Button、および SqlDataSource の宣言型マークアップは、次のようになります。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

SqlDataSource s `<SelectParameters>` セクション内のパラメーターは `ControlParameter`であり、`ControlID` や `PropertyName`などの追加のプロパティが含まれていることに注意してください。 SqlDataSource s `Select()` メソッドが呼び出されると、`ControlParameter` は、指定された Web コントロールプロパティから値を取得し、`SelectCommand`内の対応するパラメーターに割り当てます。 この例では、`MaxPrice` s Text プロパティが `@MaxPrice` パラメーター値として使用されています。

ブラウザーを使用してこのページを表示します。 最初にページにアクセスしたとき、または `MaxPrice` TextBox に値がない場合は、GridView にレコードが表示されません。

[MaxPrice テキストボックスが空のときにレコードが表示されない ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**図 6**: `MaxPrice` テキストボックスが空のときにレコードが表示されない ([クリックしてフルサイズの画像を表示する](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png))

製品が表示されない理由は、既定では、パラメーター値の空の文字列がデータベース `NULL` 値に変換されるためです。 `[UnitPrice] <= NULL` の比較は常に False と評価されるため、結果は返されません。

テキストボックスに5.00 のような値を入力し、[一致する製品の表示] ボタンをクリックします。 ポストバック時に、SqlDataSource は、パラメーターソースの1つが変更されたことを GridView に通知します。 その結果、GridView は、$5.00 以下の製品を表示して SqlDataSource に再バインドされます。

[$5.00 以下の ![製品が表示されます](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**図 7**: $5.00 以下の製品が表示される ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png)されます)

## <a name="initially-displaying-all-products"></a>すべての製品を最初に表示

ページが最初に読み込まれたときに製品を表示するのではなく、*すべて*の製品を表示することをお勧めします。 `MaxPrice` テキストボックスが空のときにすべての製品を一覧表示する方法の1つとして、パラメーター s の既定値を非常 high 値 (100万など) に設定する方法があります。これは、Northwind Traders では、単価が $100万を超える在庫を持つ可能性が低いためです。 ただし、この方法は shortsighted であり、他の状況では機能しない可能性があります。

前のチュートリアル-[宣言型パラメーター](../basic-reporting/declarative-parameters-cs.md)と[、DropDownList を使用したマスター/詳細フィルター処理](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)では、同様の問題が発生しました。 このソリューションでは、このロジックをビジネスロジック層に配置する必要がありました。 具体的には、BLL は受信値を確認し、`NULL` または予約された値の場合は、すべてのレコードを返す DAL メソッドに呼び出しをルーティングしました。 受信した値が通常のフィルター選択値の場合は、指定された値を持つパラメーター化された `WHERE` 句を使用した SQL ステートメントを実行した DAL メソッドが呼び出されます。

残念ながら、SqlDataSource を使用する場合、アーキテクチャは無視されます。 代わりに、`@MaximumPrice` パラメーターが `NULL` または予約済みの値である場合は、すべてのレコードをインテリジェントに取得するように SQL ステートメントをカスタマイズする必要があります。 この演習では、`@MaximumPrice` パラメーターが `-1.0`と等しい場合に、*すべて*のレコードが返されるようにします (製品に負の `UnitPrice` 値を設定することはできないため、`-1.0` は予約済みの値として機能します)。 これを実現するには、次の SQL ステートメントを使用します。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

この `WHERE` 句は、`@MaximumPrice` パラメーターが `-1.0`の場合に*すべて*のレコードを返します。 パラメーター値が `-1.0`されていない場合は、`UnitPrice` が `@MaximumPrice` パラメーター値以下の製品のみが返されます。 `@MaximumPrice` パラメーターの既定値を `-1.0`に設定すると、最初のページの読み込み時 (または [`MaxPrice`] ボックスが空のとき) に、`@MaximumPrice` の値が `-1.0` になり、すべての製品が表示されます。

[![MaxPrice テキストボックスが空のときにすべての製品が表示されるようになりました。](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**図 8**: `MaxPrice` テキストボックスが空のときにすべての製品が表示されるようになりました ([クリックしてフルサイズの画像を表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png))

この方法で注意すべき注意事項がいくつかあります。 まず、パラメーター s データ型が SQL クエリでの使用によって推論されることに注意してください。 `WHERE` 句を `@MaximumPrice = -1.0` から `@MaximumPrice = -1`に変更した場合、ランタイムはパラメーターを整数として扱います。 その後、`MaxPrice` テキストボックスを10進数値 (5.00 など) に割り当てようとすると、5.00 を整数に変換できないため、エラーが発生します。 これを解決するには、`WHERE` 句で `@MaximumPrice = -1.0` を使用していることを確認するか、さらに優れた `ControlParameter` オブジェクト s `Type` プロパティを Decimal に設定します。

2つ目の方法として、`OR @MaximumPrice = -1.0` を `WHERE` 句に追加すると、クエリエンジンは `UnitPrice` (存在する場合) のインデックスを使用できず、その結果、テーブルスキャンが実行されます。 これは、`Products` テーブルに十分な数のレコードがある場合に、パフォーマンスに影響を与える可能性があります。 より適切な方法は、このロジックをストアドプロシージャに移行することです。この場合、すべてのレコードを返す必要がある場合、または `WHERE` 句に `UnitPrice` 条件だけが含まれている場合は、`WHERE` 句を指定せずに、`IF` ステートメントで `Products` テーブルから `SELECT` クエリを実行することで、インデックスを使用できます。

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>手順 3: パラメーター化されたストアドプロシージャの作成と使用

ストアドプロシージャには、ストアドプロシージャ内で定義されている SQL ステートメントで使用できる一連の入力パラメーターを含めることができます。 入力パラメーターを受け取るストアドプロシージャを使用するように SqlDataSource を構成する場合、アドホック SQL ステートメントと同じ手法を使用して、これらのパラメーター値を指定できます。

SqlDataSource でストアドプロシージャを使用する方法を示すために、`GetProductsByCategory`という名前の Northwind データベースに新しいストアドプロシージャを作成します。このストアドプロシージャは `@CategoryID` という名前のパラメーターを受け取り、`CategoryID` 列が `@CategoryID`と一致する製品のすべての列を返します。 ストアドプロシージャを作成するには、サーバーエクスプローラーに移動し、`NORTHWND.MDF` データベースにドリルダウンします。 (サーバーエクスプローラーが表示されない場合は、[表示] メニューに移動して [サーバーエクスプローラー] オプションを選択すると表示されます)。

`NORTHWND.MDF` データベースで、[ストアドプロシージャ] フォルダーを右クリックし、[新しいストアドプロシージャの追加] を選択して、次の構文を入力します。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

保存アイコン (または Ctrl + S) をクリックして、ストアドプロシージャを保存します。 ストアドプロシージャをテストするには、[ストアドプロシージャ] フォルダーでストアドプロシージャを右クリックし、[実行] をクリックします。 これにより、ストアドプロシージャ s パラメーター (このインスタンスでは`@CategoryID`) を入力するように求められます。その後、結果が出力ウィンドウに表示されます。

[@CategoryID を1にして実行したときに Get$ Bycategory ストアドプロシージャを ![する](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**図 9**: `@CategoryID` を1にして実行した場合の `GetProductsByCategory` ストアドプロシージャ ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png)されます)

このストアドプロシージャを使用して、[飲料] カテゴリのすべての製品を GridView に表示します。 新しい GridView をページに追加し、`BeverageProductsDataSource`という名前の新しい SqlDataSource にバインドします。 [カスタム SQL ステートメントまたはストアドプロシージャの指定] 画面に進み、[ストアドプロシージャ] オプションボタンを選択し、ドロップダウンリストから `GetProductsByCategory` ストアドプロシージャを選択します。

[![ドロップダウンリストから [Get$ Bycategory] ストアドプロシージャを選択します。](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**図 10**: ドロップダウンリストから `GetProductsByCategory` ストアドプロシージャを選択[する (クリックしてフルサイズの画像を表示する](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png))

ストアドプロシージャは入力パラメーター (`@CategoryID`) を受け入れるため、[次へ] をクリックすると、このパラメーターの値のソースを指定するように求められます。 飲み物 `CategoryID` は1であるため、[パラメーターのソース] ボックスの一覧は [なし] のままにして、[DefaultValue] ボックスに「1」と入力します。

[ハードコーディングされた値1を使用して飲料カテゴリの製品を返す ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**図 11**: ハードコーディングされた値1を使用して飲料カテゴリの製品を返す ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png)されます)

次の宣言型マークアップに示すように、ストアドプロシージャを使用する場合、SqlDataSource s `SelectCommand` プロパティはストアドプロシージャの名前に設定され、 [`SelectCommandType` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx)は `StoredProcedure`に設定されます。これは、`SelectCommand` がアドホック SQL ステートメントではなくストアドプロシージャの名前であることを示します。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

ブラウザーでページをテストします。 飲料カテゴリに属する製品のみが表示されます。ただし、`GetProductsByCategory` ストアドプロシージャからは、`Products` テーブルのすべての列が返されるので、*すべて*の product フィールドが表示されます。 もちろん、gridview の [列の編集] ダイアログボックスから GridView に表示されるフィールドを制限したり、カスタマイズしたりすることができます。

[すべての飲み物が表示され ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**図 12**: すべての飲み物が表示されます ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png)されます)

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>手順 4: プログラムによる SqlDataSource s`Select()`ステートメントの呼び出し

前のチュートリアルで説明した例とこのチュートリアルでは、SqlDataSource コントロールを直接 GridView にバインドしました。 ただし、SqlDataSource コントロールのデータは、プログラムによってコード内でアクセスおよび列挙できます。 これは、データを照会して検査する必要があるが、表示する必要がない場合に特に便利です。 データベースに接続してコマンドを指定し、結果を取得するために、すべての定型 ADO.NET コードを記述するのではなく、SqlDataSource がこの単調なコードを処理できるようにすることができます。

プログラムによって SqlDataSource s データを操作する方法を示すために、上司がランダムに選択されたカテゴリとそれに関連付けられた製品の名前を表示する web ページを作成するように要求することを想定しています。 つまり、ユーザーがこのページにアクセスすると、`Categories` テーブルからランダムにカテゴリを選択し、カテゴリ名を表示して、そのカテゴリに属する製品を一覧表示する必要があります。

これを実現するには、2つの SqlDataSource コントロールが必要です。1つは `Categories` テーブルからランダムなカテゴリを取得し、もう1つは category s 製品を取得するためです。 この手順では、ランダムなカテゴリレコードを取得する SqlDataSource を作成します。手順5では、カテゴリの製品を取得する SqlDataSource の構築について説明します。

まず、`ParameterizedQueries.aspx` に SqlDataSource を追加し、その `ID` を `RandomCategoryDataSource`に設定します。 次の SQL クエリを使用するように構成します。

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()` は、ランダムな順序で並べ替えられたレコードを返します (「 [`NEWID()` を使用してレコードをランダムに並べ替える](http://www.sqlteam.com/item.asp?ItemID=8747)」を参照してください)。 `SELECT TOP 1` は、結果セットの最初のレコードを返します。 このクエリでは、ランダムに選択された単一のカテゴリから、`CategoryID` と `CategoryName` 列の値が返されます。

Category s `CategoryName` の値を表示するには、ラベル Web コントロールをページに追加し、その `ID` プロパティを `CategoryNameLabel`に設定して、その `Text` プロパティをオフにします。 プログラムによって SqlDataSource コントロールからデータを取得するには、`Select()` メソッドを呼び出す必要があります。 [`Select()` メソッド](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx)では、返される前にデータをどのようにメッセージするかを指定する[`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)型の1つの入力パラメーターが必要です。 これには、データの並べ替えとフィルター処理に関する指示が含まれ、SqlDataSource コントロールからのデータの並べ替えやページングを行うときに、データ Web コントロールによって使用されます。 ただし、この例では、返される前にデータを変更する必要はないため、`DataSourceSelectArguments.Empty` オブジェクトに渡されます。

`Select()` メソッドは、`IEnumerable`を実装するオブジェクトを返します。 返される正確な型は、SqlDataSource control s [`DataSourceMode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)の値によって異なります。 前のチュートリアルで説明したように、このプロパティは `DataSet` または `DataReader`のいずれかの値に設定できます。 `DataSet`に設定した場合、`Select()` メソッドは[DataView](https://msdn.microsoft.com/library/01s96x0z.aspx)オブジェクトを返します。`DataReader`に設定すると、 [`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx)を実装するオブジェクトが返されます。 `RandomCategoryDataSource` SqlDataSource の `DataSourceMode` プロパティは `DataSet` (既定値) に設定されているため、DataView オブジェクトを操作します。

次のコードは、DataView として `RandomCategoryDataSource` SqlDataSource からレコードを取得する方法と、最初の DataView 行から `CategoryName` 列の値を読み取る方法を示しています。

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` は、DataView 内の最初の `DataRowView` を返します。 `randomCategoryView[0]["CategoryName"]` は、この最初の行の `CategoryName` 列の値を返します。 DataView は弱く型指定されていることに注意してください。 特定の列の値を参照するには、列の名前を文字列として渡す必要があります (この場合は)。 図13は、ページを表示するときに `CategoryNameLabel` に表示されるメッセージを示しています。 もちろん、実際に表示されるカテゴリ名は、ページにアクセスするたびに (ポストバックを含む) `RandomCategoryDataSource` SqlDataSource によってランダムに選択されます。

[ランダムに選択されたカテゴリの名前が表示さ ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**図 13**: ランダムに選択されたカテゴリの名前が表示される ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png)されます)

> [!NOTE]
> SqlDataSource control s `DataSourceMode` プロパティが `DataReader`に設定されている場合は、`Select()` メソッドからの戻り値を `IDataReader`にキャストする必要があります。 最初の行から `CategoryName` 列の値を読み取るには、次のようなコードを使用します。

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

SqlDataSource でカテゴリをランダムに選択し、カテゴリの製品を一覧表示する GridView を追加する準備ができました。

> [!NOTE]
> ラベル Web コントロールを使用してカテゴリ名を表示するのではなく、ページに FormView または DetailsView を追加して、SqlDataSource にバインドすることができます。 ただし、ラベルを使用すると、プログラムで SqlDataSource s `Select()` ステートメントを呼び出し、結果のデータをコードで操作する方法を調べることができました。

## <a name="step-5-assigning-parameter-values-programmatically"></a>手順 5: プログラムによるパラメーター値の割り当て

このチュートリアルでこれまでに説明したすべての例では、ハードコーディングされたパラメーター値を使用しているか、事前に定義されたパラメーターのソース (querystring の値、ページの Web コントロールなど) のいずれかを使用しています。 ただし、SqlDataSource コントロール s パラメーターはプログラムで設定することもできます。 現在の例を完了するには、指定されたカテゴリに属するすべての製品を返す SqlDataSource が必要です。 この SqlDataSource には、`Page_Load` イベントハンドラーの SqlDataSource `RandomCategoryDataSource` によって返される `CategoryID` 列の値に基づいて値を設定する必要がある `CategoryID` パラメーターがあります。

まず、GridView をページに追加し、`ProductsByCategoryDataSource`という名前の新しい SqlDataSource にバインドします。 手順3で行ったのと同様に、`GetProductsByCategory` ストアドプロシージャを呼び出すように SqlDataSource を構成します。 [パラメーターソース] ドロップダウンリストは [なし] のままにします。ただし、この既定値はプログラムによって設定されるため、既定値は入力しないでください。

[パラメーターのソースまたは既定値を指定し ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**図 14**: パラメーターのソースまたは既定値を指定しない ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png)されます)

SqlDataSource ウィザードを完了すると、次のような宣言型マークアップが表示されます。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

`CategoryID` パラメーターの `DefaultValue` は、`Page_Load` イベントハンドラーでプログラムを使用して割り当てることができます。

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

この追加により、ランダムに選択されたカテゴリに関連付けられている製品を示す GridView がページに含まれます。

[パラメーターのソースまたは既定値を指定し ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**図 15**: パラメーターのソースまたは既定値を指定しない ([クリックすると、フルサイズの画像が表示](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png)されます)

## <a name="summary"></a>まとめ

SqlDataSource を使用すると、ページ開発者は、パラメーター化されたクエリを定義して、パラメーター値をハードコーディングしたり、定義済みのパラメーターソースから取得したり、プログラムによって割り当てたりすることができます。 このチュートリアルでは、アドホック SQL クエリとストアドプロシージャの両方について、データソースの構成ウィザードからパラメーター化クエリを作成する方法について説明しました。 また、ハードコーディングされたパラメーターソース、パラメーターソースとしての Web コントロール、およびパラメーター値をプログラムによって指定する方法についても説明しました。

ObjectDataSource と同様に、SqlDataSource には、基になるデータを変更する機能も用意されています。 次のチュートリアルでは、SqlDataSource を使用して `INSERT`、`UPDATE`、および `DELETE` ステートメントを定義する方法について説明します。 これらのステートメントを追加したら、GridView、DetailsView、および FormView コントロールに固有の組み込みの挿入、編集、および削除機能を利用できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Scott Clyde、Randell の機能、および Ken による Isa です。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](querying-data-with-the-sqldatasource-control-cs.md)
> [次へ](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
