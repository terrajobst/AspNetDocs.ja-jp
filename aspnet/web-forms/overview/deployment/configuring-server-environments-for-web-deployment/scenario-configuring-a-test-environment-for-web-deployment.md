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
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a><span data-ttu-id="c57cf-103">シナリオ: Web 配置用のテスト環境の構成</span><span class="sxs-lookup"><span data-stu-id="c57cf-103">Scenario: Configuring a Test Environment for Web Deployment</span></span>

<span data-ttu-id="c57cf-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c57cf-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="c57cf-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="c57cf-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="c57cf-106">このトピックでは、開発者またはテスト環境の一般的な web 配置シナリオについて説明し、同様の環境をセットアップするために完了する必要があるタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-106">This topic describes a typical web deployment scenario for developer or test environments and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="c57cf-107">開発者が web アプリケーションを操作する場合、多くの場合、開発者はサーバー環境にアクセスして、実際の設定でアプリケーションに対する変更をテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-107">When developers work on web applications, they're often given access to a server environment that they can use to test changes to their applications in a realistic setting.</span></span> <span data-ttu-id="c57cf-108">通常、この種の開発環境またはテスト環境には、次の特性があります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-108">This kind of development or test environment typically has these characteristics:</span></span>

- <span data-ttu-id="c57cf-109">この環境は、1台の web サーバーと1つのデータベースサーバーで構成されます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-109">The environment consists of a single web server and a single database server.</span></span>
- <span data-ttu-id="c57cf-110">開発者は、通常、サーバーに対する管理者特権を持っているため、環境をアプリケーションの要件に合わせて構成できます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-110">The developers usually have administrator privileges on the servers, to let them configure the environment to the requirements of their applications.</span></span>
- <span data-ttu-id="c57cf-111">アプリケーションに対する変更は頻繁に配置されるため、環境は単一ステップまたは自動のデプロイをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-111">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

<span data-ttu-id="c57cf-112">たとえば、このチュートリアルの[シナリオ](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)では、"Fabrikam, inc." の開発者は、Contact Manager ソリューションを使用しており、定期的に変更をテスト環境にデプロイする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-112">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink is a developer at Fabrikam, Inc. Matt is working on the Contact Manager solution and regularly needs to deploy changes to a test environment.</span></span> <span data-ttu-id="c57cf-113">は、テスト web サーバーとテストデータベースサーバーの管理者です。</span><span class="sxs-lookup"><span data-stu-id="c57cf-113">Matt is an administrator on the test web server and the test database server.</span></span> <span data-ttu-id="c57cf-114">最初は、このソリューションをテスト環境に直接配置できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-114">Initially, Matt needs to be able to deploy the solution to the test environment directly.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="c57cf-115">作業の進行状況と開発者がチームに参加すると、Contact Manager ソリューションは Team Foundation Server (TFS) の継続的インテグレーション (CI) 用に構成されます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-115">As work progresses and more developers join the team, the Contact Manager solution is configured for continuous integration (CI) in Team Foundation Server (TFS).</span></span> <span data-ttu-id="c57cf-116">開発者がコンテンツをチェックインするたびに、チームビルドはソリューションをビルドし、単体テストを実行して、ソリューションをテスト環境に自動的に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-116">Whenever a developer checks in content, Team Build should build the solution, run any unit tests, and automatically deploy the solution to the test environment.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a><span data-ttu-id="c57cf-117">ソリューションの概要</span><span class="sxs-lookup"><span data-stu-id="c57cf-117">Solution Overview</span></span>

<span data-ttu-id="c57cf-118">テスト環境では、リモートコンピューターからの単一ステップまたは自動の展開をサポートする必要があるため、2つの主要なアプローチを選択できます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-118">The test environment needs to support single-step or automated deployment from a remote computer, so you have a choice of two main approaches.</span></span> <span data-ttu-id="c57cf-119">次のようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-119">You can:</span></span>

- <span data-ttu-id="c57cf-120">Web Deployment Agent サービス ("リモートエージェント") を使用した配置をサポートするようにテスト web サーバーを構成します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-120">Configure the test web server to support deployment using the Web Deployment Agent Service (the "remote agent").</span></span>
- <span data-ttu-id="c57cf-121">Web 配置ハンドラーを使用した配置をサポートするようにテスト web サーバーを構成します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-121">Configure the test web server to support deployment using the Web Deploy handler.</span></span>

> [!NOTE]
> <span data-ttu-id="c57cf-122">[必要に応じて Web 配置](https://technet.microsoft.com/library/ee517345(WS.10).aspx)("一時エージェント") を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="c57cf-122">You could also use [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx) (the "temp agent").</span></span> <span data-ttu-id="c57cf-123">これは、要件と制約に関して、リモートエージェントのアプローチに似ています。</span><span class="sxs-lookup"><span data-stu-id="c57cf-123">This is similar to the remote agent approach in terms of requirements and constraints.</span></span>

<span data-ttu-id="c57cf-124">この場合、開発者には移行先サーバーに対する管理者特権があり、テスト環境には厳密なセキュリティ制約は適用されません。したがって、リモートエージェントを使用した配置をサポートするようにテスト web サーバーを構成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c57cf-124">In this case, the developers have administrator privileges on the destination servers, and the test environment is not subject to strict security constraints, so the logical choice is to configure the test web server to support deployment using the remote agent.</span></span> <span data-ttu-id="c57cf-125">これはあまり複雑ではなく、Web 配置ハンドラーのアプローチよりも初期構成が少なくて済むことが必要です。</span><span class="sxs-lookup"><span data-stu-id="c57cf-125">This is less complex and requires less initial configuration than the Web Deploy Handler approach.</span></span> <span data-ttu-id="c57cf-126">また、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="c57cf-126">You'll also need to configure your database server to support remote access and deployment.</span></span>

<span data-ttu-id="c57cf-127">これらのトピックでは、これらのタスクを完了するために必要なすべての情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-127">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="c57cf-128">[Web 配置パブリッシング (リモートエージェント) 用に Web サーバーを構成](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-128">[Configure a Web Server for Web Deploy Publishing (Remote Agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span> <span data-ttu-id="c57cf-129">このトピックでは、Windows Server 2008 R2 のクリーンビルドから開始するリモートエージェントアプローチを使用した Web 配置の発行をサポートする web サーバーを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-129">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="c57cf-130">[Web 配置パブリッシング用にデータベースサーバーを構成](configuring-a-database-server-for-web-deploy-publishing.md)します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-130">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="c57cf-131">このトピックでは、SQL Server 2008 R2 の既定のインストールから開始して、リモートアクセスと配置をサポートするようにデータベースサーバーを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c57cf-131">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c57cf-132">参考資料</span><span class="sxs-lookup"><span data-stu-id="c57cf-132">Further Reading</span></span>

<span data-ttu-id="c57cf-133">一般的なステージング環境の構成に関するガイダンスについては、「[シナリオ: Web デプロイのステージング環境を構成](scenario-configuring-a-staging-environment-for-web-deployment.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c57cf-133">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span> <span data-ttu-id="c57cf-134">一般的な運用環境の構成に関するガイダンスについては、「[シナリオ: Web 配置用の運用環境の構成](scenario-configuring-a-production-environment-for-web-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c57cf-134">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c57cf-135">[前へ](choosing-the-right-approach-to-web-deployment.md)
> [次へ](scenario-configuring-a-staging-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="c57cf-135">[Previous](choosing-the-right-approach-to-web-deployment.md)
[Next](scenario-configuring-a-staging-environment-for-web-deployment.md)</span></span>
