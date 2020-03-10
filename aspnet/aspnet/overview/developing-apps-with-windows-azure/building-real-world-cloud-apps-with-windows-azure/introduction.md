---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure を使用した実際のクラウドアプリの構築 |Microsoft Docs
author: MikeWasson
description: この電子書籍では、実際のクラウドソリューションを構築するためのパターンベースのアプローチについて説明します。 これらのパターンは、開発プロセスや...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500650"
---
# <a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="9c7f4-104">Azure を使用した実際のクラウドアプリの構築</span><span class="sxs-lookup"><span data-stu-id="9c7f4-104">Building Real-World Cloud Apps with Azure</span></span>

<span data-ttu-id="9c7f4-105">[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9c7f4-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="9c7f4-106">[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します</span><span class="sxs-lookup"><span data-stu-id="9c7f4-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="9c7f4-107">この電子書籍では、実際のクラウドソリューションを構築するためのパターンベースのアプローチについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="9c7f4-108">パターンは、開発プロセスだけでなく、アーキテクチャとコーディングのプラクティスにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="9c7f4-109">このコンテンツは、Scott Guthrie によって開発されたプレゼンテーションに基づいており、2013年6月 ([パート 1](http://vimeo.com/68215538)、[パート 2](http://vimeo.com/68215602)) で、ノルウェーの開発者のカンファレンス (NDC) によって提供されています。また、2013年9月 (パート[1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)、パート[2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)) の Microsoft Tech Ed オーストラリアで開催されています。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="9c7f4-110">[他の多く](more-patterns-and-guidance.md#acknowledgments)は、ビデオから書面によるフォームへの移行中にコンテンツを更新し、強化しました。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>

## <a name="intended-audience"></a><span data-ttu-id="9c7f4-111">対象ユーザー</span><span class="sxs-lookup"><span data-stu-id="9c7f4-111">Intended Audience</span></span>

<span data-ttu-id="9c7f4-112">クラウドの開発に関心を持っている開発者、クラウドへの移行を検討している開発者、またはクラウド開発の経験がない開発者には、知っておく必要がある最も重要な概念とベストプラクティスの簡潔な概要が記載されています。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="9c7f4-113">概念については具体的な例を示し、各章は他のリソースにリンクして詳細な情報を参照しています。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="9c7f4-114">この例とその他のリソースへのリンクは、Microsoft のフレームワークとサービスを対象としていますが、前述の原則は他の web 開発フレームワークやクラウド環境にも当てはまります。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="9c7f4-115">クラウド用に既に開発している開発者にとっては、これを実現するためのアイデアをここで見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="9c7f4-116">シリーズの各章は個別に読み取ることができるので、関心のあるトピックを選択して選択できます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="9c7f4-117">Scott Guthrie が*Azure プレゼンテーションを使用して実際のクラウドアプリを構築*し、詳細情報と更新情報を必要としている人はだれでもここで確認できます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="9c7f4-118">クラウド開発パターン</span><span class="sxs-lookup"><span data-stu-id="9c7f4-118">Cloud development patterns</span></span>

<span data-ttu-id="9c7f4-119">この電子書籍では、クラウド開発のための13の推奨パターンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="9c7f4-120">ここでは、"Pattern" は、クラウドアプリの開発、設計、コーディングに関して最適な方法であることを意味するために、ここでは最も意味のある方法で使用されています。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="9c7f4-121">これらは、次のような場合に、"成功のある pit に入る" のに役立つ鍵となるパターンです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="9c7f4-122">[すべてを自動化](automate-everything.md)します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="9c7f4-123">スクリプトを使用すると、効率を最大化し、反復的なプロセスのエラーを最小限に抑えることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="9c7f4-124">デモ: Azure 管理スクリプト。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="9c7f4-125">[ソース管理](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="9c7f4-126">DevOps ワークフローを容易にするために、ソース管理で分岐構造を設定します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="9c7f4-127">デモ: ソース管理にスクリプトを追加します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="9c7f4-128">デモ: ソース管理から機密データを保持します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="9c7f4-129">デモ: Visual Studio で Git を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="9c7f4-130">[継続的インテグレーションと継続的デリバリー](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="9c7f4-131">各ソース管理チェックインでビルドと配置を自動化します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="9c7f4-132">[Web 開発のベストプラクティス](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="9c7f4-133">Web 層のステートレスを保持します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="9c7f4-134">デモ: Azure App Service の Web Apps でのスケーリングと自動スケール。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="9c7f4-135">セッション状態を回避します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-135">Avoid session state.</span></span>
    - <span data-ttu-id="9c7f4-136">Cdn を使用できない場合は、フォールバックで CDN を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="9c7f4-137">非同期プログラミングモデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="9c7f4-138">デモ: ASP.NET MVC と Entity Framework での非同期。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="9c7f4-139">[シングルサインオン](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="9c7f4-140">Azure Active Directory の概要。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="9c7f4-141">デモ: Azure Active Directory を使用する ASP.NET アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="9c7f4-142">[データ ストレージ オプション](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="9c7f4-143">データストアの種類。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-143">Types of data stores.</span></span>
    - <span data-ttu-id="9c7f4-144">適切データストアを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="9c7f4-145">デモ: Azure SQL Database します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="9c7f4-146">[データのパーティション分割方法](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="9c7f4-147">リレーショナルデータベースのスケーリングを容易にするために、データを垂直方向、水平方向、または両方にパーティション分割します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="9c7f4-148">[非構造化 blob ストレージ](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="9c7f4-149">Blob service を使用してクラウドにファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="9c7f4-150">デモ: It アプリを修正するには、blob storage を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="9c7f4-151">[障害が](design-to-survive-failures.md)発生した場合に備えて設計します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="9c7f4-152">エラーの種類。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-152">Types of failures.</span></span>
    - <span data-ttu-id="9c7f4-153">エラーのスコープ。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-153">Failure Scope.</span></span>
    - <span data-ttu-id="9c7f4-154">Sla について理解する。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-154">Understanding SLAs.</span></span>
- <span data-ttu-id="9c7f4-155">[監視とテレメトリ](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="9c7f4-156">テレメトリアプリを購入し、アプリをインストルメント化するための独自のコードを作成する必要があるのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="9c7f4-157">デモ: Azure の新しい聖箱</span><span class="sxs-lookup"><span data-stu-id="9c7f4-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="9c7f4-158">デモ: It アプリを修正するためのコードをログに記録します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="9c7f4-159">デモ: It アプリを修正するための依存関係の挿入。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="9c7f4-160">デモ: Azure での組み込みのログ記録のサポート。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="9c7f4-161">[一時的なエラー処理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="9c7f4-162">スマートな再試行/バックオフロジックを使用して、一時的な障害の影響を軽減します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="9c7f4-163">デモ: Entity Framework 6 の再試行/バックオフ。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="9c7f4-164">[分散キャッシュ](distributed-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="9c7f4-165">分散キャッシュを使用してスケーラビリティを向上させ、データベーストランザクションのコストを削減します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="9c7f4-166">[キュー中心の作業パターン](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="9c7f4-167">Web 層とワーカー層の疎結合により、高可用性を実現し、スケーラビリティを向上します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="9c7f4-168">デモ: It アプリを修正するための Azure storage キュー。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="9c7f4-169">[その他のクラウドアプリのパターンとガイダンス](more-patterns-and-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="9c7f4-170">付録: Fix It サンプル アプリケーション</span><span class="sxs-lookup"><span data-stu-id="9c7f4-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="9c7f4-171">既知の問題</span><span class="sxs-lookup"><span data-stu-id="9c7f4-171">Known Issues</span></span>
    - <span data-ttu-id="9c7f4-172">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="9c7f4-172">Best Practices</span></span>
    - <span data-ttu-id="9c7f4-173">ダウンロード、ビルド、実行、およびデプロイする方法。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="9c7f4-174">これらのパターンはすべてのクラウド環境に適用されますが、Visual Studio、Team Foundation Service、ASP.NET、Azure などの Microsoft のテクノロジとサービスに基づく例を使用して説明します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="9c7f4-175">この章の残りの部分では、修正プログラムのサンプルアプリケーションと、It アプリを実行する Azure App Service クラウド環境での Web Apps について説明します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="9c7f4-176">Fix it サンプルアプリケーション</span><span class="sxs-lookup"><span data-stu-id="9c7f4-176">The Fix it sample application</span></span>

<span data-ttu-id="9c7f4-177">この電子書籍に示されているスクリーンショットとコード例のほとんどは、推奨されるクラウドアプリの開発パターンとプラクティスを示すために、最初に[Scott Guthrie](https://weblogs.asp.net/scottgu/)によって開発された修正プログラムの It アプリに基づいています。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![It アプリのホームページを修正する](introduction/_static/image1.png)

<span data-ttu-id="9c7f4-179">このサンプルアプリは、単純な作業項目のチケット発行システムです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="9c7f4-180">何か修正が必要な場合は、チケットを作成して他のユーザーに割り当てます。また、他のユーザーがログインし、割り当てられたチケットを確認し、作業が完了したときにチケットを完了としてマークすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="9c7f4-181">これは、標準の Visual Studio web プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="9c7f4-182">ASP.NET MVC 上に構築され、SQL Server データベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="9c7f4-183">IIS Express でローカルに実行し、Azure の Web サイトにデプロイしてクラウドで実行することができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="9c7f4-184">フォーム認証とローカルデータベースを使用するか、Google などのソーシャルプロバイダーを使用してログインできます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="9c7f4-185">(後で、Active Directory 組織アカウントを使用してログインする方法についても説明します)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![ログインページ](introduction/_static/image2.png)

<span data-ttu-id="9c7f4-187">ログインしたら、チケットを作成し、他のユーザーに割り当てて、修正が必要なものの画像をアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![修正するタスクを作成する](introduction/_static/image3.png)

![タスクが作成されたことを修正する](introduction/_static/image4.png)

<span data-ttu-id="9c7f4-190">作成した作業項目の進行状況を追跡し、自分に割り当てられているチケットを確認し、チケットの詳細を表示し、項目を完了済みとしてマークすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="9c7f4-191">これは、機能の観点から見た非常に単純なアプリですが、何百万ものユーザーに拡張できるように構築する方法を説明しており、データベースの障害や接続の終了などに対する回復力があります。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="9c7f4-192">また、自動化およびアジャイルな開発ワークフローを作成する方法についても説明します。これにより、開発サイクルを効率的かつ迅速に反復することで、簡単に開始し、アプリの品質を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="9c7f4-193">Azure App Service の Web Apps</span><span class="sxs-lookup"><span data-stu-id="9c7f4-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="9c7f4-194">It アプリケーションの修正に使用されるクラウド環境は、Web サイトを呼び出す Azure のサービスです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="9c7f4-195">このサービスは、Vm を作成したり、IIS をインストールして構成したりすることなく、独自の web アプリを Azure でホストできるようにする方法です。Vm でサイトをホストし、バックアップと回復などのサービスを自動的に提供します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="9c7f4-196">Web サイトサービスは、ASP.NET、node.js、PHP、Python で動作します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="9c7f4-197">これにより、Visual Studio、Web 配置、FTP、Git、または TFS を使用してすばやくデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="9c7f4-198">通常は、展開を開始してから、インターネット経由で更新プログラムを利用できるようになるまでに、わずか数秒で済みます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="9c7f4-199">これはすべて無料で開始でき、トラフィックの増加に合わせてスケールアップすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="9c7f4-200">内部的には、Azure App Service の Web Apps は、独自の Vm で IIS を使用して Web サイトをホストする場合に自分で作成する必要がある、アーキテクチャのコンポーネントと機能を多数提供します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="9c7f4-201">1つのコンポーネントは、IIS を自動的に構成し、サイトの実行に必要な数の Vm にアプリケーションをインストールする展開エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![展開サービス](introduction/_static/image5.png)

<span data-ttu-id="9c7f4-203">ユーザーは、web サイトにアクセスしたときに IIS Vm に直接ヒットすることはなく、[アプリケーション要求ルーティング処理 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)のロードバランサーを経由します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="9c7f4-204">これらは独自のサーバーで使用できますが、ここでの利点は、自動的に設定されることです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="9c7f4-205">セッションアフィニティ、IIS のキューの深さ、各マシンの CPU 使用率などの要因を考慮して、web サイトをホストする Vm にトラフィックを送信するスマートヒューリスティックを使用します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR ロードバランサー](introduction/_static/image6.png)

<span data-ttu-id="9c7f4-207">マシンがダウンした場合、Azure はローテーションから自動的にそれをプルし、新しい VM インスタンスをスピンアップして、新しいインスタンスへのトラフィックの転送を開始します。アプリケーションのダウンタイムは発生しません。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![コンピューター障害からの自動回復](introduction/_static/image7.png)

<span data-ttu-id="9c7f4-209">これらはすべて自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-209">All of this takes place automatically.</span></span> <span data-ttu-id="9c7f4-210">必要な作業は、web サイトを作成し、Windows PowerShell、Visual Studio、または Microsoft Azure 管理ポータルを使用してアプリケーションをデプロイすることだけです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="9c7f4-211">Visual Studio で web アプリケーションを作成し、それを Azure の Web サイトにデプロイする方法を説明する簡単で簡単なステップバイステップのチュートリアルについては、「 [azure と ASP.NET の概要](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="9c7f4-212">まとめ</span><span class="sxs-lookup"><span data-stu-id="9c7f4-212">Summary</span></span>

<span data-ttu-id="9c7f4-213">この概要では、本書に記載されているトピックの一覧、サンプルアプリケーションのスクリーンショット、Azure App Service クラウド環境での Web Apps の概要について説明しました。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="9c7f4-214">とクラウド用のアプリを開発する大きな利点の1つは、テスト環境の作成や、コードのデプロイなど、反復的な開発タスクを簡単に自動化できることです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="9c7f4-215">その方法については、次の[章](automate-everything.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="9c7f4-216">リソース</span><span class="sxs-lookup"><span data-stu-id="9c7f4-216">Resources</span></span>

<span data-ttu-id="9c7f4-217">この章で説明しているトピックの詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="9c7f4-218">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="9c7f4-218">Documentation:</span></span>

- <span data-ttu-id="9c7f4-219">[Azure App Service で Web Apps](https://azure.microsoft.com/services/app-service/web/)ます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="9c7f4-220">Web Apps に関する Azure ドキュメントのポータルページです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="9c7f4-221">Web Apps、Cloud Services、Vm: どのような場合に使用するか。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="9c7f4-222">この章で説明する WAWS は、Azure で web アプリを実行する3つの方法のうちの1つです。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="9c7f4-223">この記事では、3つの方法の違いについて説明し、シナリオに適したものを選択する方法についてのガイダンスを示します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="9c7f4-224">Web サイトと同様に、Cloud Services は Azure の PaaS 機能です。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="9c7f4-225">Vm は IaaS 機能です。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="9c7f4-226">PaaS と IaaS の詳細については、「 [Data Options](data-storage-options.md#paasiaas) 」の章を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="9c7f4-227">ビデオ:</span><span class="sxs-lookup"><span data-stu-id="9c7f4-227">Videos:</span></span>

- [<span data-ttu-id="9c7f4-228">Scott Guthrie は、「手順 0-Azure クラウド OS とは」から開始します。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="9c7f4-229">[Web サイトのアーキテクチャ-Stefan が含ま](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)れます。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="9c7f4-230">[Azure Websites 内部の Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="9c7f4-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9c7f4-231">Next</span><span class="sxs-lookup"><span data-stu-id="9c7f4-231">Next</span></span>](automate-everything.md)
