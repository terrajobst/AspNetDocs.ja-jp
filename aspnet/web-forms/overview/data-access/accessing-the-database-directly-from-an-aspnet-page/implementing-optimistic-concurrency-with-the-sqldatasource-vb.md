---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: SqlDataSource (VB) を使用したオプティミスティック同時実行制御の実装Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、オプティミスティック同時実行制御の基礎を確認し、SqlDataSource コントロールを使用して実装する方法について説明します。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 431734b5245c20ac840147cf0827fa7f8d1e4d17
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597645"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>SqlDataSource でオプティミスティック同時実行制御を実装する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe)または[PDF のダウンロード](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> このチュートリアルでは、オプティミスティック同時実行制御の基礎を確認し、SqlDataSource コントロールを使用して実装する方法について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、SqlDataSource コントロールに挿入、更新、削除の各機能を追加する方法を説明しています。 つまり、これらの機能を提供するには、コントロール s `InsertCommand`、`UpdateCommand`、`DeleteCommand` の各プロパティで、対応する `INSERT`、`UPDATE`、または `DELETE` SQL ステートメントを、`InsertParameters`、`UpdateParameters`、および `DeleteParameters` の各コレクションの適切なパラメーターと共に指定する必要がありました。 これらのプロパティとコレクションは手動で指定できますが、[データソースの構成ウィザード] の [詳細設定] ボタンをクリックすると、[`INSERT`、`UPDATE`、および `DELETE` ステートメントの生成] チェックボックスが表示され、これらのステートメントが `SELECT` ステートメントに基づいて自動的に作成されます。

[`INSERT`の生成]、[`UPDATE`]、および [`DELETE` ステートメント] チェックボックスと共に、[SQL 生成の詳細オプション] ダイアログボックスには、オプティミスティック同時実行オプションがあります (図1を参照)。 オンになっている場合、自動生成された `UPDATE` ステートメントと `DELETE` ステートメントの `WHERE` 句は、ユーザーが最後にデータをグリッドに読み込んだ後に基になるデータベースデータが変更されていない場合にのみ、更新または削除を実行するように変更されます。

![オプティミスティック同時実行制御のサポートは、[SQL 生成の詳細オプション] ダイアログボックスから追加できます。](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**図 1**: [SQL 生成の詳細オプション] ダイアログボックスでオプティミスティック同時実行制御のサポートを追加する

「[オプティミスティック同時実行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)制御の実装」チュートリアルに戻り、オプティミスティック同時実行制御の基礎と、それを ObjectDataSource に追加する方法について説明します。 このチュートリアルでは、オプティミスティック同時実行制御の基礎を詳しく説明し、SqlDataSource を使用した実装方法について説明します。

## <a name="a-recap-of-optimistic-concurrency"></a>オプティミスティック同時実行制御の要約

複数のユーザーが同時に同じデータを編集または削除できるようにする web アプリケーションの場合、1人のユーザーが別の変更を誤って上書きする可能性があります。 [オプティミスティック同時実行制御の実装](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)に関するチュートリアルでは、次の例を示しました。

Jisun と Sam の2人のユーザーが、アプリケーション内のページにアクセスしていて、ビジターが GridView コントロールを使用して製品を更新および削除できることを想像してください。 両方とも、同じ時刻の Chai の [編集] ボタンをクリックします。 Jisun は製品名を Chai 茶に変更し、[更新] ボタンをクリックします。 結果として、データベースに送信される `UPDATE` ステートメントがあります。これにより、*すべて*の製品の更新可能フィールドが設定されます (Jisun によって1つのフィールドが更新された場合でも、`ProductName`)。 この時点で、データベースには、この特定の製品について、Chai 茶、カテゴリ飲み物、仕入先の特別な液体などが含まれています。 ただし、[Sam s] 画面の GridView でも、編集可能な GridView 行の製品名は Chai として表示されます。 Jisun s の変更がコミットされてから数秒後に、Sam はカテゴリを Condiments に更新し、[更新] をクリックします。 この結果、製品名を Chai に設定する `UPDATE` ステートメントがデータベースに送信され、`CategoryID` が対応する Condiments category ID になります。 製品名に対する jisun の変更が上書きされました。

図2は、この相互作用を示しています。

[2人のユーザーが同時にレコードを更新するときに、1人のユーザーの変更によって他のが上書きされる可能性がある ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**図 2**: 2 人のユーザーが同時にレコードを更新する場合、1人のユーザーの変更によって他のが上書きされる可能性があります ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png)されます)。

このシナリオを確保に防ぐには、[同時実行制御](http://en.wikipedia.org/wiki/Concurrency_control)の形式を実装する必要があります。 [オプティミスティック同時実行制御](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)このチュートリアルでは、同時実行の競合が発生する可能性がありますが、このような競合が発生することはほとんどありません。 そのため、競合が発生した場合、オプティミスティック同時実行制御は、別のユーザーが同じデータを変更したため変更を保存できないことをユーザーに通知するだけです。

> [!NOTE]
> 多くの同時実行の競合が発生すると想定されるアプリケーションの場合、またはこのような競合が許容できない場合は、代わりにペシミスティック同時実行制御を使用できます。 ペシミスティック同時実行制御の詳細については、「[オプティミスティック同時実行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)制御の実装」を参照してください。

オプティミスティック同時実行制御は、更新または削除するレコードの値が、更新または削除処理の開始時と同じ値であることを保証することによって機能します。 たとえば、編集可能な GridView で [編集] ボタンをクリックすると、レコードの値がデータベースから読み取られ、テキストボックスやその他の Web コントロールに表示されます。 これらの元の値は、GridView によって保存されます。 その後、ユーザーが変更を行って [更新] ボタンをクリックした後、使用する `UPDATE` ステートメントで元の値と新しい値を考慮する必要があります。また、ユーザーが編集を開始した元の値がデータベース内の値と同じである場合にのみ、基になるデータベースレコードを更新します。 図3は、この一連のイベントを示しています。

[更新または削除を成功させるには、元の値が現在のデータベースの値と同じである必要があり ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**図 3**: 更新または削除を成功させるには、元の値が現在のデータベースの値と同じである必要があります ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png)されます)。

オプティミスティック同時実行制御の実装にはさまざまな方法があります (いくつかのオプションについては、「 [Bromberg](http://peterbromberg.net/)の[オプティミスティック同時実行制御のロジック](http://www.eggheadcafe.com/articles/20050719.asp)」を参照してください)。 SqlDataSource (およびデータアクセス層で使用される ADO.NET 型指定されたデータセット) によって使用される手法により、`WHERE` 句が、元のすべての値の比較を含むように強化されます。 次の `UPDATE` ステートメントでは、現在のデータベース値が GridView のレコードを更新するときに最初に取得された値と等しい場合にのみ、製品の名前と価格を更新します。 `@ProductName` パラメーターと `@UnitPrice` パラメーターには、ユーザーが入力した新しい値が含まれます。一方、`@original_ProductName` と `@original_UnitPrice` には、[編集] ボタンをクリックしたときに GridView に最初に読み込まれた値が含まれます。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

このチュートリアルで説明するように、SqlDataSource でオプティミスティック同時実行制御を有効にすることは、チェックボックスをオンにするだけで簡単です。

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>手順 1: オプティミスティック同時実行制御をサポートする SqlDataSource の作成

まず、`SqlDataSource` フォルダーから [`OptimisticConcurrency.aspx`] ページを開きます。 SqlDataSource コントロールをツールボックスからデザイナーにドラッグし、その `ID` プロパティを `ProductsDataSourceWithOptimisticConcurrency`に設定します。 次に、コントロール s スマートタグから [データソースの構成] リンクをクリックします。 ウィザードの最初の画面で、`NORTHWINDConnectionString` を操作することを選択し、[次へ] をクリックします。

[NORTHWINDConnectionString の操作を選択 ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**図 4**: `NORTHWINDConnectionString` の操作を選択する ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png)されます)

この例では、ユーザーが `Products` テーブルを編集できるようにする GridView を追加します。 そのため、[Select ステートメントの構成] 画面で、ドロップダウンリストから `Products` テーブルを選択し、図5に示すように、[`ProductID`]、[`ProductName`]、[`UnitPrice`]、[`Discontinued`] の各列を選択します。

[Products テーブルから ![、ProductID、ProductName、UnitPrice、および廃止された列を返します。](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**図 5**: `Products` テーブルから、`ProductID`、`ProductName`、`UnitPrice`、および `Discontinued` の各列を返します ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png)されます)。

列を選択したら、[詳細設定] ボタンをクリックして [SQL 生成の詳細オプション] ダイアログボックスを表示します。 `INSERT`、`UPDATE`、および `DELETE` のステートメントを生成し、オプティミスティック同時実行チェックボックスをオンにして、[OK] をクリックします (スクリーンショットについては、図1を参照してください)。 [次へ] をクリックし、[完了] をクリックしてウィザードを完了します。

データソースの構成ウィザードを完了した後、結果の `DeleteCommand` と `UpdateCommand` プロパティ、および `DeleteParameters` および `UpdateParameters` コレクションを確認します。 これを行う最も簡単な方法は、左下隅にある [ソース] タブをクリックして、ページの宣言構文を表示することです。 次のような `UpdateCommand` 値が表示されます。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

`UpdateParameters` コレクションに7つのパラメーターがある場合:

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

同様に、`DeleteCommand` のプロパティと `DeleteParameters` コレクションは次のようになります。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

[オプティミスティック同時実行制御を使用] オプションを選択すると、`UpdateCommand` プロパティと `DeleteCommand` プロパティの `WHERE` 句を補強するだけでなく、その他のパラメーターを各パラメーターコレクションに追加することもできます。

- [`ConflictDetection` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx)を `OverwriteChanges` (既定値) からに変更 `CompareAllValues`
- [`OldValuesParameterFormatString` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx)を {0} (既定値) から元の\_{0} に変更します。

データ Web コントロールが SqlDataSource s `Update()` または `Delete()` メソッドを呼び出すと、元の値が渡されます。 SqlDataSource s `ConflictDetection` プロパティが `CompareAllValues`に設定されている場合、これらの元の値はコマンドに追加されます。 `OldValuesParameterFormatString` プロパティは、これらの元の値パラメーターに使用される名前付けパターンを提供します。 データソースの構成ウィザードでは、元の\_{0} を使用して、`UpdateCommand` の元のパラメーターと `DeleteCommand` のプロパティを指定し、それに従って `UpdateParameters` コレクションを `DeleteParameters` します。

> [!NOTE]
> SqlDataSource control s の挿入機能を使用しないので、`InsertCommand` プロパティとその `InsertParameters` コレクションを削除してもかまいません。

## <a name="correctly-handlingnullvalues"></a>`NULL`値の正しく処理

ただし、オプティミスティック同時実行制御を使用しているときに、データソースの構成ウィザードによって自動生成される拡張 `UPDATE` および `DELETE` ステートメントは、`NULL` 値を含むレコードでは機能し*ません*。 その理由を確認するために、次の `UpdateCommand`を考えてみましょう。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`Products` テーブルの `UnitPrice` 列には `NULL` 値を指定できます。 特定のレコードに `UnitPrice`の `NULL` 値がある場合、`NULL = NULL` は常に False を返すため、`WHERE` 句の `[UnitPrice] = @original_UnitPrice` は*常*に false と評価されます。 したがって、`NULL` 値を含むレコードを編集または削除することはできません。 `UPDATE` と `DELETE` ステートメント `WHERE` 句は、更新または削除する行を返しません。

> [!NOTE]
> このバグは最初に Microsoft に報告され、SqlDataSource の2004年6月に、[不適切な SQL ステートメントが生成](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937)され、次のバージョンの ASP.NET で修正される予定です。

この問題を解決するには、`NULL` 値を持つことのできる**すべて**の列の `UpdateCommand` プロパティと `DeleteCommand` プロパティの両方で、`WHERE` 句を手動で更新する必要があります。 一般に、`[ColumnName] = @original_ColumnName` をに変更します。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

この変更は、宣言マークアップ、プロパティウィンドウの UpdateQuery または DeleteQuery オプション、またはデータの構成の [カスタム SQL ステートメントまたはストアドプロシージャの指定] オプションの [更新] タブと [削除] タブを使用して直接行うことができます。ソースウィザード。 ここでも、`NULL` 値を含むことができる `UpdateCommand` および `DeleteCommand` s `WHERE` 句の*すべて*の列に対してこの変更を行う必要があります。

この例に適用すると、次の変更された `UpdateCommand` と `DeleteCommand` 値が生成されます。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>手順 2: 編集および削除オプションを使用した GridView の追加

オプティミスティック同時実行制御をサポートするように SqlDataSource が構成されていれば、この同時実行制御を使用するページにデータ Web コントロールを追加するだけで済みます。 このチュートリアルでは、編集と削除の両方の機能を提供する GridView を追加してみましょう。 これを行うには、GridView をツールボックスからデザイナーにドラッグし、その `ID` を `Products`に設定します。 GridView s スマートタグから、手順1で追加した `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource コントロールにバインドします。 最後に、[編集を有効にする] チェックボックスをオンにして、スマートタグから削除オプションを有効にします。

[GridView を SqlDataSource にバインドし、編集と削除を有効に ![には](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**図 6**: GridView を SqlDataSource にバインドし、編集と削除を有効に[する (クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png)されます)

GridView を追加した後、`ProductID` BoundField を削除し、`ProductName` BoundField s `HeaderText` プロパティを Product に変更し、`UnitPrice` BoundField を更新して、その `HeaderText` プロパティが単なる価格になるように、その外観を構成します。 理想的には、編集インターフェイスを拡張して、`ProductName` 値の RequiredFieldValidator と、`UnitPrice` 値の CompareValidator (適切に書式設定された数値) を含めることができるようにします。 GridView の編集インターフェイスのカスタマイズの詳細については、[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)に関するチュートリアルを参照してください。

> [!NOTE]
> Gridview から SqlDataSource に渡された元の値がビューステートに格納されるため、GridView のビューステートを有効にする必要があります。

GridView に対してこれらの変更を行った後、GridView および SqlDataSource 宣言マークアップは次のようになります。

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

オプティミスティック同時実行制御の動作を確認するには、2つのブラウザーウィンドウを開き、両方の `OptimisticConcurrency.aspx` ページを読み込みます。 両方のブラウザーで最初の製品の [編集] ボタンをクリックします。 1つのブラウザーで製品名を変更し、[更新] をクリックします。 ブラウザーがポストバックされ、GridView が編集前のモードに戻り、編集したばかりのレコードの新しい製品名が表示されます。

2番目のブラウザーウィンドウで価格を変更し (ただし、製品名は元の値のままにします)、[更新] をクリックします。 ポストバック時に、グリッドは編集前モードに戻りますが、価格の変更は記録されません。 2番目のブラウザーでは、最初の値と同じ値が、新しい製品名と古い価格で表示されます。 2番目のブラウザーウィンドウで行った変更は失われました。 また、同時実行違反が発生したことを示す例外やメッセージがないため、変更は自動的に失われました。

[2番目のブラウザーウィンドウでの変更がサイレントに失われた ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**図 7**: 2 番目のブラウザーウィンドウでの変更がサイレントに失われました ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png)されます)

2番目のブラウザーの変更がコミットされなかった理由は、`UPDATE` statement s `WHERE` 句によってすべてのレコードが除外されているため、どの行にも影響しないためです。 `UPDATE` ステートメントをもう一度見てみましょう。

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

2番目のブラウザーウィンドウでレコードが更新されると、`WHERE` 句で指定された元の製品名は、(最初のブラウザーによって変更されたため) 既存の製品名と一致しません。 したがって、ステートメント `[ProductName] = @original_ProductName` は False を返し、`UPDATE` はどのレコードにも影響しません。

> [!NOTE]
> Delete は同じ方法で動作します。 2つのブラウザーウィンドウを開いた状態で、特定の製品を1つずつ編集し、その変更を保存します。 1つのブラウザーで変更を保存した後、もう一方の製品の同じ製品の [削除] ボタンをクリックします。 元の値は `DELETE` statement s `WHERE` 句では一致しないため、削除はサイレントに失敗します。

2番目のブラウザーウィンドウのエンドユーザーの視点から、[更新] ボタンをクリックした後、グリッドは編集前モードに戻りますが、変更は失われていました。 ただし、変更が反映されていないという視覚的なフィードバックはありません。 ユーザーの変更が同時実行違反に失われた場合は、そのことを通知し、おそらくグリッドを編集モードのままにしておきます。 これを実現する方法を見てみましょう。

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>手順 3: 同時実行違反が発生したことを確認する

同時実行違反によって行われた変更は拒否されるため、同時実行違反が発生した場合にユーザーに警告することができます。 ユーザーに警告するには、`Text` `ConcurrencyViolationMessage` という名前のページの先頭にラベル Web コントロールを追加します。これにより、別のユーザーによって同時に更新されたレコードを更新または削除しようとしたことを示すメッセージが表示されます。 他のユーザーの変更内容を確認してから、更新または削除をやり直してください。 Label コントロール s `CssClass` プロパティを Warning に設定します。これは、赤、斜体、太字、および大きいフォントでテキストを表示する `Styles.css` で定義された CSS クラスです。 最後に、Label s `Visible` と `EnableViewState` プロパティを `False`に設定します。 これにより、`Visible` プロパティを明示的に `True`に設定したポストバックだけを除き、ラベルは非表示になります。

[警告を表示するラベルコントロールをページに追加 ![には](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**図 8**: 警告を表示するためのラベルコントロールをページに追加する ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png)されます)

Update または delete を実行すると、データソースコントロールが要求された更新または削除を実行した後に、GridView s `RowUpdated` イベントハンドラーと `RowDeleted` イベントハンドラーが起動します。 これらのイベントハンドラーから、操作によって影響を受けた行の数を確認できます。 0行が影響を受けた場合は、`ConcurrencyViolationMessage` ラベルを表示します。

`RowUpdated` イベントと `RowDeleted` イベントの両方のイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

どちらのイベントハンドラーでも、`e.AffectedRows` プロパティを確認し、0に等しい場合は、`ConcurrencyViolationMessage` Label s `Visible` プロパティを `True`に設定します。 `RowUpdated` イベントハンドラーでは、`KeepInEditMode` プロパティを true に設定して、GridView を編集モードのままにするように指示します。 その場合は、データをグリッドに再バインドして、他のユーザーのデータが編集インターフェイスに読み込まれるようにする必要があります。 これは、GridView s `DataBind()` メソッドを呼び出すことによって実現されます。

図9に示すように、これら2つのイベントハンドラーを使用すると、同時実行違反が発生するたびに非常に顕著なメッセージが表示されます。

[同時実行違反の発生時にメッセージが表示される ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**図 9**: 同時実行違反の発生時にメッセージが表示される ([クリックすると、フルサイズの画像が表示](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png)されます)

## <a name="summary"></a>要約

複数の同時実行ユーザーが同じデータを編集している可能性がある web アプリケーションを作成する場合は、同時実行制御オプションを考慮することが重要です。 既定では、ASP.NET データの Web コントロールとデータソースコントロールは、同時実行制御を使用しません。 このチュートリアルで説明したように、SqlDataSource を使用したオプティミスティック同時実行制御の実装は比較的迅速で簡単です。 SqlDataSource は、拡張された `WHERE` 句を自動生成された `UPDATE` および `DELETE` のステートメントに追加するためのほとんどの業務を処理しますが、`NULL` 値の列の処理にはいくつかの微妙な違いがあります。詳細については、「`NULL` 値を正しく処理する」セクションを参照してください。

このチュートリアルでは、SqlDataSource の調査を終了します。 残りのチュートリアルでは、ObjectDataSource と階層型アーキテクチャを使用したデータの操作に戻ります。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
