---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 'シナリオ: Web 配置用のテスト環境の構成 |Microsoft Docs'
author: jrjlee
description: このトピックでは、開発者またはテスト環境の一般的な web 配置シナリオについて説明し、si を設定するために完了する必要があるタスクについて説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517984"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>シナリオ: Web 配置用のテスト環境の構成

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、開発者またはテスト環境の一般的な web 配置シナリオについて説明し、同様の環境をセットアップするために完了する必要があるタスクについて説明します。

開発者が web アプリケーションを操作する場合、多くの場合、開発者はサーバー環境にアクセスして、実際の設定でアプリケーションに対する変更をテストすることができます。 通常、この種の開発環境またはテスト環境には、次の特性があります。

- この環境は、1台の web サーバーと1つのデータベースサーバーで構成されます。
- 開発者は、通常、サーバーに対する管理者特権を持っているため、環境をアプリケーションの要件に合わせて構成できます。
- アプリケーションに対する変更は頻繁に配置されるため、環境は単一ステップまたは自動のデプロイをサポートする必要があります。

たとえば、このチュートリアルの[シナリオ](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)では、"Fabrikam, inc." の開発者は、Contact Manager ソリューションを使用しており、定期的に変更をテスト環境にデプロイする必要があります。 は、テスト web サーバーとテストデータベースサーバーの管理者です。 最初は、このソリューションをテスト環境に直接配置できる必要があります。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

作業の進行状況と開発者がチームに参加すると、Contact Manager ソリューションは Team Foundation Server (TFS) の継続的インテグレーション (CI) 用に構成されます。 開発者がコンテンツをチェックインするたびに、チームビルドはソリューションをビルドし、単体テストを実行して、ソリューションをテスト環境に自動的に配置する必要があります。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>ソリューションの概要

テスト環境では、リモートコンピューターからの単一ステップまたは自動の展開をサポートする必要があるため、2つの主要なアプローチを選択できます。 次のようにすることができます。

- Web Deployment Agent サービス ("リモートエージェント") を使用した配置をサポートするようにテスト web サーバーを構成します。
- Web 配置ハンドラーを使用した配置をサポートするようにテスト web サーバーを構成します。

> [!NOTE]
> [必要に応じて Web 配置](https://technet.microsoft.com/library/ee517345(WS.10).aspx)("一時エージェント") を使用することもできます。 これは、要件と制約に関して、リモートエージェントのアプローチに似ています。

この場合、開発者には移行先サーバーに対する管理者特権があり、テスト環境には厳密なセキュリティ制約は適用されません。したがって、リモートエージェントを使用した配置をサポートするようにテスト web サーバーを構成することをお勧めします。 これはあまり複雑ではなく、Web 配置ハンドラーのアプローチよりも初期構成が少なくて済むことが必要です。 また、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する必要もあります。

これらのトピックでは、これらのタスクを完了するために必要なすべての情報を提供します。

- [Web 配置パブリッシング (リモートエージェント) 用に Web サーバーを構成](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)します。 このトピックでは、Windows Server 2008 R2 のクリーンビルドから開始するリモートエージェントアプローチを使用した Web 配置の発行をサポートする web サーバーを構築する方法について説明します。
- [Web 配置パブリッシング用にデータベースサーバーを構成](configuring-a-database-server-for-web-deploy-publishing.md)します。 このトピックでは、SQL Server 2008 R2 の既定のインストールから開始して、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する方法について説明します。

## <a name="further-reading"></a>参考資料

一般的なステージング環境の構成に関するガイダンスについては、「[シナリオ: Web デプロイのステージング環境を構成](scenario-configuring-a-staging-environment-for-web-deployment.md)する」を参照してください。 一般的な運用環境の構成に関するガイダンスについては、「[シナリオ: Web 配置用の運用環境の構成](scenario-configuring-a-production-environment-for-web-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](choosing-the-right-approach-to-web-deployment.md)
> [次へ](scenario-configuring-a-staging-environment-for-web-deployment.md)
