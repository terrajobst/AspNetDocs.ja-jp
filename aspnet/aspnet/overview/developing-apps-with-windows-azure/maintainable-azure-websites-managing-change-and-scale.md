---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'ハンズオンラボ: メンテナンス可能な Azure Websites: 変更とスケールの管理 |Microsoft Docs'
author: rick-anderson
description: このラボでは、Microsoft Azure を使用して、web サイトを簡単に構築して運用環境に展開する方法について説明します。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506374"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="c62bf-103">ハンズオンラボ: メンテナンス可能な Azure Websites: 変更とスケールの管理</span><span class="sxs-lookup"><span data-stu-id="c62bf-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="c62bf-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="c62bf-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c62bf-105">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="c62bf-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="c62bf-106">Microsoft Azure を使用すると、簡単に web サイトを構築して運用環境にデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="c62bf-107">しかし、アプリケーションが稼働しているときには完了していません。</span><span class="sxs-lookup"><span data-stu-id="c62bf-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="c62bf-108">変化する要件、データベースの更新、スケールなどを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="c62bf-109">幸いにも、サイトの円滑な実行を維持するのに役立つ多くの機能が用意されており、Azure App Service について説明しています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="c62bf-110">Azure では、あらゆる規模の web アプリケーションに対して、セキュリティで保護された柔軟な開発、デプロイ、スケーリングのオプションを提供しています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="c62bf-111">既存のツールを活用して、インフラストラクチャを管理する手間をかけずにアプリケーションを作成してデプロイします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="c62bf-112">お気に入りの開発ツールを使用して作成されたコンテンツを簡単にデプロイできるため、実稼働 web アプリケーションを数分でプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="c62bf-113">**Git**、 **GitHub**、 **Bitbucket**、 **TFS**、および**DropBox**のサポートを使用して、既存のサイトをソース管理から直接デプロイできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="c62bf-114">Windows の**PowerShell**または任意の OS で実行されている**CLI**ツールを使用して、お気に入りの IDE またはスクリプトから直接デプロイできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="c62bf-115">デプロイが完了したら、継続的なデプロイのサポートによって、サイトを常に最新の状態に保ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="c62bf-116">Azure は、あらゆるデータに対応したスケーラブルで持続性のあるクラウドストレージ、バックアップ、回復のソリューションを提供します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="c62bf-117">アプリケーションを運用環境にデプロイする場合、テーブル、Blob、SQL データベースなどのストレージサービスは、クラウドでのアプリケーションのスケーリングに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="c62bf-118">SQL データベースでは、アプリケーションの新しいバージョンをデプロイするときに、生産性の高いデータベースを最新の状態に保つことが重要です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="c62bf-119">**Entity Framework Code First Migrations**のおかげで、データモデルの開発とデプロイは、数分で環境を更新するために簡略化されています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="c62bf-120">このハンズオンラボでは、Microsoft Azure で運用環境に web アプリをデプロイするときに発生する可能性のあるさまざまなトピックを示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="c62bf-121">すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="c62bf-122">このトピックの詳細については、「 [Azure 電子ブックを使用した実際のクラウドアプリの構築](building-real-world-cloud-apps-with-windows-azure/introduction.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="c62bf-123">概要</span><span class="sxs-lookup"><span data-stu-id="c62bf-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c62bf-124">目標</span><span class="sxs-lookup"><span data-stu-id="c62bf-124">Objectives</span></span>

<span data-ttu-id="c62bf-125">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="c62bf-126">既存のモデルを使用して Entity Framework 移行を有効にする</span><span class="sxs-lookup"><span data-stu-id="c62bf-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="c62bf-127">Entity Framework の移行を使用して、オブジェクトモデルとデータベースを適宜更新する</span><span class="sxs-lookup"><span data-stu-id="c62bf-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="c62bf-128">Git を使用した Azure App Service へのデプロイ</span><span class="sxs-lookup"><span data-stu-id="c62bf-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="c62bf-129">Microsoft Azure 管理ポータルを使用して以前のデプロイにロールバックする</span><span class="sxs-lookup"><span data-stu-id="c62bf-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="c62bf-130">Azure Storage を使用して web アプリをスケールする</span><span class="sxs-lookup"><span data-stu-id="c62bf-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="c62bf-131">Azure 管理ポータルを使用して web アプリの自動スケールを構成する</span><span class="sxs-lookup"><span data-stu-id="c62bf-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="c62bf-132">Visual Studio でのロードテストプロジェクトの作成と構成</span><span class="sxs-lookup"><span data-stu-id="c62bf-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c62bf-133">前提条件</span><span class="sxs-lookup"><span data-stu-id="c62bf-133">Prerequisites</span></span>

<span data-ttu-id="c62bf-134">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="c62bf-135">[Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="c62bf-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="c62bf-136">Azure SDK for .NET 2.2</span><span class="sxs-lookup"><span data-stu-id="c62bf-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="c62bf-137">GIT バージョン管理システム</span><span class="sxs-lookup"><span data-stu-id="c62bf-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="c62bf-138">Microsoft Azure サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="c62bf-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="c62bf-139">[無料試用版](https://aka.ms/watk-freetrial)にサインアップする</span><span class="sxs-lookup"><span data-stu-id="c62bf-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="c62bf-140">Visual Studio Professional、Test Professional、Premium、または Ultimate with MSDN または MSDN Platforms サブスクライバーであれば、今すぐ[msdn の特典](https://aka.ms/watk-msdn)をアクティブ化して、Azure での開発とテストを開始できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="c62bf-141">[Bizspark](https://aka.ms/watk-bizspark)メンバーは、Visual Studio Ultimate with MSDN サブスクリプションを通じて Azure 特典を自動的に受け取ります</span><span class="sxs-lookup"><span data-stu-id="c62bf-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="c62bf-142">[Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials プログラムのメンバーは、毎月 Azure クレジットを無料で受け取ることができます</span><span class="sxs-lookup"><span data-stu-id="c62bf-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c62bf-143">セットアップ</span><span class="sxs-lookup"><span data-stu-id="c62bf-143">Setup</span></span>

<span data-ttu-id="c62bf-144">このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="c62bf-145">エクスプローラーを開き、ラボの**ソース**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="c62bf-146">**Setup.exe**を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="c62bf-147">[ユーザーアカウント制御] ダイアログが表示されている場合は、操作を続行することを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="c62bf-148">セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="c62bf-149">コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="c62bf-149">Using the Code Snippets</span></span>

<span data-ttu-id="c62bf-150">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="c62bf-151">便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="c62bf-152">各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="c62bf-153">演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="c62bf-154">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="c62bf-155">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c62bf-156">手順</span><span class="sxs-lookup"><span data-stu-id="c62bf-156">Exercises</span></span>

<span data-ttu-id="c62bf-157">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="c62bf-158">Entity Framework 移行の使用</span><span class="sxs-lookup"><span data-stu-id="c62bf-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="c62bf-159">Web アプリをステージングにデプロイする</span><span class="sxs-lookup"><span data-stu-id="c62bf-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="c62bf-160">運用環境での配置ロールバックの実行</span><span class="sxs-lookup"><span data-stu-id="c62bf-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="c62bf-161">Azure Storage を使用したスケーリング</span><span class="sxs-lookup"><span data-stu-id="c62bf-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="c62bf-162">[Web Apps に自動スケールを使用する](#Exercise5)(Visual Studio 2013 Ultimate edition では省略可能)</span><span class="sxs-lookup"><span data-stu-id="c62bf-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="c62bf-163">このラボの推定所要時間: **75 分**</span><span class="sxs-lookup"><span data-stu-id="c62bf-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="c62bf-164">Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="c62bf-165">定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="c62bf-166">このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="c62bf-167">開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="c62bf-168">演習 1: Entity Framework の移行の使用</span><span class="sxs-lookup"><span data-stu-id="c62bf-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="c62bf-169">アプリケーションを開発するときに、データモデルが時間の経過と共に変化することがあります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="c62bf-170">これらの変更は、データベース内の既存のモデルに影響を与える可能性があります (新しいバージョンを作成している場合)。また、エラーを防ぐために、データベースを最新の状態に保つことが重要です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="c62bf-171">モデルにおけるこれらの変更の追跡を簡単にするために、 **Entity Framework Code First Migrations**モデルとデータベーススキーマを比較して変更を自動的に検出し、データベースを更新するための特定のコードを生成して、データベースの新しい*バージョン*を作成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="c62bf-172">この演習では、アプリケーションの**移行**を有効にする方法と、データベースを更新するための変更を簡単に検出して生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="c62bf-173">タスク1–移行を有効にする</span><span class="sxs-lookup"><span data-stu-id="c62bf-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="c62bf-174">この実習では、**マニアクイズ**データベースに対して**Entity Framework Code First Migrations**を有効にする手順について説明し、モデルを変更して、変更がデータベースに反映される方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="c62bf-175">Visual Studio を開き、 **Source\Ex1-UsingEntityFrameworkMigrations\Begin**から**GeekQuiz**ソリューションファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="c62bf-176">**NuGet**パッケージの依存関係をダウンロードしてインストールするために、ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="c62bf-177">これを行うには、ソリューションを右クリックし、 **[ソリューションのビルド]** をクリックするか、 **Ctrl + Shift + B**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="c62bf-178">Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="c62bf-179">**パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="c62bf-180">既存のモデルに基づく初期移行が作成されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="c62bf-181">![移行の有効化](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "移行を有効にする")</span><span class="sxs-lookup"><span data-stu-id="c62bf-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="c62bf-182">*移行の有効化*</span><span class="sxs-lookup"><span data-stu-id="c62bf-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-183">このコマンドは、 **Configuration.cs**という名前のファイルを含むマニアクイズプロジェクトに、**移行**フォルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="c62bf-184">**構成**クラスを使用すると、コンテキストの移行の動作を構成できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="c62bf-185">移行を有効にした場合、**構成**クラスを更新して、**マニアクイズ**が必要とする初期データをデータベースに設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="c62bf-186">**[移行]** で、 **Configuration.cs**ファイルを、このラボの **[source\ Assets]** フォルダーにあるものに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-187">**移行**では、すべてのデータベース更新で**Seed**メソッドが呼び出されるため、データベース内でレコードが複製されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="c62bf-188">**Addorupdate**メソッドを使用すると、重複するデータを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="c62bf-189">初期移行を追加するには、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-190">LocalDB インスタンスに &quot;GeekQuizProd&quot; という名前のデータベースがないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="c62bf-191">![ベーススキーマの移行の追加](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "ベーススキーマの移行の追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="c62bf-192">*ベーススキーマの移行の追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-193">**追加移行**では、前回の移行が作成されてからモデルに対して行った変更に基づいて、次の移行がスキャフォールディングされます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="c62bf-194">この場合、プロジェクトの最初の移行として、 **TriviaContext**クラスで定義されているすべてのテーブルを作成するスクリプトが追加されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="c62bf-195">次のコマンドを実行して、移行を実行し、データベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="c62bf-196">このコマンドでは、ターゲットデータベースに適用されている SQL ステートメントを表示する**Verbose**フラグを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="c62bf-197">![初期データベースの作成](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "初期データベースの作成")</span><span class="sxs-lookup"><span data-stu-id="c62bf-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="c62bf-198">*初期データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-199">**更新データベース**では、保留中の移行がデータベースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="c62bf-200">この場合、web.config ファイルで定義されている接続文字列を使用してデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="c62bf-201">**[表示]** メニューにアクセスして**SQL Server オブジェクトエクスプローラー**を開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="c62bf-202">![SQL Server オブジェクトエクスプローラーで開く](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server オブジェクトエクスプローラーで開く")</span><span class="sxs-lookup"><span data-stu-id="c62bf-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="c62bf-203">*SQL Server オブジェクトエクスプローラーで開く*</span><span class="sxs-lookup"><span data-stu-id="c62bf-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="c62bf-204">**[SQL Server オブジェクトエクスプローラー]** ウィンドウで、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** オプションを選択して、LocalDB インスタンスに接続します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="c62bf-205">![SQL Server インスタンスの追加](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server インスタンスの追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="c62bf-206">*SQL Server オブジェクトエクスプローラーへの SQL Server インスタンスの追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="c62bf-207">**サーバー名**を *(localdb) \ v11.0*に設定し、認証モードとして**Windows 認証**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="c62bf-208">**[接続]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="c62bf-209">![LocalDB に接続しています](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB に接続しています")</span><span class="sxs-lookup"><span data-stu-id="c62bf-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="c62bf-210">*LocalDB に接続しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="c62bf-211">**GeekQuizProd**データベースを開き、 **[テーブル]** ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="c62bf-212">ご覧のように、 **TriviaContext**クラスで定義されているすべてのテーブルが、**データベースの更新**コマンドによって生成されました。</span><span class="sxs-lookup"><span data-stu-id="c62bf-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="c62bf-213">Dbo を見つけ**ます。TriviaQuestions**テーブルを開き、[列] ノードを開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="c62bf-214">次のタスクでは、このテーブルに新しい列を追加し、**移行**を使用してデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="c62bf-215">![トリビアの質問列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "トリビアの質問列")</span><span class="sxs-lookup"><span data-stu-id="c62bf-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="c62bf-216">*トリビアの質問列*</span><span class="sxs-lookup"><span data-stu-id="c62bf-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="c62bf-217">タスク2–移行を使用してデータベーススキーマを更新する</span><span class="sxs-lookup"><span data-stu-id="c62bf-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="c62bf-218">このタスクでは、 **Entity Framework Code First Migrations**を使用して、モデルの変更を検出し、データベースを更新するために必要なコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="c62bf-219">**TriviaQuestions**エンティティを更新するには、新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="c62bf-220">次に、コマンドを実行して新しい移行を作成し、新しい列をテーブルに含めます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="c62bf-221">**ソリューションエクスプローラー**で、 **[モデル]** フォルダー内にある**TriviaQuestion.cs**ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="c62bf-222">次のコードスニペットに示すように、**ヒント**という名前の新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="c62bf-223">**パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="c62bf-224">モデルの変更を反映した新しい移行が作成されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="c62bf-225">![移行の追加](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span><span class="sxs-lookup"><span data-stu-id="c62bf-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="c62bf-226">*移行の追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-227">移行ファイルは、**上下**に2つの方法で構成さ**れてい**ます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="c62bf-228">**Up**メソッドは、アプリケーションの現在のバージョンがデータベースに適用する必要がある変更を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="c62bf-229">**Down**は、 **Up**メソッドに追加した変更を元に戻すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="c62bf-230">データベースの移行によってデータベースが更新されると、すべての移行がタイムスタンプの順序で実行され、最後の更新以降に使用されていないもののみが実行されます (\_MigrationHistory テーブルは、適用されている移行を追跡します)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="c62bf-231">すべての移行の**Up**メソッドが呼び出され、指定した変更がデータベースに対して行われます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="c62bf-232">前の移行に戻る場合は、逆の順序で変更を再実行するために**Down**メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="c62bf-233">**パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="c62bf-234">次の図に示すように、 **TriviaQuestions**テーブルに新しい列を追加するために、**データベースの更新**コマンドの出力で**Alter Table** SQL ステートメントが生成されました。</span><span class="sxs-lookup"><span data-stu-id="c62bf-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="c62bf-235">![列の追加 SQL ステートメントが生成されました](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "列の追加 SQL ステートメントが生成されました")</span><span class="sxs-lookup"><span data-stu-id="c62bf-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="c62bf-236">*列の追加 SQL ステートメントが生成されました*</span><span class="sxs-lookup"><span data-stu-id="c62bf-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="c62bf-237">**SQL Server オブジェクトエクスプローラー**で、dbo を更新し**ます。TriviaQuestions**テーブルを作成し、新しい**ヒント**列が表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="c62bf-238">![新しいヒント列を表示しています](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "新しいヒント列を表示しています")</span><span class="sxs-lookup"><span data-stu-id="c62bf-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="c62bf-239">*新しいヒント列を表示しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="c62bf-240">次のコードスニペットに示すように、 **TriviaQuestion.cs**エディターに戻り、 *Hint*プロパティに**stringlength**制約を追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="c62bf-241">**パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="c62bf-242">**パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="c62bf-243">次の図に示すように、 **TriviaQuestions**テーブルの*ヒント*列の型を更新するために、**データベースの更新**コマンドの出力で**Alter table** SQL ステートメントが生成されました。</span><span class="sxs-lookup"><span data-stu-id="c62bf-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="c62bf-244">![Alter column SQL ステートメントが生成されました](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL ステートメントが生成されました")</span><span class="sxs-lookup"><span data-stu-id="c62bf-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="c62bf-245">*Alter column SQL ステートメントが生成されました*</span><span class="sxs-lookup"><span data-stu-id="c62bf-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="c62bf-246">**SQL Server オブジェクトエクスプローラー**で、dbo を更新し**ます。TriviaQuestions**テーブルを確認し、**ヒント**列の型が**nvarchar (150)** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="c62bf-247">![新しい制約を表示しています](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "新しい制約を表示しています")</span><span class="sxs-lookup"><span data-stu-id="c62bf-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="c62bf-248">*新しい制約を表示しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="c62bf-249">演習 2: ステージングへの Web アプリのデプロイ</span><span class="sxs-lookup"><span data-stu-id="c62bf-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="c62bf-250">**Azure App Service の Web Apps**を使用すると、ステージングされた発行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="c62bf-251">ステージングされた発行では、既定の運用サイトごとにステージングサイトスロットを作成し、ダウンタイムなしでこれらのスロットを交換できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="c62bf-252">これは、パブリックにリリースする前に変更を検証し、サイトコンテンツを段階的に統合し、変更が期待どおりに機能していない場合はロールバックするのに非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="c62bf-253">この演習では、Git ソース管理を使用して、web アプリのステージング環境に**マニアクイズ**アプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="c62bf-254">これを行うには、web アプリを作成し、必要なコンポーネントを管理ポータルでプロビジョニングします。次に、 **Git**リポジトリを構成し、ローカルコンピューターからステージングスロットにアプリケーションのソースコードをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="c62bf-255">また、前の演習で作成した**Code First Migrations**を使用して、実稼働データベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="c62bf-256">次に、このテスト環境でアプリケーションを実行して、その操作を確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="c62bf-257">期待どおりに動作していることを確認したら、アプリケーションを運用環境に昇格させます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="c62bf-258">ステージングされた発行を有効にするには、web アプリが**標準モード**である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="c62bf-259">Web アプリを標準モードに変更すると、追加料金が発生することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="c62bf-260">価格の詳細については、「 [App Service の価格](https://azure.microsoft.com/pricing/details/app-service/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="c62bf-261">タスク1– Azure App Service で Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="c62bf-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="c62bf-262">このタスクでは、管理ポータルから**Azure App Service**で web アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="c62bf-263">また、 **SQL Database**を構成して、アプリケーションデータを永続化し、ソース管理用のローカル Git リポジトリを構成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="c62bf-264">[Azure 管理ポータル](https://manage.windowsazure.com)にアクセスし、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Microsoft Azure 管理ポータルにサインインします。](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="c62bf-266">*Microsoft Azure 管理ポータルにサインインします。*</span><span class="sxs-lookup"><span data-stu-id="c62bf-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="c62bf-267">ページの下部にあるコマンドバーで **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="c62bf-268">![新しい web アプリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "新しい web アプリの作成")</span><span class="sxs-lookup"><span data-stu-id="c62bf-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="c62bf-269">*新しい web アプリの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="c62bf-270">**[Compute]** 、 **[web サイト]** 、 **[カスタム作成]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="c62bf-271">![カスタム作成を使用した新しい web アプリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "カスタム作成を使用した新しい web アプリの作成")</span><span class="sxs-lookup"><span data-stu-id="c62bf-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="c62bf-272">*カスタム作成を使用した新しい web アプリの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="c62bf-273">**[新しい Web サイト-カスタム作成]** ダイアログボックスで、使用可能な**URL** (例:*マニア*) を指定し、 **[リージョン]** ボックスの一覧で場所を選択し、 **[データベース]** ボックスの一覧で **[新しい SQL データベースを作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="c62bf-274">最後に、 **[ソース管理から発行]** する チェックボックスをオンにし、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![新しい web アプリのカスタマイズ](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="c62bf-276">*新しい web アプリのカスタマイズ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="c62bf-277">データベースの設定に関する次の情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="c62bf-278">**[名前]** テキストボックスに、データベース名 (例: *geekquiz\_db*) を入力します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="c62bf-279">[サーバー **] ドロップダウン**リストで、 **[新しい SQL データベースサーバー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="c62bf-280">または、既存のサーバーを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="c62bf-281">**[データベースのユーザー名]** ボックスと **[データベースパスワード]** ボックスに、SQL データベースサーバーの管理者のユーザー名とパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="c62bf-282">既に作成してあるサーバーを選択した場合は、パスワードの入力を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![データベースの設定の指定](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="c62bf-284">*データベースの設定の指定*</span><span class="sxs-lookup"><span data-stu-id="c62bf-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="c62bf-285">**[次へ]** をクリックして次に進みます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="c62bf-286">使用するソース管理の **[ローカル Git リポジトリ]** を選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-287">デプロイ資格情報 (ユーザー名とパスワード) の入力を求められる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Git リポジトリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="c62bf-289">*Git リポジトリの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="c62bf-290">新しい web アプリが作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-291">既定では、Azure は*azurewebsites.net*にドメインを提供しますが、azure 管理ポータルを使用してカスタムドメインを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="c62bf-292">ただし、特定の Azure App Service モードを使用している場合にのみ、カスタムドメインを管理できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="c62bf-293">Azure App Service は、Free、Shared、Basic、Standard、および Premium の各エディションで使用できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="c62bf-294">無料モードと共有モードでは、すべての web アプリがマルチテナント環境で実行され、CPU、メモリ、およびネットワーク使用率のクォータがあります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="c62bf-295">無料アプリの最大数は、プランによって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="c62bf-296">標準モードでは、標準の Azure コンピューティングリソースに対応する専用の仮想マシンで実行されるアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="c62bf-297">Web アプリモードの構成は、web アプリの **[スケール]** メニューで確認できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="c62bf-298">![Azure App Service モード](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service モード")</span><span class="sxs-lookup"><span data-stu-id="c62bf-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="c62bf-299">**共有**モードまたは**標準**モードを使用している場合は、アプリの **[構成]** メニューに移動し、[*ドメイン名*] の **[ドメインの管理]** をクリックすることで、web アプリのカスタムドメインを管理できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="c62bf-300">![ドメインの管理](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "ドメインの管理")</span><span class="sxs-lookup"><span data-stu-id="c62bf-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="c62bf-301">![カスタムドメインの管理](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "カスタムドメインの管理")</span><span class="sxs-lookup"><span data-stu-id="c62bf-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="c62bf-302">Web アプリが作成されたら、 **[URL]** 列の下のリンクをクリックして、新しい web アプリが実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![新しい web アプリを参照しています](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="c62bf-304">*新しい web アプリを参照しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-304">*Browsing to the new web app*</span></span>

    ![実行中の web アプリ](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="c62bf-306">*実行中の web アプリ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="c62bf-307">タスク2–運用 SQL Database を作成する</span><span class="sxs-lookup"><span data-stu-id="c62bf-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="c62bf-308">このタスクでは、 **Entity Framework Code First Migrations**を使用して、前の作業で作成した**Azure SQL Database**インスタンスを対象とするデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="c62bf-309">管理ポータルで、前のタスクで作成した web アプリに移動し、**ダッシュボード**に移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="c62bf-310">**[ダッシュボード]** ページで、 **[概要] セクションの** **[接続文字列の表示]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="c62bf-311">![接続文字列の表示](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "接続文字列の表示")</span><span class="sxs-lookup"><span data-stu-id="c62bf-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="c62bf-312">*接続文字列の表示*</span><span class="sxs-lookup"><span data-stu-id="c62bf-312">*View connection strings*</span></span>
3. <span data-ttu-id="c62bf-313">**[接続文字列]** の値をコピーして、ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="c62bf-314">![Azure 管理ポータルの接続文字列](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理ポータルの接続文字列")</span><span class="sxs-lookup"><span data-stu-id="c62bf-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="c62bf-315">*Azure 管理ポータルの接続文字列*</span><span class="sxs-lookup"><span data-stu-id="c62bf-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="c62bf-316">**[Sql データベース]** をクリックして、Azure 内の sql データベースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="c62bf-317">![SQL Database メニュー](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database メニュー")</span><span class="sxs-lookup"><span data-stu-id="c62bf-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="c62bf-318">*SQL Database メニュー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="c62bf-319">前のタスクで作成したデータベースを見つけて、サーバーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="c62bf-320">![SQL Database サーバー](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database サーバー")</span><span class="sxs-lookup"><span data-stu-id="c62bf-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="c62bf-321">*SQL Database サーバー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-321">*SQL Database server*</span></span>
6. <span data-ttu-id="c62bf-322">サーバーの **[クイックスタート]** ページで、 **[構成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="c62bf-323">![[構成] メニュー](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "[構成] メニュー")</span><span class="sxs-lookup"><span data-stu-id="c62bf-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="c62bf-324">*[構成] メニュー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-324">*Configure menu*</span></span>
7. <span data-ttu-id="c62bf-325">[**許可さ**れた ip アドレス] セクションで、[**許可された Ip アドレスに追加**する] リンクをクリックして、ip が SQL Database サーバーに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="c62bf-326">![使用できる IP アドレス](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "許可された IP アドレス")</span><span class="sxs-lookup"><span data-stu-id="c62bf-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="c62bf-327">*使用できる IP アドレス*</span><span class="sxs-lookup"><span data-stu-id="c62bf-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="c62bf-328">ページの下部にある **[保存]** をクリックして、手順を完了します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="c62bf-329">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="c62bf-330">**パッケージマネージャーコンソール**で、次のコマンドを実行します。 *[your-CONNECTION-STRING]* プレースホルダーを、Azure からコピーした接続文字列に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="c62bf-331">![Windows Azure SQL Database を対象とするデータベースの更新](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database を対象とするデータベースの更新")</span><span class="sxs-lookup"><span data-stu-id="c62bf-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="c62bf-332">*データベースターゲットの更新 Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="c62bf-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="c62bf-333">タスク3– Git を使用してマニアクイズをステージングにデプロイする</span><span class="sxs-lookup"><span data-stu-id="c62bf-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="c62bf-334">このタスクでは、web アプリでステージングされた発行を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="c62bf-335">次に、Git を使用して、ローカルコンピューターから web アプリのステージング環境にマニアクイズアプリケーションを直接発行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="c62bf-336">ポータルに戻り、 **[名前]** 列の下にある web アプリの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![Web アプリ管理ページを開く](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="c62bf-338">*Web アプリ管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="c62bf-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="c62bf-339">**[スケール]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="c62bf-340">**[全般]** セクションで、構成の **[標準]** を選択し、コマンドバーの **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-341">現在のリージョンとサブスクリプションのすべての web アプリを**標準**モードで実行するには、 **[サイトの選択]** 構成で **[すべて選択**] チェックボックスをオンのままにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="c62bf-342">それ以外の場合は、 **[すべて選択**] チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="c62bf-343">![Web アプリを標準モードにアップグレードする](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Web アプリを標準モードにアップグレードする")</span><span class="sxs-lookup"><span data-stu-id="c62bf-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="c62bf-344">*Web アプリを標準モードにアップグレードする*</span><span class="sxs-lookup"><span data-stu-id="c62bf-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="c62bf-345">**[はい]** をクリックして変更を確定します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="c62bf-346">![標準モードへの変更を確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Web アプリモードの変更を続行しています")</span><span class="sxs-lookup"><span data-stu-id="c62bf-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="c62bf-347">*標準モードへの変更を確認しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="c62bf-348">**[ダッシュボード]** ページにアクセスし、[概要 **] セクションの**ステージングされた **[発行を有効にする]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="c62bf-349">![ステージングされる発行の有効化](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "ステージングされる発行の有効化")</span><span class="sxs-lookup"><span data-stu-id="c62bf-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="c62bf-350">*ステージングされる発行の有効化*</span><span class="sxs-lookup"><span data-stu-id="c62bf-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="c62bf-351">**[はい]** をクリックしてステージングされた発行を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="c62bf-352">![ステージングされる発行の確認](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "[はい] をクリックしてステージングされる発行を有効にする")</span><span class="sxs-lookup"><span data-stu-id="c62bf-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="c62bf-353">*ステージングされる発行の確認*</span><span class="sxs-lookup"><span data-stu-id="c62bf-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="c62bf-354">Web アプリの一覧で、web アプリ名の左側にあるマークを展開し、ステージングサイトスロットを表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="c62bf-355">これには、web アプリの名前の後に ***(ステージング)*** が続きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="c62bf-356">[ステージングサイト] をクリックして、管理ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="c62bf-357">![ステージング web アプリへの移動](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "ステージング web アプリへの移動")</span><span class="sxs-lookup"><span data-stu-id="c62bf-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="c62bf-358">*ステージングアプリへの移動*</span><span class="sxs-lookup"><span data-stu-id="c62bf-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="c62bf-359">管理ページは他の web アプリの管理ページのように見えます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="c62bf-360">**[デプロイ]** ページに移動し、 **[Git URL]** の値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="c62bf-361">この演習では、後で使用します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-361">You will use it later in this exercise.</span></span>

    ![Git URL 値をコピーしています](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="c62bf-363">*Git URL 値をコピーしています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="c62bf-364">新しい**Git Bash**コンソールを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="c62bf-365">このラボの**Source\Ex1-DeployingWebSiteToStaging\Begin**フォルダーにある**GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初期化と最初のコミット](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="c62bf-367">*Git 初期化と最初のコミット*</span><span class="sxs-lookup"><span data-stu-id="c62bf-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="c62bf-368">次のコマンドを実行して、web アプリをリモート**Git**リポジトリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="c62bf-369">プレースホルダーは、管理ポータルから取得した URL に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="c62bf-370">デプロイパスワードを入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure へのプッシュ](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="c62bf-372">*Azure へのプッシュ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-373">Web アプリの FTP ホストまたは GIT リポジトリにコンテンツをデプロイする場合は、web アプリの **[クイックスタート]** または **[ダッシュボード]** 管理ページから作成した**デプロイ資格情報**を使用して認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="c62bf-374">デプロイ資格情報がわからない場合は、管理ポータルを使用して簡単にリセットできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="c62bf-375">Web アプリの**ダッシュボード**ページを開き、 **[デプロイ資格情報のリセット]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="c62bf-376">新しいパスワードを入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="c62bf-377">デプロイ資格情報は、サブスクリプションに関連付けられているすべての web アプリで使用できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="c62bf-378">Web アプリが Azure に正常にプッシュされたことを確認するには、管理ポータルに戻り、 **[Web サイト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="c62bf-379">Web アプリを検索し、エントリを展開してステージングサイトスロットを表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="c62bf-380">**[名前]** をクリックして、管理ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="c62bf-381">**デプロイの履歴**を表示するには、 **[デプロイ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="c62bf-382">*&quot;の初期コミット&quot;* で**アクティブなデプロイ**があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![アクティブな配置](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="c62bf-384">*アクティブな配置*</span><span class="sxs-lookup"><span data-stu-id="c62bf-384">*Active deployment*</span></span>
13. <span data-ttu-id="c62bf-385">最後に、コマンドバーの **[参照]** をクリックして、web アプリに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![Web アプリの参照](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="c62bf-387">*Web アプリの参照*</span><span class="sxs-lookup"><span data-stu-id="c62bf-387">*Browse web app*</span></span>
14. <span data-ttu-id="c62bf-388">アプリケーションが正常にデプロイされた場合は、マニアクイズログインページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-389">デプロイされたアプリケーションのアドレス URL には、web アプリの名前と*ステージング*が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![ステージング環境で実行されているアプリケーション](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="c62bf-391">*ステージング環境で実行されているアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="c62bf-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="c62bf-392">アプリケーションを調査する場合は、 **[登録]** をクリックして新しいユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="c62bf-393">ユーザー名、電子メールアドレス、パスワードを入力して、アカウントの詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="c62bf-394">次に、アプリケーションはクイズの最初の質問を表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="c62bf-395">いくつかの質問に答えて、想定どおりに動作していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![使用する準備ができているアプリケーション](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="c62bf-397">*使用する準備ができているアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="c62bf-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="c62bf-398">タスク 4-Web アプリを運用環境に昇格する</span><span class="sxs-lookup"><span data-stu-id="c62bf-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="c62bf-399">これで、web アプリがステージング環境で正常に動作していることを確認できたので、運用環境に昇格させることができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="c62bf-400">このタスクでは、ステージングサイトスロットと運用サイトスロットをスワップします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="c62bf-401">管理ポータルに戻り、ステージングサイトスロットを選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="c62bf-402">コマンドバーの **[スワップ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-402">Click **Swap** in the command bar.</span></span>

    ![運用環境に切り替える](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="c62bf-404">*運用環境に切り替える*</span><span class="sxs-lookup"><span data-stu-id="c62bf-404">*Swap to production*</span></span>
2. <span data-ttu-id="c62bf-405">確認ダイアログボックスで **[はい]** をクリックして、スワップ操作を続行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="c62bf-406">Azure では、運用サイトのコンテンツとステージングサイトのコンテンツが即座に交換されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-407">ステージングバージョンの一部の設定は、自動的に運用バージョン (接続文字列の上書き、ハンドラーマッピングなど) にコピーされますが、その他の設定は変更されません (DNS エンドポイント、SSL バインドなど)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![スワップ操作を確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="c62bf-409">*スワップ操作を確認しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="c62bf-410">スワップが完了したら、運用スロットを選択し、コマンドバーの **[参照]** をクリックして運用サイトを開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="c62bf-411">アドレスバーに URL が表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-412">キャッシュをクリアするには、ブラウザーを更新する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="c62bf-413">Internet Explorer では、CTRL キーを押し**ながら R**キーを押すと、この操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![運用環境で実行されている Web アプリ](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="c62bf-415">**GitBash**コンソールで、ローカル Git リポジトリのリモート URL を更新して、運用スロットを対象にします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="c62bf-416">これを行うには、次のコマンドを実行します。プレースホルダーは、デプロイユーザー名と web アプリの名前に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-417">次の演習では、ラボを簡単にするためだけに、ステージングではなく運用サイトに変更をプッシュします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="c62bf-418">実際のシナリオでは、運用環境に昇格する前にステージング環境の変更を確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="c62bf-419">演習 3: 運用環境で展開のロールバックを実行する</span><span class="sxs-lookup"><span data-stu-id="c62bf-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="c62bf-420">ステージングと運用の間でホットスワップを実行するステージングスロットがない場合 (たとえば、 **Free**モードまたは**共有**モードを使用している場合)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="c62bf-421">これらのシナリオでは、実稼働環境に配置する前に、ローカルまたはリモートサイトでテスト環境でアプリケーションをテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="c62bf-422">ただし、テストフェーズ中に検出されない問題が運用サイトで発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="c62bf-423">この場合、できるだけ早く、より安定したバージョンのアプリケーションに簡単に切り替えるメカニズムを用意することが重要です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="c62bf-424">**Azure App Service**では、ソース管理からの継続的なデプロイによって、管理ポータルで使用できる再**デプロイ**アクションが発生します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="c62bf-425">Azure では、リポジトリにプッシュされたコミットに関連付けられているデプロイを追跡し、いつでも以前のデプロイを使用してアプリケーションを再デプロイするオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="c62bf-426">この演習では、*バグ*を意図的に挿入する**マニアクイズ**アプリケーションのコードに変更を行います。</span><span class="sxs-lookup"><span data-stu-id="c62bf-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="c62bf-427">アプリケーションを運用環境にデプロイしてエラーを確認した後、再デプロイ機能を利用して前の状態に戻ります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="c62bf-428">タスク1–マニアクイズアプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="c62bf-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="c62bf-429">このタスクでは、 **TriviaController**クラスの小さな部分のコードをリファクターして、選択したクイズオプションをデータベースから新しいメソッドに取得するロジックの一部を抽出します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="c62bf-430">前の演習で**GeekQuiz**ソリューションを使用して Visual Studio インスタンスに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="c62bf-431">**ソリューションエクスプローラー**で、 **Controllers**フォルダー内の**TriviaController.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="c62bf-432">**StoreAsync**メソッドを見つけて、次の図で強調表示されているコードを選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![コードの選択](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="c62bf-434">*コードの選択*</span><span class="sxs-lookup"><span data-stu-id="c62bf-434">*Selecting the code*</span></span>
4. <span data-ttu-id="c62bf-435">選択したコードを右クリックし、 **[リファクター]** メニューを展開して **[メソッドの抽出...]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![新しいメソッドとしてのコードの抽出](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="c62bf-437">*Extract メソッドの選択*</span><span class="sxs-lookup"><span data-stu-id="c62bf-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="c62bf-438">**[メソッドの抽出]** ダイアログボックスで、新しいメソッドに*MatchesOption*という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![メソッド名の指定](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="c62bf-440">*抽出されたメソッドの名前を指定する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="c62bf-441">次に、選択したコードを**MatchesOption**メソッドに抽出します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="c62bf-442">結果のコードは、次のスニペットに示されています。</span><span class="sxs-lookup"><span data-stu-id="c62bf-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="c62bf-443">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="c62bf-444">タスク2–マニアクイズアプリケーションを再展開する</span><span class="sxs-lookup"><span data-stu-id="c62bf-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="c62bf-445">次に、前のタスクで行った変更をリポジトリにプッシュします。これにより、運用環境への新しいデプロイがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="c62bf-446">次に、Internet Explorer に用意されている**F12 開発ツール**を使用して問題を解決してから、Azure 管理ポータルから以前のデプロイへのロールバックを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="c62bf-447">新しい**Git Bash**コンソールを開き、Azure App Service に更新されたアプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="c62bf-448">次のコマンドを実行して、変更を Azure にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="c62bf-449">**GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="c62bf-450">デプロイパスワードを入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![リファクタリングされるコードを Azure にプッシュする](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="c62bf-452">*リファクタリングされるコードを Azure にプッシュする*</span><span class="sxs-lookup"><span data-stu-id="c62bf-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="c62bf-453">Internet Explorer を開き、web アプリに移動します (例: `http://<your-web-site>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="c62bf-454">以前に作成した資格情報を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="c62bf-455">**F12**キーを押して開発ツールを起動し、 **[ネットワーク]** タブを選択し、 **[再生]** ボタンをクリックして記録を開始します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="c62bf-456">![ネットワーク記録の開始](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "ネットワーク記録の開始")</span><span class="sxs-lookup"><span data-stu-id="c62bf-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="c62bf-457">*ネットワーク記録の開始*</span><span class="sxs-lookup"><span data-stu-id="c62bf-457">*Starting network recording*</span></span>
5. <span data-ttu-id="c62bf-458">クイズの任意のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-458">Select any option of the quiz.</span></span> <span data-ttu-id="c62bf-459">何も起こらないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="c62bf-460">**F12**ウィンドウで、POST http 要求に対応するエントリに http **500**の結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 エラー](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="c62bf-462">*HTTP 500 エラー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="c62bf-463">**[コンソール]** タブを選択します。エラーは、原因の詳細と共に記録されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![ログに記録されたエラー](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="c62bf-465">*ログに記録されたエラー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-465">*Logged error*</span></span>
8. <span data-ttu-id="c62bf-466">エラーの詳細部分を見つけます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-466">Locate the details part of the error.</span></span> <span data-ttu-id="c62bf-467">明らかに、このエラーは、前の手順でコミットしたコードリファクタリングが原因で発生します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="c62bf-468">[https://login.microsoftonline.com/consumers/](`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`)</span><span class="sxs-lookup"><span data-stu-id="c62bf-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="c62bf-469">ブラウザーを閉じないでください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-469">Do not close the browser.</span></span>
10. <span data-ttu-id="c62bf-470">新しいブラウザーインスタンスで、 [Azure 管理ポータル](https://manage.windowsazure.com)に移動し、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="c62bf-471">**[Web サイト]** を選択し、演習2で作成した web アプリをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="c62bf-472">**[デプロイ]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="c62bf-473">実行されたすべてのコミットがデプロイ履歴に表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![既存の展開の一覧](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="c62bf-475">*既存の展開の一覧*</span><span class="sxs-lookup"><span data-stu-id="c62bf-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="c62bf-476">以前のコミットを選択し、コマンドバーの [再**デプロイ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![前回のコミットの再デプロイ](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="c62bf-478">*前回のコミットの再デプロイ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="c62bf-479">確認メッセージが表示されたら、 **[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-479">When prompted to confirm, click **Yes**.</span></span>

    ![再展開の確認](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="c62bf-481">デプロイが完了したら、web アプリでブラウザーインスタンスに戻り、Ctrl キーを押し**ながら F5**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="c62bf-482">いずれかのオプションをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-482">Click any of the options.</span></span> <span data-ttu-id="c62bf-483">フリップアニメーションが表示されるようになり、結果 (*正しい/正しくない*) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="c62bf-484">Optional**Git Bash**コンソールに切り替え、次のコマンドを実行して前のコミットに戻します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-485">これらのコマンドは、無効なコミットで作成された Git リポジトリ内のすべての変更を元に戻す新しいコミットを作成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="c62bf-486">その後、Azure は新しいコミットを使用してアプリケーションを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="c62bf-487">演習 4: Azure Storage を使用したスケーリング</span><span class="sxs-lookup"><span data-stu-id="c62bf-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="c62bf-488">**Blob**は、大量の非構造化テキストまたはバイナリデータ (ビデオ、オーディオ、画像など) を格納する最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="c62bf-489">アプリケーションの静的コンテンツをストレージに移行することで、イメージまたはドキュメントを直接ブラウザーに提供してアプリケーションを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="c62bf-490">この演習では、アプリケーションの静的コンテンツを Blob コンテナーに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="c62bf-491">次に、コンテンツを Blob コンテナーに**リダイレクトするために、** web.config で**ASP.NET URL 書き換えルール**を追加するようにアプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="c62bf-492">タスク1– Azure Storage アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="c62bf-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="c62bf-493">このタスクでは、管理ポータルを使用して新しいストレージアカウントを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="c62bf-494">[Azure 管理ポータル](https://manage.windowsazure.com)に移動し、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="c62bf-495">新規 を選択します。 **Data Services |Storage |簡易作成**を実行して、新しいストレージアカウントの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="c62bf-496">アカウントの一意の名前を入力し、一覧から**リージョン**を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="c62bf-497">**[ストレージアカウントの作成]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="c62bf-498">![新しいストレージアカウントを作成する](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "新しいストレージアカウントを作成する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="c62bf-499">*新しいストレージアカウントを作成する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="c62bf-500">**[ストレージ]** セクションで、新しいストレージアカウントの状態が [*オンライン*] に変わるまで待ってから、次の手順に進みます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="c62bf-501">![作成されたストレージアカウント](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "作成されたストレージアカウント")</span><span class="sxs-lookup"><span data-stu-id="c62bf-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="c62bf-502">*作成されたストレージアカウント*</span><span class="sxs-lookup"><span data-stu-id="c62bf-502">*Storage Account created*</span></span>
4. <span data-ttu-id="c62bf-503">ストレージアカウント名をクリックし、ページの上部にある **[ダッシュボード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="c62bf-504">**[ダッシュボード]** ページには、アカウントの状態と、アプリケーション内で使用できるサービスエンドポイントに関する情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="c62bf-505">![ストレージアカウントダッシュボードの表示](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "ストレージアカウントダッシュボードの表示")</span><span class="sxs-lookup"><span data-stu-id="c62bf-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="c62bf-506">*ストレージアカウントダッシュボードの表示*</span><span class="sxs-lookup"><span data-stu-id="c62bf-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="c62bf-507">ナビゲーションバーの **[アクセスキーの管理]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="c62bf-508">![[アクセスキーの管理] ボタン](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "[アクセスキーの管理] ボタン")</span><span class="sxs-lookup"><span data-stu-id="c62bf-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="c62bf-509">*[アクセスキーの管理] ボタン*</span><span class="sxs-lookup"><span data-stu-id="c62bf-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="c62bf-510">**[アクセスキーの管理]** ダイアログボックスで、**ストレージアカウント名**と**プライマリアクセスキー**をコピーします。次の演習で必要になります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="c62bf-511">次に、ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="c62bf-512">![[アクセスキーの管理] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "[アクセスキーの管理] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="c62bf-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="c62bf-513">*[アクセスキーの管理] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="c62bf-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="c62bf-514">タスク2– Azure Blob Storage に資産をアップロードする</span><span class="sxs-lookup"><span data-stu-id="c62bf-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="c62bf-515">このタスクでは、Visual Studio の [サーバーエクスプローラー] ウィンドウを使用して、ストレージアカウントに接続します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="c62bf-516">次に、blob コンテナーを作成し、マニアクイズロゴを含むファイルをコンテナーにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="c62bf-517">前の演習で**GeekQuiz**ソリューションを使用して Visual Studio インスタンスに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="c62bf-518">メニューバーから **[表示]** を選択し、 **[サーバーエクスプローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="c62bf-519">**サーバーエクスプローラー**で、 **[azure]** ノードを右クリックし、 **[azure に接続]** を選択します。サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Windows Azure へ接続](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="c62bf-521">*Azure への接続*</span><span class="sxs-lookup"><span data-stu-id="c62bf-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="c62bf-522">**[Azure]** ノードを展開し、 **[ストレージ]** を右クリックして、 **[外部ストレージの接続]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="c62bf-523">**[新しいストレージアカウントの追加]** ダイアログボックスで、前のタスクで取得した**アカウント名**と**アカウントキー**を入力し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![[新しいストレージアカウントの追加] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="c62bf-525">*[新しいストレージアカウントの追加] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="c62bf-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="c62bf-526">ストレージ**ノードの下にストレージ**アカウントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="c62bf-527">ストレージアカウントを展開し、 **[blob]** を右クリックして、 **[Blob コンテナーの作成...]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="c62bf-528">![Blob コンテナーの作成](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "BLOB コンテナーの作成")</span><span class="sxs-lookup"><span data-stu-id="c62bf-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="c62bf-529">*Blob コンテナーの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="c62bf-530">**[Blob コンテナーの作成]** ダイアログボックスで、blob コンテナーの名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="c62bf-531">![[Blob コンテナーの作成] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "[Blob コンテナーの作成] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="c62bf-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="c62bf-532">*[Blob コンテナーの作成] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="c62bf-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="c62bf-533">新しい blob コンテナーを**blob**ノードに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="c62bf-534">コンテナーのアクセス許可を変更して、コンテナーをパブリックにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="c62bf-535">これを行うには、 **images**コンテナーを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="c62bf-536">![images コンテナーのプロパティ](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images コンテナーのプロパティ")</span><span class="sxs-lookup"><span data-stu-id="c62bf-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="c62bf-537">*Images コンテナーのプロパティ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-537">*Images container properties*</span></span>
9. <span data-ttu-id="c62bf-538">**[プロパティ]** ウィンドウで、 **[パブリック読み取りアクセス]** を **[コンテナー]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="c62bf-539">![パブリック読み取りアクセスプロパティの変更](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "パブリック読み取りアクセスプロパティの変更")</span><span class="sxs-lookup"><span data-stu-id="c62bf-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="c62bf-540">*パブリック読み取りアクセスプロパティの変更*</span><span class="sxs-lookup"><span data-stu-id="c62bf-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="c62bf-541">パブリックアクセスプロパティを変更するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="c62bf-542">![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="c62bf-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="c62bf-543">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="c62bf-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="c62bf-544">**サーバーエクスプローラー**で、 **images** blob コンテナー内を右クリックし、 **[blob コンテナーの表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="c62bf-545">![Blob コンテナーの表示](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob コンテナーの表示")</span><span class="sxs-lookup"><span data-stu-id="c62bf-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="c62bf-546">*Blob コンテナーの表示*</span><span class="sxs-lookup"><span data-stu-id="c62bf-546">*View Blob Container*</span></span>
12. <span data-ttu-id="c62bf-547">新しいウィンドウで images コンテナーが開き、エントリのない凡例が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="c62bf-548">**アップロード**アイコンをクリックして、ファイルを blob コンテナーにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="c62bf-549">![エントリのないイメージコンテナー](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "エントリのないイメージコンテナー")</span><span class="sxs-lookup"><span data-stu-id="c62bf-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="c62bf-550">*エントリのないイメージコンテナー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="c62bf-551">**[Blob のアップロード]** ダイアログボックスで、ラボの**Assets**フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="c62bf-552">**Logo-big**ファイルを選択し、 **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="c62bf-553">ファイルがアップロードされるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="c62bf-554">アップロードが完了すると、[images] コンテナーにファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="c62bf-555">ファイルエントリを右クリックし、 **[URL のコピー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="c62bf-556">![Blob URL のコピー](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob ファイルの URL のコピー")</span><span class="sxs-lookup"><span data-stu-id="c62bf-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="c62bf-557">*Blob URL のコピー*</span><span class="sxs-lookup"><span data-stu-id="c62bf-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="c62bf-558">Internet Explorer を開き、URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="c62bf-559">次の画像がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="c62bf-560">![Windows Blob Storage からの logo-big イメージ](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "ストレージからの logo-big イメージ")</span><span class="sxs-lookup"><span data-stu-id="c62bf-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="c62bf-561">*Azure Blob Storage からの logo-big イメージ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="c62bf-562">タスク3– Azure Blob Storage からの静的コンテンツを使用するようにソリューションを更新する</span><span class="sxs-lookup"><span data-stu-id="c62bf-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="c62bf-563">このタスクでは、 **web.config ファイルに**ASP.NET URL 書き換えルールを追加することによって、(web アプリに存在するイメージではなく) Azure Blob Storage にアップロードされたイメージを使用するように**GeekQuiz**ソリューションを構成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="c62bf-564">Visual Studio で、 **GeekQuiz**プロジェクト**内の web.config ファイルを**開き、 **&lt;system.webserver&gt;** 要素を見つけます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="c62bf-565">次のコードを追加して、URL 書き換えルールを追加し、プレースホルダーをストレージアカウント名で更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="c62bf-566">(コードスニペット- *webEx4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="c62bf-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="c62bf-567">URL 書き換えは、受信 Web 要求をインターセプトし、要求を別のリソースにリダイレクトするプロセスです。</span><span class="sxs-lookup"><span data-stu-id="c62bf-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="c62bf-568">URL 書き換え規則は、要求をリダイレクトする必要がある場合や、要求をリダイレクトする必要がある場合に、リライトエンジンに通知します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="c62bf-569">書き換え規則は2つの文字列で構成されます。要求された URL で検索するパターン (通常は正規表現を使用) と、パターンを置換する文字列 (見つかった場合) です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="c62bf-570">詳細については、「 [ASP.NET での URL の書き換え](https://msdn.microsoft.com/library/ms972974.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="c62bf-571">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="c62bf-572">新しい**Git Bash**コンソールを開き、Azure App Service に更新されたアプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="c62bf-573">次のコマンドを実行して、変更を Azure にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="c62bf-574">**GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="c62bf-575">デプロイパスワードを入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure への更新プログラムのデプロイ](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="c62bf-577">*Azure への更新プログラムのデプロイ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="c62bf-578">タスク4–検証</span><span class="sxs-lookup"><span data-stu-id="c62bf-578">Task 4 – Verification</span></span>

<span data-ttu-id="c62bf-579">このタスクでは、 **Internet Explorer**を使用して**マニアクイズ**アプリケーションを参照し、イメージの URL 書き換えルールが動作し、 **Azure Blob Storage**でホストされているイメージにリダイレクトされることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="c62bf-580">Internet Explorer を開き、web アプリに移動します (例: `http://<your-web-site>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="c62bf-581">以前に作成した資格情報を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="c62bf-582">![イメージを使用したマニアクイズ web アプリの表示](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "イメージを使用したマニアクイズ web アプリの表示")</span><span class="sxs-lookup"><span data-stu-id="c62bf-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="c62bf-583">*イメージを使用したマニアクイズ web アプリの表示*</span><span class="sxs-lookup"><span data-stu-id="c62bf-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="c62bf-584">**F12**キーを押して開発ツールを起動し、 **[ネットワーク]** タブを選択して記録を開始します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="c62bf-585">![ネットワーク記録の開始](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "ネットワーク記録の開始")</span><span class="sxs-lookup"><span data-stu-id="c62bf-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="c62bf-586">*ネットワーク記録の開始*</span><span class="sxs-lookup"><span data-stu-id="c62bf-586">*Starting network recording*</span></span>
3. <span data-ttu-id="c62bf-587">CTRL キーを押し**ながら F5**キーを押して、web ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="c62bf-588">ページの読み込みが完了すると、http **301**の結果 (リダイレクト) と、http **200**の結果を含む `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url に対する別の要求で、 **/img/logo-big.png** url に対する http 要求が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="c62bf-589">![URL リダイレクトを確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "開発ツールでのリダイレクトの表示")</span><span class="sxs-lookup"><span data-stu-id="c62bf-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="c62bf-590">*URL リダイレクトを確認しています*</span><span class="sxs-lookup"><span data-stu-id="c62bf-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="c62bf-591">演習 5: Web Apps に自動スケールを使用する</span><span class="sxs-lookup"><span data-stu-id="c62bf-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="c62bf-592">この演習は、 **Visual Studio 2013 Ultimate Edition**でのみ利用可能な Web ロード &amp; パフォーマンステストをサポートする必要があるため、省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c62bf-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="c62bf-593">特定の Visual Studio 2013 機能の詳細について[は、ここで](https://www.microsoft.com/visualstudio/eng/products/compare)バージョンを比較してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="c62bf-594">**Azure App Service Web Apps**は、**標準モード**で実行されている Web アプリの自動スケール機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="c62bf-595">自動スケールを使用すると、負荷に応じて Azure で web アプリのインスタンス数を自動的にスケーリングできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="c62bf-596">自動スケールが有効になっている場合、Azure は web アプリの CPU を5分ごとに確認し、その時点で必要に応じてインスタンスを追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="c62bf-597">CPU 使用率が低い場合、Azure は2時間ごとにインスタンスを削除して、web アプリのパフォーマンスが低下しないようにします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="c62bf-598">この演習では、**マニアクイズ**web アプリの**自動スケール**機能を構成するために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="c62bf-599">この機能を確認するには、Visual Studio ロードテストを実行して、インスタンスのアップグレードをトリガーするためにアプリケーションに十分な CPU 負荷を生成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="c62bf-600">タスク 1-CPU メトリックに基づいて自動スケールを構成する</span><span class="sxs-lookup"><span data-stu-id="c62bf-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="c62bf-601">このタスクでは、Azure 管理ポータルを使用して、演習2で作成した web アプリの自動スケール機能を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="c62bf-602">[Microsoft Azure 管理ポータル](https://manage.windowsazure.com/)で、 **[web サイト]** を選択し、演習2で作成した web アプリをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="c62bf-603">**[スケール]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="c62bf-604">**[容量]** セクションで、 **[メトリックによるスケール]** 構成の **[CPU]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-605">CPU によってスケーリングする場合、CPU の使用率が変化した場合にアプリが使用するインスタンスの数が Azure によって動的に調整されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="c62bf-606">![CPU によるスケールの選択](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "自動スケーリングの CPU メトリックの選択")</span><span class="sxs-lookup"><span data-stu-id="c62bf-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="c62bf-607">*CPU によるスケールの選択*</span><span class="sxs-lookup"><span data-stu-id="c62bf-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="c62bf-608">**ターゲット CPU**構成を**20**-**40** % に変更します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-609">この範囲は、web アプリの平均 CPU 使用率を表します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="c62bf-610">Azure では、web アプリをこの範囲内に維持するためにインスタンスを追加または削除します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="c62bf-611">スケーリングに使用されるインスタンスの最小数と最大数は、**インスタンス数**の構成で指定されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="c62bf-612">Azure はこの制限を超えることはありません。</span><span class="sxs-lookup"><span data-stu-id="c62bf-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="c62bf-613">既定の**ターゲット CPU**値は、このラボの目的のためだけに変更されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="c62bf-614">CPU の範囲を小さい値で構成すると、アプリケーションに中程度の負荷が発生したときに自動スケールがトリガーされる可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="c62bf-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="c62bf-615">![ターゲット CPU を 20 ~ 40% に変更する](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "ターゲット CPU を 20 ~ 40% に変更する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="c62bf-616">*ターゲット CPU を 20 ~ 40% に変更する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="c62bf-617">コマンドバーの **[保存]** をクリックして、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="c62bf-618">タスク 2-Visual Studio を使用したロードテスト</span><span class="sxs-lookup"><span data-stu-id="c62bf-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="c62bf-619">**自動スケール**が構成されたので、web アプリに CPU 負荷を生成するために、Visual Studio で**Web パフォーマンスとロードテストのプロジェクト**を作成します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="c62bf-620">**Visual Studio Ultimate 2013**を開き、 **File | を選択します。新規 |プロジェクト...** を実行すると、新しいソリューションが開始されます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="c62bf-621">![新しいプロジェクトの作成](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "新しいプロジェクトを作成します。")</span><span class="sxs-lookup"><span data-stu-id="c62bf-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="c62bf-622">*新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-622">*Creating a new project*</span></span>
2. <span data-ttu-id="c62bf-623">**[新しいプロジェクト]** ダイアログボックスで、 **[Web パフォーマンスとロードテストのプロジェクト]** を選択します。  **C#[テスト**] タブ。 **.NET Framework 4.5**が選択されていることを確認し、プロジェクトに*WebAndLoadTestProject*という名前を設定して、**場所**を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="c62bf-624">![新しい Web およびロードテストプロジェクトの作成](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "新しい Web およびロードテストプロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="c62bf-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="c62bf-625">*新しい Web およびロードテストプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="c62bf-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="c62bf-626">Webtest1.webtest で、 **Web テスト** **Webtest1.webtest**ノードを右クリックし、 **[要求の追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="c62bf-627">![Webtest1.webtest への要求の追加](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Webtest1.webtest への要求の追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="c62bf-628">*Webtest1.webtest への要求の追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="c62bf-629">新しい要求 ノードの **[プロパティ]** ウィンドウで、 **[url]** プロパティを web アプリの url を指すように更新します (例: *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* )。</span><span class="sxs-lookup"><span data-stu-id="c62bf-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="c62bf-630">![Url プロパティの変更](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url プロパティの変更")</span><span class="sxs-lookup"><span data-stu-id="c62bf-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="c62bf-631">*Url プロパティの変更*</span><span class="sxs-lookup"><span data-stu-id="c62bf-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="c62bf-632">**Webtest1.webtest**ウィンドウで、 **[webtest1.webtest]** を右クリックし、 **[ループの追加...]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="c62bf-633">![Webtest1.webtest へのループの追加](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Webtest1.webtest へのループの追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="c62bf-634">*Webtest1.webtest へのループの追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="c62bf-635">**[条件付き規則と項目をループに追加]** ダイアログボックスで、 **for ループ**規則を選択し、次のプロパティを変更します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="c62bf-636">**終了値:** 1000</span><span class="sxs-lookup"><span data-stu-id="c62bf-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="c62bf-637">**コンテキストパラメーター名:** 反</span><span class="sxs-lookup"><span data-stu-id="c62bf-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="c62bf-638">**増分値:** 1</span><span class="sxs-lookup"><span data-stu-id="c62bf-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="c62bf-639">![For ループルールを選択してプロパティを更新する](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For ループルールを選択してプロパティを更新する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="c62bf-640">*For ループルールを選択してプロパティを更新する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="c62bf-641">**[ループ内の項目]** セクションで、ループの最初と最後の項目として以前に作成した要求を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="c62bf-642">続行するには、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="c62bf-643">![ループの最初と最後の項目を選択する](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "ループの最初と最後の項目を選択する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="c62bf-644">*ループの最初と最後の項目を選択する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="c62bf-645">**ソリューションエクスプローラー**で、 **WebAndLoadTestProject**プロジェクトを右クリックし、 **[追加]** メニューを展開して、 **[ロードテスト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="c62bf-646">![WebAndLoadTestProject プロジェクトへのロードテストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject プロジェクトへのロードテストの追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="c62bf-647">*WebAndLoadTestProject プロジェクトへのロードテストの追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="c62bf-648">**[新しいロードテストウィザード]** ダイアログボックスで、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="c62bf-649">![新しいロードテストウィザード](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新しいロードテストウィザード")</span><span class="sxs-lookup"><span data-stu-id="c62bf-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="c62bf-650">*新しいロードテストウィザード*</span><span class="sxs-lookup"><span data-stu-id="c62bf-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="c62bf-651">**[シナリオ]** ページで、 **[待ち時間を使用しない]** を選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="c62bf-652">![待ち時間を使用しないことを選択する](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "待ち時間を使用しないことを選択する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="c62bf-653">*待ち時間を使用しないことを選択する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="c62bf-654">**[ロードパターン]** ページで、 **[定数読み込み]** オプションが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="c62bf-655">**[ユーザーカウント]** 設定を**250**ユーザーに変更し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="c62bf-656">![ユーザーカウントを250に変更する](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "ユーザーカウントを250に変更する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="c62bf-657">*ユーザーカウントを250に変更する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="c62bf-658">**[テストミックスモデル]** ページで、 **[順次テスト順序に基づく]** を選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="c62bf-659">![テストミックスモデルの選択](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "テストミックスモデルの選択")</span><span class="sxs-lookup"><span data-stu-id="c62bf-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="c62bf-660">*テストミックスモデルの選択*</span><span class="sxs-lookup"><span data-stu-id="c62bf-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="c62bf-661">**[テストミックスモデル]** ページで **[追加...]** をクリックして、テストをミックスに追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="c62bf-662">![テストミックスへのテストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "テストミックスへのテストの追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="c62bf-663">*テストミックスへのテストの追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="c62bf-664">**[テストの追加]** ダイアログボックスで、 **[webtest1.webtest]** をダブルクリックして、 **[選択したテスト]** の一覧にテストを追加します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="c62bf-665">続行するには、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="c62bf-666">![Webtest1.webtest テストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Webtest1.webtest テストの追加")</span><span class="sxs-lookup"><span data-stu-id="c62bf-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="c62bf-667">*Webtest1.webtest テストの追加*</span><span class="sxs-lookup"><span data-stu-id="c62bf-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="c62bf-668">**[テストミックス]** ページに戻り、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="c62bf-669">![[テストミックスの完了] ページ](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "[テストミックスの完了] ページ")</span><span class="sxs-lookup"><span data-stu-id="c62bf-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="c62bf-670">*[テストミックスの完了] ページ*</span><span class="sxs-lookup"><span data-stu-id="c62bf-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="c62bf-671">**[ネットワークミックス]** ページで、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="c62bf-672">![[ネットワークミックス] ページで [次へ] をクリックします。](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "[ネットワークミックス] ページで [次へ] をクリックします。")</span><span class="sxs-lookup"><span data-stu-id="c62bf-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="c62bf-673">*[ネットワークミックス] ページで [次へ] をクリックします。*</span><span class="sxs-lookup"><span data-stu-id="c62bf-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="c62bf-674">**[ブラウザーミックス]** ページで、ブラウザーの種類として **[Internet Explorer 10.0]** を選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="c62bf-675">![ブラウザーの種類の選択](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "ブラウザーの種類の選択")</span><span class="sxs-lookup"><span data-stu-id="c62bf-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="c62bf-676">*ブラウザーの種類の選択*</span><span class="sxs-lookup"><span data-stu-id="c62bf-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="c62bf-677">**[カウンターセット]** ページで、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="c62bf-678">![[カウンターセット] ページで [次へ] をクリックします。](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "[カウンターセット] ページで [次へ] をクリックします。")</span><span class="sxs-lookup"><span data-stu-id="c62bf-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="c62bf-679">*[カウンターセット] ページで [次へ] をクリックします。*</span><span class="sxs-lookup"><span data-stu-id="c62bf-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="c62bf-680">**[実行設定]** ページで、 **[ロードテストの期間]** を**5 分**に設定し、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="c62bf-681">![ロードテストの期間を5分に設定する](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "ロードテストの期間を5分に設定する")</span><span class="sxs-lookup"><span data-stu-id="c62bf-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="c62bf-682">*ロードテストの期間を5分に設定する*</span><span class="sxs-lookup"><span data-stu-id="c62bf-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="c62bf-683">**ソリューションエクスプローラー**で、**ローカルの設定**ファイルをダブルクリックして、テストの設定を調べます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="c62bf-684">既定では、Visual Studio はローカルコンピューターを使用してテストを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-685">または、 **Azure Test Plans**を使用して、クラウドでロードテストを実行するようにテストプロジェクトを構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="c62bf-686">Azure Test Plans は、より現実的な負荷をシミュレートし、CPU 容量、使用可能なメモリ、ネットワーク帯域幅などのローカル環境の制約を回避するクラウドベースのロードテストサービスを提供します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="c62bf-687">Azure Test Plans を使用したロードテストの実行の詳細については、「[ロードテストのシナリオ](/azure/devops/test/load-test/overview?view=vsts)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![テストの設定](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="c62bf-689">タスク 3-自動スケール検証</span><span class="sxs-lookup"><span data-stu-id="c62bf-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="c62bf-690">ここでは、前のタスクで作成したロードテストを実行し、web アプリが負荷の下でどのように動作するかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="c62bf-691">**ソリューションエクスプローラー**で、 **loadtest1.loadtest**をダブルクリックしてロードテストを開きます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="c62bf-692">![Loadtest1.loadtest を開いています。 loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Loadtest1.loadtest を開いています。 loadtest")</span><span class="sxs-lookup"><span data-stu-id="c62bf-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="c62bf-693">*Loadtest1.loadtest を開いています。 loadtest*</span><span class="sxs-lookup"><span data-stu-id="c62bf-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="c62bf-694">**Loadtest1.loadtest**ウィンドウで、ツールボックスの最初のボタンをクリックして、ロードテストを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="c62bf-695">![ロードテストの実行](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "ロードテストの実行")</span><span class="sxs-lookup"><span data-stu-id="c62bf-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="c62bf-696">*ロードテストの実行*</span><span class="sxs-lookup"><span data-stu-id="c62bf-696">*Running the load test*</span></span>
3. <span data-ttu-id="c62bf-697">ロードテストが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-698">ロードテストでは、web アプリに要求を同時に送信する複数のユーザーをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="c62bf-699">テストの実行中は、使用可能なカウンターを監視して、ロードテストの実行に関連するエラー、警告、その他の情報を検出することができます。</span><span class="sxs-lookup"><span data-stu-id="c62bf-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="c62bf-700">![ロードテストの実行中](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "ロードテストが完了するまで待機しています")</span><span class="sxs-lookup"><span data-stu-id="c62bf-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="c62bf-701">*ロードテストの実行中*</span><span class="sxs-lookup"><span data-stu-id="c62bf-701">*Load test running*</span></span>
4. <span data-ttu-id="c62bf-702">テストが完了したら、管理ポータルに戻り、web アプリの **[スケール]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="c62bf-703">**[容量]** セクションで、新しいインスタンスが自動的にデプロイされたことをグラフに表示します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![新しいインスタンスが自動的に展開されました](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="c62bf-705">*新しいインスタンスが自動的に展開されました*</span><span class="sxs-lookup"><span data-stu-id="c62bf-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c62bf-706">グラフに変更が表示されるまでに数分かかる場合があります (ページを更新するには、CTRL キーを押し**ながら F5**キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="c62bf-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="c62bf-707">何も変更されていない場合は、次のようにしてみてください。</span><span class="sxs-lookup"><span data-stu-id="c62bf-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="c62bf-708">ロードテストの期間を長くする (例: **10 分**)</span><span class="sxs-lookup"><span data-stu-id="c62bf-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="c62bf-709">Web アプリの自動スケール構成で、**ターゲット CPU**範囲の最大値と最小値を小さくします。</span><span class="sxs-lookup"><span data-stu-id="c62bf-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="c62bf-710">**Azure Test Plans**を使用して、クラウドでロードテストを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="c62bf-711">詳細情報は[こちら](/azure/devops/test/load-test/index?view=vsts)です</span><span class="sxs-lookup"><span data-stu-id="c62bf-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c62bf-712">まとめ</span><span class="sxs-lookup"><span data-stu-id="c62bf-712">Summary</span></span>

<span data-ttu-id="c62bf-713">このハンズオンラボでは、Azure の運用 web アプリにアプリケーションをセットアップしてデプロイする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="c62bf-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="c62bf-714">まず、 **Entity Framework Code First Migrations**を使用してデータベースを検出して更新した後、 **Git**を使用してサイトの新しいバージョンをデプロイし、サイトの最新の安定したバージョンへのロールバックを実行します。</span><span class="sxs-lookup"><span data-stu-id="c62bf-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="c62bf-715">また、ストレージを使用してアプリケーションを拡張し、静的コンテンツを Blob コンテナーに移動する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="c62bf-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
