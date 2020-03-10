---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: Web 配置 Publishing | のデータベースサーバーの構成Microsoft Docs
author: jrjlee
description: このトピックでは、web 配置と発行をサポートするように SQL Server 2008 R2 データベースサーバーを構成する方法について説明します。 このトピックで説明するタスクは次のとおりです。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515242"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>Web 配置発行のデータベース サーバーを構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、web 配置と発行をサポートするように SQL Server 2008 R2 データベースサーバーを構成する方法について説明します。
> 
> このトピックで説明する&#x2014;タスクは、IIS Web 配置ツール (Web 配置) リモートエージェントサービスを使用するように web サーバーが構成されているかどうか、Web 配置ハンドラー、またはオフライン配置であるか、またはアプリケーションが1つの web サーバーまたはサーバーファームで実行されているかには関係ありません。 データベースを配置する方法は、セキュリティ要件やその他の考慮事項によって変化する可能性があります。 たとえば、サンプルデータを使用して、または使用せずにデータベースを配置する場合、ユーザーロールマッピングを展開するか、展開後に手動で構成することができます。 ただし、データベースサーバーを構成する方法は変わりません。

Web 配置をサポートするようにデータベースサーバーを構成するために、追加の製品やツールをインストールする必要はありません。 データベースサーバーと web サーバーが異なるコンピューター上で実行されている場合は、次のことを行うだけで済みます。

- SQL Server に TCP/IP を使用した通信を許可します。
- ファイアウォール経由のトラフィックの SQL Server を許可します。
- Web サーバーコンピューターアカウントに SQL Server ログインを指定します。
- コンピューターアカウントのログインを必要なデータベースロールにマップします。
- デプロイを実行するアカウントに、SQL Server ログインとデータベース作成者のアクセス許可を付与します。
- 繰り返しデプロイをサポートするには、デプロイアカウントのログインを**db\_所有者**データベースロールにマップします。

このトピックでは、これらの各手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、Windows Server 2008 R2 で実行されている SQL Server 2008 R2 の既定のインスタンスを使用して作業を開始していることを前提としています。 続行する前に、次のことを確認してください。

- Windows Server 2008 R2 Service Pack 1 および利用可能なすべての更新プログラムがインストールされています。
- サーバーはドメインに参加しています。
- サーバーには静的 IP アドレスがあります。
- SQL Server 2008 R2 Service Pack 1 および利用可能なすべての更新プログラムがインストールされていること。

SQL Server インスタンスには、**データベースエンジンサービス**の役割のみを含める必要があります。これは、任意の SQL Server インストールに自動的に含まれます。 ただし、構成とメンテナンスを容易にするために、[**管理ツール-基本]** と [**管理ツール-完全]** のサーバーロールを含めることをお勧めします。

> [!NOTE]
> コンピューターをドメインに参加させる方法の詳細については、「[コンピューターをドメインに参加](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)させ、ログオンする」を参照してください。 静的 IP アドレスの構成の詳細については、「[静的 Ip アドレスの構成](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)」を参照してください。 SQL Server のインストールの詳細については、「 [SQL Server 2008 R2 のインストール](https://technet.microsoft.com/library/bb500395.aspx)」を参照してください。

## <a name="enable-remote-access-to-sql-server"></a>SQL Server へのリモートアクセスを有効にする

SQL Server は、TCP/IP を使用してリモートコンピューターと通信します。 データベースサーバーと web サーバーが異なるコンピューター上にある場合は、次のことを行う必要があります。

- TCP/IP 経由の通信を許可するように SQL Server ネットワーク設定を構成します。
- SQL Server インスタンスが使用するポートで TCP トラフィック (場合によってはユーザーデータグラムプロトコル (UDP) トラフィック) を許可するように、ハードウェアまたはソフトウェアのファイアウォールを構成します。

SQL Server が TCP/IP 経由で通信できるようにするには、SQL Server 構成マネージャーを使用して、SQL Server インスタンスのネットワーク構成を変更します。

**TCP/IP を使用して SQL Server が通信できるようにするには**

1. **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントし、 **[Microsoft SQL Server 2008 R2]** をクリックし、 **[構成ツール]** をクリックして、 **[SQL Server 構成マネージャー]** をクリックします。
2. ツリービューウィンドウで、 **[SQL Server ネットワークの構成]** を展開し、 **[MSSQLSERVER のプロトコル]** をクリックします。

   > [!NOTE]
   > SQL Server の複数のインスタンスをインストールした場合は、各インスタンスの<em>[インスタンス名]</em>項目<strong>のプロトコル</strong>が表示されます。 インスタンスごとにネットワーク設定を構成する必要があります。
3. 詳細ペインで、 **[tcp/ip]** 行を右クリックし、 **[有効]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. **[警告]** ダイアログボックスで、[ **OK]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 新しいネットワーク構成を有効にするには、MSSQLSERVER サービスを再起動する必要があります。 これは、コマンドプロンプト、サービスコンソール、または SQL Server Management Studio で行うことができます。 この手順では、SQL Server Management Studio を使用します。
6. SQL Server 構成マネージャーを閉じます。
7. **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントし、 **[Microsoft SQL Server 2008 R2]** をクリックして、 **[SQL Server Management Studio]** をクリックします。
8. **[サーバーへの接続]** ダイアログボックスの **[サーバー名]** ボックスに、データベースサーバーの名前を入力し、 **[接続]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. **オブジェクトエクスプローラー**ペインで、親サーバーノード ( **TESTDB1**など) を右クリックし、 **[再起動]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. **[Microsoft SQL Server Management Studio]** ダイアログボックスで、 **[はい]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. サービスが再起動したら、SQL Server Management Studio を閉じます。

ファイアウォールを通過する SQL Server トラフィックを許可するには、まず、SQL Server インスタンスで使用されているポートを把握しておく必要があります。 これは、SQL Server インスタンスの作成方法と構成方法によって異なります。

- SQL Server の*既定のインスタンス*は、TCP ポート1433で要求 (および応答) をリッスンします。
- SQL Server の*名前付きインスタンス*は、動的に割り当てられた TCP ポートで要求をリッスンし、その要求に応答します。
- SQL Server Browser サービスが有効になっている場合、クライアントは、UDP ポート1434でサービスを照会して、特定の SQL Server インスタンスに使用する TCP ポートを調べることができます。 ただし、多くの場合、このサービスはセキュリティ上の理由で無効になっています。

SQL Server の既定のインスタンスを使用していると仮定した場合は、トラフィックを許可するようにファイアウォールを構成する必要があります。

| Direction | ポートから | ポートへの | ポートの種類 |
| --- | --- | --- | --- |
| 受信 | Any | 1433 | TCP |
| 送信 | 1433 | Any | TCP |

> [!NOTE]
> 技術的には、クライアントコンピューターは、1024と5000の間にランダムに割り当てられた TCP ポートを使用して SQL Server と通信し、それに応じてファイアウォール規則を制限することができます。 SQL Server ポートとファイアウォールの詳細については、「[ファイアウォール経由で SQL と通信するために必要な tcp/ip ポート番号](https://go.microsoft.com/?linkid=9805125)」と「[特定の Tcp ポートで受信待ちするようにサーバーを構成する方法 (SQL Server 構成マネージャー)](https://msdn.microsoft.com/library/ms177440.aspx)」を参照してください。

ほとんどの Windows Server 環境では、データベースサーバーで Windows ファイアウォールを構成することが必要になる場合があります。 既定では、Windows ファイアウォールは、規則によって明示的に禁止されていない限り、すべての送信トラフィックを許可します。 Web サーバーがデータベースに接続できるようにするには、SQL Server インスタンスが使用するポート番号の TCP トラフィックを許可する受信規則を構成する必要があります。 SQL Server の既定のインスタンスを使用している場合は、次の手順に従ってこの規則を構成できます。

**既定の SQL Server インスタンスとの通信を許可するように Windows ファイアウォールを構成するには**

1. データベースサーバーの **[スタート]** メニューで、 **[管理ツール]** をポイントし、 **[セキュリティが強化された Windows ファイアウォール]** をクリックします。
2. ツリービューペインで、 **[受信の規則]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. **操作**ウィンドウで、 **[受信の規則]** の **[新しい規則]** をクリックします。
4. 新規の受信の規則ウィザードの **[規則の種類]** ページで、 **[ポート]** を選択し、 **[次へ]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. **[プロトコルおよびポート]** ページで、 **[TCP]** が選択されていることを確認し、 **[特定のローカルポート]** ボックスに「 **1433**」と入力して、 **[次へ]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. **[操作]** ページで、 **[接続を許可する]** をそのまま使用し、 **[次へ]** をクリックします。
7. **[プロファイル]** ページで、 **[ドメイン]** を選択したままにして、 **[プライベート]** および **[パブリック]** チェックボックスをオフにし、 **[次へ]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. **[名前]** ページで、規則にわかりやすい名前を付けます (たとえば、 **SQL Server 既定のインスタンス–ネットワークアクセス**)。次に、 **[完了]** をクリックします。

SQL Server 用に Windows ファイアウォールを構成する方法の詳細については、特に、非標準ポートまたは動的ポート経由で SQL Server と通信する必要がある場合は、「[方法: データベースエンジンアクセスできるように Windows ファイアウォールを構成する](https://technet.microsoft.com/library/ms175043.aspx)」を参照してください。

## <a name="configure-logins-and-database-permissions"></a>ログインとデータベースのアクセス許可を構成する

Web アプリケーションをインターネットインフォメーションサービス (IIS) に展開すると、アプリケーションはアプリケーションプールの id を使用して実行されます。 ドメイン環境では、アプリケーションプール id は、それらが実行されているサーバーのコンピューターアカウントを使用して、ネットワークリソースにアクセスします。 コンピューターアカウントは、 <em>[domain name]</em><strong>\</strong ><em>[コンピューター名]</em> <strong>$</strong> &#x2014;(たとえば、 <strong>FABRIKAM\TESTWEB1 $</strong>) という形式になります。 Web アプリケーションがネットワーク経由でデータベースにアクセスできるようにするには、次のことを行う必要があります。

- Web サーバーコンピューターアカウントのログインを SQL Server インスタンスに追加します。
- コンピューターアカウントのログインを必要なデータベースロールにマップします (通常は**db\_datareader**と**db\_datawriter**)。

Web アプリケーションが単一サーバーではなくサーバーファームで実行されている場合は、サーバーファーム内のすべての web サーバーに対してこれらの手順を繰り返す必要があります。

> [!NOTE]
> アプリケーションプール id とネットワークリソースへのアクセスの詳細については、「[アプリケーションプール id](https://go.microsoft.com/?linkid=9805123)」を参照してください。

これらのタスクには、さまざまな方法でアプローチできます。 ログインを作成するには、次のいずれかの方法を使用できます。

- Transact-sql または SQL Server Management Studio を使用して、データベースサーバーでログインを手動で作成します。
- Visual Studio で SQL Server 2008 サーバープロジェクトを使用して、ログインを作成および配置します。

SQL Server ログインは、データベースレベルのオブジェクトではなく、サーバーレベルのオブジェクトであるため、配置するデータベースに依存しません。 そのため、任意の時点でログインを作成できます。最も簡単な方法は、データベースの配置を開始する前に、データベースサーバーでログインを手動で作成することです。 SQL Server Management Studio でログインを作成するには、次の手順を実行します。

**Web サーバーコンピューターアカウントの SQL Server ログインを作成するには**

1. データベースサーバーで、 **[スタート]** メニューの すべての **[プログラム]** をポイントし、 **[Microsoft SQL Server 2008 R2]** をクリックして、 **[SQL Server Management Studio]** をクリックします。
2. **[サーバーへの接続]** ダイアログボックスの **[サーバー名]** ボックスに、データベースサーバーの名前を入力し、 **[接続]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. **オブジェクトエクスプローラー**ペインで、 **[セキュリティ]** を右クリックし、 **[新規作成]** をポイントして、 **[ログイン]** をクリックします。
4. **[ログイン-新規作成]** ダイアログボックスの **[ログイン名]** ボックスに、web サーバーコンピューターアカウントの名前 (たとえば、 **FABRIKAM\TESTWEB1 $** ) を入力します。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. **[OK]** をクリックします。

この時点で、データベースサーバーは Web 配置パブリッシングの準備ができています。 ただし、必要なデータベースの役割にコンピューターアカウントのログインをマップするまで、展開するソリューションは機能しません。 データベースロールへのログインのマッピングでは、データベースを配置した後にロールをマップできないため、さらに多くのことを検討する必要があります。 コンピューターアカウントのログインを必要なデータベースロールにマップするには、次のいずれかの方法を使用できます。

- データベースを初めて配置した後、データベースロールをログインに手動で割り当てます。
- 配置後スクリプトを使用して、データベースロールをログインに割り当てます。

ログインとデータベースロールマッピングの作成を自動化する方法の詳細については、「[テスト環境にデータベースロールメンバーシップを配置する](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)」を参照してください。 または、次の手順を使用して、コンピューターアカウントのログインを必要なデータベースの役割に手動でマップすることもできます。 データベースを配置*するまでは、この*手順を実行できないことに注意してください。

**データベースロールを web サーバーコンピューターアカウントログインにマップするには**

1. 以前と同じように SQL Server Management Studio を開きます。
2. **オブジェクトエクスプローラー**ウィンドウで、 **[セキュリティ]** ノードを展開し、 **[ログイン]** ノードを展開します。次に、コンピューターアカウントのログイン ( **FABRIKAM\TESTWEB1 $** など) をダブルクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. **[ログインのプロパティ]** ダイアログボックスで、 **[ユーザーマッピング]** をクリックします。
4. [**このログインにマップ**されたユーザー] テーブルで、データベースの名前を選択します ( **contactmanager**など)。
5. [**データベースロールのメンバーシップ:** *[データベース名]* ] 一覧で、必要なアクセス許可を選択します。 Contact Manager サンプルソリューションの場合は、 **db\_datareader**および**db\_datawriter**ロールを選択する必要があります。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. **[OK]** をクリックします。

データベースロールの手動マッピングはテスト環境にとっては十分ではありませんが、ステージング環境や運用環境に対する自動またはワンクリックでのデプロイには適していません。 この種類のタスクを自動化する方法の詳細については、「[テスト環境にデータベースロールメンバーシップを配置する](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)」の配置後スクリプトを使用する方法に関する記事をご覧ください。

> [!NOTE]
> サーバープロジェクトとデータベースプロジェクトの詳細については、「 [Visual Studio 2010 SQL Server データベースプロジェクト](https://msdn.microsoft.com/library/ff678491.aspx)」を参照してください。

## <a name="configure-permissions-for-the-deployment-account"></a>デプロイアカウントのアクセス許可を構成する

展開の実行に使用するアカウントが SQL Server 管理者でない場合は、このアカウントのログインも作成する必要があります。 データベースを作成するには、アカウントが**dbcreator**サーバーロールのメンバーであるか、同等の権限を持っている必要があります。

> [!NOTE]
> Web 配置または VSDBCMD を使用してデータベースを配置する場合は、Windows 資格情報または SQL Server 資格情報を使用できます (SQL Server インスタンスが混合モード認証をサポートするように構成されている場合)。 次の手順では、Windows 資格情報を使用することを前提としていますが、展開を構成するときに接続文字列で SQL Server ユーザー名とパスワードを指定することはできません。

**デプロイアカウントのアクセス許可を設定するには**

1. 以前と同じように SQL Server Management Studio を開きます。
2. **オブジェクトエクスプローラー**ペインで、 **[セキュリティ]** を右クリックし、 **[新規作成]** をポイントして、 **[ログイン]** をクリックします。
3. **[ログイン-新規作成]** ダイアログボックスの **[ログイン名]** ボックスに、デプロイアカウントの名前 (たとえば、 **FABRIKAM\matt**) を入力します。
4. **[ページの選択]** ペインで、 **[サーバーロール]** をクリックします。
5. **Dbcreator**を選択し、 **[OK]** をクリックします。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

以降のデプロイをサポートするには、最初のデプロイ後に、データベースの**db\_所有者**ロールに展開アカウントを追加する必要もあります。 これは、以降の配置では、新しいデータベースを作成するのではなく、既存のデータベースのスキーマを変更するためです。 前のセクションで説明したように、データベースを作成するまで、データベースロールにユーザーを追加することはできません。

**デプロイアカウントのログインを db\_所有者データベースロールにマップするには**

1. 以前と同じように SQL Server Management Studio を開きます。
2. **[オブジェクトエクスプローラー]** ウィンドウで、 **[セキュリティ]** ノードを展開し、 **[ログイン]** ノードを展開して、コンピューターアカウントのログイン (たとえば、 **FABRIKAM\matt**) をダブルクリックします。
3. **[ログインのプロパティ]** ダイアログボックスで、 **[ユーザーマッピング]** をクリックします。
4. [**このログインにマップ**されたユーザー] テーブルで、データベースの名前を選択します ( **contactmanager**など)。
5. [**データベースロールのメンバーシップ:** *[データベース名]* ] 一覧で、 **db\_所有者**ロールを選択します。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. **[OK]** をクリックします。

## <a name="conclusion"></a>まとめ

これで、データベースサーバーは、リモートデータベースの配置を受け入れ、リモートの IIS web サーバーがデータベースにアクセスできるようになります。 データベースの配置と使用を試行する前に、次のキーポイントを確認することをお勧めします。

- リモート TCP/IP 接続を受け入れるように SQL Server を構成しましたか?
- SQL Server トラフィックを許可するようにファイアウォールを構成しましたか?
- SQL Server にアクセスするすべての web サーバーに対して、コンピューターアカウントのログインを作成しましたか?
- データベースの配置にユーザーロールマッピングを作成するスクリプトが含まれていますか。または、初めてデータベースを配置した後に手動で作成する必要がありますか。
- デプロイアカウントのログインを作成し、 **dbcreator**サーバーロールに追加しましたか?

## <a name="further-reading"></a>参考資料

データベースプロジェクトの配置のガイダンスについては、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。 配置後スクリプトを実行してデータベースロールのメンバーシップを作成する方法については、「[テスト環境へのデータベースロールのメンバーシップの配置](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)」を参照してください。 メンバーシップデータベースによってもたらされる固有のデプロイの問題を満たす方法については、「[エンタープライズ環境へのメンバーシップデータベースの配置](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [次へ](creating-a-server-farm-with-the-web-farm-framework.md)
