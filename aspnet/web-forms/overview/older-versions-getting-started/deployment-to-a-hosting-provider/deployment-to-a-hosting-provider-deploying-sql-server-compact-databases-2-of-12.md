---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server Compact データベースの配置-2/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458254"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server Compact データベースの配置-2/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、配置用に2つの SQL Server Compact データベースとデータベースエンジンを設定する方法について説明します。

データベースアクセスの場合、Contoso 大学アプリケーションは、.NET Framework に含まれていないため、アプリケーションと共に展開する必要がある次のソフトウェアを必要とします。

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (データベースエンジン)。
- [ASP.NET ユニバーサルプロバイダー](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET メンバーシップシステムで SQL Server Compact を使用できるようにする)
- [Entity Framework 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(移行を伴う Code First)。

データベース構造と、アプリケーションの2つのデータベース内のデータの一部 (すべてではない) も配置する必要があります。 通常は、アプリケーションを開発するときに、ライブサイトに配置しないデータベースにテストデータを入力します。 ただし、デプロイするいくつかの実稼働データを入力する場合もあります。 このチュートリアルでは、を展開するときに、必要なソフトウェアと正しいデータが含まれるように Contoso 大学プロジェクトを構成します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact と SQL Server Express

このサンプルアプリケーションでは、SQL Server Compact 4.0 を使用します。 このデータベースエンジンは、web サイトの比較的新しいオプションです。以前のバージョンの SQL Server Compact は、web ホスティング環境では機能しません。 SQL Server Compact には、SQL Server Express を使用した開発と完全 SQL Server への展開の一般的なシナリオと比較して、いくつかの利点があります。 選択したホスティングプロバイダーによっては、SQL Server Compact をデプロイする方がコストがかかることがあります。これは、一部のプロバイダーが完全 SQL Server データベースをサポートするために追加料金を支払うためです。 SQL Server Compact に対して追加料金は発生しません。これは、web アプリケーションの一部としてデータベースエンジン自体をデプロイできるためです。

ただし、制限も考慮する必要があります。 SQL Server Compact では、ストアドプロシージャ、トリガー、ビュー、またはレプリケーションはサポートされていません。 (SQL Server Compact でサポートされていない SQL Server の機能の完全な一覧については、「 [SQL Server Compact と SQL Server の違い](https://msdn.microsoft.com/library/bb896140.aspx)」を参照してください)。また、SQL Server Express および SQL Server データベースのスキーマやデータを操作するために使用できるツールの中には、SQL Server Compact では機能しないものもあります。 たとえば、Visual Studio で SQL Server Compact データベースを使用して SQL Server Management Studio または SQL Server Data Tools を使用することはできません。 SQL Server Compact データベースを操作するための他のオプションがあります。

- Visual Studio でサーバーエクスプローラーを使用すると、SQL Server Compact に対して制限されたデータベース操作機能を提供できます。
- [WebMatrix](https://www.microsoft.com/web/webmatrix/)のデータベース操作機能を使用できます。これにはサーバーエクスプローラーよりも多くの機能があります。
- [SQL Server Compact ツールボックス](https://github.com/ErikEJ/SqlCeToolbox)や[SQL Compact データやスキーマスクリプトユーティリティ](https://github.com/ErikEJ/SqlCeToolbox)など、比較的多機能なサードパーティまたはオープンソースのツールを使用できます。
- 独自の DDL (データ定義言語) スクリプトを記述して実行し、データベーススキーマを操作できます。

SQL Server Compact から開始し、必要に応じて後でアップグレードすることができます。 このシリーズの後のチュートリアルでは、SQL Server Compact から SQL Server Express および SQL Server に移行する方法について説明します。 ただし、新しいアプリケーションを作成していて、近い将来に SQL Server が必要になることが予想される場合は、SQL Server または SQL Server Express から始めることをお勧めします。

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>展開のための SQL Server Compact データベースエンジンの構成

Contoso 大学アプリケーションでのデータアクセスに必要なソフトウェアは、次の NuGet パッケージをインストールすることによって追加されました。

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.web. providers](http://nuget.org/List/Packages/System.Web.Providers) (ASP.NET ユニバーサルプロバイダー)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

リンクは、これらのパッケージの現在のバージョンを指しています。これらのパッケージは、このチュートリアルでダウンロードしたスタートプロジェクトにインストールされているものよりも新しい可能性があります。 ホスティングプロバイダーへの配置については、Entity Framework 5.0 以降を使用していることを確認してください。 以前のバージョンの Code First Migrations には完全な信頼が必要であり、多くのホスティングプロバイダーでは、アプリケーションは中程度の信頼で実行されます。 中程度の信頼の詳細については、「[テスト環境として IIS に配置する](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)」チュートリアルを参照してください。

NuGet パッケージのインストールは、通常、このソフトウェアをアプリケーションと共に展開するために必要なすべての処理を行います。 場合によっては、web.config ファイルの変更や、ソリューションをビルドするたびに実行される PowerShell スクリプトの追加などのタスクが必要になります。 **NuGet を使用せずにこれらの機能 (SQL Server Compact や Entity Framework など) のサポートを追加する場合は、NuGet パッケージのインストールによって、同じ作業を手動で行うことができることを確認してください。**

正常に展開できるようにするために必要なすべての処理が NuGet によって処理されない例外が1つあります。 SqlServerCompact NuGet パッケージは、プロジェクトにビルド後のスクリプトを追加します。このスクリプトは、ネイティブアセンブリをプロジェクトの*bin*フォルダーの下にある*x86*および*amd64*サブフォルダーにコピーしますが、スクリプトにはプロジェクト内のこれらのフォルダーは含まれません。 結果として、プロジェクトに手動で含める場合を除き、Web 配置によってコピー先の Web サイトにコピーされません。 (この動作は、既定の配置構成によって発生します。このチュートリアルでは使用しないもう1つのオプションは、この動作を制御する設定を変更することです。 変更できる設定は、 **[プロジェクトのプロパティ]** ウィンドウの **[パッケージ/発行 Web]** タブで、 **[配置する項目]** で**アプリケーションを実行するために必要なファイルのみ**です。 通常、この設定を変更することは、必要以上に多くのファイルが運用環境に展開される可能性があるため、通常は推奨されません。 代替方法の詳細については、「[プロジェクトプロパティの構成](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)」チュートリアルを参照してください。)

プロジェクトをビルドし、**ソリューションエクスプローラー** [すべての**ファイルを表示**] をクリックします (まだ作成していない場合)。 また、 **[更新]** をクリックする必要がある場合もあります。

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

**[Bin]** フォルダーを展開して**amd64**および**x86**フォルダーを表示し、それらのフォルダーを選択して右クリックし、 **[プロジェクトに含める]** を選択します。

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

フォルダーアイコンが変更され、そのフォルダーがプロジェクトに含まれていることが示されます。

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>アプリケーションデータベースの展開のための Code First Migrations の構成

アプリケーションデータベースを配置する場合、通常は、単に開発データベースを運用環境に配置するだけではありません。これは、ほとんどのデータがテスト目的でのみ使用されるためです。 たとえば、テストデータベースの学生名は架空の名前です。 一方、データがまったく存在しないデータベース構造だけを配置することはほとんどありません。 テストデータベースの一部のデータは実際のデータであり、ユーザーがアプリケーションの使用を開始するときに必要になる場合があります。 たとえば、有効なグレード値または実際の部署名を含むテーブルがデータベースに存在する場合があります。

この一般的なシナリオをシミュレートするには、実稼働環境に配置するデータのみをデータベースに挿入する Code First Migrations Seed メソッドを構成します。 このシードメソッドは、実稼働環境でデータベースを作成 Code First た後に運用環境で実行されるため、テストデータを挿入しません。

以前のバージョンの Code First では、移行がリリースされる前に、シードメソッドによってテストデータを挿入することが一般的でした。これは、開発時にすべてのモデルが変更されたため、データベースを完全に削除してから再作成する必要があるためです。 Code First Migrations では、データベースの変更後にテストデータが保持されるため、Seed メソッドにテストデータを含める必要はありません。 ダウンロードしたプロジェクトは、初期化子クラスのシードメソッドにすべてのデータを含めるための移行前の方法を使用します。 このチュートリアルでは、初期化子クラスを無効にして、移行を有効にします。 次に、移行構成クラスの Seed メソッドを更新して、運用環境に挿入するデータのみを挿入するようにします。

次の図は、アプリケーションデータベースのスキーマを示しています。

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

これらのチュートリアルでは、サイトを最初に展開するときに、`Student` テーブルと `Enrollment` テーブルが空であると想定します。 他のテーブルには、アプリケーションが稼働しているときに事前に読み込む必要があるデータが含まれています。

Code First Migrations を使用するため、 **Dropcreatedatabaseifmodelchanges** Code First 初期化子を使用する必要がなくなりました。 この初期化子のコードは、ContosoUniversity プロジェクトの SchoolInitializer.cs ファイルにあります。 Web.config ファイルの**appSettings**要素の設定により、アプリケーションが初めてデータベースにアクセスしようとしたときに、この初期化子が実行されます。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

アプリケーションの Web.config ファイルを開き、appSettings 要素から Code First 初期化子クラスを指定する要素を削除します。 AppSettings 要素は次のようになります。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 初期化子クラスを指定するもう1つの方法は、 *global.asax*ファイルの `Application_Start` メソッドで `Database.SetInitializer` を呼び出すことによって行います。 そのメソッドを使用して初期化子を指定するプロジェクトで移行を有効にする場合は、そのコード行を削除します。

次に、Code First Migrations を有効にします。

最初の手順として、ContosoUniversity プロジェクトがスタートアッププロジェクトとして設定されていることを確認します。 **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[スタートアッププロジェクトに設定]** を選択します。 Code First Migrations によってスタートアッププロジェクトが検索され、データベース接続文字列が検索されます。

**[ツール]** メニューで **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順にクリックします。

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

**パッケージマネージャーコンソール**ウィンドウの上部で、既定のプロジェクトとして [ContosoUniversity] を選択し、`PM>` プロンプトで「enable-移行」と入力します。

![enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

このコマンドを実行すると、ContosoUniversity プロジェクトの新しい [*移行*] フォルダーに*Configuration.cs*ファイルが作成されます。

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

DAL プロジェクトを選択しました。これは、Code First コンテキストクラスを含むプロジェクトで [移行を有効にする] コマンドを実行する必要があるためです。 このクラスがクラスライブラリプロジェクト内にある場合、Code First Migrations は、ソリューションのスタートアッププロジェクトでデータベース接続文字列を検索します。 ContosoUniversity ソリューションでは、web プロジェクトはスタートアッププロジェクトとして設定されています。 (Visual Studio でスタートアッププロジェクトとして接続文字列を含むプロジェクトを指定しない場合は、PowerShell コマンドでスタートアッププロジェクトを指定できます。 [移行を有効にする] コマンドのコマンド構文を確認するには、「get-help enable-移行」というコマンドを入力します)。

Configuration.cs ファイルを開き、`Seed` メソッドのコメントを次のコードに置き換えます。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

名前空間の `using` ステートメントをまだ持っていないため、`List` への参照の下に赤い波線が表示されます。 `List` のインスタンスの1つを右クリックし、 **[解決]** をクリックして、 **[using]** をクリックします。

![Using ステートメントを使用して解決する](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

このメニューを選択すると、ファイルの先頭付近にある `using` のステートメントに次のコードが追加されます。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> `Seed` メソッドにコードを追加することは、データベースに固定データを挿入する多くの方法の1つです。 別の方法として、各移行クラスの `Up` および `Down` メソッドにコードを追加する方法があります。 `Up` および `Down` メソッドには、データベースの変更を実装するコードが含まれています。 これらの例については、「[データベースの更新のデプロイ](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)」チュートリアルを参照してください。
> 
> `Sql` メソッドを使用して SQL ステートメントを実行するコードを記述することもできます。 たとえば、Department テーブルに予算列を追加し、移行の一部としてすべての部門の予算を $1000.00 に初期化する必要がある場合は、その移行の `Up` メソッドに次のコード行を追加します。
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> このチュートリアルで示されているこの例では、Code First Migrations `Configuration` クラスの `Seed` メソッドの `AddOrUpdate` メソッドを使用します。 Code First Migrations は、移行のたびに `Seed` メソッドを呼び出します。このメソッドは、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。 `AddOrUpdate` メソッドは、お客様のシナリオに最適な選択肢ではない可能性があります。 詳細については、「ジュリー Lerman のブログの[EF 4.3 AddOrUpdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。

CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。

次の手順では、初期移行のために `DbMigration` クラスを作成します。 この移行を使用して新しいデータベースを作成する場合は、既に存在するデータベースを削除する必要があります。 SQL Server Compact データベースは、 *App\_Data*フォルダー内の *.sdf*ファイルに含まれています。 **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトの [*アプリ\_データ*] を展開して、 *.sdf*ファイルで表される2つの SQL Server Compact データベースを表示します。

*School*ファイルを右クリックし、 **[削除]** をクリックします。

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

**[パッケージマネージャーコンソール]** ウィンドウで、「最初の移行を作成するには」というコマンドを入力し、"initial" という名前を指定します。

![add-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First Migrations は、*移行*フォルダーに別のクラスファイルを作成します。このクラスには、データベーススキーマを作成するコードが含まれています。

**パッケージマネージャーコンソール**で、"データベースの更新" コマンドを入力してデータベースを作成し、 **Seed**メソッドを実行します。

![update-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(テーブルが既に存在していて作成できないことを示すエラーが表示される場合は、データベースを削除した後、`update-database`を実行する前にアプリケーションを実行したことが原因である可能性があります。 その場合は、 *School .sdf*ファイルをもう一度削除し、`update-database` コマンドを再試行してください)。

アプリケーションを実行します。 これで、Students ページは空になりますが、インストラクターのページにはインストラクターが含まれています。 これは、アプリケーションをデプロイした後、運用環境で使用できるようにするためのものです。

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

これで、プロジェクトは*School*データベースをデプロイする準備ができました。

## <a name="creating-a-membership-database-for-deployment"></a>配置のためのメンバーシップデータベースの作成

Contoso 大学アプリケーションは、ASP.NET メンバーシップシステムとフォーム認証を使用してユーザーを認証および承認します。 ページの1つは、管理者のみがアクセスできます。 このページを表示するには、アプリケーションを実行し、 **[コース]** の下にあるポップアップメニューから **[更新プログラムのクレジット]** を選択します。 アプリケーションでは、管理者のみが **[クレジットの更新]** ページを使用することが許可されているので、 **[ログイン]** ページが表示されます。

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

パスワード "Pas $ w0rd" を使用して "admin" としてログインします ("w0rd" の文字 "o" の代わりに数字0が表示されます)。 ログインすると、 **[更新プログラムのクレジット]** ページが表示されます。

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

サイトを初めて展開する場合は、テスト用に作成したユーザーアカウントのほとんどまたはすべてを除外するのが一般的です。 この場合は、管理者アカウントを展開し、ユーザーアカウントを使用しません。 テストアカウントを手動で削除するのではなく、運用環境で必要な管理者ユーザーアカウントを1つだけ持つ新しいメンバーシップデータベースを作成します。

> [!NOTE]
> メンバーシップデータベースには、アカウントパスワードのハッシュが格納されます。 あるコンピューターから別のコンピューターにアカウントを展開するには、ハッシュルーチンが、移行元コンピューターとは異なるハッシュを移行先サーバー上で生成しないようにする必要があります。 既定のアルゴリズムを変更しない限り、ASP.NET ユニバーサルプロバイダーを使用すると、同じハッシュが生成されます。 既定のアルゴリズムは HMACSHA256 で、web.config ファイルの **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** 要素の**validation**属性で指定されています。

メンバーシップデータベースは Code First Migrations によって保持されません。また、データベースにテストアカウントをシードする自動初期化子はありません (School データベースの場合と同様)。 そのため、テストデータを使用可能な状態に保つには、新しいテストデータベースを作成する前に、そのコピーを作成します。

**ソリューションエクスプローラー**で、 *App\_Data*フォルダー内の*aspnet*ファイルの名前を*aspnet-Dev*に変更します。 (コピーを作成しないでください。名前を変更するだけで、新しいデータベースが作成されます)。

**ソリューションエクスプローラー**で、web プロジェクト (ContosoUniversity ではなく ContosoUniversity) が選択されていることを確認します。 次に、 **[プロジェクト]** メニューの **[ASP.NET Configuration]** を選択して、 **Web サイト管理ツール**(WAT) を実行します。

**[セキュリティ]** タブをクリックします。

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

**[ロールの作成または管理]** をクリックし、**管理者**ロールを追加します。

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

**[セキュリティ]** タブに戻り、 **[ユーザーの作成]** をクリックして、管理者としてユーザー "admin" を追加します。 **[ユーザーの作成]** ページの **[ユーザーの作成]** ボタンをクリックする前に、 **[管理者]** チェックボックスがオンになっていることを確認します。 このチュートリアルで使用するパスワードは "Pas $ w0rd" で、任意の電子メールアドレスを入力できます。

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

ブラウザーを閉じます。 **ソリューションエクスプローラー**で、[更新] ボタンをクリックして新しい*aspnet. .sdf*ファイルを表示します。

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

**[Aspnet. .sdf]** を右クリックし、 **[プロジェクトに含める]** を選択します。

## <a name="distinguishing-development-from-production-databases"></a>運用データベースからの開発を区別する

このセクションでは、データベースの名前を変更して、開発バージョンが School-Dev、aspnet-Dev、および production バージョンが School-Prod と aspnet-Prod になるようにします。 これは必須ではありませんが、これを行うと、データベースのテストバージョンと実稼働バージョンが混同されるのを防ぐことができます。

**ソリューションエクスプローラー**で、 **[最新]** の情報に更新 をクリックし、App\_Data フォルダーを展開して、先ほど作成した School データベースを表示します。それを右クリックし、 **[プロジェクトに含める]** を選択します。

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

*Aspnet. .sdf*を*aspnet-Prod*に変更します。

*School .sdf*の名前を*School-Dev*に変更します。

Visual Studio でアプリケーションを実行するときに、- *Dev*バージョンを使用する必要がある *-* 製品版のデータベースファイルを使用しない場合。 そのため、データベースの *-Dev*バージョンを参照するように、web.config ファイル内の接続文字列を変更する必要があります。 (School-Prod ファイルは作成されていませんが、アプリケーションを初めて実行するときに、Code First によってそのデータベースが運用環境に作成されるため、問題はありません)。

アプリケーションの Web.config ファイルを開き、接続文字列を見つけます。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

"Aspnet. .sdf" を "aspnet-Dev" に変更し、"School" を "School-Dev" に変更します。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

これで、SQL Server Compact データベースエンジンと両方のデータベースを配置する準備ができました。 次のチュートリアルでは、開発環境、テスト環境、および運用環境で異なる必要がある設定に対して、web.config ファイルの自動変換を設定*します。* (変更が必要な設定の中には接続文字列がありますが、後で発行プロファイルを作成するときにこれらの変更を設定します)。

## <a name="more-information"></a>詳細情報

NuGet の詳細については、「NuGet と Nuget の[ドキュメント](http://docs.nuget.org/docs/start-here/overview)[を使用したプロジェクトライブラリの管理](https://msdn.microsoft.com/magazine/hh547106.aspx)」を参照してください。 NuGet を使用しない場合は、NuGet パッケージを分析してインストールしたときの動作を確認する方法について学習する必要があります。 (たとえば、web.config 変換を構成したり、PowerShell スクリプトをビルド時に実行するように構成し*たりすること*があります)。NuGet のしくみの詳細については、「パッケージと構成ファイル[の作成と発行](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)」[および「ソースコード変換](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [次へ](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
