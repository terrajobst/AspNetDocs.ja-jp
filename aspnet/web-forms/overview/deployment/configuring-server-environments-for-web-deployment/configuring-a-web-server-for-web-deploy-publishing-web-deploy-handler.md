---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: Web 配置パブリッシング用に Web サーバーを構成する (Web 配置ハンドラー) |Microsoft Docs
author: jrjlee
description: このトピックでは、IIS Web 配置を使用した web 発行と配置をサポートするようにインターネットインフォメーションサービス (IIS) web サーバーを構成する方法について説明します。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: baaebd32f08d3c6b861572c5c5a16ec0fb70aaf0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589034"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>Web 配置発行の Web サーバーを構成する (Web 配置ハンドラー)

[PDF のダウンロード](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、IIS Web 配置ハンドラーを使用した web 発行と配置をサポートするようにインターネットインフォメーションサービス (IIS) web サーバーを構成する方法について説明します。
> 
> Web 配置2.0 以降を使用する場合は、アプリケーションまたはサイトを Web サーバーに取り込むために使用できる3つの主な方法があります。 次の操作を行うことができます。
> 
> - *Web 配置リモートエージェントサービス*を使用します。 この方法では、web サーバーの構成が少なくて済みますが、サーバーに何かを展開するには、ローカルサーバー管理者の資格情報を指定する必要があります。
> - *Web 配置ハンドラー*を使用します。 この方法ははるかに複雑で、web サーバーを設定するためにより多くの初期作業が必要になります。 ただし、この方法を使用する場合は、管理者以外のユーザーが展開を実行できるように IIS を構成できます。 Web 配置ハンドラーは、IIS バージョン7以降でのみ使用できます。
> - *オフライン展開*を使用します。 この方法では、web サーバーの構成を最小限にする必要がありますが、サーバー管理者は web パッケージをサーバーに手動でコピーし、IIS マネージャーを使用してインポートする必要があります。
> 
> これらの方法の主な機能、長所、および短所の詳細については、「 [Web 配置に適切なアプローチを選択する](choosing-the-right-approach-to-web-deployment.md)」を参照してください。

はい、管理者以外のユーザーに特定の IIS web サイトへのコンテンツの展開を許可します。 この方法は、多くの場合、次のようなシナリオに適しています。

- ステージング環境または運用環境。リモート展開を開始するユーザーまたはサービスアカウントは、サーバー管理者の資格情報にアクセスできない可能性があります。
- ホストされている環境。リモートユーザーが web サーバーを完全に制御したり、他のすべての web サイトにアクセスしたりすることなく、web サイトを更新できるようにします。

開発やテストのシナリオ、または小規模な組織では、サーバー管理者の資格情報を使用したコンテンツの展開は、多くの場合、悪化になります。 これらのシナリオでは、 [Web 配置リモートエージェントサービス](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)を使用した配置をサポートするように web サーバーを構成すると、より簡単なアプローチが実現します。

## <a name="task-overview"></a>タスクの概要

Web 配置 Handler アプローチを使用してリモートコンピューターから web パッケージを受け入れて展開するように web サーバーを構成するには、次の手順を実行する必要があります。

- デプロイを実行するために使用する資格情報を持つドメインユーザーアカウント ("管理者以外のユーザー") を作成または選択します。
- Web 管理サービスと基本認証モジュールを含む IIS 7.5 をインストールします。
- Web 配置2.1 以降をインストールします。
- リモート接続を許可するように Web 管理サービスを構成し、サービスを開始します。
- デプロイされたコンテンツをホストするための IIS web サイトを作成します。
- IIS マネージャーで、管理者以外のユーザーに web サイトのアクセス許可を付与します。
- Web 管理サービスの委任規則により、サービスが管理者以外のユーザーアカウントを使用して web サイトのコンテンツを追加および変更できることを確認します。
- ポート8172で着信接続を許可するようにファイアウォールを構成します。

ContactManager サンプルソリューションを具体的にホストするには、次のことも行う必要があります。

- .NET Framework 4.0 をインストールします。
- ASP.NET MVC 3 をインストールします。

このトピックでは、これらの各手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、Windows Server 2016 を実行するクリーンなサーバービルドで作業を開始していることを前提としています。 続行する前に、次のことを確認してください。

- Windows Server 2016
- サーバーはドメインに参加しています。
- サーバーには静的 IP アドレスがあります。

> [!NOTE]
> コンピューターをドメインに参加させる方法の詳細については、「[コンピューターをドメインに参加](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)させ、ログオンする」を参照してください。 静的 IP アドレスの構成の詳細については、「[静的 Ip アドレスの構成](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)」を参照してください。

## <a name="install-products-and-components"></a>製品とコンポーネントのインストール

このセクションでは、必要な製品とコンポーネントを web サーバーにインストールする手順について説明します。 開始する前に、Windows Update を実行して、サーバーが完全に最新の状態になっていることを確認することをお勧めします。

この場合は、次のものをインストールする必要があります。

- **IIS 7 推奨構成**。 これにより、web サーバー上で**Web サーバー (iis)** の役割が有効になり、ASP.NET アプリケーションをホストするために必要な iis モジュールとコンポーネントのセットがインストールされます。
- **IIS: 管理サービス**。 これにより、IIS に Web 管理サービス (WMSvc) がインストールされます。 このサービスは、IIS web サイトのリモート管理を有効にし、クライアントに Web 配置ハンドラエンドポイントを公開します。
- **IIS: 基本認証**。 IIS の基本認証モジュールがインストールされます。 これにより、Web 管理サービス (WMSvc) が、指定した資格情報を認証できるようになります。
- **Web 配置ツール 2.1**以降。 これにより、Web 配置 (およびその基になる実行可能ファイル Msdeploy.exe) がサーバーにインストールされます。 このプロセスの一部として、Web 配置ハンドラーがインストールされ、Web 管理サービスと統合されます。
- **.NET Framework 4.0**。 これは、このバージョンの .NET Framework でビルドされたアプリケーションを実行するために必要です。
- **ASP.NET MVC 3**. これにより、MVC 3 アプリケーションを実行するために必要なアセンブリがインストールされます。

> [!NOTE]
> このチュートリアルでは、Web Platform Installer を使用してさまざまなコンポーネントをインストールし、構成する方法について説明します。 Web Platform Installer を使用する必要はありませんが、依存関係を自動的に検出して、常に最新の製品バージョンを確実に取得することで、インストールプロセスが簡略化されます。 詳細については、「 [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)」を参照してください。

**必要な製品およびコンポーネントをインストールするには**

1. [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)をダウンロードしてインストールします。
2. インストールが完了すると、Web Platform Installer が自動的に起動します。

    > [!NOTE]
    > **[スタート]** メニューからいつでも Web Platform Installer を起動できるようになりました。 これを行うには、 **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[Microsoft Web Platform Installer]** をクリックします。
3. **[Web Platform Installer]** ウィンドウの上部にある **[Products]** をクリックします。
4. ウィンドウの左側のナビゲーションウィンドウで、 **[フレームワーク]** をクリックします。
5. **Microsoft .NET Framework 4**行に、.NET Framework がまだインストールされていない場合は、 **[追加]** をクリックします。

    > [!NOTE]
    > Windows Update に .NET Framework 4.0 が既にインストールされている可能性があります。 製品またはコンポーネントが既にインストールされている場合、Web Platform Installer では、 **[追加]** ボタンを、**インストールさ**れているテキストに置き換えることによってこれを示します。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. **ASP.NET MVC 3 (Visual Studio 2010)** 行で、 **[追加]** をクリックします。
7. ナビゲーションウィンドウで、 **[サーバー]** をクリックします。
8. **IIS 7 の推奨構成**行で、 **[追加]** をクリックします。
9. **[Web 配置ツール 2.1]** 行で、 **[追加]** をクリックします。
10. **[IIS: 基本認証]** 行で、 **[追加]** をクリックします。
11. **[IIS: 管理サービス]** 行で、 **[追加]** をクリックします。
12. **[インストール]** をクリックします。 Web Platform Installer には、製品&#x2014;の一覧と、インストールする関連する依存&#x2014;関係が表示されます。ライセンス条項に同意するように求められます。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. ライセンス条項を確認し、条項に同意する場合は [**同意**する] をクリックします。
14. インストールが完了したら、 **[完了]** をクリックし、 **[Web Platform Installer]** ウィンドウを閉じます。

IIS をインストールする前に .NET Framework 4.0 をインストールした場合は、 [ASP.NET Iis Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_iis 登録ツール) を実行して、最新バージョンの ASP.NET を iis に登録する必要があります。 この操作を行わないと、IIS が静的コンテンツ (HTML ファイルなど) を処理することはありませんが、ASP.NET コンテンツを参照しようとすると、 **HTTP エラー 404.0-Not Found**が返されます。 ASP.NET 4.0 が登録されていることを確認するには、次の手順を実行します。

**ASP.NET 4.0 を IIS に登録するには**

1. **[スタート]** をクリックし、「**コマンドプロンプト**」と入力します。
2. 検索結果で **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。
3. コマンドプロンプトウィンドウで、 **:** ディレクトリに移動します。
4. 次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. 任意の時点で64ビットの web アプリケーションをホストする場合は、ASP.NET の64ビットバージョンを IIS に登録する必要もあります。 これを行うには、コマンドプロンプトウィンドウで、 **\framework64\v4.0.30319**ディレクトリに移動します。
6. 次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

この時点でもう一度 Windows Update を使用して、インストールした新しい製品とコンポーネントの利用可能な更新プログラムをダウンロードしてインストールすることをお勧めします。

## <a name="configure-the-web-management-service"></a>Web 管理サービスの構成

必要なものをすべてインストールしたので、次の手順では、IIS で Web 管理サービスを構成します。 大まかに言えば、次のタスクを完了する必要があります。

- サーバーレベルで基本認証を有効にします。
- リモート接続を受け入れるように Web 管理サービスを構成します。
- Web 管理サービスを開始します。
- 必要な Web 管理サービスの委任規則が設定されていることを確認します。

**Web 管理サービスを構成するには**

1. **[スタート]** メニューの **[管理ツール]** をポイントし、 **[インターネットインフォメーションサービス (IIS) マネージャー]** をクリックします。
2. IIS マネージャーの **[接続]** ウィンドウで、サーバーノード (たとえば、 **STAGEWEB1**) をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. 中央のウィンドウで、 **[IIS]** の下にある **[認証]** をダブルクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. **[基本認証]** を右クリックし、 **[有効]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. **[接続]** ウィンドウでサーバーノードをもう一度クリックして、最上位の設定に戻ります。
6. 中央のウィンドウで、 **[管理]** の下にある **[管理サービス]** をダブルクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. 中央のウィンドウで、 **[リモート接続を有効にする]** を選択します。

    > [!NOTE]
    > Web 管理サービスが既に実行されている場合は、最初に停止する必要があります。
8. **[操作]** ウィンドウで、 **[開始]** をクリックして Web 管理サービスを開始します。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. 設定を保存するように求められたら、 **[はい]** をクリックします。

    > [!NOTE]
    > また、サービスを自動的に開始するように構成することもできます。 これを行うには、サービス コンソールを開き、 **Web 管理サービス** を右クリックして、**プロパティ** をクリックします。 **[スタートアップの種類]** ドロップダウンリストで、 **[自動]** を選択し、 **[OK]** をクリックします。
10. **[接続]** ウィンドウでサーバーノードをもう一度クリックして、最上位の設定に戻ります。
11. 中央のウィンドウで、 **[管理]** の下にある **[管理サービスの委任]** をダブルクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. 中央のウィンドウに一連のルールが含まれていることを確認します。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    これらの規則は、承認された Web 管理サービスユーザーがさまざまな Web 配置プロバイダーを使用できるようにします。 たとえば、web アプリケーションとコンテンツを Web 配置ハンドラーを使用して IIS に展開するには、認証されたすべての Web 管理サービスユーザーが**Contentpath**および**iisapp**プロバイダー (スクリーンショットで確認できる最後のルール) を使用できるようにする委任ルールが必要です。

    製品とコンポーネントをこのトピックで説明されている順序でインストールした場合、最新バージョンの Web 配置によって、必要なすべての委任規則が Web 管理サービスに自動的に追加されます。 [管理サービスの委任] ページにルールが表示されない場合は、自分で作成する必要があります。 その方法については、「 [Web 配置ハンドラーの構成](https://go.microsoft.com/?linkid=9805124)」を参照してください。
13. **[接続]** ウィンドウでサーバーノードをもう一度クリックして、最上位の設定に戻ります。

## <a name="create-and-configure-an-iis-website"></a>IIS Web サイトの作成と構成

Web コンテンツをサーバーに展開する前に、コンテンツをホストするための IIS web サイトを作成して構成する必要があります。 Web 配置は、既存の IIS web サイトにのみ web パッケージを展開できます。web サイトを作成することはできません。 また、管理者以外のアカウントがコンテンツをリモートで展開できるようにするために、少し追加の構成を行う必要があります。 大まかに言えば、次のタスクを完了する必要があります。

- ファイルシステム上にコンテンツをホストするフォルダーを作成します。
- コンテンツを提供する IIS web サイトを作成し、ローカルフォルダーに関連付けます。
- ローカルフォルダーのアプリケーションプール id に読み取りアクセス許可を付与します。
- Web アプリケーションをデプロイするドメインアカウントに、必要な IIS アクセス許可を付与します。

IIS の既定の web サイトへのコンテンツのデプロイは停止されていませんが、テストシナリオやデモンストレーションシナリオ以外では、この方法はお勧めできません。 運用環境をシミュレートするには、アプリケーションの要件に固有の設定を使用して、新しい IIS web サイトを作成する必要があります。

**IIS web サイトを作成するには**

1. ローカルファイルシステムで、コンテンツを格納するフォルダーを作成します (例、 **C:\ demosite**)。
2. **[スタート]** メニューの **[管理ツール]** をポイントし、 **[インターネットインフォメーションサービス (IIS) マネージャー]** をクリックします。
3. IIS マネージャーの **[接続]** ウィンドウで、サーバーノードを展開します (たとえば、 **STAGEWEB1**)。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. **[サイト]** ノードを右クリックし、 **[Web サイトの追加]** をクリックします。
5. **[サイト名]** ボックスに、IIS web サイトの名前 ( **demosite**など) を入力します。
6. **[物理パス]** ボックスに、ローカルフォルダーのパス (たとえば、「 **c:\** 」) を入力します (または参照してください)。
7. **[ポート]** ボックスに、web サイトをホストするポート番号 ( **85**など) を入力します。

    > [!NOTE]
    > 標準ポート番号は、HTTP の場合は80、HTTPS の場合は443です。 ただし、この web サイトをポート80でホストする場合は、サイトにアクセスする前に、既定の web サイトを停止する必要があります。
8. Web サイトのドメインネームシステム (DNS) レコードを構成する場合を除き、 **[ホスト名]** ボックスは空白のままにして、[ **OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > 運用環境では、web サイトをポート80でホストし、一致する DNS レコードと共にホストヘッダーを構成することが必要になる場合があります。 IIS 7 でホストヘッダーを構成する方法の詳細については、「 [Web サイトのホストヘッダーを構成する (iis 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)」を参照してください。 Windows Server の DNS サーバーの役割の詳細については、「 [Dns サーバーの概要](https://technet.microsoft.com/library/cc770392.aspx)」および「 [dns サーバー](https://technet.microsoft.com/windowsserver/dd448607)」を参照してください。
9. **[アクション]** ウィンドウの **[サイトの編集]** の下にある **[バインド]** をクリックします。
10. **[サイトバインド]** ダイアログボックスで、 **[追加]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. **[サイトバインドの追加]** ダイアログボックスで、既存のサイト構成に合わせて**IP アドレス**と**ポート**を設定します。
12. **[ホスト名]** ボックスに、web サーバーの名前 (たとえば、 **STAGEWEB1**) を入力し、[ **OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > 最初のサイトバインドでは、IP アドレスとポートまたは `http://localhost:85`を使用してサイトにローカルにアクセスできます。 2番目のサイトバインドを使用すると、コンピューター名 (http://stageweb1:85) など) を使用して、ドメイン上の他のコンピューターからサイトにアクセスできます。
13. **[サイトバインド]** ダイアログボックスで、 **[閉じる]** をクリックします。
14. **[接続]** ウィンドウで、 **[アプリケーションプール]** をクリックします。
15. **[アプリケーションプール]** ウィンドウで、アプリケーションプールの名前を右クリックし、 **[基本設定]** をクリックします。 既定では、アプリケーションプールの名前は web サイトの名前 ( **Demosite**など) と一致します。
16. **[.NET clr バージョン]** ボックスの一覧で **[.net clr v v4.0.30319]** を選択し、 **[OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

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

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. **[ユーザーまたはグループの選択]** ダイアログボックスで、「 **IIS\_iusrs**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。
6. <em>[フォルダー名]</em>ダイアログボックス<strong>の [アクセス許可</strong>] で、新しいグループに、既定で [<strong>実行</strong>]、[<strong>フォルダーの内容の一覧表示</strong>]、および [<strong>読み取り</strong>] &amp; のアクセス許可が割り当てられていることを確認します。 これを変更せずに、[ <strong>OK]</strong>をクリックします。
7. [ <strong>OK</strong> ] をクリックして、 <em>[フォルダー名] の [</em><strong>プロパティ</strong>] ダイアログボックスを閉じます。

最後のタスクとして、コンテンツの展開に使用する資格情報を持つ管理者以外のユーザーに適切なアクセス許可を付与する必要があります。 このユーザーには、コンテンツを web サイトにリモートでデプロイするためのアクセス許可が必要です。

**管理者以外のドメインユーザーに対して IIS web サイトのアクセス許可を構成するには**

1. IIS マネージャーの **[接続]** ウィンドウで、web サイトノード ( **demosite**など) を右クリックし、 **[展開]** をポイントして、Web 配置の **[公開の構成]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. **[Web 配置の公開の構成]** ダイアログボックスの **[公開アクセス許可を付与するユーザーを選択し]** てください の一覧の右側にある省略記号ボタンをクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. **[ユーザーの許可]** ダイアログボックスで、コンテンツの展開に使用するアカウントのドメインとユーザー名を入力し、 **[OK]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. **[Web 配置の公開の構成]** ダイアログボックスで、 **[セットアップ]** をクリックします。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > この操作では、2つの主要機能が1つのステップで実行されます。 最初に、前のセクションで検証した委任規則に従って、Web サイトをリモートで変更するアクセス許可を Web 管理サービスを通じてユーザーに付与します。 次に、web サイトのソースフォルダーに対するフルコントロール権限をユーザーに付与します。これにより、ユーザーは web サイトのコンテンツに対するアクセス許可を追加、変更、および設定できます。
5. **[Web 配置の公開の構成]** ダイアログボックスで、 **[閉じる]** をクリックします。

## <a name="configure-firewall-exceptions"></a>ファイアウォール例外の構成

既定では、IIS Web 管理サービスは TCP ポート8172でリッスンします。 Web サーバーで Windows ファイアウォールが有効になっている場合は、ポート8172の TCP トラフィックを許可する新しい受信規則を作成する必要があります (すべての送信トラフィックは Windows ファイアウォールで既定で許可されます)。 サードパーティのファイアウォールを使用する場合は、トラフィックを許可するルールを作成する必要があります。

| Direction | ポートから | ポートへの | ポートの種類 |
| --- | --- | --- | --- |
| 内部 | すべての | 8172 | TCP |
| 向け | 8172 | すべての | TCP |

Windows ファイアウォールでの規則の構成の詳細については、「[ファイアウォール規則の構成](https://technet.microsoft.com/library/dd448559(WS.10).aspx)」を参照してください。 サードパーティ製のファイアウォールについては、製品ドキュメントを参照してください。

## <a name="conclusion"></a>結論

Web サーバーでは、Web 管理サービスを介して Web 配置ハンドラーへのリモート配置を受け入れる準備ができました。 サーバーに web アプリケーションを配置する前に、次のキーポイントを確認することをお勧めします。

- IIS のサーバーレベルで基本認証を有効にしましたか?
- Web 管理サービスへのリモート接続を有効にしましたか?
- Web 管理サービスを開始しましたか?
- 管理サービスの委任規則はありますか。
- アプリケーションプール id に web サイトのソースフォルダーへの読み取りアクセス権があるかどうか。
- 管理者以外のユーザーアカウントは、IIS でサイトレベルのアクセス許可を持っていますか。
- ファイアウォールでは、TCP ポート8172でサーバーへの着信接続が許可されていますか。

## <a name="further-reading"></a>関連項目

Web 配置ハンドラーに web パッケージを配置するためにカスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを構成する方法については、「[ターゲット環境の配置プロパティの構成](configuring-deployment-properties-for-a-target-environment.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [次へ](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
