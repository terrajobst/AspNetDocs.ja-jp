---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Azure Service Bus を使用した SignalR スケールアウト (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449938"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="55b30-102">Azure Service Bus による SignalR スケールアウト (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="55b30-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="55b30-103">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="55b30-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="55b30-104">このチュートリアルでは、Service Bus バックプレーンを使用して各ロールインスタンスにメッセージを配布する Windows Azure Web ロールに SignalR アプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="55b30-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="55b30-105">前提条件:</span><span class="sxs-lookup"><span data-stu-id="55b30-105">Prerequisites:</span></span>

- <span data-ttu-id="55b30-106">Windows Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="55b30-106">A Windows Azure account.</span></span>
- <span data-ttu-id="55b30-107">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="55b30-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="55b30-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="55b30-108">Visual Studio 2012.</span></span>

<span data-ttu-id="55b30-109">Service bus のバックプレーンは、 [Windows Server バージョン1.1 の Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)とも互換性があります。</span><span class="sxs-lookup"><span data-stu-id="55b30-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="55b30-110">ただし、バージョン1.0 の Windows Server Service Bus と互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="55b30-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="55b30-111">価格</span><span class="sxs-lookup"><span data-stu-id="55b30-111">Pricing</span></span>

<span data-ttu-id="55b30-112">Service Bus バックプレーンは、トピックを使用してメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="55b30-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="55b30-113">最新の価格情報については、「 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="55b30-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="55b30-114">このドキュメントの執筆時点では、$1 未満の場合、1か月あたり100万メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="55b30-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="55b30-115">バックプレーンは、SignalR hub メソッドを呼び出すたびに service bus メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="55b30-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="55b30-116">接続、切断、グループへの参加またはグループからの脱退など、いくつかの制御メッセージもあります。</span><span class="sxs-lookup"><span data-stu-id="55b30-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="55b30-117">ほとんどのアプリケーションでは、ほとんどのメッセージトラフィックはハブメソッドの呼び出しになります。</span><span class="sxs-lookup"><span data-stu-id="55b30-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="55b30-118">概要</span><span class="sxs-lookup"><span data-stu-id="55b30-118">Overview</span></span>

<span data-ttu-id="55b30-119">詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="55b30-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="55b30-120">Windows Azure portal を使用して、新しい Service Bus 名前空間を作成します。</span><span class="sxs-lookup"><span data-stu-id="55b30-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="55b30-121">次の NuGet パッケージをアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="55b30-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="55b30-122">SignalR</span><span class="sxs-lookup"><span data-stu-id="55b30-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="55b30-123">SignalR です。</span><span class="sxs-lookup"><span data-stu-id="55b30-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="55b30-124">SignalR アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="55b30-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="55b30-125">次のコードを global.asax に追加して、バックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="55b30-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="55b30-126">各アプリケーションについて、"自分の Appname" に別の値を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="55b30-127">複数のアプリケーションで同じ値を使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="55b30-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="55b30-128">Azure サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="55b30-128">Create the Azure Services</span></span>

<span data-ttu-id="55b30-129">「[クラウドサービスを作成およびデプロイする方法](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)」の説明に従って、クラウドサービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="55b30-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="55b30-130">「簡易作成を使用してクラウドサービスを作成する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="55b30-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="55b30-131">このチュートリアルでは、証明書をアップロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="55b30-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="55b30-132">[Service Bus トピック/サブスクリプションの使用方法に関する](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)ページの説明に従って、新しい Service Bus 名前空間を作成します。</span><span class="sxs-lookup"><span data-stu-id="55b30-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="55b30-133">「サービス名前空間の作成」セクションの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="55b30-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="55b30-134">必ず、クラウドサービスと Service Bus 名前空間に同じリージョンを選択してください。</span><span class="sxs-lookup"><span data-stu-id="55b30-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="55b30-135">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="55b30-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="55b30-136">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="55b30-136">Start Visual Studio.</span></span> <span data-ttu-id="55b30-137">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="55b30-138">**[新しいプロジェクト]** ダイアログボックスで、 **[ C#ビジュアル**] を展開します。</span><span class="sxs-lookup"><span data-stu-id="55b30-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="55b30-139">**[インストールされたテンプレート]** で、 **[クラウド]** を選択し、 **[Windows Azure クラウドサービス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="55b30-140">既定の .NET Framework 4.5 をそのままにします。</span><span class="sxs-lookup"><span data-stu-id="55b30-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="55b30-141">アプリケーションにチャットサービスの名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="55b30-142">**新しい Windows Azure クラウドサービス** ダイアログで、ASP.NET MVC 4 Web ロール を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="55b30-143">右矢印ボタン ( **&gt;** ) をクリックして、ソリューションにロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="55b30-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="55b30-144">新しいロールの上にマウスポインターを置くと、鉛筆アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="55b30-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="55b30-145">ロールの名前を変更するには、このアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-145">Click this icon to rename the role.</span></span> <span data-ttu-id="55b30-146">ロールに "SignalRChat" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="55b30-147">**新しい ASP.NET MVC 4 プロジェクト**ウィザードで、 **[インターネットアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="55b30-148">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-148">Click **OK**.</span></span> <span data-ttu-id="55b30-149">プロジェクトウィザードでは、次の2つのプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="55b30-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="55b30-150">チャットサービス: このプロジェクトは Windows Azure アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="55b30-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="55b30-151">Azure ロールとその他の構成オプションを定義します。</span><span class="sxs-lookup"><span data-stu-id="55b30-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="55b30-152">SignalRChat: このプロジェクトは、ASP.NET MVC 4 プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="55b30-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="55b30-153">SignalR Chat アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="55b30-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="55b30-154">チャットアプリケーションを作成するには、チュートリアル「 [SignalR と MVC 4 を使用したはじめに](tutorial-getting-started-with-signalr-and-mvc-4.md)」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="55b30-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="55b30-155">NuGet を使用して、必要なライブラリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="55b30-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="55b30-156">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="55b30-157">**[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="55b30-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="55b30-158">Windows Azure プロジェクトではなく、ASP.NET MVC プロジェクトにパッケージをインストールするには、`-ProjectName` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="55b30-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="55b30-159">バックプレーンの構成</span><span class="sxs-lookup"><span data-stu-id="55b30-159">Configure the Backplane</span></span>

<span data-ttu-id="55b30-160">アプリケーションの global.asax ファイルに、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="55b30-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="55b30-161">ここで、service bus 接続文字列を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="55b30-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="55b30-162">Azure portal で、作成した service bus 名前空間を選択し、[アクセスキー] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="55b30-163">接続文字列をクリップボードにコピーし、 *connectionString*変数に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="55b30-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="55b30-164">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="55b30-164">Deploy to Azure</span></span>

<span data-ttu-id="55b30-165">ソリューションエクスプローラーで、チャットサービスプロジェクト内の**Roles**フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="55b30-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="55b30-166">SignalRChat ロールを右クリックし、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="55b30-167">**構成** タブを選択します。**インスタンス** で 2 を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="55b30-168">また、VM のサイズを**極小**に設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="55b30-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="55b30-169">変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="55b30-169">Save the changes.</span></span>

<span data-ttu-id="55b30-170">ソリューションエクスプローラーで、[チャットサービス] プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="55b30-171">**[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="55b30-172">初めて Windows Azure に発行する場合は、資格情報をダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="55b30-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="55b30-173">**発行**ウィザードで、[サインインして資格情報をダウンロードする] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="55b30-174">これにより、Windows Azure portal にサインインし、発行設定ファイルをダウンロードするように求められます。</span><span class="sxs-lookup"><span data-stu-id="55b30-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="55b30-175">**[インポート]** をクリックし、ダウンロードした発行設定ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="55b30-176">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-176">Click **Next**.</span></span> <span data-ttu-id="55b30-177">**[発行の設定]** ダイアログの **[クラウドサービス]** で、前の手順で作成したクラウドサービスを選択します。</span><span class="sxs-lookup"><span data-stu-id="55b30-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="55b30-178">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-178">Click **Publish**.</span></span> <span data-ttu-id="55b30-179">アプリケーションをデプロイして Vm を起動するまでに数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="55b30-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="55b30-180">ここで、チャットアプリケーションを実行すると、ロールインスタンスは、Service Bus のトピックを使用して Azure Service Bus 経由で通信します。</span><span class="sxs-lookup"><span data-stu-id="55b30-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="55b30-181">トピックは、複数のサブスクライバーを許可するメッセージキューです。</span><span class="sxs-lookup"><span data-stu-id="55b30-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="55b30-182">バックプレーンによって、トピックとサブスクリプションが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="55b30-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="55b30-183">サブスクリプションとメッセージアクティビティを表示するには、Azure portal を開き、Service Bus 名前空間を選択し、[トピック] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="55b30-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="55b30-184">メッセージアクティビティがダッシュボードに表示されるまでに数分かかります。</span><span class="sxs-lookup"><span data-stu-id="55b30-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="55b30-185">SignalR は、トピックの有効期間を管理します。</span><span class="sxs-lookup"><span data-stu-id="55b30-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="55b30-186">アプリケーションが配置されている限り、トピックを手動で削除したり、設定を変更したりしないでください。</span><span class="sxs-lookup"><span data-stu-id="55b30-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
