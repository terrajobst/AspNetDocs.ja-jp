---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 高度なエンタープライズ Web デプロイ |Microsoft Docs
author: jrjlee
description: このチュートリアルでは、多くのエンタープライズ展開シナリオで必要または望ましいさまざまなタスクを実行する方法について説明します。 イタリア語 translati の場合...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474958"
---
# <a name="advanced-enterprise-web-deployment"></a>高度なエンタープライズ Web 配置

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このチュートリアルでは、多くのエンタープライズ展開シナリオで必要または望ましいさまざまなタスクを実行する方法について説明します。
> 
> これらのチュートリアルのイタリア語翻訳については、 [http://www.lucamorelli.it](http://www.lucamorelli.it)を参照してください。

これは、Fabrikam, Inc. という架空の会社のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部となります。このチュートリアルシリーズでは、&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ソリューション&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「ビルド[プロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法に基づいて&#x2014;います。この方法では、ビルドプロセスは、各配置先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="scenario-overview"></a>シナリオの概要

これらのチュートリアルの高度なシナリオについては、「[エンタープライズ Web 配置: シナリオの概要](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」を参照してください。 このチュートリアルを開始する前に、このトピックを確認することをお勧めします。

## <a name="how-to-use-this-tutorial"></a>このチュートリアルの使用方法

- このチュートリアルの各トピックは自己完結型であり、エンタープライズ展開シナリオで発生する特定の課題または問題に対処します。 これらのトピックを特定の順序で処理する必要はありません。 ただし、このチュートリアルでは、いくつかの高度なタスクについて説明します。 そのため、このコンテンツを最大限に活用するために、エンタープライズチュートリアルの[Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)で説明されている概念と手法について理解しておく必要があります。
- このチュートリアルには、次のトピックが含まれています。
- ["What If" 展開を実行](performing-a-what-if-deployment.md)しています。 ほとんどのシナリオでは、実際に変更を行う前に、提案されたデプロイがターゲット環境または既存のコンテンツに与える影響を判断する必要があります。 このトピックでは、実際には変更を加えずに、ターゲット環境にコンテンツをデプロイした場合と同様に、ログファイルとデータベース更新スクリプトを生成するために "what-if" 配置を実行する方法について説明します。 これらのリソースを分析すると、ライブデプロイの前に潜在的な問題を特定するのに役立ちます。
- [複数の環境でのデータベース配置のカスタマイズ](customizing-database-deployments-for-multiple-environments.md)。 複数の変換先にデータベースプロジェクトを配置する場合は、多くの場合、各ターゲット環境の配置プロパティをカスタマイズすることをお勧めします。 たとえば、テスト環境では、通常、すべての配置でデータベースを再作成します。一方、ステージング環境や運用環境では、データを保持するために増分更新を行う方がはるかに多くなります。 このトピックでは、これらのプロパティの変更を配置ロジックに組み込む方法について説明します。そのためには、各ターゲット環境に対して環境固有の配置構成 (sqldeployment) ファイルを作成します。
- テスト環境にデータベースロールメンバーシップを配置する。 たとえば、継続的インテグレーション (CI) を&#x2014;ビルドしてテスト環境&#x2014;に配置するなど、すべての配置でデータベースを再作成する場合、通常は毎回データベースロールのメンバーシップを構成する必要があります。 たとえば、通常、web アプリケーションに関連付けられているアプリケーションプール id にアクセス許可を付与する必要があります。 このトピックでは、配置後の SQL スクリプトを配置ロジックに追加することによって、このプロセスを自動化する方法について説明します。
- [エンタープライズ環境にメンバーシップデータベースを展開する](deploying-membership-databases-to-enterprise-environments.md)。 ASP.NET メンバーシップデータベースには、デプロイプロセスが複雑になる可能性があるさまざまな特性があります。 たとえば、スキーマのみの配置では、データベースは操作不可能な状態のままになります。 ほとんどのシナリオでは、各送信先環境にメンバーシップデータベースを直接作成することをお勧めします。 ただし、メンバーシップデータベースを配置する必要がある場合は、このトピックでは、固有の課題を満たすために使用できるいくつかの方法について説明します。
- [ファイルとフォルダーを展開から除外](excluding-files-and-folders-from-deployment.md)する。 シナリオによっては、web パッケージのコンテンツを特定の配置先環境に合わせて調整することが必要になる場合があります。 たとえば、テスト環境に配置するときに JavaScript ライブラリの完全バージョンを含め、クライアント側のデバッグをサポートすることができますが、ステージング環境または運用環境に配置するときには、縮小版のライブラリを使用します。 このトピックでは、パッケージ作成プロセスから特定のファイルとフォルダーを除外する方法について説明します。
- [Web 配置を使用して Web アプリケーションをオフラインに](taking-web-applications-offline-with-web-deploy.md)する。 ソリューションをステージング環境または運用環境に配置するときは、通常、デプロイプロセスの間、web アプリケーションをオフラインにすることをお勧めします。 このトピックでは、デプロイプロセスの開始時に web アプリケーションに*アプリ\_オフライン .htm*ファイルを追加して、最後に削除する方法について説明します。 *アプリ\_オフライン .htm*ファイルが配置されている間、web アプリケーションを参照するすべてのユーザーが、*オフライン .Htm ファイル\_アプリ*に自動的にリダイレクトされます。
- [MSBuild から Windows PowerShell スクリプトを実行して](running-windows-powershell-scripts-from-msbuild-project-files.md)います。 多くの展開シナリオでは、レジストリへのカスタムイベントソースの追加や SQL Server インスタンス間のレプリケーションの構成など、より複雑な配置後アクションが必要になります。 これらのアクションは、多くの場合、Windows PowerShell スクリプトを通じて行われます。 このトピックでは、ビルドおよび配置のプロセスの一部として、Microsoft Build Engine (MSBuild) プロジェクトファイルから Windows PowerShell スクリプトを実行する方法について説明します。
- [パッケージ化プロセスのトラブルシューティング](troubleshooting-the-packaging-process.md)。 Web 発行パイプライン (WPP) では、web アプリケーションプロジェクトのパッケージ化プロセスに関する詳細な情報を生成するために使用できる、 **Enablepackageprocessの**という名前の MSBuild プロパティを定義します。 このトピックでは、プロパティの動作と使用方法について説明します。

## <a name="key-technologies"></a>主要テクノロジ

このチュートリアルでは、これらの製品とテクノロジを使用して、自動化されたビルドと web 配置をサポートする方法について説明します。

- Visual Studio 2010 および Team Foundation Server (TFS) 2010
- MSBuild と TFS チームビルド
- インターネットインフォメーションサービス (IIS) 7.5
- IIS Web 配置ツール (Web 配置) 2.1
- VSDBCMD データベース配置ユーティリティ

## <a name="other-tutorials-in-this-series"></a>このシリーズの他のチュートリアル

これは、エンタープライズ規模の web デプロイに関する一連の5つのチュートリアルの一部です。 このシリーズの他のチュートリアルは次のとおりです。

- [エンタープライズシナリオでの Web アプリケーションの展開](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 この入門用コンテンツでは、チュートリアルシリーズのコンテキストの背景を提供しています。 このチュートリアルでは、チュートリアルシナリオについて説明し、シリーズ全体で説明されているタスクとチュートリアルが、より広範なアプリケーションライフサイクル管理 (ALM) プロセスにどのように適合するかを示します。
- [企業の Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 このチュートリアルでは、MSBuild プロジェクトファイル、WPP、Web 配置、およびその他の関連テクノロジについて概念的に説明します。 これらのツールを組み合わせて使用して、複雑な展開プロセスを管理する方法について説明します。
- [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 このチュートリアルでは、Web Deployment Agent サービス (リモートエージェント) を使用したリモート web パッケージの展開や、Web 配置ハンドラーとリモートデータベースの配置など、さまざまな展開シナリオをサポートするように Windows サーバーを構成する方法について説明します。 独自の環境に適した配置方法を選択するためのガイダンスを提供します。また、Web Farm Framework (WFF) を使用して、サーバーファーム内のすべての web サーバーに配置された web アプリケーションをレプリケートする方法についても説明します。
- [Web 配置の Team Foundation Server を構成して](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)います。 このチュートリアルでは、CI プロセスの一部としての自動デプロイ、特定のビルドの手動による配置など、さまざまな配置シナリオをサポートするように TFS を構成する方法について説明します。

> [!div class="step-by-step"]
> [Next](performing-a-what-if-deployment.md)
