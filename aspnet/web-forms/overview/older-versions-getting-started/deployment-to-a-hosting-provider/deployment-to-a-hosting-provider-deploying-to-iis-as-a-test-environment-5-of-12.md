---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションの配置: テスト環境としての IIS への配置-5/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515680"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションの配置: テスト環境としての IIS への配置-5/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、ASP.NET web アプリケーションをローカルコンピューター上の IIS に配置する方法について説明します。

アプリケーションを開発する場合は、通常、Visual Studio で実行することでテストします。 既定では、これは Visual Studio 開発サーバー (Cassini とも呼ばれます) を使用していることを意味します。 Visual Studio 開発サーバーを使用すると、Visual Studio での開発時のテストが簡単になりますが、IIS とまったく同じようには機能しません。 その結果、Visual Studio でアプリケーションをテストするときに、アプリケーションが正常に実行されることはありますが、ホスト環境の IIS に配置すると失敗します。

次の方法で、アプリケーションをより確実にテストできます。

1. 開発中に Visual Studio でテストする場合は、Visual Studio 開発サーバーではなく IIS Express または完全な IIS を使用します。 通常、この方法では、IIS でのサイトの実行方法がより正確にエミュレートされます。 ただし、この方法では、配置プロセスをテストしたり、配置プロセスの結果が正常に実行されることを検証したりすることはありません。
2. 後で運用環境に配置する場合と同じプロセスを使用して、開発用コンピューター上の IIS にアプリケーションを配置します。 このメソッドは、IIS でアプリケーションが正しく実行されることを検証するだけでなく、デプロイプロセスを検証します。
3. 実稼働環境にできるだけ近いテスト環境にアプリケーションをデプロイします。 これらのチュートリアルの運用環境はサードパーティのホスティングプロバイダーなので、最適なテスト環境は、ホスティングプロバイダーによる2番目のアカウントになります。 この2番目のアカウントはテストにのみ使用しますが、運用アカウントと同じ方法で設定します。

このチュートリアルでは、オプション2の手順について説明します。 オプション3に関するガイダンスは、「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルの最後に記載されています。このチュートリアルの最後には、オプション1のリソースへのリンクがあります。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="configuring-the-application-to-run-in-medium-trust"></a>中程度の信頼で実行されるようにアプリケーションを構成する

IIS をインストールして配置する前に、通常の共有ホスティング環境と同様に、サイトを実行するように web.config ファイルの設定を変更します。

通常、ホスティングプロバイダーは、web サイトを*中程度の信頼*で実行します。これは、許可されていないものがあることを意味します。 たとえば、アプリケーションコードは Windows レジストリにアクセスできず、アプリケーションのフォルダー階層の外部にあるファイルの読み取りや書き込みもできません。 既定では、アプリケーションはローカルコンピューター上で*高い信頼*で実行されます。つまり、アプリケーションは、運用環境に配置するときに失敗する可能性がある処理を実行できます。 したがって、テスト環境に実稼働環境をより正確に反映させるには、アプリケーションを中程度の信頼で実行するように構成します。

アプリケーションの Web.config ファイルで、次の例に示すように、 **system.web 要素に** **trust**要素を追加します。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

これで、アプリケーションはローカルコンピューター上でも IIS の中程度の信頼で実行されるようになります。 この設定を使用すると、アプリケーションコードによって、運用環境でエラーが発生する可能性のある処理をできるだけ早くキャッチできます。

> [!NOTE]
> Entity Framework Code First Migrations を使用している場合は、バージョン5.0 以降がインストールされていることを確認してください。 Entity Framework バージョン4.3 では、データベーススキーマを更新するために、移行には完全な信頼が必要です。

## <a name="installing-iis-and-web-deploy"></a>IIS と Web 配置のインストール

開発用コンピューターに IIS を配置するには、IIS と Web 配置がインストールされている必要があります。 これらは、既定の Windows 7 構成には含まれていません。 IIS と Web 配置の両方を既にインストールしている場合は、次のセクションに進んでください。

Web platform Installer は iis 用に推奨される構成をインストールし、必要に応じて iis および Web 配置の前提条件を自動的にインストールするため、IIS と Web 配置をインストールするには、 [Web Platform installer](https://www.microsoft.com/web/downloads/platform.aspx)を使用することをお勧めします。

Web Platform Installer を実行して IIS と Web 配置をインストールするには、次のリンクを使用します。 IIS、Web 配置、または必要なコンポーネントのいずれかが既にインストールされている場合は、不足しているものだけが Web Platform Installer によってインストールされます。

- [WebPI を使用した IIS と Web 配置のインストール](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>既定のアプリケーションプールを .NET 4 に設定する

IIS をインストールした後、 **Iis マネージャー**を実行して、.NET Framework バージョン4が既定のアプリケーションプールに割り当てられていることを確認します。

Windows の **[スタート]** メニューから、 **[実行]** を選択し、「inetmgr.exe」と入力して、 **[OK]** をクリックします。 ( **[実行]** コマンドが **[スタート]** メニューにない場合は、Windows キーと R キーを押して開くことができます。 または、タスクバーを右クリックし、 **[プロパティ]** をクリックします。 [**スタート] メニュー**を選択し、 **[カスタマイズ]** をクリックして、 **[コマンドの実行]** を選択します。

**[接続]** ウィンドウで、サーバーノードを展開し、 **[アプリケーションプール]** を選択します。 次の図に示すように、 **[アプリケーションプール]** ウィンドウで、 **DefaultAppPool**が .net framework version 4 に割り当てられている場合は、次のセクションに進みます。

[![Inetmgr_showing_4。0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

アプリケーションプールが2つだけ表示され、その両方が .NET Framework 2.0 に設定されている場合は、IIS で ASP.NET 4 をインストールする必要があります。

- Windows の **[スタート]** メニューの **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックして、コマンドプロンプトウィンドウを開きます。 次に、次のコマンドを使用して、 [aspnet\_iis 登録ツール](https://msdn.microsoft.com/library/k6h9cz8h.aspx)を実行し、IIS に ASP.NET 4 をインストールします。 (64 ビットシステムでは、"Framework" を "Framework64" に置き換えます)。

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP。 NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    このコマンドは .NET Framework 4 の新しいアプリケーションプールを作成しますが、既定のアプリケーションプールは2.0 に設定されたままになります。 .NET 4 を対象とするアプリケーションをそのアプリケーションプールに配置するため、アプリケーションプールを .NET 4 に変更する必要があります。

**IIS マネージャー**を閉じた場合は、もう一度実行し、サーバーノードを展開して **[アプリケーションプール]** をクリックすると、 **[アプリケーションプール]** ウィンドウが再び表示されます。

**[アプリケーションプール]** ウィンドウで、 **[DefaultAppPool**] をクリックし、 **[操作]** ウィンドウで **[基本設定]** をクリックします。

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

**[アプリケーションプールの編集]** ダイアログボックスで **.NET Framework バージョン**を **.NET Framework v v4.0.30319**に変更し、[ **OK]** をクリックします。

[![Selecting_。 NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

これで、IIS に発行する準備ができました。

## <a name="publishing-to-iis"></a>IIS への発行

Visual Studio 2010 と Web 配置を使用してデプロイできる方法はいくつかあります。

- Visual Studio のワンクリック発行を使用します。
- *展開パッケージ*を作成し、IIS マネージャーの UI を使用してインストールします。 展開パッケージは、IIS にサイトをインストールするために必要なすべてのファイルとメタデータを含む *.zip*ファイルで構成されます。
- 展開パッケージを作成し、コマンドラインを使用してインストールします。

デプロイタスクを自動化するように Visual Studio を設定するために、前のチュートリアルで実行したプロセスは、これら3つの方法すべてに適用されます。 これらのチュートリアルでは、これらのメソッドの1つ目を使用します。 配置パッケージの使用方法の詳細については、「 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx)」を参照してください。

発行する前に、管理者モードで Visual Studio を実行していることを確認してください。 (Windows 7 の **[スタート]** メニューで、使用している Visual Studio のバージョンのアイコンを右クリックし、 **[管理者として実行]** を選択します)。ローカルコンピューター上の IIS に発行する場合にのみ、発行に管理者モードが必要です。

**ソリューションエクスプローラー**で、(ContosoUniversity プロジェクトではなく) ContosoUniversity プロジェクトを右クリックし、 **[発行]** を選択します。

**Web の発行** ウィザードが表示されます。

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

ドロップダウンリストで、[ **&lt;新しい...&gt;** ] を選択します。

**[新しいプロファイル]** ダイアログボックスで、「Test」と入力し、 **[OK]** をクリックします。

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

この名前は、前に作成した web.config 変換ファイルの中間ノードと同じです。 この対応により、このプロファイルを使用して発行するときに web.config 変換が適用されます。

ウィザードは自動的に **[接続]** タブに進みます。

**[サービス URL]** ボックスに、「 *localhost*」と入力します。

**[サイト/アプリケーション]** ボックスに、「 *Default Web Site/ContosoUniversity」と*入力します。

**[宛先 URL]** ボックスに、「`http://localhost/ContosoUniversity`」と入力します。

**送信先 URL**の設定は必須ではありません。 Visual Studio がアプリケーションの配置を完了すると、既定のブラウザーが自動的にこの URL に表示されます。 配置後にブラウザーが自動的に開かないようにする場合は、このボックスを空白のままにします。

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

**[接続の検証]** をクリックして設定が正しいことを確認し、ローカルコンピューターの IIS に接続できることを確認します。

緑色のチェックマークは、接続が成功したことを確認します。

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

**[次]** へ をクリックして、 **[設定]** タブに進みます。

**[構成]** ボックスの一覧で、配置するビルド構成を指定します。 既定値は Release です。これが必要です。

[**ターゲットで追加ファイルを削除**する] チェックボックスをオフのままにします。 これは最初の配置であるため、コピー先のフォルダーにはまだファイルがありません。

**[データベース]** セクションで、 **schoolcontext.cs**の [接続文字列] ボックスに次の値を入力します。

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

配置プロセスでは、この接続文字列が配置された Web.config ファイルに配置されます。これは、**実行時にこの接続文字列を使用する (実行時にこの接続文字列を使用する**)。

また、 **[schoolcontext.cs]** の下の **[Code First Migrations の適用]** を選択します。 このオプションを選択すると、配置プロセスによって、配置された Web.config ファイルが `MigrateDatabaseToLatestVersion` 初期化子を指定するように構成されます。 この初期化子は、配置後にアプリケーションが初めてデータベースにアクセスしたときに、データベースを最新バージョンに自動的に更新します。

**Defaultconnection**の [接続文字列] ボックスに、次の値を入力します。

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

**更新データベース**をクリアしたままにします。 メンバーシップデータベースは、アプリ\_データ内の .sdf ファイルをコピーすることによってデプロイされます。このデータベースでは、配置プロセスで他の操作を実行しないようにします。

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

**[次]** へ をクリックして、 **[プレビュー]** タブに進みます。

**[プレビュー]** タブで、 **[プレビューの開始]** をクリックして、コピーされるファイルの一覧を表示します。

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

**[発行]** をクリックします。

Visual Studio が管理者モードでない場合は、アクセス許可のエラーを示すエラーメッセージが表示されることがあります。 その場合は、Visual Studio を閉じて、管理者モードで開き、もう一度発行してみてください。

Visual Studio が管理者モードの場合、 **[出力]** ウィンドウは成功したビルドと発行を報告します。

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

ブラウザーが自動的に開き、ローカルコンピューターの IIS で実行されている Contoso 大学のホームページが表示されます。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>テスト環境でのテスト

環境インジケーターには、"(Dev)" ではなく "(Test)" と表示されます。これは、環境インジケーターの*web.config 変換が*成功したことを示しています。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

**[Students]** ページを実行して、デプロイされたデータベースに学生がいないことを確認します。 このページを選択すると、Code First によってデータベースが作成され、`Seed` メソッドが実行されるため、読み込みに数分かかる場合があります。 (これは、アプリケーションがデータベースにアクセスしようとしていないためにホームページを使用していた場合には行われませんでした)。

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

**インストラクターページを**実行して、Code First がインストラクターのデータでデータベースをシード処理したことを確認します。

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

**学生メニューから** **[学生の追加]** を選択し、学生を追加します。次に、 **[学生]** ページで新しい学生を表示して、データベースへの書き込みが正常に完了したことを確認します。

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

**[コース]** メニューの **[クレジットの更新]** を選択します。 **[更新プログラムのクレジット]** ページには管理者権限が必要であるため、 **[ログイン]** ページが表示されます。 前の手順で作成した管理者アカウントの資格情報を入力します ("admin" と "Pas $ w0rd")。 **[更新プログラムのクレジット]** ページが表示され、前のチュートリアルで作成した管理者アカウントがテスト環境に正しく配置されていることを確認します。

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

プレースホルダーファイルのみを含む*Elmah*フォルダーが存在することを確認します。

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First Migrations の web.config の自動変更の確認

デプロイされたアプリケーションの*web.config*ファイルを*C:\inetpub\wwwroot\ContosoUniversity*で開き、データベースを最新バージョンに自動的に更新するように配置プロセスが構成さ Code First Migrations れている場所を確認できます。

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

また、配置プロセスでは、データベーススキーマを更新するために排他的に使用する Code First Migrations 用の新しい接続文字列も作成しました。

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

この追加の接続文字列を使用すると、データベーススキーマの更新用に1つのユーザーアカウントを指定し、アプリケーションデータアクセスに別のユーザーアカウントを指定することができます。 たとえば、db\_所有者ロールを Code First Migrations に割り当て、db\_datareader および db\_datawriter ロールをアプリケーションに割り当てることができます。 これは、アプリケーション内の悪意のある可能性のあるコードによってデータベーススキーマが変更されないようにする、一般的な多層防御パターンです。 (たとえば、SQL インジェクション攻撃が成功した場合に発生する可能性があります)。このパターンは、これらのチュートリアルでは使用されません。 SQL Server Compact には適用されません。このシリーズの後のチュートリアルで SQL Server に移行するときには適用されません。 Cytanium サイトには、Cytanium で作成した SQL Server データベースにアクセスするためのユーザーアカウントが1つだけ用意されています。 シナリオでこのパターンを実装できる場合は、次の手順を実行します。

1. **Web の発行**ウィザードの **[設定]** タブで、完全なデータベーススキーマ更新権限を持つユーザーを指定する接続文字列を入力し、 **[実行時にこの接続文字列を使用]** する チェックボックスをオフにします。 配置された Web.config ファイルで、これが `DatabasePublish` 接続文字列になります。
2. アプリケーションで実行時に使用する接続文字列の Web.config ファイル変換を作成します。

これで、開発用コンピューター上の IIS にアプリケーションを配置し、そこでテストしました。 これにより、展開プロセスによって、アプリケーションのコンテンツが適切な場所にコピーされているかどうかが確認されます (展開する必要のないファイルは除外されます)。また、展開時に IIS が正しく構成された Web 配置ます。 次のチュートリアルでは、まだ完了していない配置タスクを検索するテストをもう1つ実行します。これは、 *Elmah*フォルダーのフォルダーアクセス許可の設定です。

## <a name="more-information"></a>詳細情報

Visual Studio で IIS または IIS Express を実行する方法の詳細については、次のリソースを参照してください。

- IIS.net サイトの[IIS Express の概要](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)。
- Scott Guthrie のブログで[IIS Express を紹介](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx)します。
- [方法: Visual Studio で Web プロジェクトの Web サーバーを指定する](https://msdn.microsoft.com/library/ms178108.aspx)
- [IIS と](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)ASP.NET サイトの ASP.NET 開発サーバーの主な相違点。
- Rick Anderson のブログで[、ASP.NET MVC または Web フォームアプリケーションを IIS 7 で30秒以内にテスト](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx)します。 このエントリでは、Visual Studio 開発サーバー (Cassini) を使用したテストが IIS Express でのテストほど信頼性の低いものではなく、IIS Express でのテストが IIS でのテストほど信頼性がない理由の例を示します。

アプリケーションが中程度の信頼で実行されている場合に発生する可能性がある問題の詳細については、「Rolla サイトからの4人の[信頼での ASP.NET アプリケーションのホスティング](http://www.4guysfromrolla.com/articles/100307-1.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [次へ](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
