---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure ワーカーロールで OWIN をホストする |Microsoft Docs
author: MikeWasson
description: このチュートリアルでは、Microsoft Azure worker ロールで OWIN を自己ホストする方法について説明します。 Open Web Interface for .NET (OWIN) は、.NET Web サーバー間の抽象化を定義します...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472396"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="b72c8-104">Azure Worker ロールで OWIN をホストする</span><span class="sxs-lookup"><span data-stu-id="b72c8-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="b72c8-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b72c8-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b72c8-106">このチュートリアルでは、Microsoft Azure worker ロールで OWIN を自己ホストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="b72c8-107">[Open Web Interface for .net](http://owin.org/) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="b72c8-108">OWIN は、サーバーから web アプリケーションを分離します。これにより、OWIN は、Azure ワーカーロール内など、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするのに最適です。</span><span class="sxs-lookup"><span data-stu-id="b72c8-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="b72c8-109">このチュートリアルでは、Microsoft Azure worker ロール内で OWIN アプリケーションを自己ホストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="b72c8-110">Worker ロールの詳細については、「 [Azure 実行モデル](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b72c8-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b72c8-111">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="b72c8-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="b72c8-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b72c8-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="b72c8-113">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="b72c8-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="b72c8-114">Owin. Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b72c8-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="b72c8-115">Microsoft Azure プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="b72c8-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="b72c8-116">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="b72c8-117">Azure コンピューティングエミュレーターを使用してローカルでアプリケーションをデバッグするには、管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="b72c8-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="b72c8-118">**[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="b72c8-119">**インストールされているテンプレート**から、ビジュアルC# の下にある **クラウド** をクリックし、**Windows Azure クラウドサービス** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="b72c8-120">プロジェクトに "AzureApp" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="b72c8-121">**[新しい Windows Azure クラウドサービス]** ダイアログで、 **[Worker ロール]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="b72c8-122">既定の名前 ("WorkerRole1") をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="b72c8-123">この手順では、ワーカーロールをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="b72c8-124">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="b72c8-125">作成される Visual Studio ソリューションには、次の2つのプロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="b72c8-126">AzureApp&quot; &quot;Azure アプリケーションのロールと構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="b72c8-127">&quot;WorkerRole1&quot; には、ワーカーロールのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b72c8-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="b72c8-128">一般に、Azure アプリケーションには複数のロールを含めることができますが、このチュートリアルでは1つのロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="b72c8-129">OWIN 自己ホストパッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="b72c8-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="b72c8-130">**[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックし、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="b72c8-131">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="b72c8-132">HTTP エンドポイントを追加する</span><span class="sxs-lookup"><span data-stu-id="b72c8-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="b72c8-133">ソリューションエクスプローラーで、AzureApp プロジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="b72c8-134">ロール ノードを展開し、WorkerRole1 を右クリックして、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="b72c8-135">**[エンドポイント]** をクリックして、 **[エンドポイントの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="b72c8-136">**プロトコル** ドロップダウンリストで、http を選択します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="b72c8-137">**[パブリックポート]** と **[プライベートポート]** に、「80」と入力します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="b72c8-138">このポート番号は別の番号でもかまいません。</span><span class="sxs-lookup"><span data-stu-id="b72c8-138">These port numbers can be different.</span></span> <span data-ttu-id="b72c8-139">パブリックポートは、クライアントがロールに要求を送信するときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="b72c8-140">OWIN Startup クラスを作成する</span><span class="sxs-lookup"><span data-stu-id="b72c8-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="b72c8-141">ソリューションエクスプローラーで、WorkerRole1 プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="b72c8-142">クラスに `Startup` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-142">Name the class `Startup`.</span></span>

<span data-ttu-id="b72c8-143">すべての定型コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="b72c8-144">`UseWelcomePage` 拡張メソッドは、アプリケーションに単純な HTML ページを追加して、サイトが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="b72c8-145">OWIN ホストを開始する</span><span class="sxs-lookup"><span data-stu-id="b72c8-145">Start the OWIN Host</span></span>

<span data-ttu-id="b72c8-146">WorkerRole.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="b72c8-147">このクラスは、ワーカーロールが開始および停止したときに実行されるコードを定義します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="b72c8-148">次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="b72c8-149">`WorkerRole` クラスに**IDisposable**メンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="b72c8-150">`OnStart` メソッドで、次のコードを追加してホストを起動します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="b72c8-151">**WebApp**メソッドは、OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="b72c8-152">`Startup` クラスの名前は、メソッドの型パラメーターです。</span><span class="sxs-lookup"><span data-stu-id="b72c8-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="b72c8-153">慣例により、ホストはこのクラスの `Configure` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="b72c8-154">*\_アプリ*インスタンスを破棄するには、`OnStop` をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="b72c8-155">WorkerRole.cs の完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="b72c8-156">ソリューションをビルドし、F5 キーを押して、Azure コンピューティングエミュレーターでアプリケーションをローカルに実行します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="b72c8-157">ファイアウォールの設定によっては、エミュレーターでのファイアウォールの使用を許可することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b72c8-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="b72c8-158">コンピューティングエミュレーターは、エンドポイントにローカル IP アドレスを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="b72c8-159">IP アドレスを見つけるには、コンピューティングエミュレーターの UI を表示します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="b72c8-160">タスクバーの通知領域のエミュレーターアイコンを右クリックし、 **[コンピューティングエミュレーター UI の表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="b72c8-161">サービスの展開で、サービスの詳細情報の展開 [id]、IP アドレスを検索します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="b72c8-162">Web ブラウザーを開き、http:\/\/*アドレス*に移動します。ここで、 *address*はコンピューティングエミュレーターによって割り当てられた IP アドレスです。たとえば、`http://127.0.0.1:80`のようにします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="b72c8-163">OWIN のようこそページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="b72c8-164">Deploy to Azure (Azure へのデプロイ)</span><span class="sxs-lookup"><span data-stu-id="b72c8-164">Deploy to Azure</span></span>

<span data-ttu-id="b72c8-165">この手順では、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="b72c8-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="b72c8-166">まだお持ちでない場合は、無料試用版アカウントを数分で作成できます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b72c8-167">詳細については、「 [Microsoft Azure 無料試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b72c8-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="b72c8-168">ソリューションエクスプローラーで、AzureApp プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="b72c8-169">**[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="b72c8-170">Azure アカウントにサインインしていない場合は、 **[サインイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="b72c8-171">サインインしたら、サブスクリプションを選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="b72c8-172">クラウドサービスの名前を入力し、リージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="b72c8-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="b72c8-173">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="b72c8-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="b72c8-174">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b72c8-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="b72c8-175">[Azure のアクティビティログ] ウィンドウに、デプロイの進行状況が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b72c8-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="b72c8-176">アプリがデプロイされたら、`http://appname.cloudapp.net/`に移動します。ここで、 *appname*はクラウドサービスの名前です。</span><span class="sxs-lookup"><span data-stu-id="b72c8-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b72c8-177">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="b72c8-177">Additional Resources</span></span>

- [<span data-ttu-id="b72c8-178">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="b72c8-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="b72c8-179">GitHub の Katana プロジェクト</span><span class="sxs-lookup"><span data-stu-id="b72c8-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
