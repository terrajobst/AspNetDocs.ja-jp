---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: すべてを自動化 (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457168"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="2fe89-104">すべてを自動化 (Azure を使用した実際のクラウドアプリの構築)</span><span class="sxs-lookup"><span data-stu-id="2fe89-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="2fe89-105">[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2fe89-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="2fe89-106">[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します</span><span class="sxs-lookup"><span data-stu-id="2fe89-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="2fe89-107">Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="2fe89-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="2fe89-108">ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="2fe89-109">電子書籍の概要については、[最初の章](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fe89-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="2fe89-110">最初の3つのパターンは、特にクラウドプロジェクトに対して、実際にはどのようなソフトウェア開発プロジェクトにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="2fe89-111">このパターンは、開発タスクの自動化に関するものです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="2fe89-112">手動プロセスは低速でエラーが発生しやすいため、これは重要なトピックです。可能な限り多くの機能を自動化することで、高速で信頼性の高い、アジャイルなワークフローを設定できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="2fe89-113">これは、オンプレミスの環境で自動化することが困難または不可能な多くのタスクを簡単に自動化できるため、クラウド開発にとっては一意です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="2fe89-114">たとえば、新しい web サーバーとバックエンド Vm、データベース、blob ストレージ (ファイルストレージ)、キューなどを含むテスト環境全体を設定できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="2fe89-115">DevOps ワークフロー</span><span class="sxs-lookup"><span data-stu-id="2fe89-115">DevOps Workflow</span></span>

<span data-ttu-id="2fe89-116">"DevOps" という言葉が増えています。</span><span class="sxs-lookup"><span data-stu-id="2fe89-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="2fe89-117">ソフトウェアを効率的に開発するために、開発と運用のタスクを統合する必要があるという認識から除外された用語。</span><span class="sxs-lookup"><span data-stu-id="2fe89-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="2fe89-118">有効にするワークフローの種類は、アプリを開発し、デプロイし、運用環境で使用して学習し、学習した内容に応じてそれを変更し、そのサイクルを迅速かつ確実に繰り返すことができます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="2fe89-119">成功したクラウド開発チームの中には、1日に何度もライブ環境にデプロイされているものがあります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="2fe89-120">Azure チームは、2-3 か月ごとにメジャー更新プログラムをデプロイするために使用しましたが、現時点では、2-3 日ごとにマイナー更新プログラムをリリースし、2-3 週ごとにメジャーリリースをリリースしました。</span><span class="sxs-lookup"><span data-stu-id="2fe89-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="2fe89-121">このリズムを利用することで、お客様からのフィードバックに迅速に対応することができます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="2fe89-122">そのためには、反復可能で信頼性が高く予測可能で、サイクル時間が短くなる開発および展開のサイクルを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps ワークフロー](automate-everything/_static/image1.png)

<span data-ttu-id="2fe89-124">つまり、機能についてのアイデアがあり、顧客がそれを使用してフィードバックを提供するまでの期間は、できるだけ短くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="2fe89-125">最初の3つのパターン (すべてを自動化、ソース管理、継続的な統合と配信) は、そのようなプロセスを可能にするために推奨されるベストプラクティスに関するものです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="2fe89-126">Azure の管理スクリプト</span><span class="sxs-lookup"><span data-stu-id="2fe89-126">Azure management scripts</span></span>

<span data-ttu-id="2fe89-127">[この電子ブックの概要](introduction.md)では、web ベースのコンソールである Azure 管理ポータルについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="2fe89-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="2fe89-128">管理ポータルでは、Azure にデプロイしたすべてのリソースを監視および管理できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="2fe89-129">Web アプリや Vm などのサービスを作成および削除したり、サービスを構成したり、サービス操作を監視したりするための簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="2fe89-130">これは優れたツールですが、これを使用するのは手動のプロセスです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="2fe89-131">任意のサイズの実稼働アプリケーションを開発する場合、特にチーム環境では、Azure を学習して調査し、繰り返し実行するプロセスを自動化するために、ポータル UI を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2fe89-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="2fe89-132">管理ポータルまたは Visual Studio で手動で実行できるほぼすべてのものは、REST 管理 API を呼び出すことによっても実行できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="2fe89-133">[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)を使用してスクリプトを作成することも、 [Chef](http://www.opscode.com/chef/)や[パペット](http://puppetlabs.com/puppet/what-is-puppet)などのオープンソースフレームワークを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="2fe89-134">また、Mac または Linux 環境で Bash コマンドラインツールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="2fe89-135">Azure では、これらのさまざまな環境に対して Api をスクリプト化しています。また、スクリプトではなくコードを記述する場合は、 [.net MANAGEMENT API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)を用意しています。</span><span class="sxs-lookup"><span data-stu-id="2fe89-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="2fe89-136">この問題を修正するために、テスト環境を作成し、その環境にプロジェクトを配置するプロセスを自動化する Windows PowerShell スクリプトをいくつか作成しました。これらのスクリプトの内容をいくつか確認します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="2fe89-137">環境作成スクリプト</span><span class="sxs-lookup"><span data-stu-id="2fe89-137">Environment creation script</span></span>

<span data-ttu-id="2fe89-138">まず、 *New-AzureWebsiteEnv*という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="2fe89-139">テスト用に修正プログラムをデプロイできる Azure 環境が作成されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="2fe89-140">このスクリプトが実行する主なタスクは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="2fe89-141">Web アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-141">Create a web app.</span></span>
- <span data-ttu-id="2fe89-142">ストレージ アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-142">Create a storage account.</span></span> <span data-ttu-id="2fe89-143">(後の章で説明するように、blob およびキューに対して必要です)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="2fe89-144">SQL Database サーバーと2つのデータベース (アプリケーションデータベースとメンバーシップデータベース) を作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="2fe89-145">ストレージアカウントとデータベースへのアクセスにアプリが使用する設定を Azure に格納します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="2fe89-146">デプロイを自動化するために使用される設定ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="2fe89-147">スクリプトを実行する</span><span class="sxs-lookup"><span data-stu-id="2fe89-147">Run the script</span></span>

> [!NOTE]
> <span data-ttu-id="2fe89-148">この章では、スクリプトと、それらを実行するために入力するコマンドの例を示します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="2fe89-149">このデモでは、スクリプトを実行するために必要な知識をすべて提供するわけではありません。</span><span class="sxs-lookup"><span data-stu-id="2fe89-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="2fe89-150">詳しい手順については、「[付録: Fix It サンプルアプリケーション](the-fix-it-sample-application.md#deploybase)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fe89-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>

<span data-ttu-id="2fe89-151">Azure サービスを管理する PowerShell スクリプトを実行するには、Azure PowerShell コンソールをインストールし、Azure サブスクリプションで動作するように構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="2fe89-152">セットアップが完了したら、次のようなコマンドを使用して、Fix It environment 作成スクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="2fe89-153">`Name` パラメーターは、データベースとストレージアカウントを作成するときに使用する名前を指定し、`SqlDatabasePassword` パラメーターは SQL Database 用に作成される管理者アカウントのパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="2fe89-154">他にも使用できるパラメーターがあります。これについては後で説明します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell ウィンドウ](automate-everything/_static/image2.png)

<span data-ttu-id="2fe89-156">スクリプトが終了すると、管理ポータルで作成された内容を確認できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="2fe89-157">2つのデータベースがあります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-157">You'll find two databases:</span></span>

![データベース](automate-everything/_static/image3.png)

<span data-ttu-id="2fe89-159">ストレージアカウント:</span><span class="sxs-lookup"><span data-stu-id="2fe89-159">A storage account:</span></span>

![ストレージ アカウント](automate-everything/_static/image4.png)

<span data-ttu-id="2fe89-161">と web アプリは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-161">And a web app:</span></span>

![[Web サイト]](automate-everything/_static/image5.png)

<span data-ttu-id="2fe89-163">Web アプリの **[構成]** タブで、修正プログラムのアプリ用にストレージアカウントの設定と SQL database 接続文字列が設定されていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings と connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="2fe89-165">*Automation*フォルダーには、 *&lt;websitename&gt;pubxml*ファイルも含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2fe89-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="2fe89-166">このファイルには、先ほど作成した Azure 環境にアプリケーションをデプロイするために MSBuild が使用する設定が格納されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="2fe89-167">例 :</span><span class="sxs-lookup"><span data-stu-id="2fe89-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="2fe89-168">ご覧のとおり、スクリプトは完全なテスト環境を作成し、プロセス全体は約90秒で完了しています。</span><span class="sxs-lookup"><span data-stu-id="2fe89-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="2fe89-169">チーム内の他のユーザーがテスト環境を作成しようとしている場合は、スクリプトを実行するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="2fe89-170">高速であるだけでなく、使用している環境と同一の環境を使用していることも確信できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="2fe89-171">すべてのユーザーが管理ポータル UI を使用して手動で設定した場合は、自信を持っていなくても問題ありません。</span><span class="sxs-lookup"><span data-stu-id="2fe89-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="2fe89-172">スクリプトの概要</span><span class="sxs-lookup"><span data-stu-id="2fe89-172">A look at the scripts</span></span>

<span data-ttu-id="2fe89-173">実際には、この作業を実行する3つのスクリプトがあります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="2fe89-174">コマンドラインからを呼び出すと、他の2つのタスクが自動的に使用されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="2fe89-175">*New-AzureWebSiteEnv*はメインスクリプトです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="2fe89-176">*New-AzureStorage*によってストレージアカウントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="2fe89-177">*New-AzureSql*によってデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="2fe89-178">メインスクリプトのパラメーター</span><span class="sxs-lookup"><span data-stu-id="2fe89-178">Parameters in the main script</span></span>

<span data-ttu-id="2fe89-179">メインスクリプト New-AzureWebSiteEnv では、次のいくつかのパラメーターが定義されて*い*ます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="2fe89-180">2つのパラメーターが必要です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-180">Two parameters are required:</span></span>

- <span data-ttu-id="2fe89-181">スクリプトによって作成される web アプリの名前。</span><span class="sxs-lookup"><span data-stu-id="2fe89-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="2fe89-182">(これは、URL: `<name>.azurewebsites.net`にも使用されます)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="2fe89-183">スクリプトによって作成されるデータベースサーバーの新しい管理ユーザーのパスワード。</span><span class="sxs-lookup"><span data-stu-id="2fe89-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="2fe89-184">省略可能なパラメーターを使用すると、データセンターの場所 (既定では "米国西部")、データベースサーバー管理者名 (既定では "dbuser")、およびデータベースサーバーのファイアウォール規則を指定できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="2fe89-185">Web アプリの作成</span><span class="sxs-lookup"><span data-stu-id="2fe89-185">Create the web app</span></span>

<span data-ttu-id="2fe89-186">最初のスクリプトでは、`New-AzureWebsite` コマンドレットを呼び出して web アプリを作成し、web アプリ名と場所のパラメーター値を渡します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="2fe89-187">ストレージ アカウントの作成</span><span class="sxs-lookup"><span data-stu-id="2fe89-187">Create the storage account</span></span>

<span data-ttu-id="2fe89-188">次に、メインスクリプトは、ストレージアカウント名に " *&lt;websitename&gt;* storage" を指定し、web アプリと同じデータセンターの場所を指定して、 *New-AzureStorage*スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;* storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="2fe89-189">*New-AzureStorage*は、`New-AzureStorageAccount` コマンドレットを呼び出してストレージアカウントを作成し、アカウント名とアクセスキーの値を返します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="2fe89-190">ストレージアカウント内の blob とキューにアクセスするには、アプリケーションにこれらの値が必要になります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="2fe89-191">常に新しいストレージアカウントを作成することはできません。必要に応じて既存のストレージアカウントを使用するように指示するパラメーターを追加することで、スクリプトを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="2fe89-192">データベースを作成する</span><span class="sxs-lookup"><span data-stu-id="2fe89-192">Create the databases</span></span>

<span data-ttu-id="2fe89-193">次に、既定のデータベースとファイアウォール規則の名前を設定した後、メインスクリプトによってデータベース作成スクリプト*New-AzureSql*が実行されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="2fe89-194">データベース作成スクリプトでは、開発用コンピューターの IP アドレスを取得し、ファイアウォール規則を設定して、開発用コンピューターがサーバーに接続して管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2fe89-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="2fe89-195">次に、データベースの作成スクリプトでは、データベースを設定するためのいくつかの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="2fe89-196">`New-AzureSqlDatabaseServer` コマンドレットを使用してサーバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="2fe89-197">開発用コンピューターがサーバーを管理し、web アプリがそれに接続できるようにするためのファイアウォール規則を作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="2fe89-198">`New-AzureSqlDatabaseServerContext` コマンドレットを使用して、サーバー名と資格情報を含むデータベースコンテキストを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="2fe89-199">`New-PSCredentialFromPlainText` は、`ConvertTo-SecureString` コマンドレットを呼び出してパスワードを暗号化し、`Get-Credential` コマンドレットが返すのと同じ型である `PSCredential` オブジェクトを返す、スクリプト内の関数です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="2fe89-200">`New-AzureSqlDatabase` コマンドレットを使用して、アプリケーションデータベースとメンバーシップデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="2fe89-201">ローカルに定義された関数を呼び出して、各データベースの接続文字列を作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-201">Calls a locally defined function to create a connection string for each database.</span></span> <span data-ttu-id="2fe89-202">アプリケーションは、これらの接続文字列を使用してデータベースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="2fe89-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="2fe89-203">SQLAzureDatabaseConnectionString は、指定されたパラメーター値から接続文字列を作成するスクリプトで定義された関数です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="2fe89-204">データベースサーバー名と接続文字列を含むハッシュテーブルを返します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="2fe89-205">Fix It アプリでは、個別のメンバーシップとアプリケーションデータベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="2fe89-206">メンバーシップとアプリケーションの両方のデータを1つのデータベースに格納することもできます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="2fe89-207">アプリの設定と接続文字列を保存する</span><span class="sxs-lookup"><span data-stu-id="2fe89-207">Store app settings and connection strings</span></span>

<span data-ttu-id="2fe89-208">Azure には、設定と接続文字列を格納する機能があります。この機能を使用すると、Web.config ファイルで `appSettings` または `connectionStrings` コレクションを読み取ろうとしたときに、アプリケーションに返される内容を自動的に上書きすることができます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="2fe89-209">これは、の配置時に web.config[変換](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)を適用する代わりに使用します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="2fe89-210">詳細については、この電子ブックの「[機微なデータを Azure に保存](source-control.md#appsettings)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fe89-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="2fe89-211">環境作成スクリプトは、azure で実行するときに、アプリケーションがストレージアカウントとデータベースにアクセスするために必要なすべての `appSettings` と `connectionStrings` の値を Azure に格納します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="2fe89-212">[新しい聖箱](http://newrelic.com/)は、[監視とテレメトリ](monitoring-and-telemetry.md)の章で説明しているテレメトリフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="2fe89-213">また、環境作成スクリプトによって web アプリが再起動され、新しい聖なる値が確実に取得されるようになります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="2fe89-214">展開の準備</span><span class="sxs-lookup"><span data-stu-id="2fe89-214">Preparing for deployment</span></span>

<span data-ttu-id="2fe89-215">プロセスの最後に、環境作成スクリプトは2つの関数を呼び出して、配置スクリプトで使用されるファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="2fe89-216">これらの関数のいずれかによって、発行プロファイル *(&lt;websitename&gt;pubxml*ファイル) が作成されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="2fe89-217">このコードは、Azure REST API を呼び出して発行設定を取得し、情報を *.publishsettings*ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="2fe89-218">次に、そのファイルの情報をテンプレートファイル (*pubxml. template*) と共に使用して、発行プロファイルを含む*pubxml*ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="2fe89-219">この2段階のプロセスでは、Visual Studio での作業をシミュレートします。 *.publishsettings*ファイルをダウンロードし、それをインポートして発行プロファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="2fe89-220">もう1つの関数は、別のテンプレートファイル (website-environment) を使用して、配置スクリプトが*pubxml*ファイルと共に使用する設定を含むファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="2fe89-221">トラブルシューティングとエラー処理</span><span class="sxs-lookup"><span data-stu-id="2fe89-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="2fe89-222">スクリプトはプログラムに似ています。エラーが発生する可能性があり、エラーの原因と原因を把握したい場合があります。</span><span class="sxs-lookup"><span data-stu-id="2fe89-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="2fe89-223">このため、環境作成スクリプトは、すべての詳細メッセージが表示されるように、`VerbosePreference` 変数の値を `SilentlyContinue` から `Continue` に変更します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="2fe89-224">また、`ErrorActionPreference` 変数の値を `Continue` から `Stop`に変更し、終了しないエラーが発生した場合でもスクリプトが停止するようにします。</span><span class="sxs-lookup"><span data-stu-id="2fe89-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="2fe89-225">作業を行う前に、スクリプトは開始時刻を格納して、完了した経過時間を計算できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2fe89-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="2fe89-226">処理が完了すると、スクリプトによって経過時間が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="2fe89-227">また、すべてのキー操作について、スクリプトは詳細なメッセージを書き込みます。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="2fe89-228">デプロイ スクリプト</span><span class="sxs-lookup"><span data-stu-id="2fe89-228">Deployment script</span></span>

<span data-ttu-id="2fe89-229">*New-AzureWebsiteEnv*スクリプトは、環境の作成に使用されます。 *Publish-AzureWebsite*スクリプトは、アプリケーションの展開に使用します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="2fe89-230">デプロイスクリプトは、環境作成スクリプトによって作成された*website-environment*ファイルから web アプリの名前を取得します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="2fe89-231">次のように、 *.publishsettings*ファイルからデプロイユーザーのパスワードを取得します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="2fe89-232">プロジェクトをビルドして配置する[MSBuild](http://msbuildbook.com/)コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="2fe89-233">また、コマンドラインで `Launch` パラメーターを指定した場合は、`Show-AzureWebsite` コマンドレットを呼び出して、web サイトの URL に既定のブラウザーを開きます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="2fe89-234">デプロイスクリプトは、次のようなコマンドを使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="2fe89-235">この処理が完了すると、クラウドで実行されているサイトと共に、`<websitename>.azurewebsites.net` の URL でブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![Windows Azure に展開された It アプリの修正](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="2fe89-237">要約</span><span class="sxs-lookup"><span data-stu-id="2fe89-237">Summary</span></span>

<span data-ttu-id="2fe89-238">これらのスクリプトを使用すると、同じ手順が常に同じ順序で同じオプションを使用して実行されることを保証できます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="2fe89-239">これにより、チームの各開発者は、他のチームメンバーの環境や運用環境では実際には同じように動作しない、自分のコンピューターに独自の作業をしたり、何かを行ったりしないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="2fe89-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="2fe89-240">同様の方法で、管理ポータルで実行できるほとんどの Azure 管理機能を自動化できます。そのためには、REST API、Windows PowerShell スクリプト、.NET 言語 API、または Linux または Mac で実行できる Bash ユーティリティを使用します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="2fe89-241">次の[章](source-control.md)では、ソースコードを見て、ソースコードリポジトリにスクリプトを含めることが重要な理由を説明します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="2fe89-242">リソース</span><span class="sxs-lookup"><span data-stu-id="2fe89-242">Resources</span></span>

- <span data-ttu-id="2fe89-243">[Windows PowerShell For Azure をインストールして構成](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="2fe89-244">Azure PowerShell コマンドレットをインストールする方法と、Azure アカウントを管理するために必要な証明書をコンピューターにインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="2fe89-245">これは、PowerShell 自体を学習するためのリソースへのリンクも用意されているため、開始するのに最適な場所です。</span><span class="sxs-lookup"><span data-stu-id="2fe89-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="2fe89-246">[Azure スクリプトセンター](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="2fe89-247">Azure サービスを管理するスクリプトを開発するためのリソースへの WindowsAzure.com ポータル、入門チュートリアルへのリンク、コマンドレットリファレンスドキュメントとソースコード、およびサンプルスクリプト</span><span class="sxs-lookup"><span data-stu-id="2fe89-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="2fe89-248">[週末 Scripter: はじめに Azure と PowerShell を使用](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-248">[Weekend Scripter: Getting Started with Azure and PowerShell](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="2fe89-249">この記事では、Windows PowerShell 専用のブログで、Azure の管理機能に PowerShell を使用する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="2fe89-250">[Azure クロスプラットフォームコマンドラインインターフェイスをインストールして構成](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)します。</span><span class="sxs-lookup"><span data-stu-id="2fe89-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="2fe89-251">Mac、Linux、および Windows システムで動作する Azure scripting framework の入門チュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="2fe89-252">「 [Azure sdk とツールのダウンロード」の「コマンドラインツール」セクション](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2fe89-253">Azure のコマンドラインツールに関連するドキュメントおよびダウンロードのポータルページです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="2fe89-254">[Azure 管理ライブラリと .NET を使用してすべてを自動化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="2fe89-255">Scott マン Selman は、Azure 用の .NET management API を紹介しています。</span><span class="sxs-lookup"><span data-stu-id="2fe89-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="2fe89-256">[Windows PowerShell スクリプトを使用した開発環境およびテスト環境の発行](https://msdn.microsoft.com/library/azure/dn642480.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="2fe89-257">Visual Studio によって web プロジェクトに自動的に生成される発行スクリプトの使用方法について説明する MSDN ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="2fe89-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="2fe89-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。</span><span class="sxs-lookup"><span data-stu-id="2fe89-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="2fe89-259">Visual studio で Windows PowerShell の言語サポートを追加する visual Studio 拡張機能。</span><span class="sxs-lookup"><span data-stu-id="2fe89-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2fe89-260">[前へ](introduction.md)
> [次へ](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="2fe89-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
