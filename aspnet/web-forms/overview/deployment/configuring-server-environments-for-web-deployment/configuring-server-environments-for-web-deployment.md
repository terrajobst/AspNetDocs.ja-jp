---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: Web 配置用のサーバー環境の構成 |Microsoft Docs
author: jrjlee
description: このチュートリアルでは、1回のクリックで、または自動化された web サイトのデプロイと発行をサポートするようにサーバー環境を設定する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515116"
---
# <a name="configuring-server-environments-for-web-deployment"></a>Web 配置のサーバー環境を構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このチュートリアルでは、さまざまなシナリオで、1回のクリックで、または自動化された web サイトのデプロイと発行をサポートするようにサーバー環境を設定する方法について説明します。 このチュートリアルでは、web サーバーを構成して、Web Farm Framework (WFF) サーバーファームを展開するための特定の方法をサポートするように web サーバーを構成するなど、さまざまなタスクを実行する方法について説明します。より高度なエンドツーエンドのガイダンス。
> 
> このチュートリアルでは、「[エンタープライズ Web デプロイ: シナリオの概要](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」で説明した Fabrikam, inc. のデプロイシナリオを例とネットワークインフラストラクチャの参照ポイントとして使用します。
> 
> これらのチュートリアルのイタリア語翻訳については、 [http://www.lucamorelli.it](http://www.lucamorelli.it)を参照してください。

このチュートリアルには、次のトピックが含まれています。

- [適切な Web 展開手法を選択する](choosing-the-right-approach-to-web-deployment.md)
- [シナリオ: Web 展開のテスト環境を構成する](scenario-configuring-a-test-environment-for-web-deployment.md)
- [シナリオ: Web 展開のステージング環境を構成する](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [シナリオ: Web 展開の運用環境を構成する](scenario-configuring-a-production-environment-for-web-deployment.md)
- [Web 配置発行の Web サーバーを構成する (リモート エージェント)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [Web 配置発行の Web サーバーを構成する (Web 配置ハンドラー)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [Web 配置発行の Web サーバーを構成する (オフライン展開)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [Web 配置発行のデータベース サーバーを構成する](configuring-a-database-server-for-web-deploy-publishing.md)
- [Web Farm Framework でサーバー ファームを作成する](creating-a-server-farm-with-the-web-farm-framework.md)
- [ターゲット環境の展開プロパティを構成する](configuring-deployment-properties-for-a-target-environment.md)

最初のトピック「 [Web 配置に適切な方法を選択](choosing-the-right-approach-to-web-deployment.md)する」では、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) 2.0 を使用して web アプリケーションを公開するために使用できる主な方法について説明します。 また、各アプローチにマップされるシナリオも特定します。 ここから、各シナリオトピックでは、完了する必要があるタスクの概要を説明し、これらのタスクを完了するために必要なトピックを示します。

「ソリューションをビルドして配置するための[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法を使用している場合、最後のトピック「[ターゲット環境の配置プロパティの構成](configuring-deployment-properties-for-a-target-environment.md)」では、異なる配置先環境に配置するために環境固有のプロジェクトファイルを構成する方法について説明します。

## <a name="key-technologies"></a>主要テクノロジ

このチュートリアルでは、これらの製品とテクノロジを使用して、web 配置をサポートする方法を中心に説明します。

- IIS 7.5
- Web 配置2.x
- WFF 2.x
- IIS Web 管理サービス (WMSvc)

このチュートリアルでは、Windows Server 2008 R2、SQL Server 2008 R2、ASP.NET 4.0、ASP.NET MVC 3 の使用についても取り上げています。

## <a name="other-tutorials-in-this-series"></a>このシリーズの他のチュートリアル

これは、エンタープライズ規模の web デプロイに関する一連の5つのチュートリアルの一部です。 このシリーズの他のチュートリアルは次のとおりです。

- [エンタープライズシナリオでの Web アプリケーションの展開](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 この入門用コンテンツでは、チュートリアルシリーズのコンテキストの背景を提供しています。 このチュートリアルでは、チュートリアルシナリオについて説明し、シリーズ全体で説明されているタスクとチュートリアルが、より広範なアプリケーションライフサイクル管理 (ALM) プロセスにどのように適合するかを示します。
- [企業の Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 このチュートリアルでは、Microsoft Build Engine (MSBuild) プロジェクトファイル、Web 発行パイプライン、Web 配置、およびその他の関連テクノロジについて概念的に説明します。 これらのツールを組み合わせて使用して、複雑な展開プロセスを管理する方法について説明します。
- [Web 配置の Team Foundation Server を構成して](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)います。 このチュートリアルでは、Team Foundation Server (TFS) を構成して、継続的インテグレーション (CI) プロセスの一部としての自動展開、特定のビルドの手動による配置など、さまざまな展開シナリオをサポートする方法について説明します。
- [高度なエンタープライズ Web デプロイ](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 このチュートリアルでは、複数の環境でのデータベース配置のカスタマイズ、展開からのファイルとフォルダーの除外、展開プロセス中の web アプリケーションのオフライン化など、さまざまな高度な展開タスクを実行する方法について説明します.

> [!div class="step-by-step"]
> [Next](choosing-the-right-approach-to-web-deployment.md)
