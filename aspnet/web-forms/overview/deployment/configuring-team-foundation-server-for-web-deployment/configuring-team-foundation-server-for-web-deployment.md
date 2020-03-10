---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: Web 配置用の Team Foundation Server の構成 |Microsoft Docs
author: jrjlee
description: このチュートリアルでは、Team Foundation Server (TFS) 2010 を構成して、ソリューションをビルドし、さまざまなターゲット環境に web コンテンツをデプロイする方法について説明します。 これ。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424204"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>Web 配置の Team Foundation Server を構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このチュートリアルでは、Team Foundation Server (TFS) 2010 を構成して、ソリューションをビルドし、さまざまなターゲット環境に web コンテンツをデプロイする方法について説明します。 これには、開発者が変更を行うたびにコンテンツが自動的に配置される継続的インテグレーション (CI) シナリオが含まれます。 また、ビルドがテスト環境で検証および検証された後に、管理者が特定のビルドの配置をステージング環境にトリガーする必要がある場合に、手動のトリガーシナリオを含めることもできます。 このチュートリアルのトピックでは、次のような構成プロセス全体について説明します。
> 
> - TFS で新しいチームプロジェクトを作成する方法。
> - ソース管理にコンテンツを追加する方法。
> - CI と配置をサポートするようにビルドサーバーを構成する方法。
> - 配置ロジックを含むビルド定義を作成する方法。
> - 自動展開のためのアクセス許可を構成する方法。
> 
> これらのチュートリアルのイタリア語翻訳については、 [http://www.lucamorelli.it](http://www.lucamorelli.it)を参照してください。

このチュートリアルでは、TFS 2010 をインストールし、初期構成プロセスの一環としてチームプロジェクトコレクションを作成していることを前提としています。 [Visual Studio 2010 の Team Foundation インストールガイド](https://go.microsoft.com/?linkid=9805132)では、これらのタスクに関する包括的なガイダンスを提供しています。

## <a name="context"></a>Context

これは、Fabrikam, Inc. という架空の会社のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部となります。このチュートリアルシリーズでは、&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ソリューション&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「ビルド[プロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法に基づいて&#x2014;います。この方法では、ビルドプロセスは、各配置先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="scenario-overview"></a>シナリオの概要

これらのチュートリアルの高度なシナリオについては、「[エンタープライズ Web 配置: シナリオの概要](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」を参照してください。 このチュートリアルを開始する前に、このトピックを確認することをお勧めします。

## <a name="how-to-use-this-tutorial"></a>このチュートリアルの使用方法

このチュートリアルで説明されているタスクを初めて実行する場合、またはサンプルソリューションを使用して例を実行する場合は、チュートリアルのトピックを順番に実行する必要があります。 または、個々のトピックを特定のタスクのガイダンスとして使用することもできます。 このチュートリアルには、次のトピックが含まれています。

- [TFS でチームプロジェクトを作成する](creating-a-team-project-in-tfs.md)。 チームプロジェクトは、ソース管理、プロセス管理、および TFS でのビルドのコア単位です。 ソース管理にコンテンツを追加したり、ビルド定義を作成したりする前に、チームプロジェクトを作成する必要があります。
- [ソース管理にコンテンツを追加](adding-content-to-source-control.md)しています。 チームプロジェクトを作成したら、ソース管理へのコンテンツの追加を開始できます。 ビルドの構成を開始する前に、プロジェクトとソリューションを外部の依存関係と共に追加する必要があります。
- [Web 配置用に TFS ビルドサーバーを構成](configuring-a-tfs-build-server-for-web-deployment.md)する。 チームプロジェクトのコンテンツをビルドする場合は、ビルドサーバーを構成する必要があります。 ほとんどの場合、これは TFS インストールとは別のコンピューターに配置する必要があります。 ビルドサーバーを構成するには、TFS ビルドサービスのインストールと構成、Visual Studio 2010 のインストール、ビルドコントローラーとビルドエージェントの作成、コードが正常にビルドされるために必要な製品またはコンポーネントのインストール、およびをインストールする必要があります。インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置)。
- [配置をサポートするビルド定義を作成](creating-a-build-definition-that-supports-deployment.md)する。 TFS でのビルドのキューまたはトリガーを開始する前に、チームプロジェクトのビルド定義を少なくとも1つ作成する必要があります。 ビルド定義では、ビルドに含める必要があるもの、ビルドをトリガーする必要があるもの、ビルド出力をチームビルドが送信する場所など、ビルドのすべての側面を定義します。 ビルド定義を構成して、カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを実行することができます。これにより、自動ビルドに配置ロジックを含めることができます。
- [特定のビルドを配置](deploying-a-specific-build.md)します。 多くのシナリオでは、最新のビルドではなく、特定のビルドをターゲット環境に配置する必要があります。 この場合、特定のドロップフォルダーからコンテンツを展開するビルド定義を構成できます。
- [チームビルド配置のアクセス許可を構成して](configuring-permissions-for-team-build-deployment.md)います。 ビルドサービスが自動ビルドプロセスの一部としてコンテンツを配置する場合は、任意の送信先 web サーバーおよびデータベースサーバーのビルドサービスアカウントにさまざまなアクセス許可を付与する必要があります。

## <a name="key-technologies"></a>主要テクノロジ

このチュートリアルでは、これらの製品とテクノロジを使用して、自動化されたビルドと web 配置をサポートする方法について説明します。

- Visual Studio Team Foundation Server 2010
- チームビルドと MSBuild
- Web デプロイ

このチュートリアルでは、Windows Server 2008 R2、IIS 7.5、SQL Server 2008 R2、ASP.NET 4.0、ASP.NET MVC 3 の使用についても取り上げています。

## <a name="other-tutorials-in-this-series"></a>このシリーズの他のチュートリアル

これは、エンタープライズ規模の web デプロイに関する一連の5つのチュートリアルの一部です。 このシリーズの他のチュートリアルは次のとおりです。

- [エンタープライズシナリオでの Web アプリケーションの展開](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 この入門用コンテンツでは、チュートリアルシリーズのコンテキストの背景を提供しています。 このチュートリアルでは、チュートリアルシナリオについて説明し、シリーズ全体で説明されているタスクとチュートリアルが、より広範なアプリケーションライフサイクル管理 (ALM) プロセスにどのように適合するかを示します。
- [企業の Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 このチュートリアルでは、MSBuild プロジェクトファイル、Web 発行パイプライン (WPP)、Web 配置、およびその他の関連テクノロジについて概念的に説明します。 これらのツールを組み合わせて使用して、複雑な展開プロセスを管理する方法について説明します。
- [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 このチュートリアルでは、Web Deployment Agent サービス (リモートエージェント) を使用したリモート web パッケージの展開や、Web 配置ハンドラーとリモートデータベースの配置など、さまざまな展開シナリオをサポートするように Windows サーバーを構成する方法について説明します。 独自の環境に適した配置方法を選択するためのガイダンスを提供します。また、Web Farm Framework (WFF) を使用して、サーバーファーム内のすべての web サーバーに配置された web アプリケーションをレプリケートする方法についても説明します。
- [高度なエンタープライズ Web デプロイ](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 このチュートリアルでは、複数の環境でのデータベース配置のカスタマイズ、展開からのファイルとフォルダーの除外、展開プロセス中の web アプリケーションのオフライン化など、さまざまな高度な展開タスクを実行する方法について説明します.

> [!div class="step-by-step"]
> [Next](creating-a-team-project-in-tfs.md)
