---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 'アプリケーションライフサイクル管理: 開発から運用、Microsoft Docs'
author: jrjlee
description: このトピックでは、架空の企業が、テスト環境、ステージング環境、および運用環境を通じて ASP.NET web アプリケーションのデプロイを管理する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520426"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>アプリケーションライフサイクル管理: 開発から運用まで

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、架空の企業が、継続的な開発プロセスの一環として、テスト環境、ステージング環境、および運用環境を通じて ASP.NET web アプリケーションのデプロイを管理する方法について説明します。 トピック全体で、特定のタスクの実行方法に関する詳細情報とチュートリアルへのリンクが提供されています。
> 
> このトピックは、企業での web 展開に関する[一連のチュートリアル](deploying-web-applications-in-enterprise-scenarios.md)の概要を説明することを目的としています。 ここで&#x2014;説明するいくつかの概念を理解していない場合は、これらのすべてのタスクと手法について詳しく説明しているチュートリアルを参照してください。
> 
> > [!NOTE]
> > わかりやすくするために、このトピックでは、配置プロセスの一部としてのデータベースの更新については説明しません。 ただし、データベース機能の増分更新は、多くのエンタープライズ展開シナリオで必要とされます。この方法については、このチュートリアルシリーズの後の方で説明します。 詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。

## <a name="overview"></a>概要

ここに示すデプロイプロセスは、「[エンタープライズ Web デプロイ: シナリオの概要](enterprise-web-deployment-scenario-overview.md)」で説明されている Fabrikam, inc. のデプロイシナリオに基づいています。 このトピックを学習する前に、シナリオの概要をお読みください。 基本的に、このシナリオでは、通常のエンタープライズ環境におけるさまざまなフェーズを通じて、適度に複雑な web アプリケーション ( [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)) の展開を組織が管理する方法を確認します。

大まかに言えば、Contact Manager ソリューションは、開発とデプロイのプロセスの一部として、これらの段階を通過します。

1. 開発者は、一部のコードを Team Foundation Server (TFS) 2010 にチェックインします。
2. TFS は、コードをビルドし、チームプロジェクトに関連付けられているすべての単体テストを実行します。
3. TFS によって、ソリューションがテスト環境に配置されます。
4. 開発チームは、テスト環境でソリューションを検証し、検証します。
5. ステージング環境の管理者は、ステージング環境への "what-if" 展開を実行して、デプロイで問題が発生するかどうかを確立します。
6. ステージング環境の管理者は、ステージング環境へのライブデプロイを実行します。
7. このソリューションでは、ステージング環境でユーザー受け入れテストを実施します。
8. Web 配置パッケージは、手動で運用環境にインポートされます。

これらのステージは、継続的な開発サイクルの一部を形成します。

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

実際には、各ステージについて詳しく説明しているように、このプロセスよりも少し複雑になります。 Fabrikam, Inc. は、ターゲット環境ごとに異なるアプローチを使用して配置を行います。

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

このトピックの残りの部分では、このデプロイライフサイクルの次の主要な段階について説明します。

- **前提条件**: 配置ロジックを配置する前に、サーバーインフラストラクチャをどのように構成する必要があります。
- 最初の**開発と配置**: ソリューションを初めて配置する前に行う必要があること。
- **テストへの配置**: 開発者が新しいコードをチェックインするときに、テスト環境にコンテンツをパッケージ化して配置する方法を示します。
- **ステージング環境への配置**: ステージング環境に特定のビルドを配置する方法と、"what-if" 配置を実行して問題が発生しないようにする方法について説明します。
- **運用環境への配置**: ネットワークインフラストラクチャがリモート展開を妨げている場合に、運用環境に web パッケージをインポートする方法について説明します。

## <a name="prerequisites"></a>前提条件

配置シナリオの最初のタスクは、サーバーインフラストラクチャが展開ツールと手法の要件を満たしていることを確認することです。 この場合、Fabrikam, Inc. は、次のようなサーバーインフラストラクチャを構成しています。

- TFS は、チームプロジェクトコレクション、ビルドコントローラー、およびビルドエージェントを含めるように構成されています。 詳細については、「[自動 Web 展開の Team Foundation Server の構成](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)」を参照してください。
- テスト環境は、web Deployment Agent サービス ("リモートエージェント") を使用したリモート展開を受け入れるように構成されています。詳細については、「 [Web 配置用のテスト環境を構成](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md)する」および「 [Web 配置発行用に Web サーバーを構成する (リモートエージェント)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)」を参照してください。
- ステージング環境は、Web 配置ハンドラエンドポイントを使用したリモートデプロイを受け入れるように構成されています。「[シナリオ: Web デプロイのステージング環境の構成](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md)」および「 [Web 配置発行用の Web サーバーの構成 (Web 配置ハンドラー)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)」を参照してください。
- 運用環境は、管理者が web 配置パッケージをインターネットインフォメーションサービス (IIS) に手動でインポートできるように構成されています。詳細については、「 [Web 配置用の運用環境の構成](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md)」および「 [Web 配置発行用に Web サーバーを構成する (オフライン展開)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)」を参照してください。

## <a name="initial-development-and-deployment"></a>初期の開発と配置

Fabrikam 社の開発チームは、初めて Contact Manager ソリューションをデプロイする前に、次のタスクを実行する必要があります。

- TFS で新しいチームプロジェクトを作成します。
- 配置ロジックを含む Microsoft Build Engine (MSBuild) プロジェクトファイルを作成します。
- デプロイプロセスをトリガーする TFS ビルド定義を作成します。

### <a name="create-a-new-team-project"></a>新しいチームプロジェクトの作成

- Tfs 管理者 Walters は、「 [tfs でのチームプロジェクトの作成](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)」の説明に従って、アプリケーションの新しいチームプロジェクトを作成します。 次に、リード開発者であるのは、スケルトンソリューションを作成します。 彼は、「[ソース管理にコンテンツを追加する](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)」で説明されているように、TFS でファイルを新しいチームプロジェクトにチェックインします。

### <a name="create-the-deployment-logic"></a>配置ロジックを作成する

「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている「プロジェクトファイルの分割」の方法を使用して、さまざまなカスタム MSBuild プロジェクトファイルを作成します。 次のように作成します。

- 配置プロセスを実行する*Publish. proj*という名前のプロジェクトファイル。 このファイルには、ソリューション内のプロジェクトをビルドし、web パッケージを作成して、移行先サーバー環境にパッケージを配置する MSBuild ターゲットが含まれています。
- *Env-Dev. proj*と*env*という名前の環境固有のプロジェクトファイル。 これらの設定には、テスト環境とステージング環境に固有の設定 (接続文字列、サービスエンドポイント、web パッケージを受信するリモートサービスの詳細など) が含まれます。 特定の宛先環境に適した設定を選択するためのガイダンスについては、「[ターゲット環境の配置プロパティを構成する](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)」を参照してください。

配置を実行するには、ユーザーが MSBuild またはチームビルドを使用して発行元の*proj*ファイルを実行し、コマンドライン引数として、関連する環境固有のプロジェクトファイル (*Env*または*env*) の場所を指定します。 次に、 *Publish*ファイルは環境固有のプロジェクトファイルをインポートして、各ターゲット環境に対して発行命令の完全なセットを作成します。

> [!NOTE]
> これらのカスタムプロジェクトファイルの動作は、MSBuild を呼び出すために使用するメカニズムに依存しません。 たとえば、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、MSBuild コマンドラインを直接使用することができます。 「[配置コマンドファイルを作成して実行](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)する」の説明に従って、コマンドファイルからプロジェクトファイルを実行できます。 または、「[配置をサポートするビルド定義の作成](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)」で説明されているように、TFS のビルド定義からプロジェクトファイルを実行することもできます。  
> どちらの場合も、最終的には、&#x2014;同じ MSBuild がマージされたプロジェクトファイルを実行し、ソリューションをターゲット環境に配置します。 これにより、発行プロセスをトリガーするための柔軟性が大幅に向上します。

カスタムプロジェクトファイルを作成したら、そのファイルをソリューションフォルダーに追加し、ソース管理にチェックインします。

### <a name="create-build-definitions"></a>ビルド定義の作成

最終的な準備タスクとして、次のようにして、新しいチームプロジェクトの3つのビルド定義を作成します。

- **Deploytotest**。 これにより、Contact Manager ソリューションがビルドされ、チェックインが行われるたびに、テスト環境に配置されます。
- **Deploytostaging**。 これにより、開発者がビルドをキューに配置するときに、指定した前のビルドからステージング環境にリソースがデプロイされます。
- **Deploytostaging-WhatIf**。 これにより、開発者がビルドをキューに配置するときに、ステージング環境への "what-if" 配置が実行されます。

以下のセクションでは、これらの各ビルド定義の詳細について説明します。

## <a name="deployment-to-test"></a>テストする配置

Fabrikam, Inc. の開発チームは、テスト環境を管理して、検証と検証、ユーザビリティテスト、互換性テスト、アドホックテスト、探索的テストなど、さまざまなソフトウェアテストアクティビティを実施します。

開発チームは、 **Deploytotest**という名前の TFS でビルド定義を作成しました。 このビルド定義は継続的インテグレーショントリガーを使用します。これは、Fabrikam, Inc. の開発チームのメンバーがチェックインを実行するたびにビルドプロセスが実行されることを意味します。 ビルドがトリガーされると、ビルド定義は次のようになります。

- ContactManager .sln ソリューションをビルドします。 これにより、ソリューション内のすべてのプロジェクトがビルドされます。
- ソリューションのフォルダー構造で単体テストを実行します (ソリューションが正常にビルドされた場合)。
- 配置プロセスを制御するカスタムプロジェクトファイルを実行します (ソリューションが正常にビルドされ、単体テストが成功した場合)。

最終的には、ソリューションが正常にビルドされ、単体テストに合格すると、web パッケージとその他のデプロイリソースがテスト環境に配置されます。

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>デプロイプロセスはどのように機能しますか。

**Deploytotest**ビルド定義は、次の引数を MSBuild に提供します。

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

**Deployonbuild = true**および**deploytarget = パッケージ**のプロパティは、チームビルドがソリューション内のプロジェクトをビルドするときに使用されます。 プロジェクトが web アプリケーションプロジェクトの場合、これらのプロパティは MSBuild に対してプロジェクトの web 配置パッケージを作成するように指示します。 **TargetEnvPropsFile**プロパティは、インポートする環境固有のプロジェクトファイルを検索する場所を指定し*ます。*

> [!NOTE]
> このようなビルド定義を作成する方法の詳細なチュートリアルについては、「[配置をサポートするビルド定義の作成](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)」を参照してください。

*Publish*ファイルには、ソリューション内の各プロジェクトをビルドするターゲットが含まれています。 ただし、チームビルドでファイルを実行している場合は、これらのビルドターゲットをスキップする条件付きロジックも含まれます。 これにより、単体テストを実行する機能など、チームビルドが提供する追加のビルド機能を利用できます。 ソリューションのビルドまたは単体テストが失敗した場合、*発行の proj*ファイルは実行されず、アプリケーションは配置されません。

条件付きロジックは、 **BuildingInTeamBuild**プロパティを評価することによって実現されます。 これは、チームビルドを使用してプロジェクトをビルドするときに自動的に**true**に設定される MSBuild プロパティです。

## <a name="deployment-to-staging"></a>ステージング環境へのデプロイ

ビルドがテスト環境で開発チームのすべての要件を満たしている場合、チームは同じビルドをステージング環境に配置することができます。 ステージング環境は、通常、運用環境または "ライブ" 環境の特性 (サーバーの仕様、オペレーティングシステムとソフトウェア、ネットワーク構成など) と一致するように構成されています。 ステージング環境は、ロードテスト、ユーザー受け入れテスト、および広範な内部レビューによく使用されます。 ビルドは、ビルドサーバーから直接ステージング環境に配置されます。

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

ソリューションをステージング環境に配置するために使用されるビルド定義 ( **deploytostaging-WhatIf**および**deploytostaging**) は、次の特性を共有します。

- 実際には何もビルドしません。 渡されるソリューションをステージング環境にデプロイする場合、テスト環境で既に検証および検証済みの特定の既存のビルドを配置したいと考えています。 ビルド定義では、配置プロセスを制御するカスタムプロジェクトファイルを実行するだけで済みます。
- 渡されるビルドをトリガーする場合、ビルドパラメーターを使用して、ビルドサーバーから配置するリソースを含むビルドを指定します。
- ビルド定義は自動的にはトリガーされません。 ステージング環境にソリューションをデプロイする場合は、手動でビルドをキューに配置します。

ステージング環境へのデプロイに関する大まかなプロセスは次のとおりです。

1. ステージング環境管理者である渡 Walters は、 **Deploytostaging-WhatIf**ビルド定義を使用してビルドをキューに置いています。 渡されるビルド定義パラメーターを使用して、配置するビルドを指定します。
2. **Deploytostaging-WhatIf**ビルド定義は、"what-if" モードでカスタムプロジェクトファイルを実行します。 これにより、渡がライブデプロイを実行したかのようにログファイルが生成されますが、実際には移行先の環境が変更されることはありません。
3. 渡されるログファイルをレビューして、ステージング環境でのデプロイの影響を確認します。 具体的には、渡される内容、更新される内容、削除される内容を確認する必要があります。
4. 配置によって既存のリソースやデータに対して望ましくない変更が行われないことを確認した場合は、 **Deploytostaging**ビルド定義を使用してビルドをキューに配置します。
5. **Deploytostaging**ビルド定義は、カスタムプロジェクトファイルを実行します。 これにより、ステージング環境のプライマリ web サーバーにデプロイリソースが発行されます。
6. Web Farm Framework (WFF) コントローラーは、ステージング環境の web サーバーを同期します。 これにより、サーバーファーム内のすべての web サーバーでアプリケーションを使用できるようになります。

### <a name="how-does-the-deployment-process-work"></a>デプロイプロセスはどのように機能しますか。

**Deploytostaging**ビルド定義は、次の引数を MSBuild に提供します。

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

**TargetEnvPropsFile**プロパティは、インポートする環境固有のプロジェクトファイルを検索する場所を指定し*ます。* **Outputroot**プロパティは、組み込みの値をオーバーライドし、デプロイするリソースを含むビルドフォルダーの場所を示します。 渡がビルドをキューに置いたときに、 **[パラメーター]** タブを使用して**outputroot**プロパティの更新された値を指定します。

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> このようなビルド定義を作成する方法の詳細については、「[特定のビルドを配置](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)する」を参照してください。

**Deploytostaging-WhatIf**ビルド定義には、 **deploytostaging**ビルド定義と同じ配置ロジックが含まれています。 ただし、追加の引数**WhatIf = true**が含まれています。

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

"WhatIf *" ファイル内*では、 **WhatIf**プロパティによって、すべてのデプロイリソースが "what-if" モードで公開される必要があることが示されます。 つまり、配置が先に進んでいるかのようにログファイルが生成されますが、移行先の環境では実際には何も変更されません。 これにより、提案された展開&#x2014;の影響、特に何が追加されるか、何が更新されるか、&#x2014;および実際に変更を行う前に何が削除されるかを評価できます。

> [!NOTE]
> "What-if" 展開を構成する方法の詳細については、「 ["What If" 展開の実行](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)」を参照してください。

ステージング環境でプライマリ web サーバーにアプリケーションをデプロイすると、WFF はサーバーファーム内のすべてのサーバー間でアプリケーションを自動的に同期します。

> [!NOTE]
> Web サーバーを同期するように WFF を構成する方法の詳細については、「 [Web ファームフレームワークを使用したサーバーファームの作成](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)」を参照してください。

## <a name="deployment-to-production"></a>運用環境への配置

ステージング環境でビルドが承認されると、Fabrikam, Inc. チームはアプリケーションを運用環境に発行できます。 運用環境では、アプリケーションが "ライブ" になり、エンドユーザーの対象ユーザーに到達します。

運用環境は、インターネットに接続された境界ネットワーク内にあります。 これは、ビルドサーバーを含む内部ネットワークから分離されています。 実稼働環境管理者 (根本アンドリュース) は、web 配置パッケージをビルドサーバーから手動でコピーし、プライマリ運用 web サーバー上の IIS にインポートする必要があります。

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

これは、運用環境へのデプロイの大まかなプロセスです。

1. 開発チームは、ビルドを運用環境にデプロイする準備ができていることを知らせるものとします。 チームは、ビルドサーバーのドロップフォルダー内にある web 配置パッケージの場所を根本とします。
2. リサは、ビルドサーバーから web パッケージを収集し、運用環境のプライマリ web サーバーにコピーします。
3. リサは、IIS マネージャーを使用して、プライマリ web サーバー上に web パッケージをインポートおよび発行します。
4. WFF コントローラーは、運用環境の web サーバーを同期します。 これにより、サーバーファーム内のすべての web サーバーでアプリケーションを使用できるようになります。

### <a name="how-does-the-deployment-process-work"></a>デプロイプロセスはどのように機能しますか。

IIS マネージャーには、IIS web サイトへの web パッケージの発行を容易にする、アプリケーションパッケージのインポートウィザードが含まれています。 この手順を実行する方法のチュートリアルについては、「 [Web パッケージを手動でインストール](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)する」を参照してください。

## <a name="conclusion"></a>まとめ

このトピックでは、一般的なエンタープライズ規模の web アプリケーションのデプロイライフサイクルについて説明しました。

このトピックでは、web アプリケーションの展開のさまざまな側面に関するガイダンスを提供する一連のチュートリアルの一部を示します。 実際には、デプロイプロセスの各段階で、追加のタスクと考慮事項が多数あり、それらをすべて1つのチュートリアルで説明することはできません。 詳細については、次のチュートリアルを参照してください。

- [企業の Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 このチュートリアルでは、MSBuild と IIS Web 配置ツール (Web 配置) を使用した web 配置手法の概要について説明します。
- [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 このチュートリアルでは、さまざまな展開シナリオをサポートするように Windows server 環境を構成する方法について説明します。
- [自動 Web 展開用に Team Foundation Server を構成して](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)います。 このチュートリアルでは、配置ロジックを TFS ビルドプロセスに統合する方法について説明します。
- [高度なエンタープライズ Web デプロイ](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 このチュートリアルでは、組織が直面する複雑な展開の課題をいくつか満たす方法について説明します。

> [!div class="step-by-step"]
> [[戻る]](enterprise-web-deployment-scenario-overview.md)
