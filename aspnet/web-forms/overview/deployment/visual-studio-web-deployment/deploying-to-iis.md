---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 'Visual Studio を使用した ASP.NET Web デプロイ: テストへの配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520372"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>Visual Studio を使用した ASP.NET Web 配置: テストへの配置

[Tom Dykstra](https://github.com/tdykstra)

このチュートリアルシリーズでは、Visual Studio 2017 を使用して Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service するために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

現在のバージョンの Azure へのデプロイについては、「 [azure で ASP.NET Core web アプリを作成](/azure/app-service/app-service-web-get-started-dotnet)する」を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、ローカルコンピューター上のインターネットインフォメーションサーバー (IIS) に ASP.NET web アプリケーションを展開します。

一般に、アプリケーションを開発する場合は、Visual Studio で実行してテストします。 既定では、Visual Studio 2017 の web アプリケーションプロジェクトでは、開発用 web サーバーとして IIS Express が使用されます。 IIS Express は、Visual Studio 2017 が既定で使用する Visual Studio 開発サーバー (Cassini とも呼ばれます) よりも完全な IIS と同様に動作します。 ただし、開発 web サーバーは IIS とまったく同じように動作しません。 その結果、Visual Studio でアプリを正常に実行してテストすることはできますが、IIS に配置すると失敗します。

アプリケーションを確実にテストするには、次の2つの方法があります。

1. 後で運用環境に配置する場合と同じプロセスを使用して、開発用コンピューター上の IIS にアプリケーションを配置します。

   Web プロジェクトを実行するときに IIS を使用するように Visual Studio を構成できますが、それでも配置プロセスはテストされません。 このメソッドは、デプロイプロセスを検証し、IIS でアプリケーションが正しく実行されることを確認します。

2. 実稼働環境と同様に、アプリケーションをテスト環境にデプロイします。 
 
   これらのチュートリアルの運用環境は、Azure App Service で Web Apps ます。 理想的なテスト環境は、Azure サービスで作成された追加の web アプリです。 運用 web アプリと同じように設定されますが、テストにのみ使用します。

オプション2は、テスト方法として最も信頼性の高い方法です。 オプション2を使用する場合、必ずしもオプション1を使用する必要はありません。 ただし、サードパーティのホスティングプロバイダーにデプロイする場合は、オプション2が実現できないか、コストがかかる可能性があります。そのため、このチュートリアルシリーズでは両方の方法を紹介します。 オプション2のガイダンスについては、「[運用環境へのデプロイ](deploying-to-production.md)」チュートリアルをご覧ください。

Visual Studio で web サーバーを使用する方法の詳細については、「 [Visual studio の Web サーバー」を](https://msdn.microsoft.com/library/58wxa9w5.aspx)参照してください。 ASP.NET web プロジェクトを参照してください。

リマインダー: チュートリアルを実行するときにエラーメッセージが表示されたり、機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="download-the-contoso-university-starter-project"></a>Contoso 大学 starter プロジェクトをダウンロードする

Contoso 大学の Visual Studio starter ソリューションとプロジェクトをダウンロードしてインストールします。 このソリューションには、完成したチュートリアルが含まれています。 

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>IIS のインストール

開発用コンピューター上の IIS に配置するには、IIS と Web 配置がインストールされていることを確認します。 既定では、Visual Studio は Web 配置をインストールしますが、IIS は既定の Windows 10、Windows 8、または Windows 7 の構成には含まれていません。 既に IIS をインストールしており、既定のアプリケーションプールが既に .NET 4 に設定されている場合は、[次のセクション](#sqlexpress)に進みます。

1. IIS と Web 配置をインストールするには、 [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx)を使用することをお勧めします。 WPI は、IIS を含む推奨される IIS 構成をインストールし、必要に応じて前提条件を Web 配置します。

   IIS、Web 配置、または必要なコンポーネントのいずれかが既にインストールされている場合は、不足しているものだけが WPI によってインストールされます。

   * Web Platform Installer を使用して、IIS と Web 配置をインストールします。
    
     ![WPI を使用して IIS をインストールする](deploying-to-iis/_static/image30.png)

     ![WPI を使用して Web 配置をインストールする](deploying-to-iis/_static/image31.png)

     IIS 7 がインストールされることを示すメッセージが表示されます。 このリンクは、Windows 8 の IIS 8 で機能します。ただし、Windows 8 以降では、次の手順を実行して、ASP.NET 4.7 がインストールされていることを確認してください。

   * [**コントロールパネル]** を開き、[プログラムと機能]**の [Windows の機能の有効化または無効化**] ** >  > ** の [プログラム**と機能** > ] を開きます。

   * **インターネットインフォメーションサービス**、 **World Wide Web Services**、**アプリケーション開発機能**を展開します。
   
   * **ASP.NET 4.7**が選択されていることを確認します。

     ![ASP.NET 4.7 を選択します](deploying-to-iis/_static/image1a.png)

   * **World Wide Web サービス**と**IIS 管理コンソール**が選択されていることを確認します。 IIS と IIS マネージャーがインストールされます。
    
     ![World Wide Web サービスの選択](deploying-to-iis/_static/image24.png)    
  
   * **[OK]** を選択します。 インストールが行われていることを示すダイアログボックスメッセージが表示されます。

IIS をインストールした後、 **Iis マネージャー**を実行して、.NET Framework バージョン4が既定のアプリケーションプールに割り当てられていることを確認します。

1. WINDOWS + R キーを押して、[ファイルの**実行**] ダイアログボックスを開きます。

   (Windows 8 以降では、**スタート**ページで「run」と入力します。 Windows 7 では、 **[スタート]** メニューから **[実行]** を選択します。 **[実行]** が **[スタート]** メニューにない場合は、タスクバーを右クリックし、 **[プロパティ]** を選択します。 [**スタート] メニュー**を選択し、 **[カスタマイズ]** をクリックして、 **[コマンドの実行]** を選択します。

2. 「Inetmgr.exe」と入力し、[ **OK]** を選択します。

3. **[接続]** ウィンドウで、サーバーノードを展開し、 **[アプリケーションプール]** を選択します。 次の図に示すように、 **[アプリケーションプール]** ウィンドウで、 **DefaultAppPool**が .net framework version 4 に割り当てられている場合は、次のセクションに進みます。

   ![Inetmgr_showing_4。0_app_pools](deploying-to-iis/_static/image5a.png)

4. 2つのアプリケーションプールのみが表示され、両方が .NET Framework 2.0 に設定されている場合は、IIS に ASP.NET 4 をインストールします。

   Windows 8 以降の場合は、前のセクションの手順「ASP.NET 4.7 がインストールされていることを確認するには」を参照してください。または、「 [windows 8 および Windows Server 2012 に ASP.NET 4.5 をインストールする方法](https://support.microsoft.com/kb/2736284)」を参照してください。 Windows 7 の場合は、Windows の **[スタート]** メニューの **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックして、コマンドプロンプトウィンドウを開きます。 次のコマンドを使用して、 [aspnet\_iis 登録ツール](https://msdn.microsoft.com/library/k6h9cz8h.aspx)を実行し、IIS に ASP.NET 4 をインストールします。 (32 ビットシステムでは、"Framework64" を "Framework" に置き換えます)。

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   このコマンドは .NET Framework 4 の新しいアプリケーションプールを作成しますが、既定のアプリケーションプールは2.0 に設定されたままになります。 .NET 4 を対象とするアプリケーションをそのアプリケーションプールに配置しているため、アプリケーションプールを .NET 4 に変更します。

5. **IIS マネージャー**を閉じた場合は、もう一度実行し、サーバーノードを展開して、 **[アプリケーションプール]** を選択します。

6. **[アプリケーションプール]** ウィンドウで、 **[DefaultAppPool]** を選択します。 **[操作]** ウィンドウで、 **[基本設定]** を選択します。

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. **[アプリケーションプールの編集]** ダイアログボックスで、 **.net clr バージョン**を **.net clr v v4.0.30319**に変更します。 **[OK]** を選択します。

   ![Selecting_。 NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

これで、IIS に web アプリケーションを発行する準備ができました。 ただし、まず、テスト用のデータベースを作成します。

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>SQL Server Express をインストールする

LocalDB は IIS で動作するように設計されていないため、テスト環境には SQL Server Express がインストールされている必要があります。 SQL Server Express Visual Studio 2010 を使用している場合は、既定でインストールされています。 Visual Studio 2012 以降を使用している場合は、SQL Server Express をインストールします。

SQL Server Express をインストールするには、[ダウンロードセンター (Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)) からダウンロードしてインストールします。 

SQL Server インストールセンターの最初のページで、**新規 SQL Server スタンドアロンインストールを実行するか、既存のインストールに機能を追加**して、既定の選択肢を受け入れる指示に従います。 インストールウィザードで、既定の設定をそのまま使用します。 インストールオプションの詳細については、「インストール[ウィザードからの SQL Server のインストール (セットアップ)](https://msdn.microsoft.com/library/ms143219.aspx)」を参照してください。

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>テスト環境用の SQL Server Express データベースを作成する

Contoso 大学のアプリケーションには、次の2つのデータベースがあります。 

1. メンバーシップデータベース 
2. アプリケーションデータベース 

これらのデータベースは、2つの異なるデータベースまたは1つのデータベースに配置できます。 これらを組み合わせると、データベースの結合が簡単になります。 

サードパーティのホスティングプロバイダーにデプロイする場合は、ホスティングプランによって、それらを結合する理由が提供されることもあります。 たとえば、プロバイダーは複数のデータベースに対してより多くの料金を請求する場合や、複数のデータベースを許可しない場合があります。

このチュートリアルでは、テスト環境の2つのデータベースと、ステージング環境と運用環境の1つのデータベースに配置します。

Visual Studio の **表示** メニューで、**サーバーエクスプローラー** (visual Web Developer では**データベースエクスプローラー** ) を選択します。 **[データ接続]** を右クリックし、 **[新しい SQL Server データベースの作成]** を選択します。

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

**[新しい SQL Server データベースの作成]** ダイアログボックスで、 **[サーバー名]** ボックスに「.\SQLExpress」と入力し、 **[新しいデータベース名]** ボックスに「ContosoUniversity」と入力します。 **[OK]** を選択します。

![Aspnet の作成-ContosoUniversity](deploying-to-iis/_static/image9.png)

同じ手順に従って、`ContosoUniversity`という名前の新しい SQL Server Express School データベースを作成します。

**サーバーエクスプローラー**には、2つの新しいデータベースが表示されます。

![サーバーエクスプローラーの新しいデータベース](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>新しいデータベースの grant スクリプトを作成する

開発用コンピューターの IIS でアプリケーションを実行すると、アプリケーションは既定のアプリケーションプールの資格情報を使用してデータベースにアクセスします。 ただし、既定では、アプリケーションプールには、データベースを開くためのアクセス許可がありません。 これは、そのアクセス許可を付与するスクリプトを実行する必要があることを意味します。 このセクションでは、そのスクリプトを作成し、後で実行して、アプリケーションが IIS で実行されているときにデータベースを開けるようにします。

テキストエディターで、次の SQL コマンドを新しいファイルにコピーし、 *Grant .sql*として保存します。 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

Visual Studio で、Contoso 大学ソリューションを開きます。 (プロジェクトのいずれかではなく) ソリューションを右クリックし、 **[追加]** を選択します。 **[既存の項目]** を選択し、を参照して *.sql*を指定し、それを開きます。

> [!NOTE]
> このスクリプトは、このチュートリアルで指定されているように、Windows 10、Windows 8、または Windows 7 の IIS 設定を使用して、SQL Server Express 2012 以降とで動作するように設計されています。 異なるバージョンの SQL Server または Windows を使用している場合、またはコンピューターに IIS を別の方法でセットアップする場合は、このスクリプトの変更が必要になることがあります。 SQL Server スクリプトの詳細については、「 [SQL Server オンラインブック](https://go.microsoft.com/fwlink/?LinkId=132511)」を参照してください。

> [!NOTE] 
> **セキュリティ**に関する注意このスクリプトは、実行時にデータベースにアクセスするユーザーに `db_owner` アクセス許可を付与します。これは、運用環境で使用するものです。 場合によっては、完全なデータベーススキーマ更新権限を持つユーザーを配置に対してのみ指定し、データの読み取りと書き込みのみを行う権限を持つ別のユーザーを実行時に指定することができます。 詳細については、このチュートリアルで後述する「 [Code First Migrations に対する web.config の自動変更のレビュー](#reviewingmigrations) 」を参照してください。

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>アプリケーションデータベースで grant スクリプトを実行する

データベースの配置で[Dbdacfx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)プロバイダーが使用されるため、配置時にメンバーシップデータベースで許可スクリプトを実行するように発行プロファイルを構成することができます。 Code First Migrations の配置中にスクリプトを実行することはできません。これは、アプリケーションデータベースを配置する方法です。 これは、アプリケーションデータベースに配置する前に、スクリプトを手動で実行する必要があることを意味します。

1. Visual Studio で、前の手順で作成した*Grant .sql*ファイルを開きます。

2. **[接続]** を選択します。 

    ![[接続] ボタン](deploying-to-iis/_static/image11.png)

3. **[サーバーへの接続]** ダイアログボックスで、**サーバー名**として「 *.\SQLExpress* 」と入力します。 **[接続]** を選択します。

4. データベース ボックスの一覧で  **ContosoUniversity** を選択します。 **[実行]** を選択します。 

   ![](deploying-to-iis/_static/image12.png)

アプリケーションの実行時にデータベーステーブルを作成するための Code First Migrations のために、既定のアプリケーションプール id には、アプリケーションデータベースに対する十分なアクセス許可が与えられます。

## <a name="publish-to-iis"></a>IIS に公開する

Visual Studio と Web 配置を使用して IIS に配置できる方法はいくつかあります。

* Visual Studio のワンクリック発行を使用します。
* コマンドラインから発行します。
* 展開パッケージを作成し、IIS マネージャーを使用してインストールします。 パッケージには、IIS にサイトをインストールするために必要なすべてのファイルとメタデータを含む .zip ファイルがあります。
* 展開パッケージを作成し、コマンドラインを使用してインストールします。

デプロイタスクを自動化するように Visual Studio を設定する前のチュートリアルで実行したプロセスは、これらのすべての方法に適用されます。 これらのチュートリアルでは、最初の2つの方法を使用します。 配置パッケージの使用方法の詳細については、「web[配置パッケージを作成およびインストール](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)する」を参照してください。

発行する前に、管理者モードで Visual Studio を実行していることを確認してください。 タイトルバーに **(管理者)** が表示されない場合は、Visual Studio を閉じます。 Windows 8 (またはそれ以降) の**スタート**ページまたは windows 7 の **[スタート]** メニューで、Visual Studio アイコンを右クリックし、 **[管理者として実行]** を選択します。 ローカルコンピューター上の IIS に発行する場合、管理者モードは発行にのみ必要です。

### <a name="create-the-publish-profile"></a>発行プロファイルを作成する

1. **ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクト ( **ContosoUniversity**プロジェクトではありません) を右クリックします。 **[発行]** を選択します。 **[発行]** ページが表示されます。

2. **[新しいプロファイル]** を選択します。 **[発行先の選択]** ダイアログボックスが表示されます。

3. **[IIS、FTP など]** を選択します。 **[プロファイルの作成]** を選択します。 **発行**ウィザードが表示されます。

   ![Web の発行ウィザードの [プロファイル] タブ](deploying-to-iis/_static/image26.png)

4. **[発行方法]** ドロップダウンメニューから、 **[Web 配置]** を選択します。

5. **[サーバー]** に「 *localhost*」と入力します。

6. **[サイト名]** に「 *Default Web Site/ContosoUniversity」と*入力します。

7. **[宛先 URL]** に「 *http://localhost/ContosoUniversity* 」と入力します。

   **送信先 URL**の設定は必須ではありません。 Visual Studio がアプリケーションの配置を完了すると、既定のブラウザーが自動的にこの URL に表示されます。 配置後にブラウザーが自動的に開かないようにする場合は、このボックスを空白のままにします。

8. **[接続の検証]** を選択して、設定が正しいことを確認し、ローカルコンピューターの IIS に接続できることを確認します。

   緑色のチェックマークは、接続が成功したことを確認します。

   ![Web の発行ウィザードの [接続] タブ](deploying-to-iis/_static/image27.png)

9. **[次]** へ を選択して、 **[設定]** タブに進みます。

10. **[構成]** ボックスの一覧で、配置するビルド構成を指定します。 **リリース**の既定値に設定したままにします。 このチュートリアルでは、デバッグビルドを配置しません。

11. [**ファイルの発行オプション]** を展開します。 **アプリ\_データフォルダーから ファイルを除外する** を選択します。

    テスト環境では、アプリケーションは、 *App\_Data*フォルダー内の .mdf ファイルではなく、ローカル SQL Server Express インスタンスで作成したデータベースにアクセスします。

12. [**発行時にプリコンパイル**を解除し、**ターゲットで追加ファイルを削除**する] チェックボックスをオフにします。

    ![[設定] タブのファイル発行オプション](deploying-to-iis/_static/image15a.png)

    プリコンパイルは、主に大規模なサイトに便利なオプションです。 サイトが発行された後にページが初めて要求されたときに、起動時間を短縮することができます。

    追加のファイルを削除する必要はありません。これは最初の展開なので、コピー先のフォルダーにファイルがまだ存在しないためです。

    > [!NOTE] 
    > 同じサイトへの後続の配置のために [**転送先で追加のファイルを削除**する] を選択した場合は、展開する前にどのファイルが削除されるかを事前に確認できるように、プレビュー機能を使用してください。 期待される動作は、Web 配置が、プロジェクトで削除された移行先サーバー上のファイルを削除することです。 ただし、コピー元とコピー先のフォルダーの下のフォルダー構造全体が比較されます。また、場合によっては、削除したくないファイルが削除される Web 配置があります。
    > 
    > たとえば、ルートフォルダーにプロジェクトを配置するときに、サーバーのサブフォルダーに web アプリケーションがある場合、サブフォルダーは削除されます。 Contoso.com のメインサイト用に1つのプロジェクトがあり、contoso.com/blog にブログ用の別のプロジェクトがあるとします。 ブログアプリケーションはサブフォルダーにあります。 メインサイトの展開時に [**ターゲットで追加ファイルを削除**する] を選択すると、ブログアプリケーションが削除されます。
    > 
    > 別の例では、アプリ\_データフォルダーが予期せず削除される可能性があります。 SQL Server Compact などの一部のデータベースでは、アプリケーション\_データフォルダーにデータベースファイルが格納されます。 最初の配置の後、以降の配置ではデータベースファイルをコピーしないようにするため、[パッケージ/発行 Web] タブの [**アプリ\_データを除外**する] を選択します。その後、[**ターゲットで追加ファイルを削除**する] を選択した場合、データベースファイルとアプリ\_データフォルダー自体は、次回の発行時に削除されます。

### <a name="configure-deployment-for-the-membership-database"></a>メンバーシップデータベースの配置を構成する

次の手順は、ダイアログボックスの **[データベース]** セクションの**defaultconnection**データベースに適用されます。

1. **[リモート接続文字列]** ボックスに、新しい SQL Server Express メンバーシップデータベースを指す次の接続文字列を入力します。

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   配置プロセスでは、配置された Web.config ファイルにこの接続文字列を格納します。これは、この接続文字列を**実行時に使用する**ためです。

    **サーバーエクスプローラー**から接続文字列を取得することもできます。 **サーバーエクスプローラー**で、 **[データ接続]** を展開し、 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**データベースを選択します。次に、 **[プロパティ]** ウィンドウで、**接続文字列**の値をコピーします。 この接続文字列には、`Pooling=False`削除できる追加の設定が1つあります。

2. **[データベースの更新]** を選択します。

   これにより、配置中にデータベーススキーマが転送先データベースに作成されます。 次のステップでは、実行する必要がある追加のスクリプトを指定します。1つは、既定のアプリケーションプールへのデータベースアクセスを許可するスクリプト、もう1つはデータを配置するスクリプトです。

3. **[データベースの更新の構成]** を選択します。
 
4. **[データベースの更新の構成]** ダイアログボックスで、 **[SQL スクリプトの追加]** を選択します。 先ほどソリューションフォルダーに保存した*Grant .sql*スクリプトに移動します。

5. *Aspnet-data-dev*スクリプトを追加するには、この手順を繰り返します。

   ![メンバーシップデータベースのデータベースの更新の構成](deploying-to-iis/_static/image16.png)

6. **[閉じる]** を選択します。

### <a name="configure-deployment-for-the-application-database"></a>アプリケーションデータベースの展開の構成

Visual Studio によって Entity Framework `DbContext` クラスが検出されると、[データベース **] セクションに**エントリが作成されます。このエントリには、 **[データベースの更新]** チェックボックスではなく **[Code First Migrations の実行]** チェックボックスがあります。 このチュートリアルでは、このチェックボックスを使用して Code First Migrations 展開を指定します。

場合によっては、`DbContext` データベースを使用していても、データベースを配置するために移行ではなく dbDacFx プロバイダーを使用したい場合があります。 そのような場合は、MSDN の ASP.NET Web デプロイに関する FAQ で、「[移行せずに Code First データベースをデプロイする操作方法](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)」を参照してください。

次の手順は、ダイアログボックスの **[データベース]** セクションの**schoolcontext.cs**データベースに適用されます。

1. **[リモート接続文字列]** ボックスに、新しい SQL Server Express アプリケーションデータベースを指す次の接続文字列を入力します。

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   配置プロセスでは、配置された Web.config ファイルにこの接続文字列を格納します。これは、この接続文字列を**実行時に使用する**ためです。

   また、メンバーシップデータベースの接続文字列と同じ方法で、**サーバーエクスプローラー**からアプリケーションデータベースの接続文字列を取得することもできます。

2. **[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。

   このオプションを選択すると、配置プロセスによって、配置された Web.config ファイルが `MigrateDatabaseToLatestVersion` 初期化子を指定するように構成されます。 この初期化子は、配置後にアプリケーションが初めてデータベースにアクセスしたときに、データベースを最新バージョンに自動的に更新します。

### <a name="configure-publish-profile-transforms"></a>発行プロファイルの変換を構成する

1. **[閉じる]** を選択します。 変更を保存するかどうかを確認するメッセージが表示されたら、[**はい]** を選択します。

2. **ソリューションエクスプローラー**で、 **[プロパティ]** 、 **[publishprofiles]** の順に展開します。

3. [ *Customprofile. pubxml* ] を右クリックし、名前を「 *Test pubxml*」に変更します。

4. [ *Pubxml*] を右クリックします。 **[構成の変換の追加]** を選択します。

   ![[構成変換の追加] メニュー](deploying-to-iis/_static/image17.png)

   Visual Studio は、 *web.config*変換ファイルを作成して開きます。

5. *Web.config 変換ファイル*で、開始構成タグの直後に次のコードを挿入します。

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    テスト発行プロファイルを使用すると、この変換によって環境インジケーターが "Test" に設定されます。 デプロイされたサイトでは、"Contoso 大学" H1 見出しの後に "(Test)" と表示されます。

6. ファイルを保存して閉じます。

7. *Web.config ファイルを*右クリックし、 **[プレビューの変換]** を選択して、コード化した変換によって予想される変更が生成されるようにします。

    Web.config の**プレビュー**ウィンドウには、 *web.config 変換と* *web.config 変換の*両方を適用した結果が表示されます。

### <a name="preview-the-deployment-updates"></a>デプロイの更新をプレビューする

1. Web の**発行**ウィザードをもう一度開きます (ContosoUniversity プロジェクトを右クリックし、 **[発行]** 、 **[プレビュー]** の順に選択します)。

2. **[プレビュー]** ダイアログボックスで **[プレビューの開始]** を選択すると、コピーされるファイルの一覧が表示されます。 

   ![発行のプレビュー](deploying-to-iis/_static/image29.png)

   また、[データベースの**プレビュー** ] リンクを選択して、メンバーシップデータベースで実行されるスクリプトを確認することもできます。 (Code First Migrations 配置に対して実行されるスクリプトはありません。そのため、アプリケーションデータベースをプレビューすることはできません)。

3. **[発行]** を選択します。

   Visual Studio が管理者モードでない場合は、アクセス許可のエラーメッセージが表示されることがあります。 その場合は、Visual Studio を閉じて、管理者モードで開き、もう一度発行してみてください。

   Visual Studio が管理者モードの場合、 **[出力]** ウィンドウは成功したビルドと発行を報告します。

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   発行プロファイルの **[接続]** タブの **[送信先 url]** ボックスに url を入力した場合は、コンピューターの IIS で実行されている Contoso 大学のホームページがブラウザーによって自動的に開きます。

## <a name="test-in-the-test-environment"></a>テスト環境でテストする

環境インジケーターには、"(Dev)" ではなく "(Test)" と表示されます。これは、環境インジケーターの*web.config 変換が*成功したことを示しています。

インストラクターページを実行し**て、Code First**がインストラクターのデータでデータベースをシード処理したことを確認します。 このページを選択すると、Code First によってデータベースが作成され、`Seed` メソッドが実行されるため、読み込みに数分かかる場合があります。 (これは、アプリケーションがデータベースにアクセスしようとしていないためにホームページを使用していた場合には行われませんでした)。

**[Students]** タブを選択して、デプロイされたデータベースに学生がいないことを確認します。

**学生**メニューから **[学生の追加]** を選択します。 学生を追加し、 **[Students]** ページで新しい学生を表示します。 これにより、データベースへの書き込みが正常に完了したことが確認されます。

**[コース]** メニューの **[クレジットの更新]** を選択します。 **[更新プログラムのクレジット]** ページには管理者権限が必要であるため、 **[ログイン]** ページが表示されます。 前の手順で作成した管理者アカウントの資格情報を入力します ("admin" と "devpwd")。 **[更新プログラムのクレジット]** ページが表示されます。 これにより、前のチュートリアルで作成した管理者アカウントがテスト環境に正しく配置されていることを確認します。

*C:\inetpub\wwwroot\ContosoUniversity*フォルダー内に、プレースホルダーファイルのみを含む*ELMAH*フォルダーが存在することを確認します。

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First Migrations の web.config の自動変更を確認する

デプロイされたアプリケーションの*web.config*ファイルを*C:\inetpub\wwwroot\ContosoUniversity*で開き、データベースを最新バージョンに自動的に更新するように配置プロセスが構成さ Code First Migrations れている場所を確認できます。

![](deploying-to-iis/_static/image21.png)

また、配置プロセスでは、データベーススキーマを更新するために排他的に使用する Code First Migrations 用の新しい接続文字列も作成しました。

![Database_Publish 接続文字列](deploying-to-iis/_static/image22.png)

この追加の接続文字列を使用すると、データベーススキーマの更新用に1つのユーザーアカウントを指定し、アプリケーションデータアクセスに別のユーザーアカウントを指定することができます。 たとえば、db **\_所有者**ロールを、 **db\_datawriter**ロールと共に Code First Migrations および**db\_** アプリケーションに割り当てることができます。 これは、アプリケーション内の悪意のある可能性のあるコードによってデータベーススキーマが変更されないようにする、一般的な多層防御パターンです。 (たとえば、SQL インジェクション攻撃が成功した場合に発生する可能性があります)。これらのチュートリアルでは、このパターンは使用しません。 このパターンをシナリオに実装するには、次の手順を実行します。

1. Web の**発行**ウィザードの **[設定]** タブで、完全なデータベーススキーマ更新権限を持つユーザーを指定する接続文字列を入力します。 **[実行時にこの接続文字列を使用する]** チェックボックスをオフにします。 配置された Web.config ファイルで、これが `DatabasePublish` 接続文字列になります。

2. アプリケーションで実行時に使用する接続文字列の Web.config ファイル変換を作成します。

## <a name="summary"></a>まとめ

これで、開発用コンピューター上の IIS にアプリケーションを配置し、そこでテストしました。

![テストのホームページ](deploying-to-iis/_static/image23.png)

これにより、展開プロセスによって、アプリケーションのコンテンツが適切な場所にコピーされたことが確認されます (展開する必要のないファイルは除外されます)。また、展開時に IIS が正しく構成されていることを Web 配置ます。 次のチュートリアルでは、まだ完了していない配置タスクを検索するテストをもう1つ実行します。この場合、 *Elm ah*フォルダーのフォルダーアクセス許可を設定します。

## <a name="more-information"></a>詳細情報

Visual Studio で IIS または IIS Express を実行する方法の詳細については、次のリソースを参照してください。

- IIS.net サイトの[IIS Express の概要](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)。
- Scott Guthrie のブログで[IIS Express を紹介](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx)します。
- [ASP.NET Web プロジェクトのための Visual Studio の Web サーバー](https://msdn.microsoft.com/library/58wxa9w5.aspx)。
- [IIS と](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)ASP.NET サイトの ASP.NET 開発サーバーの主な相違点。

アプリケーションが中程度の信頼で実行されている場合に発生する可能性がある問題の詳細については、Rolla サイトの4人の担当者に[おける中程度の信頼での ASP.NET アプリケーションのホスティング](http://www.4guysfromrolla.com/articles/100307-1.aspx)

> [!div class="step-by-step"]
> [前へ](project-properties.md)
> [次へ](setting-folder-permissions.md)
