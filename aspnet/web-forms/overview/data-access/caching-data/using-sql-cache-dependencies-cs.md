---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: SQL キャッシュの依存関係C#を使用する () |Microsoft Docs
author: rick-anderson
description: 最も簡単なキャッシュ方法は、キャッシュされたデータの有効期限が指定した期間後に切れるようにすることです。 ただし、この簡単な方法では、キャッシュされたデータが
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bc27a08e39606c25b8f99d6ea057d2a853f08a6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443086"
---
# <a name="using-sql-cache-dependencies-c"></a>SQL キャッシュ依存関係を使用する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip)または[PDF のダウンロード](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> 最も簡単なキャッシュ方法は、キャッシュされたデータの有効期限が指定した期間後に切れるようにすることです。 ただし、この簡単な方法では、キャッシュされたデータが基になるデータソースと関連付けられていないことを意味します。その結果、古いデータが長すぎるか、現在のデータが短時間で期限切れになります。 より優れたアプローチは、SqlCacheDependency クラスを使用して、SQL データベースで基になるデータが変更されるまでデータがキャッシュされたままになるようにすることです。 このチュートリアルでは、その方法を説明します。

## <a name="introduction"></a>はじめに

アーキテクチャチュートリアルの ObjectDataSource および[キャッシュデータ](caching-data-in-the-architecture-cs.md)[を使用](caching-data-with-the-objectdatasource-cs.md)してデータをキャッシュするキャッシュ技法では、時間ベースの有効期限を使用して、指定した期間の経過後にキャッシュからデータを削除しました。 この方法は、データ staleness に対するキャッシュのパフォーマンス向上のバランスを取るための最も簡単な方法です。 時間の有効期限を*x*秒に設定すると、ページ開発者は、キャッシュのパフォーマンス上のメリットを*x*秒だけで concedes ことができます。ただし、データが最大で*x*秒を超えないようにすることは簡単です。 もちろん、静的なデータの場合、 *x*は web アプリケーションの有効期間に拡張できます。これは、「[アプリケーションの起動時にデータをキャッシュ](caching-data-at-application-startup-cs.md)する」チュートリアルで確認したものです。

データベースデータをキャッシュする場合、時間ベースの有効期限は使いやすいものとして選択されることがよくありますが、多くの場合、不適切な解決策になります。 データベース内の基になるデータが変更されるまで、データベースのデータはキャッシュされたままになることが理想的です。その後、キャッシュは削除されます。 この方法では、キャッシュのパフォーマンス上の利点が最大限に向上し、古いデータの存続期間を最小限に抑えることができます。 ただし、これらの利点を活用するためには、基になるデータベースデータが変更されたことを認識し、対応する項目をキャッシュから見つけするシステムがいくつか存在している必要があります。 ASP.NET 2.0 より前のページ開発者は、このシステムの実装を担当していました。

ASP.NET 2.0 は、対応するキャッシュされた項目を削除できるように、データベース内で変更が発生したことを判断するために[`SqlCacheDependency` クラス](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)および必要なインフラストラクチャを提供します。 基になるデータがどのように変更されたかを判断するには、通知とポーリングの2つの方法があります。 通知とポーリングの違いについて説明した後、ポーリングをサポートするために必要なインフラストラクチャを作成し、宣言型のシナリオやプログラムによるシナリオで `SqlCacheDependency` クラスを使用する方法について説明します。

## <a name="understanding-notification-and-polling"></a>通知とポーリングについて

データベース内のデータが変更された日時を判断するには、通知とポーリングの2つの手法を使用できます。 通知を使用すると、クエリが最後に実行されてから特定のクエリの結果が変更されたときに、そのクエリに関連付けられているキャッシュされた項目が削除された時点で、データベースは ASP.NET ランタイムに自動的に警告します。 データベースサーバーは、ポーリングを使用して、特定のテーブルが最後に更新された日時に関する情報を保持します。 ASP.NET ランタイムは、データベースを定期的にポーリングして、キャッシュに入ってから変更されたテーブルを確認します。 データが変更されているテーブルには、関連付けられているキャッシュ項目が削除されます。

通知オプションは、ポーリングよりも設定が少なくて済むため、テーブルレベルではなくクエリレベルで変更が追跡されるため、より詳細な設定が必要になります。 残念ながら、通知は Microsoft SQL Server 2005 (つまり、Express 以外のエディション) の全エディションでのみ利用できます。 ただし、ポーリングオプションは、7.0 から2005のすべてのバージョンの Microsoft SQL Server に使用できます。 これらのチュートリアルでは SQL Server 2005 の Express edition を使用しているため、ポーリングオプションの設定と使用について重点的に説明します。 SQL Server 2005 s の通知機能に関するその他のリソースについては、このチュートリアルの最後にある「参考資料」セクションを参照してください。

ポーリングを使用する場合、データベースは、`tableName`、`notificationCreated`、および `changeId`の3つの列を持つ `AspNet_SqlCacheTablesForChangeNotification` という名前のテーブルを含めるように構成する必要があります。 このテーブルには、web アプリケーションの SQL キャッシュ依存関係で使用する必要があるデータを含むテーブルごとに1行のデータが格納されます。 `tableName` 列はテーブルの名前を指定し、`notificationCreated` はテーブルに行が追加された日付と時刻を示します。 `changeId` 列の型は `int` で、初期値は0です。 この値は、テーブルへの変更ごとにインクリメントされます。

データベースでは、`AspNet_SqlCacheTablesForChangeNotification` テーブルに加えて、SQL キャッシュ依存関係に表示される可能性のある各テーブルにトリガーを含める必要もあります。 これらのトリガーは、行が挿入、更新、または削除されるたびに実行され、テーブルの `changeId` 値が `AspNet_SqlCacheTablesForChangeNotification`でインクリメントされます。

ASP.NET ランタイムは、`SqlCacheDependency` オブジェクトを使用してデータをキャッシュするときに、テーブルの現在の `changeId` を追跡します。 データベースは定期的にチェックされ、`changeId` がデータベース内の値と異なる `SqlCacheDependency` オブジェクトは削除されます。これは、データがキャッシュされてからテーブルに変更があったことを示す `changeId` 値が異なるためです。

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>手順 1:`aspnet_regsql.exe`コマンドラインプログラムを探索する

ポーリング方法を使用する場合、データベースは、前述のインフラストラクチャを格納するようにセットアップする必要があります。定義済みのテーブル (`AspNet_SqlCacheTablesForChangeNotification`)、いくつかのストアドプロシージャ、および web アプリケーションの SQL キャッシュの依存関係で使用できる各テーブルのトリガーです。 これらのテーブル、ストアドプロシージャ、およびトリガーは、`$WINDOWS$\Microsoft.NET\Framework\version` フォルダーにあるコマンドラインプログラム `aspnet_regsql.exe`を使用して作成できます。 `AspNet_SqlCacheTablesForChangeNotification` テーブルと関連するストアドプロシージャを作成するには、コマンドラインから次のコマンドを実行します。

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> これらのコマンドを実行するには、指定されたデータベースログインが[`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx)ロールと[`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx)ロールに存在する必要があります。 `aspnet_regsql.exe` コマンドラインプログラムによってデータベースに送信された T-sql を確認するには、こちらの[ブログエントリ](http://scottonwriting.net/sowblog/posts/10709.aspx)を参照してください。

たとえば、Windows 認証を使用して `ScottsServer` という名前のデータベースサーバーで `pubs` という名前の Microsoft SQL Server データベースにポーリングするためのインフラストラクチャを追加するには、適切なディレクトリに移動し、コマンドラインで次のように入力します。

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

データベースレベルのインフラストラクチャを追加した後、SQL キャッシュの依存関係で使用されるこれらのテーブルにトリガーを追加する必要があります。 `aspnet_regsql.exe` コマンドラインプログラムをもう一度使用しますが、`-t` スイッチを使用してテーブル名を指定し、`-ed` スイッチを使用するのではなく、次のように `-et`を使用します。

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

`ScottsServer`上の `pubs` データベースの `authors` テーブルおよび `titles` テーブルにトリガーを追加するには、次のように使用します。

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

このチュートリアルでは、トリガーを `Products`、`Categories`、および `Suppliers` テーブルに追加します。 ここでは、手順 3. の特定のコマンドライン構文について説明します。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>手順 2:`App_Data` で Microsoft SQL Server 2005 Express Edition データベースを参照する

`aspnet_regsql.exe` コマンドラインプログラムでは、必要なポーリングインフラストラクチャを追加するために、データベースとサーバー名が必要です。 ただし、`App_Data` フォルダーに存在する Microsoft SQL Server 2005 Express データベースのデータベースとサーバー名は何ですか。 データベースとサーバーの名前を調べる必要はありません。最も簡単な方法は、データベースを `localhost\SQLExpress` データベースインスタンスにアタッチし、 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)を使用してデータの名前を変更することです。 SQL Server 2005 の全バージョンがコンピューターにインストールされている場合は、既にコンピューターに SQL Server Management Studio がインストールされている可能性があります。 Express edition のみを使用している場合は、無料の[Microsoft SQL Server Management Studio Express edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)をダウンロードできます。

まず、Visual Studio を終了します。 次に、SQL Server Management Studio を開き、Windows 認証を使用して `localhost\SQLExpress` サーバーへの接続を選択します。

![Localhost\SQLExpress サーバーにアタッチする](using-sql-cache-dependencies-cs/_static/image1.gif)

**図 1**: `localhost\SQLExpress` サーバーにアタッチする

サーバーに接続すると、Management Studio にサーバーが表示され、データベース、セキュリティなどのサブフォルダーが表示されます。 Databases フォルダーを右クリックし、[アタッチ] オプションを選択します。 [データベースのアタッチ] ダイアログボックスが表示されます (図2を参照)。 [追加] ボタンをクリックし、web アプリケーション s `App_Data` フォルダー内の `NORTHWND.MDF` データベースフォルダーを選択します。

[NORTHWND.MDF をアタッチ ![ます。App_Data フォルダーからの MDF データベース](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**図 2**: `App_Data` フォルダーから `NORTHWND.MDF` データベースをアタッチする ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image2.png)されます)

これにより、データベースが [データベース] フォルダーに追加されます。 データベース名には、データベースファイルへの完全なパス、または[GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)を付加した完全パスを指定できます。 Aspnet\_のコマンドラインツールを使用するときに、この長いデータベース名を入力する必要がないようにするには、アタッチしたデータベースを右クリックし、[名前の変更] を選択して、データベースの名前をよりわかりやすい名前に変更します。 データベースの名前を DataTutorials に変更しました。

![アタッチされたデータベースの名前を、よりわかりやすい名前に変更します。](using-sql-cache-dependencies-cs/_static/image3.gif)

**図 3**: アタッチされたデータベースの名前を人にわかりやすい名前に変更する

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>手順 3: ポーリングインフラストラクチャを Northwind データベースに追加する

これで、`App_Data` フォルダーから `NORTHWND.MDF` データベースがアタッチされたので、ポーリングインフラストラクチャを追加する準備が整いました。 データベースの名前を DataTutorials に変更した場合は、次の4つのコマンドを実行します。

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

これらの4つのコマンドを実行した後、Management Studio でデータベース名を右クリックし、[タスク] サブメニューにアクセスして、[デタッチ] を選択します。 次に、Management Studio を閉じて、Visual Studio を再度開きます。

Visual Studio を再び開いたら、サーバーエクスプローラーを使用してデータベースをドリルダウンします。 新しいテーブル (`AspNet_SqlCacheTablesForChangeNotification`)、新しいストアドプロシージャ、および `Products`、`Categories`、および `Suppliers` テーブルのトリガーに注意してください。

![データベースに必要なポーリングインフラストラクチャが含まれるようになりました](using-sql-cache-dependencies-cs/_static/image4.gif)

**図 4**: データベースに必要なポーリングインフラストラクチャが含まれるようになった

## <a name="step-4-configuring-the-polling-service"></a>手順 4: ポーリングサービスを構成する

データベースに必要なテーブル、トリガー、およびストアドプロシージャを作成したら、最後の手順として、ポーリングサービスを構成します。これは、使用するデータベースとポーリング頻度をミリ秒単位で指定することによって `Web.config` によって行われます。 次のマークアップは、1秒ごとに Northwind データベースをポーリングします。

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

`<add>` 要素 (NorthwindDB) の `name` 値により、ユーザーが判読できる名前が特定のデータベースに関連付けられます。 SQL キャッシュの依存関係を使用する場合は、ここで定義されているデータベース名と、キャッシュされたデータの基になっているテーブルを参照する必要があります。 `SqlCacheDependency` クラスを使用して、手順 6. で SQL キャッシュの依存関係とキャッシュされたデータをプログラムで関連付ける方法について説明します。

SQL キャッシュの依存関係が確立されると、ポーリングシステムは、`<databases>` 要素で定義されているデータベースに `pollTime` ミリ秒ごとに接続し、`AspNet_SqlCachePollingStoredProcedure` ストアドプロシージャを実行します。 このストアドプロシージャは `aspnet_regsql.exe` コマンドラインツールを使用して手順3で戻されました。 `AspNet_SqlCacheTablesForChangeNotification`内の各レコードの `tableName` と `changeId` の値を返します。 古くなった SQL キャッシュ依存関係はキャッシュから削除されます。

`pollTime` 設定では、パフォーマンスとデータ staleness のトレードオフが発生します。 `pollTime` 値を小さくすると、データベースへの要求数が増加しますが、キャッシュから古いデータをより迅速に見つけます。 `pollTime` 値を大きくすると、データベース要求の数が減少しますが、バックエンドデータが変更されてから関連するキャッシュ項目が削除されるまでの間の遅延が増加します。 幸いなことに、データベース要求では、単純な簡易テーブルから少数の行を返す単純なストアドプロシージャを実行しています。 ただし、アプリケーションのデータベースアクセスとデータ staleness の間で最適なバランスを見つけるために、さまざまな `pollTime` 値を試してみることをお勧めします。 許容される最小 `pollTime` 値は500です。

> [!NOTE]
> 上の例では、`<sqlCacheDependency>` 要素に1つの `pollTime` 値を指定していますが、必要に応じて `<add>` 要素の `pollTime` 値を指定することもできます。 これは、複数のデータベースを指定し、データベースごとにポーリング頻度をカスタマイズする場合に便利です。

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>手順 5: SQL キャッシュの依存関係を宣言的に操作する

手順 1. ~ 4. で、必要なデータベースインフラストラクチャを設定し、ポーリングシステムを構成する方法を説明しました。 このインフラストラクチャが整ったら、プログラムまたは宣言的手法を使用して、関連付けられた SQL キャッシュ依存関係を持つ項目をデータキャッシュに追加できるようになりました。 この手順では、SQL キャッシュの依存関係を宣言によって操作する方法を確認します。 手順 6. では、プログラムによるアプローチについて説明します。

[Objectdatasource チュートリアルを使用したキャッシュデータ](caching-data-with-the-objectdatasource-cs.md)では、objectdatasource の宣言型キャッシュ機能について説明しています。 単に `EnableCaching` プロパティを `true` に設定し、`CacheDuration` プロパティを一定の時間間隔に設定すると、ObjectDataSource は、基になるオブジェクトから返されたデータを指定された間隔で自動的にキャッシュします。 ObjectDataSource では、1つまたは複数の SQL キャッシュの依存関係を使用することもできます。

SQL キャッシュの依存関係を宣言によって使用する方法を示すには、`Caching` フォルダーの [`SqlCacheDependencies.aspx`] ページを開き、[ツールボックス] からデザイナーに GridView をドラッグします。 GridView の `ID` を `ProductsDeclarative` に設定し、そのスマートタグから、`ProductsDataSourceDeclarative`という名前の新しい ObjectDataSource にバインドするように選択します。

[新しい ObjectDataSource という名前の ![を作成します。](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**図 5**: `ProductsDataSourceDeclarative` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image4.png)される)

`ProductsBLL` クラスを使用するように ObjectDataSource を構成し、[選択] タブのドロップダウンリストを `GetProducts()`に設定します。 [更新] タブで、3つの入力パラメーター (`productName`、`unitPrice`、および `productID`) を使用して、`UpdateProduct` のオーバーロードを選択します。 [挿入] タブと [削除] タブで、ドロップダウンリストを [(なし)] に設定します。

[3つの入力パラメーターで UpdateProduct オーバーロードを使用 ![](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**図 6**: 3 つの入力パラメーターを使用して Updateproduct オーバーロードを使用する ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image6.png)されます)

[[挿入] タブと [削除] タブで、ドロップダウンリストを [(なし)] に設定 ![ます。](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**図 7**: 挿入と削除のタブでドロップダウンリストを (なし) に設定する ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image8.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、各データフィールドの GridView に BoundFields と CheckBoxFields が作成されます。 すべてのフィールドを削除し、`ProductName`、`CategoryName`、および `UnitPrice`を指定して、これらのフィールドの書式を調整します。 GridView s スマートタグから、[ページングを有効にする]、[並べ替えを有効にする]、および [編集を有効にする] チェックボックスをオンにします。 Visual Studio によって、ObjectDataSource s `OldValuesParameterFormatString` プロパティが `original_{0}`に設定されます。 GridView s edit 機能を正常に動作させるには、このプロパティを宣言構文から完全に削除するか、または `{0}`を既定値に設定し直す必要があります。

最後に、GridView の上にラベル Web コントロールを追加し、その `ID` プロパティを `ODSEvents` に設定し、その `EnableViewState` プロパティを `false`に設定します。 これらの変更を行った後、ページの宣言型マークアップは次のようになります。 SQL キャッシュの依存関係機能を示すために必要ではない GridView フィールドに対して、いくつかのカスタマイズされたカスタマイズを行ったことに注意してください。

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

次に、ObjectDataSource s `Selecting` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

ObjectDataSource s `Selecting` イベントは、基になるオブジェクトからデータを取得するときにのみ発生することを思い出してください。 ObjectDataSource が独自のキャッシュからデータにアクセスする場合、このイベントは発生しません。

ここでは、ブラウザーを使用してこのページにアクセスします。 まだキャッシュを実装していないので、グリッドをページ表示、並べ替え、または編集するたびに、図8に示すように、ページに [イベントが発生しました] というテキストが表示されます。

[GridView がページング、編集、または並べ替えられるたびに、ObjectDataSource s 選択イベントが発生する ![ます。](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**図 8**: GridView がページング、編集、または並べ替えされるたびに ([クリックしてフルサイズのイメージを表示](using-sql-cache-dependencies-cs/_static/image10.png))、ObjectDataSource s `Selecting` イベントが発生する

「 [Objectdatasource チュートリアルを使用](caching-data-with-the-objectdatasource-cs.md)したデータのキャッシュ」で説明したように、`EnableCaching` プロパティを `true` に設定すると、objectdatasource は `CacheDuration` プロパティによって指定された期間のデータをキャッシュします。 ObjectDataSource には、 [`SqlCacheDependency` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)もあります。このプロパティは、次のパターンを使用して、キャッシュされたデータに1つ以上の SQL キャッシュの依存関係を追加します。

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

ここで、 *databaseName*は `Web.config`の `<add>` 要素の `name` 属性で指定されているデータベースの名前です。 *tableName*はデータベーステーブルの名前です。 たとえば、Northwind s `Products` テーブルに対する SQL キャッシュの依存関係に基づいてデータを無期限にキャッシュする ObjectDataSource を作成するには、ObjectDataSource s `EnableCaching` プロパティを `true` に設定し、その `SqlCacheDependency` プロパティを NorthwindDB: Products に設定します。

> [!NOTE]
> SQL キャッシュ依存関係*と*時間ベースの有効期限を使用するには、`EnableCaching` を `true`に設定し、時間間隔に `CacheDuration` して、データベースとテーブル名に `SqlCacheDependency` します。 時間ベースの有効期限に達した場合、または、基になるデータベースデータが変更されたことがポーリングシステムによって記録された場合、ObjectDataSource はデータを削除します。

`SqlCacheDependencies.aspx` の GridView では、`Products` と `Categories` の2つのテーブルのデータが表示されます (product s `CategoryName` フィールドは `JOIN` の `Categories`を使用して取得されます)。 そのため、SQL キャッシュの依存関係を2つ指定します。 NorthwindDB: Products;NorthwindDB: カテゴリ。

[製品とカテゴリで SQL キャッシュの依存関係を使用してキャッシュをサポートするように ObjectDataSource を構成 ![には](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**図 9**: `Products` および `Categories` で SQL キャッシュの依存関係を使用してキャッシュをサポートするように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](using-sql-cache-dependencies-cs/_static/image12.png))

キャッシュをサポートするように ObjectDataSource を構成したら、ブラウザーを使用してページに戻ります。 ここでも、[編集] ボタンまたは [キャンセル] ボタンをクリックすると、最初のページに移動したときに表示されるテキスト選択イベントが表示されます。 これは、データが ObjectDataSource s キャッシュに読み込まれた後、`Products` または `Categories` テーブルが変更されるか、GridView によってデータが更新されるまで、データはそのまま残されるためです。

グリッドをページングし、選択したイベントが発生したテキストがないことを通知した後、新しいブラウザーウィンドウを開き、[編集]、[挿入]、[削除] セクション (`~/EditInsertDelete/Basics.aspx`) の基本チュートリアルに移動します。 製品の名前または価格を更新します。 次に、最初のブラウザーウィンドウに対して、別のデータページを表示するか、グリッドを並べ替えるか、または行 s の [編集] ボタンをクリックします。 この時点で、基になるデータベースデータが変更されたため、選択したイベントが再表示されます (図10を参照)。 テキストが表示されない場合は、しばらく待ってからもう一度やり直してください。 ポーリングサービスは `pollTime` ミリ秒ごとに `Products` テーブルに対する変更を確認しているので、基になるデータが更新されてからキャッシュされたデータが削除されるまでには遅延があります。

[見つけテーブルを変更して、キャッシュされた製品データをする ![](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**図 10**: Products テーブルを変更してキャッシュされた製品データを見つけ[する (クリックしてフルサイズの画像を表示する](using-sql-cache-dependencies-cs/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>手順 6: プログラムで`SqlCacheDependency`クラスを操作する

アーキテクチャチュートリアルの[キャッシュデータ](caching-data-in-the-architecture-cs.md)は、キャッシュと ObjectDataSource を密に結合するのではなく、アーキテクチャで個別のキャッシュレイヤーを使用する利点を確認しました。 このチュートリアルでは、データキャッシュをプログラムで操作する方法を示す `ProductsCL` クラスを作成しました。 キャッシュレイヤーで SQL キャッシュの依存関係を利用するには、`SqlCacheDependency` クラスを使用します。

ポーリングシステムでは、`SqlCacheDependency` オブジェクトが特定のデータベースとテーブルのペアに関連付けられている必要があります。 たとえば、次のコードでは、Northwind データベースの `Products` テーブルに基づいて `SqlCacheDependency` オブジェクトを作成します。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

`SqlCacheDependency` s コンストラクターへの2つの入力パラメーターは、それぞれデータベース名とテーブル名です。 ObjectDataSource s `SqlCacheDependency` プロパティと同様に、使用されるデータベース名は `Web.config`の `<add>` 要素の `name` 属性で指定された値と同じです。 テーブル名は、データベーステーブルの実際の名前です。

データキャッシュに追加された項目に `SqlCacheDependency` を関連付けるには、依存関係を受け入れる `Insert` メソッドオーバーロードのいずれかを使用します。 次のコードでは、永続的な期間のデータキャッシュに*値*を追加しますが、それを `Products` テーブルの `SqlCacheDependency` に関連付けます。 つまり、メモリの制約によって削除されるまで、またはポーリングシステムによって `Products` テーブルがキャッシュされてから変更されたことが検出されるまで、*値*はキャッシュに保持されます。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

キャッシュレイヤー s `ProductsCL` クラスは、時間ベースの有効期限60秒を使用して、`Products` テーブルのデータを現在キャッシュしています。 代わりに、SQL キャッシュの依存関係を使用するように、このクラスを更新してみましょう。 データをキャッシュに追加するための `ProductsCL` クラス s `AddCacheItem` メソッドには、現在、次のコードが含まれています。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

`MasterCacheKeyArray` キャッシュ依存関係の代わりに `SqlCacheDependency` オブジェクトを使用するように、このコードを更新します。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

この機能をテストするには、gridview を既存の `ProductsDeclarative` GridView の下のページに追加します。 この新しい GridView s `ID` を `ProductsProgrammatic` に設定し、そのスマートタグを通じて、`ProductsDataSourceProgrammatic`という名前の新しい ObjectDataSource にバインドします。 `ProductsCL` クラスを使用するように ObjectDataSource を構成し、[選択] タブと [更新] タブのドロップダウンリストにそれぞれ `GetProducts` と `UpdateProduct`を設定します。

[ProductsCL クラスを使用するように ObjectDataSource を構成 ![には](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**図 11**: `ProductsCL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](using-sql-cache-dependencies-cs/_static/image16.png))

[[SELECT Tab s] ドロップダウンリストから GetProducts メソッドを選択 ![ます。](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**図 12**: [select Tab s] ドロップダウンリストから `GetProducts` メソッドを選択[する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image18.png)されます)

[![[更新] タブのドロップダウンリストから UpdateProduct メソッドを選択します。](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**図 13**: [更新] タブのドロップダウンリストから Updateproduct メソッドを選択[する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-cs/_static/image20.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、各データフィールドの GridView に BoundFields と CheckBoxFields が作成されます。 このページに最初に追加された GridView と同様に、`ProductName`、`CategoryName`、および `UnitPrice`のすべてのフィールドを削除し、必要に応じてこれらのフィールドの書式を設定します。 GridView s スマートタグから、[ページングを有効にする]、[並べ替えを有効にする]、および [編集を有効にする] チェックボックスをオンにします。 `ProductsDataSourceDeclarative` ObjectDataSource と同様に、Visual Studio は `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` プロパティを `original_{0}`に設定します。 GridView s edit 機能が正常に機能するためには、このプロパティを `{0}` に戻します (または、プロパティの割り当てを宣言構文から完全に削除します)。

これらのタスクを完了すると、結果として得られる GridView および ObjectDataSource の宣言マークアップは次のようになります。

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

キャッシュ層で SQL キャッシュの依存関係をテストするには、`ProductCL` クラス s `AddCacheItem` メソッドにブレークポイントを設定し、デバッグを開始します。 最初に `SqlCacheDependencies.aspx`にアクセスしたときに、データが最初に要求され、キャッシュに格納されるため、ブレークポイントに達する必要があります。 次に、GridView 内の別のページに移動するか、いずれかの列を並べ替えます。 これにより、GridView はデータを再クエリしますが、`Products` データベーステーブルが変更されていないため、データがキャッシュ内に存在する必要があります。 データがキャッシュに繰り返し見つからない場合は、コンピューターに十分なメモリがあることを確認してから、もう一度やり直してください。

GridView のいくつかのページを使用してページングを行った後、2番目のブラウザーウィンドウを開き、[編集]、[挿入]、[削除] セクション (`~/EditInsertDelete/Basics.aspx`) の基本チュートリアルに移動します。 Products テーブルからレコードを更新してから、最初のブラウザーウィンドウから新しいページを表示するか、並べ替えヘッダーのいずれかをクリックします。

このシナリオでは、次の2つのいずれかが表示されます。ブレークポイントがヒットすると、データベースの変更によってキャッシュデータが削除されたことを示します。または、ブレークポイントにヒットしません。つまり、`SqlCacheDependencies.aspx` に古いデータが表示されるようになります。 ブレークポイントにヒットしない場合は、データが変更されてからポーリングサービスがまだ起動していない可能性があります。 ポーリングサービスは `pollTime` ミリ秒ごとに `Products` テーブルに対する変更を確認しているので、基になるデータが更新されてからキャッシュされたデータが削除されるまでには遅延があります。

> [!NOTE]
> この遅延は、`SqlCacheDependencies.aspx`の GridView で製品の1つを編集するときに表示される可能性が高くなります。 アーキテクチャチュートリアルの[キャッシュデータ](caching-data-in-the-architecture-cs.md)では、`MasterCacheKeyArray` キャッシュ依存関係を追加して、`ProductsCL` クラス s `UpdateProduct` メソッドを使用して編集されるデータがキャッシュから削除されたことを確認しました。 ただし、この手順の前半で `AddCacheItem` メソッドを変更するときには、このキャッシュの依存関係を置き換えました。したがって、`ProductsCL` クラスは、ポーリングシステムが `Products` テーブルに変更を記録するまで、キャッシュされたデータを引き続き表示します。 手順 7. で `MasterCacheKeyArray` キャッシュの依存関係を再度導入する方法について説明します。

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>手順 7: キャッシュされた項目に複数の依存関係を関連付ける

`MasterCacheKeyArray` キャッシュの依存関係を使用して、*すべて*の製品関連データが、関連付けられている1つの項目が更新されたときにキャッシュから確実に削除されることを思い出してください。 たとえば、`GetProductsByCategoryID(categoryID)` メソッドでは、一意の*categoryID*値ごとに `ProductsDataTables` インスタンスがキャッシュされます。 これらのオブジェクトのいずれかが削除されると、`MasterCacheKeyArray` キャッシュの依存関係によって、他のオブジェクトも削除されます。 このキャッシュ依存関係がない場合、キャッシュされたデータが変更されると、他のキャッシュされた製品データが古くなっている可能性があります。 そのため、SQL キャッシュの依存関係を使用する場合は、`MasterCacheKeyArray` キャッシュの依存関係を維持することが重要です。 ただし、data cache s `Insert` メソッドでは、1つの依存関係オブジェクトのみが許可されます。

さらに、SQL キャッシュの依存関係を使用する場合は、複数のデータベーステーブルを依存関係として関連付けることが必要になる場合があります。 たとえば、`ProductsCL` クラスにキャッシュされた `ProductsDataTable` には、各製品のカテゴリ名と業者名が含まれていますが、`AddCacheItem` 方法では `Products`に対する依存関係のみが使用されます。 この場合、ユーザーがカテゴリまたは供給業者の名前を更新すると、キャッシュされた製品データはキャッシュに残り、期限切れになります。 したがって、キャッシュされた製品データは、`Products` テーブルだけでなく、`Categories` テーブルと `Suppliers` テーブルにも依存するようにします。

[`AggregateCacheDependency` クラス](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)は、複数の依存関係をキャッシュ項目に関連付けるための手段を提供します。 まず、`AggregateCacheDependency` インスタンスを作成します。 次に、`AggregateCacheDependency` s `Add` メソッドを使用して、依存関係のセットを追加します。 その後、データキャッシュに項目を挿入する場合は、`AggregateCacheDependency` インスタンスを渡します。 `AggregateCacheDependency` インスタンスの*いずれか*の依存関係が変更されると、キャッシュされた項目は削除されます。

`ProductsCL` クラス s `AddCacheItem` メソッドの更新されたコードを次に示します。 メソッドは、`Products`、`Categories`、および `Suppliers` テーブルの `SqlCacheDependency` オブジェクトと共に `MasterCacheKeyArray` キャッシュ依存関係を作成します。 これらはすべて、`aggregateDependencies`という名前の1つの `AggregateCacheDependency` オブジェクトに結合され、その後 `Insert` メソッドに渡されます。

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

この新しいコードをテストします。これで、`Products`、`Categories`、または `Suppliers` テーブルに変更が加えられたため、キャッシュされたデータが削除されます。 さらに、`ProductsCL` クラス s `UpdateProduct` メソッドは、GridView を通じて製品を編集するときに呼び出されます。このメソッドは、キャッシュ依存関係の `MasterCacheKeyArray` を見つけします。これにより、キャッシュされた `ProductsDataTable` が削除され、次の要求でデータが再取得されます。

> [!NOTE]
> SQL キャッシュの依存関係は、[出力キャッシュ](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)と共に使用することもできます。 この機能のデモンストレーションについては、「 [SQL Server での ASP.NET 出力キャッシュの使用](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)」を参照してください。

## <a name="summary"></a>まとめ

データベースデータをキャッシュする場合、データはデータベースで変更されるまでキャッシュに保持されるのが理想的です。 ASP.NET 2.0 を使用すると、SQL キャッシュの依存関係を作成し、宣言型とプログラムによる両方のシナリオで使用できます。 この方法の課題の1つは、データが変更されたときの検出です。 Microsoft SQL Server 2005 の完全バージョンでは、クエリの結果が変更されたときにアプリケーションを警告できる通知機能を提供します。 SQL Server 2005 とそれ以前のバージョンの SQL Server の Express Edition では、代わりにポーリングシステムを使用する必要があります。 幸いにも、必要なポーリングインフラストラクチャの設定は非常に簡単です。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [Microsoft SQL Server 2005 でのクエリ通知の使用](https://msdn.microsoft.com/library/ms175110.aspx)
- [クエリ通知の作成](https://msdn.microsoft.com/library/ms188669.aspx)
- [`SqlCacheDependency` クラスを使用した ASP.NET でのキャッシュ](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 登録ツール (`aspnet_regsql.exe`)](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [`SqlCacheDependency` の概要](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Marko Rangel、Teresa Murphy、および Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](caching-data-at-application-startup-cs.md)
> [次へ](caching-data-with-the-objectdatasource-vb.md)
