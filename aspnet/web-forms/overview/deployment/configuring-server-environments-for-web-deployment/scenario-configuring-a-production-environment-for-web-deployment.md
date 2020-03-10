---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 'シナリオ: Web 配置用の運用環境の構成 |Microsoft Docs'
author: jrjlee
description: このトピックでは、運用環境の一般的な web 配置シナリオについて説明し、同様の手順を実行するために完了する必要のあるタスクについて説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515932"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>シナリオ: Web 配置用の運用環境の構成

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、運用環境の一般的な web 配置シナリオについて説明し、同様の環境を設定するために完了する必要があるタスクについて説明します。

運用環境は、web アプリケーションまたは web サイトの最終的な保存先です。 この時点で、アプリケーションはテストを経て、ステージング環境に配置され、"稼働可能" にする準備が整いました。 運用環境の特性は、web コンテンツの性質と目的、組織の規模、対象ユーザー、その他多くの要因によって大きく異なる場合があります。 企業規模のシナリオでは、運用環境には次の特性があります。

- この環境は、負荷分散された複数の web サーバーと1つ以上のデータベースサーバーで構成されます。多くの場合、フェールオーバークラスタリングとデータベースミラーリングがあります。
- 環境がインターネットに接続されている場合は、内部ネットワークから分離されている可能性があります。 境界ネットワーク内の別のサブネット上にある場合もあれば、別のドメインにある場合もあれば、まったく別のネットワークインフラストラクチャ上にある場合もあります。
- 開発者やビルドサーバープロセスアカウントは、実稼働サーバーで管理者特権を持つことはほとんどありません。
- アプリケーションに対する変更は、テストまたはステージングのデプロイよりも頻度が低くなります。

> [!NOTE]
> 複数のサーバーにまたがるデータベースの配置をスケールアウトする方法については、このチュートリアルでは扱いません。 この領域の詳細については、 [SQL Server オンラインブック](https://technet.microsoft.com/library/ms130214.aspx)を参照してください。

たとえば、このチュートリアルの[シナリオ](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)では、チームビルドサーバーには、ユーザーが Contact Manager ソリューションを構築し、1回の手順でステージング環境にデプロイできるビルド定義が含まれています。 アプリケーションを実稼働環境に展開する準備ができたら、セキュリティ要件とネットワークインフラストラクチャによって課される制約により、運用環境の管理者は web パッケージを運用 web サーバーに手動でコピーしてインポートする必要があります。これはインターネットインフォメーションサービス (IIS) マネージャーを介して行われます。

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>ソリューションの概要

このシナリオでは、次のような展開要件を分析して、これらの事実を推測できます。

- セキュリティの制限とネットワーク構成により、1回のクリックまたは自動の展開をサポートするように運用環境を構成することはできません。 このシナリオでは、オフライン展開が唯一の方法です。
- 運用環境には複数の web サーバーが含まれているため、Web Farm Framework (WFF) を使用してサーバーファームを作成できます。 この方法を使用すると、管理者はアプリケーションを1つの web サーバー (プライマリサーバー) にインポートするだけで、運用環境の他のすべての web サーバー上に配置がレプリケートされます。

これらのトピックでは、これらのタスクを完了するために必要なすべての情報を提供します。

- [Web ファームフレームワークを使用してサーバーファームを作成](configuring-a-database-server-for-web-deploy-publishing.md)します。 このトピックでは、WFF を使用してサーバーファームを作成および構成する方法について説明します。これにより、web platform 製品とコンポーネント、構成設定、および web サイトとアプリケーションが、負荷分散された複数の web サーバー間でレプリケートされます。
- [Web 配置公開用に Web サーバーを構成する (オフライン展開)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 このトピックでは、Windows Server 2008 R2 のクリーンビルドから開始して、管理者が web パッケージを手動でインポートして展開できる web サーバーを構築する方法について説明します。
- [Web 配置パブリッシング用にデータベースサーバーを構成](configuring-a-database-server-for-web-deploy-publishing.md)します。 このトピックでは、SQL Server 2008 R2 の既定のインストールから開始して、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する方法について説明します。

## <a name="further-reading"></a>参考資料

一般的な開発者テスト環境の構成に関するガイダンスについては、「[シナリオ: Web 配置用のテスト環境の構成](scenario-configuring-a-test-environment-for-web-deployment.md)」を参照してください。 一般的なステージング環境の構成に関するガイダンスについては、「[シナリオ: Web デプロイのステージング環境を構成](scenario-configuring-a-staging-environment-for-web-deployment.md)する」を参照してください。

> [!div class="step-by-step"]
> [前へ](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [次へ](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
