---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure ワーカーロールでのホスト ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: 'チュートリアル: OWIN を使用して、Web API フレームワークをセルフホストする Azure Worker ロールで ASP.NET Web API をホストします。'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448408"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="a4d80-103">Azure Worker ロールでのホスト ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="a4d80-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="a4d80-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a4d80-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="a4d80-105">このチュートリアルでは、OWIN を使用して Web API フレームワークをセルフホストする Azure Worker ロールで ASP.NET Web API をホストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="a4d80-106">[Open Web Interface for .net](http://owin.org/) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="a4d80-107">OWIN は、サーバーから web アプリケーションを分離します。これにより、OWIN は、Azure ワーカーロール内など、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするのに最適です。</span><span class="sxs-lookup"><span data-stu-id="a4d80-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="a4d80-108">このチュートリアルでは、HttpListener パッケージを使用します。これは、自己ホスト型の OWIN アプリケーションに使用される HTTP サーバーを提供します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a4d80-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="a4d80-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="a4d80-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a4d80-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="a4d80-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a4d80-111">Web API 2</span></span>
> - [<span data-ttu-id="a4d80-112">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="a4d80-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="a4d80-113">Microsoft Azure プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="a4d80-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="a4d80-114">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="a4d80-115">Azure コンピューティングエミュレーターを使用してローカルでアプリケーションをデバッグするには、管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="a4d80-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="a4d80-116">**[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="a4d80-117">**インストールされているテンプレート**から、ビジュアルC# の下にある **クラウド** をクリックし、**Windows Azure クラウドサービス** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="a4d80-118">プロジェクトに "AzureApp" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="a4d80-119">**[新しい Windows Azure クラウドサービス]** ダイアログで、 **[Worker ロール]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="a4d80-120">既定の名前 ("WorkerRole1") をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="a4d80-121">この手順では、ワーカーロールをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="a4d80-122">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="a4d80-123">作成される Visual Studio ソリューションには、次の2つのプロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="a4d80-124">AzureApp&quot; &quot;Azure アプリケーションのロールと構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="a4d80-125">&quot;WorkerRole1&quot; には、ワーカーロールのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a4d80-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="a4d80-126">一般に、Azure アプリケーションには複数のロールを含めることができますが、このチュートリアルでは1つのロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="a4d80-127">Web API と OWIN パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="a4d80-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="a4d80-128">**[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックし、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="a4d80-129">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="a4d80-130">HTTP エンドポイントを追加する</span><span class="sxs-lookup"><span data-stu-id="a4d80-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="a4d80-131">ソリューションエクスプローラーで、AzureApp プロジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="a4d80-132">ロール ノードを展開し、WorkerRole1 を右クリックして、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="a4d80-133">**[エンドポイント]** をクリックして、 **[エンドポイントの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="a4d80-134">**プロトコル** ドロップダウンリストで、http を選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="a4d80-135">**[パブリックポート]** と **[プライベートポート]** に、「80」と入力します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="a4d80-136">このポート番号は別の番号でもかまいません。</span><span class="sxs-lookup"><span data-stu-id="a4d80-136">These port numbers can be different.</span></span> <span data-ttu-id="a4d80-137">パブリックポートは、クライアントがロールに要求を送信するときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="a4d80-138">セルフホスト用に Web API を構成する</span><span class="sxs-lookup"><span data-stu-id="a4d80-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="a4d80-139">ソリューションエクスプローラーで、WorkerRole1 プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="a4d80-140">クラスに `Startup` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="a4d80-141">このファイルの定型コードをすべて次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="a4d80-142">Web API コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="a4d80-142">Add a Web API Controller</span></span>

<span data-ttu-id="a4d80-143">次に、Web API コントローラークラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="a4d80-144">WorkerRole1 プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="a4d80-145">クラスに TestController という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-145">Name the class TestController.</span></span> <span data-ttu-id="a4d80-146">このファイルの定型コードをすべて次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="a4d80-147">わかりやすくするために、このコントローラーでは、プレーンテキストを返す2つの GET メソッドを定義しています。</span><span class="sxs-lookup"><span data-stu-id="a4d80-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="a4d80-148">OWIN ホストを開始する</span><span class="sxs-lookup"><span data-stu-id="a4d80-148">Start the OWIN Host</span></span>

<span data-ttu-id="a4d80-149">WorkerRole.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="a4d80-150">このクラスは、ワーカーロールが開始および停止したときに実行されるコードを定義します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="a4d80-151">次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="a4d80-152">`WorkerRole` クラスに**IDisposable**メンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="a4d80-153">`OnStart` メソッドで、次のコードを追加してホストを起動します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="a4d80-154">**WebApp**メソッドは、OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="a4d80-155">`Startup` クラスの名前は、メソッドの型パラメーターです。</span><span class="sxs-lookup"><span data-stu-id="a4d80-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="a4d80-156">慣例により、ホストはこのクラスの `Configure` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="a4d80-157">*\_アプリ*インスタンスを破棄するには、`OnStop` をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="a4d80-158">WorkerRole.cs の完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="a4d80-159">ソリューションをビルドし、F5 キーを押して、Azure コンピューティングエミュレーターでアプリケーションをローカルに実行します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="a4d80-160">ファイアウォールの設定によっては、エミュレーターでのファイアウォールの使用を許可することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a4d80-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="a4d80-161">次のような例外が発生した場合は、こちらの[ブログ投稿](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)で回避策をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a4d80-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="a4d80-162">"ファイルまたはアセンブリ ' Owin, Version = 2.0.2.0, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' またはその依存関係の1つが読み込めませんでした。</span><span class="sxs-lookup"><span data-stu-id="a4d80-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="a4d80-163">見つかったアセンブリのマニフェスト定義がアセンブリ参照と一致しません。</span><span class="sxs-lookup"><span data-stu-id="a4d80-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="a4d80-164">(HRESULT からの例外: 0x80131040) "</span><span class="sxs-lookup"><span data-stu-id="a4d80-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="a4d80-165">コンピューティングエミュレーターは、エンドポイントにローカル IP アドレスを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="a4d80-166">IP アドレスを見つけるには、コンピューティングエミュレーターの UI を表示します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="a4d80-167">タスクバーの通知領域のエミュレーターアイコンを右クリックし、 **[コンピューティングエミュレーター UI の表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="a4d80-168">サービスの展開で、サービスの詳細情報の展開 [id]、IP アドレスを検索します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="a4d80-169">Web ブラウザーを開き、 http://<em>address</em>/test/1 に移動します。ここで、 <em>address</em>はコンピューティングエミュレーターによって割り当てられた IP アドレスです。たとえば、`http://127.0.0.1:80/test/1`のようにします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="a4d80-170">Web API コントローラーからの応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="a4d80-171">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="a4d80-171">Deploy to Azure</span></span>

<span data-ttu-id="a4d80-172">この手順では、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="a4d80-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="a4d80-173">まだお持ちでない場合は、無料試用版アカウントを数分で作成できます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a4d80-174">詳細については、「 [Microsoft Azure 無料試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d80-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="a4d80-175">ソリューションエクスプローラーで、AzureApp プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="a4d80-176">**[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="a4d80-177">Azure アカウントにサインインしていない場合は、 **[サインイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="a4d80-178">サインインしたら、サブスクリプションを選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="a4d80-179">クラウドサービスの名前を入力し、リージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="a4d80-180">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="a4d80-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="a4d80-181">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a4d80-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="a4d80-182">[Azure のアクティビティログ] ウィンドウに、デプロイの進行状況が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a4d80-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="a4d80-183">アプリがデプロイされたら、 http://appname.cloudapp.net/test/1に移動します。</span><span class="sxs-lookup"><span data-stu-id="a4d80-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="a4d80-184">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a4d80-184">Additional Resources</span></span>

- [<span data-ttu-id="a4d80-185">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="a4d80-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="a4d80-186">GitHub の Katana プロジェクト</span><span class="sxs-lookup"><span data-stu-id="a4d80-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
