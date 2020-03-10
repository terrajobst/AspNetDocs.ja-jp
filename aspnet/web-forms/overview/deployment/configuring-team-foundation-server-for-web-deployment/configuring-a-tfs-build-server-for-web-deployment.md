---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: Web 配置用の TFS ビルドサーバーの構成 |Microsoft Docs
author: jrjlee
description: このトピックでは、Team Foundation Server (TFS) ビルドサーバーを準備して、チームビルドとインターネット Informat を使用してソリューションをビルドおよび配置する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512224"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>Web 配置の TFS ビルド サーバーを構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、チームビルドおよびインターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、ソリューションをビルドおよび配置するための Team Foundation Server (TFS) ビルドサーバーを準備する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

ソリューションをビルドして配置するためにビルドサーバーを準備するには、次の作業を行う必要があります。

- TFS ビルドサービスをインストールして構成します。
- Visual Studio 2010 をインストールします。
- .NET Framework または ASP.NET MVC のバージョンなど、ソリューションのビルドに必要な製品またはコンポーネントをインストールします。
- Web 配置2.0 以降をインストールします。

このトピックでは、これらの手順を実行する方法、または既存のリソースを参照する方法について説明します。 このトピックのタスクとチュートリアルでは、次のことを前提としています。

- Windows Server 2008 R2 Service Pack 1 を実行しているクリーンなサーバービルドから開始します。
- サーバーは、静的 IP アドレスを使用してドメインに参加しています。
- 「[エンタープライズ Web デプロイ: シナリオの概要](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」で説明されているように、TFS アプリケーション層を別のサーバーにインストールしました。

### <a name="who-performs-these-procedures"></a>これらの手順を実行するユーザー

ほとんどの場合、TFS 管理者はビルドサーバーの構成を担当します。 場合によっては、開発者チームが特定のビルドサーバーの所有権を取得することがあります。

## <a name="install-and-configure-the-tfs-build-service"></a>TFS ビルドサービスのインストールと構成

ビルドサーバーを構成する場合、最初のタスクは、TFS ビルドサービスをインストールして構成することです。 このプロセスの一環として、次のことを行う必要があります。

- TFS ビルドサービスをインストールし、サービスアカウントを構成します。 配置を含むすべてのビルドタスクは、ビルドサービスアカウントの id を使用して実行されます。
- *ビルドコントローラー*と1つ以上の*ビルドエージェント*を作成します。 各ビルドコントローラーは、一連のビルドエージェントを管理します。 ビルドをキューに置いた場合、ビルドコントローラーは、ビルドタスクを利用可能なビルドエージェントに割り当てます。 TFS の各チームプロジェクトコレクションは、1つのビルドコントローラーにマップされます。
- ビルド出力用のドロップフォルダーを構成します。 これはネットワーク共有です。 Web 配置パッケージなどのすべてのビルド出力は、ドロップフォルダーに送信されます。

MSDN の「 [Team Foundation ビルドの管理](https://msdn.microsoft.com/library/ms252495.aspx)」の章には、次のタスクを実行するために必要なすべてのリソースが含まれています。

- ビルドサービス、ビルドコントローラー、ビルドエージェントなど、Team Foundation ビルドの概念の概要については、「 [Team Foundation ビルドシステムについ](https://msdn.microsoft.com/library/dd793166.aspx)て」を参照してください。
- ビルドサービスのインストールと構成の詳細については、「[ビルドコンピューターの構成](https://msdn.microsoft.com/library/ms181712.aspx)」を参照してください。
- ビルドコントローラーの作成の詳細については、「[ビルドコントローラーの作成と操作](https://msdn.microsoft.com/library/ee330987.aspx)」を参照してください。
- ビルドエージェントの作成の詳細については、「[ビルドエージェントの作成と操作](https://msdn.microsoft.com/library/bb399135.aspx)」を参照してください。
- ドロップフォルダーの作成と構成の詳細については、「[ドロップフォルダーの設定](https://msdn.microsoft.com/library/bb778394.aspx)」を参照してください。

## <a name="install-required-products-and-components"></a>必要な製品とコンポーネントのインストール

ビルドサーバーでソリューションをビルドできるようにするには、ソリューションに必要なすべての製品、コンポーネント、またはアセンブリをインストールする必要があります。 Web platform コンポーネントをインストールする前に、ビルドサーバーに Visual Studio 2010 (任意のバージョン) をインストールする必要があります。 これにより、コア Microsoft Build Engine (MSBuild) ターゲットファイルと Web 発行パイプライン (WPP) ターゲットファイルがビルドサービスで使用できるようになります。 また、Visual Studio インストーラーで Web 配置もインストールする必要があります。これは、ビルドプロセスの一部として Web パッケージを配置する場合に必要になります。

一般的な web プラットフォームコンポーネントをインストールする最良の方法は、 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)を使用することです。 これにより、各製品の最新バージョンをインストールし、各製品の前提条件を自動的に検出してインストールすることができます。 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ソリューションの場合は、Web Platform Installer を使用して、次の製品およびコンポーネントをインストールする必要があります。

- **.NET Framework 4.0**。 これは、このバージョンの .NET Framework でビルドされたアプリケーションを実行するために必要です。
- **Web 配置ツール 2.1**以降。 これにより、Web 配置 (およびその基になる実行可能ファイル Msdeploy.exe) がサーバーにインストールされます。 このプロセスの一環として、Web Deployment Agent サービスをインストールして起動します。 このサービスを使用すると、リモートコンピューターから web パッケージを展開できます。
- **ASP.NET MVC 3**. これにより、ASP.NET MVC 3 アプリケーションを実行するために必要なアセンブリがインストールされます。

**必要な製品およびコンポーネントをインストールするには**

1. Visual Studio 2010 をインストールします。 インストールする機能の選択を求めるメッセージが表示されたら、次のものを含める必要があります。

    1. コンパイルが必要なすべてのプログラミング言語。
    2. Visual Web Developer。 これにより、WPP ターゲットがビルドサーバーに追加されます。

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 のインストールが完了したら、 [Visual studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133)をダウンロードしてインストールします (インストールメディアにまだ含まれていない場合)。

    > [!NOTE]
    > Visual Studio 2010 Service Pack 1 では、MSBuild が Msdeploy.exe 実行可能ファイルを見つけることができないバグが解決されます。
3. [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)をダウンロードして起動します。
4. **Web Platform Installer 3.0**ウィンドウの上部にある **[Products]** をクリックします。
5. ウィンドウの左側のナビゲーションウィンドウで、 **[フレームワーク]** をクリックします。
6. **Microsoft .NET Framework 4**行に、.NET Framework がまだインストールされていない場合は、 **[追加]** をクリックします。

    > [!NOTE]
    > Windows Update に .NET Framework 4.0 が既にインストールされている可能性があります。 製品またはコンポーネントが既にインストールされている場合、Web Platform Installer では、 **[追加]** ボタンを、**インストールさ**れているテキストに置き換えることによってこれを示します。

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. **ASP.NET MVC 3 (Visual Studio 2010)** 行で、 **[追加]** をクリックします。
8. ナビゲーションウィンドウで、 **[サーバー]** をクリックします。
9. **[Web 配置ツール 2.1]** 行で、 **[追加]** をクリックします。
10. **[インストール]** をクリックします。 Web Platform Installer には、製品&#x2014;の一覧と、インストールする関連する依存&#x2014;関係が表示されます。ライセンス条項に同意するように求められます。
11. ライセンス条項を確認し、条項に同意する場合は [**同意**する] をクリックします。
12. インストールが完了したら、 **[完了]** をクリックし、 **[Web Platform Installer 3.0]** ウィンドウを閉じます。

> [!NOTE]
> 配置プロセスに VSDBCMD や SQLCMD などのツールの使用が含まれている場合は、これらがビルドサーバーにインストールされていることを確認する必要があります。 VSDBCMD は Visual Studio ツールであり、通常は Team Foundation ビルドをインストールするときにサーバーに追加されます。 SQLCMD は SQL Server ツールです。 スタンドアロンバージョンの SQLCMD は、 [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134)のページからダウンロードできます。

## <a name="conclusion"></a>まとめ

この時点で、ビルドサーバーは、web アプリケーションプロジェクトのビルドと配置を開始する準備ができています。 次のトピック「[配置をサポートするビルド定義の作成](creating-a-build-definition-that-supports-deployment.md)」では、ビルド定義を作成および構成して、プロジェクトをビルドおよび配置するタイミングと方法を制御する方法について説明します。

## <a name="further-reading"></a>参考資料

チームビルドを操作するための一般的なガイダンスについては、「 [Team Foundation ビルドの管理](https://msdn.microsoft.com/library/ms252495.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](adding-content-to-source-control.md)
> [次へ](creating-a-build-definition-that-supports-deployment.md)
