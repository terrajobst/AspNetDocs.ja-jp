---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Azure Service Bus を使用したスケールアウトの SignalR |Microsoft Docs
author: bradygaster
description: このトピックで使用されているソフトウェアのバージョン Visual Studio 2013 このトピックの SignalR 1.x バージョンについては、このトピックの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467734"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="da07d-103">Azure Service Bus による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="da07d-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="da07d-104">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="da07d-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="da07d-105">このチュートリアルでは、Service Bus バックプレーンを使用して各ロールインスタンスにメッセージを配布する Windows Azure Web ロールに SignalR アプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="da07d-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="da07d-106">( [Azure App Service の web apps](https://docs.microsoft.com/azure/app-service-web/)では、Service Bus バックプレーンを使用することもできます)。</span><span class="sxs-lookup"><span data-stu-id="da07d-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="da07d-107">前提条件:</span><span class="sxs-lookup"><span data-stu-id="da07d-107">Prerequisites:</span></span>

- <span data-ttu-id="da07d-108">Windows Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="da07d-108">A Windows Azure account.</span></span>
- <span data-ttu-id="da07d-109">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="da07d-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="da07d-110">Visual Studio 2012 または 2013。</span><span class="sxs-lookup"><span data-stu-id="da07d-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="da07d-111">Service bus のバックプレーンは、 [Windows Server バージョン1.1 の Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)とも互換性があります。</span><span class="sxs-lookup"><span data-stu-id="da07d-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="da07d-112">ただし、バージョン1.0 の Windows Server Service Bus と互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="da07d-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="da07d-113">価格</span><span class="sxs-lookup"><span data-stu-id="da07d-113">Pricing</span></span>

<span data-ttu-id="da07d-114">Service Bus バックプレーンは、トピックを使用してメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="da07d-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="da07d-115">最新の価格情報については、「 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da07d-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="da07d-116">このドキュメントの執筆時点では、$1 未満の場合、1か月あたり100万メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="da07d-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="da07d-117">バックプレーンは、SignalR hub メソッドを呼び出すたびに service bus メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="da07d-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="da07d-118">接続、切断、グループへの参加またはグループからの脱退など、いくつかの制御メッセージもあります。</span><span class="sxs-lookup"><span data-stu-id="da07d-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="da07d-119">ほとんどのアプリケーションでは、ほとんどのメッセージトラフィックはハブメソッドの呼び出しになります。</span><span class="sxs-lookup"><span data-stu-id="da07d-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="da07d-120">概要</span><span class="sxs-lookup"><span data-stu-id="da07d-120">Overview</span></span>

<span data-ttu-id="da07d-121">詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="da07d-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="da07d-122">Windows Azure portal を使用して、新しい Service Bus 名前空間を作成します。</span><span class="sxs-lookup"><span data-stu-id="da07d-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="da07d-123">次の NuGet パッケージをアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="da07d-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="da07d-124">SignalR</span><span class="sxs-lookup"><span data-stu-id="da07d-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="da07d-125">[SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)または[SignalR..](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="da07d-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="da07d-126">SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="da07d-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="da07d-127">Startup.cs に次のコードを追加して、バックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="da07d-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="da07d-128">このコードでは、[トピックの数](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)と[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)の既定値を使用してバックプレーンが構成されます。</span><span class="sxs-lookup"><span data-stu-id="da07d-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="da07d-129">これらの値を変更する方法の詳細については、「 [SignalR Performance: スケールアウトメトリック](signalr-performance.md#scaleout_metrics)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da07d-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="da07d-130">各アプリケーションについて、"自分の Appname" に別の値を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="da07d-131">複数のアプリケーションで同じ値を使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="da07d-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="da07d-132">Azure サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="da07d-132">Create the Azure Services</span></span>

<span data-ttu-id="da07d-133">「[クラウドサービスを作成およびデプロイする方法](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)」の説明に従って、クラウドサービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="da07d-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="da07d-134">「簡易作成を使用してクラウドサービスを作成する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="da07d-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="da07d-135">このチュートリアルでは、証明書をアップロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="da07d-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="da07d-136">[Service Bus トピック/サブスクリプションの使用方法に関する](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)ページの説明に従って、新しい Service Bus 名前空間を作成します。</span><span class="sxs-lookup"><span data-stu-id="da07d-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="da07d-137">「サービス名前空間の作成」セクションの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="da07d-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="da07d-138">必ず、クラウドサービスと Service Bus 名前空間に同じリージョンを選択してください。</span><span class="sxs-lookup"><span data-stu-id="da07d-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="da07d-139">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="da07d-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="da07d-140">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="da07d-140">Start Visual Studio.</span></span> <span data-ttu-id="da07d-141">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="da07d-142">**[新しいプロジェクト]** ダイアログボックスで、 **[ C#ビジュアル**] を展開します。</span><span class="sxs-lookup"><span data-stu-id="da07d-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="da07d-143">**[インストールされたテンプレート]** で、 **[クラウド]** を選択し、 **[Windows Azure クラウドサービス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="da07d-144">既定の .NET Framework 4.5 をそのままにします。</span><span class="sxs-lookup"><span data-stu-id="da07d-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="da07d-145">アプリケーションにチャットサービスの名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="da07d-146">**新しい Windows Azure クラウドサービス** ダイアログで、ASP.NET Web Role を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="da07d-147">右矢印ボタン ( **&gt;** ) をクリックして、ソリューションにロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="da07d-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="da07d-148">新しいロールの上にマウスポインターを置くと、鉛筆アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="da07d-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="da07d-149">ロールの名前を変更するには、このアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-149">Click this icon to rename the role.</span></span> <span data-ttu-id="da07d-150">ロールに "SignalRChat" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="da07d-151">**New ASP.NET プロジェクト** ダイアログボックスで、**MVC** を選択し、OK をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="da07d-152">プロジェクトウィザードでは、次の2つのプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="da07d-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="da07d-153">チャットサービス: このプロジェクトは Windows Azure アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="da07d-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="da07d-154">Azure ロールとその他の構成オプションを定義します。</span><span class="sxs-lookup"><span data-stu-id="da07d-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="da07d-155">SignalRChat: このプロジェクトは、ASP.NET MVC 5 プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="da07d-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="da07d-156">SignalR Chat アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="da07d-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="da07d-157">チャットアプリケーションを作成するには、チュートリアル「 [SignalR と MVC 5 でのはじめに](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="da07d-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="da07d-158">NuGet を使用して、必要なライブラリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="da07d-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="da07d-159">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="da07d-160">**[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="da07d-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="da07d-161">Windows Azure プロジェクトではなく、ASP.NET MVC プロジェクトにパッケージをインストールするには、`-ProjectName` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="da07d-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="da07d-162">バックプレーンの構成</span><span class="sxs-lookup"><span data-stu-id="da07d-162">Configure the Backplane</span></span>

<span data-ttu-id="da07d-163">アプリケーションの Startup.cs ファイルに、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="da07d-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="da07d-164">ここで、service bus 接続文字列を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da07d-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="da07d-165">Azure portal で、作成した service bus 名前空間を選択し、[アクセスキー] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="da07d-166">接続文字列をクリップボードにコピーし、 *connectionString*変数に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="da07d-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="da07d-167">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="da07d-167">Deploy to Azure</span></span>

<span data-ttu-id="da07d-168">ソリューションエクスプローラーで、チャットサービスプロジェクト内の**Roles**フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="da07d-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="da07d-169">SignalRChat ロールを右クリックし、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="da07d-170">**構成** タブを選択します。**インスタンス** で 2 を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="da07d-171">また、VM のサイズを**極小**に設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="da07d-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="da07d-172">変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="da07d-172">Save the changes.</span></span>

<span data-ttu-id="da07d-173">ソリューションエクスプローラーで、[チャットサービス] プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="da07d-174">**[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="da07d-175">初めて Windows Azure に発行する場合は、資格情報をダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="da07d-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="da07d-176">**発行**ウィザードで、[サインインして資格情報をダウンロードする] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="da07d-177">これにより、Windows Azure portal にサインインし、発行設定ファイルをダウンロードするように求められます。</span><span class="sxs-lookup"><span data-stu-id="da07d-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="da07d-178">**[インポート]** をクリックし、ダウンロードした発行設定ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="da07d-179">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-179">Click **Next**.</span></span> <span data-ttu-id="da07d-180">**[発行の設定]** ダイアログの **[クラウドサービス]** で、前の手順で作成したクラウドサービスを選択します。</span><span class="sxs-lookup"><span data-stu-id="da07d-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="da07d-181">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-181">Click **Publish**.</span></span> <span data-ttu-id="da07d-182">アプリケーションをデプロイして Vm を起動するまでに数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="da07d-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="da07d-183">ここで、チャットアプリケーションを実行すると、ロールインスタンスは、Service Bus のトピックを使用して Azure Service Bus 経由で通信します。</span><span class="sxs-lookup"><span data-stu-id="da07d-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="da07d-184">トピックは、複数のサブスクライバーを許可するメッセージキューです。</span><span class="sxs-lookup"><span data-stu-id="da07d-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="da07d-185">バックプレーンによって、トピックとサブスクリプションが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="da07d-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="da07d-186">サブスクリプションとメッセージアクティビティを表示するには、Azure portal を開き、Service Bus 名前空間を選択し、[トピック] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da07d-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="da07d-187">メッセージアクティビティがダッシュボードに表示されるまでに数分かかります。</span><span class="sxs-lookup"><span data-stu-id="da07d-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="da07d-188">SignalR は、トピックの有効期間を管理します。</span><span class="sxs-lookup"><span data-stu-id="da07d-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="da07d-189">アプリケーションが配置されている限り、トピックを手動で削除したり、設定を変更したりしないでください。</span><span class="sxs-lookup"><span data-stu-id="da07d-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="da07d-190">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="da07d-190">Troubleshooting</span></span>

<span data-ttu-id="da07d-191">**InvalidOperationException "サポートされている唯一の IsolationLevel は ' IsolationLevel ' です。"**</span><span class="sxs-lookup"><span data-stu-id="da07d-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="da07d-192">このエラーは、操作のトランザクションレベルが `Serializable`以外に設定されている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="da07d-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="da07d-193">他のトランザクションレベルで実行されている操作がないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="da07d-193">Verify that no operations are being performed with other transaction levels.</span></span>
