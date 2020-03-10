---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Visual Studio 2010 を使用したエンタープライズシナリオでの Web アプリケーションのデプロイ | |Microsoft Docs
author: jrjlee
description: この一連のチュートリアルでは、さまざまなエンタープライズシナリオで web アプリケーションをデプロイするために使用できるツールと手法について説明します。 最適な使用方法について説明します。
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463432"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>Visual Studio 2010 を利用し、エンタープライズ シナリオで Web アプリケーションを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> この一連のチュートリアルでは、さまざまなエンタープライズシナリオで web アプリケーションをデプロイするために使用できるツールと手法について説明します。 ここでは、Visual Studio 2010、Microsoft Build Engine (MSBuild)、インターネットインフォメーションサービス (IIS) 7.5、IIS Web 配置ツール (Web 配置)、Web Farm Framework (WFF)、および VSDBCMD などのユーティリティを使用して、次のようなテクノロジを最大限に活用する方法について説明します。デプロイプロセスを簡素化し、管理します。 これには、次のことを支援する概念的な概要とタスク指向のガイダンスが含まれています。
> 
> - エンタープライズ規模の web アプリケーションのデプロイ要件を確認して確立します。
> - テスト、ステージング、および運用 web サーバー環境を構成して、web 配置をサポートします。
> - 自動 web デプロイをサポートするように Team Foundation Server (TFS) の継続的インテグレーション (CI) プロセスを構成します。
> - さまざまな要件や制限があるさまざまなサーバー環境に、エンタープライズ規模の web アプリケーションをデプロイします。
> - 異なるサーバー環境で実行されている web アプリケーションに変更を配置します。
> 
> > [!NOTE]
> > これらのチュートリアルでは、TFS を CI サーバーとして使用する方法について説明しますが、ガイダンスは任意の CI サーバーに簡単に応用できます。 チュートリアルを理解して活用するために、TFS に関する詳細な知識は必要ありません。
> 
> 
> これらのチュートリアルのイタリア語翻訳については、 [http://www.lucamorelli.it](http://www.lucamorelli.it)を参照してください。

## <a name="about-the-authors"></a>作成者について

Jason Lee は、Microsoft の製品やテクノロジ (特に SharePoint と ASP.NET) を数年間操作した[コンテンツマスタ](http://www.contentmaster.com/)を持つ主要技術者です。 Jason は、コンピューティングの博士号を保持し、現在は MCPD および MCTS 認定を受けています。 Jason のテクニカルブログは、 [www.jrjlee.com](http://www.jrjlee.com/)で読むことができます。

Benjamin は、彼のキャリアに、ホワイトペーパー、SDK ドキュメント、PowerPoint プレゼンテーション、およびインストラクター主導のオンライントレーニングコースを執筆した[コンテンツマスタ](http://www.contentmaster.com/)を持つ主要技術者です。 ASP.NET ドキュメントチームの元のメンバーは、10年以上にわたって Microsoft の web テクノロジを使用しました。

## <a name="target-audience"></a>対象読者

この一連のチュートリアルは、Visual Studio 2010 を使用してエンタープライズ規模の web アプリケーションを作成する ASP.NET web アプリケーション開発者およびソリューションアーキテクトを対象としています。 コンテンツから最大限の価値を得るには、Visual Studio 2010 を使い慣れており、TFS に関する基本的な知識を持ち、ASP.NET MVC 3、Windows Communication Foundation (WCF)、IIS、SQL などの Microsoft web platform テクノロジを認識している必要があります。サーバーと Visual Studio データベースプロジェクト。 ただし、展開ツールやテクノロジについて理解している必要はなく、CI システムを設定する方法を知っておく必要もありません。

## <a name="requirements"></a>必要条件

チュートリアルに従って、これらのチュートリアルで説明されているタスクを実行するには、開発用コンピューターにこのソフトウェアをインストールする必要があります。

- Visual Studio 2010 Premium または Ultimate Edition Service Pack 1
- .NET Framework 4.0
- .NET Framework 3.5 Service Pack 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

これらのチュートリアルで説明されている配置手順を実行するには、サンプルの Web アプリケーション配置環境にアクセスする必要があります。 最良の結果を得るために、これらの環境は組織のエンタープライズ展開パターンを反映する必要があります。 その後、このドキュメントに記載されているチュートリアルを変更して、組織の展開環境と要件を反映することができます。

## <a name="series-contents"></a>系列の内容

この概要セクションは、2つのトピックで構成されています。 これらは、次のチュートリアルのための広範なコンテキストを提供するように設計されています。

- [エンタープライズ Web 展開: シナリオの概要](enterprise-web-deployment-scenario-overview.md)。 このトピックでは、このシリーズの各チュートリアルを過小にピン留めするシナリオについて説明します。 このシナリオでは、エンタープライズ規模の web アプリケーションを開発するため、Fabrikam, Inc. という架空の会社のアプリケーションライフサイクル管理 (ALM) 要件に焦点を当てています。
- [アプリケーションライフサイクル管理: 開発から運用まで](application-lifecycle-management-from-development-to-production.md)。 このトピックでは、デプロイプロセスの概要とエンドツーエンドの概要について説明します。 Fabrikam, Inc. が、継続的な開発プロセスの一環として、テスト環境、ステージング環境、および運用環境を通じて、エンタープライズ規模の ASP.NET web アプリケーションを移行する方法を示します。

このシリーズには、4つのチュートリアルセットが含まれています。 それぞれが、web 配置のさまざまな側面に焦点を当てています。

- [企業の Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 このチュートリアルでは、MSBuild プロジェクトファイル、Web 発行パイプライン、Web 配置、およびその他の関連テクノロジについて概念的に説明します。 これらのツールを組み合わせて使用して、複雑な展開プロセスを管理する方法について説明します。
- [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 このチュートリアルでは、Web Deployment Agent サービス ("リモートエージェント") を使用したリモート web パッケージの展開や、Web 配置ハンドラーとリモートデータベースの配置など、さまざまな展開シナリオをサポートするように Windows サーバーを構成する方法について説明します。 独自の環境に適した配置方法を選択するためのガイダンスを提供します。また、WFF を使用して、サーバーファーム内のすべての web サーバーにデプロイされた web アプリケーションをレプリケートする方法についても説明します。
- [Web 配置の Team Foundation Server を構成して](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)います。 このチュートリアルでは、CI プロセスの一部としての自動デプロイ、特定のビルドの手動による配置など、さまざまな配置シナリオをサポートするように TFS を構成する方法について説明します。
- [高度なエンタープライズ Web デプロイ](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 このチュートリアルでは、複数の環境でのデータベース配置のカスタマイズ、展開からのファイルとフォルダーの除外、展開プロセス中の web アプリケーションのオフライン化など、さまざまな高度な展開タスクを実行する方法について説明します.

## <a name="where-to-start"></a>開始する場所

この一連のチュートリアルでは、架空のエンタープライズ展開シナリオと共に、現実的な複雑さレベルのサンプルソリューションを使用して、参照実装を提供し、タスクとチュートリアルに共通のコンテキストを提供します。 次のトピック「[エンタープライズ Web 配置: シナリオの概要](enterprise-web-deployment-scenario-overview.md)」では、シナリオとサンプルソリューションについて説明します。 そこから、お客様のニーズに最も合ったチュートリアルとトピックを利用できます。

> [!div class="step-by-step"]
> [Next](enterprise-web-deployment-scenario-overview.md)
