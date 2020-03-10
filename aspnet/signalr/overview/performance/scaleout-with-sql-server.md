---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server を使用したスケールアウトの SignalR |Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467740"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="7be4a-103">SQL Server による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="7be4a-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="7be4a-104">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="7be4a-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="7be4a-105">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7be4a-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="7be4a-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7be4a-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="7be4a-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="7be4a-107">.NET 4.5</span></span>
> - <span data-ttu-id="7be4a-108">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="7be4a-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="7be4a-109">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="7be4a-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="7be4a-110">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="7be4a-111">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="7be4a-111">Questions and comments</span></span>
>
> <span data-ttu-id="7be4a-112">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="7be4a-113">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="7be4a-114">このチュートリアルでは、SQL Server を使用して、2つの異なる IIS インスタンスに配置されている SignalR アプリケーション全体にメッセージを配布します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="7be4a-115">このチュートリアルは1つのテストコンピューターで実行することもできますが、完全な効果を得るには、SignalR アプリケーションを複数のサーバーに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7be4a-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="7be4a-116">また、いずれかのサーバーまたは別の専用サーバーに SQL Server をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7be4a-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="7be4a-117">もう1つの方法は、Azure で Vm を使用してチュートリアルを実行することです。</span><span class="sxs-lookup"><span data-stu-id="7be4a-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="7be4a-118">前提条件</span><span class="sxs-lookup"><span data-stu-id="7be4a-118">Prerequisites</span></span>

<span data-ttu-id="7be4a-119">Microsoft SQL Server 2005 以降。</span><span class="sxs-lookup"><span data-stu-id="7be4a-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="7be4a-120">バックプレーンは、SQL Server のデスクトップエディションとサーバーエディションの両方をサポートします。</span><span class="sxs-lookup"><span data-stu-id="7be4a-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="7be4a-121">SQL Server Compact Edition または Azure SQL Database はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="7be4a-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="7be4a-122">(アプリケーションが Azure でホストされている場合は、代わりに Service Bus バックプレーンを検討してください)。</span><span class="sxs-lookup"><span data-stu-id="7be4a-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="7be4a-123">概要</span><span class="sxs-lookup"><span data-stu-id="7be4a-123">Overview</span></span>

<span data-ttu-id="7be4a-124">詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="7be4a-125">新しい空のデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-125">Create a new empty database.</span></span> <span data-ttu-id="7be4a-126">バックプレーンによって、このデータベースに必要なテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="7be4a-127">次の NuGet パッケージをアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="7be4a-128">SignalR</span><span class="sxs-lookup"><span data-stu-id="7be4a-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="7be4a-129">SignalR. SqlServer</span><span class="sxs-lookup"><span data-stu-id="7be4a-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="7be4a-130">SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="7be4a-131">Startup.cs に次のコードを追加して、バックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="7be4a-132">このコードは、 [Tablecount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx)と[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)の既定値を使用してバックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="7be4a-133">これらの値を変更する方法の詳細については、「 [SignalR Performance: スケールアウトメトリック](signalr-performance.md#scaleout_metrics)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="7be4a-134">データベースを構成する</span><span class="sxs-lookup"><span data-stu-id="7be4a-134">Configure the Database</span></span>

<span data-ttu-id="7be4a-135">アプリケーションで Windows 認証を使用するか SQL Server 認証を使用してデータベースにアクセスするかを決定します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="7be4a-136">に関係なく、データベースユーザーがログインし、スキーマを作成し、テーブルを作成する権限を持っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="7be4a-137">バックプレーンが使用する新しいデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="7be4a-138">データベースに任意の名前を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-138">You can give the database any name.</span></span> <span data-ttu-id="7be4a-139">データベースにテーブルを作成する必要はありません。バックプレーンによって、必要なテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="7be4a-140">Service Broker を有効にする</span><span class="sxs-lookup"><span data-stu-id="7be4a-140">Enable Service Broker</span></span>

<span data-ttu-id="7be4a-141">バックプレーンデータベースの Service Broker を有効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7be4a-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="7be4a-142">Service Broker は SQL Server でのメッセージングとキューのネイティブサポートを提供します。これにより、バックプレーンが更新をより効率的に受信できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7be4a-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="7be4a-143">(ただし、バックプレーンは Service Broker なしでも動作します)。</span><span class="sxs-lookup"><span data-stu-id="7be4a-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="7be4a-144">Service Broker が有効になっているかどうかを確認するには、**データベース**カタログビューの **\_Broker\_enabled**列に対してクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="7be4a-145">Service Broker を有効にするには、次の SQL クエリを使用します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="7be4a-146">このクエリでデッドロックが発生した場合は、データベースに接続されているアプリケーションがないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="7be4a-147">トレースを有効にした場合、トレースには Service Broker が有効になっているかどうかも表示されます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="7be4a-148">SignalR アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="7be4a-148">Create a SignalR Application</span></span>

<span data-ttu-id="7be4a-149">次のいずれかのチュートリアルに従って、SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="7be4a-150">SignalR 2.0 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="7be4a-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="7be4a-151">SignalR 2.0 および MVC 5 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="7be4a-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="7be4a-152">次に、SQL Server によるスケールアウトをサポートするようにチャットアプリケーションを変更します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="7be4a-153">まず、SignalR NuGet パッケージをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="7be4a-154">Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7be4a-155">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="7be4a-156">次に、Startup.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="7be4a-157">**Configure**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="7be4a-158">アプリケーションをデプロイして実行する</span><span class="sxs-lookup"><span data-stu-id="7be4a-158">Deploy and Run the Application</span></span>

<span data-ttu-id="7be4a-159">SignalR アプリケーションをデプロイするための Windows Server インスタンスを準備します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="7be4a-160">IIS ロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-160">Add the IIS role.</span></span> <span data-ttu-id="7be4a-161">WebSocket プロトコルなど、"アプリケーション開発" 機能を含めます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="7be4a-162">また、管理サービス ([管理ツール] の下に表示されます) も含めます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="7be4a-163">**Web 配置3.0 をインストールします。**</span><span class="sxs-lookup"><span data-stu-id="7be4a-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="7be4a-164">IIS マネージャーを実行すると、Microsoft Web Platform のインストールを求めるメッセージが表示されます。または、[インストーラーをダウンロード](https://go.microsoft.com/fwlink/?LinkId=255386)することもできます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="7be4a-165">プラットフォームインストーラーで Web 配置を検索し、Web 配置3.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="7be4a-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="7be4a-166">Web 管理サービスが実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="7be4a-167">実行されていない場合は、サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-167">If not, start the service.</span></span> <span data-ttu-id="7be4a-168">(Windows サービスの一覧に [Web 管理サービス] が表示されない場合は、IIS ロールを追加したときに管理サービスがインストールされていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="7be4a-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="7be4a-169">最後に、TCP 用にポート8172を開きます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="7be4a-170">これは Web 配置ツールが使用するポートです。</span><span class="sxs-lookup"><span data-stu-id="7be4a-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="7be4a-171">これで、開発用コンピューターからサーバーに Visual Studio プロジェクトを配置する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="7be4a-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="7be4a-172">ソリューションエクスプローラーで、ソリューションを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7be4a-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="7be4a-173">Web 配置に関する詳細なドキュメントについては、「 [Visual Studio と ASP.NET の Web 配置コンテンツマップ](../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="7be4a-174">アプリケーションを2台のサーバーに配置する場合は、各インスタンスを別のブラウザーウィンドウで開き、各インスタンスがもう一方から SignalR メッセージを受信することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7be4a-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="7be4a-175">(もちろん、運用環境では、2つのサーバーはロードバランサーの背後に配置されます)。</span><span class="sxs-lookup"><span data-stu-id="7be4a-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="7be4a-176">アプリケーションを実行すると、SignalR によってデータベースにテーブルが自動的に作成されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="7be4a-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="7be4a-177">SignalR はテーブルを管理します。</span><span class="sxs-lookup"><span data-stu-id="7be4a-177">SignalR manages the tables.</span></span> <span data-ttu-id="7be4a-178">アプリケーションが配置されている限り、行を削除したり、テーブルを変更したりしないでください。</span><span class="sxs-lookup"><span data-stu-id="7be4a-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
