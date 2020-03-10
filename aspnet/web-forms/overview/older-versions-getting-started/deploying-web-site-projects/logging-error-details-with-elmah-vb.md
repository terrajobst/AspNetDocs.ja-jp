---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
title: ELMAH でエラーの詳細をログに記録する (VB) |Microsoft Docs
author: rick-anderson
description: エラーログモジュールとハンドラー (ELMAH) は、運用環境で実行時エラーをログに記録するための別の方法を提供します。 ELMAH は無料のオープンソースエラーです...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: a5f0439f-18b2-4c89-96ab-75b02c616f46
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
msc.type: authoredcontent
ms.openlocfilehash: 46b7fc22807c8cb9f47ff035639815d7b6104735
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421906"
---
# <a name="logging-error-details-with-elmah-vb"></a>ELMAH でエラーの詳細をログに記録する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_vb.pdf)

> エラーログモジュールとハンドラー (ELMAH) は、運用環境で実行時エラーをログに記録するための別の方法を提供します。 ELMAH は、オープンソースのエラーログライブラリです。このライブラリには、エラーのフィルター処理や、web ページからのエラーログの表示、RSS フィードの表示、コンマ区切りファイルとしてのダウンロードなどの機能が含まれています。 このチュートリアルでは、ELMAH のダウンロードと構成について説明します。

## <a name="introduction"></a>はじめに

[前のチュートリアル](logging-error-details-with-asp-net-health-monitoring-vb.md)では、ASP を検証しています。ネットワークの正常性監視システム。広範な Web イベントを記録するための、すぐに使用できるライブラリが用意されています。 多くの開発者は、正常性監視を使用して、未処理の例外の詳細をログに記録し、電子メールで送信します。 ただし、このシステムにはいくつかの問題点があります。 1つ目は、ログに記録されたイベントに関する情報を表示するためのユーザーインターフェイスがないことです。 過去10回のエラーの概要を表示する場合、または先週発生したエラーの詳細を表示する場合は、データベースをからかうするか、電子メールの受信トレイをスキャンするか、または `aspnet_WebEvent_Events` テーブルからの情報を表示する web ページを作成する必要があります。

もう1つの問題点は、稼動状況の監視の複雑さを中心にしています。 正常性の監視を使用して大量のイベントを記録することができます。また、イベントをログに記録する方法とタイミングを指定するさまざまなオプションがあるため、正常性監視システムを正しく構成することは煩雑タスクになる可能性があります。 最後に、互換性の問題があります。 正常性の監視は、バージョン2.0 の .NET Framework に最初に追加されたため、ASP.NET バージョン1.x を使用して作成された古い web アプリケーションでは使用できません。 さらに、前のチュートリアルで使用した `SqlWebEventProvider` クラスは、エラーの詳細をデータベースに記録するために、Microsoft SQL Server データベースでのみ機能します。 XML ファイルや Oracle データベースなどの代替データストアにエラーを記録する必要がある場合は、カスタムログプロバイダークラスを作成する必要があります。

正常性監視システムの代替手段は、 [Atif た](http://www.raboof.com/)によって作成された無料のオープンソースのエラーログシステムである、エラーログモジュールとハンドラー (ELMAH) です。 2つのシステムの最も顕著な違いは、エラーの一覧と、web ページおよび RSS フィードからの特定のエラーの詳細を表示する ELAMH の機能です。 ELMAH は、エラーをログに記録するだけなので、正常性の監視よりも簡単に構成できます。 さらに、ELMAH には、ASP.NET 1.x、ASP.NET 2.0、および ASP.NET 3.5 アプリケーションのサポートが含まれており、さまざまなログソースプロバイダーが付属しています。

このチュートリアルでは、ASP.NET アプリケーションに ELMAH を追加するために必要な手順について説明します。 作業開始

> [!NOTE]
> 正常性監視システムと ELMAH の両方に、独自の長所と短所があります。 両方のシステムを試して、ニーズに最も適したものを決定することをお勧めします。

## <a name="adding-elmah-to-an-aspnet-web-application"></a>ASP.NET Web アプリケーションに ELMAH を追加する

ELMAH を新規または既存の ASP.NET アプリケーションに統合することは、5分未満で簡単で簡単なプロセスです。 簡単に言うと、次の4つの簡単な手順を行います。

1. ELMAH をダウンロードし、web アプリケーションに `Elmah.dll` アセンブリを追加します。
2. `Web.config`に ELMAH の HTTP モジュールとハンドラーを登録します。
3. ELMAH の構成オプションを指定します。
4. 必要に応じて、エラーログのソースインフラストラクチャを作成します。

ここでは、これら4つの手順を1つずつ順番に説明します。

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>手順 1: ELMAH プロジェクトファイルのダウンロードと Web アプリケーションへの`Elmah.dll`の追加

ELMAH 1.0 BETA 3 (ビルド 10617)、書き込み時の最新バージョンは、このチュートリアルで利用できるダウンロードに含まれています。 または、 [ELMAH web サイト](https://code.google.com/p/elmah/)にアクセスして最新バージョンを取得したり、ソースコードをダウンロードしたりすることもできます。 ELMAH ダウンロードをデスクトップ上のフォルダーに抽出し、ELMAH アセンブリファイル (`Elmah.dll`) を探します。

> [!NOTE]
> `Elmah.dll` ファイルは、ダウンロードの `Bin` フォルダーにあります。このフォルダーには、異なる .NET Framework バージョンのサブフォルダーと、リリースビルドとデバッグビルドのサブフォルダーがあります。 適切なフレームワークのバージョンについては、リリースビルドを使用してください。 たとえば、ASP.NET 3.5 web アプリケーションをビルドする場合は、`Bin\net-3.5\Release` フォルダーから `Elmah.dll` ファイルをコピーします。

次に、Visual Studio を開き、ソリューションエクスプローラーで web サイト名を右クリックし、コンテキストメニューから [参照の追加] を選択して、アセンブリをプロジェクトに追加します。 [参照の追加] ダイアログボックスが表示されます。 [参照] タブに移動し、`Elmah.dll` ファイルを選択します。 この操作により、`Elmah.dll` ファイルが web アプリケーションの `Bin` フォルダーに追加されます。

> [!NOTE]
> Web アプリケーションプロジェクト (WAP) の種類では、ソリューションエクスプローラーに `Bin` フォルダーは表示されません。 代わりに、[参照] フォルダーの下にこれらの項目が表示されます。

`Elmah.dll` アセンブリには、ELMAH システムによって使用されるクラスが含まれています。 これらのクラスは、次の3つのカテゴリのいずれかに分類されます。

- **Http モジュール**-http モジュールは、`Error` イベントなどの `HttpApplication` イベントのイベントハンドラーを定義するクラスです。 ELMAH には複数の HTTP モジュールが含まれており、最も連動なものは次の3つです。 

    - `ErrorLogModule`-未処理の例外をログソースに記録します。
    - `ErrorMailModule`-未処理の例外の詳細を電子メールメッセージで送信します。
    - `ErrorFilterModule`-開発者が指定したフィルターを適用して、ログに記録される例外と無視される例外を決定します。
- **Http ハンドラー** -http ハンドラーは、特定の種類の要求のマークアップを生成するクラスです。 ELMAH には、エラーの詳細を web ページとして、RSS フィードとして、またはコンマ区切りファイル (CSV) として表示する HTTP ハンドラーが含まれています。
- **エラーログのソース**-ELMAH では、メモリ、Microsoft SQL Server データベース、Microsoft access データベース、Oracle データベース、XML ファイル、SQLite データベース、または Vista DB データベースに対して、エラーを記録することができます。 正常性監視システムと同様に、ELMAH のアーキテクチャはプロバイダーモデルを使用して構築されています。つまり、必要に応じて、独自のカスタムログソースプロバイダーを作成し、シームレスに統合することができます。

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>手順 2: ELMAH の HTTP モジュールとハンドラーの登録

`Elmah.dll` ファイルには、未処理の例外を自動的にログに記録したり、web ページからエラーの詳細を表示したりするために必要な HTTP モジュールとハンドラーが含まれていますが、web アプリケーションの構成に明示的に登録する必要があります。 `ErrorLogModule` HTTP モジュールは、登録されると、`HttpApplication`の `Error` イベントをサブスクライブします。 このイベントが発生するたびに、`ErrorLogModule` によって、指定したログソースに例外の詳細が記録されます。 ログソースプロバイダーの定義方法については、次のセクション「ELMAH の構成」を参照してください。 `ErrorLogPageFactory` HTTP ハンドラーファクトリは、web ページからエラーログを表示するときにマークアップを生成します。

HTTP モジュールとハンドラーを登録するための具体的な構文は、サイトの電源を入れている web サーバーによって異なります。 ASP.NET 開発サーバーおよび Microsoft の IIS バージョン6.0 以前では、HTTP モジュールとハンドラーは、`<system.web>` 要素内に表示される `<httpModules>` および `<httpHandlers>` セクションに登録されています。 IIS 7.0 を使用している場合は、`<system.webServer>` 要素の `<modules>` と `<handlers>` のセクションに登録する必要があります。 さいわい、使用する web サーバーに関係なく、*両方*の場所で HTTP モジュールとハンドラーを定義できます。 このオプションは、使用されている web サーバーに関係なく、開発環境と運用環境で同じ構成を使用できるようにするため、最もポータブルなオプションです。

まず、`ErrorLogModule` HTTP モジュールと `ErrorLogPageFactory` HTTP ハンドラーを `<system.web>`の `<httpModules>` および `<httpHandlers>` セクションに登録します。 構成でこれらの2つの要素が既に定義されている場合は、ELMAH の HTTP モジュールおよびハンドラーの `<add>` 要素を含めるだけです。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample1.xml)]

次に、`<system.webServer>` 要素に ELMAH の HTTP モジュールとハンドラーを登録します。 以前と同様に、この要素が構成にまだ存在していない場合は、それを追加します。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample2.xml)]

既定では、HTTP モジュールとハンドラーが `<system.web>` セクションに登録されている場合、IIS 7 はを示します。 `<validation>` 要素の `validateIntegratedModeConfiguration` 属性は、このようなエラーメッセージを非表示にするように IIS 7 に指示します。

`ErrorLogPageFactory` HTTP ハンドラーを登録するための構文には、`elmah.axd`に設定されている `path` 属性が含まれていることに注意してください。 この属性は、`elmah.axd` という名前のページに対して要求が到着した場合に、`ErrorLogPageFactory` HTTP ハンドラーによって要求が処理されることを web アプリケーションに通知します。 このチュートリアルの後半では、`ErrorLogPageFactory` HTTP ハンドラーの動作について説明します。

### <a name="step-3-configuring-elmah"></a>手順 3: ELMAH の構成

ELMAH は、`<elmah>`という名前のカスタム構成セクションで、web サイトの `Web.config` ファイルでその構成オプションを検索します。 `Web.config` でカスタムセクションを使用するには、まず `<configSections>` 要素で定義する必要があります。 `Web.config` ファイルを開き、次のマークアップを `<configSections>`に追加します。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample3.xml)]

> [!NOTE]
> ASP.NET 1.x アプリケーションの ELMAH を構成する場合は、上の `<section>` の要素から `requirePermission="false"` 属性を削除します。

上記の構文では、カスタム `<elmah>` セクションとそのサブセクション (`<security>`、`<errorLog>`、`<errorMail>`、および `<errorFilter>`) が登録されます。

次に、`Web.config`に `<elmah>` セクションを追加します。 このセクションは、`<system.web>` 要素と同じレベルに表示されます。 `<elmah>` セクション内で、`<security>` と `<errorLog>` のセクションを次のように追加します。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample4.xml)]

`<security>` セクションの `allowRemoteAccess` 属性は、リモートアクセスが許可されているかどうかを示します。 この値が0に設定されている場合、エラーログ web ページはローカルにのみ表示されます。 この属性が1に設定されている場合、リモートとローカルの両方のユーザーについて、エラーログ web ページが有効になります。 ここでは、リモート訪問者のエラーログ web ページを無効にしてみましょう。 セキュリティに関する考慮事項について説明した後、後でリモートアクセスを許可します。

`<errorLog>` セクションでは、エラーの詳細が記録される場所を指定するエラーログのソースを定義します。これは、正常性監視システムの `<providers>` セクションに似ています。 上記の構文では、エラーログソースとして `SqlErrorLog` クラスを指定しています。これにより、`connectionStringName` 属性値によって指定された Microsoft SQL Server データベースにエラーが記録されます。

> [!NOTE]
> ELMAH には、XML ファイル、Microsoft Access データベース、Oracle データベース、およびその他のデータストアにエラーを記録するために使用できる追加のエラーログプロバイダーが付属しています。 これらの代替エラーログプロバイダーの使用方法については、ELMAH ダウンロードに含まれているサンプル `Web.config` ファイルを参照してください。

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>手順 4: エラーログのソースインフラストラクチャの作成

ELMAH の `SqlErrorLog` プロバイダーは、指定された Microsoft SQL Server データベースにエラーの詳細を記録します。 `SqlErrorLog` プロバイダーは、このデータベースに `ELMAH_Error` という名前のテーブルと、`ELMAH_GetErrorsXml`、`ELMAH_GetErrorXml`、および `ELMAH_LogError`の3つのストアドプロシージャがあることを想定しています。 ELMAH ダウンロードには、このテーブルとこれらのストアドプロシージャを作成するための T-sql を含む `db` フォルダーに `SQLServer.sql` という名前のファイルが含まれています。 `SqlErrorLog` プロバイダーを使用するには、データベースで次のステートメントを実行する必要があります。

**図 1**と**2**は、`SqlErrorLog` プロバイダーが必要とするデータベースオブジェクトが追加された後の Visual Studio のデータベースエクスプローラーを示しています。

[![](logging-error-details-with-elmah-vb/_static/image2.png)](logging-error-details-with-elmah-vb/_static/image1.png)

**図 1**: `SqlErrorLog` プロバイダーが `ELMAH_Error` テーブルにエラーを記録する

[![](logging-error-details-with-elmah-vb/_static/image4.png)](logging-error-details-with-elmah-vb/_static/image3.png)

**図 2**: `SqlErrorLog` プロバイダーが3つのストアドプロシージャを使用する

## <a name="elmah-in-action"></a>ELMAH のアクション

この時点で、web アプリケーションに ELMAH を追加し、`ErrorLogModule` HTTP モジュールと `ErrorLogPageFactory` HTTP ハンドラーを登録し、`Web.config`で ELMAH の構成オプションを指定し、`SqlErrorLog` エラーログプロバイダーに必要なデータベースオブジェクトを追加しました。 これで、ELMAH の動作を確認する準備ができました。 書籍のレビューの web サイトにアクセスし、`Genre.aspx?ID=foo`などの実行時エラーを生成するページや、`NoSuchPage.aspx`などの存在しないページにアクセスします。 これらのページにアクセスしたときに表示される内容は、`<customErrors>` の構成と、ローカルまたはリモートのどちらにアクセスしているかによって異なります。 (このトピックについては、「 [*カスタムエラーページの表示*」チュートリアル](displaying-a-custom-error-page-vb.md)を参照してください)。

ELMAH は、未処理の例外が発生したときにユーザーに表示される内容に影響しません。詳細をログに記録するだけです。 このエラーログには、web サイトのルート (`http://localhost/BookReviews/elmah.axd`など) から `elmah.axd` web ページからアクセスできます。 (このファイルはプロジェクトに物理的に存在しませんが、要求がに対して提供されると、ランタイムは、ブラウザーに返されたマークアップを生成する `ErrorLogPageFactory` HTTP ハンドラーに要求をディスパッチ `elmah.axd` ます)。

> [!NOTE]
> また、[`elmah.axd`] ページを使用して、ELMAH にテストエラーを生成するように指示することもできます。 `elmah.axd/test` (のよう `http://localhost/BookReviews/elmah.axd/test`に) にアクセスすると、ELMAH は `Elmah.TestException`型の例外をスローします。これには、"これはテスト例外であり、無視しても安全です。" というエラーメッセージが表示されます。

**図 3**は、開発環境から `elmah.axd` にアクセスするときのエラーログを示しています。

[![](logging-error-details-with-elmah-vb/_static/image6.png)](logging-error-details-with-elmah-vb/_static/image5.png)

**図 3**: `Elmah.axd` Web ページのエラーログを表示する  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image7.png)される)

**図 3**のエラーログには6つのエラーエントリが含まれています。 各エントリには、HTTP 状態コード (これらのエラーの場合は404または 500)、種類、説明、エラーが発生したときにログオンしたユーザーの名前、および日付と時刻が含まれます。 [詳細] リンクをクリックすると、エラーの詳細 (**図 4**を参照) に示されているのと同じエラーメッセージを含むページが、エラー発生時のサーバー変数の値と共に表示されます (**図 5**を参照)。 また、エラーの詳細が保存されている未加工の XML を表示することもできます。これには、HTTP POST ヘッダーの値などの追加情報が含まれます。

[![](logging-error-details-with-elmah-vb/_static/image9.png)](logging-error-details-with-elmah-vb/_static/image8.png)

**図 4**: エラーの詳細を表示する YSOD  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image10.png)される)

[![](logging-error-details-with-elmah-vb/_static/image12.png)](logging-error-details-with-elmah-vb/_static/image11.png)

**図 5**: エラー発生時のサーバー変数コレクションの値を調べる  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image13.png)される)

運用 web サイトに ELMAH をデプロイするには、次のことが伴います。

- 運用環境の `Bin` フォルダーに `Elmah.dll` ファイルをコピーする
- 運用環境で使用される `Web.config` ファイルに ELMAH 固有の構成設定をコピーする
- 運用データベースにエラーログソースインフラストラクチャを追加します。

前のチュートリアルでは、開発から運用にファイルをコピーするための手法について説明しました。 実稼働データベースでエラーログソースインフラストラクチャを取得する最も簡単な方法は、SQL Server Management Studio を使用して運用データベースに接続し、`SqlServer.sql` スクリプトファイルを実行して、必要なテーブルとストアドプロシージャを作成することです。

### <a name="viewing-the-error-details-page-on-production"></a>運用環境のエラーの詳細ページを表示する

サイトを運用環境にデプロイしたら、運用 web サイトにアクセスして、未処理の例外を生成します。 開発環境と同様に、ELMAH は、未処理の例外が発生したときに表示されるエラーページには影響しません。代わりに、エラーをログに記録するだけです。 運用環境からエラーログページ (`elmah.axd`) にアクセスしようとすると、**図 6**に示されている禁止ページが表示されます。

[![](logging-error-details-with-elmah-vb/_static/image15.png)](logging-error-details-with-elmah-vb/_static/image14.png)

**図 6**: 既定では、リモート訪問者がエラーログ Web ページを表示できない  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image16.png)される)

ELMAH 構成の `<security>` セクションでは、`allowRemoteAccess` 属性を0に設定しています。これにより、リモートユーザーがエラーログを表示することが禁止されます。 エラーの詳細によってセキュリティの脆弱性やその他の機密情報が明らかになる可能性があるので、匿名の訪問者がエラーログを表示できないようにすることが重要です。 この属性を1に設定して、エラーログへのリモートアクセスを有効にする場合は、承認されたユーザーのみがアクセスできるように `elmah.axd` パスをロックすることが重要です。 これは、`Web.config` ファイルに `<location>` 要素を追加することによって実現できます。

次の構成では、管理者ロールのユーザーのみがエラーログ web ページにアクセスできます。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample5.xml)]

> [!NOTE]
> 管理者ロールとシステムの3人のユーザー (Scott、Jisun、および Alice) は、アプリケーションサービスチュートリアルを使用した[ *web サイトの構成*](configuring-a-website-that-uses-application-services-vb.md)に追加されました。 Scott および Jisun というユーザーは、管理者ロールのメンバーです。 認証と承認の詳細については、 [Web サイトのセキュリティ](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアルを参照してください。

これで、運用環境のエラーログをリモートユーザーが表示できるようになりました。エラーログ web ページのスクリーンショットについては、**図 3**、 **4**、および**5**を参照してください。 ただし、匿名ユーザーまたは管理者以外のユーザーがエラーログページを表示しようとすると、**図 7**に示すように、ログインページ (`Login.aspx`) に自動的にリダイレクトされます。

[![](logging-error-details-with-elmah-vb/_static/image18.png)](logging-error-details-with-elmah-vb/_static/image17.png)

**図 7**: 承認されていないユーザーがログインページに自動的にリダイレクトされる  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image19.png)される)

### <a name="programmatically-logging-errors"></a>プログラムによるエラーのログ記録

ELMAH の `ErrorLogModule` HTTP モジュールは、未処理の例外を指定されたログソースに自動的に記録します。 または、`ErrorSignal` クラスとその `Raise` メソッドを使用して、ハンドルされない例外を発生させずにエラーをログに記録することもできます。 `Raise` メソッドには `Exception` オブジェクトが渡され、その例外がスローされ、処理されずに ASP.NET ランタイムに到達したかのようにログに記録されます。 ただし、`Raise` メソッドが呼び出された後も要求は正常に実行されますが、スローされた未処理の例外によって要求の通常の実行が中断され、ASP.NET ランタイムによって構成されたエラーページが表示されます。

`ErrorSignal` クラスは、何らかのアクションが失敗する可能性がある場合に便利ですが、実行されている操作全体の致命的なエラーではありません。 たとえば、web サイトには、ユーザーの入力を取得してデータベースに格納し、その情報が処理されたことを知らせる電子メールをユーザーに送信するフォームが含まれている場合があります。 情報がデータベースに正常に保存されても、電子メールメッセージの送信時にエラーが発生する場合はどうすればよいですか。 1つの方法として、例外をスローして、そのユーザーをエラーページに送信する方法があります。 ただし、ユーザーが入力した情報が保存されていないと思われることがあります。 別の方法として、電子メール関連のエラーをログに記録する方法もありますが、ユーザーの操作を変更することはできません。 ここでは、`ErrorSignal` クラスが役に立ちます。

[!code-vb[Main](logging-error-details-with-elmah-vb/samples/sample6.vb)]

## <a name="error-notification-via-email"></a>電子メールによるエラー通知

エラーの詳細を指定された受信者に電子メールで送信するように、データベースにエラーを記録することもできます。 この機能は `ErrorMailModule` HTTP モジュールによって提供されます。そのため、エラーの詳細を電子メールで送信するには、この HTTP モジュールを `Web.config` に登録する必要があります。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample7.xml)]

次に、電子メールの送信者と受信者、件名、および電子メールが非同期に送信されるかどうかを示す `<elmah>` 要素の `<errorMail>` セクションに、エラーの電子メールに関する情報を指定します。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample8.xml)]

上記の設定を適用すると、実行時エラーが発生するたびに、エラーの詳細と共に support@example.com に電子メールが送信されます。 ELMAH のエラーメールには、エラーの詳細 web ページ、エラーメッセージ、スタックトレース、およびサーバー変数 (**図 4**および**5**を参照) に表示されているものと同じ情報が含まれています。 エラーメールには、例外の詳細も添付ファイルとしてのデスコンテンツ (`YSOD.html`) が含まれています。

**図 8**に、`Genre.aspx?ID=foo`にアクセスして生成された ELMAH のエラーメールを示します。 **図 8**はエラーメッセージとスタックトレースのみを示していますが、サーバー変数は電子メールの本文にさらに下に含まれています。

[![](logging-error-details-with-elmah-vb/_static/image21.png)](logging-error-details-with-elmah-vb/_static/image20.png)

**図 8**: ELMAH でエラーの詳細を電子メールで送信するように構成する  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-elmah-vb/_static/image22.png)される)

## <a name="only-logging-errors-of-interest"></a>目的のエラーのみをログに記録する

既定では、ELMAH は、404などの HTTP エラーを含む、未処理のすべての例外の詳細をログに記録します。 エラーフィルタリングを使用して、これらのエラーやその他の種類のエラーを無視するように ELMAH に指示できます。 フィルター処理ロジックは、ELMAH の `ErrorFilterModule` HTTP モジュールによって実行されます。フィルター処理ロジックを使用するには、`Web.config` に登録する必要があります。 フィルター処理の規則は、[`<errorFilter>`] セクションで指定します。

次のマークアップは、エラー404をログに記録しないように ELMAH に指示します。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample9.xml)]

> [!NOTE]
> エラーフィルターを使用するには、`ErrorFilterModule` HTTP モジュールを登録する必要があります。

`<test>` セクション内の `<equal>` 要素は、アサーションと呼ばれます。 アサーションが true と評価された場合、エラーは ELMAH のログからフィルター処理されます。 使用できるアサーションは、`<greater>`、`<greater-or-equal>`、`<not-equal>`、`<lesser>`、`<lesser-or-equal>`などです。 また、`<and>` と `<or>` ブール演算子を使用してアサーションを組み合わせることもできます。 さらに、単純な JavaScript 式をアサーションとして含めることも、独自のアサーションをまたはC# Visual Basic に記述することもできます。

ELMAH のエラーフィルタリング機能の詳細については、 [elmah wiki](https://code.google.com/p/elmah/w/list)の[「エラーのフィルター処理」セクション](https://code.google.com/p/elmah/wiki/ErrorFiltering)を参照してください。

## <a name="summary"></a>まとめ

ELMAH は、ASP.NET web アプリケーションのエラーをログに記録するためのシンプルで、かつ強力なメカニズムを提供します。 Microsoft の正常性監視システムと同様に、ELMAH はデータベースにエラーを記録し、電子メールでエラーの詳細を開発者に送信することができます。 正常性監視システムとは異なり、ELMAH には、Microsoft SQL Server、Microsoft Access、Oracle、XML ファイルなど、さまざまな種類のエラーログデータストアの既定のサポートが含まれています。 また、ELMAH には、エラーログと、web ページからの特定のエラーに関する詳細情報を表示するための組み込みのメカニズムが用意されています (`elmah.axd`)。 また、[`elmah.axd`] ページでは、エラー情報を RSS フィードまたはコンマ区切り値ファイル (CSV) として表示することもできます。このファイルは、Microsoft Excel を使用して読み取ることができます。 また、宣言型またはプログラムによるアサーションを使用して、ログからのエラーをフィルター処理するように ELMAH に指示することもできます。 および ELMAH は、ASP.NET バージョン1.x アプリケーションで使用できます。

配置されたすべてのアプリケーションには、未処理の例外を自動的にログに記録し、開発チームに通知を送信するためのメカニズムが必要です。 正常性の監視を使用して実行するか、または ELMAH をセカンダリにするかを指定します。 つまり、正常性の監視と ELMAH のどちらを使用するかに関係なく、両方のシステムを評価し、ニーズに最も合ったものを選択します。 根本的に重要なのは、運用環境でハンドルされない例外をログに記録するメカニズムがいくつかあります。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ELMAH-エラーログモジュールとハンドラー](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH プロジェクトページ](https://code.google.com/p/elmah/)(ソースコード、サンプル、wiki)
- [Web アプリケーションに ELMAH をプラグインして未処理の例外をキャッチする](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx)(ビデオ)
- [セキュリティエラーログページ](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [HTTP モジュールとハンドラーを使用してプラグ可能な ASP.NET コンポーネントを作成する](https://msdn.microsoft.com/library/aa479332.aspx)
- [Web サイトのセキュリティに関するチュートリアル](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [前へ](logging-error-details-with-asp-net-health-monitoring-vb.md)
> [次へ](precompiling-your-website-vb.md)
