---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
title: SqlDataSource (C#) を使用したデータの挿入、更新、および削除Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、ObjectDataSource コントロールでデータの挿入、更新、および削除を許可する方法について学習しました。 SqlDataSource コントロールでサポートされている...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a526f0ec-779e-4a2b-a476-6604090d25ce
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 495e0e81a67e6926e1c4fa92e29ebbda747cd418
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445018"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-c"></a>SqlDataSource でデータを挿入、更新、削除する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_CS.exe)または[PDF のダウンロード](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/datatutorial49cs1.pdf)

> 前のチュートリアルでは、ObjectDataSource コントロールでデータの挿入、更新、および削除を許可する方法について学習しました。 SqlDataSource コントロールは同じ操作をサポートしますが、この方法は異なります。このチュートリアルでは、データの挿入、更新、および削除を行うための SqlDataSource を構成する方法について説明します。

## <a name="introduction"></a>はじめに

[挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)について説明したように、GridView コントロールには、組み込みの更新および削除機能が用意されています。また、DetailsView コントロールと FormView コントロールには、編集および削除機能と共に挿入サポートが含まれています。 これらのデータ変更機能は、コード行を記述しなくても、データソースコントロールに直接接続できます。 [挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)については、ObjectDataSource を使用して、GridView、DetailsView、FormView コントロールでの挿入、更新、および削除を容易にします。 または、ObjectDataSource の代わりに SqlDataSource を使用することもできます。

挿入、更新、および削除をサポートするために、ObjectDataSource を使用して、挿入、更新、または削除アクションを実行するために呼び出すオブジェクトレイヤーメソッドを指定する必要があることを思い出してください。 SqlDataSource を使用する場合は、`INSERT`、`UPDATE`、および `DELETE` SQL ステートメント (またはストアドプロシージャ) を実行する必要があります。 このチュートリアルで説明するように、これらのステートメントは手動で作成することも、SqlDataSource s データソース構成ウィザードで自動的に生成することもできます。

> [!NOTE]
> GridView、DetailsView、および FormView コントロールの挿入、編集、および削除機能については既に説明したので、このチュートリアルでは、これらの操作をサポートする SqlDataSource コントロールの構成に焦点を当てます。 GridView、DetailsView、および FormView 内でこれらの機能を実装するときにブラシを作成する必要がある場合は、データの編集、挿入、および削除に関するチュートリアルに戻り、[挿入、更新、削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)を説明します。

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>手順 1:`INSERT`、`UPDATE`、および`DELETE`ステートメントの指定

これまでの2つのチュートリアルで説明したように、SqlDataSource コントロールからデータを取得するには、次の2つのプロパティを設定する必要があります。

1. `ConnectionString`。クエリの送信先となるデータベースを指定します。
2. `SelectCommand`。結果を返すために実行するアドホック SQL ステートメントまたはストアドプロシージャ名を指定します。

パラメーターを持つ `SelectCommand` 値の場合、パラメーター値は SqlDataSource s `SelectParameters` コレクションを介して指定され、ハードコーディングされた値、共通パラメーターソース値 (querystring フィールド、セッション変数、Web コントロール値など)、またはプログラムによって割り当てられることがあります。 SqlDataSource control s `Select()` メソッドがプログラムによって、またはデータ Web コントロールから自動的に呼び出されると、データベースへの接続が確立され、パラメーター値がクエリに割り当てられ、コマンドがデータベースに shuttled されます。 結果は、コントロール s の `DataSourceMode` プロパティの値に応じて、データセットまたは DataReader として返されます。

データの選択と共に、SqlDataSource コントロールを使用して、`INSERT`、`UPDATE`、および `DELETE` SQL ステートメントをほぼ同じ方法で挿入、更新、および削除することができます。 実行する SQL ステートメント `INSERT`、`UPDATE`、および `DELETE` の `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティを割り当てるだけです。 ステートメントにパラメーターがある場合は (ほとんどの場合)、`InsertParameters`、`UpdateParameters`、および `DeleteParameters` コレクションに含めます。

`InsertCommand`、`UpdateCommand`、または `DeleteCommand` 値が指定されると、対応するデータ Web コントロール s スマートタグの [挿入の有効化]、[編集の有効化]、または [削除の有効化] オプションが使用できるようになります。 これを説明するために、「 [SqlDataSource Control チュートリアルを使用](querying-data-with-the-sqldatasource-control-cs.md)してデータにクエリを実行する」で作成した `Querying.aspx` ページから例を見て、削除機能を含むように拡張します。

まず、`SqlDataSource` フォルダーから `InsertUpdateDelete.aspx` ページと `Querying.aspx` ページを開きます。 `Querying.aspx` ページのデザイナーから、最初の例の SqlDataSource と GridView (`ProductsDataSource` コントロールと `GridView1` コントロール) を選択します。 2つのコントロールを選択したら、[編集] メニューの [コピー] をクリックします (または、Ctrl + C キーを押します)。 次に、`InsertUpdateDelete.aspx` のデザイナーにアクセスして、コントロールを貼り付けます。 2つのコントロールを `InsertUpdateDelete.aspx`に移動したら、ブラウザーでページをテストします。 `Products` データベーステーブルのすべてのレコードについて、`ProductID`、`ProductName`、および `UnitPrice` 列の値が表示されます。

[すべての製品が ProductID で並べ替えられて ![表示されます。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.png)

**図 1**: すべての製品が `ProductID` 順に一覧表示されます ([クリックすると、フルサイズの画像が表示](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.png)されます)

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>SqlDataSource s`DeleteCommand`と`DeleteParameters`プロパティの追加

この時点で、`Products` テーブルのすべてのレコードと、このデータを表示する GridView が返されるのは、SqlDataSource です。 目標は、この例を拡張して、ユーザーが GridView で製品を削除できるようにすることです。 これを実現するには、SqlDataSource コントロール s `DeleteCommand` と `DeleteParameters` プロパティの値を指定してから、削除をサポートするように GridView を構成する必要があります。

`DeleteCommand` プロパティと `DeleteParameters` プロパティは、さまざまな方法で指定できます。

- 宣言型の構文を使用する
- デザイナーのプロパティウィンドウから
- データソース構成ウィザードの [カスタム SQL ステートメントまたはストアドプロシージャの指定] 画面から
- データソースの構成ウィザードの [ビューのテーブルから列を指定] 画面の [詳細設定] ボタンを使用して、`DeleteCommand` と `DeleteParameters` のプロパティで使用される `DELETE` SQL ステートメントとパラメーターコレクションを実際に自動的に生成します。

ここでは、手順 2. で `DELETE` ステートメントを自動的に作成する方法について説明します。 ここでは、デザイナーのプロパティウィンドウを使用します。ただし、データソースの構成ウィザードまたは宣言型の構文オプションは同様に機能します。

`InsertUpdateDelete.aspx`のデザイナーで、SqlDataSource `ProductsDataSource` をクリックし、プロパティウィンドウを表示します ([表示] メニューの [プロパティウィンドウ] をクリックするか、F4 キーを押します)。 [DeleteQuery] プロパティを選択すると、一連の省略記号が表示されます。

![[プロパティ] ウィンドウで DeleteQuery プロパティを選択します。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.gif)

**図 2**: [プロパティ] ウィンドウで Deletequery プロパティを選択する

> [!NOTE]
> SqlDataSource に DeleteQuery プロパティがありません。 DeleteQuery は、`DeleteCommand` プロパティと `DeleteParameters` プロパティの組み合わせであり、デザイナーでウィンドウを表示するときにプロパティウィンドウにのみ表示されます。 ソースビューのプロパティウィンドウを参照している場合は、代わりに `DeleteCommand` プロパティが見つかります。

DeleteQuery プロパティの省略記号をクリックして、[コマンドおよびパラメーターエディター] ダイアログボックスを表示します (図3を参照)。 このダイアログボックスでは、`DELETE` SQL ステートメントを指定し、パラメーターを指定できます。 [`DELETE` コマンド] ボックスに次のクエリを入力します (手動で、または必要に応じてクエリビルダーを使用します)。

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample1.sql)]

次に、[パラメーターの更新] ボタンをクリックして、以下のパラメーターの一覧に `@ProductID` パラメーターを追加します。

[![[プロパティ] ウィンドウで DeleteQuery プロパティを選択します。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.png)

**図 3**: [プロパティ] ウィンドウで Deletequery プロパティを選択[する (クリックすると、フルサイズの画像が表示](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.png)されます)

このパラメーターに値を指定しないでください (パラメーターソースは None のままにし*て*おきます)。 削除サポートを GridView に追加すると、GridView は、[削除] ボタンがクリックされた行の `DataKeys` コレクションの値を使用して、このパラメーター値を自動的に指定します。

> [!NOTE]
> `DELETE` クエリで使用されるパラメーター名は、GridView、DetailsView、または FormView の `DataKeyNames` 値の名前と同じで*ある必要があり*ます。 つまり、Products テーブルの主キー列名 (したがって、GridView のいる datakeynames 値) が `ProductID`であるため、`DELETE` ステートメントのパラメーターには `@ProductID` (たとえば、`@ID`) という名前が付けられています。

パラメーター名と `DataKeyNames` 値が一致しない場合、GridView は `DataKeys` コレクションの値にパラメーターを自動的に割り当てることはできません。

[コマンドおよびパラメーターエディター] ダイアログボックスに削除関連の情報を入力したら、[OK] をクリックし、ソースビューにアクセスして、結果の宣言型マークアップを確認します。

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample2.aspx)]

`DeleteCommand` プロパティ、`<DeleteParameters>` セクション、および `productID`という名前のパラメーターオブジェクトが追加されていることに注意してください。

## <a name="configuring-the-gridview-for-deleting"></a>削除のための GridView の構成

`DeleteCommand` プロパティが追加されたので、GridView s スマートタグに [削除を有効にする] オプションが含まれるようになりました。 さあ、このチェックボックスをオンにします。 [挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)について説明したように、これにより、GridView は `ShowDeleteButton` プロパティが `true`に設定された commandfield を追加します。 図4に示すように、ブラウザーを使用してページにアクセスすると、[削除] ボタンが表示されます。 このページをテストするには、いくつかの製品を削除します。

[各 GridView 行に [Delete] ボタンが追加され ![](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.png)

**図 4**: 各 GridView 行に Delete ボタンが追加されました ([クリックすると、フルサイズの画像が表示](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.png)されます)

[削除] ボタンをクリックするとポストバックが発生すると、GridView は、[削除] ボタンをクリックした行の `DataKeys` コレクション値の値を `ProductID` パラメーターに割り当て、SqlDataSource s `Delete()` メソッドを呼び出します。 次に、SqlDataSource コントロールはデータベースに接続し、`DELETE` ステートメントを実行します。 次に、GridView は SqlDataSource に再バインドし、現在の製品セットを取得して表示します (削除されたレコードは含まれなくなりました)。

> [!NOTE]
> GridView は `DataKeys` コレクションを使用して SqlDataSource パラメーターを設定するため、GridView の `DataKeyNames` プロパティが主キーを構成する列に設定され、SqlDataSource s `SelectCommand` によってこれらの列が返されることが重要です。 さらに、SqlDataSource s `DeleteCommand` のパラメーター名が `@ProductID`に設定されていることが重要です。 `DataKeyNames` プロパティが設定されていない場合、またはパラメーターの名前が `@ProductsID`でない場合は、[削除] ボタンをクリックするとポストバックが発生しますが、実際にはレコードは削除されません。

図5は、この対話をグラフィカルに示しています。 データ Web コントロールからの挿入、更新、および削除に関連するイベントのチェーンの詳細については、「[挿入、更新、および削除に関連するイベントの調査」](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)を参照してください。

![GridView の [削除] ボタンをクリックすると、SqlDataSource s Delete () メソッドが呼び出されます。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.gif)

**図 5**: GridView の [削除] ボタンをクリックすると、SqlDataSource s `Delete()` メソッドが呼び出される

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>手順 2:`INSERT`、`UPDATE`、および`DELETE`ステートメントを自動的に生成する

手順 1. で確認したように、`INSERT`、`UPDATE`、および `DELETE` SQL ステートメントは、プロパティウィンドウまたはコントロール s 宣言構文を使用して指定できます。 ただし、この方法では手動で SQL ステートメントを手動で書き出す必要がありますが、単調なとエラーが発生しやすくなります。 幸いにも、データソースの構成ウィザードでは、[ビューのテーブルから列を指定] 画面を使用して、`INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成するオプションが用意されています。

ここでは、この自動生成オプションについて説明します。 `InsertUpdateDelete.aspx` のデザイナーに DetailsView を追加し、その `ID` プロパティを `ManageProducts`に設定します。 次に、[DetailsView s] スマートタグから、新しいデータソースを作成し、`ManageProductsDataSource`という名前の SqlDataSource を作成します。

[Manage製品 Datasource という名前の新しい SqlDataSource を作成 ![には](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.png)

**図 6**: `ManageProductsDataSource` という名前の新しい SqlDataSource を作成[する (クリックすると、フルサイズの画像が表示](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.png)される)

データソースの構成ウィザードで、`NORTHWINDConnectionString` 接続文字列を使用することを選択し、[次へ] をクリックします。 [Select ステートメントの構成] 画面で、[テーブルまたはビューから列を指定する] ラジオボタンを選択したままにして、ドロップダウンリストから `Products` テーブルを選択します。 `ProductID`、`ProductName`、`UnitPrice`、および `Discontinued` の列をチェックボックスの一覧から選択します。

[Products テーブルを使用して ![、ProductID、ProductName、UnitPrice、および廃止された列を返します。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.png)

**図 7**: `Products` テーブルを使用して、`ProductID`、`ProductName`、`UnitPrice`、および `Discontinued` 列を返す ([クリックすると、フルサイズの画像が表示](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image10.png)されます)

選択したテーブルと列に基づいて `INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成するには、[詳細設定] ボタンをクリックし、[`INSERT`の生成]、[`UPDATE`]、[`DELETE` ステートメント] チェックボックスをオンにします。

![[INSERT、UPDATE、および DELETE ステートメントの生成] チェックボックスをオンにします。](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.gif)

**図 8**: [`INSERT`の生成]、[`UPDATE`]、および [`DELETE` ステートメント] チェックボックスをオンにする

[`INSERT`の生成]、[`UPDATE`]、および [`DELETE` ステートメント] チェックボックスは、選択したテーブルに主キーがあり、主キー列 (または列) が返された列の一覧に含まれている場合にのみチェック可能なになります。 [オプティミスティック同時実行制御を使用する] チェックボックスをオンにすると、[`INSERT`の生成]、[`UPDATE`]、および [`DELETE` ステートメント] チェックボックスがオンになった後に選択できるようになります。このチェックボックスをオンにすると、結果の `UPDATE` ステートメントと `DELETE` ステートメント内の `WHERE` 句が拡張され、 ここでは、このチェックボックスをオフのままにします。オプティミスティック同時実行制御については、次のチュートリアルでは SqlDataSource コントロールを使用します。

[`INSERT`の生成]、[`UPDATE`、および `DELETE` ステートメント] チェックボックスをオンにした後、[OK] をクリックして [Select ステートメントの構成] 画面に戻り、[次へ] をクリックして、[完了] をクリックし、データソースの構成ウィザードを完了します。 ウィザードを完了すると、Visual Studio によって、`ProductID`、`ProductName`、および `UnitPrice` 列の DetailsView に BoundFields が追加され、`Discontinued` 列の CheckBoxField が表示されます。 DetailsView s スマートタグから、[ページングを有効にする] オプションをオンにして、このページにアクセスするユーザーが製品をステップ実行できるようにします。 また、DetailsView の `Width` と `Height` プロパティもクリアします。

スマートタグの [挿入を有効にする]、[編集を有効にする]、および [削除オプションを有効にする] があることに注意してください。 これは、次の宣言構文に示すように、SqlDataSource に `InsertCommand`、`UpdateCommand`、および `DeleteCommand`の値が含まれているためです。

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample3.aspx)]

SqlDataSource コントロールの `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティに対して値が自動的に設定されていることに注意してください。 `InsertCommand` プロパティと `UpdateCommand` プロパティで参照される列のセットは、`SELECT` ステートメントの列に基づいています。 つまり、`InsertCommand` および `UpdateCommand`内の*すべて*の Products 列を使用するのではなく、`SelectCommand` で指定された列 `ProductID`( [`IDENTITY` 列](http://www.sqlteam.com/item.asp?ItemID=102)であるため、省略されています。これは、編集時に値を変更できず、挿入時に自動的に割り当てられます)。 さらに、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` プロパティの各パラメーターには、`InsertParameters`、`UpdateParameters`、および `DeleteParameters` コレクションに対応するパラメーターがあります。

DetailsView のデータ変更機能を有効にするには、[挿入を有効にする]、[編集を有効にする]、および [スマートタグの削除オプションを有効にする] をオンにします。 これにより、`ShowInsertButton`、`ShowEditButton`、および `ShowDeleteButton` プロパティが `true`に設定された CommandField が追加されます。

ブラウザーのページにアクセスし、DetailsView に含まれる [編集]、[削除]、および [新規] ボタンを確認します。 [編集] ボタンをクリックすると、DetailsView が編集モードに変わり、`ReadOnly` プロパティがテキストボックスとして `false` (既定) に設定されている各 BoundField と、チェックボックスとして CheckBoxField が表示されます。

[DetailsView s の既定の編集インターフェイスを ![する](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image11.png)

**図 9**: DetailsView の既定の編集インターフェイス ([クリックしてフルサイズのイメージを表示する](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image12.png))

同様に、現在選択されている製品を削除したり、システムに新しい製品を追加したりすることもできます。 `InsertCommand` ステートメントは、`ProductName`、`UnitPrice`、および `Discontinued` 列でのみ機能するため、他の列には、挿入時にデータベースによって割り当てられた `NULL` または既定値があります。 ObjectDataSource と同様に、`InsertCommand` に `NULL` s が許可されていないデータベーステーブルの列があり、既定値がない場合は、`INSERT` ステートメントを実行しようとすると SQL エラーが発生します。

> [!NOTE]
> DetailsView s の挿入および編集インターフェイスには、カスタマイズや検証の一種がありません。 検証コントロールを追加したり、インターフェイスをカスタマイズしたりするには、BoundFields を TemplateFields に変換する必要があります。 詳細については、「[編集および挿入インターフェイスに検証コントロールを追加](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)する」および「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)」を参照してください。

また、更新と削除では、DetailsView は現在の product s `DataKey` value を使用します。これは、`DataKeyNames` プロパティが構成されている場合にのみ存在します。 編集または削除が無効になっているように見える場合は、`DataKeyNames` プロパティが設定されていることを確認します。

## <a name="limitations-of-automatically-generating-sql-statements"></a>SQL ステートメントの自動生成に関する制限事項

[`INSERT`の生成]、[`UPDATE`]、および [`DELETE` ステートメント] オプションは、テーブルから列を選択する場合にのみ使用できるため、より複雑なクエリの場合は、手順1で作成したのと同様に、独自の `INSERT`、`UPDATE`、および `DELETE` のステートメントを記述する必要があります。 一般的に、SQL `SELECT` ステートメントでは `JOIN` s を使用して1つ以上の参照テーブルのデータを表示します (製品情報を表示するときに、`Categories` table s `CategoryName` フィールドを元に戻すなど)。 同時に、ユーザーがコアテーブル (この場合は`Products`) に対してデータの編集、更新、または挿入を行えるようにすることもできます。

`INSERT`、`UPDATE`、および `DELETE` の各ステートメントは手動で入力できますが、次のような時間節約のヒントを検討してください。 最初に、`Products` テーブルからのみデータを取得するように SqlDataSource を設定します。 [データソースの構成ウィザード] を使用すると、`INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成できるように、テーブルまたはビュー画面から列を指定できます。 次に、ウィザードが完了したら、プロパティウィンドウから SelectQuery を構成します (または、データソースの構成ウィザードに戻りますが、[カスタム SQL ステートメントまたはストアドプロシージャを指定します] オプションを使用します)。 次に、`SELECT` ステートメントを更新して、`JOIN` 構文を含めます。 この手法は、自動的に生成された SQL ステートメントの時間を節約し、よりカスタマイズされた `SELECT` ステートメントを使用できるようにします。

`INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成するもう1つの制限は、`INSERT` ステートメントと `UPDATE` ステートメントの列が、`SELECT` ステートメントによって返される列に基づいていることです。 ただし、多くのフィールドを更新または挿入することが必要になる場合があります。 たとえば、手順 2. の例では、`UnitPrice` BoundField を読み取り専用にする必要があるかもしれません。 その場合は、`UpdateCommand`に表示されません。 または、GridView に表示されないテーブルフィールドの値を設定することもできます。 たとえば、新しいレコードを追加するときに、`QuantityPerUnit` の値を TODO に設定することができます。

このようなカスタマイズが必要な場合は、プロパティウィンドウ、ウィザードの [カスタム SQL ステートメントまたはストアドプロシージャの指定] オプション、または宣言型の構文を使用して、手動で作成する必要があります。

> [!NOTE]
> データ Web コントロールに対応するフィールドがないパラメーターを追加する場合は、これらのパラメーター値に何らかの方法で値を割り当てる必要があることに注意してください。 これらの値は、`InsertCommand` または `UpdateCommand`で直接ハードコーディングすることができます。定義済みのソース (querystring、セッション状態、ページ上の Web コントロールなど) から取得できます。またはは、前のチュートリアルで説明したように、プログラムで割り当てることができます。

## <a name="summary"></a>まとめ

データ Web コントロールで組み込みの挿入、編集、および削除機能を使用するには、バインドされているデータソースコントロールがそのような機能を提供する必要があります。 SqlDataSource の場合、これは `INSERT`、`UPDATE`、および `DELETE` SQL ステートメントを `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティに割り当てる必要があることを意味します。 これらのプロパティおよび対応する parameters コレクションは、データソースの構成ウィザードを使用して手動で追加することも、自動的に生成することもできます。 このチュートリアルでは、両方の手法を検討しています。

オプティミスティック同時実行制御の[実装](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md)に関するチュートリアルでは、ObjectDataSource と共にオプティミスティック同時実行制御を使用しています。 SqlDataSource コントロールは、オプティミスティック同時実行制御も提供します。 手順 2. で説明したように、`INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成する場合、このウィザードにはオプティミスティック同時実行制御オプションが用意されています。 次のチュートリアルで説明するように、SqlDataSource でオプティミスティック同時実行制御を使用すると、`UPDATE` および `DELETE` ステートメント内の `WHERE` 句が変更され、ページに最後にデータが表示されてから他の列の値が変更されないようになります。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](using-parameterized-queries-with-the-sqldatasource-cs.md)
> [次へ](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
