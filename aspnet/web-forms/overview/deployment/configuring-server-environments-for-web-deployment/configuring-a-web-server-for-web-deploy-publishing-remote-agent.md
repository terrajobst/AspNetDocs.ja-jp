---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: Web 配置パブリッシング用の Web サーバーの構成 (リモートエージェント) |Microsoft Docs
author: jrjlee
description: このトピックでは、IIS Web 配置を使用して web 発行と配置をサポートするようにインターネットインフォメーションサービス (IIS) web サーバーを構成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589049"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>Web 配置発行の Web サーバーを構成する (リモート エージェント)

[Jason Lee](https://github.com/jrjlee)

[PDF のダウンロード](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、IIS Web Deployment Tool (Web 配置) リモートエージェントサービスを使用して、web 発行および展開をサポートするようにインターネットインフォメーションサービス (IIS) web サーバーを構成する方法について説明します。
> 
> Web 配置2.0 以降を使用する場合は、アプリケーションまたはサイトを Web サーバーに取り込むために使用できる3つの主な方法があります。 次の操作を行うことができます。
> 
> - *Web 配置リモートエージェントサービス*を使用します。 この方法では、web サーバーの構成が少なくて済みますが、サーバーに何かを展開するには、ローカルサーバー管理者の資格情報を指定する必要があります。
> - *Web 配置ハンドラー*を使用します。 この方法ははるかに複雑で、web サーバーを設定するためにより多くの初期作業が必要になります。 ただし、この方法を使用する場合は、管理者以外のユーザーが展開を実行できるように IIS を構成できます。 Web 配置ハンドラーは、IIS バージョン7以降でのみ使用できます。
> - *オフライン展開*を使用します。 この方法では、web サーバーの構成を最小限にする必要がありますが、サーバー管理者は web パッケージをサーバーに手動でコピーし、IIS マネージャーを使用してインポートする必要があります。
> 
> これらの方法の主な機能、長所、および短所の詳細については、「 [Web 配置に適切なアプローチを選択する](choosing-the-right-approach-to-web-deployment.md)」を参照してください。

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>Web 配置リモートエージェントは適切な方法ですか。

はい。コンテンツを展開するユーザーが、移行先サーバーで管理者の資格情報を提供できます。 この方法は、多くの場合、次のようなシナリオに適しています。

- 開発環境またはテスト環境。開発者は、対象となる web サーバーとデータベースサーバーを完全に制御できます。
- 小規模な組織では、1人のユーザーまたは少数のユーザーのグループが、アプリケーションのライフサイクル全体を制御します。

多くの大規模な組織では、特にステージング環境や運用環境では、web サーバーに対する管理者権限をユーザーに付与するのは現実的ではありません。 ホストされている web サーバーの場合、これは特にそうではない可能性があります。 また、ビルドサーバーからの配置を自動化する予定がある場合は、展開プロセスで管理者の資格情報を使用しないことをお勧めします。 これらのシナリオでは、 [Web 配置ハンドラー](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)を使用した配置をサポートするように web サーバーを構成すると、より適切な選択肢が得られる場合があります。

## <a name="task-overview"></a>タスクの概要

このトピックでは、Web 配置リモートエージェントアプローチを使用して、リモートコンピューターから web パッケージを受け入れて展開するようにインターネットインフォメーションサービス (IIS) 7.5 web サーバーを構成する方法について説明します。 次のことを行う必要があります。

- IIS 7.5 および IIS 7 推奨構成をインストールします。
- Web 配置2.1 以降をインストールします。
- デプロイされたコンテンツをホストするための IIS web サイトを作成します。
- Web Deployment Agent サービスが実行されていることを確認します。

サンプルソリューションを具体的にホストするには、次のことも行う必要があります。

- .NET Framework 4.0 をインストールします。
- ASP.NET MVC 3 をインストールします。

このトピックでは、これらの各手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、Windows Server 2008 R2 を実行するクリーンなサーバービルドから始めることを前提としています。 続行する前に、次のことを確認してください。

- Windows Server 2008 R2 Service Pack 1 および利用可能なすべての更新プログラムがインストールされています。
- サーバーはドメインに参加しています。
- サーバーには静的 IP アドレスがあります。

> [!NOTE]
> コンピューターをドメインに参加させる方法の詳細については、「[コンピューターをドメインに参加](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)させ、ログオンする」を参照してください。 静的 IP アドレスの構成の詳細については、「[静的 Ip アドレスの構成](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)」を参照してください。 リモートエージェントサービスは IIS 6 以降でサポートされているため、ドメインに参加する必要はありません。 ただし、このチュートリアルの手順は IIS 7.5 で開発およびテストされており、他のバージョンの手順は異なる場合があります。

## <a name="install-products-and-components"></a>製品とコンポーネントのインストール

このセクションでは、必要な製品とコンポーネントを web サーバーにインストールする手順について説明します。 開始する前に、Windows Update を実行して、サーバーが完全に最新の状態になっていることを確認することをお勧めします。

この場合は、次のものをインストールする必要があります。

- **IIS 7 推奨構成**。 これにより、web サーバー上で**Web サーバー (iis)** の役割が有効になり、ASP.NET アプリケーションをホストするために必要な iis モジュールとコンポーネントのセットがインストールされます。
- **.NET Framework 4.0**。 これは、このバージョンの .NET Framework でビルドされたアプリケーションを実行するために必要です。
- **Web 配置ツール 2.1**以降。 これにより、Web 配置 (およびその基になる実行可能ファイル Msdeploy.exe) がサーバーにインストールされます。 このプロセスの一環として、Web Deployment Agent サービスをインストールして起動します。 このサービスを使用すると、リモートコンピューターから web パッケージを展開できます。
- **ASP.NET MVC 3**. これにより、MVC 3 アプリケーションを実行するために必要なアセンブリがインストールされます。

> [!NOTE]
> このチュートリアルでは、Web Platform Installer を使用して必要なコンポーネントをインストールし、構成する方法について説明します。 Web Platform Installer を使用する必要はありませんが、依存関係を自動的に検出して、常に最新の製品バージョンを確実に取得することで、インストールプロセスが簡略化されます。 詳細については、「 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)」を参照してください。

**必要な製品およびコンポーネントをインストールするには**

1. [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)をダウンロードしてインストールします。
2. インストールが完了すると、Web Platform Installer が自動的に起動します。

    > [!NOTE]
    > **[スタート]** メニューからいつでも Web Platform Installer を起動できるようになりました。 これを行うには、 **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[Microsoft Web Platform Installer]** をクリックします。
3. **Web Platform Installer 3.0**ウィンドウの上部にある **[Products]** をクリックします。
4. ウィンドウの左側のナビゲーションウィンドウで、 **[フレームワーク]** をクリックします。
5. **Microsoft .NET Framework 4**行に、.NET Framework がまだインストールされていない場合は、 **[追加]** をクリックします。

    > [!NOTE]
    > Windows Update に .NET Framework 4.0 が既にインストールされている可能性があります。 製品またはコンポーネントが既にインストールされている場合、Web Platform Installer では、 **[追加]** ボタンを、**インストールさ**れているテキストに置き換えることによってこれを示します。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. **ASP.NET MVC 3 (Visual Studio 2010)** 行で、 **[追加]** をクリックします。
7. ナビゲーションウィンドウで、 **[サーバー]** をクリックします。
8. **IIS 7 の推奨構成**行で、 **[追加]** をクリックします。
9. **[Web 配置ツール 2.1]** 行で、 **[追加]** をクリックします。
10. **[インストール]** をクリックします。 Web Platform Installer には、製品&#x2014;の一覧と、インストールする関連する依存&#x2014;関係が表示されます。ライセンス条項に同意するように求められます。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. ライセンス条項を確認し、条項に同意する場合は [**同意**する] をクリックします。
12. インストールが完了したら、 **[完了]** をクリックし、 **[Web Platform Installer 3.0]** ウィンドウを閉じます。

IIS をインストールする前に .NET Framework 4.0 をインストールした場合は、 [ASP.NET Iis Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_iis 登録ツール) を実行して、最新バージョンの ASP.NET を iis に登録する必要があります。 この操作を行わないと、IIS が静的コンテンツ (HTML ファイルなど) を処理することはありませんが、ASP.NET コンテンツを参照しようとすると、 **HTTP エラー 404.0-Not Found**が返されます。 この手順を使用して、ASP.NET 4.0 が登録されていることを確認できます。

**ASP.NET 4.0 を IIS に登録するには**

1. **[スタート]** をクリックし、「**コマンドプロンプト**」と入力します。
2. 検索結果で **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。
3. コマンドプロンプトウィンドウで、 **:** ディレクトリに移動します。
4. 次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 任意の時点で64ビットの web アプリケーションをホストする場合は、ASP.NET の64ビットバージョンを IIS に登録する必要もあります。 これを行うには、コマンドプロンプトウィンドウで、 **\framework64\v4.0.30319**ディレクトリに移動します。
6. 次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

この時点でもう一度 Windows Update を使用して、インストールした新しい製品とコンポーネントの利用可能な更新プログラムをダウンロードしてインストールすることをお勧めします。

## <a name="configure-the-iis-website"></a>IIS Web サイトを構成する

Web コンテンツをサーバーに展開する前に、コンテンツをホストするための IIS web サイトを作成して構成する必要があります。 Web 配置は、既存の IIS web サイトにのみ web パッケージを展開できます。web サイトを作成することはできません。 大まかに言えば、次のタスクを完了する必要があります。

- ファイルシステム上にコンテンツをホストするフォルダーを作成します。
- コンテンツを提供する IIS web サイトを作成し、ローカルフォルダーに関連付けます。
- ローカルフォルダーのアプリケーションプール id に読み取りアクセス許可を付与します。

IIS の既定の web サイトへのコンテンツのデプロイは停止されていませんが、テストシナリオやデモンストレーションシナリオ以外では、この方法はお勧めできません。 運用環境をシミュレートするには、アプリケーションの要件に固有の設定を使用して、新しい IIS web サイトを作成する必要があります。

**IIS web サイトを作成して構成するには**

1. ローカルファイルシステムで、コンテンツを格納するフォルダーを作成します (例、 **C:\ demosite**)。
2. **[スタート]** メニューの **[管理ツール]** をポイントし、 **[インターネットインフォメーションサービス (IIS) マネージャー]** をクリックします。
3. IIS マネージャーの **[接続]** ウィンドウで、サーバーノードを展開します (たとえば、 **TESTWEB1**)。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. **[サイト]** ノードを右クリックし、 **[Web サイトの追加]** をクリックします。
5. **[サイト名]** ボックスに、IIS web サイトの名前 ( **demosite**など) を入力します。
6. **[物理パス]** ボックスに、ローカルフォルダーのパス (たとえば、「 **c:\** 」) を入力します (または参照してください)。
7. **[ポート]** ボックスに、web サイトをホストするポート番号 ( **85**など) を入力します。

    > [!NOTE]
    > 標準ポート番号は、HTTP の場合は80、HTTPS の場合は443です。 ただし、この web サイトをポート80でホストする場合は、サイトにアクセスする前に、既定の web サイトを停止する必要があります。
8. Web サイトのドメインネームシステム (DNS) レコードを構成する場合を除き、 **[ホスト名]** ボックスは空白のままにして、[ **OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 運用環境では、web サイトをポート80でホストし、一致する DNS レコードと共にホストヘッダーを構成することが必要になる場合があります。 IIS 7 でホストヘッダーを構成する方法の詳細については、「 [Web サイトのホストヘッダーを構成する (iis 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)」を参照してください。 Windows Server 2008 R2 の DNS サーバーの役割の詳細については、「 [Dns サーバーの概要](https://technet.microsoft.com/library/cc770392.aspx)」および「 [dns サーバー](https://technet.microsoft.com/windowsserver/dd448607)」を参照してください。
9. **[アクション]** ウィンドウの **[サイトの編集]** の下にある **[バインド]** をクリックします。
10. **[サイトバインド]** ダイアログボックスで、 **[追加]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. **[サイトバインドの追加]** ダイアログボックスで、既存のサイト構成に合わせて**IP アドレス**と**ポート**を設定します。
12. **[ホスト名]** ボックスに、web サーバーの名前 (たとえば、 **TESTWEB1**) を入力し、[ **OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 最初のサイトバインドでは、IP アドレスとポートまたは `http://localhost:85`を使用してサイトにローカルにアクセスできます。 2番目のサイトバインドを使用すると、コンピューター名 (http://testweb1:85) など) を使用して、ドメイン上の他のコンピューターからサイトにアクセスできます。
13. **[サイトバインド]** ダイアログボックスで、 **[閉じる]** をクリックします。
14. **[接続]** ウィンドウで、 **[アプリケーションプール]** をクリックします。
15. **[アプリケーションプール]** ウィンドウで、アプリケーションプールの名前を右クリックし、 **[基本設定]** をクリックします。 既定では、アプリケーションプールの名前は web サイトの名前 ( **Demosite**など) と一致します。
16. **[.NET Framework のバージョン]** ボックスの一覧で **[.NET Framework v v4.0.30319]** を選択し、 **[OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > サンプルソリューションには .NET Framework 4.0 が必要です。 これは Web 配置全般の要件ではありません。

Web サイトがコンテンツを提供できるようにするには、アプリケーションプール id に、コンテンツが格納されているローカルフォルダーに対する読み取りアクセス許可が必要です。 IIS 7.5 では、アプリケーションプールは既定で一意のアプリケーションプール id で実行されます (以前のバージョンの IIS とは異なり、アプリケーションプールは通常、ネットワークサービスアカウントを使用して実行されます)。 アプリケーションプール id は実際のユーザーアカウントではなく、ユーザーまたはグループ&#x2014;の一覧には表示されず、アプリケーションプールの起動時に動的に作成されます。 各アプリケーションプール id は、非表示の項目としてローカル**IIS\_IUSRS**セキュリティグループに追加されます。

ファイルまたはフォルダーのアプリケーションプール id にアクセス許可を付与するには、次の2つの方法があります。

- <strong>IIS AppPool\</strong ><em>[アプリケーションプール名]</em>( <strong>iis AppPool\DemoSite</strong>など) の形式を使用して、アプリケーションプール id に直接アクセス許可を割り当てます。
- **IIS\_IUSRS**グループにアクセス許可を割り当てます。

最も一般的な方法は、ローカルの**IIS\_IUSRS**グループにアクセス許可を割り当てることです。この方法では、ファイルシステムのアクセス許可を再構成せずにアプリケーションプールを変更できるためです。 次の手順では、このグループベースの方法を使用します。

> [!NOTE]
> IIS 7.5 でのアプリケーションプール id の詳細については、「[アプリケーションプール id](https://go.microsoft.com/?linkid=9805123)」を参照してください。

**IIS web サイトのフォルダーのアクセス許可を構成するには**

1. Windows エクスプローラーで、ローカルフォルダーの場所を参照します。
2. フォルダーを右クリックし、 **[プロパティ]** をクリックします。
3. **[セキュリティ]** タブで、 **[編集]** をクリックし、 **[追加]** をクリックします。
4. **[場所]** をクリックします。 **[場所]** ダイアログボックスで、ローカルサーバーを選択し、[ **OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. **[ユーザーまたはグループの選択]** ダイアログボックスで、「 **IIS\_iusrs**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。
6. <em>[フォルダー名]</em>ダイアログボックス<strong>の [アクセス許可</strong>] で、新しいグループに、既定で [<strong>実行</strong>]、[<strong>フォルダーの内容の一覧表示</strong>]、および [<strong>読み取り</strong>] &amp; のアクセス許可が割り当てられていることを確認します。 これを変更せずに、[ <strong>OK]</strong>をクリックします。
7. [ <strong>OK</strong> ] をクリックして、 <em>[フォルダー名] の [</em><strong>プロパティ</strong>] ダイアログボックスを閉じます。

サーバーに web パッケージを配置する前の最後のタスクとして、Web Deployment Agent サービスが実行されていることを確認する必要があります。 リモートコンピューターからパッケージを展開する場合、Web Deployment Agent サービスはパッケージのコンテンツの抽出とインストールを行います。 サービスは、Web 配置ツールをインストールし、ネットワークサービス id で実行すると、既定で開始されます。

さまざまなコマンドラインユーティリティまたは Windows PowerShell コマンドレットを使用して、サービスが複数の異なる方法で実行されているかどうかを確認できます。 この手順では、UI ベースの簡単な方法について説明します。

**Web Deployment Agent サービスが実行されていることを確認するには**

1. **[スタート]** メニューで、 **[管理ツール]** をポイントして、 **[サービス]** をクリックします。
2. **[Web Deployment Agent サービス]** 行を見つけて、 **[状態]** が **[開始]** に設定されていることを確認します。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. サービスがまだ開始されていない場合は、 **[開始]** をクリックします。

## <a name="configure-firewall-exceptions"></a>ファイアウォール例外の構成

既定では、リモートエージェントサービスは、次の URL の TCP ポート80でリッスンします。

<http://servername.com/MSDEPLOYAGENTSERVICE>

ほとんどの場合、web サーバーはポート80で HTTP 要求をリッスンするため、リモートエージェントサービスに対して追加のファイアウォール規則を構成する必要はありません。 標準以外のポートでリッスンするようにインストールをカスタマイズした場合は、必要に応じてファイアウォールの例外を構成する必要があります。

## <a name="conclusion"></a>結論

この時点で、web サーバーは、リモートコンピューターから web パッケージを受け入れてインストールする準備ができています。 サーバーに web アプリケーションを配置する前に、次のキーポイントを確認することをお勧めします。

- ASP.NET 4.0 を IIS に登録しましたか?
- アプリケーションプール id に web サイトのソースフォルダーへの読み取りアクセス権があるかどうか。
- Web Deployment Agent サービスは実行されていますか?

## <a name="further-reading"></a>関連項目

カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを構成してリモートエージェントサービスに web パッケージを配置する方法のガイダンスについては、「[ターゲット環境の配置プロパティの構成](configuring-deployment-properties-for-a-target-environment.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](scenario-configuring-a-production-environment-for-web-deployment.md)
> [次へ](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
