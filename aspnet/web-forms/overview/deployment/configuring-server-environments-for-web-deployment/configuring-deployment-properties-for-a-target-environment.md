---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: ターゲット環境の配置プロパティの構成 |Microsoft Docs
author: jrjlee
description: このトピックでは、サンプルの Contact Manager ソリューションを特定のターゲット環境にデプロイするために、環境固有のプロパティを構成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 9742be7d718384c1b108d5f2c0c43e8e8d4fe8a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516808"
---
# <a name="configuring-deployment-properties-for-a-target-environment"></a>ターゲット環境の配置プロパティを構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、サンプルの Contact Manager ソリューションを特定のターゲット環境にデプロイするために、環境固有のプロパティを構成する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ソリューション&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「ビルド[プロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法に基づいて&#x2014;います。この方法では、ビルドプロセスは、各配置先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="process-overview"></a>プロセスの概要

Contact Manager ソリューションのビルドと配置に使用するプロジェクトファイルは、次の2つの物理ファイルに分割されます。

- ユニバーサルビルド設定と命令 ( *Publish*ファイル) を含む1つ。
- 1つは、環境固有のビルド設定 (*env、proj*、 *env*など) を格納するものです。

ビルド時に、適切な環境固有のプロジェクトファイルが universal *Publish. proj*ファイルにマージされ、ビルド命令の完全なセットが形成されます。 独自の配置シナリオを記述した設定を使用して、環境固有のプロジェクトファイルを作成またはカスタマイズすることにより、特定の宛先環境への配置を構成できます。

これらの値の多くは、宛先の環境が特に&#x2014;どのように構成されているかによって決定されます。対象の web サーバーが Web Deployment Agent サービス (リモートエージェント) と Web 配置ハンドラーのどちらを使用するように構成されているかによって決まります。 これらの方法の詳細と、独自の環境に適したアプローチを選択するためのガイダンスについては、「 [Web 配置に適切なアプローチを選択する](choosing-the-right-approach-to-web-deployment.md)」を参照してください。

[Contact Manager のシナリオ](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)には、次の2つの環境固有のプロジェクトファイルが必要です。

- 開発者テスト環境への配置 (*Env Dev. proj*)。 開発者テスト環境は、リモートエージェントを使用したリモート配置を受け入れるように構成されています。詳細については、「[シナリオ: Web 配置用のテスト環境を構成](scenario-configuring-a-test-environment-for-web-deployment.md)する」を参照してください。 このファイルには、リモートエージェントエンドポイントアドレスと、接続文字列やサービスエンドポイントなどの場所固有の設定を指定する必要があります。
- ステージング環境への配置 (*Env-Stage. proj*)。 ステージング環境は、Web 配置ハンドラーを使用したリモートデプロイを受け入れるように構成されています。詳細については、「[シナリオ: Web デプロイのステージング環境の構成](scenario-configuring-a-staging-environment-for-web-deployment.md)」を参照してください。 このファイルには、Web 配置ハンドラエンドポイントアドレスだけでなく、接続文字列やサービスエンドポイントなどの場所固有の設定も指定する必要があります。

環境固有のプロジェクトファイルで構成する設定は、web パッケージ自体&#x2014;の内容には影響しないことに注意してください。パッケージの配置方法と、パッケージの抽出時に提供されるパラメーター値を制御します。 「[シナリオ: Web 配置用に運用環境を構成](scenario-configuring-a-production-environment-for-web-deployment.md)する」および「 [Web パッケージを手動でインストール](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)する」の説明に従って、web パッケージを運用環境に手動でインポートする場合は、パッケージの生成時に環境固有のプロジェクトファイルで使用した設定には関係ありません。 インターネットインフォメーションサービス (IIS) マネージャーでは、パッケージをインポートするときに、接続文字列やサービスエンドポイントなどのパラメーター化された値を入力するように求められます。

連絡先マネージャーソリューションを独自のターゲット環境に配置するには、このファイルをカスタマイズするか、テンプレートとして使用し、独自のファイルを作成します。

**Contact Manager ソリューションの環境固有の配置設定を構成するには**

1. Visual Studio 2010 で ContactManager-WCF ソリューションを開きます。
2. **[ソリューションエクスプローラー]** ウィンドウで、 **Publish**フォルダーを展開し、 **EnvConfig**フォルダーを展開して、 **[Env-Dev. proj]** をダブルクリックします。

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. *Env*ファイル内のプロパティ値を、独自のテスト環境の正しい値に置き換えます。

    > [!NOTE]
    > これらの各プロパティの詳細については、この手順の後の表を参照してください。
4. 作業内容を保存し、 *Env Dev. proj*ファイルを閉じます。

## <a name="choosing-the-right-deployment-properties"></a>適切に展開するためのプロパティの選択

次の表で*は、環境*固有のサンプルプロジェクトファイルの各プロパティの目的について説明し、指定する必要のある値についていくつかのガイダンスを提供します。

|                                                        プロパティ名                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        詳細                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>Msdeploycomputername</strong>対象の web サーバーまたはサービスエンドポイントの名前。               |                                                                                                                                                                                                                                              対象の web サーバー上のリモートエージェントサービスにデプロイする場合は、ターゲットコンピューター名 (たとえば、 <strong>TESTWEB1</strong>または<strong>TESTWEB1.fabrikam.net</strong>) を指定するか、リモートエージェントエンドポイントを指定できます (たとえば、`http://TESTWEB1/MSDEPLOYAGENTSERVICE`)。 各ケースでは、配置は同じように動作します。 送信先 Web サーバーの Web 配置ハンドラーに配置する場合は、サービスエンドポイントを指定し、IIS web サイトの名前をクエリ文字列パラメーターとして含める必要があります (`https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`など)。                                                                                                                                                                                                                                              |
|         <strong>Msdeployauth</strong>Web 配置がリモートコンピューターに対して認証を行うために使用するメソッド。          |                                                                                                                                                                                                                          これは<strong>NTLM</strong>または<strong>Basic</strong>に設定する必要があります。 通常、リモートエージェントサービスに配置している場合は<strong>NTLM</strong>を使用し、Web 配置ハンドラーに配置する場合は<strong>Basic</strong>を使用します。 基本認証を使用する場合は、展開を実行するために IIS Web 配置ツール (Web 配置) が偽装する必要があるユーザー名とパスワードも指定する必要があります。 この例では、これらの値は、 <strong>Msdeployusername</strong>プロパティと<strong>MSDeployPassword</strong>プロパティを通じて提供されます。 NTLM 認証を使用する場合は、これらのプロパティを省略するか、空白のままにしておくことができます。                                                                                                                                                                                                                          |
| <strong>Msdeployusername</strong>基本認証を使用する場合、Web 配置はリモートコンピューターでこのアカウントを使用します。  |                                                                                                                                                                                                                                                                                                                                                                                                                       これは、<em>ドメイン</em>\*username * (たとえば、 <strong>FABRIKAM\matt</strong>) の形式で指定する必要があります。 この値は、基本認証を指定した場合にのみ使用されます。 NTLM 認証を使用する場合は、プロパティを省略できます。 値を指定した場合は無視されます。                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong>基本認証を使用する場合、Web 配置はリモートコンピューターでこのパスワードを使用します。 |                                                                                                                                                                                                                                                                                                                                                                                                                    これは、 <strong>Msdeployusername</strong>プロパティで指定したユーザーアカウントのパスワードです。 この値は、基本認証を指定した場合にのみ使用されます。 NTLM 認証を使用する場合は、プロパティを省略できます。 値を指定した場合は無視されます。                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong>Contact Manager MVC アプリケーションをデプロイする IIS パス。     |                                                                                                                                                                                                                                                                                                                                                                        このパスは、IIS マネージャーに表示される [<em>iis web サイト名</em>]/[<em>web</em><em>アプリケーション名</em>] の形式で指定する必要があります。 アプリケーションを配置する前に、IIS web サイトが存在する必要があることに注意してください。 たとえば、DemoSite という名前の IIS web サイトを作成した場合は、MVC アプリケーションの IIS パスを DemoSite/ContactManager として指定できます。                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong>Contact Manager WCF サービスをデプロイする IIS パス。    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          たとえば、DemoSite という名前の IIS web サイトを作成した場合は、WCF サービスの IIS パスを<strong>demosite/ContactManagerService</strong>として指定できます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>Contactmanagertargeturl</strong>WCF サービスに到達できる URL。                   |                                                                                                                                                     これは、[<em>IIS web サイトのルート URL</em>]/[<em>サービスアプリケーション名</em>]/[<em>サービスエンドポイント</em>] の形式になります。 たとえば、ポート85で IIS web サイトを作成した場合、URL の形式は `http://localhost:85/ContactManagerService/ContactService.svc`になります。 MVC アプリケーションと WCF サービスは同じサーバーにデプロイされていることに注意してください。 このため、この URL は、インストールされているコンピューターからのみアクセスされます。 このため、URL では localhost または IP アドレスを使用することをお勧めします。コンピューター名やホストヘッダーではなく、IP アドレスを使用することをお勧めします。 コンピューター名またはホストヘッダーを使用する場合、IIS の[ループバックチェック](https://go.microsoft.com/?linkid=9805131)のセキュリティ機能によって URL がブロックされ、 <strong>HTTP 401.1-未承認</strong>のエラーが返されることがあります。                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong>データベースサーバーの接続文字列です。                  | 接続文字列は、VSDBCMD がデータベースサーバーへの接続に使用する資格情報と、データベースを作成するために使用する資格情報、およびデータベースサーバーへの接続とデータベースとの対話に web サーバーアプリケーションプールが使用する資格情報の両方を決定します。 基本的に、ここでは2つの選択肢があります。 <strong>Integrated security = true</strong>を指定できます。この場合、統合 Windows 認証が使用されます。 <strong>DATA Source = TESTDB1; integrated security = true</strong>の場合、VSDBCMD 実行可能ファイルを実行するユーザーの資格情報を使用してデータベースが作成され、アプリケーションは web サーバーコンピューターアカウントの id を使用してデータベースにアクセスします。 または、SQL Server アカウントのユーザー名とパスワードを指定することもできます。 この場合、データベースを作成するための VSDBCMD と、データベースとの対話のためのアプリケーションプール ( <strong>Data Source = TESTDB1;) の両方で、SQL Server の資格情報が使用されます。ユーザー Id = ASqlUser;Password = Pa $ $w 0rd</strong>このトピックのチュートリアルでは、統合 Windows 認証を使用することを前提としています。 |
|        <strong>Cmtargetdatabase</strong>データベースサーバーに作成するデータベースの名前を指定します。        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     ここで指定する値は、パラメーターとして VSDBCMD コマンドに追加されます。 また、web サーバー上のアプリケーションプールがデータベースとの対話に使用できる完全な接続文字列を作成するためにも使用されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

これらの例は、特定の展開シナリオでこれらのプロパティを構成する方法を示しています。

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>例 1&#x2014;リモートエージェントサービスへの展開

次の点に注意してください。

- TESTWEB1 のリモートエージェントサービスに配置しています。
- NTLM 認証を使用する Web 配置を指示しています。 Microsoft Build Engine (MSBuild) の呼び出しに使用した資格情報を使用して Web 配置が実行されます。
- 統合認証を使用して、 **Contactmanager**データベースを TESTDB1 にデプロイしています。 データベースは、MSBuild を呼び出すために使用した資格情報を使用してデプロイされます。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]

### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>例 2&#x2014;Web 配置ハンドラエンドポイントへの配置

次の点に注意してください。

- STAGEWEB1 の Web 配置 Handler サービスエンドポイントに配置しています。
- 基本認証を使用する Web 配置を指示しています。
- リモートコンピューター上の FABRIKAM\stagingdeployer アカウントを偽装する Web 配置を指定しています。
- SQL Server 認証を使用して、 **Contactmanager**データベースを STAGEDB1 にデプロイしています。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]

## <a name="conclusion"></a>まとめ

この時点で、プロジェクトファイルは、Contact Manager ソリューションをビルドして1つ以上の送信先環境に配置するように完全に構成されています。

このようなプロジェクトファイルを単一ステップの反復可能なデプロイプロセスの一部として使用するには、MSBuild を使用して*Publish*ファイルを実行し、環境固有のプロジェクトファイルの場所をパラメーターとして渡す必要があります。 これは、さまざまな方法で行うことができます。

- MSBuild の概要とカスタムプロジェクトファイルの概要については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」を参照してください。
- カスタムプロジェクトファイルを実行する MSBuild コマンドを作成する方法の詳細については、「 [Web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」を参照してください。
- 単一ステップの反復可能なデプロイのために MSBuild コマンドをコマンドファイルに組み込む方法については、「[配置コマンドファイルの作成と実行](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)」を参照してください。
- チームビルドからカスタムプロジェクトファイルを実行する方法については、「[配置をサポートするビルド定義の作成](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [[戻る]](creating-a-server-farm-with-the-web-farm-framework.md)
