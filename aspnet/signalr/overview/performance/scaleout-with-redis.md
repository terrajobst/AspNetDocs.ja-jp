---
uid: signalr/overview/performance/scaleout-with-redis
title: Redis による SignalR スケールアウト |Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467776"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="35ca4-103">Redis による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="35ca4-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="35ca4-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="35ca4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="35ca4-105">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="35ca4-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="35ca4-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="35ca4-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="35ca4-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="35ca4-107">.NET 4.5</span></span>
> - <span data-ttu-id="35ca4-108">SignalR バージョン2.4</span><span class="sxs-lookup"><span data-stu-id="35ca4-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="35ca4-109">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="35ca4-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="35ca4-110">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="35ca4-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="35ca4-111">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="35ca4-111">Questions and comments</span></span>
>
> <span data-ttu-id="35ca4-112">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="35ca4-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="35ca4-113">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="35ca4-114">このチュートリアルでは、 [Redis](http://redis.io/)を使用して、2つの異なる IIS インスタンスに展開されている SignalR アプリケーション全体にメッセージを配信します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="35ca4-115">Redis は、メモリ内のキーと値のストアです。</span><span class="sxs-lookup"><span data-stu-id="35ca4-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="35ca4-116">また、パブリッシュ/サブスクライブモデルを持つメッセージングシステムもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="35ca4-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="35ca4-117">SignalR Redis バックプレーンは、pub/sub 機能を使用して、他のサーバーにメッセージを転送します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="35ca4-118">このチュートリアルでは、3台のサーバーを使用します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="35ca4-119">Windows を実行する2台のサーバー。これは、SignalR アプリケーションの展開に使用します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="35ca4-120">Linux を実行する1台のサーバー。 Redis の実行に使用します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="35ca4-121">このチュートリアルのスクリーンショットでは、Ubuntu 12.04 TLS を使用しました。</span><span class="sxs-lookup"><span data-stu-id="35ca4-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="35ca4-122">使用する物理サーバーが3台ない場合は、Hyper-v で Vm を作成できます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="35ca4-123">もう1つの方法は、Azure で Vm を作成することです。</span><span class="sxs-lookup"><span data-stu-id="35ca4-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="35ca4-124">このチュートリアルでは、Redis の公式実装を使用していますが、MSOpenTech[の Windows ポート](https://github.com/MSOpenTech/redis)もあります。</span><span class="sxs-lookup"><span data-stu-id="35ca4-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="35ca4-125">セットアップと構成は異なりますが、それ以外の手順は同じです。</span><span class="sxs-lookup"><span data-stu-id="35ca4-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="35ca4-126">Redis による SignalR スケールアウトは、Redis クラスターをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="35ca4-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="35ca4-127">概要</span><span class="sxs-lookup"><span data-stu-id="35ca4-127">Overview</span></span>

<span data-ttu-id="35ca4-128">詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="35ca4-129">Redis をインストールし、Redis サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="35ca4-130">次の NuGet パッケージをアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="35ca4-131">SignalR</span><span class="sxs-lookup"><span data-stu-id="35ca4-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="35ca4-132">SignalR. StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="35ca4-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="35ca4-133">SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="35ca4-134">Startup.cs に次のコードを追加して、バックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="35ca4-135">Hyper-v 上の Ubuntu</span><span class="sxs-lookup"><span data-stu-id="35ca4-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="35ca4-136">Windows Hyper-v を使用すると、Windows Server 上に Ubuntu VM を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="35ca4-137">[http://www.ubuntu.com](http://www.ubuntu.com/)から Ubuntu ISO をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="35ca4-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="35ca4-138">Hyper-v で、新しい VM を追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="35ca4-139">**[仮想ハードディスクの接続]** 手順で、 **[仮想ハードディスクの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="35ca4-140">**[インストールオプション]** ステップで **[イメージファイル (.iso)]** を選択し、 **[参照]** をクリックして、Ubuntu インストール iso を参照します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="35ca4-141">Redis のインストール</span><span class="sxs-lookup"><span data-stu-id="35ca4-141">Install Redis</span></span>

<span data-ttu-id="35ca4-142">[http://redis.io/download](http://redis.io/download)の手順に従って Redis をダウンロードしてビルドします。</span><span class="sxs-lookup"><span data-stu-id="35ca4-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="35ca4-143">これにより、`src` ディレクトリに Redis バイナリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="35ca4-144">既定では、Redis はパスワードを必要としません。</span><span class="sxs-lookup"><span data-stu-id="35ca4-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="35ca4-145">パスワードを設定するには、ソースコードのルートディレクトリにある `redis.conf` ファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="35ca4-146">(編集する前に、ファイルのバックアップコピーを作成してください)`redis.conf`に次のディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="35ca4-147">次に、Redis サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="35ca4-148">Redis がリッスンする既定のポートであるポート6379を開きます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="35ca4-149">(構成ファイルのポート番号は変更できます)。</span><span class="sxs-lookup"><span data-stu-id="35ca4-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="35ca4-150">SignalR アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="35ca4-150">Create the SignalR Application</span></span>

<span data-ttu-id="35ca4-151">次のいずれかのチュートリアルに従って、SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="35ca4-152">SignalR 2.0 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="35ca4-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="35ca4-153">SignalR 2.0 および MVC 5 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="35ca4-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="35ca4-154">次に、Redis でのスケールアウトをサポートするようにチャットアプリケーションを変更します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="35ca4-155">まず、`Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet パッケージをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="35ca4-156">Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="35ca4-157">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="35ca4-158">次に、Startup.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="35ca4-159">**構成**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="35ca4-160">"server" は、Redis を実行しているサーバーの名前です。</span><span class="sxs-lookup"><span data-stu-id="35ca4-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="35ca4-161">*ポート番号*を指定します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-161">*port* is the port number</span></span>
- <span data-ttu-id="35ca4-162">"password" は、redis ファイルで定義したパスワードです。</span><span class="sxs-lookup"><span data-stu-id="35ca4-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="35ca4-163">"AppName" は任意の文字列です。</span><span class="sxs-lookup"><span data-stu-id="35ca4-163">"AppName" is any string.</span></span> <span data-ttu-id="35ca4-164">SignalR は、この名前で Redis pub/sub チャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="35ca4-165">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="35ca4-166">アプリケーションをデプロイして実行する</span><span class="sxs-lookup"><span data-stu-id="35ca4-166">Deploy and Run the Application</span></span>

<span data-ttu-id="35ca4-167">SignalR アプリケーションをデプロイするための Windows Server インスタンスを準備します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="35ca4-168">IIS ロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-168">Add the IIS role.</span></span> <span data-ttu-id="35ca4-169">WebSocket プロトコルなど、"アプリケーション開発" 機能を含めます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="35ca4-170">また、管理サービス ([管理ツール] の下に表示されます) も含めます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="35ca4-171">**Web 配置3.0 をインストールします。**</span><span class="sxs-lookup"><span data-stu-id="35ca4-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="35ca4-172">IIS マネージャーを実行すると、Microsoft Web Platform のインストールを求めるメッセージが表示されます。または、[インストーラーをダウンロード](https://go.microsoft.com/fwlink/?LinkId=255386)することもできます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="35ca4-173">プラットフォームインストーラーで Web 配置を検索し、Web 配置3.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="35ca4-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="35ca4-174">Web 管理サービスが実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="35ca4-175">実行されていない場合は、サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-175">If not, start the service.</span></span> <span data-ttu-id="35ca4-176">(Windows サービスの一覧に [Web 管理サービス] が表示されない場合は、IIS ロールを追加したときに管理サービスがインストールされていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="35ca4-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="35ca4-177">既定では、Web 管理サービスは TCP ポート8172でリッスンします。</span><span class="sxs-lookup"><span data-stu-id="35ca4-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="35ca4-178">Windows ファイアウォールで、ポート8172の TCP トラフィックを許可する新しい受信の規則を作成します。</span><span class="sxs-lookup"><span data-stu-id="35ca4-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="35ca4-179">詳細については、「[ファイアウォール規則の構成](https://technet.microsoft.com/library/dd448559(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="35ca4-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="35ca4-180">(Azure で Vm をホストしている場合は、Azure portal で直接行うことができます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="35ca4-181">「[仮想マシンに対してエンドポイントを設定する方法」を](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)参照してください)。</span><span class="sxs-lookup"><span data-stu-id="35ca4-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="35ca4-182">これで、開発用コンピューターからサーバーに Visual Studio プロジェクトを配置する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="35ca4-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="35ca4-183">ソリューションエクスプローラーで、ソリューションを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="35ca4-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="35ca4-184">Web 配置に関する詳細なドキュメントについては、「 [Visual Studio と ASP.NET の Web 配置コンテンツマップ](../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="35ca4-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="35ca4-185">アプリケーションを2台のサーバーに配置する場合は、各インスタンスを別のブラウザーウィンドウで開き、各インスタンスがもう一方から SignalR メッセージを受信することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="35ca4-186">(もちろん、運用環境では、2つのサーバーはロードバランサーの背後に配置されます)。</span><span class="sxs-lookup"><span data-stu-id="35ca4-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="35ca4-187">Redis に送信されるメッセージを確認する場合は、redis と共にインストールされる**redis cli**クライアントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="35ca4-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
