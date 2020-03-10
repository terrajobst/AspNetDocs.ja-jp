---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: チームビルド配置のアクセス許可を構成する |Microsoft Docs
author: jrjlee
description: このトピックでは、ビルドサーバーが自動 b の一部として web サーバーおよびデータベースサーバーにコンテンツをデプロイできるようにするためのアクセス許可を構成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518506"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>チーム ビルド配置のアクセス許可を構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、ビルドサーバーが自動ビルドプロセスの一環として web サーバーおよびデータベースサーバーにコンテンツを配置できるようにするためのアクセス許可を構成する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

Team Foundation Server (TFS) 2010 ビルドサービスをインストールするときに、サービスを実行する id を指定します。 既定では、これは Network Service アカウントです。 または、ドメインアカウントを使用してビルドサービスを実行するように構成することもできます。

Windows 認証を必要とし、チームビルドを使用して自動化する予定の展開タスクは、ビルドサービス id を使用して実行されます。 そのため、web サーバーとデータベースサーバーで必要なアクセス許可をビルドサービス id に付与する必要があります。

> [!NOTE]
> Network Service アカウントは、コンピューターアカウントを使用して他のコンピューターに対する認証を行います。 コンピューターアカウントは、* [ドメイン名]\[マシン名] * **$** &#x2014;のようになります。たとえば、 **FABRIKAM\TFSBUILD $** です。 そのため、ビルドサービスがネットワークサービス id を使用して実行されている場合は、ビルドサーバーのコンピューターアカウント id に必要なアクセス許可を付与する必要があります。

## <a name="configuring-web-server-permissions"></a>Web サーバーのアクセス許可の構成

「 [Web 配置に適切なアプローチを選択](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)する」で説明したように、web パッケージをリモート web サーバーに配置する場合は、次の2つの主な方法を使用できます。

- 移行先サーバーで*Web Deployment Agent サービス*(リモートエージェントとも呼ばれます) を対象にして、リモートの場所からアプリケーションを展開します。
- 移行先サーバーで*インターネットインフォメーションサービス*(*IIS) Web 配置ハンドラー*をターゲットにして、リモートの場所からアプリケーションを展開します。

この場合、リモートエージェントには次の2つの重要な制限があります。

- リモートエージェントは、NTLM 認証のみをサポートしています。 言い換えると、デプロイでは、別のアカウントを偽装&#x2014;できないビルドサービス id を使用する必要があります。
- リモートエージェントを使用するには、展開を実行するアカウントが対象サーバーの管理者である必要があります。

これらの2つの制限により、自動化されたチームビルドの配置に対してリモートエージェントのアプローチが望ましくないようになります。 この方法を使用するには、ビルドサービスアカウントをターゲット web サーバーの管理者にする必要があります。

これに対し、Web 配置ハンドラーのアプローチには、次のような利点があります。

- Web 配置ハンドラーは、HTTPS 経由の基本認証をサポートしています。これにより、別のアカウントの資格情報を IIS Web 配置ツール (Web 配置) に渡すことができます。
- 対象の web サーバーを構成して、管理者以外のユーザーが Web 配置ハンドラーを使用して特定の IIS web サイトにコンテンツを展開できるようにすることができます。

そのため、チームビルドから Web パッケージの配置を自動化する場合は、Web 配置ハンドラーを対象にすることをお勧めします。 これは推奨されるプロセスです。

1. 展開に使用する低特権ドメインアカウントを作成します。
2. Web 配置ハンドラーを構成し、特定の IIS web サイトにコンテンツを展開するために必要なアクセス許可をアカウントに付与します。詳細については、「 [Web サーバーを Web 配置発行用に構成する (Web 配置ハンドラー)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)」を参照してください。
3. 基本認証を使用し、作成したドメインアカウントの資格情報を指定して、デプロイを実行するために、Web 配置を呼び出し、Web 配置ハンドラーをターゲットにします。

[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションでは、認証の種類 (基本または NTLM)、Web 配置の資格情報、および環境固有のプロジェクトファイル内のエンドポイントアドレス (リモートエージェントまたは Web 配置ハンドラー) を指定します。 これらの値は、プロジェクトファイルの実行時に Web 配置コマンドを策定して実行するために使用されます。 詳細については、「 [Web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」を参照してください。

アクセス許可の構成方法など、Web 配置ハンドラーの構成の詳細については、「 [Web 配置発行用の Web サーバーの構成 (Web 配置ハンドラー)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)」を参照してください。 リモートエージェントの構成の詳細については、「 [Web 配置の発行用の Web サーバーの構成 (リモートエージェント)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)」を参照してください。

## <a name="configuring-database-server-permissions"></a>データベースサーバーのアクセス許可の構成

SQL Server にデータベースを配置するには、次のことを行う必要があります。

- SQL Server インスタンスに展開するアカウントのログインを作成します。
- SQL Server インスタンスに対して、ログインの**DBCreator**権限を付与します。
- 初期デプロイ後に、ターゲットデータベースの**db\_所有者**ロールにログインを追加します。 これは、後続の配置では、新しいデータベースを作成するのではなく、既存のデータベースを変更するために必要です。

NTLM 認証または SQL Server 認証を使用して、SQL Server インスタンスに対する認証を行うことができます。

- NTLM 認証を使用する場合は、上記で説明したアクセス許可をビルドサービスアカウントに付与する必要があります。
- SQL Server 認証を使用する場合は、前に説明したアクセス許可を SQL Server アカウントに付与する必要があります。 また、データベースの配置に使用する接続文字列に SQL Server のユーザー名とパスワードを含める必要があります。

データベース配置のアクセス許可を構成する方法の詳細な手順については、「 [Web 配置発行用のデータベースサーバーの構成](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)」を参照してください。

## <a name="conclusion"></a>まとめ

この時点で、チームビルドから web アプリケーションとデータベースの配置を自動化するときに、必要なアクセス許可と、開いている認証オプションを理解しておく必要があります。 また、IIS web サーバーおよび SQL Server データベースサーバーに対して必要なアクセス許可を実装することもできます。

## <a name="further-reading"></a>参考資料

リモート展開をサポートするように Windows server 環境を構成する方法の詳細については、「 [Web 配置用のサーバー環境の構成](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [[戻る]](deploying-a-specific-build.md)
