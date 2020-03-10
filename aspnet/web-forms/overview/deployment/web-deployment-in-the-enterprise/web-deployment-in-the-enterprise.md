---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Enterprise | での Web デプロイMicrosoft Docs
author: jrjlee
description: このチュートリアルでは、エンタープライズ規模の web アプリケーションの devel への展開を管理するときに発生する多くの課題を満たす方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509716"
---
# <a name="web-deployment-in-the-enterprise"></a>エンタープライズの Web 配置

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このチュートリアルでは、エンタープライズ規模の web アプリケーションの開発、テスト、ステージング、および運用環境への展開を管理する際に発生する多くの課題を満たす方法について説明します。 このチュートリアルでは、さまざまな一般的なタスクと手順を説明するために、概念とタスク指向のコンテンツを組み合わせた参照ソリューションを紹介します。
> 
> これらのチュートリアルのイタリア語翻訳については、 [http://www.lucamorelli.it](http://www.lucamorelli.it)を参照してください。

## <a name="enterprise-deployment-challenges"></a>エンタープライズ展開の課題

組織は、複雑なエンタープライズ規模のソリューションのデプロイを管理する場合に、次のような課題に直面することがよくあります。

- 開発者やテスト環境、ステージングプラットフォーム、実稼働サーバーなど、複数の環境にプロジェクトを配置できる必要があります。 ソリューションは、環境ごとに異なる構成設定を使用して展開する必要があります。
- 単一ステップまたは自動化されたビルドおよび配置プロセスの一環として、複数の依存プロジェクトを同時に配置する必要があります。
- 自動プロセスから展開を促進できる必要があります。 たとえば、継続的インテグレーション (CI) プロセスを使用して、新しいコードがチェックインされたときに web アプリケーションをテスト環境に配置するとします。
- 開発者は、デプロイプロセスを制御し、デプロイ変数を Visual Studio の外部から設定できる必要があります。これは、開発者がすべてのターゲット環境に対して適切な構成設定または必要な資格情報を持っていない可能性があるためです。
- スキーマベースのデータベースプロジェクトを配置し、後続の配置で既存のデータを保持する必要があります。
- ユーザーアカウントデータを展開せずに、メンバーシップデータベースをアドホックにデプロイする必要がある。 また、既存のユーザーアカウントデータを失うことなく、デプロイされたメンバーシップデータベースのスキーマを更新する必要がある場合もあります。
- さまざまなターゲット環境にコンテンツを展開する場合は、特定のファイルまたはフォルダーを除外する必要があります。

## <a name="overview-of-approach"></a>アプローチの概要

このチュートリアルは、このシリーズの他のチュートリアルと共に、この高レベルのアプローチを使用して、上記の課題を満たしています。

- **カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、ビルドと配置の全体的なプロセスを制御します。**
- これにより、単一のスクリプト可能な操作の一部として、ソリューション内のすべてのプロジェクトをビルドして配置することができます。
- 環境固有の設定は、環境固有の単純なプロジェクトファイルを使用して構成します。 ソリューション構成を使用した Visual Studio 中心のアプローチと、さまざまな環境のデプロイを構成するためのプロファイルの発行とは対照的に、この方法では、Visual Studio の外部からデプロイプロセスを構成および管理できます。 これは、開発者が接続文字列、サービスエンドポイント、サーバーの資格情報、およびその他の配置変数についての事前知識を必要としないことを意味します。
- カスタムプロジェクトファイルは、Team Foundation Server (TFS) ワークフローの一部として、チームビルドによって呼び出すことができます。 これにより、CI シナリオの自動化された展開を構成できます。

**Web アプリケーションプロジェクトをパッケージ化して配置するには、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用します。**

- Web 配置に用意されているフレームワークを使用すると、web アプリケーションのコンテンツをパッケージ化して目的の IIS web サーバーに配置できます。これには、依存関係、構成設定、セキュリティ設定、およびその他の要件も含まれます。
- カスタム MSBuild プロジェクトファイル内から、パッケージ化と配置のプロセス全体を制御できます。 接続文字列、サービスエンドポイント、IIS 変換先の詳細など、web 配置パッケージに付随する構成設定を操作することもできます。
- Web 配置には、Web 発行パイプラインと共に、デプロイをカスタマイズできる多数の拡張ポイントが用意されています。 たとえば、web 配置パッケージから不要なファイルやフォルダーを除外するのは簡単です。

**データベーススキーマを配置および更新するには、VSDBCMD ユーティリティを使用します。**

- VSDBCMD を使用すると、データベーススキーマファイル (.dbschema) からデータベースを配置できます。このファイルは、Visual Studio データベースプロジェクトをビルドするときに生成されます。 これに対し、Web 配置に含まれるデータベース配置機能は、ローカル SQL Server インスタンスから既存のデータベースを配置する場合に適しています。
- データベースプロジェクトを配置するための Visual Studio の機能とは異なり、VSDBCMD を使用すると、既存のターゲットデータベースに差分更新を配置できます。 これにより、データベーススキーマのアップグレード中に、既存のデータを保持することができます。
- カスタム MSBuild プロジェクトファイル内から VSDBCMD コマンドを実行できます。

## <a name="content-map"></a>コンテンツマップ

このチュートリアルには、4つの主要領域に分類されるトピックが含まれています。

これらのトピックでは、&#x2014;Contact Manager ソリューション&#x2014;のリファレンスソリューションを紹介し、それをダウンロードしてローカルコンピューターで構成する方法について説明します。

- [連絡先マネージャー ソリューション](the-contact-manager-solution.md)
- [連絡先マネージャー ソリューションを設定する](setting-up-the-contact-manager-solution.md)

これらのトピックでは、MSBuild プロジェクトファイルを紹介し、カスタムプロジェクトファイルを作成および使用する方法について説明し、Contact Manager ソリューションのデプロイプロセスについて説明します。

- [プロジェクト ファイルについて理解する](understanding-the-project-file.md)
- [ビルド処理について理解する](understanding-the-build-process.md)

これらのトピックでは、web アプリケーションの配置について説明します。これには、ビルドとパッケージ化のプロセスのしくみ、ビルドプロセスと Web 発行パイプラインとの統合方法、配置パラメーターを変更する方法、ターゲットに web パッケージを配置する方法などが含まれます。下

- [Web アプリケーション プロジェクトのビルドとパッケージ化](building-and-packaging-web-application-projects.md)
- [Web パッケージ展開のパラメーターを構成する](configuring-parameters-for-web-package-deployment.md)
- [Web パッケージを展開する](deploying-web-packages.md)

- [データベースプロジェクトの配置](deploying-database-projects.md)Visual Studio データベースプロジェクトの配置に使用できるさまざまな手法について説明し、それぞれの方法の長所と短所を示します。 [配置コマンドファイルを作成して実行](creating-and-running-a-deployment-command-file.md)する方法では、配置ロジックをカプセル化する単純なコマンドファイルを作成する方法について説明します。また、複雑なソリューションを単一ステップのプロセスとして配置することもできます。
- 最後に、 [Web パッケージを手動でインストール](manually-installing-web-packages.md)すると、IIS に web パッケージをインポートする方法を示すチュートリアルが終了します。

## <a name="key-technologies"></a>主要テクノロジ

このチュートリアルのトピックでは、主にこれらのテクノロジを使用してビルドと配置を管理します。

- Visual Studio 2010
- MSBuild
- IIS 7.5
- Web Deploy 2.0
- VSDBCMD データベース配置ユーティリティ

## <a name="other-tutorials-in-this-series"></a>このシリーズの他のチュートリアル

これは、エンタープライズ規模の web デプロイに関する一連の5つのチュートリアルの一部です。 このシリーズの他のチュートリアルは次のとおりです。

- [エンタープライズシナリオでの Web アプリケーションの展開](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 この入門用コンテンツでは、チュートリアルシリーズのコンテキストの背景を提供しています。 このチュートリアルでは、チュートリアルシナリオについて説明し、シリーズ全体で説明されているタスクとチュートリアルが、より広範なアプリケーションライフサイクル管理 (ALM) プロセスにどのように適合するかを示します。
- [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 このチュートリアルでは、Web Deployment Agent サービス (リモートエージェント) を使用したリモート web パッケージの展開や、Web 配置ハンドラーとリモートデータベースの配置など、さまざまな展開シナリオをサポートするように Windows サーバーを構成する方法について説明します。 独自の環境に適した配置方法を選択するためのガイダンスを提供します。また、Web Farm Framework (WFF) を使用して、サーバーファーム内のすべての web サーバーに配置された web アプリケーションをレプリケートする方法についても説明します。
- [Web 配置の Team Foundation Server を構成して](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)います。 このチュートリアルでは、CI プロセスの一部としての自動デプロイ、特定のビルドの手動による配置など、さまざまな配置シナリオをサポートするように TFS を構成する方法について説明します。
- [高度なエンタープライズ Web デプロイ](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 このチュートリアルでは、複数の環境でのデータベース配置のカスタマイズ、展開からのファイルとフォルダーの除外、展開プロセス中の web アプリケーションのオフライン化など、さまざまな高度な展開タスクを実行する方法について説明します.

> [!div class="step-by-step"]
> [Next](the-contact-manager-solution.md)
