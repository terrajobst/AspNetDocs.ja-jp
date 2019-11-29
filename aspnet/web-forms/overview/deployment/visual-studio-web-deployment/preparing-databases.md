---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 'Visual Studio を使用した ASP.NET Web 配置: データベース配置の準備 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618518"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Visual Studio を使用した ASP.NET Web 配置: データベース配置の準備

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、データベースの配置の準備ができているプロジェクトを取得する方法について説明します。 アプリケーションの2つのデータベース内のデータのデータベース構造と一部 (すべてではない) は、テスト環境、ステージング環境、および運用環境に配置する必要があります。

通常は、アプリケーションを開発するときに、ライブサイトに配置しないデータベースにテストデータを入力します。 ただし、いくつかの実稼働データを配置することもできます。 このチュートリアルでは、Contoso 大学プロジェクトを構成し、を展開するときに正しいデータが含まれるように SQL スクリプトを準備します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

このサンプルアプリケーションでは SQL Server Express LocalDB を使用します。 SQL Server Express は SQL Server の無償エディションです。 これは、完全なバージョンの SQL Server と同じデータベースエンジンに基づいているため、開発時によく使用されます。 SQL Server Express でテストし、アプリケーションが実稼働環境でも同じように動作することを保証できます。ただし、SQL Server エディションによって異なる機能については、いくつかの例外があります。

LocalDB は、 *.mdf*ファイルとしてデータベースを操作できるようにする SQL Server Express の特別な実行モードです。 通常、LocalDB データベースファイルは、web プロジェクトの*App\_Data*フォルダーに保持されます。 SQL Server Express のユーザーインスタンス機能では、.mdf ファイルを使用することもでき*ます*が、ユーザーインスタンス機能は非推奨とされます。そのため、 *.mdf*ファイルを使用する場合は LocalDB をお勧めします。

通常 SQL Server Express は、運用 web アプリケーションでは使用されません。 LocalDB は、IIS で動作するように設計されていないため、web アプリケーションでの運用環境での使用は推奨されません。

Visual Studio 2012 では、LocalDB は既定で Visual Studio と共にインストールされます。 Visual Studio 2010 以前のバージョンでは、SQL Server Express (LocalDB なし) が既定で Visual Studio と共にインストールされています。そのため、[このシリーズの最初のチュートリアル](introduction.md)で前提条件の1つとしてインストールしたのはそのためです。

LocalDB を含む SQL Server エディションの詳細については、 [SQL Server データベースで](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)使用する次のリソースを参照してください。

## <a name="entity-framework-and-universal-providers"></a>Entity Framework とユニバーサルプロバイダー

データベースアクセスの場合、Contoso 大学アプリケーションは、.NET Framework に含まれていないため、アプリケーションと共に展開する必要がある次のソフトウェアを必要とします。

- [ASP.NET ユニバーサルプロバイダー](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET メンバーシップシステムで Azure SQL Database を使用できるようにします)
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

このソフトウェアは NuGet パッケージに含まれているため、必要なアセンブリがプロジェクトと共に配置されるように、プロジェクトは既に設定されています。 (このリンクは、これらのパッケージの現在のバージョンを指していますが、このチュートリアルでダウンロードしたスタートプロジェクトにインストールされているものよりも新しい可能性があります)。

Azure ではなくサードパーティのホスティングプロバイダーにデプロイする場合は、Entity Framework 5.0 以降を使用していることを確認してください。 以前のバージョンの Code First Migrations では完全な信頼が必要であり、ほとんどのホスティングプロバイダーは、中程度の信頼でアプリケーションを実行します。 中程度の信頼の詳細については、「[テスト環境として IIS に配置する](deploying-to-iis.md)」チュートリアルを参照してください。

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>アプリケーションデータベースの展開用に Code First Migrations を構成する

Contoso 大学アプリケーションデータベースは Code First によって管理されており、Code First Migrations を使用してデプロイします。 Code First Migrations を使用したデータベース配置の概要については、[このシリーズの最初のチュートリアル](introduction.md)を参照してください。

アプリケーションデータベースを配置する場合、通常は、単に開発データベースを運用環境に配置するだけではありません。これは、ほとんどのデータがテスト目的でのみ使用されるためです。 たとえば、テストデータベースの学生名は架空の名前です。 一方、データがまったく存在しないデータベース構造だけを配置することはほとんどありません。 テストデータベースの一部のデータは実際のデータであり、ユーザーがアプリケーションの使用を開始するときに必要になる場合があります。 たとえば、有効なグレード値または実際の部署名を含むテーブルがデータベースに存在する場合があります。

この一般的なシナリオをシミュレートするには、運用環境に配置するデータのみをデータベースに挿入する Code First Migrations `Seed` メソッドを構成します。 この `Seed` 方法では、運用環境でデータベースを作成 Code First た後に運用環境で実行されるため、テストデータを挿入することはできません。

以前のバージョンの Code First では、移行がリリースされる前に、`Seed` 方法でテストデータを挿入することが一般的でした。これは、開発時にすべてのモデルが変更されたため、データベースを完全に削除してから再作成する必要があるためです。 Code First Migrations では、データベースの変更後にテストデータが保持されるため、`Seed` メソッドにテストデータを含める必要はありません。 ダウンロードしたプロジェクトでは、初期化子クラスの `Seed` メソッドにすべてのデータを含める方法を使用します。 このチュートリアルでは、その初期化子クラスを無効にし、移行を有効にします。 次に、移行構成クラスの `Seed` メソッドを更新して、運用環境に挿入するデータのみを挿入するようにします。

次の図は、アプリケーションデータベースのスキーマを示しています。

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

これらのチュートリアルでは、サイトを最初に展開するときに、`Student` テーブルと `Enrollment` テーブルが空であると想定します。 他のテーブルには、アプリケーションが稼働しているときに事前に読み込む必要があるデータが含まれています。

### <a name="disable-the-initializer"></a>初期化子を無効にする

Code First Migrations を使用するため、`DropCreateDatabaseIfModelChanges` Code First 初期化子を使用する必要はありません。 この初期化子のコードは、ContosoUniversity プロジェクトの*SchoolInitializer.cs*ファイルにあります。 *Web.config ファイルの*`appSettings` 要素の設定により、アプリケーションが初めてデータベースにアクセスしようとするたびに、この初期化子が実行されます。

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

アプリケーションの*web.config*ファイルを開き、Code First 初期化子クラスを指定する `add` 要素を削除またはコメントアウトします。 `appSettings` 要素は次のようになります。

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 初期化子クラスを指定するもう1つの方法は、 *global.asax*ファイルの `Application_Start` メソッドで `Database.SetInitializer` を呼び出すことによって行います。 そのメソッドを使用して初期化子を指定するプロジェクトで移行を有効にする場合は、そのコード行を削除します。

> [!NOTE]
> Visual Studio 2013 を使用している場合は、PMC の手順 2. と 3. (a) の間に次の手順を追加して、EF の現在のバージョンを取得します。 (B) プロジェクトをビルドしてビルドエラーの一覧を取得し、修正します。 存在しなくなった名前空間の using ステートメントを削除し、右クリックして [解決] をクリックし、必要なときに使用するステートメントを追加し、EntityState の発生を EntityState に変更します。

### <a name="enable-code-first-migrations"></a>Code First Migrations を有効にする

1. ContosoUniversity プロジェクト (ContosoUniversity ではない) がスタートアッププロジェクトとして設定されていることを確認します。 **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[スタートアッププロジェクトに設定]** を選択します。 Code First Migrations によってスタートアッププロジェクトが検索され、データベース接続文字列が検索されます。
2. **[ツール]** メニューの [ **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] をクリックします。

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. **パッケージマネージャーコンソール**ウィンドウの上部で、既定のプロジェクトとして [ContosoUniversity] を選択し、`PM>` プロンプトで「enable-移行」と入力します。

    ![-移行コマンドを有効にする](preparing-databases/_static/image4.png)

    ([*移行を有効に*する] コマンドが認識されないというエラーが表示された場合は、コマンド*更新プログラムパッケージ Entityframework-Reinstall*を入力して、もう一度やり直してください。)

    このコマンドを実行すると、ContosoUniversity プロジェクトに*migration フォルダーが*作成され、このフォルダーには、移行の構成に使用できる*Configuration.cs*ファイルと、データベースを作成する最初の移行のための*InitialCreate.cs*ファイルの2つのファイルが配置されます。

    ![移行フォルダー](preparing-databases/_static/image5.png)

    **パッケージマネージャーコンソール**の [既定の**プロジェクト**] ドロップダウンリストで DAL プロジェクトを選択したのは、Code First コンテキストクラスを含むプロジェクトで `enable-migrations` コマンドを実行する必要があるためです。 このクラスがクラスライブラリプロジェクト内にある場合、Code First Migrations は、ソリューションのスタートアッププロジェクトでデータベース接続文字列を検索します。 ContosoUniversity ソリューションでは、web プロジェクトはスタートアッププロジェクトとして設定されています。 Visual Studio でスタートアッププロジェクトとして接続文字列を含むプロジェクトを指定しない場合は、PowerShell コマンドでスタートアッププロジェクトを指定できます。 コマンドの構文を表示するには、`get-help enable-migrations`コマンドを入力します。

    データベースが既に存在しているため、`enable-migrations` コマンドによって最初の移行が自動的に作成されました。 別の方法として、移行によってデータベースを作成することもできます。 これを行うには、移行を有効にする前に、**サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー**を使用して ContosoUniversity データベースを削除します。 移行を有効にした後、"追加-移行 InitialCreate" コマンドを入力して、最初の移行を手動で作成します。 次に、"データベースの更新" コマンドを入力して、データベースを作成できます。

### <a name="set-up-the-seed-method"></a>Seed メソッドを設定する

このチュートリアルでは、Code First Migrations `Configuration` クラスの `Seed` メソッドにコードを追加することによって、固定データを追加します。 Code First Migrations は、移行のたびに `Seed` メソッドを呼び出します。

`Seed` メソッドは移行のたびに実行されるため、最初の移行後にテーブルにデータが既に存在しています。 この状況に対処するには、`AddOrUpdate` メソッドを使用して、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。 `AddOrUpdate` メソッドは、お客様のシナリオに最適な選択肢ではない可能性があります。 詳細については、「ジュリー Lerman のブログの[EF 4.3 AddOrUpdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。

1. *Configuration.cs*ファイルを開き、`Seed` メソッドのコメントを次のコードに置き換えます。

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 名前空間の `using` ステートメントをまだ持っていないため、`List` への参照の下に赤い波線が表示されます。 `List` のインスタンスの1つを右クリックし、 **[解決]** をクリックして、 **[using]** をクリックします。

    ![Using ステートメントを使用して解決する](preparing-databases/_static/image6.png)

    このメニューを選択すると、ファイルの先頭付近にある `using` のステートメントに次のコードが追加されます。

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。

これで、プロジェクトは*ContosoUniversity*データベースを配置する準備ができました。 アプリケーションを配置した後、アプリケーションを初めて実行し、データベースにアクセスするページに移動すると、Code First によってデータベースが作成され、この `Seed` メソッドが実行されます。

> [!NOTE]
> `Seed` メソッドにコードを追加することは、データベースに固定データを挿入する多くの方法の1つです。 別の方法として、各移行クラスの `Up` および `Down` メソッドにコードを追加する方法があります。 `Up` および `Down` メソッドには、データベースの変更を実装するコードが含まれています。 これらの例については、「[データベースの更新のデプロイ](deploying-a-database-update.md)」チュートリアルを参照してください。
> 
> `Sql` メソッドを使用して SQL ステートメントを実行するコードを記述することもできます。 たとえば、Department テーブルに予算列を追加し、移行の一部としてすべての部門の予算を $1000.00 に初期化する必要がある場合は、その移行の `Up` メソッドに次のコード行を追加します。
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>メンバーシップデータベースの展開用スクリプトの作成

Contoso 大学アプリケーションは、ASP.NET メンバーシップシステムとフォーム認証を使用してユーザーを認証および承認します。 **[更新プログラムのクレジット]** ページには、管理者ロールに属しているユーザーのみがアクセスできます。

アプリケーションを実行し、 **[コース]** をクリックして、 **[クレジットの更新]** をクリックします。

![クレジットの更新のクリック](preparing-databases/_static/image7.png)

**[更新プログラムのクレジット]** ページに管理者特権が必要なため、 **[ログイン]** ページが表示されます。

ユーザー名として「 *admin* 」を、パスワードとして「 *devpwd* 」と入力し、 **[ログイン]** をクリックします。

![ログインページ](preparing-databases/_static/image8.png)

**[更新プログラムのクレジット]** ページが表示されます。

![クレジットの更新ページ](preparing-databases/_static/image9.png)

ユーザーとロールの情報*は、web.config ファイルの* **defaultconnection**接続文字列で指定されている*ContosoUniversity*データベースにあります。

このデータベースは Entity Framework Code First によって管理されていないため、移行を使用して展開することはできません。 DbDacFx プロバイダーを使用してデータベーススキーマを配置し、データベーステーブルに初期データを挿入するスクリプトを実行するように発行プロファイルを構成します。

> [!NOTE]
> 新しい ASP.NET メンバーシップシステム (現在は ASP.NET Identity という名前) が Visual Studio 2013 で導入されました。 新しいシステムでは、アプリケーションテーブルとメンバーシップテーブルの両方を同じデータベースに保持することができます。また、Code First Migrations を使用して両方を展開することができます。 サンプルアプリケーションでは、以前の ASP.NET メンバーシップシステムが使用されています。これは、Code First Migrations を使用して展開することはできません。 このメンバーシップデータベースを配置する手順は、アプリケーションが Entity Framework Code First によって作成されていない SQL Server データベースを配置する必要があるその他のシナリオにも適用されます。

ここでも、通常、開発中の運用環境で同じデータを使用する必要はありません。 サイトを初めて展開する場合は、テスト用に作成したユーザーアカウントのほとんどまたはすべてを除外するのが一般的です。 このため、ダウンロードしたプロジェクトには、2つのメンバーシップデータベースがあります。 *aspnet-ContosoUniversity*と development users および*aspnet-ContosoUniversity-Prod*を使用します。 このチュートリアルでは、ユーザー名は*admin*と*nonadmin*の両方のデータベースで同じです。 両方のユーザーには、開発用データベース内の*devpwd*パスワードと、実稼働データベースの*prodpwd*があります。

開発ユーザーをテスト環境に配置し、運用ユーザーをステージングおよび運用環境に展開します。 これを行うには、このチュートリアルで、開発用と運用用の2つの SQL スクリプトを作成します。以降のチュートリアルでは、これらのスクリプトを実行するように発行プロセスを構成します。

> [!NOTE]
> メンバーシップデータベースには、アカウントパスワードのハッシュが格納されます。 あるコンピューターから別のコンピューターにアカウントを展開するには、ハッシュルーチンが、移行元コンピューターとは異なるハッシュを移行先サーバー上で生成しないようにする必要があります。 既定のアルゴリズムを変更しない限り、ASP.NET ユニバーサルプロバイダーを使用すると、同じハッシュが生成されます。 既定のアルゴリズムは HMACSHA256 で、web.config ファイルの **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** 要素の**validation**属性で指定されています。

データ配置スクリプトを手動で作成するには、SQL Server Management Studio (SSMS) を使用するか、サードパーティ製のツールを使用します。 このチュートリアルの残りの部分では、SSMS でその方法を説明しますが、SSMS をインストールして使用しない場合は、プロジェクトの完成版からスクリプトを取得し、ソリューションフォルダーに格納するセクションにスキップできます。

SSMS をインストールするには、ダウンロードセンターからインストールします[2012 Microsoft SQL Server。](https://www.microsoft.com/download/details.aspx?id=29062)これには、 [ENU\x64\SQLManagementStudio\_x64\_enu](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe)または[ENU\x86\SQLManagementStudio\_x86\_enu](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)をクリックします。 システムに対して間違ったものを選択すると、インストールに失敗し、もう一方を試すことができます。

(これは 600 mb のダウンロードであることに注意してください。 インストールには時間がかかる場合があり、コンピューターの再起動が必要になる場合があります)。

SQL Server インストールセンターの最初のページで、[**新規 SQL Server スタンドアロンインストールを実行するか、既存のインストールに機能を追加**します] をクリックし、指示に従って既定の選択肢を受け入れます。

### <a name="create-the-development-database-script"></a>開発用データベーススクリプトの作成

1. SSMS を実行します。
2. **[サーバーへの接続]** ダイアログボックスで、**サーバー名**として *「(localdb) \ v11.0* 」と入力し、 **[認証]** を **[Windows 認証]** のままにして、 **[接続]** をクリックします。

    ![SSMS からサーバーへの接続](preparing-databases/_static/image10.png)
3. **[オブジェクトエクスプローラー]** ウィンドウで、 **[データベース**] を展開し、 **[ContosoUniversity]** を右クリックして、 **[タスク]** をクリックし、 **[スクリプトの生成]** をクリックします。

    ![SSMS のスクリプト生成](preparing-databases/_static/image11.png)
4. **[スクリプトの生成とパブリッシュ]** ダイアログボックスで、 **[スクリプト作成オプションの設定]** をクリックします。

    **[オブジェクトの選択]** ステップはスキップできます。既定では、**データベース全体とすべてのデータベースオブジェクトをスクリプト**化する必要があるためです。
5. **[詳細設定]** をクリックします。

    ![SSMS スクリプト作成オプション](preparing-databases/_static/image12.png)
6. スクリプト **[作成の詳細オプション]** ダイアログボックスで、 **[スクリプトを作成するデータの種類]** までスクロールし、ドロップダウンリストの **[データのみ]** をクリックします。
7. **スクリプトを使用**してデータベースを**False**に変更します。 USE ステートメントは Azure SQL Database に対して有効ではなく、テスト環境での SQL Server Express の配置には必要ありません。

    ![SSMS スクリプトデータのみ、USE ステートメントは使用しない](preparing-databases/_static/image13.png)
8. **[OK]** をクリックします。
9. **[スクリプトの生成とパブリッシュ]** ダイアログボックスの **[ファイル名]** ボックスに、スクリプトを作成する場所を指定します。 ソリューションフォルダー (ContosoUniversity ファイルがあるフォルダー) のパスと、ファイル名を*aspnet-data-dev*に変更します。
10. **[次]** へ をクリックして **[概要]** タブにアクセスし、もう一度 **[次へ]** をクリックしてスクリプトを作成します。

    ![SSMS スクリプトの作成](preparing-databases/_static/image14.png)
11. **[完了]** をクリックします。

### <a name="create-the-production-database-script"></a>実稼働データベーススクリプトを作成する

実稼働データベースでプロジェクトを実行していないため、まだ LocalDB インスタンスにアタッチされていません。 そのため、最初にデータベースをアタッチする必要があります。

1. SSMS**オブジェクトエクスプローラー**で、 **[データベース]** を右クリックし、 **[アタッチ]** をクリックします。

    ![SSMS のアタッチ](preparing-databases/_static/image15.png)
2. **[データベースのアタッチ]** ダイアログボックスで **[追加]** をクリックし、 *App\_Data*フォルダー内の*aspnet-ContosoUniversity-Prod*ファイルに移動します。

     ![SSMS アタッチする .mdf ファイルを追加する](preparing-databases/_static/image16.png)
3. **[OK]** をクリックします。
4. 前に使用したのと同じ手順に従って、実稼働ファイル用のスクリプトを作成します。 スクリプトファイルに*aspnet-data-prod*という名前を指定します。

## <a name="summary"></a>要約

これで、両方のデータベースを配置する準備ができました。ソリューションフォルダーには、2つのデータ配置スクリプトが用意されています。

![データ配置スクリプト](preparing-databases/_static/image17.png)

次のチュートリアルでは、配置に影響を与えるプロジェクト設定を構成し、配置されたアプリケーションで異なる必要がある設定に対して、自動 web.config ファイル変換を設定*します。*

## <a name="more-information"></a>その他の情報

NuGet の詳細については、「NuGet と Nuget の[ドキュメント](http://docs.nuget.org/docs/start-here/overview)[を使用したプロジェクトライブラリの管理](https://msdn.microsoft.com/magazine/hh547106.aspx)」を参照してください。 NuGet を使用しない場合は、NuGet パッケージを分析してインストールしたときの動作を確認する方法について学習する必要があります。 (たとえば、web.config 変換を構成したり、PowerShell スクリプトをビルド時に実行するように構成し*たりすること*があります)。NuGet のしくみの詳細については、「パッケージと構成ファイル[の作成と発行](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)」[および「ソースコード変換](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)」を参照してください。

> [!div class="step-by-step"]
> [前へ](introduction.md)
> [次へ](web-config-transformations.md)
