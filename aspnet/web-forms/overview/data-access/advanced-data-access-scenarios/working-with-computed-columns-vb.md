---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
title: 計算列を使用する (VB) |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server では、データベーステーブルを作成するときに、通常は、式から計算される値を持つ計算列を定義できます。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 5811b8ff-ed56-40fc-9397-6b69ae09a8f6
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: e425d7363c2cdea6efb0ba51f3fc2b6a5330bf2a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74603118"
---
# <a name="working-with-computed-columns-vb"></a>計算列を使用する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_VB.zip)または[PDF のダウンロード](working-with-computed-columns-vb/_static/datatutorial71vb1.pdf)

> Microsoft SQL Server では、データベーステーブルを作成するときに、同じデータベースレコード内の他の値を参照する式から値を計算する計算列を定義できます。 このような値はデータベースで読み取り専用であるため、Tableadapter を操作するときに特別な考慮が必要です。 このチュートリアルでは、計算列によって生じる課題を満たす方法について説明します。

## <a name="introduction"></a>はじめに

Microsoft SQL Server では、 *[計算列](https://msdn.microsoft.com/library/ms191250.aspx)* を使用できます。これは、通常、同じテーブル内の他の列から値を参照する式から値が計算される列です。 たとえば、時間追跡データモデルには、`ServicePerformed`、`EmployeeID`、`Rate`、`Duration`などの列を含む `ServiceLog` という名前のテーブルがある場合があります。 サービス項目あたりの使用量 (期間を乗算した値) は、web ページまたは他のプログラムインターフェイスを使用して計算できますが、この情報を報告した `AmountDue` という名前の `ServiceLog` テーブルに列を含めると便利な場合があります。 この列は通常の列として作成できますが、`Rate` または `Duration` の列の値が変更された場合はいつでも更新する必要があります。 より適切な方法は、`Rate * Duration`式を使用して、`AmountDue` 列を計算列にすることです。 この操作を行うと、クエリで参照されたときに `AmountDue` 列の値が SQL Server によって自動的に計算されます。

計算列の値は式によって決定されるため、このような列は読み取り専用であるため、`INSERT` または `UPDATE` のステートメントで値を代入することはできません。 ただし、アドホック SQL ステートメントを使用する TableAdapter のメインクエリに計算列が含まれている場合は、自動生成された `INSERT` および `UPDATE` ステートメントに自動的に含まれます。 その結果、TableAdapter の `INSERT` と `UPDATE` クエリと `InsertCommand` および `UpdateCommand` プロパティを更新して、計算列への参照を削除する必要があります。

アドホック SQL ステートメントを使用する TableAdapter で計算列を使用する場合の1つの問題は、tableadapter 構成ウィザードが完了するたびに、TableAdapter s `INSERT` および `UPDATE` クエリが自動的に再生成されることです。 このため、計算列は `INSERT` から手動で削除され、ウィザードを再実行すると `UPDATE` クエリは再表示されます。 ストアドプロシージャを使用する Tableadapter はこの高まるの影響を受けませんが、手順3で対処する独自の特性があります。

このチュートリアルでは、Northwind データベースの `Suppliers` テーブルに計算列を追加し、対応する TableAdapter を作成して、このテーブルとその計算列を操作します。 Tableadapter 構成ウィザードの使用時にカスタマイズが失われないよう、アドホック SQL ステートメントではなくストアドプロシージャを使用します。

始めましょう!

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>手順 1:`Suppliers`テーブルに計算列を追加する

Northwind データベースには計算列がないため、自分で追加する必要があります。 このチュートリアルでは、`ContactName` (`ContactTitle`、`CompanyName`) の形式で、連絡先の名前、役職、および会社の勤務先を返す `FullContactName` という `Suppliers` テーブルに計算列を追加します。 この計算列は、仕入先に関する情報を表示するときにレポートで使用される場合があります。

まず、サーバーエクスプローラーの `Suppliers` テーブルを右クリックし、コンテキストメニューから [テーブル定義を開く] を選択して `Suppliers` テーブル定義を開きます。 これにより、テーブルの列とそのプロパティ (データ型、`NULL` が許可されているかどうかなど) が表示されます。 計算列を追加するには、まず、列の名前をテーブル定義に入力します。 次に、列プロパティウィンドウの [計算列の指定] セクションの [(式)] ボックスに式を入力します (図1を参照)。 計算列に `FullContactName` という名前を指定し、次の式を使用します。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample1.sql)]

`+` 演算子を使用して、SQL で文字列を連結できることに注意してください。 `CASE` ステートメントは、従来のプログラミング言語の条件のように使用できます。 上の式では、`CASE` ステートメントをとして読み取ることができます。 `ContactTitle` が `NULL` ない場合は、`ContactTitle` 値をコンマで連結して出力します。それ以外の場合は、何も出力しません。 `CASE` ステートメントの有用性の詳細については、「 [SQL `CASE` ステートメントの機能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)」を参照してください。

> [!NOTE]
> ここでは、`CASE` ステートメントを使用する代わりに、代わりに `ISNULL(ContactTitle, '')`を使用することもできます。 NULL 以外の場合、 [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx)は*checkexpression*を返します。それ以外の場合は、 *replacementValue*を返します。 このインスタンスでは `ISNULL` または `CASE` のいずれかを使用できますが、`CASE` ステートメントの柔軟性が `ISNULL`で一致しない複雑なシナリオがあります。

この計算列を追加すると、画面は図1のスクリーンショットのようになります。

[FullContactName という名前の計算列を [仕入先テーブルに追加するには](working-with-computed-columns-vb/_static/image2.png)](working-with-computed-columns-vb/_static/image1.png)

**図 1**: `FullContactName` という名前の計算列を `Suppliers` テーブルに追加[する (クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image3.png)されます)

計算列に名前を付け、その式を入力したら、ツールバーの [保存] アイコンをクリックするか、Ctrl キーを押しながら S キーを押すか、または [ファイル] メニューに移動して [`Suppliers`の保存] をクリックして、テーブルへの変更を保存します。

テーブルを保存すると、[`Suppliers` table s 列] ボックスの一覧にある [追加] 列を含むサーバーエクスプローラーが更新されます。 さらに、(数式) テキストボックスに入力した式は、不要な空白を除去する同等の式に自動的に調整されます。これにより、列名が角かっこ (`[]`) で囲まれ、より明示的に操作の順序が示されます。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample2.sql)]

Microsoft SQL Server の計算列の詳細については、[技術ドキュメント](https://msdn.microsoft.com/library/ms191250.aspx)を参照してください。 また、計算列を作成する手順については、 [「方法: 計算列を指定する](https://msdn.microsoft.com/library/ms188300.aspx)」をご覧ください。

> [!NOTE]
> 既定では、計算列は物理的にテーブルに格納されるのではなく、クエリで参照されるたびに再計算されます。 ただし、[保存されている] チェックボックスをオンにすると、計算列をテーブルに物理的に格納するように SQL Server に指示できます。 これにより、計算列にインデックスを作成できます。これにより、`WHERE` 句で計算列の値を使用するクエリのパフォーマンスが向上します。 詳細については、「[計算列にインデックスを作成する](https://msdn.microsoft.com/library/ms189292.aspx)」を参照してください。

## <a name="step-2-viewing-the-computed-column-s-values"></a>手順 2: 計算列の値の表示

データアクセス層での作業を開始する前に、`FullContactName` の値を表示するのに1分かかります。 サーバーエクスプローラーから、`Suppliers` テーブル名を右クリックし、コンテキストメニューから [新しいクエリ] を選択します。 クエリに含めるテーブルを選択するように求めるクエリウィンドウが表示されます。 `Suppliers` テーブルを追加し、[閉じる] をクリックします。 次に、[仕入先] テーブルの `CompanyName`、`ContactName`、`ContactTitle`、および `FullContactName` の各列を確認します。 最後に、ツールバーの赤い感嘆符アイコンをクリックしてクエリを実行し、結果を表示します。

図2に示すように、結果には `FullContactName`が含まれており、`ContactName` (`ContactTitle`、`CompanyName`) の形式を使用して、`CompanyName`、`ContactName`、および `ContactTitle` 列が一覧表示されます。

[![FullContactName は、[宛先] 形式 ([部署]、[CompanyName]) を使用します。](working-with-computed-columns-vb/_static/image5.png)](working-with-computed-columns-vb/_static/image4.png)

**図 2**: `FullContactName` は `ContactName` (`ContactTitle`、`CompanyName`) の形式を使用します ([クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image6.png)されます)。

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>手順 3: データアクセス層への`SuppliersTableAdapter`の追加

アプリケーションでサプライヤー情報を操作するには、まず、DAL に TableAdapter と DataTable を作成する必要があります。 これは、前のチュートリアルで確認したのと同じ簡単な手順を使用して実現するのが理想的です。 ただし、計算列を使用すると、議論に役立ついくつかのしわが生じます。

アドホック SQL ステートメントを使用する TableAdapter を使用している場合は、tableadapter 構成ウィザードを使用して、単に tableadapter s メインクエリに計算列を含めることができます。 ただし、この場合は、計算列を含む `INSERT` および `UPDATE` ステートメントが自動生成されます。 これらのメソッドのいずれかを実行しようとすると `SqlException`、列*ColumnName*を変更できません。これは、計算列であるか、UNION 演算子の結果がスローされるためです。 `INSERT` および `UPDATE` ステートメントは、TableAdapter の `InsertCommand` および `UpdateCommand` プロパティを使用して手動で調整できますが、TableAdapter 構成ウィザードを再実行するたびに、これらのカスタマイズは失われます。

アドホック SQL ステートメントを使用する Tableadapter の高まるにより、計算列を操作するときはストアドプロシージャを使用することをお勧めします。 既存のストアドプロシージャを使用する場合は、「[型指定されたデータセットの tableadapter の既存のストアドプロシージャの使用](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)」のチュートリアルで説明されているように、単に tableadapter を構成します。 ただし、TableAdapter ウィザードを使用してストアドプロシージャを作成する場合は、最初にメインクエリから計算列を省略することが重要です。 メインクエリに計算列を含めると、完了時に、対応するストアドプロシージャを作成できないことが TableAdapter 構成ウィザードによって通知されます。 つまり、最初に計算列のないメインクエリを使用して TableAdapter を構成してから、対応するストアドプロシージャと TableAdapter s `SelectCommand` を手動で更新して計算列を含める必要があります。 この方法は`JOIN`*s*チュートリアルを[使用するように TableAdapter を更新](updating-the-tableadapter-to-use-joins-vb.md)する方法と似ています。

このチュートリアルでは、新しい TableAdapter を追加し、自動的にストアドプロシージャを作成するようにします。 そのため、最初にメインクエリから計算列 `FullContactName` を省略する必要があります。

まず、`~/App_Code/DAL` フォルダー内の `NorthwindWithSprocs` データセットを開きます。 デザイナー内を右クリックし、コンテキストメニューから [新しい TableAdapter の追加] を選択します。 これにより、TableAdapter 構成ウィザードが起動します。 データを照会するデータベース (`Web.config`から`NORTHWNDConnectionString`) を指定し、[次へ] をクリックします。 `Suppliers` テーブルに対してクエリまたは変更を行うストアドプロシージャをまだ作成していないので、[新しいストアドプロシージャの作成] オプションを選択して、ウィザードによってテーブルが作成されるようにして、[次へ] をクリックします。

[![[新しいストアドプロシージャの作成] オプションを選択する](working-with-computed-columns-vb/_static/image8.png)](working-with-computed-columns-vb/_static/image7.png)

**図 3**: [新しいストアドプロシージャを作成する] オプションを選択[する (クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image9.png)されます)

次の手順では、メインクエリを入力するように求められます。 次のクエリを入力します。これにより、各仕入先の `SupplierID`、`CompanyName`、`ContactName`、および `ContactTitle` 列が返されます。 このクエリでは、計算列 (`FullContactName`) が意図的に省略されていることに注意してください。ここでは、対応するストアドプロシージャを更新して、手順 4. でこの列を含めます。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample3.sql)]

メインクエリを入力して [次へ] をクリックすると、ウィザードによって生成される4つのストアドプロシージャに名前を指定できるようになります。 図4に示すように、これらのストアドプロシージャ `Suppliers_Select`、`Suppliers_Insert`、`Suppliers_Update`、および `Suppliers_Delete`に名前を付けます。

[自動生成されたストアドプロシージャの名前をカスタマイズ ![には](working-with-computed-columns-vb/_static/image11.png)](working-with-computed-columns-vb/_static/image10.png)

**図 4**: 自動生成されたストアドプロシージャの名前をカスタマイズ[する (クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image12.png)されます)

次のウィザードステップでは、TableAdapter のメソッドに名前を指定し、データにアクセスして更新するために使用するパターンを指定することができます。 3つのチェックボックスをすべてオンにしたままにして、`GetData` メソッドの名前を `GetSuppliers`に変更します。 [完了] をクリックしてウィザードを終了します。

[GetData メソッドの名前を GetSuppliers に変更 ![には](working-with-computed-columns-vb/_static/image14.png)](working-with-computed-columns-vb/_static/image13.png)

**図 5**: `GetData` メソッドの名前を `GetSuppliers` に変更する ([クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image15.png)されます)

[完了] をクリックすると、ウィザードによって4つのストアドプロシージャが作成され、TableAdapter および対応する DataTable が型指定されたデータセットに追加されます。

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>手順 4: TableAdapter s メインクエリに計算列を含める

ここで、手順 3. で作成した TableAdapter と DataTable を更新して、`FullContactName` 計算列を含める必要があります。 これには 2 つの手順が含まれます。

1. `FullContactName` 計算列を返すように `Suppliers_Select` ストアドプロシージャを更新する
2. 対応する `FullContactName` 列を含むように DataTable を更新しています。

まず、サーバーエクスプローラーに移動し、[ストアドプロシージャ] フォルダーにドリルダウンします。 `Suppliers_Select` ストアドプロシージャを開き、`FullContactName` 計算列を含めるように `SELECT` クエリを更新します。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample4.sql)]

ツールバーの [保存] アイコンをクリックするか、Ctrl キーを押しながら S キーを押すか、または [ファイル] メニューの [`Suppliers_Select` の保存] オプションを選択して、ストアドプロシージャへの変更を保存します。

次に、データセットデザイナーに戻り、`SuppliersTableAdapter`を右クリックして、コンテキストメニューから [構成] を選択します。 `Suppliers_Select` 列のデータ列コレクションに `FullContactName` 列が含まれるようになったことに注意してください。

[TableAdapter s 構成ウィザードを実行して DataTable の列を更新 ![には](working-with-computed-columns-vb/_static/image17.png)](working-with-computed-columns-vb/_static/image16.png)

**図 6**: TableAdapter の構成ウィザードを実行して DataTable の列を更新する ([クリックすると、フルサイズのイメージが表示](working-with-computed-columns-vb/_static/image18.png)されます)

[完了] をクリックしてウィザードを終了します。 これにより、対応する列が `SuppliersDataTable`に自動的に追加されます。 TableAdapter ウィザードは、`FullContactName` 列が計算列であるため、読み取り専用であることを検出するのに十分なスマートです。 その結果、列 s `ReadOnly` プロパティが `true`に設定されます。 これを確認するには、`SuppliersDataTable` から列を選択し、プロパティウィンドウにアクセスします (図7を参照)。 `FullContactName` 列 s `DataType` と `MaxLength` プロパティも、それに応じて設定されることに注意してください。

[FullContactName 列が読み取り専用としてマークされている](working-with-computed-columns-vb/_static/image20.png)](working-with-computed-columns-vb/_static/image19.png)

**図 7**: `FullContactName` 列が読み取り専用としてマークされている ([クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image21.png)されます)

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>手順 5:`GetSupplierBySupplierID`メソッドを TableAdapter に追加する

このチュートリアルでは、仕入先を更新可能なグリッドで表示する ASP.NET ページを作成します。 これまでのチュートリアルでは、厳密に型指定された DataTable として DAL から特定のレコードを取得し、そのプロパティを更新して、変更を反映するために更新された DataTable を DAL に送り返すことで、ビジネスロジック層から1つのレコードを更新しました。データベース。 この最初の手順を実行するには、DAL から更新されるレコードを取得する必要があります。まず、`GetSupplierBySupplierID(supplierID)` メソッドを DAL に追加する必要があります。

データセットのデザインで `SuppliersTableAdapter` を右クリックし、コンテキストメニューから [クエリの追加] オプションを選択します。 手順 3. で行ったように、[新しいストアドプロシージャの作成] オプションを選択して、ウィザードで新しいストアドプロシージャを生成します (このウィザードの手順のスクリーンショットについては、図3を参照してください)。 このメソッドは複数の列を含むレコードを返すため、行を返す SELECT である SQL クエリを使用することを指定し、[次へ] をクリックします。

[![[行を返す] オプションを選択します。](working-with-computed-columns-vb/_static/image23.png)](working-with-computed-columns-vb/_static/image22.png)

**図 8**: [行を返す] オプションを選択[する (クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image24.png)されます)

後続の手順では、このメソッドに使用するクエリを入力するように求められます。 次のように入力します。これにより、メインクエリと同じデータフィールドが返されますが、特定の仕入先についてはを返します。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample5.sql)]

次の画面では、自動生成されるストアドプロシージャに名前を指定するように求められます。 このストアドプロシージャに名前を `Suppliers_SelectBySupplierID`、[次へ] をクリックします。

[ストアドプロシージャの名前を ![Suppliers_SelectBySupplierID](working-with-computed-columns-vb/_static/image26.png)](working-with-computed-columns-vb/_static/image25.png)

**図 9**: ストアドプロシージャに `Suppliers_SelectBySupplierID` という名前[を指定する (クリックしてフルサイズの画像を表示する](working-with-computed-columns-vb/_static/image27.png))

最後に、TableAdapter に使用するデータアクセスパターンとメソッド名を入力するように求められます。 両方のチェックボックスをオンのままにしますが、`FillBy` および `GetDataBy` メソッドの名前をそれぞれ `FillBySupplierID` および `GetSupplierBySupplierID`に変更します。

[TableAdapter メソッドに FillBySupplierID およびという名前を ![](working-with-computed-columns-vb/_static/image29.png)](working-with-computed-columns-vb/_static/image28.png)

**図 10**: TableAdapter メソッド `FillBySupplierID` および `GetSupplierBySupplierID` の名前を指定[する (クリックすると、フルサイズのイメージが表示](working-with-computed-columns-vb/_static/image30.png)されます)

[完了] をクリックしてウィザードを終了します。

## <a name="step-6-creating-the-business-logic-layer"></a>手順 6: ビジネスロジック層を作成する

手順1で作成した計算列を使用する ASP.NET ページを作成する前に、まず、BLL に対応するメソッドを追加する必要があります。 手順 7. で作成した ASP.NET ページでは、ユーザーがサプライヤーを表示および編集できるようになります。 そのため、少なくとも、すべてのサプライヤーを取得するためのメソッドを提供し、特定の業者を更新するために、BLL が必要です。

`~/App_Code/BLL` フォルダーに `SuppliersBLLWithSprocs` という名前の新しいクラスファイルを作成し、次のコードを追加します。

[!code-vb[Main](working-with-computed-columns-vb/samples/sample6.vb)]

他の BLL クラスと同様に、`SuppliersBLLWithSprocs` には、`Public` と `GetSuppliers` の2つの `UpdateSupplier`メソッドと共に `SuppliersTableAdapter` クラスのインスタンスを返す `Protected` `Adapter` プロパティがあります。 `GetSuppliers` メソッドはを呼び出し、データアクセス層の対応する `GetSupplier` メソッドによって返された `SuppliersDataTable` を返します。 `UpdateSupplier` メソッドは、DAL の `GetSupplierBySupplierID(supplierID)` メソッドの呼び出しによって更新される特定の供給業者に関する情報を取得します。 次に、`CategoryName`、`ContactName`、および `ContactTitle` の各プロパティを更新し、変更された `SuppliersRow` オブジェクトを渡して、データアクセス層 s `Update` メソッドを呼び出して、これらの変更をデータベースにコミットします。

> [!NOTE]
> `SupplierID` と `CompanyName`を除き、仕入先テーブルのすべての列で `NULL` 値が許可されます。 したがって、渡された `contactName` パラメーターまたは `contactTitle` パラメーターが `Nothing` 場合、それぞれ `ContactTitle` メソッドと `NULL` メソッドを使用して、対応する `ContactName` および `SetContactNameNull` プロパティを `SetContactTitleNull` データベース値に設定する必要があります。

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>手順 7: プレゼンテーション層から計算列を操作する

計算列が `Suppliers` テーブルに追加され、DAL と BLL がそれに従って更新されると、`FullContactName` 計算列で動作する ASP.NET ページを作成する準備が整います。 まず、`AdvancedDAL` フォルダーの [`ComputedColumns.aspx`] ページを開き、ツールボックスから GridView をデザイナーにドラッグします。 GridView s `ID` プロパティを `Suppliers` に設定し、そのスマートタグから `SuppliersDataSource`という名前の新しい ObjectDataSource にバインドします。 手順6でもう一度追加した `SuppliersBLLWithSprocs` クラスを使用するように ObjectDataSource を構成し、[次へ] をクリックします。

[SuppliersBLLWithSprocs クラスを使用するように ObjectDataSource を構成 ![には](working-with-computed-columns-vb/_static/image32.png)](working-with-computed-columns-vb/_static/image31.png)

**図 11**: `SuppliersBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](working-with-computed-columns-vb/_static/image33.png))

`SuppliersBLLWithSprocs` クラスで定義されているメソッドは、`GetSuppliers` と `UpdateSupplier`の2つだけです。 [選択] タブと [更新] タブでこれら2つのメソッドが指定されていることを確認し、[完了] をクリックして ObjectDataSource の構成を完了します。

データソース構成ウィザードが完了すると、返された各データフィールドの BoundField が Visual Studio によって追加されます。 `SupplierID` BoundField を削除し、`CompanyName`、`ContactName`、`ContactTitle`、および `FullContactName` BoundFields の `HeaderText` プロパティをそれぞれ会社、連絡先名、タイトル、完全な連絡先名に変更します。 スマートタグから、[編集を有効にする] チェックボックスをオンにして、GridView の組み込み編集機能をオンにします。

BoundFields を GridView に追加するだけでなく、データソースウィザードを完了すると、Visual Studio によって ObjectDataSource s `OldValuesParameterFormatString` プロパティが元の\_{0}に設定されます。 この設定を既定値の {0} に戻します。

GridView および ObjectDataSource に対してこれらの編集を行った後、宣言型マークアップは次のようになります。

[!code-aspx[Main](working-with-computed-columns-vb/samples/sample7.aspx)]

次に、ブラウザーを使用してこのページにアクセスします。 図12に示すように、各仕入先は `FullContactName` 列を含むグリッドに一覧表示されます。値は、`ContactName` (`ContactTitle`、`CompanyName`) として書式設定された他の3つの列を連結したものにすぎません。

[各業者がグリッドに表示され ![](working-with-computed-columns-vb/_static/image35.png)](working-with-computed-columns-vb/_static/image34.png)

**図 12**: 各供給業者がグリッドに表示される ([クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image36.png)されます)

特定の業者の [編集] ボタンをクリックすると、ポストバックが発生し、その行が編集インターフェイスに表示されます (図13を参照)。 最初の3つの列は、既定の編集インターフェイスを表示します。 `Text` プロパティがデータフィールドの値に設定されている TextBox コントロールです。 ただし、`FullContactName` 列はテキストとして残ります。 データソース構成ウィザードの完了時に、BoundFields が GridView に追加されたときに、`FullContactName` BoundField s `ReadOnly` プロパティが `True` に設定されました。これは、`SuppliersDataTable` 内の対応する `FullContactName` 列の `ReadOnly` プロパティが `True`に設定されているためです。 手順 4. で説明したように、TableAdapter によって列が計算列であることが検出されたため、`FullContactName` s `ReadOnly` プロパティが `True` に設定されました。

[![FullContactName 宛先列を編集できない ](working-with-computed-columns-vb/_static/image38.png)](working-with-computed-columns-vb/_static/image37.png)

**図 13**: `FullContactName` 列は編集できません ([クリックすると、フルサイズの画像が表示](working-with-computed-columns-vb/_static/image39.png)されます)

1つまたは複数の編集可能な列の値を更新し、[更新] をクリックします。 変更を反映するために、`FullContactName` s 値が自動的に更新されることに注意してください。

> [!NOTE]
> GridView では、現在、編集可能なフィールドに連結フィールドが使用され、その結果、既定の編集インターフェイスが使用されます。 `CompanyName` フィールドは必須であるため、RequiredFieldValidator を含む TemplateField に変換する必要があります。 これは関心のある読者のための演習として残されています。 BoundField を TemplateField に変換し、検証コントロールを追加するための詳細な手順については、「[編集および挿入インターフェイスに検証コントロールを追加する](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)」のチュートリアルを参照してください。

## <a name="summary"></a>要約

テーブルのスキーマを定義すると、Microsoft SQL Server によって計算列を含めることができます。 これらは、通常、同じレコード内の他の列の値を参照する式から値が計算される列です。 計算列の値は式に基づいているため、これらは読み取り専用であり、`INSERT` または `UPDATE` ステートメントで値を代入することはできません。 これにより、対応する `INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成しようとする TableAdapter のメインクエリで計算列を使用する場合の課題が生じます。

このチュートリアルでは、計算列によって生じる問題を回避するための手法について説明しました。 具体的には、TableAdapter でストアドプロシージャを使用して、アドホック SQL ステートメントを使用する Tableadapter に固有の高まるを克服しています。 TableAdapter ウィザードで新しいストアドプロシージャを作成する場合は、データ変更ストアドプロシージャが生成されないようにするため、メインクエリで計算列を最初に省略することが重要です。 TableAdapter が最初に構成された後は、その `SelectCommand` ストアドプロシージャを再設定して、計算列を含めることができます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Geisenow and Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](adding-additional-datatable-columns-vb.md)
> [次へ](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
