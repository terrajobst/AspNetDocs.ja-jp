---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redis による SignalR スケールアウト (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431206"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="ec29d-102">Redis による SignalR スケールアウト (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="ec29d-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="ec29d-103">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ec29d-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="ec29d-104">このチュートリアルでは、 [Redis](http://redis.io/)を使用して、2つの異なる IIS インスタンスに展開されている SignalR アプリケーション全体にメッセージを配信します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="ec29d-105">Redis は、メモリ内のキーと値のストアです。</span><span class="sxs-lookup"><span data-stu-id="ec29d-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="ec29d-106">また、パブリッシュ/サブスクライブモデルを持つメッセージングシステムもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ec29d-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="ec29d-107">SignalR Redis バックプレーンは、pub/sub 機能を使用して、他のサーバーにメッセージを転送します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="ec29d-108">このチュートリアルでは、3台のサーバーを使用します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="ec29d-109">Windows を実行する2台のサーバー。これは、SignalR アプリケーションの展開に使用します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="ec29d-110">Linux を実行する1台のサーバー。 Redis の実行に使用します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="ec29d-111">このチュートリアルのスクリーンショットでは、Ubuntu 12.04 TLS を使用しました。</span><span class="sxs-lookup"><span data-stu-id="ec29d-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="ec29d-112">使用する物理サーバーが3台ない場合は、Hyper-v で Vm を作成できます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="ec29d-113">もう1つの方法は、Azure で Vm を作成することです。</span><span class="sxs-lookup"><span data-stu-id="ec29d-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="ec29d-114">このチュートリアルでは、Redis の公式実装を使用していますが、MSOpenTech[の Windows ポート](https://github.com/MSOpenTech/redis)もあります。</span><span class="sxs-lookup"><span data-stu-id="ec29d-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="ec29d-115">セットアップと構成は異なりますが、それ以外の手順は同じです。</span><span class="sxs-lookup"><span data-stu-id="ec29d-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ec29d-116">Redis による SignalR スケールアウトは、Redis クラスターをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="ec29d-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="ec29d-117">概要</span><span class="sxs-lookup"><span data-stu-id="ec29d-117">Overview</span></span>

<span data-ttu-id="ec29d-118">詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ec29d-119">Redis をインストールし、Redis サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="ec29d-120">次の NuGet パッケージをアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="ec29d-121">SignalR</span><span class="sxs-lookup"><span data-stu-id="ec29d-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="ec29d-122">SignalR. Redis.</span><span class="sxs-lookup"><span data-stu-id="ec29d-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="ec29d-123">SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="ec29d-124">次のコードを global.asax に追加して、バックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="ec29d-125">Hyper-v 上の Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ec29d-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="ec29d-126">Windows Hyper-v を使用すると、Windows Server 上に Ubuntu VM を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="ec29d-127">[http://www.ubuntu.com](http://www.ubuntu.com/)から Ubuntu ISO をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="ec29d-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="ec29d-128">Hyper-v で、新しい VM を追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="ec29d-129">**[仮想ハードディスクの接続]** 手順で、 **[仮想ハードディスクの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="ec29d-130">**[インストールオプション]** ステップで **[イメージファイル (.iso)]** を選択し、 **[参照]** をクリックして、Ubuntu インストール iso を参照します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="ec29d-131">Redis のインストール</span><span class="sxs-lookup"><span data-stu-id="ec29d-131">Install Redis</span></span>

<span data-ttu-id="ec29d-132">[http://redis.io/download](http://redis.io/download)の手順に従って Redis をダウンロードしてビルドします。</span><span class="sxs-lookup"><span data-stu-id="ec29d-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="ec29d-133">これにより、`src` ディレクトリに Redis バイナリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="ec29d-134">既定では、Redis はパスワードを必要としません。</span><span class="sxs-lookup"><span data-stu-id="ec29d-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="ec29d-135">パスワードを設定するには、ソースコードのルートディレクトリにある `redis.conf` ファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="ec29d-136">(編集する前に、ファイルのバックアップコピーを作成してください)`redis.conf`に次のディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="ec29d-137">次に、Redis サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="ec29d-138">Redis がリッスンする既定のポートであるポート6379を開きます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="ec29d-139">(構成ファイルのポート番号は変更できます)。</span><span class="sxs-lookup"><span data-stu-id="ec29d-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="ec29d-140">SignalR アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="ec29d-140">Create the SignalR Application</span></span>

<span data-ttu-id="ec29d-141">次のいずれかのチュートリアルに従って、SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="ec29d-142">SignalR でのはじめに</span><span class="sxs-lookup"><span data-stu-id="ec29d-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="ec29d-143">SignalR と MVC 4 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="ec29d-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="ec29d-144">次に、Redis でのスケールアウトをサポートするようにチャットアプリケーションを変更します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="ec29d-145">まず、SignalR NuGet パッケージをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="ec29d-146">Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ec29d-147">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="ec29d-148">次に、global.asax ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="ec29d-149">**Application\_Start**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="ec29d-150">"server" は、Redis を実行しているサーバーの名前です。</span><span class="sxs-lookup"><span data-stu-id="ec29d-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="ec29d-151">*ポート番号*を指定します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-151">*port* is the port number</span></span>
- <span data-ttu-id="ec29d-152">"password" は、redis ファイルで定義したパスワードです。</span><span class="sxs-lookup"><span data-stu-id="ec29d-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="ec29d-153">"AppName" は任意の文字列です。</span><span class="sxs-lookup"><span data-stu-id="ec29d-153">"AppName" is any string.</span></span> <span data-ttu-id="ec29d-154">SignalR は、この名前で Redis pub/sub チャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="ec29d-155">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="ec29d-156">アプリケーションをデプロイして実行する</span><span class="sxs-lookup"><span data-stu-id="ec29d-156">Deploy and Run the Application</span></span>

<span data-ttu-id="ec29d-157">SignalR アプリケーションをデプロイするための Windows Server インスタンスを準備します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="ec29d-158">IIS ロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-158">Add the IIS role.</span></span> <span data-ttu-id="ec29d-159">WebSocket プロトコルなど、"アプリケーション開発" 機能を含めます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="ec29d-160">また、管理サービス ([管理ツール] の下に表示されます) も含めます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="ec29d-161">**Web 配置3.0 をインストールします。**</span><span class="sxs-lookup"><span data-stu-id="ec29d-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="ec29d-162">IIS マネージャーを実行すると、Microsoft Web Platform のインストールを求めるメッセージが表示されます。または、[インストーラーをダウンロード](https://go.microsoft.com/fwlink/?LinkId=255386)することもできます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="ec29d-163">プラットフォームインストーラーで Web 配置を検索し、Web 配置3.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="ec29d-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="ec29d-164">Web 管理サービスが実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="ec29d-165">実行されていない場合は、サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-165">If not, start the service.</span></span> <span data-ttu-id="ec29d-166">(Windows サービスの一覧に [Web 管理サービス] が表示されない場合は、IIS ロールを追加したときに管理サービスがインストールされていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="ec29d-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="ec29d-167">既定では、Web 管理サービスは TCP ポート8172でリッスンします。</span><span class="sxs-lookup"><span data-stu-id="ec29d-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="ec29d-168">Windows ファイアウォールで、ポート8172の TCP トラフィックを許可する新しい受信の規則を作成します。</span><span class="sxs-lookup"><span data-stu-id="ec29d-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="ec29d-169">詳細については、「[ファイアウォール規則の構成](https://technet.microsoft.com/library/dd448559(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ec29d-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="ec29d-170">(Azure で Vm をホストしている場合は、Azure portal で直接行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="ec29d-171">「[仮想マシンに対してエンドポイントを設定する方法」を](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)参照してください)。</span><span class="sxs-lookup"><span data-stu-id="ec29d-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="ec29d-172">これで、開発用コンピューターからサーバーに Visual Studio プロジェクトを配置する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="ec29d-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="ec29d-173">ソリューションエクスプローラーで、ソリューションを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ec29d-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="ec29d-174">Web 配置に関する詳細なドキュメントについては、「 [Visual Studio と ASP.NET の Web 配置コンテンツマップ](../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ec29d-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="ec29d-175">アプリケーションを2台のサーバーに配置する場合は、各インスタンスを別のブラウザーウィンドウで開き、各インスタンスがもう一方から SignalR メッセージを受信することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="ec29d-176">(もちろん、運用環境では、2つのサーバーはロードバランサーの背後に配置されます)。</span><span class="sxs-lookup"><span data-stu-id="ec29d-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="ec29d-177">Redis に送信されるメッセージを確認する場合は、redis と共にインストールされる**redis cli**クライアントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ec29d-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
