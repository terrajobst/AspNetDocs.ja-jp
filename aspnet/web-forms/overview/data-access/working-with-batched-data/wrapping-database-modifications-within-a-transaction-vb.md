---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
title: トランザクション内でのデータベース変更のラップ (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルは、データのバッチの更新、削除、および挿入についての最初の4つです。 このチュートリアルでは、データベーストランザクションでできることについて説明します。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 7d821db5-6cbb-4b38-af14-198f9155fc82
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
msc.type: authoredcontent
ms.openlocfilehash: dee95ee2789a69aac5aa79b8358e58e3ee99e1b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78475888"
---
# <a name="wrapping-database-modifications-within-a-transaction-vb"></a>トランザクション内のデータベース変更をラップする (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_VB.zip)または[PDF のダウンロード](wrapping-database-modifications-within-a-transaction-vb/_static/datatutorial63vb1.pdf)

> このチュートリアルは、データのバッチの更新、削除、および挿入についての最初の4つです。 このチュートリアルでは、データベーストランザクションでバッチ変更をアトミック操作として実行する方法について説明します。これにより、すべての手順が成功するか、すべての手順が失敗します。

## <a name="introduction"></a>はじめに

[「データの挿入、更新、削除の概要」](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)で説明したように、GridView では行レベルの編集と削除のサポートが組み込まれています。 マウスを数回クリックするだけで、コードを記述せずに豊富なデータ変更インターフェイスを作成することができます。ただし、コンテンツが行ごとに編集および削除される場合に限ります。 ただし、特定のシナリオでは、これは不十分であり、レコードのバッチを編集または削除する機能をユーザーに提供する必要があります。

たとえば、ほとんどの web ベースの電子メールクライアントでは、グリッドを使用して各メッセージが一覧表示されます。各行には、電子メール情報 (件名、送信者など) と共にチェックボックスがあります。 このインターフェイスを使うと、ユーザーは複数のメッセージを確認し、[選択したメッセージの削除] ボタンをクリックして削除できます。 バッチ編集インターフェイスは、ユーザーが多くの異なるレコードを頻繁に編集する場合に最適です。 変更する必要があるレコードごとに、ユーザーが [編集] をクリックして変更を行い、[更新] をクリックするのではなく、バッチ編集インターフェイスによって各行が編集インターフェイスと共に表示されます。 ユーザーは、変更する必要がある行のセットをすばやく変更し、[すべて更新] ボタンをクリックして変更を保存することができます。 この一連のチュートリアルでは、データのバッチを挿入、編集、および削除するためのインターフェイスを作成する方法について説明します。

バッチ操作を実行するときは、バッチ内の操作の一部が成功するかどうかを判断することが重要です。 バッチ削除インターフェイスを考えてみます。最初に選択したレコードが正常に削除された場合に、2番目のレコードが失敗した場合 (外部キー制約違反が原因で、 最初のレコードの削除をロールバックする必要がありますか。最初のレコードを削除したままにすることは許容されますか。

バッチ操作を[アトミックな操作](http://en.wikipedia.org/wiki/Atomic_operation)として処理する場合、すべての手順が成功するか、すべての手順が失敗する場合は、[データベーストランザクション](http://en.wikipedia.org/wiki/Database_transaction)のサポートを含めるようにデータアクセス層を拡張する必要があります。 データベーストランザクションでは、トランザクションの全体で実行される一連の `INSERT`、`UPDATE`、および `DELETE` ステートメントの原子性を保証し、最新のすべてのデータベースシステムでサポートされている機能です。

このチュートリアルでは、DAL を拡張してデータベーストランザクションを使用する方法について説明します。 以降のチュートリアルでは、バッチの挿入、更新、および削除のための web ページの実装について説明します。 始めましょう!

> [!NOTE]
> バッチトランザクション内のデータを変更する場合、原子性は必ずしも必要ではありません。 場合によっては、web ベースの電子メールクライアントから一連の電子メールを削除するなど、一部のデータ変更が成功し、同じバッチ内の他のユーザーが失敗することがあります。 削除処理中にデータベースエラーが発生した場合は、エラーなしで処理されたレコードを削除したままにすることができます。 このような場合は、データベーストランザクションをサポートするために DAL を変更する必要はありません。 ただし、その他のバッチ操作シナリオでは、原子性が不可欠です。 顧客が銀行口座から別の銀行口座に資金を移動する場合、2つの操作を実行する必要があります。1つ目のアカウントから資金を差し引き、2番目の口座に追加する必要があります。 銀行では最初のステップが成功しても、2番目のステップは失敗しても、その顧客は当然てしまうことを気にすることはできません。 このチュートリアルでは、次の3つのチュートリアルで作成するインターフェイスの挿入、更新、および削除をバッチで使用する予定がない場合でも、データベーストランザクションをサポートするために、DAL の機能強化を実装することをお勧めします。

## <a name="an-overview-of-transactions"></a>トランザクションの概要

ほとんどのデータベースには*トランザクション*のサポートが含まれており、複数のデータベースコマンドを1つの論理的な作業単位にグループ化することができます。 トランザクションを構成するデータベースコマンドはアトミックであることが保証されます。つまり、すべてのコマンドが失敗するか、すべてが成功します。

一般に、トランザクションは、次のパターンを使用して SQL ステートメントによって実装されます。

1. トランザクションの開始を示します。
2. トランザクションを構成する SQL ステートメントを実行します。
3. 手順 2. のステートメントのいずれかでエラーが発生した場合は、トランザクションをロールバックします。
4. 手順 2. のすべてのステートメントがエラーなしで完了した場合は、トランザクションをコミットします。

トランザクションの作成、コミット、およびロールバックに使用される SQL ステートメントは、SQL スクリプトの記述時やストアドプロシージャの作成時に手動で入力することも、 [`System.Transactions` 名前空間](https://msdn.microsoft.com/library/system.transactions.aspx)の ADO.NET またはクラスを使用してプログラムによって指定することもできます。 このチュートリアルでは、ADO.NET を使用したトランザクションの管理のみを確認します。 今後のチュートリアルでは、データアクセス層でストアドプロシージャを使用する方法について説明します。この時点で、トランザクションを作成、ロールバック、およびコミットするための SQL ステートメントについて説明します。 詳細については、「 [SQL Server ストアドプロシージャでのトランザクションの管理](http://www.4guysfromrolla.com/webtech/080305-1.shtml)」を参照してください。

> [!NOTE]
> `System.Transactions` 名前空間の[`TransactionScope` クラス](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx)を使用すると、開発者はトランザクションのスコープ内で一連のステートメントをプログラムによってラップできます。また、2つの異なるデータベース、または Microsoft SQL Server データベース、Oracle データベース、Web サービスなどの異種データストアの種類も含めて、複数のソースが関係する複雑なトランザクションがサポートされます。 このチュートリアルでは、`TransactionScope` クラスの代わりに ADO.NET トランザクションを使用することにしました。これは、ADO.NET がデータベーストランザクションにより固有であり、多くの場合、リソースの消費量がはるかに少なくなるためです。 また、特定のシナリオでは、`TransactionScope` クラスは Microsoft 分散トランザクションコーディネーター (MSDTC) を使用します。 MSDTC を取り巻く構成、実装、およびパフォーマンスの問題により、特に専門的で高度なトピックが作成され、これらのチュートリアルの範囲を超えています。

ADO.NET で SqlClient プロバイダーを使用する場合、トランザクションは[`SqlTransaction` オブジェクト](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)を返す[`SqlConnection` クラス](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)s [`BeginTransaction` メソッド](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)の呼び出しを通じて開始されます。 トランザクションを作成するデータ変更ステートメントは、`try...catch` ブロック内に配置されます。 `try` ブロック内のステートメントでエラーが発生した場合、実行は、`SqlTransaction` オブジェクト s [`Rollback` メソッド](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)を介してトランザクションをロールバックできる `catch` ブロックに転送されます。 すべてのステートメントが正常に完了した場合、`try` ブロックの最後に `SqlTransaction` object s [`Commit` メソッド](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx)を呼び出すと、トランザクションがコミットされます。 次のコードスニペットは、このパターンを示しています。 ADO.NET でトランザクションを使用する場合のその他の構文と例については、「[トランザクションとデータベースの一貫性の維持](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)」を参照してください。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample1.vb)]

既定では、型指定されたデータセット内の Tableadapter はトランザクションを使用しません。 トランザクションのサポートを提供するには、上記のパターンを使用する追加のメソッドを含むように TableAdapter クラスを拡張して、トランザクションのスコープ内で一連のデータ変更ステートメントを実行する必要があります。 手順 2. では、部分クラスを使用してこれらのメソッドを追加する方法について説明します。

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>手順 1: バッチ処理されたデータ Web ページの操作を作成する

データベーストランザクションをサポートするために DAL を拡張する方法について説明する前に、まず、このチュートリアルで必要となる ASP.NET web ページと、次の3つのページを作成します。 まず、`BatchData` という名前の新しいフォルダーを追加し、次の ASP.NET ページを追加します。各ページは `Site.master` マスターページに関連付けられています。

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する](wrapping-database-modifications-within-a-transaction-vb/_static/image1.gif)

**図 1**: SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`Default.aspx` は `SectionLevelTutorialListing.ascx` ユーザーコントロールを使用して、そのセクション内のチュートリアルの一覧を表示します。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](wrapping-database-modifications-within-a-transaction-vb/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image1.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](wrapping-database-modifications-within-a-transaction-vb/_static/image2.png)されます)

最後に、これらの4つのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、`<siteMapNode>`サイトマップのカスタマイズの後に、次のマークアップを追加します。

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample2.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、バッチ化されたデータのチュートリアルを使用するための項目が含まれるようになりました。

![サイトマップに、バッチ処理されたデータの使用に関するチュートリアルのエントリが含まれるようになりました。](wrapping-database-modifications-within-a-transaction-vb/_static/image3.gif)

**図 3**: サイトマップに、バッチ処理されたデータの使用に関するチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>手順 2: データベーストランザクションをサポートするためのデータアクセス層の更新

最初のチュートリアルで説明したように、[データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)では、DAL 内の型指定されたデータセットは Datatable と tableadapter で構成されています。 データテーブルはデータを保持しますが、Tableadapter はデータベースから Datatable にデータを読み取り、Datatable に加えられた変更でデータベースを更新する機能を提供します。 Tableadapter には、データを更新するための2つのパターンが用意されています。これは、Batch Update と DB Direct と呼ばれていました。 バッチ更新パターンでは、TableAdapter にデータセット、DataTable、または Datarow のコレクションが渡されます。 このデータは列挙され、挿入、変更、または削除された行ごとに、`InsertCommand`、`UpdateCommand`、または `DeleteCommand` が実行されます。 DB ダイレクトパターンでは、1つのレコードの挿入、更新、または削除に必要な列の値が TableAdapter に渡されます。 次に、DB Direct pattern メソッドは、渡された値を使用して、適切な `InsertCommand`、`UpdateCommand`、または `DeleteCommand` ステートメントを実行します。

使用する更新パターンに関係なく、Tableadapter の自動生成メソッドはトランザクションを使用しません。 既定では、TableAdapter によって実行される挿入、更新、または削除は、1つの個別の操作として扱われます。 たとえば、データベースに10個のレコードを挿入するために、BLL の一部のコードで DB ダイレクトパターンが使用されているとします。 このコードは、TableAdapter s `Insert` メソッドを10回呼び出します。 最初の5つの挿入が成功しても、6番目の挿入によって例外が発生した場合、最初の5つの挿入レコードはデータベースに残ります。 同様に、バッチ更新パターンを使用して、DataTable 内の挿入、変更、および削除された行に対して挿入、更新、および削除を実行する場合、最初のいくつかの変更が成功したが、後でエラーが発生した場合は、以前の変更が完了したはデータベースに残ります。

特定のシナリオでは、一連の変更に対して原子性を確保する必要があります。 これを実現するには、トランザクションの包括的な下で `InsertCommand`、`UpdateCommand`、および `DeleteCommand` を実行する新しいメソッドを追加して、手動で TableAdapter を拡張する必要があります。 「[データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)」では、[部分クラス](http://en.wikipedia.org/wiki/Partial_type)を使用して、型指定されたデータセット内の datatable の機能を拡張する方法を見てきました。 この手法は、Tableadapter でも使用できます。

型指定されたデータセット `Northwind.xsd` は、`App_Code` folder s `DAL` サブフォルダーにあります。 `TransactionSupport` という名前の `DAL` フォルダーにサブフォルダーを作成し、`ProductsTableAdapter.TransactionSupport.vb` という名前の新しいクラスファイルを追加します (図4を参照)。 このファイルには、トランザクションを使用してデータ変更を実行するためのメソッドを含む `ProductsTableAdapter` の部分実装が格納されます。

![TransactionSupport という名前のフォルダーと ProductsTableAdapter という名前のクラスファイルを追加します。](wrapping-database-modifications-within-a-transaction-vb/_static/image4.gif)

**図 4**: `TransactionSupport` という名前のフォルダーと、という `ProductsTableAdapter.TransactionSupport.vb` 名前のクラスファイルを追加する

`ProductsTableAdapter.TransactionSupport.vb` ファイルに次のコードを入力します。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample3.vb)]

ここでは、クラス宣言内の `Partial` キーワードは、内に追加されたメンバーが `NorthwindTableAdapters` 名前空間の `ProductsTableAdapter` クラスに追加されることをコンパイラに示しています。 ファイルの先頭にある `Imports System.Data.SqlClient` ステートメントに注意してください。 TableAdapter は SqlClient プロバイダーを使用するように構成されているため、内部的には[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx)オブジェクトを使用して、そのコマンドをデータベースに発行します。 そのため、`SqlTransaction` クラスを使用してトランザクションを開始し、それをコミットするかロールバックする必要があります。 Microsoft SQL Server 以外のデータストアを使用している場合は、適切なプロバイダーを使用する必要があります。

これらのメソッドには、トランザクションの開始、ロールバック、およびコミットに必要な構成要素が用意されています。 これらは `Public`としてマークされ、`ProductsTableAdapter`内、DAL 内の別のクラス、または BLL などのアーキテクチャの別の層から使用できるようにします。 `BeginTransaction` は、TableAdapter の内部 `SqlConnection` (必要に応じて) を開き、トランザクションを開始して `Transaction` プロパティに割り当て、トランザクションを内部 `SqlDataAdapter` s `SqlCommand` オブジェクトにアタッチします。 `CommitTransaction` と `RollbackTransaction` は、内部 `Rollback` オブジェクトを閉じる前に、それぞれ `Transaction` オブジェクト s `Commit` および `Connection` メソッドを呼び出します。

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>手順 3: トランザクションの包括的なデータを更新および削除するメソッドを追加する

これらのメソッドが完成したので、`ProductsDataTable` にメソッドを追加したり、トランザクションの包括的な一連のコマンドを実行する BLL にメソッドを追加したりできます。 次のメソッドでは、バッチ更新パターンを使用して、トランザクションを使用して `ProductsDataTable` インスタンスを更新します。 `BeginTransaction` メソッドを呼び出してトランザクションを開始し、次に `Try...Catch` ブロックを使用してデータ変更ステートメントを発行します。 `Adapter` object s `Update` メソッドの呼び出しで例外が発生した場合、トランザクションがロールバックされ、例外が再スローされる `catch` ブロックに実行が転送されます。 `Update` メソッドは、指定された `ProductsDataTable` の行を列挙し、必要な `InsertCommand`、`UpdateCommand`、および `DeleteCommand` を実行することで、バッチ更新パターンを実装していることを思い出してください。 これらのコマンドのいずれかでエラーが発生した場合は、トランザクションがロールバックされ、トランザクションの有効期間中に行われた以前の変更が元に戻されます。 `Update` ステートメントがエラーなしで完了した場合、トランザクション全体がコミットされます。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample4.vb)]

`ProductsTableAdapter.TransactionSupport.vb`の部分クラスを使用して、`UpdateWithTransaction` メソッドを `ProductsTableAdapter` クラスに追加します。 または、このメソッドをビジネスロジック層 s `ProductsBLL` クラスに追加して、いくつかのマイナー構文変更を加えることもできます。 つまり、`Me.BeginTransaction()`、`Me.CommitTransaction()`、および `Me.RollbackTransaction()` のキーワード `Me` は `Adapter` に置き換える必要があります (`Adapter` は `ProductsBLL` 型の `ProductsTableAdapter`のプロパティの名前であることを思い出してください)。

`UpdateWithTransaction` メソッドはバッチ更新パターンを使用しますが、次のメソッドに示すように、一連の DB ダイレクト呼び出しをトランザクションのスコープ内で使用することもできます。 `DeleteProductsWithTransaction` メソッドは、`Integer`型の `List(Of T)` を入力として受け入れます。これは、削除する `ProductID` s です。 メソッドは `BeginTransaction` への呼び出しを通じてトランザクションを開始した後、`Try` ブロック内で、各 `ProductID` 値に対して DB ダイレクトパターン `Delete` メソッドを呼び出して、指定されたリストを反復処理します。 `Delete` の呼び出しが失敗した場合、トランザクションがロールバックされ、例外が再スローされる `Catch` ブロックに制御が移ります。 `Delete` のすべての呼び出しが成功した場合、トランザクションはコミットされます。 このメソッドを `ProductsBLL` クラスに追加します。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample5.vb)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>複数の Tableadapter にまたがるトランザクションの適用

このチュートリアルで調べるトランザクション関連のコードでは、`ProductsTableAdapter` に対する複数のステートメントをアトミック操作として扱うことができます。 しかし、異なるデータベーステーブルに対して複数の変更をアトミックに実行する必要がある場合はどうでしょうか。 たとえば、カテゴリを削除するときに、最初に現在の製品を他のカテゴリに再割り当てすることが必要になる場合があります。 これらの2つの手順では、製品を再割り当てし、カテゴリを削除して、分割不可能な操作として実行する必要があります。 ただし `ProductsTableAdapter` には `Products` テーブルを変更するためのメソッドのみが含まれており、`CategoriesTableAdapter` には `Categories` テーブルを変更するためのメソッドのみが含まれています。 では、トランザクションに両方の Tableadapter を含めるにはどうすればよいでしょうか。

1つの方法として、`DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` という名前の `CategoriesTableAdapter` にメソッドを追加し、そのメソッドで、製品を再割り当てして、ストアドプロシージャ内で定義されたトランザクションのスコープ内のカテゴリを削除するストアドプロシージャを呼び出すことができます。 この後のチュートリアルでは、ストアドプロシージャでトランザクションを開始、コミット、およびロールバックする方法について説明します。

別の方法として、`DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` メソッドを含む、DAL にヘルパークラスを作成することもできます。 このメソッドは、`CategoriesTableAdapter` と `ProductsTableAdapter` のインスタンスを作成し、これらの2つの Tableadapter `Connection` プロパティを同じ `SqlConnection` インスタンスに設定します。 その時点で、2つの Tableadapter のいずれかが `BeginTransaction`の呼び出しでトランザクションを開始します。 製品を再割り当てし、カテゴリを削除する Tableadapter メソッドは、必要に応じてトランザクションがコミットまたはロールバックされた `Try...Catch` ブロックで呼び出されます。

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>手順 4: ビジネスロジック層に`UpdateWithTransaction`メソッドを追加する

手順3では、DAL の `ProductsTableAdapter` に `UpdateWithTransaction` メソッドを追加しました。 BLL に対応するメソッドを追加する必要があります。 プレゼンテーション層は DAL に直接呼び出して `UpdateWithTransaction` メソッドを呼び出すことができますが、これらのチュートリアルでは、プレゼンテーション層から DAL を分離するレイヤーアーキテクチャを定義する strived があります。 そのため、この方法を behooves してください。

`ProductsBLL` クラスファイルを開き、対応する DAL メソッドを単に呼び出す `UpdateWithTransaction` という名前のメソッドを追加します。 `ProductsBLL`: `UpdateWithTransaction`に2つの新しいメソッドが追加されました。これは、手順 3. で追加した `DeleteProductsWithTransaction`です。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample6.vb)]

> [!NOTE]
> これらのメソッドには、ASP.NET pages 分離コードクラスからこれらのメソッドを直接呼び出すため、`ProductsBLL` クラスのほとんどのメソッドに割り当てられた `DataObjectMethodAttribute` 属性は含まれません。 `DataObjectMethodAttribute` を使用して、ObjectDataSource のデータソース構成ウィザードと  タブ (SELECT、UPDATE、INSERT、または DELETE) に表示するメソッドにフラグを設定することを思い出してください。 GridView にはバッチ編集または削除のサポートが組み込まれていないため、コードなしの宣言型の方法を使用するのではなく、プログラムでこれらのメソッドを呼び出す必要があります。

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>手順 5: プレゼンテーション層からデータベースデータをアトミックに更新する

レコードのバッチを更新するときのトランザクションの影響を示すために、では、GridView 内のすべての製品を一覧表示するユーザーインターフェイスを作成し、クリックすると、製品 `CategoryID` 値に再割り当てするボタン Web コントロールを追加します。 具体的には、最初のいくつかの製品に有効な `CategoryID` 値が割り当てられ、他の製品には存在しない `CategoryID` 値が意図的に割り当てられるように、カテゴリの再割り当てが進行します。 `CategoryID` が既存のカテゴリ `CategoryID`と一致しない製品を使用してデータベースを更新しようとすると、外部キー制約違反が発生し、例外が発生します。 この例では、トランザクションを使用すると、外部キー制約違反から発生した例外によって、以前の有効な `CategoryID` 変更がロールバックされます。 ただし、トランザクションを使用しない場合は、初期カテゴリの変更が残ります。

まず、`BatchData` フォルダーの [`Transactions.aspx`] ページを開き、ツールボックスから GridView をデザイナーにドラッグします。 その `ID` を `Products` に設定し、そのスマートタグから `ProductsDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLL` クラス s `GetProducts` メソッドからデータをプルするように ObjectDataSource を構成します。 これは読み取り専用の GridView であるため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定し、[完了] をクリックします。

[製品の Bll クラス s GetProducts メソッドを使用するように ObjectDataSource を構成 ![には](wrapping-database-modifications-within-a-transaction-vb/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image3.png)

**図 5**: `ProductsBLL` クラス s `GetProducts` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](wrapping-database-modifications-within-a-transaction-vb/_static/image4.png))

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](wrapping-database-modifications-within-a-transaction-vb/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image5.png)

**図 6**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズの画像を表示する](wrapping-database-modifications-within-a-transaction-vb/_static/image6.png))

データソースの構成ウィザードを完了すると、Visual Studio によって、連結されたフィールドと製品データフィールドの CheckBoxField が作成されます。 `ProductID`、`ProductName`、`CategoryID`、および `CategoryName` を除くすべてのフィールドを削除し、`ProductName` プロパティと `CategoryName` BoundFields をそれぞれ Product および Category に変更します。`HeaderText` スマートタグから、[ページングを有効にする] オプションをオンにします。 これらの変更を行った後、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample7.aspx)]

次に、GridView の上に3つのボタン Web コントロールを追加します。 最初のボタン s Text プロパティを [更新グリッド] に設定し、2番目のを [カテゴリの変更] (トランザクションあり) に設定し、3つ目の [s] をクリックしてカテゴリを変更します (トランザクションなし)。

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample8.aspx)]

この時点で、Visual Studio のデザインビューは、図7に示すスクリーンショットのようになります。

[ページに GridView と3つのボタン Web コントロールが含まれている ![](wrapping-database-modifications-within-a-transaction-vb/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image7.png)

**図 7**: ページに GridView と3つのボタンの Web コントロールが含まれている ([クリックしてフルサイズのイメージを表示する](wrapping-database-modifications-within-a-transaction-vb/_static/image8.png))

3つのボタン `Click` イベントのそれぞれに対してイベントハンドラーを作成し、次のコードを使用します。

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample9.vb)]

更新ボタン s `Click` イベントハンドラーは、`Products` GridView s `DataBind` メソッドを呼び出すことによって、単にデータを GridView に再バインドします。

2番目のイベントハンドラーは、製品 `CategoryID` s を再割り当てし、BLL の新しいトランザクションメソッドを使用して、トランザクションのすべてのデータベースの更新を実行します。 各製品 `CategoryID` は、`ProductID`と同じ値に設定されることに注意してください。 これは、最初のいくつかの製品に対しては正常に機能します。これらの製品には、有効な `CategoryID` s にマップするために `ProductID` 値があるためです。 しかし `ProductID` s が大きくなりすぎた場合、`ProductID` s と `CategoryID` s の重複は適用されなくなります。

3番目の `Click` イベントハンドラーは、同じ方法で製品 `CategoryID` を更新しますが、`ProductsTableAdapter` s default `Update` メソッドを使用してデータベースに更新を送信します。 この `Update` メソッドは、トランザクション内の一連のコマンドをラップするのではなく、最初に検出された外部キー制約違反エラーが発生する前に、これらの変更が行われます。

この動作を説明するには、ブラウザーを使用してこのページにアクセスします。 最初に、図8に示すように、データの最初のページが表示されます。 次に、[カテゴリの変更 (トランザクションあり)] ボタンをクリックします。 これにより、ポストバックが発生し、すべての製品 `CategoryID` 値を更新しようとしますが、外部キー制約違反が発生します (図9を参照)。

[ページング可能な GridView に製品が表示される ![](wrapping-database-modifications-within-a-transaction-vb/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image9.png)

**図 8**: 製品がページング可能な GridView で表示される ([クリックすると、フルサイズの画像が表示](wrapping-database-modifications-within-a-transaction-vb/_static/image10.png)されます)

[カテゴリを再割り当て ![と、外部キー制約違反になります](wrapping-database-modifications-within-a-transaction-vb/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image11.png)

**図 9**: カテゴリを再割り当てすると外部キー制約違反が発生する ([クリックすると、フルサイズの画像が表示](wrapping-database-modifications-within-a-transaction-vb/_static/image12.png)されます)

ここで、ブラウザーの [戻る] ボタンをクリックし、[更新] グリッドボタンをクリックします。 データを更新すると、図8に示すようにまったく同じ出力が表示されます。 つまり、`CategoryID` の製品の一部が有効な値に変更され、データベースで更新された場合でも、外部キー制約違反が発生したときにロールバックされました。

次に、[カテゴリの変更 (トランザクションなし)] ボタンをクリックします。 これにより、同じ外部キー制約違反エラーが発生します (図9を参照)。ただし今回は、`CategoryID` 値が有効な値に変更された製品はロールバックされません。 ブラウザーの [戻る] ボタンをクリックすると、[グリッドの更新] ボタンが表示されます。 図10に示すように、最初の8つの製品の `CategoryID` のが再割り当てされています。 たとえば、図8では、変更履歴の `CategoryID` は1になっていましたが、図10では2に再割り当てされています。

[一部の製品では CategoryID 値が更新されていますが、他の製品では ![](wrapping-database-modifications-within-a-transaction-vb/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image13.png)

**図 10**: 一部の製品 `CategoryID` 値が更新されましたが、他の製品は更新されませんでした ([クリックしてフルサイズの画像を表示](wrapping-database-modifications-within-a-transaction-vb/_static/image14.png))

## <a name="summary"></a>まとめ

既定では、TableAdapter のメソッドは、実行されたデータベースステートメントをトランザクションのスコープ内にラップしませんが、わずかな作業で、トランザクションを作成、コミット、およびロールバックするメソッドを追加できます。 このチュートリアルでは、`ProductsTableAdapter` クラスに、`BeginTransaction`、`CommitTransaction`、および `RollbackTransaction`の3つのメソッドを作成しました。 これらのメソッドを `Try...Catch` ブロックと共に使用して、一連のデータ変更ステートメントをアトミックにする方法について説明しました。 具体的には、`ProductsTableAdapter`で `UpdateWithTransaction` メソッドを作成しました。このメソッドは、バッチ更新パターンを使用して、指定された `ProductsDataTable`の行に対して必要な変更を実行します。 また、`DeleteProductsWithTransaction` メソッドを BLL の `ProductsBLL` クラスに追加しました。このクラスは、`ProductID` 値の `List` を入力として受け取り、各 `Delete` に対して DB Direct pattern メソッド `ProductID`を呼び出します。 どちらの方法でも、最初にトランザクションを作成し、次に `Try...Catch` ブロック内でデータ変更ステートメントを実行します。 例外が発生した場合は、トランザクションがロールバックされます。それ以外の場合はコミットされます。

手順 5. では、トランザクションバッチ更新の効果と、トランザクションを使用しないバッチ更新の影響を示しています。 次の3つのチュートリアルでは、このチュートリアルで説明した基礎に基づいて、バッチの更新、削除、挿入を実行するためのユーザーインターフェイスを作成します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [トランザクションを使用したデータベースの一貫性の維持](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [SQL Server ストアドプロシージャでのトランザクションの管理](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [簡単に作成されたトランザクション: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope と Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [.NET での Oracle Database トランザクションの使用](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Dave Gardner、Hilton Giesenow、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](batch-inserting-cs.md)
> [次へ](batch-updating-vb.md)
