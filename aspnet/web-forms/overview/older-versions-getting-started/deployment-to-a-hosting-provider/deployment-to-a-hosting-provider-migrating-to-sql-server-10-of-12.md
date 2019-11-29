---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server 12 | への移行Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640563"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server 12 の10への移行

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、SQL Server Compact から SQL Server に移行する方法について説明します。 そのためには、ストアドプロシージャ、トリガー、ビュー、レプリケーションなど、SQL Server Compact でサポートされていない SQL Server 機能を利用することが必要になることがあります。 SQL Server Compact と SQL Server の違いの詳細については、 [SQL Server Compact のデプロイ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)に関するチュートリアルを参照してください。

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>SQL Server Express と完全な SQL Server 開発

SQL Server にアップグレードする場合は、開発環境とテスト環境で SQL Server または SQL Server Express を使用することをお勧めします。 ツールのサポートとデータベースエンジンの機能の違いに加えて、SQL Server Compact とその他のバージョンの SQL Server 間のプロバイダー実装には違いがあります。 これらの違いにより、同じコードによって異なる結果が生成される可能性があります。 そのため、SQL Server Compact を開発データベースとして保持する場合は、運用環境に配置する前に、SQL Server また SQL Server Express はテスト環境でサイトを十分にテストする必要があります。

SQL Server Compact とは異なり、SQL Server Express は基本的には同じデータベースエンジンであり、完全 SQL Server と同じ .NET プロバイダーを使用します。 SQL Server Express でテストする場合は、SQL Server と同じ結果を得ることができます。 SQL Server で使用できるのと同じデータベースツールの大部分 ( [SQL Server プロファイラー](https://msdn.microsoft.com/library/ms181091.aspx)されている重要な例外) を使用して、ストアドプロシージャ、ビュー、トリガー、レプリケーションなどの SQL Server の他の機能をサポート SQL Server Express ことができます。 (通常は、運用 web サイトで完全 SQL Server を使用する必要があります。 SQL Server Express は共有ホスティング環境で実行できますが、そのように設計されていないため、多くのホスティングプロバイダーではサポートされていません)。

Visual Studio 2012 を使用している場合、通常は Visual Studio と共にインストールされるため、開発環境には SQL Server Express LocalDB を選択します。 ただし、LocalDB は IIS では機能しないため、テスト環境では SQL Server または SQL Server Express のいずれかを使用する必要があります。

### <a name="combining-databases-versus-keeping-them-separate"></a>データベースの結合と分離

Contoso 大学アプリケーションには、メンバーシップデータベース (*aspnet*) とアプリケーションデータベース (*School*) という2つの SQL Server Compact データベースがあります。 移行時に、これらのデータベースを2つの異なるデータベースまたは1つのデータベースに移行できます。 アプリケーションデータベースとメンバーシップデータベースの間のデータベースの結合を容易にするために、これらを組み合わせて使用することもできます。 ホスティングプランでは、それらを組み合わせる理由が提供される場合もあります。 たとえば、ホスティングプロバイダーは複数のデータベースに対してより多くの料金を請求する場合や、複数のデータベースを許可しない場合があります。 このチュートリアルで使用されている Cytanium Lite ホスティングアカウントの場合は、1つの SQL Server データベースのみが許可されます。

このチュートリアルでは、次のように2つのデータベースを移行します。

- 開発環境で2つの LocalDB データベースに移行します。
- テスト環境で2つの SQL Server Express データベースに移行します。
- 運用環境で完全に結合された1つの SQL Server データベースに移行します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="installing-sql-server-express"></a>SQL Server Express のインストール

既定では、Visual Studio 2010 には SQL Server Express が自動的にインストールされますが、既定では Visual Studio 2012 と共にインストールされません。 SQL Server 2012 Express をインストールするには、次のリンクをクリックしてください。

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

*Enu/x64/sqlexpr\_x64\_enu*または*enu/X86/sqlexpr\_x86\_enu*を選択し、インストールウィザードで既定の設定をそのまま使用します。 インストールオプションの詳細については、「インストール[ウィザードから SQL Server 2012 をインストールする (セットアップ)](https://msdn.microsoft.com/library/ms143219.aspx)」を参照してください。

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>テスト環境用の SQL Server Express データベースの作成

次の手順では、ASP.NET membership データベースと School データベースを作成します。

**表示** メニューの **サーバーエクスプローラー** (Visual Web Developer では**データベースエクスプローラー** ) を選択し、**データ接続** を右クリックして、**新しい SQL Server データベースの作成** を選択します。

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

**[新しい SQL Server データベースの作成]** ダイアログボックスの **[サーバー名]** ボックスに「.\SQLExpress」と入力し、 **[新しいデータベース名]** ボックスに「aspnet-Test」と入力して、[ **OK]** をクリックします。

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

同じ手順に従って、"School-Test" という名前の新しい SQL Server Express School データベースを作成します。

(後で開発環境用に各データベースの追加インスタンスを作成し、2つのデータベースセットを区別できるようにする必要があるため、これらのデータベース名に "Test" を追加しています)。

**サーバーエクスプローラー**に、2つの新しいデータベースが表示されるようになりました。

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>新しいデータベースに対して Grant スクリプトを作成する

開発用コンピューターの IIS でアプリケーションを実行すると、アプリケーションは既定のアプリケーションプールの資格情報を使用してデータベースにアクセスします。 ただし、既定では、アプリケーションプール id には、データベースを開くためのアクセス許可がありません。 そのため、そのアクセス許可を付与するスクリプトを実行する必要があります。 このセクションでは、後で実行するスクリプトを作成して、アプリケーションが IIS で実行されたときにデータベースを開けるようにします。

「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで作成したソリューションの*solutionfiles*フォルダーで、 *Grant .sql*という名前の新しい SQL ファイルを作成します。 次の SQL コマンドをファイルにコピーし、ファイルを保存して閉じます。

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> このスクリプトは、このチュートリアルで指定されているように、SQL Server 2008 と Windows 7 の IIS 設定で動作するように設計されています。 異なるバージョンの SQL Server または Windows を使用している場合、またはコンピューターに IIS を別の方法でセットアップする場合は、このスクリプトへの変更が必要になることがあります。 SQL Server スクリプトの詳細については、「 [SQL Server オンラインブック](https://go.microsoft.com/fwlink/?LinkId=132511)」を参照してください。

> [!NOTE] 
> 
> **セキュリティ**に関する注意このスクリプトは、実行時にデータベースにアクセスするユーザーに対して、db\_所有者のアクセス許可を付与します。これは、運用環境で使用するものです。 場合によっては、完全なデータベーススキーマ更新権限を持つユーザーを配置に対してのみ指定し、実行時にデータの読み取りと書き込みのみの権限を持つユーザーを指定することが必要になる場合があります。 詳細については、「[テスト環境としての IIS への配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)」の「 **Code First Migrations の Web.config の自動変更を確認**する」を参照してください。

## <a name="configuring-database-deployment-for-the-test-environment"></a>テスト環境のデータベース配置の構成

次に、各データベースに対して次のタスクが実行されるように Visual Studio を構成します。

- コピー先データベースにソースデータベースの構造 (テーブル、列、制約など) を作成する SQL スクリプトを生成します。
- 転送元データベースのデータをコピー先のデータベースのテーブルに挿入する SQL スクリプトを生成します。
- 生成されたスクリプトと、作成した Grant スクリプトを対象のデータベースに実行します。

プロジェクトの**プロパティ**ウィンドウを開き、 **[SQL のパッケージ化/発行]** タブを選択します。

**[構成]** ドロップダウンリストで **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認します。

[**このページを有効にする] を**クリックします。

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

**[SQL のパッケージ化/発行]** タブは、従来の配置方法を指定するため、通常は無効になっています。 ほとんどのシナリオでは、 **Web の発行**ウィザードでデータベースの配置を構成する必要があります。 SQL Server Compact から SQL Server または SQL Server Express への移行は、この方法が適切な選択である特殊なケースです。

[Web.config**からのインポート] を**クリックします。

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual *Studio は、web.config ファイルで*接続文字列を検索し、メンバーシップデータベース用と School データベース用の接続文字列を検索し、**データベースエントリ**テーブル内の各接続文字列に対応する行を追加します。 検出された接続文字列は既存の SQL Server Compact データベース用です。次の手順では、これらのデータベースを配置する方法と場所を構成します。

データベースの配置設定は、データベース**エントリ**のテーブルの下にある **[データベースエントリの詳細]** セクションに入力します。 次の図に示すように、データベースエントリの **[詳細]** セクションに表示される設定は、 **[データベースエントリ]** テーブルのいずれかの行に関連します。

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>メンバーシップデータベースの配置設定の構成

メンバーシップデータベースに適用される設定を構成するには、 **[データベースエントリ]** テーブルで**Defaultconnection-Deployment**行を選択します。

**[転送先データベースの接続文字列]** に、新しい SQL Server Express メンバーシップデータベースを指す接続文字列を入力します。 **サーバーエクスプローラー**から必要な接続文字列を取得できます。 **サーバーエクスプローラー**で、 **[データ接続]** を展開し、 **aspnetTest**データベースを選択します。次に、 **[プロパティ]** ウィンドウで、**接続文字列**の値をコピーします。

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

ここでは、同じ接続文字列が再現されます。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

この接続文字列をコピーし、 **[SQL のパッケージ化/発行]** タブの **[転送先データベースの接続文字列]** に貼り付けます。

**[既存のデータベースからデータまたはスキーマをプル**する] が選択されていることを確認します。 これにより、SQL スクリプトが自動的に生成され、転送先データベースで実行されます。

**ソースデータベースの値の接続文字列***は、web.config ファイルから*抽出され、開発 SQL Server Compact データベースを指します。 これは、変換先データベースで後で実行されるスクリプトを生成するために使用されるソースデータベースです。 データベースの実稼働バージョンを配置するため、"aspnet-Dev" を "aspnet-Prod" に変更します。

データ (ユーザーアカウントとロール) とデータベース構造をコピーする必要があるので、**データベーススクリプト作成オプション**をスキーマから**スキーマおよびデータ**に**のみ**変更します。

以前に作成した許可スクリプトを実行するように配置を構成するには、 **[データベーススクリプト]** セクションに追加する必要があります。 **[スクリプトの追加]** をクリックし、 **[SQL スクリプトの追加]** ダイアログボックスで、grant スクリプトを保存したフォルダーに移動します (これは、ソリューションファイルが格納されているフォルダーです)。 *Grant .sql*という名前のファイルを選択し、 **[開く]** をクリックします。

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

**データベースエントリ**の**Defaultconnection-デプロイ**行の設定は、次の図のようになります。

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School データベースの展開設定を構成する

次に、 **[データベースエントリ]** テーブルの**schoolcontext.cs**行を選択して、School データベースの配置設定を構成します。

前に使用したのと同じ方法を使用して、新しい SQL Server Express データベースの接続文字列を取得できます。 **[SQL のパッケージ化/発行]** タブで、この接続文字列を**転送先データベースの接続文字列**にコピーします。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

**[既存のデータベースからデータまたはスキーマをプル**する] が選択されていることを確認します。

**ソースデータベースの値の接続文字列***は、web.config ファイルから*抽出され、開発 SQL Server Compact データベースを指します。 "School-Dev" を "School-Prod" に変更して、データベースの実稼働バージョンを展開します。 (App\_Data フォルダーに School-Prod ファイルを作成したことはありません。そのため、後で ContosoUniversity プロジェクトフォルダー内の App\_Data フォルダーにそのファイルをテスト環境からコピーします)。

**データベーススクリプト作成オプション**を**スキーマおよびデータ**に変更します。

また、スクリプトを実行して、このデータベースに対する読み取りと書き込みのアクセス許可をアプリケーションプール id に付与する必要があります。そのため、メンバーシップデータベースの場合と同様に、 *grant .sql*スクリプトファイルを追加します。

完了すると、**データベースエントリ**の**schoolcontext.cs**行の設定は次の図のようになります。

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

**[SQL のパッケージ化/発行]** タブへの変更を保存します。

*C:\inetpub\wwwroot\ContosoUniversity\App\_data*フォルダーの*School-Prod*ファイルを、ContosoUniversity プロジェクトの*App\_data*フォルダーにコピーします。

### <a name="specifying-transacted-mode-for-the-grant-script"></a>Grant スクリプトのトランザクションモードの指定

配置プロセスでは、データベーススキーマとデータを配置するスクリプトが生成されます。 既定では、これらのスクリプトはトランザクション内で実行されます。 ただし、既定では、カスタムスクリプト (grant スクリプトなど) はトランザクションでは実行されません。 配置プロセスでトランザクションモードが混在している場合、配置中にスクリプトを実行すると、タイムアウトエラーが発生することがあります。 このセクションでは、トランザクションで実行するカスタムスクリプトを構成するために、プロジェクトファイルを編集します。

**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクトを右クリックし、 **[プロジェクトのアンロード]** を選択します。

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

次に、プロジェクトを再び右クリックし、 **[Edit ContosoUniversity]** を選択します。

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio エディターには、プロジェクトファイルの XML コンテンツが表示されます。 `PropertyGroup` 要素がいくつかあることに注意してください。 (イメージでは、`PropertyGroup` 要素の内容は省略されています)。

![プロジェクトファイルエディターウィンドウ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

最初の1つは、`Condition` 属性を持たないもので、ビルド構成に関係なく適用される設定です。 1つの `PropertyGroup` 要素は、デバッグビルド構成にのみ適用されます (`Condition` 属性に注意してください)。1つはリリースビルド構成にのみ適用され、もう1つはテストビルド構成にのみ適用されます。 リリースビルド構成の `PropertyGroup` 要素内に、 **[SQL のパッケージ化/発行]** タブで入力した設定を含む `PublishDatabaseSettings` 要素が表示されます。指定した各 grant スクリプトに対応する `Object` 要素があります ("Grant .sql" の2つのインスタンスに注意してください)。 既定では、各 grant スクリプトの `Source` 要素の `Transacted` 属性は `False`です。

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

`Source` 要素の `Transacted` 属性の値を `True`に変更します。

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

プロジェクトファイルを保存して閉じ、**ソリューションエクスプローラー**でプロジェクトを右クリックして、 **[プロジェクトの再読み込み]** を選択します。

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>接続文字列の web.config 変換の設定

**[Sql のパッケージ化/発行]** タブで入力した新しい sql Express データベースの接続文字列は、配置時に移行先データベースを更新する場合にのみ Web 配置によって使用されます。 *配置された web.config ファイル*内の接続文字列が新しい SQL Server Express データベースを指すように *、web.config の変換を*設定する必要があります。 ( **[SQL のパッケージ化/発行]** タブを使用する場合、発行プロファイルで接続文字列を構成することはできません)。

Web.config*を開き、* `connectionStrings` 要素を次の例の `connectionStrings` 要素に置き換えます。 (コンテキストを提供するためにここに示されている周囲のコードではなく、connectionStrings 要素のみをコピーするようにしてください)。

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

このコードにより、配置された*web.config*ファイルで、各 `add` 要素の `connectionString` と `providerName` 属性が置き換えられます。 これらの接続文字列は、 **[SQL のパッケージ化/発行]** タブで入力したものと同じではありません。Entity Framework とユニバーサルプロバイダーに必要なため、設定 "MultipleActiveResultSets = True" が追加されました。

## <a name="installing-sql-server-compact"></a>SQL Server Compact のインストール

SqlServerCompact NuGet パッケージには、Contoso 大学アプリケーション用の SQL Server Compact データベースエンジンアセンブリが用意されています。 ただし現在は、SQL Server データベースで実行するスクリプトを作成するために、SQL Server Compact データベースを読み取ることができる Web 配置アプリケーションではありません。 Web 配置が SQL Server Compact データベースを読み取ることができるようにするには、 [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)のリンクを使用して開発用コンピューターに SQL Server Compact をインストールします。

## <a name="deploying-to-the-test-environment"></a>テスト環境への配置

テスト環境に発行するには、発行プロファイルデータベースの設定ではなく、データベースの発行の **[SQL のパッケージ化/発行]** タブを使用するように構成された発行プロファイルを作成する必要があります。

まず、既存のテストプロファイルを削除します。

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。

**[プロファイル]** タブを選択します。

**[プロファイルの管理]** をクリックします。

**[テスト]** を選択し、 **[削除]** をクリックして、 **[閉じる]** をクリックします。

この変更を保存するには、 **Web の発行**ウィザードを閉じます。

次に、新しいテストプロファイルを作成し、それを使用してプロジェクトを発行します。

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。

**[プロファイル]** タブを選択します。

ドロップダウンリストから  **&lt;新規作成...&gt;** を選択し、プロファイル名として「Test」と入力します。

**[サービス URL]** ボックスに、「 *localhost*」と入力します。

**[サイト/アプリケーション]** ボックスに、「 *Default Web Site/ContosoUniversity」と*入力します。

**[宛先 URL]** ボックスに、「`http://localhost/ContosoUniversity/`」と入力します。

[次へ] をクリックします。

**設定** タブには、**SQL のパッケージ化/発行** タブが構成されていることが警告され、新しいデータベースの公開の強化を有効にする をクリックして上書きすることができます。 このデプロイでは、 **[SQL のパッケージ化/発行]** タブの設定を上書きしないため、 **[次へ]** をクリックします。

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

**[プレビュー]** タブには、**パブリッシュするデータベースが選択**されていないことを示すメッセージが表示されますが、これは、データベースの発行が発行プロファイルで構成されていないことを意味します。

**[発行]** をクリックします。

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio によってアプリケーションが配置され、テスト環境のサイトのホームページにブラウザーが開かれます。 インストラクターページを実行して、前に見たものと同じデータが表示されていることを確認します。 **[学生の追加]** ページを実行し、新しい学生を追加して、 **[students]** ページで新しい学生を表示します。 これにより、データベースを更新できるかどうかが確認されます。 **[更新プログラムのクレジット]** ページ (ログインする必要があります) を選択して、メンバーシップデータベースが展開されていて、それにアクセスできることを確認します。

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>運用環境用の SQL Server データベースの作成

テスト環境にデプロイしたので、運用環境へのデプロイをセットアップする準備ができました。 テスト環境の場合は、配置先のデータベースを作成することによって開始します。 概要を思い出してください。 Cytanium Lite ホスティングプランでは、単一の SQL Server データベースのみが許可されているため、2つではなく、データベースを1つだけ設定します。 メンバーシップと学校 SQL Server Compact データベースのすべてのテーブルとデータは、運用環境の1つの SQL Server データベースにデプロイされます。

[http://panel.cytanium.com](http://panel.cytanium.com)の Cytanium コントロールパネルにアクセスします。 **データベース**上にマウスポインターを置き、 **[SQL Server 2008]** をクリックします。

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

**[SQL Server 2008]** ページで、 **[データベースの作成]** をクリックします。

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

データベースに "School" という名前を付け、 **[保存]** をクリックします。 (このページではプレフィックス "contosouSchool" が自動的に追加されるため、有効な名前は "" になります)。

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

同じページで、 **[ユーザーの作成]** をクリックします。 Cytanium のサーバーでは、統合 Windows セキュリティを使用するのではなく、アプリケーションプールの id でデータベースを開いて、データベースを開く権限を持つユーザーを作成します。 ユーザーの資格情報を、実稼働の*web.config*ファイルにある接続文字列に追加します。 この手順では、これらの資格情報を作成します。

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

**[SQL ユーザーのプロパティ]** ページで、必要なフィールドを入力します。

- 名前として「ユーザー」と入力します。
- パスワードを入力してください。
- 既定のデータベースとして **[contosouSchool]** を選択します。
- **[ContosouSchool]** チェックボックスをオンにします。

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>運用環境のデータベース配置の構成

これで、前にテスト環境で行ったように、 **[SQL のパッケージ化/発行]** タブでデータベース配置設定を設定できるようになりました。

プロジェクトの**プロパティ**ウィンドウを開き、 **[SQL のパッケージ化/発行]** タブを選択し、 **[構成]** ドロップダウンリストで **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認します。

各データベースの配置設定を構成する場合、運用環境とテスト環境の間の主な違いは、接続文字列の構成方法です。 テスト環境では、複数の変換先データベースの接続文字列を入力しましたが、運用環境では、両方のデータベースで同期先接続文字列が同じになります。 これは、両方のデータベースを運用環境の1つのデータベースに配置するためです。

### <a name="configuring-deployment-settings-for-the-membership-database"></a>メンバーシップデータベースの配置設定の構成

メンバーシップデータベースに適用される設定を構成するには、**データベースエントリ**テーブルで**Defaultconnection-Deployment**行を選択します。

**[転送先データベースの接続文字列]** に、先ほど作成した新しい実稼働 SQL Server データベースを指す接続文字列を入力します。 ウェルカムメールから接続文字列を取得できます。 電子メールの関連部分には、次のサンプルの接続文字列が含まれています。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

3つの変数を置き換えた後、必要な接続文字列は次の例のようになります。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

この接続文字列をコピーし、 **[SQL のパッケージ化/発行]** タブの **[転送先データベースの接続文字列]** に貼り付けます。

**既存のデータベースからのデータまたはスキーマのプル**がまだ選択されていること、および**データベーススクリプト作成オプション**がまだ**スキーマとデータ**であることを確認します。

**[データベーススクリプト]** ボックスで、Grant .sql スクリプトの横にあるチェックボックスをオフにします。

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School データベースの展開設定を構成する

次に、School データベースの設定を構成するために、 **[データベースエントリ]** テーブルの**schoolcontext.cs**行を選択します。

メンバーシップデータベースのフィールドにコピーしたコピー**先データベースの接続文字列**に、同じ接続文字列をコピーします。

**既存のデータベースからのデータまたはスキーマのプル**がまだ選択されていること、および**データベーススクリプト作成オプション**がまだ**スキーマとデータ**であることを確認します。

**[データベーススクリプト]** ボックスで、Grant .sql スクリプトの横にあるチェックボックスをオフにします。

**[SQL のパッケージ化/発行]** タブへの変更を保存します。

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>運用データベースへの接続文字列の Web.config 変換の設定

次に *、配置された web.config ファイル*内の接続文字列が新しい実稼働データベースを指すように*web.config 変換を設定します。* 使用する Web 配置の **[SQL のパッケージ化/発行]** タブで入力した接続文字列は、`MultipleResultSets` オプションを追加する場合を除いて、アプリケーションで使用する必要がある接続文字列と同じです。

Web.config*を開き、* `connectionStrings` 要素を次の例のような `connectionStrings` 要素に置き換えます。 (コンテキストを表示するために提供されているタグではなく、`connectionStrings` の要素のみをコピーします)。

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

*Web.config ファイルで*接続文字列を常に暗号化するように指示するアドバイスが表示されることがあります。 これは、自社のネットワーク上のサーバーにを展開する場合に適しています。 ただし、共有ホスティング環境に配置する場合は、ホスティングプロバイダーのセキュリティプラクティスを信頼しているため、接続文字列を暗号化する必要はありません。

## <a name="deploying-to-the-production-environment"></a>運用環境への配置

これで、運用環境にデプロイする準備ができました。 Web 配置は、プロジェクトの*アプリ\_data*フォルダー内の SQL Server Compact データベースを読み取り、すべてのテーブルとデータを運用環境の SQL Server データベースに再作成します。 **[Web のパッケージ化/発行]** タブ設定を使用して発行するには、運用環境用の新しい発行プロファイルを作成する必要があります。

最初に、以前のテストプロファイルと同じように、既存の運用プロファイルを削除します。

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。

**[プロファイル]** タブを選択します。

**[プロファイルの管理]** をクリックします。

**[運用]** を選択し、 **[削除]** をクリックして、 **[閉じる]** をクリックします。

この変更を保存するには、 **Web の発行**ウィザードを閉じます。

次に、新しい実稼働プロファイルを作成し、それを使用してプロジェクトを発行します。

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。

**[プロファイル]** タブを選択します。

**[インポート]** をクリックし、前の手順でダウンロードした .publishsettings ファイルを選択します。

**[接続]** タブで、**宛先 URL**を正しい一時 URL (この例では http://contosouniversity.com.vserver01.cytanium.com ) に変更します。

プロファイルの名前を運用環境に変更します。 ( **[プロファイル]** タブを選択し、 **[プロファイルの管理]** をクリックして実行します)。

Web の**発行**ウィザードを閉じて、変更を保存します。

実稼働環境でデータベースが更新されている実際のアプリケーションでは、発行する前に、次の2つの手順を実行します。

1. 「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルに示されているように、*アプリ\_offline .htm*をアップロードします。
2. Cytanium コントロールパネルの**ファイルマネージャー**機能を使用して、 *Aspnet-Prod*ファイルと*School-Prod*ファイルを運用サイトから ContosoUniversity プロジェクトの*App\_Data*フォルダーにコピーします。 これにより、新しい SQL Server データベースに配置しているデータに、運用 web サイトによって行われた最新の更新が確実に含まれるようになります。

Web 上の **[発行**] ツールバーで、**運用**プロファイルが選択されていることを確認し、 **[発行]** をクリックします。

発行する前に<em>\_offline .htm</em>をアップロードした場合は、Cytanium コントロールパネルの [<strong>ファイルマネージャー</strong> ] ユーティリティを使用して、<em>アプリ\_をオフライン</em>で削除する必要があります。をテストする前に、.htm を使用します。 また、<em>アプリ\_データ</em>フォルダーから<em>.sdf</em>ファイルを削除することもできます。

これで、ブラウザーを開き、パブリックサイトの URL にアクセスして、テスト環境に配置した後と同じようにアプリケーションをテストできるようになりました。

## <a name="switching-to-sql-server-express-localdb-in-development"></a>開発中の SQL Server Express LocalDB への切り替え

概要で説明したように、通常は、テストおよび運用環境で使用する開発で同じデータベースエンジンを使用することをお勧めします。 (開発環境で SQL Server Express を使用する利点は、開発環境、テスト環境、および運用環境でデータベースが同じように機能することです)。このセクションでは、Visual Studio からアプリケーションを実行するときに、LocalDB SQL Server Express を使用するように ContosoUniversity プロジェクトを設定します。

この移行を実行する最も簡単な方法は、Code First して、メンバーシップシステムによって新しい開発データベースの両方を作成できるようにすることです。 この方法を移行に使用するには、次の3つの手順が必要です。

1. 新しい SQL Express LocalDB データベースを指定するように接続文字列を変更します。
2. Web サイト管理ツールを実行して、管理者ユーザーを作成します。 これにより、メンバーシップデータベースが作成されます。
3. アプリケーションデータベースの作成とシードを行うには、Code First Migrations を使用します。

### <a name="updating-connection-strings-in-the-webconfig-file"></a>Web.config ファイル内の接続文字列の更新

*Web.config ファイルを*開き、`connectionStrings` 要素を次のコードに置き換えます。

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>メンバーシップデータベースの作成

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択し、 **[プロジェクト]** メニューの **[ASP.NET の構成]** をクリックします。

[セキュリティ] タブを選択します。

**[ロールの作成または管理]** をクリックし、**管理者**ロールを作成します。

[セキュリティ] タブに戻ります。

**[ユーザーの作成]** をクリックし、 **[管理者]** チェックボックスをオンにして、admin という名前のユーザーを作成します。

**Web サイト管理ツール**を閉じます。

### <a name="creating-the-school-database"></a>School データベースを作成する

パッケージマネージャーコンソールウィンドウを開きます。

**[既定のプロジェクト]** ドロップダウンリストで、ContosoUniversity プロジェクトを選択します。

次のコマンドを入力します。

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First Migrations は、データベースを作成する最初の移行を適用してから、AddBirthDate 移行を適用してから、Seed メソッドを実行します。

Ctrl キーを押しながら F5 キーを押して、サイトを実行します。 テスト環境と運用環境で行ったように、 **[学生の追加]** ページを実行し、新しい学生を追加して、 **[students]** ページで新しい学生を表示します。 これにより、School データベースが作成および初期化されたこと、およびそのデータベースへの読み取りと書き込みのアクセス権があることが確認されます。

**[更新プログラムのクレジット]** ページを選択してログインし、メンバーシップデータベースが展開されていることと、それにアクセスできることを確認します。 ユーザーアカウントを移行していない場合は、管理者アカウントを作成し、 **[更新プログラムのクレジット]** ページを選択して、有効であることを確認します。

## <a name="cleaning-up-sql-server-compact-files"></a>SQL Server Compact ファイルのクリーンアップ

SQL Server Compact をサポートするために含まれていたファイルと NuGet パッケージは不要になりました。 必要に応じて (この手順は必要ありません)、不要なファイルと参照をクリーンアップできます。

**ソリューションエクスプローラー**で、 *App\_Data*フォルダーから *.sdf*ファイルを削除し、 *bin*フォルダーから*amd64*および*x86*フォルダーを削除します。

**ソリューションエクスプローラー**で、(プロジェクトの1つではなく) ソリューションを右クリックし、 **[ソリューションの NuGet パッケージの管理]** をクリックします。

**[NuGet パッケージの管理]** ダイアログボックスの左ペインで、 **[インストールされたパッケージ]** を選択します。

**SqlServerCompact**パッケージを選択し、 **[管理]** をクリックします。

**[プロジェクトの選択**] ダイアログボックスで、両方のプロジェクトが選択されます。 両方のプロジェクトでパッケージをアンインストールするには、両方のチェックボックスをオフにし、[ **OK]** をクリックします。

依存パッケージもアンインストールするかどうかを確認するダイアログボックスが表示されたら、[いいえ] をクリックします。 これらのうちの1つは、保持する必要がある Entity Framework パッケージです。

同じ手順に従って、 **SqlServerCompact**パッケージをアンインストールします。 (パッケージは、 **SqlServerCompact**パッケージが**SqlServerCompact**パッケージに依存しているため、この順序でアンインストールする必要があります)。

これで、SQL Server Express と完全 SQL Server に正常に移行できました。 次のチュートリアルでは、別のデータベースを変更します。テストデータベースと実稼働データベースで SQL Server Express と完全 SQL Server が使用されている場合は、データベースの変更を配置する方法を確認します。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
