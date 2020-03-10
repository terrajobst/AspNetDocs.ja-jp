---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 'シナリオ: Web デプロイのステージング環境を構成する |Microsoft Docs'
author: jrjlee
description: このトピックでは、ステージング環境の一般的な web 配置シナリオについて説明し、同様の env を設定するために完了する必要があるタスクについて説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518008"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>シナリオ: Web 配置用のステージング環境の構成

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、ステージング環境の一般的な web 配置シナリオについて説明し、同様の環境をセットアップするために完了する必要があるタスクについて説明します。

多くの組織では、ステージング環境を使用して、web アプリケーションまたは web サイトの更新をプレビューしています。 これにより、組織内のメンバーは、サイトが "運用" される前に新しい機能やコンテンツを探索して確認できるようになります。また、その他の場合は、運用環境に展開されます。 ステージング環境は、実稼働環境を可能な限り忠実にレプリケートするように設計されており、現実的なプレビューを提供します。 通常、この種類のステージング環境には次の特性があります。

- この環境は、負荷分散された複数の web サーバーと1つ以上のデータベースサーバーで構成されます。多くの場合、フェールオーバークラスタリングとデータベースミラーリングがあります。
- アプリケーションは、開発チームによって手動で配置することも、チームビルドサーバーによって自動的に配置することもできます。
- アプリケーションを展開するユーザーまたはプロセスアカウントは、ステージングサーバーに対する管理者特権を持っていない可能性があります。
- アプリケーションに対する変更は頻繁に配置されるため、環境は単一ステップまたは自動のデプロイをサポートする必要があります。

> [!NOTE]
> 複数のサーバーにまたがるデータベースの配置をスケールアウトする方法については、このチュートリアルでは扱いません。 この領域の詳細については、 [SQL Server オンラインブック](https://technet.microsoft.com/library/ms130214.aspx)を参照してください。

たとえば、このチュートリアルの[シナリオ](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)では、TEAM FOUNDATION SERVER (TFS) が Contact Manager ソリューションを管理します。 TFS 管理者である渡 Walters は、開発者が必要に応じてステージング環境へのデプロイをトリガーできるビルド定義を作成しました。

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

ほとんどの場合、必ずしも最新のビルドをステージング環境に配置する必要はありません。 代わりに、テスト環境で検証と検証を行っている特定のビルドを配置する方がはるかに多くなります。

## <a name="solution-overview"></a>ソリューションの概要

このシナリオでは、次のような展開要件を分析して、これらの事実を推測できます。

- デプロイを実行するユーザーまたはプロセスアカウントには、ステージングサーバーに対する管理者特権がないため、ステージング web サーバーは管理者以外の展開をサポートする必要があります。 そのため、リモートエージェントではなく、Web 配置ハンドラーを使用するようにステージング web サーバーを構成する必要があります。
- ステージング環境には複数の web サーバーが含まれていますが、1回のクリックまたは自動配置をサポートする必要があるため、サーバーファームを作成するには Web Farm Framework (WFF) を使用する必要があります。 この方法を使用すると、アプリケーションを1つの web サーバー (プライマリサーバー) に配置できます。 WFF は、ステージング環境内の他のすべての web サーバー上でデプロイをレプリケートします。
- 配置を実行するユーザーまたはプロセスアカウントには、データベースを作成するためのアクセス許可が必要です。 そのため、リモートアクセスと配置をサポートするようにデータベースサーバーを構成するだけでなく、データベースサーバーの**dbcreator**サーバーロールにアカウントを追加する必要があります。

これらのトピックでは、これらのタスクを完了するために必要なすべての情報を提供します。

- [Web ファームフレームワークを使用してサーバーファームを作成](creating-a-server-farm-with-the-web-farm-framework.md)します。 このトピックでは、WFF を使用してサーバーファームを作成および構成する方法について説明します。これにより、web platform 製品とコンポーネント、構成設定、および web サイトとアプリケーションが、負荷分散された複数の web サーバー間でレプリケートされます。
- [Web 配置公開用に Web サーバーを構成します (Web 配置ハンドラー)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 このトピックでは、Windows Server 2008 R2 のクリーンビルドから開始するリモートエージェントアプローチを使用した Web 配置の発行をサポートする web サーバーを構築する方法について説明します。
- [Web 配置パブリッシング用にデータベースサーバーを構成](configuring-a-database-server-for-web-deploy-publishing.md)します。 このトピックでは、SQL Server 2008 R2 の既定のインストールから開始して、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する方法について説明します。

## <a name="further-reading"></a>参考資料

一般的な開発者テスト環境の構成に関するガイダンスについては、「[シナリオ: Web 配置用のテスト環境の構成](scenario-configuring-a-test-environment-for-web-deployment.md)」を参照してください。 一般的な運用環境の構成に関するガイダンスについては、「[シナリオ: Web 配置用の運用環境の構成](scenario-configuring-a-production-environment-for-web-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](scenario-configuring-a-test-environment-for-web-deployment.md)
> [次へ](scenario-configuring-a-production-environment-for-web-deployment.md)
