---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: マネージコードを使用したストアドプロシージャとユーザー定義関数の作成 (VB) |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 は .NET 共通言語ランタイムと統合されているため、開発者はマネージコードを使用してデータベースオブジェクトを作成できます。 このチュートリアル...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ac5f71d519689a9dc84fb82a04196d520cca6e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443842"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>マネージド コードでストアド プロシージャとユーザー定義関数を作成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip)または[PDF のダウンロード](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 は .NET 共通言語ランタイムと統合されているため、開発者はマネージコードを使用してデータベースオブジェクトを作成できます。 このチュートリアルでは、Visual Basic またはC#コードを使用してマネージストアドプロシージャとマネージユーザー定義関数を作成する方法について説明します。 また、Visual Studio のこれらのエディションで、このようなマネージデータベースオブジェクトをデバッグする方法についても説明します。

## <a name="introduction"></a>はじめに

Microsoft s SQL Server 2005 などのデータベースでは、データの挿入、変更、および取得に[transact-sql (構造化照会言語 transact-sql)](http://en.wikipedia.org/wiki/Transact-SQL)が使用されます。 ほとんどのデータベースシステムには、1つの再利用可能な単位として実行できる一連の SQL ステートメントをグループ化するための構造が含まれています。 ストアドプロシージャの一例を次に示します。 もう1つは、*ユーザー定義関数*(udf) です。これは、手順 9. で詳細を確認するコンストラクトです。

SQL は、データのセットを操作できるように設計されています。 `SELECT`、`UPDATE`、および `DELETE` の各ステートメントは、本質的に、対応するテーブル内のすべてのレコードに適用され、`WHERE` 句によってのみ制限されます。 しかし、一度に1つのレコードを操作し、スカラーデータを操作するために設計された言語機能は多数あります。 [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553)では、レコードのセットを一度に1つずつループすることができます。 `LEFT`、`CHARINDEX`、`PATINDEX` などの文字列操作関数は、スカラーデータを操作します。 SQL には、`IF` や `WHILE`などの制御フローステートメントも含まれています。

Microsoft SQL Server 2005 より前では、ストアドプロシージャと Udf は T-sql ステートメントのコレクションとしてのみ定義できました。 ただし、SQL Server 2005 は、[共通言語ランタイム (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)との統合を提供するように設計されています。これは、すべての .net アセンブリで使用されるランタイムです。 そのため、SQL Server 2005 データベースのストアドプロシージャと Udf は、マネージコードを使用して作成できます。 つまり、ストアドプロシージャまたは UDF を Visual Basic クラスのメソッドとして作成できます。 これにより、これらのストアドプロシージャおよび Udf は、.NET Framework と独自のカスタムクラスの機能を利用できるようになります。

このチュートリアルでは、マネージストアドプロシージャとユーザー定義関数を作成する方法と、それらを Northwind データベースに統合する方法について説明します。 始めましょう!

> [!NOTE]
> マネージデータベースオブジェクトには、対応する SQL server よりも利点があります。 言語の豊富さと知識があり、既存のコードとロジックを再利用できることが主な利点です。 ただし、管理されたデータベースオブジェクトは、処理ロジックがあまり必要としないデータのセットを操作する場合に効率が低下する可能性があります。 マネージコードと T-sql を使用する利点の詳細については、[マネージコードを使用してデータベースオブジェクトを作成する利点](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)を確認してください。

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>手順 1:`App_Data` から Northwind データベースを移動する

これまでのすべてのチュートリアルでは、web アプリケーションの `App_Data` フォルダーに Microsoft SQL Server 2005 Express Edition データベースファイルが使用されています。 データベースを `App_Data` に配置すると、すべてのファイルが1つのディレクトリ内に配置され、チュートリアルをテストするための追加の構成手順を必要としないため、これらのチュートリアルを簡単に配布して実行できます。

ただし、このチュートリアルでは、で Northwind データベースを `App_Data` から移動し、SQL Server 2005 Express Edition データベースインスタンスに明示的に登録します。 このチュートリアルの手順は `App_Data` フォルダー内のデータベースを使用して実行できますが、データベースを SQL Server 2005 Express Edition データベースインスタンスに明示的に登録すると、いくつかの手順がはるかに簡単になります。

このチュートリアルのダウンロードには、`DataFiles`という名前のフォルダーに配置された `NORTHWND.MDF` と `NORTHWND_log.LDF` の2つのデータベースファイルがあります。 チュートリアルを独自に実装している場合は、Visual Studio を終了し、`NORTHWND.MDF` と `NORTHWND_log.LDF` ファイルを web サイトの `App_Data` フォルダーから web サイトの外部のフォルダーに移動します。 データベースファイルを別のフォルダーに移動したら、Northwind データベースを SQL Server 2005 Express Edition データベースインスタンスに登録する必要があります。 これは SQL Server Management Studio から行うことができます。 SQL Server 2005 の Express 以外のエディションがコンピューターにインストールされている場合は、Management Studio が既にインストールされている可能性があります。 コンピューターに SQL Server 2005 Express Edition しかない場合は、 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)をダウンロードしてインストールしてください。

SQL Server Management Studio を起動します。 図1に示すように、Management Studio は、どのサーバーに接続するかをたずねることで開始されます。 サーバー名として「localhost\SQLExpress」と入力し、[認証] ボックスの一覧で [Windows 認証] を選択し、[接続] をクリックします。

![適切なデータベースインスタンスに接続する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**図 1**: 適切なデータベースインスタンスに接続する

接続した後、[オブジェクトエクスプローラー] ウィンドウには、データベース、セキュリティ情報、管理オプションなど、SQL Server 2005 Express Edition データベースインスタンスに関する情報が一覧表示されます。

Northwind データベースは、`DataFiles` フォルダー (または移動した場所) に SQL Server 2005 Express Edition データベースインスタンスにアタッチする必要があります。 [データベース] フォルダーを右クリックし、ショートカットメニューの [アタッチ] をクリックします。 [データベースのアタッチ] ダイアログボックスが表示されます。 [追加] ボタンをクリックし、適切な `NORTHWND.MDF` ファイルにドリルダウンして、[OK] をクリックします。 この時点で、画面は図2のようになります。

[適切なデータベースインスタンスに接続 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**図 2**: 適切なデータベースインスタンスに接続する ([クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png)されます)

> [!NOTE]
> [データベースのアタッチ] ダイアログボックスを使用し Management Studio て SQL Server 2005 Express Edition インスタンスに接続するときは、[マイドキュメント] などのユーザープロファイルディレクトリにドリルダウンすることはできません。 そのため、`NORTHWND.MDF` と `NORTHWND_log.LDF` ファイルは、ユーザープロファイル以外のディレクトリに配置してください。

[OK] ボタンをクリックして、データベースをアタッチします。 [データベースのアタッチ] ダイアログボックスが閉じ、オブジェクトエクスプローラーにアタッチされたデータベースが一覧表示されます。 Northwind データベースには、`9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`のような名前が付いている可能性があります。 データベースの名前を Northwind に変更するには、データベースを右クリックし、[名前の変更] を選択します。

![データベースの名前を Northwind に変更する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**図 3**: データベースの名前を Northwind に変更する

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>手順 2: Visual Studio で新しいソリューションと SQL Server プロジェクトを作成する

SQL Server 2005 でマネージストアドプロシージャまたは Udf を作成するには、ストアドプロシージャと UDF ロジックをクラスの Visual Basic コードとして記述します。 コードを記述したら、このクラスをアセンブリ (`.dll` ファイル) にコンパイルし、アセンブリを SQL Server データベースに登録した後、アセンブリ内の対応するメソッドを参照するストアドプロシージャまたは UDF オブジェクトをデータベース内に作成する必要があります。 これらの手順はすべて手動で実行できます。 任意のテキストエディターでコードを作成し、コマンドラインから Visual Basic コンパイラ (`vbc.exe`) を使用してコンパイルし、 [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx)コマンドまたは Management Studio を使用してデータベースに登録し、同様の方法でストアドプロシージャまたは UDF オブジェクトを追加できます。 幸いなことに、Visual Studio の Professional および Team Systems バージョンには、これらのタスクを自動化する SQL Server プロジェクトの種類が含まれています。 このチュートリアルでは、SQL Server プロジェクトの種類を使用して、マネージストアドプロシージャと UDF を作成します。

> [!NOTE]
> Visual Web Developer または Standard edition の Visual Studio を使用している場合は、代わりに手動での方法を使用する必要があります。 手順13では、これらの手順を手動で実行するための詳細な手順について説明します。 手順13を読む前に手順 2 ~ 12 を読むことをお勧めします。これらの手順には、使用している Visual Studio のバージョンに関係なく適用する必要がある重要な SQL Server 構成手順が含まれているためです。

まず、Visual Studio を開きます。 [ファイル] メニューの [新しいプロジェクト] をクリックして、[新しいプロジェクト] ダイアログボックスを表示します (図4を参照)。 データベースプロジェクトの種類にドリルダウンし、右側に表示されているテンプレートから、新しい SQL Server プロジェクトの作成を選択します。 このプロジェクトに `ManagedDatabaseConstructs` 名前を付け、`Tutorial75`という名前のソリューション内に配置することを選択しました。

[新しい SQL Server プロジェクトを作成 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**図 4**: 新しい SQL Server プロジェクトを作成[する (クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))

[新しいプロジェクト] ダイアログボックスの [OK] ボタンをクリックして、ソリューションと SQL Server プロジェクトを作成します。

SQL Server プロジェクトは、特定のデータベースに関連付けられています。 その結果、新しい SQL Server プロジェクトを作成した後、すぐにこの情報を指定するように求められます。 図5に、手順1で SQL Server 2005 Express Edition データベースインスタンスに登録した Northwind データベースを指すように入力された [新しいデータベース参照] ダイアログボックスを示します。

![SQL Server プロジェクトを Northwind データベースに関連付ける](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**図 5**: SQL Server プロジェクトを Northwind データベースに関連付ける

このプロジェクト内で作成するマネージストアドプロシージャと Udf をデバッグするには、接続に対して SQL/CLR デバッグサポートを有効にする必要があります。 (図5のように) SQL Server プロジェクトを新しいデータベースに関連付けるたびに、Visual Studio は接続で SQL/CLR デバッグを有効にするかどうかを確認します (図6を参照)。 [はい] をクリックします。

![SQL/CLR デバッグを有効にする](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**図 6**: SQL/CLR デバッグを有効にする

この時点で、新しい SQL Server プロジェクトがソリューションに追加されました。 これには、`Test Scripts` という名前のフォルダーが含まれています。このファイルは、プロジェクトで作成されたマネージデータベースオブジェクトのデバッグに使用される、`Test.sql`という名前のファイルです。 ここでは、手順 12. でのデバッグについて説明します。

これで、新しいマネージストアドプロシージャと Udf をこのプロジェクトに追加できるようになりましたが、最初にソリューションに既存の web アプリケーションを含めます。 [ファイル] メニューの [追加] オプションを選択し、[既存の Web サイト] を選択します。 適切な web サイトフォルダーに移動し、[OK] をクリックします。 図7に示すように、これによりソリューションが更新され、web サイトと `ManagedDatabaseConstructs` SQL Server プロジェクトの2つのプロジェクトが含まれるようになります。

![ソリューションエクスプローラーに2つのプロジェクトが含まれるようになりました](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**図 7**: ソリューションエクスプローラーに2つのプロジェクトが含まれるようになった

`Web.config` の `NORTHWNDConnectionString` 値は、現在 `App_Data` フォルダー内の `NORTHWND.MDF` ファイルを参照しています。 このデータベースを `App_Data` から削除し、SQL Server 2005 Express Edition データベースインスタンスに明示的に登録したため、`NORTHWNDConnectionString` 値を更新する必要があります。 Web サイトの `Web.config` ファイルを開き、`NORTHWNDConnectionString` の値を変更して、接続文字列が `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`を読み取るようにします。 この変更の後、`Web.config` の `<connectionStrings>` セクションは次のようになります。

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> [前のチュートリアル](debugging-stored-procedures-vb.md)で説明したように、ASP.NET web サイトなどのクライアントアプリケーションから SQL Server オブジェクトをデバッグする場合は、接続プールを無効にする必要があります。 上に示した接続文字列は、接続プール (`Pooling=false`) を無効にします。 ASP.NET web サイトからマネージストアドプロシージャおよび Udf のデバッグを計画していない場合は、接続プールを有効にします。

## <a name="step-3-creating-a-managed-stored-procedure"></a>手順 3: マネージストアドプロシージャの作成

マネージストアドプロシージャを Northwind データベースに追加するには、まず、SQL Server プロジェクトのメソッドとしてストアドプロシージャを作成する必要があります。 ソリューションエクスプローラーから、`ManagedDatabaseConstructs` プロジェクト名を右クリックし、[新しいアイテムの追加] を選択します。 [新しい項目の追加] ダイアログボックスが表示され、プロジェクトに追加できるマネージデータベースオブジェクトの種類が一覧表示されます。 図8に示すように、これにはストアドプロシージャやユーザー定義関数などが含まれます。

まず、廃止されたすべての製品を単に返すストアドプロシージャを追加します。 新しいストアドプロシージャファイルに `GetDiscontinuedProducts.vb`名前を指定します。

[GetDiscontinuedProducts という名前の新しいストアドプロシージャを追加 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**図 8**: `GetDiscontinuedProducts.vb` という名前の新しいストアドプロシージャを追加[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png)されます)

これにより、次の内容を含む新しい Visual Basic クラスファイルが作成されます。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

ストアドプロシージャは、`StoredProcedures`という名前の `Partial` クラスファイル内の `Shared` メソッドとして実装されていることに注意してください。 さらに、`GetDiscontinuedProducts` メソッドは、メソッドをストアドプロシージャとしてマークする[`SqlProcedure` 属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx)で修飾されます。

次のコードでは、`SqlCommand` オブジェクトを作成し、その `CommandText` を、`Discontinued` フィールドが1と等しい製品の `Products` テーブルからすべての列を返す `SELECT` クエリに設定します。 次に、コマンドを実行し、結果をクライアントアプリケーションに送り返します。 このコードを `GetDiscontinuedProducts` メソッドに追加します。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

すべてのマネージデータベースオブジェクトは、呼び出し元のコンテキストを表す[`SqlContext` オブジェクト](https://msdn.microsoft.com/library/ms131108.aspx)にアクセスできます。 `SqlContext` は、 [`Pipe` プロパティ](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)を介して[`SqlPipe` オブジェクト](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)へのアクセスを提供します。 この `SqlPipe` オブジェクトは、SQL Server データベースと呼び出し元のアプリケーションの間で情報をフェリーするために使用されます。 その名前が示すように、 [`ExecuteAndSend` メソッド](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)は渡された `SqlCommand` オブジェクトを実行し、結果をクライアントアプリケーションに返します。

> [!NOTE]
> マネージデータベースオブジェクトは、セットベースのロジックではなく、手続き型ロジックを使用するストアドプロシージャおよび Udf に最適です。 手続き型のロジックでは、行ごとにデータセットを処理するか、スカラーデータを操作する必要があります。 ただし、先ほど作成した `GetDiscontinuedProducts` メソッドには、手続き型のロジックは含まれません。 そのため、T-sql ストアドプロシージャとして実装するのが理想的です。 マネージストアドプロシージャを作成および配置するために必要な手順を示すために、マネージストアドプロシージャとして実装されています。

## <a name="step-4-deploying-the-managed-stored-procedure"></a>手順 4: マネージストアドプロシージャの配置

このコードが完成すると、Northwind データベースにデプロイできるようになります。 SQL Server プロジェクトを配置すると、コードがアセンブリにコンパイルされ、アセンブリがデータベースに登録され、データベースに対応するオブジェクトが作成されて、アセンブリ内の適切なメソッドにリンクされます。 配置オプションによって実行されるタスクの正確なセットは、手順13でより正確に記述されます。 ソリューションエクスプローラーで `ManagedDatabaseConstructs` プロジェクト名を右クリックし、[配置] オプションを選択します。 ただし、配置は次のエラーで失敗します: ' EXTERNAL ' 付近に正しくない構文があります。 現在のデータベースの互換性レベルを高い値に設定し、この機能を有効にする必要があります。 ストアドプロシージャ `sp_dbcmptlevel`のヘルプを参照してください。

このエラーメッセージは、アセンブリを Northwind データベースに登録しようとしたときに発生します。 SQL Server 2005 データベースにアセンブリを登録するには、データベースの互換性レベルを90に設定する必要があります。 既定では、新しい SQL Server 2005 データベースの互換性レベルは90です。 ただし、Microsoft SQL Server 2000 を使用して作成されたデータベースの既定の互換性レベルは80です。 Northwind データベースは最初 Microsoft SQL Server 2000 データベースであったため、その互換性レベルは現在は80に設定されているため、マネージデータベースオブジェクトを登録するには、90に上げる必要があります。

データベースの互換性レベルを更新するには、Management Studio で新しいクエリウィンドウを開き、次のように入力します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

ツールバーの [実行] アイコンをクリックして、上記のクエリを実行します。

[Northwind データベースの互換性レベルを更新 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**図 9**: Northwind データベースの互換性レベルを更新[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png)されます)

互換性レベルを更新した後、SQL Server プロジェクトを再デプロイします。 今回は、配置がエラーなしで完了する必要があります。

SQL Server Management Studio に戻り、オブジェクトエクスプローラーで Northwind データベースを右クリックして、[最新の状態に更新] を選択します。 次に、[プログラミング] フォルダーをドリルダウンし、[アセンブリ] フォルダーを展開します。 図10に示すように、Northwind データベースには、`ManagedDatabaseConstructs` プロジェクトによって生成されたアセンブリが含まれるようになりました。

![ManagedDatabaseConstructs アセンブリが Northwind データベースに登録されるようになりました。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**図 10**: `ManagedDatabaseConstructs` アセンブリが Northwind データベースに登録されるようになりました。

さらに、[ストアドプロシージャ] フォルダーを展開します。 ここには、`GetDiscontinuedProducts`という名前のストアドプロシージャが表示されます。 このストアドプロシージャは、配置プロセスによって作成され、`ManagedDatabaseConstructs` アセンブリの `GetDiscontinuedProducts` メソッドを指します。 `GetDiscontinuedProducts` ストアドプロシージャを実行すると、`GetDiscontinuedProducts` メソッドが実行されます。 これはマネージストアドプロシージャであるため、Management Studio (ストアドプロシージャ名の横にあるロックアイコン) を使用して編集することはできません。

![GetDiscontinuedProducts ストアドプロシージャは、[ストアドプロシージャ] フォルダーに一覧表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**図 11**: `GetDiscontinuedProducts` ストアドプロシージャが [ストアドプロシージャ] フォルダーに表示される

マネージストアドプロシージャを呼び出すことができるようになる前に、もう1つのハードルが必要です。データベースはマネージコードの実行を防止するように構成されています。 これを確認するには、新しいクエリウィンドウを開き、`GetDiscontinuedProducts` ストアドプロシージャを実行します。 次のエラーメッセージが表示されます。 .NET Framework でのユーザーコードの実行が無効になっています。 Clr enabled 構成オプションを有効にします。

Northwind データベースの構成情報を確認するには、クエリウィンドウでコマンド `exec sp_configure` を入力して実行します。 これは、clr enabled 設定が現在0に設定されていることを示しています。

[clr enabled 設定が現在0に設定されて ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**図 12**: Clr enabled 設定が現在0に設定されている ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png)されます)

図12の各構成設定には4つの値が表示されています。最小値と最大値、および構成値と実行値です。 Clr enabled 設定の構成値を更新するには、次のコマンドを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

`exec sp_configure` を再実行すると、上記のステートメントによって clr enabled 設定の config 値が1に更新されたが、実行値がまだ0に設定されていることがわかります。 この構成の変更を反映するには、 [`RECONFIGURE` コマンド](https://msdn.microsoft.com/library/ms176069.aspx)を実行する必要があります。これにより、実行値が現在の構成値に設定されます。 クエリウィンドウに `RECONFIGURE` を入力し、ツールバーの [実行] アイコンをクリックするだけです。 `exec sp_configure` 実行すると、clr が有効になっている設定の構成値と実行値の値が1になります。

Clr enabled 構成が完了すると、マネージ `GetDiscontinuedProducts` ストアドプロシージャを実行する準備が整います。 クエリウィンドウで、コマンド `exec` `GetDiscontinuedProducts`を入力して実行します。 ストアドプロシージャを呼び出すと、`GetDiscontinuedProducts` メソッド内の対応するマネージコードが実行されます。 このコードは、`SELECT` クエリを発行して、廃止されたすべての製品を返し、このデータを呼び出し元のアプリケーションに返します。これは、このインスタンスで SQL Server Management Studio ます。 Management Studio は、これらの結果を受け取り、結果ウィンドウに表示します。

[GetDiscontinuedProducts ストアドプロシージャが、廃止されたすべての製品を返す ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**図 13**: `GetDiscontinuedProducts` ストアドプロシージャは、すべての廃止された製品を返します ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png)されます)

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>手順 5: 入力パラメーターを受け取るマネージストアドプロシージャの作成

これらのチュートリアル全体で作成したクエリとストアドプロシージャの多くは、*パラメーター*を使用しています。 たとえば、「[型指定されたデータセットの tableadapter 用に新しいストアドプロシージャを作成する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)」チュートリアルでは、`@CategoryID`という名前の入力パラメーターを受け取る `GetProductsByCategoryID` という名前のストアドプロシージャを作成しました。 次に、ストアドプロシージャは、指定された `@CategoryID` パラメーターの値に一致する `CategoryID` フィールドを持つすべての製品を返します。

入力パラメーターを受け取るマネージストアドプロシージャを作成するには、メソッドの定義でこれらのパラメーターを指定するだけです。 これを説明するために、次のように `GetProductsWithPriceLessThan`という名前の `ManagedDatabaseConstructs` プロジェクトに別のマネージストアドプロシージャを追加します。 このマネージストアドプロシージャは、価格を指定する入力パラメーターを受け取り、`UnitPrice` フィールドがパラメーター s 値よりも小さいすべての製品を返します。

新しいストアドプロシージャをプロジェクトに追加するには、`ManagedDatabaseConstructs` プロジェクト名を右クリックし、[新しいストアドプロシージャの追加] を選択します。 このファイルには `GetProductsWithPriceLessThan.vb` という名前を付けます。 手順 3. で見たように、これにより、`Partial` クラス `StoredProcedures`内に配置された `GetProductsWithPriceLessThan` という名前のメソッドを使用して、新しい Visual Basic クラスファイルが作成されます。

`GetProductsWithPriceLessThan` メソッドの定義を更新して、`price` という名前の[`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx)入力パラメーターを受け取り、クエリ結果を実行して返すコードを記述します。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan` メソッドの定義とコードは、手順 3. で作成した `GetDiscontinuedProducts` メソッドの定義とコードによく似ています。 唯一の違いは、`GetProductsWithPriceLessThan` メソッドが入力パラメーターとして受け入れ (`price`)、`SqlCommand` s クエリにパラメーター (`@MaxPrice`) が含まれていること、およびパラメーターが `SqlCommand` s に追加され、`Parameters` の変数の値が割り当てられていることです。`price`

このコードを追加した後、SQL Server プロジェクトを再デプロイします。 次に、SQL Server Management Studio に戻り、[ストアドプロシージャ] フォルダーを更新します。 新しいエントリが表示 `GetProductsWithPriceLessThan`ます。 図14に示すように、クエリウィンドウから、コマンド `exec GetProductsWithPriceLessThan 25`を入力して実行します。これにより、$25 未満のすべての製品が一覧表示されます。

[$25 未満の ![製品が表示される](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**図 14**: $25 未満の製品が表示されます ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png)されます)

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>手順 6: データアクセス層からマネージストアドプロシージャを呼び出す

この時点で、`GetDiscontinuedProducts` と `GetProductsWithPriceLessThan` のマネージストアドプロシージャを `ManagedDatabaseConstructs` プロジェクトに追加し、Northwind SQL Server データベースに登録しました。 また、これらのマネージストアドプロシージャを SQL Server Management Studio から呼び出しました (図13および14を参照してください)。 ただし、ASP.NET アプリケーションでこれらのマネージストアドプロシージャを使用するには、アーキテクチャのデータアクセス層とビジネスロジック層にそれらを追加する必要があります。 この手順では、`NorthwindWithSprocs` 型指定されたデータセットの `ProductsTableAdapter` に2つの新しいメソッドを追加します。これは、型指定された[データセットの tableadapter チュートリアル用に新しいストアドプロシージャを作成するため](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)に最初に作成されました。 手順 7. で、対応するメソッドを BLL に追加します。

Visual Studio で `NorthwindWithSprocs` 型指定されたデータセットを開き、`GetDiscontinuedProducts`という名前の `ProductsTableAdapter` に新しいメソッドを追加します。 新しいメソッドを TableAdapter に追加するには、デザイナーで TableAdapter の名前を右クリックし、コンテキストメニューの [クエリの追加] オプションを選択します。

> [!NOTE]
> Northwind データベースを `App_Data` フォルダーから SQL Server 2005 Express Edition データベースインスタンスに移動したため、web.config 内の対応する接続文字列を更新して、この変更を反映する必要があります。 手順2では、`Web.config`の `NORTHWNDConnectionString` 値の更新について説明しました。 この更新を行ったことを忘れた場合は、[クエリの追加に失敗しました] というエラーメッセージが表示されます。 新しいメソッドを TableAdapter に追加しようとしたときに、ダイアログボックスにオブジェクト `Web.config` の接続 `NORTHWNDConnectionString` が見つかりません。 このエラーを解決するには、[OK] をクリックし、`Web.config` にアクセスして、手順 2. で説明されているように `NORTHWNDConnectionString` の値を更新します。 その後、メソッドを TableAdapter にもう一度追加します。 今回は、エラーなしで動作します。

新しいメソッドを追加すると、TableAdapter クエリの構成ウィザードが起動されます。これは、過去のチュートリアルで何度も使用しています。 最初の手順では、TableAdapter がデータベースにアクセスする方法を指定するように求められます。これには、アドホック SQL ステートメントを使用する方法と、新規または既存のストアドプロシージャを使用する方法があります。 `GetDiscontinuedProducts` マネージストアドプロシージャを既に作成し、データベースと共に登録しているので、[既存のストアドプロシージャを使用する] オプションを選択し、[次へ] をクリックします。

[![[既存のストアドプロシージャを使用する] オプションを選択する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**図 15**: [既存のストアドプロシージャを使用する] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png)されます)

次の画面では、メソッドが呼び出すストアドプロシージャを確認するメッセージが表示されます。 ドロップダウンリストから [`GetDiscontinuedProducts` マネージストアドプロシージャ] を選択し、[次へ] をクリックします。

[GetDiscontinuedProducts マネージストアドプロシージャを選択 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**図 16**: `GetDiscontinuedProducts` マネージストアドプロシージャを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png)されます)

次に、ストアドプロシージャから行を返すか、単一の値を返すか、または何も返さないかを指定するように求められます。 `GetDiscontinuedProducts` は廃止された製品の行のセットを返すため、最初のオプション (表形式のデータ) を選択し、[次へ] をクリックします。

[表形式のデータオプションを選択 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**図 17**: 表形式のデータオプションを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png)されます)

ウィザードの最後の画面では、使用するデータアクセスパターンと、結果として生成されるメソッドの名前を指定できます。 両方のチェックボックスをオンのままにして、メソッドに `FillByDiscontinued` と `GetDiscontinuedProducts`という名前を指定します。 [完了] をクリックしてウィザードを終了します。

[![名前メソッドの FillByDiscontinued および GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**図 18**: メソッドに `FillByDiscontinued` と `GetDiscontinuedProducts` の名前を指定[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png)されます)

これらの手順を繰り返して、`FillByPriceLessThan` という名前のメソッドを作成し、`GetProductsWithPriceLessThan` マネージストアドプロシージャの `ProductsTableAdapter` に `GetProductsWithPriceLessThan` します。

図19は、`GetDiscontinuedProducts` および `GetProductsWithPriceLessThan` マネージストアドプロシージャの `ProductsTableAdapter` にメソッドを追加した後のデータセットデザイナーのスクリーンショットを示しています。

[ProductsTableAdapter には、この手順で追加された新しいメソッドが含まれて ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**図 19**: `ProductsTableAdapter` には、この手順で追加した新しいメソッドが含まれています ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)されます)

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>手順 7: ビジネスロジック層に対応するメソッドを追加する

手順 4. と 5. で追加したマネージストアドプロシージャを呼び出すメソッドを含むようにデータアクセス層を更新したので、次に、対応するメソッドをビジネスロジック層に追加する必要があります。 次の2つのメソッドを `ProductsBLLWithSprocs` クラスに追加します。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

どちらの方法でも、対応する DAL メソッドが呼び出され、`ProductsDataTable` インスタンスが返されます。 各メソッドの上にある `DataObjectMethodAttribute` マークアップにより、これらのメソッドは、ObjectDataSource s データソース構成ウィザードの [選択] タブのドロップダウンリストに表示されます。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>手順 8: プレゼンテーション層からマネージストアドプロシージャを呼び出す

ビジネスロジックとデータアクセス層が拡張され、`GetDiscontinuedProducts` および `GetProductsWithPriceLessThan` マネージストアドプロシージャの呼び出しがサポートされるようになったため、ASP.NET ページを使用してこれらのストアドプロシージャの結果を表示できるようになりました。

`AdvancedDAL` フォルダーの [`ManagedFunctionsAndSprocs.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグします。 GridView s `ID` プロパティを `DiscontinuedProducts` に設定し、そのスマートタグから `DiscontinuedProductsDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLLWithSprocs` クラス s `GetDiscontinuedProducts` メソッドからデータをプルするように ObjectDataSource を構成します。

[製品 Bllwithsproc クラスを使用するように ObjectDataSource を構成 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**図 20**: `ProductsBLLWithSprocs` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))

[![[選択] タブのドロップダウンリストから GetDiscontinuedProducts メソッドを選択します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**図 21**: [選択] タブのドロップダウンリストから `GetDiscontinuedProducts` メソッドを選択する ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png)されます)

このグリッドを使用して製品情報が表示されるだけなので、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定し、[完了] をクリックします。

ウィザードを完了すると、Visual Studio によって `ProductsDataTable`の各データフィールドに BoundField または CheckBoxField が自動的に追加されます。 `ProductName` と `Discontinued`を除くこれらのフィールドをすべて削除してください。その時点で、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

ブラウザーを使用してこのページを表示します。 ページにアクセスすると、ObjectDataSource は `ProductsBLLWithSprocs` クラス s `GetDiscontinuedProducts` メソッドを呼び出します。 手順 7. で説明したように、このメソッドは、`GetDiscontinuedProducts` ストアドプロシージャを呼び出す DAL `ProductsDataTable` クラス `GetDiscontinuedProducts` メソッドを呼び出します。 このストアドプロシージャはマネージストアドプロシージャであり、手順3で作成したコードを実行して、廃止された製品を返します。

マネージストアドプロシージャによって返された結果は、DAL によって `ProductsDataTable` にパッケージ化され、BLL に返されます。これにより、GridView にバインドされて表示されるプレゼンテーション層に返されます。 予想どおりに、廃止された製品がグリッドに表示されます。

[廃止された製品が一覧表示される ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**図 22**: 廃止された製品が一覧表示される ([クリックしてフルサイズの画像を表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png))

さらに、テキストボックスと別の GridView をページに追加します。 この GridView で、`ProductsBLLWithSprocs` クラス s `GetProductsWithPriceLessThan` メソッドを呼び出すことによって、テキストボックスに入力された量よりも少ない製品が表示されるようにします。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>手順 9: T-sql Udf の作成と呼び出し

ユーザー定義関数 (Udf) は、データベースオブジェクトで、プログラミング言語の関数のセマンティクスと密接に似ています。 Visual Basic の関数と同様に、Udf にはさまざまな数の入力パラメーターを含めることができ、特定の型の値を返すことができます。 UDF は、スカラーデータ (文字列、整数など) または表形式のデータのいずれかを返すことができます。 ここでは、スカラーデータ型を返す UDF で始まる両方の種類の Udf について簡単に見ていきます。

次の UDF は、特定の製品の在庫の推定値を計算します。 これは、3つの入力パラメーター (特定の製品の `UnitPrice`、`UnitsInStock`、および `Discontinued` 値) を使用して、`money`型の値を返すことによって行われます。 `UnitsInStock`によって `UnitPrice` を乗算することによって、在庫の推定値を計算します。 廃止された項目の場合、この値は半分になります。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

この UDF をデータベースに追加した後は、[プログラミング] フォルダー、[関数]、[スカラー値関数] の順に展開して、Management Studio で見つけることができます。 次のような `SELECT` クエリで使用できます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

`udf_ComputeInventoryValue` UDF を Northwind データベースに追加しました。図23は、Management Studio を通じて表示する場合の上記の `SELECT` クエリの出力を示しています。 UDF は、オブジェクトエクスプローラーの [スカラー値関数] フォルダーの下にも表示されます。

[各製品の在庫値が一覧表示され ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**図 23**: 各製品のインベントリ値が表示されます ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png)されます)

Udf は表形式のデータも返すことができます。 たとえば、特定のカテゴリに属する製品を返す UDF を作成できます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF は `@CategoryID` 入力パラメーターを受け取り、指定された `SELECT` クエリの結果を返します。 作成されたこの UDF は、`SELECT` クエリの `FROM` (または `JOIN`) 句で参照できます。 次の例では、各飲料の `ProductID`、`ProductName`、および `CategoryID` の値を返します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

`udf_GetProductsByCategoryID` UDF を Northwind データベースに追加しました。図24は、Management Studio を通じて表示される上記の `SELECT` クエリの出力を示しています。 表形式データを返す Udf は、[オブジェクトエクスプローラー s テーブル-値関数] フォルダーにあります。

[各飲料に対して ProductID、ProductName、および CategoryID が一覧表示され ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**図 24**: 各飲料の `ProductID`、`ProductName`、および `CategoryID` が一覧表示されます ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)されます)。

> [!NOTE]
> Udf の作成と使用の詳細については、「[ユーザー定義関数の概要](http://www.sqlteam.com/item.asp?ItemID=1955)」を参照してください。 また[、ユーザー定義関数の長所と短所について](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)も確認してください。

## <a name="step-10-creating-a-managed-udf"></a>手順 10: マネージ UDF の作成

前の例で作成した `udf_ComputeInventoryValue` と `udf_GetProductsByCategoryID` Udf は、T-sql データベースオブジェクトです。 SQL Server 2005 はマネージ Udf もサポートしています。これは、手順 3. と 5. のマネージストアドプロシージャと同じように `ManagedDatabaseConstructs` プロジェクトに追加できます。 この手順では、をマネージコードで `udf_ComputeInventoryValue` UDF を実装します。

マネージ UDF を `ManagedDatabaseConstructs` プロジェクトに追加するにはソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 [新しい項目の追加] ダイアログボックスからユーザー定義テンプレートを選択し、新しい UDF ファイルに `udf_ComputeInventoryValue_Managed.vb`という名前を指定します。

[新しいマネージ UDF を ManagedDatabaseConstructs プロジェクトに追加 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**図 25**: 新しいマネージ UDF を `ManagedDatabaseConstructs` プロジェクトに追加する ([クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))

ユーザー定義関数テンプレートは、という名前のメソッドを使用して `UserDefinedFunctions` という名前の `Partial` クラスを作成します。このメソッドの名前は、クラスファイルの名前 (このインスタンスでは`udf_ComputeInventoryValue_Managed`) と同じです。 このメソッドは、メソッドにマネージ UDF としてフラグを適用する[`SqlFunction` 属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)を使用して修飾されます。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

`udf_ComputeInventoryValue` メソッドは現在[`SqlString` オブジェクト](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)を返し、入力パラメーターを受け取りません。 メソッド定義を更新して、3つの入力パラメーター (`UnitPrice`、`UnitsInStock`、および `Discontinued` を受け取り、`SqlMoney` オブジェクトを返すようにする必要があります。 在庫値を計算するためのロジックは、T-sql `udf_ComputeInventoryValue` UDF のものと同じです。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

UDF メソッドの入力パラメーターは、対応する SQL 型であることに注意してください。 `UnitPrice` フィールドの `SqlMoney`、`UnitsInStock`の[`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) 、`SqlBoolean`の[`Discontinued`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx)です。 これらのデータ型には、`Products` テーブルで定義されている型が反映されます。 `UnitPrice` 列は `money`型、`smallint`型の `UnitsInStock` 列、および `Discontinued` 型の `bit`列です。

このコードは、最初に、値0が割り当てられた `inventoryValue` という名前の `SqlMoney` インスタンスを作成します。 `Products` テーブルでは、`UnitsInPrice` および `UnitsInStock` 列のデータベース `NULL` 値を使用できます。 したがって、最初に、これらの値に `NULL` s が含まれているかどうかを確認する必要があります。これは、`SqlMoney` オブジェクト s [`IsNull` プロパティ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)を使用して行います。 `UnitPrice` と `UnitsInStock` の両方に非`NULL` 値が含まれている場合は、その2つの製品である `inventoryValue` を計算します。 `Discontinued` が true の場合は、値を半分にします。

> [!NOTE]
> `SqlMoney` オブジェクトでは、2つの `SqlMoney` インスタンスを乗算できます。 `SqlMoney` インスタンスにリテラル浮動小数点数を乗算することはできません。 このため、`inventoryValue` を半分にするには、値0.5 を持つ新しい `SqlMoney` インスタンスで乗算します。

## <a name="step-11-deploying-the-managed-udf"></a>手順 11: マネージ UDF を展開する

マネージ UDF が作成されたので、Northwind データベースにデプロイする準備ができました。 手順 4. で見たように、SQL Server プロジェクト内の管理オブジェクトは、ソリューションエクスプローラーでプロジェクト名を右クリックし、コンテキストメニューから [配置] オプションを選択することによって配置されます。

プロジェクトを配置したら、SQL Server Management Studio に戻り、[スカラー値関数] フォルダーを更新します。 2つのエントリが表示されるようになります。

- `dbo.udf_ComputeInventoryValue`-手順 9. で作成した T-sql UDF と
- `dbo.udf ComputeInventoryValue_Managed`-配置されたばかりの手順10で作成したマネージ UDF。

このマネージ UDF をテストするには、Management Studio 内から次のクエリを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

このコマンドは、T-sql `udf_ComputeInventoryValue` UDF ではなく、マネージ `udf ComputeInventoryValue_Managed` UDF を使用しますが、出力は同じです。 図23に戻って、UDF の出力のスクリーンショットを参照してください。

## <a name="step-12-debugging-the-managed-database-objects"></a>手順 12: マネージデータベースオブジェクトのデバッグ

「[ストアドプロシージャのデバッグ](debugging-stored-procedures-vb.md)」のチュートリアルでは、Visual Studio を使用して SQL Server をデバッグするための3つのオプション (直接データベースデバッグ、アプリケーションデバッグ、SQL Server プロジェクトからのデバッグ) について説明しました。 マネージデータベースオブジェクトは、直接データベースデバッグを使用してデバッグすることはできませんが、クライアントアプリケーションからデバッグしたり、SQL Server プロジェクトから直接デバッグしたりすることはできます。 ただし、デバッグを機能させるには、SQL Server 2005 データベースで SQL/CLR デバッグを許可する必要があります。 最初に `ManagedDatabaseConstructs` プロジェクトを作成したときに、Visual Studio から SQL/CLR デバッグを有効にするかどうかをたずねるメッセージが表示されたことを思い出してください (手順2の図6を参照)。 この設定を変更するには、[サーバーエクスプローラー] ウィンドウでデータベースを右クリックします。

![データベースで SQL/CLR デバッグが許可されていることを確認する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**図 26**: データベースで SQL/CLR デバッグが許可されていることを確認する

`GetProductsWithPriceLessThan` マネージストアドプロシージャをデバッグすることを考えてみましょう。 まず、`GetProductsWithPriceLessThan` メソッドのコード内にブレークポイントを設定します。

[GetProductsWithPriceLessThan メソッドにブレークポイントを設定 ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**図 27**: `GetProductsWithPriceLessThan` メソッドにブレークポイントを設定[する (クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))

まず、SQL Server プロジェクトからマネージデータベースオブジェクトをデバッグする方法を見てみましょう。 このソリューションには2つのプロジェクトが含まれています。 `ManagedDatabaseConstructs` SQL Server プロジェクトと web サイトでは、SQL Server プロジェクトからデバッグするために、デバッグを開始するときに `ManagedDatabaseConstructs` SQL Server プロジェクトを起動するように Visual Studio に指示する必要があります。 ソリューションエクスプローラーで `ManagedDatabaseConstructs` プロジェクトを右クリックし、コンテキストメニューから [スタートアッププロジェクトに設定] オプションを選択します。

`ManagedDatabaseConstructs` プロジェクトをデバッガーから起動すると、`Test Scripts` フォルダーにある `Test.sql` ファイル内の SQL ステートメントが実行されます。 たとえば、`GetProductsWithPriceLessThan` マネージストアドプロシージャをテストするには、既存の `Test.sql` ファイルの内容を次のステートメントに置き換えます。これにより、`@CategoryID` の値14.95 で渡される `GetProductsWithPriceLessThan` マネージストアドプロシージャが呼び出されます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

上記のスクリプトを `Test.sql`に入力したら、[デバッグ] メニューに移動して [デバッグの開始] を選択するか、ツールバーの F5 キーまたは緑色の再生アイコンをクリックしてデバッグを開始します。 これにより、ソリューション内にプロジェクトがビルドされ、管理対象データベースオブジェクトが Northwind データベースに配置されて、`Test.sql` スクリプトが実行されます。 この時点で、ブレークポイントにヒットし、`GetProductsWithPriceLessThan` メソッドをステップ実行したり、入力パラメーターの値を調べたりすることができます。

[GetProductsWithPriceLessThan メソッド内のブレークポイントにヒットした ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**図 28**: `GetProductsWithPriceLessThan` メソッド内のブレークポイントにヒットしました ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png)されます)

クライアントアプリケーションを使用して SQL database オブジェクトをデバッグするには、アプリケーションのデバッグをサポートするようにデータベースを構成する必要があります。 サーバーエクスプローラーでデータベースを右クリックし、[アプリケーションのデバッグ] オプションがオンになっていることを確認します。 さらに、ASP.NET アプリケーションを構成して、SQL デバッガーと統合し、接続プールを無効にする必要があります。 これらの手順については、「[ストアドプロシージャのデバッグ](debugging-stored-procedures-vb.md)」チュートリアルの手順 2. で詳しく説明しました。

ASP.NET アプリケーションとデータベースを構成したら、ASP.NET web サイトをスタートアッププロジェクトとして設定し、デバッグを開始します。 ブレークポイントが設定されている管理オブジェクトの1つを呼び出すページにアクセスすると、アプリケーションが停止し、制御がデバッガーに対して有効になります。このとき、図28に示すようにコードをステップ実行できます。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>手順 13: マネージデータベースオブジェクトを手動でコンパイルして配置する

SQL Server プロジェクトを使用すると、管理されたデータベースオブジェクトの作成、コンパイル、および配置を簡単に行うことができます。 残念ながら、SQL Server プロジェクトは、Visual Studio の Professional および Team Systems エディションでのみ使用できます。 Visual Web Developer または Standard Edition の Visual Studio を使用していて、マネージデータベースオブジェクトを使用する場合は、手動で作成して配置する必要があります。 これには、次の4つのステップが含まれます。

1. マネージデータベースオブジェクトのソースコードを含むファイルを作成します。
2. オブジェクトをアセンブリにコンパイルします。
3. SQL Server 2005 データベースにアセンブリを登録します。
4. SQL Server に、アセンブリ内の適切なメソッドを指すデータベースオブジェクトを作成します。

これらのタスクを説明するために、を使用して、`UnitPrice` が指定した値より大きい製品を返す新しいマネージストアドプロシージャを作成します。 `GetProductsWithPriceGreaterThan.vb` という名前のコンピューターに新しいファイルを作成し、ファイルに次のコードを入力します (Visual Studio、メモ帳、または任意のテキストエディターを使用してこれを行うことができます)。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

このコードは、手順 5. で作成した `GetProductsWithPriceLessThan` メソッドのコードとほぼ同じです。 唯一の違いは、メソッド名、`WHERE` 句、およびクエリで使用されるパラメーター名です。 `GetProductsWithPriceLessThan` メソッドに戻り、`WHERE` 句 read: `WHERE UnitPrice < @MaxPrice`に戻します。 ここでは、`GetProductsWithPriceGreaterThan`で、`WHERE UnitPrice > @MinPrice` を使用します。

ここで、このクラスをコンパイルしてアセンブリにする必要があります。 コマンドラインで、`GetProductsWithPriceGreaterThan.vb` ファイルを保存したディレクトリに移動し、 C#コンパイラ (`csc.exe`) を使用してクラスファイルをアセンブリにコンパイルします。

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

`bc.exe` v を含むフォルダーがシステム `PATH`に含まれていない場合は、次のようにパスを完全に参照する必要があります。 `%WINDOWS%\Microsoft.NET\Framework\version\`は、次のようにします。

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[GetProductsWithPriceGreaterThan をアセンブリにコンパイル ![には](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**図 29**: アセンブリに `GetProductsWithPriceGreaterThan.vb` をコンパイル[する (クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png)されます)

`/t` フラグは、Visual Basic クラスファイルを (実行可能ファイルではなく) DLL にコンパイルする必要があることを指定します。 `/out` フラグは、結果として生成されるアセンブリの名前を指定します。

> [!NOTE]
> `GetProductsWithPriceGreaterThan.vb` クラスファイルをコマンドラインからコンパイルするのではなく、 [Visual Basic Express edition](https://msdn.microsoft.com/vstudio/express/vb/)を使用するか、Visual Studio Standard edition で別のクラスライブラリプロジェクトを作成することもできます。 S ren Jacob Lauritsen は、このような Visual Basic Express Edition プロジェクトを提供しています。このプロジェクトには、`GetProductsWithPriceGreaterThan` ストアドプロシージャ用のコードと、手順3、5、および10で作成した2つのマネージストアドプロシージャと UDF が用意されています。 また、の ren プロジェクトには、対応するデータベースオブジェクトを追加するために必要な T-sql コマンドも含まれています。

アセンブリにコンパイルされたコードを使用して、SQL Server 2005 データベース内にアセンブリを登録する準備ができました。 これを行うには、T-sql を使用するか、コマンド `CREATE ASSEMBLY`を使用するか、SQL Server Management Studio を使用します。 Management Studio の使用に重点を置いてみましょう。

Management Studio から、Northwind データベースの [プログラミング] フォルダーを展開します。 サブフォルダーの1つはアセンブリです。 新しいアセンブリをデータベースに手動で追加するには、[アセンブリ] フォルダーを右クリックし、コンテキストメニューの [新しいアセンブリ] をクリックします。 [新しいアセンブリ] ダイアログボックスが表示されます (図30を参照)。 [参照] ボタンをクリックして、コンパイルした `ManuallyCreatedDBObjects.dll` アセンブリを選択し、[OK] をクリックしてアセンブリをデータベースに追加します。 オブジェクトエクスプローラーに `ManuallyCreatedDBObjects.dll` アセンブリは表示されません。

[手動 Createddbo![dll アセンブリをデータベースに追加するには](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**図 30**: `ManuallyCreatedDBObjects.dll` アセンブリをデータベースに追加する ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png)されます)

![手動 Createddboの .dll がオブジェクトエクスプローラーに一覧表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**図 31**: `ManuallyCreatedDBObjects.dll` がオブジェクトエクスプローラーに一覧表示されます。

アセンブリは Northwind データベースに追加されましたが、ストアドプロシージャはアセンブリの `GetProductsWithPriceGreaterThan` メソッドに関連付けられています。 これを行うには、新しいクエリウィンドウを開き、次のスクリプトを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

これにより、`GetProductsWithPriceGreaterThan` という名前の Northwind データベースに新しいストアドプロシージャが作成され、マネージメソッド `GetProductsWithPriceGreaterThan` に関連付けられます (これは、アセンブリ `ManuallyCreatedDBObjects`にあるクラス `StoredProcedures`にあります)。

上記のスクリプトを実行した後、オブジェクトエクスプローラーの [ストアドプロシージャ] フォルダーを最新の状態に更新します。 新しいストアドプロシージャのエントリ `GetProductsWithPriceGreaterThan` が表示されます。これには、その横にロックアイコンがあります。 このストアドプロシージャをテストするには、クエリウィンドウで次のスクリプトを入力して実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

図32に示すように、上記のコマンドでは、`UnitPrice` が $24.95 を超える製品に関する情報が表示されます。

[手動 Createddbo![.dll がオブジェクトエクスプローラーに一覧表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**図 32**: オブジェクトエクスプローラーに `ManuallyCreatedDBObjects.dll` が表示されている ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png)されます)

## <a name="summary"></a>まとめ

Microsoft SQL Server 2005 は、共通言語ランタイム (CLR) との統合を提供します。これにより、マネージコードを使用してデータベースオブジェクトを作成できます。 以前は、これらのデータベースオブジェクトは T-sql を使用してのみ作成できましたが、Visual Basic などの .NET プログラミング言語を使用してこれらのオブジェクトを作成できるようになりました。 このチュートリアルでは、2つのマネージストアドプロシージャとマネージユーザー定義関数を作成しました。

Visual Studio s SQL Server プロジェクトの種類により、マネージデータベースオブジェクトの作成、コンパイル、配置が容易になります。 さらに、豊富なデバッグ機能が用意されています。 ただし、SQL Server プロジェクトの種類は、Visual Studio の Professional および Team Systems エディションでのみ使用できます。 Visual Web Developer または Standard Edition の Visual Studio を使用している場合は、手順 13. で説明したように、作成、コンパイル、および配置の手順を手動で実行する必要があります。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ユーザー定義関数の長所と短所](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [マネージコードでの SQL Server 2005 オブジェクトの作成](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005 でマネージコードを使用してトリガーを作成する](http://www.15seconds.com/issue/041006.htm)
- [方法: CLR SQL Server ストアドプロシージャを作成および実行する](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [方法: CLR SQL Server ユーザー定義関数を作成および実行する](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [方法: `Test.sql` スクリプトを編集して SQL オブジェクトを実行する](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [ユーザー定義関数の概要](http://www.sqlteam.com/item.asp?ItemID=1955)
- [マネージコードと SQL Server 2005 (ビデオ)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-SQL リファレンス](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [チュートリアル: マネージコードでのストアドプロシージャの作成](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Jacob Lauritsen でした。 この記事の内容を確認するだけでなく、この記事C#のダウンロードに含まれている Visual Express Edition プロジェクトを作成して、マネージデータベースオブジェクトを手動でコンパイルすることもできました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](debugging-stored-procedures-vb.md)
