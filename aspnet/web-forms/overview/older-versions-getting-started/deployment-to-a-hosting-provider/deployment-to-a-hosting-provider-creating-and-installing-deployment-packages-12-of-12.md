---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact での ASP.NET Web アプリケーションのデプロイ: トラブルシューティング (12 インチ) |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639874"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: トラブルシューティング (12 インチ)

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、および Windows Azure Web サイトへのデプロイ方法については、「 [ASP.NET Web deployment Using Visual studio](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。

このページでは、Visual Studio を使用して ASP.NET web アプリケーションを配置するときに発生する可能性のある一般的な問題について説明します。 それぞれについて、1つまたは複数の考えられる原因と、対応するソリューションが提供されます。

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>'/' アプリケーションのサーバーエラー-現在のカスタムエラー設定により、エラーの詳細をリモートで表示できません

### <a name="scenario"></a>通信の種類

リモートホストにサイトを展開した後、web.config ファイルの customErrors 設定を示すエラーメッセージが表示されますが、エラーの実際の原因は示されていません。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

既定では、ASP.NET は、web アプリケーションがローカルコンピューター上で実行されている場合にのみ、詳細なエラー情報を表示します。 一般に、web アプリケーションがインターネット経由で公開されている場合は、詳細なエラー情報を表示しないようにします。ハッカーはこの情報を使用してアプリケーションの脆弱性を検出できるためです。 ただし、サイトまたは更新プログラムをサイトに展開するときに問題が発生し、実際のエラーメッセージが表示されることがあります。

リモートホストで実行されているときに、アプリケーションで詳細なエラーメッセージを表示できるようにするには、web.config ファイルを編集して `customErrors` モードをオフにし、アプリケーションを再デプロイして、アプリケーションを再度実行します。

1. アプリケーションの Web.config ファイルの `system.web` 要素に `customErrors` 要素がある場合は、`mode` 属性を "off" に変更します。 それ以外の場合は、次の例に示すように、`mode` 属性を "off" に設定して、`system.web` 要素に `customErrors` 要素を追加します。

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. アプリケーションを展開します。
3. アプリケーションを実行し、エラーが発生する原因となったものをすべて繰り返します。 これで、実際のエラーメッセージを確認できます。
4. エラーを解決したら、元の `customErrors` 設定を復元し、アプリケーションを再展開します。

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>を使用する Web ページでアクセスが拒否される SQL Server Compact

### <a name="scenario"></a>通信の種類

SQL Server Compact を使用するサイトを展開し、データベースにアクセスする配置済みサイトでページを実行すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

サーバー上のネットワークサービスアカウントは、 *bin\amd64*または*bin\x86*フォルダーにある SQL service Compact ネイティブバイナリを読み取ることができる必要がありますが、これらのフォルダーに対する読み取りアクセス許可がありません。 *Bin*フォルダーで NETWORK SERVICE の読み取りアクセス許可を設定し、アクセス許可をサブフォルダーに拡張します。

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>アクセス許可が不足しているため、構成ファイルを読み取れません

### <a name="scenario"></a>通信の種類

Visual Studio の [発行] ボタンをクリックしてローカルコンピューター上の IIS にアプリケーションを配置すると、発行が失敗し、次のようなエラーメッセージが**出力**ウィンドウに表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

ローカルコンピューターでワンクリックで IIS に発行するには、管理者権限を使用して Visual Studio を実行している必要があります。 Visual Studio を閉じて、管理者権限で再起動します。

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>対象のコンピューターに接続できませんでした...指定されたプロセスの使用

### <a name="scenario"></a>通信の種類

Visual Studio の [発行] ボタンをクリックしてアプリケーションを配置すると、発行が失敗し、**出力**ウィンドウに次のようなエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

プロキシサーバーは、移行先サーバーとの通信を中断しています。 Windows のコントロールパネルまたは Internet Explorer で、 **[インターネットオプション]** を選択し、 **[接続]** タブを選択します。 **[インターネットのプロパティ]** ダイアログボックスで、 **[LAN の設定]** をクリックします。 **[ローカルエリアネットワーク (LAN) の設定]** ダイアログボックスで、 **[設定を自動的に検出]** する チェックボックスをオフにします。 次に、[発行] ボタンをもう一度クリックします。

問題が解決しない場合は、システム管理者に問い合わせて、プロキシまたはファイアウォールの設定で実行できることを確認してください。 この問題が発生するのは、Web 配置が Web 管理サービスの展開 (8172) で非標準ポートを使用するためです。その他の接続の場合、Web 配置はポート80を使用します。 サードパーティのホスティングプロバイダーにデプロイする場合、通常は Web 管理サービスを使用します。

## <a name="default-net-40-application-pool-does-not-exist"></a>既定の .NET 4.0 アプリケーションプールが存在しません

### <a name="scenario"></a>通信の種類

.NET Framework 4 を必要とするアプリケーションを展開すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

ASP.NET 4 は IIS にインストールされていません。 配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。 デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。 詳細については、「[テスト環境として IIS に配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)する」チュートリアルを参照してください。

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>初期化文字列の形式は、インデックス0から始まる仕様に準拠していません。

### <a name="scenario"></a>通信の種類

ワンクリック発行を使用してアプリケーションを配置した後、データベースにアクセスするページを実行すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

配置したサイトの web.config ファイルを開き、次の例に示すように、接続*文字列の値*が `$(ReplaceableToken_`で始まるかどうかを確認します。

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

接続文字列が次の例のようになっている場合は、プロジェクトファイルを編集し、次のプロパティを、すべてのビルド構成の `PropertyGroup` 要素に追加します。

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

その後、アプリケーションを再デプロイします。

## <a name="http-500-internal-server-error"></a>HTTP 500 内部サーバーエラー

### <a name="scenario"></a>通信の種類

展開されたサイトを実行すると、次のエラーメッセージが表示され、エラーの原因を示す特定の情報が表示されません。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

500エラーには多くの原因がありますが、これらのチュートリアルに従うと、xml 変換ファイルの1つに XML 要素を間違った場所に配置することが考えられます。 たとえば、`<configuration>`のすぐ下ではなく `<system.web>` の下に `<location>` 要素を挿入する変換を配置すると、このエラーが発生します。 この場合の解決策は、XML 変換ファイルを修正して再配置することです。

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 内部サーバーエラー

### <a name="scenario"></a>通信の種類

展開されたサイトを実行すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

展開したサイトは ASP.NET 4 をターゲットにしていますが、ASP.NET 4 はサーバーの IIS に登録されていません。 サーバーで、管理者特権でのコマンドプロンプトを開き、次のコマンドを実行して ASP.NET 4 を登録します。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。 詳細については、「[テスト環境として IIS に配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)する」チュートリアルを参照してください。

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>アプリ\_データ内の SQL Server Express データベースを開くことができませんでした

### <a name="scenario"></a>通信の種類

*Web.config ファイルの*接続文字列を更新して、 *App\_Data*フォルダー内の *.mdf*ファイルとして SQL Server Express データベースを指すようにしました。アプリケーションを初めて実行すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

*.Mdf*ファイルの名前は、以前に既存のデータベースの *.mdf*ファイルを削除した場合でも、コンピューター上に存在していた SQL Server Express データベースの名前と一致させることはできません。 *.Mdf*ファイルの名前を、データベース名として使用されていない名前に変更し、新しい名前を使用するように*web.config ファイルを*変更します。 別の方法として、 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、以前に存在していた SQL Server Express データベースを削除することもできます。

## <a name="model-compatibility-cannot-be-checked"></a>モデルの互換性を確認できません

### <a name="scenario"></a>通信の種類

新しい SQL Server Express データベースを指すように*web.config ファイルの接続文字列を更新*し、アプリケーションを初めて実行したときに、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

Web.config ファイルに指定したデータベース名が、コンピューター上で以前に使用されていた場合は、データベースが既に存在している可能性があります。 前にコンピューターで使用されていない新しい名前を選択し、この新しいデータベース名を使用するように*web.config ファイルを変更します。* 別の方法として、 [SQL Server Express ユーティリティ](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)または[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、既存のデータベースを削除することもできます。

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>スクリプトがユーザーまたはロールを作成しようとしたときの SQL エラー

### <a name="scenario"></a>通信の種類

**[Sql のパッケージ化/発行]** タブで構成されたデータベース配置を使用している場合、配置中に実行される SQL スクリプトには create User または create Role コマンドがあり、これらのコマンドが実行されるとスクリプトの実行が失敗します。 次のような詳細なメッセージが表示される場合があります。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

**[SQL のパッケージ化/発行]** タブではなく、 **Web の発行**ウィザードでデータベースの配置を構成したときにこのエラーが発生した場合は、[[構成と配置](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)] フォーラムでスレッドを作成すると、このトラブルシューティングのページにソリューションが追加されます。

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

配置の実行に使用しているユーザーアカウントに、ユーザーまたはロールを作成するためのアクセス許可がありません。 たとえば、ホスティング会社は、`db_datareader`、`db_datawriter`、および `db_ddladmin` ロールを、ユーザーに対して設定されたユーザーアカウントに割り当てることができます。 これらは、ほとんどのデータベースオブジェクトを作成するのに十分ですが、ユーザーまたはロールを作成するためのものではありません。 このエラーを回避する方法の1つは、データベースの配置からユーザーとロールを除外することです。 これを行うには、データベースの自動的に生成されたスクリプトの `PreSource` 要素を編集して、次の属性が含まれるようにします。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

プロジェクトファイルの `PreSource` 要素を編集する方法の詳細については、「[方法: プロジェクトファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)する」を参照してください。 開発用データベースのユーザーまたはロールが転送先データベースに存在する必要がある場合は、ホスティングプロバイダーに問い合わせてください。

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>配置時にカスタムスクリプトを実行すると SQL Server タイムアウトエラーが発生する

### <a name="scenario"></a>通信の種類

配置時に実行するカスタム SQL スクリプトを指定し、Web 配置実行するとタイムアウトになります。

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

トランザクションモードが異なる複数のスクリプトを実行すると、タイムアウトエラーが発生する可能性があります。 既定では、自動的に生成されたスクリプトはトランザクション内で実行されますが、カスタムスクリプトでは実行されません。 **[Sql のパッケージ化/発行]** タブで **[既存のデータベースからデータまたはスキーマをプル]** する オプションを選択し、カスタムの sql スクリプトを追加する場合は、すべてのスクリプトで同じトランザクション設定が使用されるように、一部のスクリプトのトランザクション設定を変更する必要があります。 詳細については、「[方法: Web アプリケーションプロジェクトを使用してデータベースを配置](https://msdn.microsoft.com/library/dd465343.aspx)する」を参照してください。

すべてが同じでもこのエラーが発生するようにトランザクション設定を構成した場合は、スクリプトを個別に実行することをお勧めします。 SQL の **[パッケージ化/発行]** タブの **[データベーススクリプト]** グリッドで、タイムアウトエラーを発生させるスクリプトの **[含める]** チェックボックスをオフにし、プロジェクトを発行します。 次に、 **[データベーススクリプト]** グリッドに戻り、そのスクリプトの **[インクルード]** チェックボックスをオンにして、他のスクリプトの **[含める]** チェックボックスをオフにします。 その後、プロジェクトを再度発行します。 今回は、発行時に、選択したカスタムスクリプトのみが実行されます。

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>サイトマニフェストのストリームデータはまだ使用できません

### <a name="scenario"></a>通信の種類

`t` (テスト) オプションを指定して *.deploy*ファイルを使用してパッケージをインストールすると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

エラーメッセージは、コマンドがテストレポートを生成できないことを意味します。 ただし、`y` (実際のインストール) オプションを使用すると、コマンドが実行される場合があります。 このメッセージは、テストモードでのコマンドの実行に問題があることを示しています。

## <a name="this-application-requires-managedruntimeversion-v40"></a>このアプリケーションには ManagedRuntimeVersion v4.0 が必要です

### <a name="scenario"></a>通信の種類

を展開しようとすると、次のエラーメッセージが表示されます。

 エラー: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlscript ' のストリームデータはまだ使用できません。 使用しようとしているアプリケーションプールの ' managedRuntimeVersion ' プロパティが ' v2.0 ' に設定されています。 このアプリケーションには ' v4.0 ' が必要です。 

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

ASP.NET 4 は IIS にインストールされていません。 配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。 デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft. Deployment. DeploymentProviderOptions をキャストできません

### <a name="scenario"></a>通信の種類

パッケージを展開すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

Web 配置 1.1 UI を使用して、Web 配置2.0 がインストールされているサーバーに IIS マネージャーから展開しようとしています。 IIS リモート管理ツールを使用してパッケージをインポートして展開する場合は、接続を確立するときに **[利用可能な新機能]** ダイアログボックスを確認します。 (このダイアログボックスは、接続が最初に確立されたときに1回だけ表示される場合があります。 接続をクリアして最初からやり直すには、IIS マネージャーを終了し、コマンドプロンプトで `inetmgr /reset` を入力して再度起動します)。一覧に表示されている機能の1つが**WEB 配置 UI**で、バージョン番号が8よりも低い場合、展開先のサーバーに1.1 と2.0 の両方のバージョンの Web 配置がインストールされている可能性があります。 2\.0 がインストールされているクライアントから展開するには、サーバーに Web 配置2.0 のみがインストールされている必要があります。 この問題を解決するには、ホスティングプロバイダーに連絡する必要があります。

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>SQL Server Compact のネイティブコンポーネントを読み込むことができません

### <a name="scenario"></a>通信の種類

展開されたサイトを実行すると、次のエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

配置されたサイトには、ネイティブアセンブリをアプリケーションの*bin*フォルダーの下に持つ*amd64*および*x86*サブフォルダーがありません。 SQL Server Compact がインストールされているコンピューターでは、ネイティブアセンブリは*C:\Program are SQL Server Compact Edition\v4.0\Private*に配置されます。 Visual Studio プロジェクトの正しいフォルダーに正しいファイルを取り込むには、NuGet SqlServerCompact パッケージをインストールするのが最善の方法です。 パッケージのインストールでは、ネイティブアセンブリを*amd64*および*x86*にコピーするビルド後スクリプトが追加されます。 ただし、これらを展開するためには、プロジェクトに手動で含める必要があります。 詳細については、 [SQL Server Compact のデプロイ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)に関するチュートリアルを参照してください。

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Entity Framework Code First アプリケーションを展開した後の "パスが有効ではありません" エラーが発生する

### <a name="scenario"></a>通信の種類

Entity Framework Code First Migrations を使用するアプリケーションと DBMS (SQL Server Compact など) をデプロイして、そのデータベースをアプリの\_データフォルダー内のファイルに格納します。 最初の配置後にデータベースを作成するように構成された Code First Migrations。 アプリケーションを実行すると、次の例のようなエラーメッセージが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

データベースを作成しようとしていますが、アプリ\_データフォルダーが存在しません Code First。 をデプロイしたときに*app\_data*フォルダーにファイルがないか、**プロジェクトのプロパティ**ウィンドウの **[パッケージ/発行 Web]** タブで [**アプリ\_データを除外**する] を選択しました。 サーバーにコピーするファイルがフォルダーに存在しない場合、配置プロセスではサーバーにフォルダーが作成されません。 サイトにデータベースが既にセットアップされている場合は、[発行プロファイル] で [**宛先にある追加のファイルを削除**する] を選択した場合、配置プロセスによってファイルと*アプリ\_データ*フォルダー自体が削除されます。 この問題を解決するには、*アプリの\_データ*フォルダーに .txt ファイルなどのプレースホルダーファイルを配置し、[**アプリ\_データを除外**する] を選択して再デプロイします。 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"基になる RCW から分離された COM オブジェクトは使用できません。"

### <a name="scenario"></a>通信の種類

これで、ワンクリック発行を使用してアプリケーションをデプロイした後、次のエラーが表示されるようになりました。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

通常、このエラーを解決するには、Visual Studio の終了と再起動が必要です。

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>発行に使用されるユーザーの資格情報に setACL 機関がないため、展開が失敗する

### <a name="scenario"></a>通信の種類

フォルダーのアクセス許可を設定する権限がないことを示すエラーが表示され、発行が失敗します (使用しているユーザーアカウントには setACL 機関がありません)。

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。 サイトフォルダーの既定のアクセス許可が正しいことがわかっていて、設定する必要がない場合は、この動作を無効にします。そのためには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合は) .targets ファイルに **&lt;includesetaclprovideron ondestination&lt;&gt;** を追加します。 これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>アプリケーションがアプリケーションフォルダーに書き込もうとしたときにアクセス拒否エラーが発生する

### <a name="scenario"></a>通信の種類

アプリケーションフォルダーのいずれかでファイルを作成または編集しようとすると、アプリケーションエラーが発生します。これは、そのフォルダーに対する書き込み権限がないためです。

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。 アプリケーションにサブフォルダーへの書き込みアクセス権が必要な場合は、[フォルダーのアクセス許可の設定](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)と[運用環境への配置に](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)関するチュートリアルに従って、そのフォルダーのアクセス許可を設定できます。 アプリケーションにサイトのルートフォルダーへの書き込みアクセス権が必要な場合は、ルートフォルダーに対する読み取り専用アクセスを設定できないようにする必要があります。これを行うには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合) .targets ファイルに **&lt;includesetaclprovideron&lt;&gt;on**を追加します これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。 <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>構成エラー-targetFramework 属性が、インストールされているバージョンより後のバージョンを参照してい .NET Framework

### <a name="scenario"></a>通信の種類

ASP.NET 4.5 を対象とする web プロジェクトが正常に発行されましたが、アプリケーションを実行すると (web.config ファイルで `customErrors` モードが "off" に設定されている場合)、次のエラーが表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

エラーページの [ソースエラー] ボックスには、web.config の次の行がエラーの原因として強調表示されます。

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>考えられる原因と解決策

サーバーは ASP.NET 4.5 をサポートしていません。 ASP.NET 4.5 のサポートを追加できるかどうかを判断するには、ホスティングプロバイダーに問い合わせてください。 サーバーのアップグレードがオプションではない場合は、代わりに ASP.NET 4 以前を対象とする web プロジェクトをデプロイする必要があります。ASP.NET 4 以前の web プロジェクトを同じ宛先に配置する場合は、 **web の発行**ウィザードの **[設定]** タブにある **[変換先で追加のファイルを削除]** する チェックボックスをオンにします。 [**転送先で追加のファイルを削除**する] を選択しないと、構成エラーページが引き続き表示されます。

[プロジェクトの**プロパティ**] ウィンドウには [ターゲットフレームワーク] ドロップダウンリストが含まれていますが、 **.NET Framework 4.5**から **.NET Framework 4**に変更するだけでこの問題を解決することはできません。 ターゲットフレームワークを以前のバージョンの framework に変更すると、プロジェクトはその後のフレームワークバージョンのアセンブリへの参照を保持し、実行されなくなります。 これらの参照を手動で変更するか、.NET Framework 4 以前を対象とする新しいプロジェクトを作成する必要があります。 詳細については、「 [Web サイトのターゲット設定 .NET Framework](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
