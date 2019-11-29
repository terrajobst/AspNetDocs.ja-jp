---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: 型指定されたデータセットの Tableadapter (C#) に対する既存のストアドプロシージャの使用Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、TableAdapter ウィザードを使用して新しいストアドプロシージャを生成する方法を学習しました。 このチュートリアルでは、同じ TableAdapter について説明します。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 440bef2a-1641-4238-99e3-8e2d44e7d94c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: cfe03c244fb6f9f0a201aecb6eae211ab946175f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74603831"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>型指定された DataSet の TableAdapters に既存のストアド プロシージャを使用する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_CS.zip)または[PDF のダウンロード](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial68cs1.pdf)

> 前のチュートリアルでは、TableAdapter ウィザードを使用して新しいストアドプロシージャを生成する方法を学習しました。 このチュートリアルでは、既存のストアドプロシージャで同じ TableAdapter ウィザードを使用する方法について説明します。 また、データベースに新しいストアドプロシージャを手動で追加する方法についても説明します。

## <a name="introduction"></a>はじめに

前の[チュートリアル](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)では、アドホック SQL ステートメントではなく、ストアドプロシージャを使用してデータにアクセスするように、型指定されたデータセットの tableadapter を構成する方法を説明しました。 特に、TableAdapter ウィザードでこれらのストアドプロシージャを自動的に作成する方法を調べました。 レガシアプリケーションを ASP.NET 2.0 に移植する場合、または既存のデータモデルに対して ASP.NET 2.0 web サイトを構築する場合は、必要なストアドプロシージャがデータベースに既に含まれている可能性があります。 または、手動で、またはストアドプロシージャを自動生成する TableAdapter ウィザード以外の何らかのツールを使用して、ストアドプロシージャを作成することもできます。

このチュートリアルでは、既存のストアドプロシージャを使用するように TableAdapter を構成する方法について説明します。 Northwind データベースには、いくつかの組み込みストアドプロシージャが含まれているだけであるため、Visual Studio 環境を使用してデータベースに新しいストアドプロシージャを手動で追加するために必要な手順についても説明します。 始めましょう!

> [!NOTE]
> 「[トランザクション内でのデータベース変更のラッピング](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)」チュートリアルでは、トランザクション (`BeginTransaction`、`CommitTransaction`など) をサポートするメソッドを TableAdapter に追加しました。 また、トランザクションをストアドプロシージャ内で完全に管理することもできます。この場合、データアクセスレイヤーコードを変更する必要はありません。 このチュートリアルでは、トランザクションのスコープ内でストアドプロシージャ s ステートメントを実行するために使用される T-sql コマンドについて説明します。

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>手順 1: Northwind データベースへのストアドプロシージャの追加

Visual Studio を使用すると、データベースに新しいストアドプロシージャを簡単に追加できます。 「」では、Northwind データベースに新しいストアドプロシージャを追加します。これにより、特定の `CategoryID` 値を持つ列の `Products` テーブルからすべての列が返されます。 [サーバーエクスプローラー] ウィンドウで Northwind データベースを展開し、そのフォルダー (データベースダイアグラム、テーブル、ビューなど) が表示されるようにします。 前のチュートリアルで見たように、[ストアドプロシージャ] フォルダーには、データベースの既存のストアドプロシージャが含まれています。 新しいストアドプロシージャを追加するには、[ストアドプロシージャ] フォルダーを右クリックし、ショートカットメニューの [新しいストアドプロシージャの追加] オプションを選択します。

[![[ストアドプロシージャ] フォルダーを右クリックし、新しいストアドプロシージャを追加します。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**図 1**: [ストアドプロシージャ] フォルダーを右クリックして新しいストアドプロシージャを追加[する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png)されます)

図1に示すように、[新しいストアドプロシージャの追加] オプションを選択すると、Visual Studio のスクリプトウィンドウが開き、ストアドプロシージャの作成に必要な SQL スクリプトのアウトラインが表示されます。 このスクリプトを具体化して実行します。この時点で、ストアドプロシージャがデータベースに追加されます。

次のスクリプトを入力します。

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

このスクリプトを実行すると、`Products_SelectByCategoryID`という名前の Northwind データベースに新しいストアドプロシージャが追加されます。 このストアドプロシージャは、1つの入力パラメーター (`int`型の`@CategoryID`) を受け取り、一致する `CategoryID` 値を持つこれらの製品のすべてのフィールドを返します。

この `CREATE PROCEDURE` スクリプトを実行してストアドプロシージャをデータベースに追加するには、ツールバーの [保存] アイコンをクリックするか、Ctrl + S キーを押します。 この操作を実行すると、ストアドプロシージャフォルダーが更新され、新しく作成されたストアドプロシージャが表示されます。 また、ウィンドウのスクリプトによって、はらみが `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` から `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`に変更されます。 `CREATE PROCEDURE` によってデータベースに新しいストアドプロシージャが追加され、`ALTER PROCEDURE` は既存のプロシージャを更新します。 スクリプトの開始が `ALTER PROCEDURE`に変更されたため、ストアドプロシージャの入力パラメーターまたは SQL ステートメントを変更し、[保存] アイコンをクリックすると、ストアドプロシージャが変更されて更新されます。

図2は、`Products_SelectByCategoryID` ストアドプロシージャが保存された後の Visual Studio を示しています。

[ストアドプロシージャ Products_SelectByCategoryID がデータベースに追加された ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png)

**図 2**: ストアドプロシージャ `Products_SelectByCategoryID` がデータベースに追加されました ([クリックしてフルサイズの画像を表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png))

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>手順 2: 既存のストアドプロシージャを使用するように TableAdapter を構成する

`Products_SelectByCategoryID` ストアドプロシージャがデータベースに追加されたので、メソッドのいずれかが呼び出されたときに、このストアドプロシージャを使用するようにデータアクセス層を構成できます。 特に、先ほど作成した `Products_SelectByCategoryID` ストアドプロシージャを呼び出す `NorthwindWithSprocs` 型指定されたデータセットの `ProductsTableAdapter` に `GetProductsByCategoryID(categoryID)` メソッドを追加します。

まず、`NorthwindWithSprocs` データセットを開きます。 `ProductsTableAdapter` を右クリックし、[クエリの追加] を選択して、TableAdapter クエリの構成ウィザードを起動します。 前の[チュートリアル](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)では、TableAdapter で新しいストアドプロシージャを作成することを選択しました。 ただし、このチュートリアルでは、新しい TableAdapter メソッドを既存の `Products_SelectByCategoryID` ストアドプロシージャに接続する必要があります。 そのため、ウィザードの最初の手順で [既存のストアドプロシージャを使用する] オプションを選択し、[次へ] をクリックします。

[![[既存のストアドプロシージャを使用する] オプションを選択する](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)

**図 3**: [既存のストアドプロシージャを使用する] オプションを選択[する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png)されます)

次の画面には、データベースのストアドプロシージャを含むドロップダウンリストが表示されます。 ストアドプロシージャを選択すると、左側に入力パラメーターが、右側に返されるデータフィールド (存在する場合) が一覧表示されます。 一覧から `Products_SelectByCategoryID` ストアドプロシージャを選択し、[次へ] をクリックします。

[Products_SelectByCategoryID ストアドプロシージャを選択 ![には](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)

**図 4**: `Products_SelectByCategoryID` ストアドプロシージャを選択[する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png)されます)

次の画面では、ストアドプロシージャによって返されるデータの種類を確認します。この回答では、TableAdapter のメソッドによって返される型を決定します。 たとえば、表形式のデータが返されることを示す場合、メソッドは、ストアドプロシージャによって返されたレコードを格納する `ProductsDataTable` インスタンスを返します。 これに対して、このストアドプロシージャが1つの値を返すことを示す場合、TableAdapter は、ストアドプロシージャによって返される最初のレコードの最初の列の値が割り当てられた `object` を返します。

`Products_SelectByCategoryID` ストアドプロシージャは、特定のカテゴリに属するすべての製品を返します。そのため、最初の回答の表形式データを選択し、[次へ] をクリックします。

[ストアドプロシージャが表形式データを返すことを示す ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)

**図 5**: ストアドプロシージャが表形式データを返すことを示します ([クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png)されます)

残っているのは、使用するメソッドパターン、およびこれらのメソッドの名前を示すことだけです。 [DataTable にデータを格納し、DataTable オプションを返す] の両方をオンのままにします。ただし、メソッドの名前を `FillByCategoryID` と `GetProductsByCategoryID`に変更します。 次に、[次へ] をクリックして、ウィザードが実行するタスクの概要を確認します。 すべてが正しい場合は、[完了] をクリックします。

[メソッドに FillByCategoryID と Get製品 Bycategoryid の ![名前を指定します。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**図 6**: メソッドに `FillByCategoryID` と `GetProductsByCategoryID` の名前を指定[する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png)されます)

> [!NOTE]
> 先ほど作成した TableAdapter メソッド `FillByCategoryID` と `GetProductsByCategoryID`では、`int`型の入力パラメーターを想定しています。 この入力パラメーター値は、`@CategoryID` パラメーターを使用してストアドプロシージャに渡されます。 ストアドプロシージャの `Products_SelectByCategory` パラメーターを変更する場合は、これらの TableAdapter メソッドのパラメーターも更新する必要があります。 [前のチュートリアル](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)で説明したように、これは、パラメーターコレクションのパラメーターを手動で追加または削除するか、TableAdapter ウィザードを再実行することによって、次の2つの方法のいずれかで行うことができます。

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>手順 3: BLL に`GetProductsByCategoryID(categoryID)`メソッドを追加する

`GetProductsByCategoryID` DAL メソッドが完了したら、次の手順として、ビジネスロジック層でこのメソッドへのアクセスを提供します。 `ProductsBLLWithSprocs` クラスファイルを開き、次のメソッドを追加します。

[!code-csharp[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.cs)]

この BLL メソッドは、`ProductsTableAdapter` s `GetProductsByCategoryID` メソッドから返された `ProductsDataTable` を返します。 `DataObjectMethodAttribute` 属性は、ObjectDataSource s データソース構成ウィザードによって使用されるメタデータを提供します。 特に、このメソッドは [タブ s の選択] ドロップダウンリストに表示されます。

## <a name="step-4-displaying-products-by-category"></a>手順 4: カテゴリ別の製品の表示

新しく追加された `Products_SelectByCategoryID` ストアドプロシージャ、および対応する DAL および BLL メソッドをテストするには、DropDownList と GridView を含む ASP.NET ページを作成します。 DropDownList には、選択したカテゴリに属する製品が GridView に表示されますが、データベース内のすべてのカテゴリが一覧表示されます。

> [!NOTE]
> 前のチュートリアルでは、DropDownLists を使用してマスター/詳細インターフェイスを作成しました。 このようなマスター/詳細レポートの実装の詳細については、「DropDownList チュートリアルを[使用したマスター/詳細のフィルタリング](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)」を参照してください。

`AdvancedDAL` フォルダーの [`ExistingSprocs.aspx`] ページを開き、[ツールボックス] から [DropDownList] をデザイナーにドラッグします。 DropDownList s `ID` プロパティを `Categories` に設定し、その `AutoPostBack` プロパティを `true`に設定します。 次に、スマートタグから、DropDownList を `CategoriesDataSource`という名前の新しい ObjectDataSource にバインドします。 `CategoriesBLL` クラス s `GetCategories` メソッドからデータを取得するように ObjectDataSource を構成します。 [更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[カテゴリ Bll クラス s GetCategories メソッドからデータを取得 ![には](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**図 7**: `CategoriesBLL` クラス s `GetCategories` メソッドからデータ[を取得する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png)されます)

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png)

**図 8**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズの画像を表示する](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png))

ObjectDataSource ウィザードが完了したら、[`CategoryName` データ] フィールドを表示し、各 `ListItem`の `Value` として [`CategoryID`] フィールドを使用するように DropDownList を構成します。

この時点で、DropDownList および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.aspx)]

次に、GridView をデザイナーにドラッグして、DropDownList の下に配置します。 GridView の `ID` を `ProductsByCategory` に設定し、そのスマートタグから `ProductsByCategoryDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLLWithSprocs` クラスを使用するように `ProductsByCategoryDataSource` ObjectDataSource を構成し、`GetProductsByCategoryID(categoryID)` メソッドを使用してそのデータを取得します。 この GridView はデータの表示にのみ使用されるため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定し、[次へ] をクリックします。

[製品 Bllwithsproc クラスを使用するように ObjectDataSource を構成 ![には](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png)

**図 9**: `ProductsBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png))

[Get$ Bycategoryid (categoryID) メソッドからデータを取得 ![には](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)

**図 10**: `GetProductsByCategoryID(categoryID)` メソッドからデータ[を取得する (クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png)されます)

[選択] タブで選択したメソッドはパラメーターを必要とするため、ウィザードの最後の手順によって、パラメーター s のソースが要求されます。 [パラメーターソース] ドロップダウンリストを [制御] に設定し、[ControlID] ドロップダウンリストから `Categories` コントロールを選択します。 [完了] をクリックしてウィザードを終了します。

[categoryID パラメーターのソースとして [カテゴリ] を使用 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**図 11**: `Categories` DropDownList を `categoryID` パラメーターのソースとして使用する ([クリックしてフルサイズのイメージを表示する](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png))

ObjectDataSource ウィザードを完了すると、Visual Studio によって、各製品データフィールドに対して BoundFields と CheckBoxField が追加されます。 これらのフィールドは、必要に応じて自由にカスタマイズできます。

ブラウザーを使用してページにアクセスします。 ページにアクセスすると、飲み物カテゴリが選択され、対応する製品がグリッドに表示されます。 図12に示すように、ドロップダウンリストを別のカテゴリに変更すると、ポストバックが発生し、グリッドが新しく選択されたカテゴリの製品と共に再読み込みされます。

[[生成] カテゴリの製品 ![表示されます。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**図 12**: [生成] カテゴリの製品が表示される ([クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png)されます)

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>手順 5: トランザクションのスコープ内でストアドプロシージャ s ステートメントをラップする

「[トランザクション内でのデータベース変更のラップ](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)」チュートリアルでは、トランザクションのスコープ内で一連のデータベース変更ステートメントを実行する方法について説明しました。 トランザクションの全体で実行された変更はすべて成功するか、すべて失敗し、原子性が保証されることを思い出してください。 トランザクションを使用する方法は次のとおりです。

- `System.Transactions` 名前空間のクラスを使用すると、
- データアクセス層では、`SqlTransaction`のような ADO.NET クラスを使用します。
- ストアドプロシージャ内に直接 T-sql トランザクションコマンドを追加する

「*トランザクション内でのデータベース変更のラッピング*」チュートリアルでは、DAL の ADO.NET クラスを使用しています。 このチュートリアルの残りの部分では、ストアドプロシージャ内から T-sql コマンドを使用してトランザクションを管理する方法について説明します。

トランザクションを手動で開始、コミット、およびロールバックするための3つの主要な SQL コマンドは、それぞれ `BEGIN TRANSACTION`、`COMMIT TRANSACTION`、および `ROLLBACK TRANSACTION`です。 ADO.NET アプローチと同様に、ストアドプロシージャ内からトランザクションを使用する場合は、次のパターンを適用する必要があります。

1. トランザクションの開始を示します。
2. トランザクションを構成する SQL ステートメントを実行します。
3. 手順 2. のステートメントのいずれかでエラーが発生した場合は、トランザクションをロールバックします。
4. 手順 2. のすべてのステートメントがエラーなしで完了した場合は、トランザクションをコミットします。

このパターンは、次のテンプレートを使用して T-sql 構文で実装できます。

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

このテンプレートは、`TRY...CATCH` ブロックを定義することによって開始されます。これは SQL Server 2005 の新しいコンストラクトです。 のC#`try...catch` ブロックと同様に、SQL `TRY...CATCH` ブロックは `TRY` ブロック内のステートメントを実行します。 いずれかのステートメントでエラーが発生した場合、コントロールは直ちに `CATCH` ブロックに転送されます。

トランザクションを記述する SQL ステートメントの実行中にエラーが発生しなかった場合は、`COMMIT TRANSACTION` ステートメントによって変更がコミットされ、トランザクションが完了します。 ただし、いずれかのステートメントでエラーが発生した場合、`CATCH` ブロック内の `ROLLBACK TRANSACTION` は、トランザクションが開始される前の状態にデータベースを返します。 また、このストアドプロシージャは[RAISERROR コマンド](https://msdn.microsoft.com/library/ms178592.aspx)を使用してエラーを生成します。これにより、アプリケーションで `SqlException` が発生します。

> [!NOTE]
> `TRY...CATCH` ブロックは SQL Server 2005 の新機能であるため、以前のバージョンの Microsoft SQL Server を使用している場合、上記のテンプレートは機能しません。 SQL Server 2005 を使用していない場合は、他のバージョンの SQL Server で動作するテンプレートについては、「 [SQL Server ストアドプロシージャのトランザクションの管理」](http://www.4guysfromrolla.com/webtech/080305-1.shtml)を参照してください。

具体的な例を見てみましょう。 `Categories` テーブルと `Products` テーブルの間には外部キー制約が存在します。つまり、`Products` テーブル内の各 `CategoryID` フィールドは `CategoryID` テーブルの `Categories` 値にマップされる必要があります。 この制約に違反するアクション (製品が関連付けられているカテゴリを削除しようとするなど) があると、外部キー制約違反になります。 これを確認するには、「バイナリデータの処理」セクション (`~/BinaryData/UpdatingAndDeleting.aspx`) の「既存のバイナリデータの更新と削除」の例を参照してください。 このページには、システム内の各カテゴリが [編集] ボタンと [削除] ボタンと共に一覧表示されます (図13を参照)。ただし、飲み物など、関連付けられた製品を含むカテゴリを削除しようとすると、外部キー制約違反が原因で削除が失敗します (図14を参照)。

[[編集] ボタンと [削除] ボタンを使用して各カテゴリを GridView に表示 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png)

**図 13**: 各カテゴリが GridView に編集および削除ボタン付きで表示される ([クリックしてフルサイズのイメージを表示する](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png))

[既存の製品を含むカテゴリを削除することはできません ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)

**図 14**: 既存の製品を持つカテゴリを削除することはできません ([クリックすると、フルサイズの画像が表示](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png)されます)

ただし、関連付けられている製品があるかどうかにかかわらず、カテゴリを削除できるようにすることを想像してください。 製品のカテゴリを削除する必要がある場合は、既存の製品も削除するとします (別の方法としては、単に製品 `CategoryID` 値を `NULL`に設定します)。 この機能は、foreign key 制約の cascade ルールを使用して実装できます。 または、`@CategoryID` 入力パラメーターを受け取るストアドプロシージャを作成し、呼び出されたときに、関連付けられているすべての製品と指定したカテゴリを明示的に削除することもできます。

このようなストアドプロシージャでの最初の試行は、次のようになります。

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

これによって、関連付けられている製品とカテゴリが確実に削除されますが、トランザクションの包括状態では削除されません。 `Categories` に、特定の `@CategoryID` 値の削除を禁止する外部キー制約があると仮定します。 問題は、このような場合に、カテゴリを削除しようとする前にすべての製品が削除されることです。 結果として、このようなカテゴリの場合、このストアドプロシージャは、他のテーブル内に関連レコードが残っているので、カテゴリのすべての製品を削除します。

ただし、ストアドプロシージャがトランザクションのスコープ内でラップされていた場合、`Categories`で削除が失敗したときに、`Products` テーブルの削除がロールバックされます。 次のストアドプロシージャスクリプトでは、トランザクションを使用して、2つの `DELETE` ステートメント間で原子性を確保します。

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.sql)]

`Categories_Delete` ストアドプロシージャを Northwind データベースに追加してみましょう。 ストアドプロシージャをデータベースに追加する手順については、手順1を参照してください。

## <a name="step-6-updating-thecategoriestableadapter"></a>手順 6:`CategoriesTableAdapter` の更新

`Categories_Delete` ストアドプロシージャをデータベースに追加しましたが、現在、DAL は、アドホック SQL ステートメントを使用して削除を実行するように構成されています。 `CategoriesTableAdapter` を更新し、代わりに `Categories_Delete` ストアドプロシージャを使用するように指示する必要があります。

> [!NOTE]
> このチュートリアルの前半では、`NorthwindWithSprocs` データセットを使用しました。 ただし、そのデータセットにはエンティティが1つだけ存在し、`ProductsDataTable`、カテゴリを操作する必要があります。 そのため、このチュートリアルの残りの部分では、`Northwind` データセットを参照するデータアクセス層について説明します。これは、[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)に関するチュートリアルで最初に作成したものです。

Northwind データセットを開き、`CategoriesTableAdapter`を選択して、プロパティウィンドウにアクセスします。 プロパティウィンドウには、TableAdapter によって使用される `InsertCommand`、`UpdateCommand`、`DeleteCommand`、`SelectCommand` と、その名前と接続情報が表示されます。 詳細を表示するには、[`DeleteCommand`] プロパティを展開します。 図15に示すように、`DeleteCommand` s `CommandType` プロパティは Text に設定されています。これは、`CommandText` プロパティのテキストをアドホック SQL クエリとして送信するように指示します。

![デザイナーで CategoriesTableAdapter を選択すると、[プロパティ] ウィンドウにそのプロパティが表示されます。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)

**図 15**: デザイナーで `CategoriesTableAdapter` を選択すると、[プロパティ] ウィンドウにそのプロパティが表示されます。

これらの設定を変更するには、プロパティウィンドウで (DeleteCommand) のテキストを選択し、ドロップダウンリストから [(新規)] を選択します。 これにより、`CommandText`、`CommandType`、および `Parameters` の各プロパティの設定がクリアされます。 次に、[`CommandType`] プロパティを `StoredProcedure` に設定し、`CommandText` のストアドプロシージャの名前 (`dbo.Categories_Delete`) を入力します。 この順序でプロパティが入力されていることを確認した場合は、まず `CommandType` を入力し、次に `CommandText` をクリックすると、パラメーターコレクションが自動的に設定されます。 これらのプロパティをこの順序で入力しない場合は、parameters コレクションエディターを使用して手動でパラメーターを追加する必要があります。 どちらの場合も、parameters プロパティの省略記号をクリックしてパラメーターコレクションエディターを表示し、正しいパラメーター設定が変更されていることを確認することをお勧めします (図16を参照)。 ダイアログボックスにパラメーターが表示されない場合は、`@CategoryID` パラメーターを手動で追加します (`@RETURN_VALUE` パラメーターを追加する必要はありません)。

![パラメーター設定が正しいことを確認してください](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**図 16**: パラメーターの設定が正しいことを確認する

DAL が更新されると、カテゴリを削除すると、そのカテゴリに関連付けられているすべての製品が自動的に削除され、トランザクションの包括的なものになります。 これを確認するには、[既存のバイナリデータの更新と削除] ページに戻り、いずれかのカテゴリの [削除] ボタンをクリックします。 マウスを1回クリックするだけで、カテゴリとそれに関連付けられているすべての製品が削除されます。

> [!NOTE]
> 選択したカテゴリと一緒に複数の製品を削除する `Categories_Delete` ストアドプロシージャをテストする前に、データベースのバックアップコピーを作成することをお勧めします。 `App_Data`で `NORTHWND.MDF` データベースを使用している場合は、単に Visual Studio を閉じ、`App_Data` 内の MDF ファイルと LDF ファイルを他のフォルダーにコピーします。 機能のテスト後、データベースを復元するには、Visual Studio を終了し、`App_Data` 内の現在の MDF ファイルと LDF ファイルをバックアップコピーに置き換えます。

## <a name="summary"></a>要約

TableAdapter ウィザードによって自動的にストアドプロシージャが生成されますが、そのようなストアドプロシージャが既に作成されている場合や、手動で作成したり、他のツールを使用したりする場合もあります。 このようなシナリオに対応するために、既存のストアドプロシージャを参照するように TableAdapter を構成することもできます。 このチュートリアルでは、Visual Studio 環境を使用してデータベースにストアドプロシージャを手動で追加する方法と、TableAdapter のメソッドをこれらのストアドプロシージャに接続する方法について説明しました。 また、ストアドプロシージャ内からのトランザクションの開始、コミット、およびロールバックに使用される T-sql コマンドとスクリプトパターンについても説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Geisenow、S ren Jacob Lauritsen、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [次へ](updating-the-tableadapter-to-use-joins-cs.md)
