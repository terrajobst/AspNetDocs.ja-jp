---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: ホスト ASP.NET Web API 2 では、Azure Worker ロール - ASP.NET 4.x
author: MikeWasson
description: 'チュートリアル: Azure ワーカー ロールで OWIN を使用して Web API フレームワークを自己ホストするには、ASP.NET Web API をホストします。'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: bfb23aafb814010e8651965dad91ca20a37fd786
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404625"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="e5fa7-103">ASP.NET Web API 2 では、Azure Worker ロールをホストします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="e5fa7-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e5fa7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="e5fa7-105">このチュートリアルでは、OWIN を使用して Web API フレームワークを自己ホストする Azure ワーカー ロールで ASP.NET Web API をホストする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="e5fa7-106">[.NET 用 Web インターフェイスを開き](http://owin.org/)(OWIN) .NET web サーバーおよび web アプリケーション間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="e5fa7-107">OWIN により、OWIN の IIS の外部の独自のプロセスで web アプリケーションを自己ホストするために最適ですが、サーバーから web アプリケーションの分離 – Azure worker ロール内など。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="e5fa7-108">このチュートリアルでは、Microsoft.Owin.Host.HttpListener パッケージを使用します OWIN アプリケーションを自己ホストするために使用する HTTP サーバーを提供します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e5fa7-109">このチュートリアルで使用されるソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="e5fa7-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="e5fa7-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e5fa7-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="e5fa7-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="e5fa7-111">Web API 2</span></span>
> - [<span data-ttu-id="e5fa7-112">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="e5fa7-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="e5fa7-113">Microsoft Azure プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="e5fa7-114">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="e5fa7-115">Azure コンピューティング エミュレーターを使用してローカルでのアプリケーションをデバッグするには、管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="e5fa7-116">**ファイル** メニューのをクリックして**新規**、 をクリックし、**プロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="e5fa7-117">**インストールされたテンプレート**、Visual c# では、クリックして**クラウド** をクリックし、 **Windows Azure クラウド サービス**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="e5fa7-118">プロジェクトとして「AzureApp」という名前にして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="e5fa7-119">**新しい Windows Azure クラウド サービス**ダイアログ ボックスで、ダブルクリックして**ワーカー ロール**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="e5fa7-120">既定の名前 ("WorkerRole1") のままにします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="e5fa7-121">この手順では、ソリューションにワーカー ロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="e5fa7-122">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="e5fa7-123">作成された Visual Studio ソリューションには、2 つのプロジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="e5fa7-124">&quot;AzureApp&quot;ロールと Azure のアプリケーションの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="e5fa7-125">&quot;WorkerRole1&quot;ワーカー ロールのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="e5fa7-126">一般に、Azure のアプリケーションは、このチュートリアルは、1 つのロールを使用しますが、複数のロールを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="e5fa7-127">Web API と OWIN パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="e5fa7-128">**ツール** メニューのをクリックして**NuGet パッケージ マネージャー**、 をクリックし、**パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="e5fa7-129">パッケージ マネージャー コンソール ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="e5fa7-130">HTTP エンドポイントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="e5fa7-131">ソリューション エクスプ ローラーで、AzureApp プロジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="e5fa7-132">ロール ノードを展開し、WorkerRole1 を右クリックし、**プロパティ**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="e5fa7-133">クリックして**エンドポイント**、 をクリックし、**エンドポイントの追加**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="e5fa7-134">**プロトコル**ドロップダウン リストで、"http"を選択します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="e5fa7-135">**パブリック ポート**と**プライベート ポート**80」と入力します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="e5fa7-136">これらのポート番号が異なることがあります。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-136">These port numbers can be different.</span></span> <span data-ttu-id="e5fa7-137">パブリック ポートは、ロール要求を送信するときに使用するクライアントです。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="e5fa7-138">用の Web API を構成する自己ホスト</span><span class="sxs-lookup"><span data-stu-id="e5fa7-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="e5fa7-139">ソリューション エクスプ ローラーで WorkerRole1 プロジェクトを右クリックし、選択**追加** / **クラス**新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="e5fa7-140">クラスに `Startup` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="e5fa7-141">このファイルの定型コードのすべて、次に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="e5fa7-142">Web API コント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-142">Add a Web API Controller</span></span>

<span data-ttu-id="e5fa7-143">次に、Web API コント ローラー クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="e5fa7-144">WorkerRole1 プロジェクトを右クリックして**追加** / **クラス**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="e5fa7-145">TestController クラスの名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-145">Name the class TestController.</span></span> <span data-ttu-id="e5fa7-146">このファイルの定型コードのすべて、次に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="e5fa7-147">わかりやすくするため、このコント ローラーはプレーン テキストを返す 2 つの GET メソッドだけを定義します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="e5fa7-148">OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-148">Start the OWIN Host</span></span>

<span data-ttu-id="e5fa7-149">WorkerRole.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="e5fa7-150">このクラスは、ワーカー ロールが開始および停止時に実行されるコードを定義します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="e5fa7-151">次の追加ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="e5fa7-152">追加、 **IDisposable**メンバーを`WorkerRole`クラス。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="e5fa7-153">`OnStart`メソッドでは、ホストを起動する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="e5fa7-154">**WebApp.Start**メソッドは、OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="e5fa7-155">名前、`Startup`クラスは、メソッドの型パラメーター。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="e5fa7-156">慣例により、ホストが呼び出す、`Configure`このクラスのメソッド。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="e5fa7-157">上書き、`OnStop`を破棄する、 *\_アプリ*インスタンス。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="e5fa7-158">WorkerRole.cs の完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="e5fa7-159">ソリューションをビルドし、f5 キーを押して Azure コンピューティング エミュレーターでアプリケーションをローカルで実行します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="e5fa7-160">ファイアウォールの設定によっては、ファイアウォール経由のエミュレーターを許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="e5fa7-161">次のような例外が発生した場合を参照してください[このブログの投稿](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)問題を回避します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="e5fa7-162">"ファイルまたはアセンブリを読み込むことができません ' Microsoft.Owin、バージョン 2.0.2.0、カルチャを = = neutral, PublicKeyToken = 31bf3856ad364e35' またはその依存関係の 1 つ。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="e5fa7-163">指定したアセンブリのマニフェスト定義では、アセンブリ参照は一致しません。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="e5fa7-164">(HRESULT からの例外: 0x80131040)"</span><span class="sxs-lookup"><span data-stu-id="e5fa7-164">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="e5fa7-165">コンピューティング エミュレーターでは、エンドポイントに、ローカル IP アドレスが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="e5fa7-166">コンピューティング エミュレーター UI を表示することによって、IP アドレスを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="e5fa7-167">タスク バー通知領域のエミュレーター アイコンを右クリックして**コンピューティング エミュレーター UI**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="e5fa7-168">サービスの展開で、サービスの詳細情報の展開 [id]、IP アドレスを検索します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="e5fa7-169">Web ブラウザーを開き、 http:// に移動します<em>アドレス</em>/テスト/1、位置<em>アドレス</em>は、コンピューティング エミュレーターによって割り当てられた IP アドレスは、たとえば、 `http://127.0.0.1:80/test/1` 。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="e5fa7-170">Web API コント ローラーからの応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="e5fa7-171">Azure に配置する</span><span class="sxs-lookup"><span data-stu-id="e5fa7-171">Deploy to Azure</span></span>

<span data-ttu-id="e5fa7-172">この手順では、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="e5fa7-173">1 つをいない場合は、ほんの数分で無料試用版アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e5fa7-174">詳細については、次を参照してください。 [Microsoft Azure の無料試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="e5fa7-175">ソリューション エクスプ ローラーで、AzureApp プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="e5fa7-176">**[発行]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="e5fa7-177">Azure アカウントにサインインしていない場合はクリックして**サインイン**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="e5fa7-178">サインインした後、サブスクリプションを選択およびクリックして**次**します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="e5fa7-179">クラウド サービスの名前を入力し、リージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="e5fa7-180">**[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="e5fa7-181">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="e5fa7-182">Azure アクティビティ ログ ウィンドウには、展開の進行状況が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="e5fa7-183">アプリが展開されると、参照 http://appname.cloudapp.net/test/1 します。</span><span class="sxs-lookup"><span data-stu-id="e5fa7-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="e5fa7-184">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="e5fa7-184">Additional Resources</span></span>

- [<span data-ttu-id="e5fa7-185">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="e5fa7-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="e5fa7-186">GitHub の Katana プロジェクト</span><span class="sxs-lookup"><span data-stu-id="e5fa7-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
