---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: 型指定されたデータセットの Tableadapter (C#) の新しいストアドプロシージャの作成Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、コードに SQL ステートメントを作成し、実行するデータベースにステートメントを渡しました。 もう1つの方法として、...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 751282ca-5870-4d66-84e4-6cefae23eb4a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: db0d83a0fd1f1f175001d20844b298be0cf7e1cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74609134"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>型指定された DataSet の TableAdapters に新しいストアド プロシージャを作成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_CS.zip)または[PDF のダウンロード](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial67cs1.pdf)

> 前のチュートリアルでは、コードに SQL ステートメントを作成し、実行するデータベースにステートメントを渡しました。 別の方法としては、ストアドプロシージャを使用する方法があります。ここでは、SQL ステートメントがデータベースで事前に定義されています。 このチュートリアルでは、TableAdapter ウィザードで新しいストアドプロシージャを生成する方法について説明します。

## <a name="introduction"></a>はじめに

これらのチュートリアルのデータアクセス層 (DAL) では、型指定されたデータセットを使用します。 「[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)」チュートリアルで説明したように、型指定されたデータセットは、厳密に型指定された Datatable と tableadapter で構成されます。 Datatable は、システム内の論理エンティティを表し、データアクセスを実行する基になるデータベースとの Tableadapter インターフェイスを使用します。 これには、データを使用した Datatable の読み込み、スカラーデータを返すクエリの実行、およびデータベースからのレコードの挿入、更新、および削除が含まれます。

Tableadapter によって実行される SQL コマンドは、`SELECT columnList FROM TableName`やストアドプロシージャなどのアドホック SQL ステートメントのいずれかになります。 アーキテクチャの Tableadapter では、アドホック SQL ステートメントを使用します。 ただし、多くの開発者やデータベース管理者は、セキュリティ、保守容易性、および更新可能性の理由により、アドホック SQL ステートメントでストアドプロシージャを優先します。 他のユーザーは、柔軟性を高めるためにアドホック SQL ステートメントを優先的に使用します。 独自の作業では、アドホック SQL ステートメントを使用してストアドプロシージャを優先しますが、以前のチュートリアルを簡略化するためにアドホック SQL ステートメントを使用することを選択しました。

Tableadapter を定義するとき、または新しいメソッドを追加する場合、TableAdapter ウィザードを使用すると、アドホック SQL ステートメントを使用するのと同じように、新しいストアドプロシージャを作成したり、既存のストアドプロシージャを使用したりするのが簡単になります。 このチュートリアルでは、TableAdapter ウィザードでストアドプロシージャを自動生成する方法について説明します。 次のチュートリアルでは、既存または手動で作成したストアドプロシージャを使用するように TableAdapter のメソッドを構成する方法について説明します。

> [!NOTE]
> 「渡 Howard のブログエントリ」では、ストアドプロシージャを使用しないことについて説明してい[ます。](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/)また、ストアドプロシージャとアドホック SQL の長所と短所については、「ストアドプロシージャ[が悪い、M kay?](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx) 」を[参照して](https://weblogs.asp.net/fbouma/)ください。

## <a name="stored-procedure-basics"></a>ストアド プロシージャの基本

関数は、すべてのプログラミング言語に共通の構造体です。 関数は、関数が呼び出されたときに実行されるステートメントのコレクションです。 関数は入力パラメーターを受け取り、必要に応じて値を返すことができます。 *[ストアドプロシージャ](http://en.wikipedia.org/wiki/Stored_procedure)* は、プログラミング言語の関数と多くの類似点を共有するデータベース構造です。 ストアドプロシージャは、ストアドプロシージャが呼び出されたときに実行される一連の T-sql ステートメントで構成されます。 ストアドプロシージャは、0個以上の入力パラメーターを受け取ることができ、スカラー値、出力パラメーター、または `SELECT` クエリからの結果セットを返すことができます。

> [!NOTE]
> ストアドプロシージャは、多くの場合、sprocs または Sp と呼ばれます。

ストアドプロシージャは、 [`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) t-sql ステートメントを使用して作成されます。 たとえば、次の T-sql スクリプトは、`@CategoryID` という名前の1つのパラメーターを受け取る `GetProductsByCategoryID` という名前のストアドプロシージャを作成し、`UnitPrice`テーブル内で、一致する `Discontinued` 値を持つ列の `ProductID`、`ProductName`、`Products`、および `CategoryID` の各フィールドを返します。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

このストアドプロシージャを作成した後は、次の構文を使用して呼び出すことができます。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.sql)]

> [!NOTE]
> 次のチュートリアルでは、Visual Studio IDE を使用してストアドプロシージャを作成する方法について説明します。 ただし、このチュートリアルでは、TableAdapter ウィザードによってストアドプロシージャが自動的に生成されるようにします。

ストアドプロシージャは、単にデータを返すだけでなく、1つのトランザクションのスコープ内で複数のデータベースコマンドを実行するためによく使用されます。 たとえば、`DeleteCategory`という名前のストアドプロシージャは、`@CategoryID` パラメーターを使用して、2つの `DELETE` ステートメントを実行します。1つは、関連する製品を削除するステートメント、もう1つは指定したカテゴリを削除するものです。 ストアドプロシージャ内の複数のステートメントは、トランザクション内で自動的にラップされ*ません*。 ストアドプロシージャの複数のコマンドがアトミック操作として扱われるようにするには、追加の T-sql コマンドを発行する必要があります。 以降のチュートリアルでは、ストアドプロシージャのコマンドをトランザクションのスコープ内にラップする方法について説明します。

アーキテクチャ内でストアドプロシージャを使用する場合、データアクセス層のメソッドは、アドホック SQL ステートメントを発行するのではなく、特定のストアドプロシージャを呼び出します。 これにより、(データベース上で) 実行される SQL ステートメントの場所を、アプリケーションのアーキテクチャ内で定義するのではなく、一元化できます。 このような集中化により、クエリの検索、分析、およびチューニングが容易になり、データベースの使用場所や方法によりわかりやすい画像が得られます。

ストアドプロシージャの基礎の詳細については、このチュートリアルの最後にある「詳細情報」セクションのリソースを参照してください。

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>手順 1: 高度なデータアクセス層シナリオの Web ページを作成する

ストアドプロシージャを使用した DAL の作成に関する説明を開始する前に、まず、web サイトプロジェクトの ASP.NET ページを作成してみましょう。このページでは、次のいくつかのチュートリアルに必要となります。 まず、`AdvancedDAL`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![高度なデータアクセス層シナリオのチュートリアルの ASP.NET ページを追加する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**図 1**: 高度なデータアクセス層シナリオのチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`AdvancedDAL` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png)されます)

最後に、これらのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、バッチ処理されたデータ `<siteMapNode>`を操作した後に、次のマークアップを追加します。

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、高度な DAL シナリオのチュートリアルの項目が含まれるようになりました。

![サイトマップに、高度な DAL シナリオチュートリアルのエントリが含まれるようになりました。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)

**図 3**: サイトマップに、高度な DAL シナリオチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>手順 2: 新しいストアドプロシージャを作成するための TableAdapter の構成

アドホック SQL ステートメントの代わりにストアドプロシージャを使用するデータアクセス層を作成する方法については、「`NorthwindWithSprocs.xsd`」という名前の `~/App_Code/DAL` フォルダーに新しい型指定されたデータセットを作成します。 このプロセスの詳細については、前のチュートリアルで説明したので、次の手順に進みます。 型指定されたデータセットの作成と構成の詳細な手順については、「[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)」チュートリアルを参照してください。

新しいデータセットをプロジェクトに追加するには、[`DAL`] フォルダーを右クリックし、[新しい項目の追加] を選択して、図4に示すようにデータセットテンプレートを選択します。

[新しい型指定されたデータセットを NorthwindWithSprocs という名前のプロジェクトに追加 ![ます。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png)

**図 4**: `NorthwindWithSprocs.xsd` という名前のプロジェクトに新しい型指定されたデータセットを追加する ([クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)されます)

これにより、新しい型指定されたデータセットが作成され、デザイナーが開き、新しい TableAdapter が作成され、TableAdapter 構成ウィザードが起動します。 TableAdapter 構成ウィザードの最初のステップでは、使用するデータベースを選択するように求められます。 Northwind データベースへの接続文字列がドロップダウンリストに表示されます。 これを選択し、[次へ] をクリックします。

次の画面では、TableAdapter がデータベースにアクセスする方法を選択できます。 前のチュートリアルでは、最初のオプションである [SQL ステートメントを使用] を選択しました。 このチュートリアルでは、2番目のオプション [新しいストアドプロシージャの作成] を選択し、[次へ] をクリックします。

[新しいストアドプロシージャを作成するように TableAdapter に指示 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png)

**図 5**: TableAdapter に新しいストアドプロシージャを作成するように指示する ([クリックしてフルサイズのイメージを表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png))

アドホック SQL ステートメントを使用する場合と同様に、次の手順では、TableAdapter のメインクエリに `SELECT` ステートメントを指定するように求められます。 ただし、ここで入力した `SELECT` ステートメントを使用してアドホッククエリを直接実行する代わりに、TableAdapter s ウィザードによって、この `SELECT` クエリを含むストアドプロシージャが作成されます。

この TableAdapter には、次の `SELECT` クエリを使用します。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

[SELECT クエリを入力 ![には](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png)

**図 6**: `SELECT` クエリを入力[する (クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)されます)

> [!NOTE]
> 上記のクエリは、`Northwind` 型指定されたデータセットの `ProductsTableAdapter` のメインクエリと若干異なります。 `Northwind` 型指定されたデータセットの `ProductsTableAdapter` には、各製品カテゴリおよび仕入先のカテゴリ名と会社名を返すための2つの相関サブクエリが含まれていることを思い出してください。 後の「 [join を使用するように TableAdapter を更新する](updating-the-tableadapter-to-use-joins-cs.md)」チュートリアルでは、この関連データをこの tableadapter に追加する方法について説明します。

[詳細オプション] ボタンをクリックします。 ここから、ウィザードで TableAdapter の insert、update、および delete の各ステートメントを生成するかどうか、オプティミスティック同時実行制御を使用するかどうか、および挿入と更新後にデータテーブルを更新するかどうかを指定できます。 既定では、[Insert、Update、および Delete ステートメントを生成する] オプションがオンになっています。 このチェックボックスはオンのままにします。 このチュートリアルでは、[オプティミスティック同時実行制御を使用する] オプションをオフのままにします。

TableAdapter ウィザードによってストアドプロシージャが自動的に作成された場合、[データテーブルの更新] オプションは無視されます。 このチェックボックスがオンになっているかどうかにかかわらず、結果の insert および update ストアドプロシージャは、挿入または更新されたレコードだけを取得します。手順 3. で説明します。

![[Insert、Update、および Delete ステートメントの生成] オプションをオンのままにします。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png)

**図 7**: [Insert、Update、および Delete ステートメントの生成] オプションをオンにしたままにする

> [!NOTE]
> [オプティミスティック同時実行制御を使用する] チェックボックスをオンにすると、他のフィールドに変更があった場合にデータが更新されないようにするための条件が `WHERE` 句に追加されます。 TableAdapter の組み込みのオプティミスティック同時実行制御機能の使用方法の詳細については、「[オプティミスティック同時実行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md)制御の実装」を参照してください。

`SELECT` クエリを入力し、[Insert、Update、および Delete ステートメントの生成] オプションがオンになっていることを確認したら、[次へ] をクリックします。 図8に示す次の画面では、データの選択、挿入、更新、および削除のためにウィザードで作成されるストアドプロシージャの名前を入力するように求められます。 これらのストアドプロシージャ名を `Products_Select`、`Products_Insert`、`Products_Update`、および `Products_Delete`に変更します。

[ストアドプロシージャの名前を変更 ![には](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**図 8**: ストアドプロシージャの名前[を変更する (クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png)されます)

TableAdapter ウィザードで4つのストアドプロシージャを作成するために使用する T-sql を確認するには、[SQL スクリプトのプレビュー] ボタンをクリックします。 [SQL スクリプトのプレビュー] ダイアログボックスから、スクリプトをファイルに保存したり、クリップボードにコピーしたりすることができます。

![ストアドプロシージャの生成に使用する SQL スクリプトのプレビュー](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**図 9**: ストアドプロシージャの生成に使用する SQL スクリプトをプレビューする

ストアドプロシージャに名前を付けた後、[次へ] をクリックして、対応するメソッドに名前を付けます。 アドホック SQL ステートメントを使用する場合と同様に、既存の DataTable にデータを格納したり、新しい DataTable を返したりするメソッドを作成できます。 また、TableAdapter にレコードの挿入、更新、および削除のための DB ダイレクトパターンを含めるかどうかも指定できます。 この3つのチェックボックスはすべてオンのままにしますが、DataTable メソッドの戻り値を `GetProducts` に変更します (図10を参照)。

[メソッドの ![名前と GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)

**図 10**: メソッドに `Fill` と `GetProducts` の名前を指定[する (クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png)されます)

[次へ] をクリックして、ウィザードが実行する手順の概要を表示します。 [完了] ボタンをクリックしてウィザードを完了します。 ウィザードが完了すると、データセットデザイナーに戻ります。これには、`ProductsDataTable`が含まれています。

[データセットデザイナーに新しく追加された製品 Datatable が表示される ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)

**図 11**: データセットデザイナーに新しく追加された `ProductsDataTable` が表示される ([クリックしてフルサイズのイメージを表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png))

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>手順 3: 新しく作成したストアドプロシージャを調べる

手順 2. で使用した TableAdapter ウィザードでは、データの選択、挿入、更新、および削除のためのストアドプロシージャが自動的に作成されました。 これらのストアドプロシージャは、Visual Studio を使用して表示または変更できます。そのためには、サーバーエクスプローラーに移動し、database s ストアドプロシージャフォルダーにドリルダウンします。 図12に示すように、Northwind データベースには、`Products_Delete`、`Products_Insert`、`Products_Select`、および `Products_Update`の4つの新しいストアドプロシージャが含まれています。

![手順 2. で作成した4つのストアドプロシージャは、データベースの [ストアドプロシージャ] フォルダーにあります。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)

**図 12**: 手順 2. で作成した4つのストアドプロシージャは、データベースの [ストアドプロシージャ] フォルダーにあります。

> [!NOTE]
> サーバーエクスプローラーが表示されない場合は、[表示] メニューの [サーバーエクスプローラー] オプションを選択します。 手順 2. で追加した製品関連のストアドプロシージャが表示されない場合は、[ストアドプロシージャ] フォルダーを右クリックし、[最新の状態に更新] をクリックします。

ストアドプロシージャを表示または変更するには、サーバーエクスプローラーで名前をダブルクリックするか、またはストアドプロシージャを右クリックして [開く] を選択します。 図13は、`Products_Delete` ストアドプロシージャを開いた場合を示しています。

[![ストアドプロシージャは、Visual Studio 内から開いたり変更したりできます。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png)

**図 13**: Visual Studio 内からストアドプロシージャを開いたり変更したりする ([クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)されます)

`Products_Delete` ストアドプロシージャと `Products_Select` ストアドプロシージャの内容は、非常に簡単です。 一方、`Products_Insert` および `Products_Update` のストアドプロシージャは、`INSERT` および `UPDATE` ステートメントの後に `SELECT` ステートメントを実行するため、より詳しく調査することを保証します。 たとえば、次の SQL は `Products_Insert` ストアドプロシージャを構成します。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

このストアドプロシージャは、TableAdapter s ウィザードで指定された `SELECT` クエリによって返された列 `Products` を入力パラメーターとして受け取り、これらの値を `INSERT` ステートメントで使用します。 `INSERT` ステートメントの後に、`SELECT` クエリを使用して、新しく追加されたレコードの `Products` 列の値 (`ProductID`を含む) が返されます。 この更新機能は、バッチ更新パターンを使用して新しいレコードを追加するときに役立ちます。新しく追加された `ProductRow` インスタンス `ProductID` プロパティには、データベースによって割り当てられた自動インクリメント値が自動的に更新されるためです。

次のコードは、この機能を示しています。 これには、`NorthwindWithSprocs` 型指定されたデータセット用に作成された `ProductsTableAdapter` と `ProductsDataTable` が含まれています。 新しい製品をデータベースに追加するには、`ProductsRow` インスタンスを作成し、その値を指定し、TableAdapter s `Update` メソッドを呼び出して `ProductsDataTable`を渡します。 内部的には、TableAdapter s `Update` メソッドは、渡された DataTable の `ProductsRow` インスタンスを列挙し (この例では、追加したもののみが存在します)、適切な insert、update、または delete コマンドを実行します。 この場合、`Products_Insert` ストアドプロシージャが実行され、`Products` テーブルに新しいレコードが追加され、新しく追加されたレコードの詳細が返されます。 その後、`ProductsRow` instance s `ProductID` の値が更新されます。 `Update` メソッドが完了したら、`ProductsRow` s `ProductID` プロパティを使用して、新しく追加したレコード s `ProductID` 値にアクセスできます。

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.cs)]

同様に `Products_Update` ストアドプロシージャには、その `UPDATE` ステートメントの後に `SELECT` ステートメントが含まれます。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample7.sql)]

このストアドプロシージャには `ProductID`の2つの入力パラメーターが含まれていることに注意してください: `@Original_ProductID` と `@ProductID`。 この機能により、主キーが変更される可能性があるシナリオが可能になります。 たとえば、employee データベースでは、各従業員レコードで、従業員の社会保障番号が主キーとして使用される場合があります。 既存の従業員の社会保障番号を変更するには、新しい社会保障番号と元の社会保障番号の両方を指定する必要があります。 `Products` テーブルの場合、`ProductID` 列は `IDENTITY` 列であり、変更することはできないため、このような機能は必要ありません。 実際、`Products_Update` ストアドプロシージャの `UPDATE` ステートメントには、列リストに `ProductID` 列が含まれていません。 したがって、`UPDATE` statement s `WHERE` 句で `@Original_ProductID` が使用されている間は、`Products` テーブルでは不要であり、`@ProductID` パラメーターで置き換えることができます。 ストアドプロシージャのパラメーターを変更する場合は、そのストアドプロシージャを使用する TableAdapter メソッドも更新することが重要です。

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>手順 4: ストアドプロシージャのパラメーターを変更し、TableAdapter を更新する

`@Original_ProductID` パラメーターは余分なので、s を使用して `Products_Update` ストアドプロシージャから完全に削除します。 `Products_Update` ストアドプロシージャを開き、`@Original_ProductID` パラメーターを削除します。 `UPDATE` ステートメントの `WHERE` 句で、`@Original_ProductID` から使用されているパラメーター名を `@ProductID`に変更します。 これらの変更を行った後、ストアドプロシージャ内の T-sql は次のようになります。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample8.sql)]

これらの変更をデータベースに保存するには、ツールバーの [保存] アイコンをクリックするか、Ctrl + S キーを押します。 この時点で、`Products_Update` ストアドプロシージャでは `@Original_ProductID` 入力パラメーターは想定されていませんが、TableAdapter はこのようなパラメーターを渡すように構成されています。 データセットデザイナーで TableAdapter を選択し、プロパティウィンドウに移動し、`UpdateCommand` s `Parameters` コレクション内の省略記号をクリックすることで、TableAdapter が `Products_Update` ストアドプロシージャに送信するパラメーターを確認できます。 これにより、図14に示す [パラメーターコレクションエディター] ダイアログボックスが表示されます。

![Parameters コレクションエディターには、Products_Update ストアドプロシージャに渡されたパラメーターが一覧表示されます。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png)

**図 14**: Parameters コレクションエディターには、`Products_Update` ストアドプロシージャに渡されたパラメーターの一覧が表示されます。

このパラメーターは、メンバーの一覧から `@Original_ProductID` パラメーターを選択し、[削除] ボタンをクリックするだけで削除できます。

または、デザイナーで TableAdapter を右クリックし、[構成] を選択して、すべてのメソッドで使用されるパラメーターを更新することもできます。 これにより、TableAdapter 構成ウィザードが表示され、ストアドプロシージャが受け取る必要があるパラメーターと共に、選択、挿入、更新、および削除に使用されるストアドプロシージャが一覧表示されます。 [更新] ドロップダウンリストをクリックすると、`Products_Update` ストアドプロシージャに必要な入力パラメーターが表示されます。このパラメーターには、`@Original_ProductID` が含まれなくなりました (図15を参照)。 [完了] をクリックするだけで、TableAdapter によって使用されるパラメーターコレクションが自動的に更新されます。

[![、または TableAdapter の構成ウィザードを使用して、そのメソッドのパラメーターコレクションを更新することもできます。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**図 15**: または、TableAdapter の構成ウィザードを使用してメソッドのパラメーターコレクションを更新することもできます ([クリックすると、フルサイズのイメージが表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png)されます)。

## <a name="step-5-adding-additional-tableadapter-methods"></a>手順 5: TableAdapter メソッドの追加

手順2で説明したように、新しい TableAdapter を作成する場合は、対応するストアドプロシージャを自動的に生成するのが簡単です。 TableAdapter にメソッドを追加する場合も同様です。 これを説明するために、「」では、手順 2. で作成した `ProductsTableAdapter` に `GetProductByProductID(productID)` メソッドを追加します。 このメソッドは、`ProductID` 値を入力として受け取り、指定された製品の詳細を返します。

まず、TableAdapter を右クリックし、コンテキストメニューの [クエリの追加] を選択します。

![新しいクエリを TableAdapter に追加する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**図 16**: TableAdapter に新しいクエリを追加する

これにより、tableadapter クエリの構成ウィザードが開始されます。このウィザードでは、まず TableAdapter がデータベースにアクセスする方法を確認するプロンプトが表示されます。 新しいストアドプロシージャを作成するには、[新しいストアドプロシージャを作成する] オプションを選択し、[次へ] をクリックします。

[![[新しいストアドプロシージャを作成する] オプションを選択する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)

**図 17**: [新しいストアドプロシージャを作成する] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png)されます)

次の画面では、実行するクエリの種類、一連の行または単一のスカラー値を返すかどうか、`UPDATE`、`INSERT`、または `DELETE` ステートメントを実行するかどうかを確認するプロンプトが表示されます。 `GetProductByProductID(productID)` メソッドでは行が返されるため、[行を返す] オプションを選択したままにして [次へ] をクリックします。

[![[行を返す] オプションを選択します。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)

**図 18**: [行を返す] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)されます)

次の画面には、TableAdapter のメインクエリが表示されます。このクエリには、ストアドプロシージャの名前 (`dbo.Products_Select`) だけが表示されます。 ストアドプロシージャ名を次の `SELECT` ステートメントに置き換えます。これにより、指定した製品のすべての product フィールドが返されます。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample9.sql)]

[ストアドプロシージャ名を SELECT クエリに置き換える ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)

**図 19**: ストアドプロシージャ名を `SELECT` クエリに置き換える ([クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)されます)

次の画面では、作成されるストアドプロシージャに名前を指定するように求められます。 `Products_SelectByProductID` 名を入力し、[次へ] をクリックします。

[新しいストアドプロシージャの名前を ![Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**図 20**: 新しいストアドプロシージャの名前を `Products_SelectByProductID`[にする (クリックしてフルサイズの画像を表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image46.png))

ウィザードの最後の手順では、生成されたメソッド名を変更すると共に、DataTable パターンを使用するか、DataTable パターンを返すか、またはその両方を使用するかを示すことができます。 このメソッドでは、両方のオプションをオンのままにして、メソッドの名前を `FillByProductID` に変更し、`GetProductByProductID`します。 [次へ] をクリックして、ウィザードが実行する手順の概要を表示し、[完了] をクリックしてウィザードを完了します。

[TableAdapter のメソッドの名前を FillByProductID および GetProductByProductID に変更 ![には](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image47.png)

**図 21**: TableAdapter のメソッドの名前を `FillByProductID` と `GetProductByProductID` に変更する ([クリックしてフルサイズのイメージを表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image49.png))

ウィザードを完了すると、新しいメソッドが使用できる `GetProductByProductID(productID)` ようになります。このメソッドを呼び出すと、先ほど作成した `Products_SelectByProductID` ストアドプロシージャが実行されます。 この新しいストアドプロシージャをサーバーエクスプローラーから表示するには、[ストアドプロシージャ] フォルダーにドリルダウンして `Products_SelectByProductID` を開いてください (表示されない場合は、[ストアドプロシージャ] フォルダーを右クリックして [最新の状態に更新] をクリックします)。

`SelectByProductID` ストアドプロシージャは入力パラメーターとして `@ProductID` を受け取り、ウィザードで入力した `SELECT` ステートメントを実行します。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>手順 6: ビジネスロジック層クラスの作成

チュートリアルシリーズ全体を通じて、プレゼンテーション層がビジネスロジック層 (BLL) へのすべての呼び出しを行ったレイヤーアーキテクチャを維持することを strived ました。 この設計上の決定に従うためには、まず、新しい型指定されたデータセットの BLL クラスを作成してから、プレゼンテーション層から製品データにアクセスできるようにする必要があります。

`~/App_Code/BLL` フォルダーに `ProductsBLLWithSprocs.cs` という名前の新しいクラスファイルを作成し、次のコードを追加します。

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample11.cs)]

このクラスは、前のチュートリアルで `ProductsBLL` クラスセマンティクスを模倣していますが、`NorthwindWithSprocs` データセットの `ProductsTableAdapter` と `ProductsDataTable` オブジェクトを使用しています。 たとえば、`ProductsBLL` のようにクラスファイルの先頭に `using NorthwindTableAdapters` ステートメントを記述するのではなく、`ProductsBLLWithSprocs` クラスは `using NorthwindWithSprocsTableAdapters`を使用します。 同様に、このクラスで使用される `ProductsDataTable` および `ProductsRow` のオブジェクトには、`NorthwindWithSprocs` 名前空間がプレフィックスとして付けられます。 `ProductsBLLWithSprocs` クラスには、`GetProducts` と `GetProductByProductID`の2つのデータアクセスメソッドと、1つの製品インスタンスを追加、更新、および削除するためのメソッドが用意されています。

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>手順 7: プレゼンテーション層からの`NorthwindWithSprocs`データセットの操作

この時点で、ストアドプロシージャを使用して基になるデータベースデータにアクセスし、変更する DAL が作成されました。 また、製品を追加、更新、削除するためのメソッドと共に、すべての製品または特定の製品を取得するメソッドを含む基本的な BLL も作成しました。 このチュートリアルを終了するには、`ProductsBLLWithSprocs` クラスを使用してレコードの表示、更新、および削除を行う ASP.NET ページを作成します。

`AdvancedDAL` フォルダーの [`NewSprocs.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグして、`Products`という名前を付けます。 GridView s スマートタグから、`ProductsDataSource`という名前の新しい ObjectDataSource にバインドすることを選択します。 図22に示すように、`ProductsBLLWithSprocs` クラスを使用するように ObjectDataSource を構成します。

[製品 Bllwithsproc クラスを使用するように ObjectDataSource を構成 ![には](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image50.png)

**図 22**: `ProductsBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image52.png))

[選択] タブのドロップダウンリストには、`GetProducts` と `GetProductByProductID`の2つのオプションがあります。 GridView 内のすべての製品を表示するため、`GetProducts` 方法を選択します。 [更新]、[挿入]、[削除] の各タブのドロップダウンリストには、それぞれ1つのメソッドがあります。 これらの各ドロップダウンリストに適切なメソッドが選択されていることを確認し、[完了] をクリックします。

ObjectDataSource ウィザードが完了すると、Visual Studio によって、BoundFields と CheckBoxField が製品データフィールドの GridView に追加されます。 [編集を有効にする] チェックボックスをオンにして、組み込みの編集および削除機能をオンにします。

[編集と削除のサポートが有効になっている GridView がページに含まれて ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image53.png)

**図 23**: 編集および削除のサポートが有効になっている GridView がページに含まれている ([クリックしてフルサイズのイメージを表示する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image55.png))

前のチュートリアルで説明したように、ObjectDataSource ウィザードの完了時に、Visual Studio は `OldValuesParameterFormatString` プロパティを元の\_{0}に設定します。 この値は、BLL のメソッドで想定されるパラメーターによってデータ変更機能が適切に機能するために、{0} の既定値に戻す必要があります。 したがって、`OldValuesParameterFormatString` プロパティを {0} に設定するか、宣言構文からプロパティを完全に削除するようにしてください。

データソースの構成ウィザードを完了し、GridView でサポートを編集および削除し、ObjectDataSource s `OldValuesParameterFormatString` プロパティを既定値に戻すと、ページ s の宣言型マークアップは次のようになります。

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample12.aspx)]

この時点で、編集インターフェイスをカスタマイズして検証を含め、`CategoryID` と `SupplierID` 列を DropDownLists として表示することで、GridView を整理できます。 また、[削除] ボタンにクライアント側の確認を追加することもできます。このような拡張機能を実装することをお勧めします。 これらのトピックについては前のチュートリアルで説明したため、ここでは説明しません。

GridView を拡張するかどうかに関係なく、ページ s のコア機能をブラウザーでテストします。 図24に示すように、行ごとの編集と削除の機能を提供する GridView の製品がページに一覧表示されます。

[GridView から製品を表示、編集、および削除できる ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image56.png)

**図 24**: GridView で製品を表示、編集、および削除できる ([クリックすると、フルサイズの画像が表示](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image58.png)されます)

## <a name="summary"></a>要約

型指定されたデータセット内の Tableadapter は、アドホック SQL ステートメントまたはストアドプロシージャを使用して、データベースのデータにアクセスできます。 ストアドプロシージャを使用する場合は、既存のストアドプロシージャを使用するか、または `SELECT` クエリに基づいて新しいストアドプロシージャを作成するように TableAdapter ウィザードを指定することができます。 このチュートリアルでは、ストアドプロシージャを自動的に作成する方法について説明しました。

ストアドプロシージャが自動生成されると時間が節約されますが、ウィザードによって作成されたストアドプロシージャは、独自に作成したものとは一致しない場合があります。 1つの例として、`Products_Update` ストアドプロシージャがあります。これは、`@Original_ProductID` パラメーターが不要な場合でも、`@Original_ProductID` と `@ProductID` 入力パラメーターの両方を必要とします。

多くのシナリオでは、ストアドプロシージャが既に作成されている場合や、ストアドプロシージャのコマンドをより細かく制御できるように手動でビルドする場合があります。 どちらの場合も、メソッドに既存のストアドプロシージャを使用するように TableAdapter に指示します。 次のチュートリアルで、これを実現する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ストアドプロシージャの作成と保守](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [ストアドプロシージャからスカラーデータを取得する](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [ストアドプロシージャの基本 SQL Server](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [ストアドプロシージャ: 概要](http://www.sqlteam.com/item.asp?ItemID=563)
- [ストアドプロシージャの作成](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Geisenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [次へ](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
