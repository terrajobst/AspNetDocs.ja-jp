---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager ソリューション |Microsoft Docs
author: jrjlee
description: この一連のチュートリアルでは、Contact&#x2014;Manager ソリューション&#x2014;のサンプルソリューションを使用して、現実的な leve を持つエンタープライズ規模のアプリケーションを表します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473812"
---
# <a name="the-contact-manager-solution"></a><span data-ttu-id="ae3a1-103">連絡先マネージャー ソリューション</span><span class="sxs-lookup"><span data-stu-id="ae3a1-103">The Contact Manager Solution</span></span>

<span data-ttu-id="ae3a1-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ae3a1-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="ae3a1-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="ae3a1-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="ae3a1-106">この[一連のチュートリアル](web-deployment-in-the-enterprise.md)では、Contact&#x2014;Manager ソリューション&#x2014;のサンプルソリューションを使用して、現実的なレベルの複雑さを持つエンタープライズ規模のアプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="ae3a1-107">このトピックでは、Contact Manager ソリューションについて説明し、ソリューションの主要なコンポーネントについて説明します。また、この種のアプリケーションをエンタープライズ環境のさまざまな移行先プラットフォームに展開する際の課題を示します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="ae3a1-108">これらのチュートリアルのトピックを参照しながら、連絡先マネージャーソリューションを参照の実装として使用して、エンタープライズ展開シナリオで特定の課題を満たす方法を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="ae3a1-109">次のトピック「 [Contact Manager ソリューションの設定](setting-up-the-contact-manager-solution.md)」では、開発者のワークステーションでソリューションをダウンロードして実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="ae3a1-110">ソリューションの概要</span><span class="sxs-lookup"><span data-stu-id="ae3a1-110">Solution Overview</span></span>

<span data-ttu-id="ae3a1-111">Contact Manager ソリューションは、次の4つのプロジェクトで構成されています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="ae3a1-112">**Contactmanager. Mvc**。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="ae3a1-113">これは、ソリューションのエントリポイントを表す ASP.NET MVC 3 web アプリケーションプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="ae3a1-114">これには、ユーザーが連絡先の詳細を作成して表示できるようにするなど、基本的な web アプリケーション機能がいくつか用意されています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="ae3a1-115">アプリケーションは、Windows Communication Foundation (WCF) サービスを利用して連絡先と ASP.NET アプリケーションサービスデータベースを管理し、認証と承認を管理します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="ae3a1-116">**Contactmanager. データベース**。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-116">**ContactManager.Database**.</span></span> <span data-ttu-id="ae3a1-117">これは、Visual Studio データベースプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="ae3a1-118">プロジェクトでは、連絡先の詳細を格納するデータベースのスキーマを定義します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="ae3a1-119">**Contactmanager. サービス**。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-119">**ContactManager.Service**.</span></span> <span data-ttu-id="ae3a1-120">これは、WCF web サービスプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-120">This is a WCF web service project.</span></span> <span data-ttu-id="ae3a1-121">WCF サービスは、呼び出し元が**Contactmanager**データベースに対して作成、取得、更新、削除 (CRUD) 操作を実行できるようにするエンドポイントを公開します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="ae3a1-122">サービスは、 **contactmanager**データベースと**Contactmanager. 共通 .dll**アセンブリに依存しています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="ae3a1-123">**Contactmanager. 共通**。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-123">**ContactManager.Common**.</span></span> <span data-ttu-id="ae3a1-124">これはクラスライブラリプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-124">This is a class library project.</span></span> <span data-ttu-id="ae3a1-125">WCF サービスは、このアセンブリで定義されている型に依存しています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="ae3a1-126">このソリューションには、Publish という名前のソリューションフォルダーも含まれています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="ae3a1-127">これには、ビルドおよび配置プロセスを制御および操作する方法を示すさまざまなカスタムプロジェクトファイルとコマンドファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="ae3a1-128">これらの詳細については、このチュートリアルの後半で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="ae3a1-129">概念レベルでは、ソリューションのコンポーネントは次のようにまとめられます。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="ae3a1-130">ASP.NET MVC 3 web アプリケーションは ASP.NET メンバーシッププロバイダーを使用しますが、web アプリケーション内のすべてのページで匿名アクセスが許可されます。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="ae3a1-131">これは、現実的な構成ではありません。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="ae3a1-132">ただし、この方法でソリューションをセットアップすることで、ユーザーアカウントとロールを構成しなくても、ソリューションの配置とテストを容易に行えるようになります。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>

## <a name="deployment-challenges"></a><span data-ttu-id="ae3a1-133">デプロイの課題</span><span class="sxs-lookup"><span data-stu-id="ae3a1-133">Deployment Challenges</span></span>

<span data-ttu-id="ae3a1-134">Contact Manager ソリューションは、多くのエンタープライズ展開シナリオに共通するいくつかの展開の課題を示しています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="ae3a1-135">ソリューションは、複数の依存プロジェクトで構成されています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="ae3a1-136">これらのプロジェクトを同時に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="ae3a1-137">接続文字列とサービスエンドポイントは、環境ごとに更新する必要があります。多くの場合、この情報を開発者が使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="ae3a1-138">**Contactmanager**データベースをステージング環境と運用環境に配置する場合は、以降の配置で既存のデータを保持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="ae3a1-139">ASP.NET アプリケーションサービスデータベースを展開する場合は、一部の構成データを展開する必要がありますが、ユーザーアカウントデータは省略します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="ae3a1-140">プロジェクトには、配置すべきではないファイルとフォルダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="ae3a1-141">これらのファイルとフォルダーを展開プロセスから除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="ae3a1-142">ソリューションでは、Team Foundation Server (TFS) ビルドサーバーからの自動化された配置をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ae3a1-143">まとめ</span><span class="sxs-lookup"><span data-stu-id="ae3a1-143">Conclusion</span></span>

<span data-ttu-id="ae3a1-144">このトピックでは、Contact Manager ソリューションの概要について説明し、多数のエンタープライズ展開シナリオに共通する展開上のいくつかの課題を特定しました。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="ae3a1-145">このチュートリアルの残りのトピックでは、これらの課題に対応するために使用できるいくつかの手法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="ae3a1-146">次のトピック「 [Contact Manager ソリューションの設定](setting-up-the-contact-manager-solution.md)」では、開発者のワークステーションでソリューションをダウンロードして実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ae3a1-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ae3a1-147">[前へ](web-deployment-in-the-enterprise.md)
> [次へ](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ae3a1-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
