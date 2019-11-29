---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
title: 結合を使用するように TableAdapter を更新する (VB) |Microsoft Docs
author: rick-anderson
description: データベースを使用する場合は、複数のテーブルに分散されているデータを要求するのが一般的です。 2つの異なるテーブルからデータを取得するには、次のいずれかの方法を使用します。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: e624a3e0-061b-4efc-8b0e-5877f9ff6714
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c94baa99b126cdd24d69afc3d02bfe8b069419b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74604223"
---
# <a name="updating-the-tableadapter-to-use-joins-vb"></a>JOIN を使用するように TableAdapter を更新する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_VB.zip)または[PDF のダウンロード](updating-the-tableadapter-to-use-joins-vb/_static/datatutorial69vb1.pdf)

> データベースを使用する場合は、複数のテーブルに分散されているデータを要求するのが一般的です。 2つの異なるテーブルからデータを取得するには、相関サブクエリまたは結合操作のいずれかを使用できます。 このチュートリアルでは、メインクエリに結合を含む TableAdapter を作成する方法を確認する前に、相関サブクエリと結合構文を比較します。

## <a name="introduction"></a>はじめに

リレーショナルデータベースでは、多くの場合、使用するデータは複数のテーブルに分散されます。 たとえば、製品情報を表示する場合、各製品に対応するカテゴリと仕入先の名前を一覧表示することが考えられます。 `Products` テーブルには値 `CategoryID` と `SupplierID` がありますが、実際のカテゴリと仕入先の名前はそれぞれ `Categories` テーブルと `Suppliers` テーブルにあります。

関連する別のテーブルから情報を取得するには、*相関サブクエリ*また*は `JOIN`を*使用できます。 相関サブクエリは、入れ子になった `SELECT` クエリで、外側のクエリの列を参照します。 たとえば、[データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)に関するチュートリアルでは、`ProductsTableAdapter` s メインクエリで2つの相関サブクエリを使用して、各製品のカテゴリ名と仕入先名を返しました。 `JOIN` は、2つの異なるテーブルの関連する行をマージする SQL コンストラクトです。 ここでは、 [SqlDataSource コントロール](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb.md)チュートリアルを使用してデータにクエリを実行し、各製品と共にカテゴリ情報を表示する方法について `JOIN` 説明します。

Tableadapter で `JOIN` s を使用しない理由は、TableAdapter s ウィザードの制限により、対応する `INSERT`、`UPDATE`、および `DELETE` ステートメントが自動生成されるためです。 具体的には、TableAdapter のメインクエリに `JOIN` が含まれている場合、TableAdapter では、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティに対してアドホック SQL ステートメントまたはストアドプロシージャを自動作成することはできません。

このチュートリアルでは、メインクエリに `JOIN` を含む TableAdapter を作成する方法を確認する前に、相関サブクエリと `JOIN` s を簡単に比較対照します。

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>相関サブクエリと`JOIN` の比較と比較

`Northwind` データセットの最初のチュートリアルで作成した `ProductsTableAdapter` は、相関サブクエリを使用して、各製品に対応するカテゴリおよび仕入先名を返します。 `ProductsTableAdapter` s メインクエリを以下に示します。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample1.sql)]

2つの相関サブクエリ (`(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` と `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)`) は、製品ごとに1つの値を外部 `SELECT` ステートメントの列リストに追加の列として返す `SELECT` クエリです。

または、`JOIN` を使用して、各製品の仕入先とカテゴリ名を返すこともできます。 次のクエリでは、上の例と同じ出力が返されますが、サブクエリの代わりに `JOIN` s が使用されます。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample2.sql)]

`JOIN` は、特定の条件に基づいて、あるテーブルのレコードを別のテーブルのレコードとマージします。 上記のクエリでは、たとえば、`LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` は、各製品レコードを、`CategoryID` 値が製品 s `CategoryID` 値と一致するカテゴリレコードとマージするように SQL Server に指示します。 マージされた結果を使用すると、各製品の対応するカテゴリフィールド (`CategoryName`など) を操作できます。

> [!NOTE]
> `JOIN` は、リレーショナルデータベースからデータを照会するときによく使用されます。 `JOIN` 構文を初めて使用する場合、または使用方法について少しの話をする必要がある場合は、「 [W3](http://www.w3schools.com/)」で[SQL Join のチュートリアル](http://www.w3schools.com/sql/sql_join.asp)をお勧めします。 また、 [SQL オンラインブック](https://msdn.microsoft.com/library/ms130214.aspx)の「 [`JOIN` の基礎](https://msdn.microsoft.com/library/ms191517.aspx)」および「[サブクエリの基礎](https://msdn.microsoft.com/library/ms189575.aspx)」を参照してください。

`JOIN` s と相関サブクエリは両方とも、他のテーブルから関連データを取得するために使用できます。そのため、多くの開発者は、頭の初歩を残し、使用する方法を知ります。 これまでに説明したすべての SQL 中心は、ほぼ同じようにパフォーマンスを向上させることができます。これは、ほぼ同一の実行プランを生成 SQL Server という点ではありません。 そのようなアドバイスは、お客様とチームが最も使いやすい手法を使用することです。 この助言を分離した後、これらの専門家は、相関サブクエリで `JOIN` s の設定をすぐに表していることに注意してください。

型指定されたデータセットを使用してデータアクセス層を構築する場合、サブクエリを使用すると、ツールの動作が向上します。 特に、TableAdapter s ウィザードでは、メインクエリに `JOIN` が含まれている場合に、対応する `INSERT`、`UPDATE`、および `DELETE` ステートメントが自動生成されませんが、相関サブクエリを使用すると、これらのステートメントが自動生成されます。

この欠点を調べるには、`~/App_Code/DAL` フォルダーに一時的に型指定されたデータセットを作成します。 TableAdapter 構成ウィザードで、アドホック SQL ステートメントを使用することを選択し、次の `SELECT` クエリを入力します (図1を参照)。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample3.sql)]

[結合を含むメインクエリを入力 ![には](updating-the-tableadapter-to-use-joins-vb/_static/image2.png)](updating-the-tableadapter-to-use-joins-vb/_static/image1.png)

**図 1**: `JOIN` s を含むメインクエリを入力[する (クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image3.png)されます)

既定では、TableAdapter は、メインクエリに基づいて、`INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に作成します。 [詳細設定] ボタンをクリックすると、この機能が有効になっていることがわかります。 この設定にかかわらず、`INSERT`、`UPDATE`、および `DELETE` の各ステートメントは、メインクエリに `JOIN`が含まれているため、TableAdapter で作成することはできません。

![結合を含むメインクエリを入力します](updating-the-tableadapter-to-use-joins-vb/_static/image4.png)

**図 2**: `JOIN` s を含むメインクエリを入力する

[完了] をクリックしてウィザードを終了します。 この時点で、データセットのデザイナーには、`SELECT` クエリ s 列リストに返される各フィールドの列を含む DataTable を含む単一の TableAdapter が含まれます。 これには、図3に示すように、`CategoryName` と `SupplierName`が含まれます。

![DataTable には、列リストで返される各フィールドの列が含まれます。](updating-the-tableadapter-to-use-joins-vb/_static/image5.png)

**図 3**: DataTable には、列リストで返された各フィールドの列が含まれている

DataTable には適切な列が含まれていますが、TableAdapter には `InsertCommand`、`UpdateCommand`、および `DeleteCommand` プロパティの値がありません。 これを確認するには、デザイナーで TableAdapter をクリックし、プロパティウィンドウにアクセスします。 `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティが [(なし)] に設定されていることがわかります。

[InsertCommand、UpdateCommand、および DeleteCommand プロパティが (None) に設定されて ![](updating-the-tableadapter-to-use-joins-vb/_static/image7.png)](updating-the-tableadapter-to-use-joins-vb/_static/image6.png)

**図 4**: `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティが (なし) に設定されている ([クリックしてフルサイズの画像を表示する](updating-the-tableadapter-to-use-joins-vb/_static/image8.png))

この欠点を回避するには、プロパティウィンドウを使用して、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティの SQL ステートメントとパラメーターを手動で指定します。 または、`JOIN` s を含ま*ない*ように TableAdapter のメインクエリを構成して開始することもできます。 これにより、`INSERT`、`UPDATE`、および `DELETE` ステートメントが自動的に生成されるようになります。 ウィザードが完了したら、プロパティウィンドウから TableAdapter の `SelectCommand` を手動で更新して、`JOIN` 構文を含めることができます。

この方法は機能しますが、アドホック SQL クエリを使用する場合は非常に脆弱です。これは、ウィザードを使用して TableAdapter のメインクエリを再構成するたびに、自動生成された `INSERT`、`UPDATE`、および `DELETE` ステートメントが再作成されるためです。 これは、TableAdapter を右クリックし、コンテキストメニューから [構成] を選択して、ウィザードを再度完了すると、後で行ったすべてのカスタマイズが失われることを意味します。

TableAdapter の自動生成された `INSERT`、`UPDATE`、および `DELETE` ステートメントの高まるは、さいわい、アドホック SQL ステートメントに限定されています。 TableAdapter でストアドプロシージャが使用されている場合は、ストアドプロシージャが変更される心配をせずに、`SelectCommand`、`InsertCommand`、`UpdateCommand`、または `DeleteCommand` ストアドプロシージャをカスタマイズし、TableAdapter 構成ウィザードを再実行することができます。

次のいくつかの手順では、最初に、対応する挿入、更新、および削除の各ストアドプロシージャが自動生成されるように `JOIN` を省略するメインクエリを使用する TableAdapter を作成します。 次に、関連テーブルから追加の列を返す `JOIN` が使用されるように、`SelectCommand` を更新します。 最後に、対応するビジネスロジックレイヤークラスを作成し、ASP.NET web ページで TableAdapter を使用する方法を示します。

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>手順 1: 簡略化されたメインクエリを使用して TableAdapter を作成する

このチュートリアルでは、`NorthwindWithSprocs` データセットの `Employees` テーブルに TableAdapter と厳密に型指定された DataTable を追加します。 `Employees` テーブルには、従業員のマネージャーの `EmployeeID` を指定した `ReportsTo` フィールドが含まれています。 たとえば、employee Anne 川本の `ReportTo` 値は5です。これは、秋山加藤の `EmployeeID` です。 その結果、Anne は秋山さん、上司に報告します。 各従業員の `ReportsTo` 値を報告することに加えて、上司の名前を取得することもできます。 これは、`JOIN`を使用して実現できます。 ただし、最初に TableAdapter を作成するときに `JOIN` を使用すると、ウィザードによって、対応する挿入、更新、および削除の各機能が自動的に生成されなくなります。 そのため、最初に、メインクエリに `JOIN` が含まれていない TableAdapter を作成します。 次に、手順2で、`JOIN`を使用してマネージャーの名前を取得するようにメインクエリのストアドプロシージャを更新します。

まず、`~/App_Code/DAL` フォルダー内の `NorthwindWithSprocs` データセットを開きます。 デザイナーを右クリックし、コンテキストメニューの [追加] オプションを選択して、[TableAdapter] メニュー項目を選択します。 これにより、TableAdapter 構成ウィザードが起動します。 図5に示すように、ウィザードで新しいストアドプロシージャを作成し、[次へ] をクリックします。 TableAdapter ウィザードでの新しいストアドプロシージャの作成の詳細については、「[型指定されたデータセットの tableadapter の新しいストアドプロシージャの作成](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)」チュートリアルを参照してください。

[![[新しいストアドプロシージャの作成] オプションを選択します。](updating-the-tableadapter-to-use-joins-vb/_static/image10.png)](updating-the-tableadapter-to-use-joins-vb/_static/image9.png)

**図 5**: [新しいストアドプロシージャを作成する] オプションを選択[する (クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image11.png)されます)

TableAdapter のメインクエリには、次の `SELECT` ステートメントを使用します。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample4.sql)]

このクエリには `JOIN` が含まれていないため、TableAdapter ウィザードでは、対応する `INSERT`、`UPDATE`、および `DELETE` ステートメントを含むストアドプロシージャと、メインクエリを実行するためのストアドプロシージャが自動的に作成されます。

次の手順では、TableAdapter のストアドプロシージャに名前を指定できます。 図6に示すように、`Employees_Select`、`Employees_Insert`、`Employees_Update`、および `Employees_Delete`の名前を使用します。

[TableAdapter s ストアドプロシージャの名前を ![](updating-the-tableadapter-to-use-joins-vb/_static/image13.png)](updating-the-tableadapter-to-use-joins-vb/_static/image12.png)

**図 6**: TableAdapter のストアドプロシージャに名前[を指定する (クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image14.png)されます)

最後の手順では、TableAdapter のメソッドに名前を指定するように求められます。 `Fill` を使用し、メソッド名として `GetEmployees` します。 また、[更新を直接データベースに送信するためのメソッドを作成する (GenerateDBDirectMethods)] チェックボックスはオンのままにしてください。

[TableAdapter のメソッドに ![名前を入力し、GetEmployees します。](updating-the-tableadapter-to-use-joins-vb/_static/image16.png)](updating-the-tableadapter-to-use-joins-vb/_static/image15.png)

**図 7**: TableAdapter のメソッド `Fill` と `GetEmployees` の名前を指定[する (クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image17.png)されます)

ウィザードが完了したら、しばらく時間を取って、データベース内のストアドプロシージャを確認してください。 `Employees_Select`、`Employees_Insert`、`Employees_Update`、および `Employees_Delete`の4つの新しいものが表示されます。 次に、`EmployeesDataTable` を調べて、先ほど作成した `EmployeesTableAdapter` ます。 DataTable には、メインクエリによって返される各フィールドの列が含まれています。 TableAdapter をクリックし、プロパティウィンドウにアクセスします。 ここでは、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティが、対応するストアドプロシージャを呼び出すように正しく構成されていることがわかります。

[TableAdapter には、挿入、更新、削除の各機能が含まれて ![](updating-the-tableadapter-to-use-joins-vb/_static/image19.png)](updating-the-tableadapter-to-use-joins-vb/_static/image18.png)

**図 8**: TableAdapter には挿入、更新、および削除の機能が含まれています ([クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image20.png)されます)

挿入、更新、および削除の各ストアドプロシージャが自動的に作成され、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティが正しく構成されているので、`SelectCommand` s ストアドプロシージャをカスタマイズして各従業員のマネージャーに関する追加情報を返すことができます。 具体的には、`JOIN` を使用し、マネージャーの `FirstName` と `LastName` の値を返すように `Employees_Select` ストアドプロシージャを更新する必要があります。 ストアドプロシージャを更新した後は、これらの追加列が含まれるように DataTable を更新する必要があります。 これらの2つのタスクについては、手順 2. と 3. で説明します。

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>手順 2:`JOIN` を含むようにストアドプロシージャをカスタマイズする

まず、サーバーエクスプローラーに移動し、Northwind データベースの [ストアドプロシージャ] フォルダーにドリルダウンして、`Employees_Select` ストアドプロシージャを開きます。 このストアドプロシージャが表示されない場合は、[ストアドプロシージャ] フォルダーを右クリックし、[最新の状態に更新] をクリックします。 `LEFT JOIN` を使用して manager の姓と名を返すようにストアドプロシージャを更新します。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample5.sql)]

`SELECT` ステートメントを更新した後、[ファイル] メニューの [`Employees_Select`の保存] をクリックして変更を保存します。 または、ツールバーの [保存] アイコンをクリックするか、Ctrl + S キーを押します。 変更を保存した後、サーバーエクスプローラーで `Employees_Select` ストアドプロシージャを右クリックし、[実行] を選択します。 これにより、ストアドプロシージャが実行され、結果が出力ウィンドウに表示されます (図9を参照)。

[ストアドプロシージャの結果が ![出力ウィンドウに表示されます。](updating-the-tableadapter-to-use-joins-vb/_static/image22.png)](updating-the-tableadapter-to-use-joins-vb/_static/image21.png)

**図 9**: ストアドプロシージャの結果が出力ウィンドウに表示される ([クリックしてフルサイズの画像を表示する](updating-the-tableadapter-to-use-joins-vb/_static/image23.png))

## <a name="step-3-updating-the-datatable-s-columns"></a>手順 3: DataTable s 列を更新する

この時点で、`Employees_Select` ストアドプロシージャは `ManagerFirstName` と `ManagerLastName` の値を返しますが、`EmployeesDataTable` にはこれらの列がありません。 これらの欠損列は、次の2つの方法のいずれかで DataTable に追加できます。

- データセットデザイナーで DataTable**を右クリック**し、[追加] メニューの [列] をクリックします。 その後、列に名前を指定し、それに応じてプロパティを設定できます。
- **自動**-TableAdapter 構成ウィザードは、`SelectCommand` ストアドプロシージャによって返されるフィールドを反映するように、DataTable の列を更新します。 アドホック SQL ステートメントを使用すると、`SelectCommand` に `JOIN`が含まれるようになったため、`InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各プロパティも削除されます。 ただし、ストアドプロシージャを使用する場合、これらのコマンドプロパティはそのまま残ります。

前のチュートリアルでは、前のチュートリアルで DataTable 列を手動で追加する方法について説明しました。[詳細については、マスターレコードの箇条書きリスト](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)と[ファイルのアップロード](../working-with-binary-files/uploading-files-vb.md)に関する記事をご覧ください。このプロセスについては、次のチュートリアルでさらに詳しく説明します。 ただし、このチュートリアルでは、が TableAdapter 構成ウィザードを使用して自動アプローチを使用します。

まず、`EmployeesTableAdapter` を右クリックし、コンテキストメニューから [構成] を選択します。 これにより、TableAdapter 構成ウィザードが表示されます。これには、選択、挿入、更新、および削除に使用するストアドプロシージャが、戻り値とパラメーター (存在する場合) と共に一覧表示されます。 図10に、このウィザードを示します。 ここで、`Employees_Select` ストアドプロシージャが `ManagerFirstName` と `ManagerLastName` フィールドを返すようになったことがわかります。

[![、Employees_Select ストアドプロシージャの更新された列の一覧が表示されます。](updating-the-tableadapter-to-use-joins-vb/_static/image25.png)](updating-the-tableadapter-to-use-joins-vb/_static/image24.png)

**図 10**: ウィザードに `Employees_Select` ストアドプロシージャの更新された列の一覧が表示される ([クリックしてフルサイズの画像を表示する](updating-the-tableadapter-to-use-joins-vb/_static/image26.png))

[完了] をクリックしてウィザードを完了します。 データセットデザイナーに戻ると、`EmployeesDataTable` に `ManagerFirstName` と `ManagerLastName`の2つの列が追加されます。

[EmployeesDataTable に2つの新しい列が含まれている ![](updating-the-tableadapter-to-use-joins-vb/_static/image28.png)](updating-the-tableadapter-to-use-joins-vb/_static/image27.png)

**図 11**: `EmployeesDataTable` に2つの新しい列が含まれている ([クリックしてフルサイズの画像を表示する](updating-the-tableadapter-to-use-joins-vb/_static/image29.png))

更新された `Employees_Select` ストアドプロシージャが有効であり、TableAdapter の挿入、更新、および削除の機能がまだ機能していることを示すために、ユーザーが従業員を表示および削除できるようにする web ページを作成してみましょう。 ただし、このようなページを作成する前に、最初にビジネスロジック層に新しいクラスを作成して、`NorthwindWithSprocs` データセットから従業員を操作できるようにする必要があります。 手順4では、`EmployeesBLLWithSprocs` クラスを作成します。 手順5では、ASP.NET ページからこのクラスを使用します。

## <a name="step-4-implementing-the-business-logic-layer"></a>手順 4: ビジネスロジック層を実装する

`EmployeesBLLWithSprocs.vb`という名前の `~/App_Code/BLL` フォルダーに新しいクラスファイルを作成します。 このクラスは、既存の `EmployeesBLL` クラスのセマンティクスを模倣しています。この新しいクラスでは、より少数のメソッドを提供し、`Northwind` データセットではなく `NorthwindWithSprocs` データセットを使用します。 `EmployeesBLLWithSprocs` クラスに次のコードを追加します。

[!code-vb[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample6.vb)]

`EmployeesBLLWithSprocs` class s `Adapter` プロパティは、`NorthwindWithSprocs` データセットの `EmployeesTableAdapter`のインスタンスを返します。 これは、クラス `GetEmployees` および `DeleteEmployee` メソッドによって使用されます。 `GetEmployees` メソッドは、対応する `GetEmployees` メソッドを `EmployeesTableAdapter` 呼び出します。このメソッドは、`Employees_Select` ストアドプロシージャを呼び出し、結果を `EmployeeDataTable`に設定します。 `DeleteEmployee` メソッドは同様に、`EmployeesTableAdapter` s `Delete` メソッドを呼び出します。これにより、`Employees_Delete` ストアドプロシージャが呼び出されます。

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>手順 5: プレゼンテーション層のデータを操作する

`EmployeesBLLWithSprocs` クラスが完成したら、ASP.NET ページを使用して従業員データを操作する準備ができました。 `AdvancedDAL` フォルダーの [`JOINs.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグし、`ID` プロパティを [`Employees`] に設定します。 次に、GridView s スマートタグから、グリッドを `EmployeesDataSource`という名前の新しい ObjectDataSource コントロールにバインドします。

`EmployeesBLLWithSprocs` クラスを使用するように ObjectDataSource を構成します。 [選択] タブと [削除] タブで、ドロップダウンリストから [`GetEmployees`] および [`DeleteEmployee`] メソッドが選択されていることを確認します。 [完了] をクリックして、ObjectDataSource の構成を完了します。

[EmployeesBLLWithSprocs クラスを使用するように ObjectDataSource を構成 ![には](updating-the-tableadapter-to-use-joins-vb/_static/image31.png)](updating-the-tableadapter-to-use-joins-vb/_static/image30.png)

**図 12**: `EmployeesBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](updating-the-tableadapter-to-use-joins-vb/_static/image32.png))

[GetEmployees メソッドと DeleteEmployee メソッドが ObjectDataSource で使用さ ![](updating-the-tableadapter-to-use-joins-vb/_static/image34.png)](updating-the-tableadapter-to-use-joins-vb/_static/image33.png)

**図 13**: ObjectDataSource で `GetEmployees` および `DeleteEmployee` メソッドを使用する ([クリックしてフルサイズのイメージを表示する](updating-the-tableadapter-to-use-joins-vb/_static/image35.png))

Visual Studio によって、`EmployeesDataTable` s 列ごとに BoundField が GridView に追加されます。 `Title`、`LastName`、`FirstName`、`ManagerFirstName`、および `ManagerLastName` を除くこれらの連結フィールドをすべて削除し、最後の4つの BoundFields の `HeaderText` プロパティを姓、名、マネージャー名、およびマネージャーの姓にそれぞれ変更します。

ユーザーがこのページから従業員を削除できるようにするには、次の2つの作業を行う必要があります。 まず、削除機能を提供するように GridView に指示します。そのためには、スマートタグから [削除を有効にする] オプションをオンにします。 次に、objectdatasource の `OldValuesParameterFormatString` プロパティを、ObjectDataSource ウィザードで設定された値 (`original_{0}`) から既定値 (`{0}`) に変更します。 これらの変更を行った後、GridView および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample7.aspx)]

ブラウザーでページにアクセスして、ページをテストします。 図14に示すように、ページには、各従業員と上司の名前が表示されます (所有している場合)。

[Employees_Select ストアドプロシージャ内の結合によってマネージャー名が返される ![](updating-the-tableadapter-to-use-joins-vb/_static/image37.png)](updating-the-tableadapter-to-use-joins-vb/_static/image36.png)

**図 14**: `Employees_Select` ストアドプロシージャの `JOIN` がマネージャーの名前を返す ([クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image38.png)されます)

[削除] ボタンをクリックすると、削除中のワークフローが開始されます。このワークフローは `Employees_Delete` ストアドプロシージャの実行に culminates ます。 ただし、ストアドプロシージャで試行された `DELETE` ステートメントは、外部キー制約違反によって失敗します (図15を参照)。 具体的には、各従業員は `Orders` テーブルに1つ以上のレコードを持っているため、削除は失敗します。

[対応する注文がある従業員を削除すると、外部キー制約違反が発生する ![](updating-the-tableadapter-to-use-joins-vb/_static/image40.png)](updating-the-tableadapter-to-use-joins-vb/_static/image39.png)

**図 15**: 対応する注文がある従業員を削除すると、外部キー制約違反が発生する ([クリックすると、フルサイズの画像が表示](updating-the-tableadapter-to-use-joins-vb/_static/image41.png)されます)

従業員を削除できるようにするには、次の方法があります。

- Foreign key 制約を連鎖削除に更新します。
- 削除する従業員の `Orders` テーブルからレコードを手動で削除します。または、
- `Employees` レコードを削除する前に、最初に `Orders` テーブルから関連レコードを削除するように `Employees_Delete` ストアドプロシージャを更新します。 この手法については、 [「型指定されたデータセットの tableadapter の既存のストアドプロシージャの使用](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)」のチュートリアルで説明しました。

この作業をリーダーの演習として残しておきます。

## <a name="summary"></a>要約

リレーショナルデータベースを使用する場合、クエリでは、複数の関連テーブルからデータを取得するのが一般的です。 相関サブクエリと `JOIN` には、クエリ内の関連テーブルからデータにアクセスするための2つの異なる手法が用意されています。 前のチュートリアルでは、通常、相関サブクエリを使用しました。これは、TableAdapter が `JOIN` に関連するクエリの `INSERT`、`UPDATE`、および `DELETE` ステートメントを自動生成できないためです。 これらの値は手動で指定できますが、アドホック SQL ステートメントを使用する場合は、TableAdapter 構成ウィザードの完了時にすべてのカスタマイズが上書きされます。

さいわい、ストアドプロシージャを使用して作成された Tableadapter は、アドホック SQL ステートメントを使用して作成されたものと同じ高まるを持つことはできません。 そのため、ストアドプロシージャを使用する場合は、メインクエリで `JOIN` を使用する TableAdapter を作成することができます。 このチュートリアルでは、このような TableAdapter を作成する方法を説明しました。 ここでは、対応する insert、update、および delete の各ストアドプロシージャが自動作成されるように、TableAdapter のメインクエリに対して `JOIN`のない `SELECT` クエリを使用して開始しました。 TableAdapter の初期構成が完了したので、`SelectCommand` ストアドプロシージャを拡張して、`JOIN` を使用し、TableAdapter 構成ウィザードを再実行して `EmployeesDataTable` s 列を更新しました。

TableAdapter 構成ウィザードを再実行すると、`Employees_Select` ストアドプロシージャによって返されたデータフィールドを反映するように、`EmployeesDataTable` の列が自動的に更新されます。 または、これらの列を DataTable に手動で追加することもできます。 次のチュートリアルでは、DataTable に列を手動で追加する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Geisenow、David u、および Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [次へ](adding-additional-datatable-columns-vb.md)
