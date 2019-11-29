---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: Web 配置発行用に Web サーバーを構成する (オフライン展開) |Microsoft Docs
author: jrjlee
description: このトピックでは、オフラインの web 発行と配置をサポートするように IIS web サーバーを構成する方法について説明します。 インターネットインフォメーションサービス (I...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: f93cf11085fb19afb97b71aca8f638bd88fe658b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621099"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="90c37-104">Web 配置発行の Web サーバーを構成する (オフライン配置)</span><span class="sxs-lookup"><span data-stu-id="90c37-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>

<span data-ttu-id="90c37-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="90c37-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="90c37-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="90c37-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="90c37-107">このトピックでは、オフラインの web 発行と配置をサポートするように IIS web サーバーを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="90c37-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="90c37-108">インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) 2.0 以降を使用する場合、アプリケーションまたはサイトを web サーバーに取り込むために使用できる主な方法が3つあります。</span><span class="sxs-lookup"><span data-stu-id="90c37-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="90c37-109">次の操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="90c37-109">You can:</span></span>
> 
> - <span data-ttu-id="90c37-110">*Web 配置リモートエージェントサービス*を使用します。</span><span class="sxs-lookup"><span data-stu-id="90c37-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="90c37-111">この方法では、web サーバーの構成が少なくて済みますが、サーバーに何かを展開するには、ローカルサーバー管理者の資格情報を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="90c37-112">*Web 配置ハンドラー*を使用します。</span><span class="sxs-lookup"><span data-stu-id="90c37-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="90c37-113">この方法ははるかに複雑で、web サーバーを設定するためにより多くの初期作業が必要になります。</span><span class="sxs-lookup"><span data-stu-id="90c37-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="90c37-114">ただし、この方法を使用する場合は、管理者以外のユーザーが展開を実行できるように IIS を構成できます。</span><span class="sxs-lookup"><span data-stu-id="90c37-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="90c37-115">Web 配置ハンドラーは、IIS バージョン7以降でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="90c37-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="90c37-116">*オフライン展開*を使用します。</span><span class="sxs-lookup"><span data-stu-id="90c37-116">Use *offline deployment*.</span></span> <span data-ttu-id="90c37-117">この方法では、web サーバーの構成を最小限にする必要がありますが、サーバー管理者は web パッケージをサーバーに手動でコピーし、IIS マネージャーを使用してインポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="90c37-118">これらの方法の主な機能、長所、および短所の詳細については、「 [Web 配置に適切なアプローチを選択する](choosing-the-right-approach-to-web-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="90c37-119">はい (ネットワークインフラストラクチャまたはセキュリティの制限によってリモート展開が妨げられる場合)。</span><span class="sxs-lookup"><span data-stu-id="90c37-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="90c37-120">これは、インターネットに接続された実稼働環境で、web サーバーが物理的に、また&#x2014;はサーバーインフラストラクチャの他の部分&#x2014;からのファイアウォールとサブネットのいずれかによって分離されている場合に発生する可能性が最も高くなります。</span><span class="sxs-lookup"><span data-stu-id="90c37-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="90c37-121">当然ながら、web アプリケーションが定期的に更新される場合、この方法はあまり好ましくありません。</span><span class="sxs-lookup"><span data-stu-id="90c37-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="90c37-122">インフラストラクチャで許可されている場合は、Web 配置ハンドラーまたは Web 配置リモートエージェントサービスを使用して、リモート展開を有効にすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="90c37-123">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="90c37-123">Task Overview</span></span>

<span data-ttu-id="90c37-124">Web パッケージのオフラインインポートと配置をサポートするように web サーバーを構成するには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="90c37-125">IIS 7.5 および IIS 7 推奨構成をインストールします。</span><span class="sxs-lookup"><span data-stu-id="90c37-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="90c37-126">Web 配置2.1 以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="90c37-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="90c37-127">デプロイされたコンテンツをホストするための IIS web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="90c37-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="90c37-128">Web Deployment Agent サービスを無効にします。</span><span class="sxs-lookup"><span data-stu-id="90c37-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="90c37-129">サンプルソリューションを具体的にホストするには、次のことも行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="90c37-130">.NET Framework 4.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="90c37-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="90c37-131">ASP.NET MVC 3 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="90c37-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="90c37-132">このトピックでは、これらの各手順を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="90c37-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="90c37-133">このトピックのタスクとチュートリアルでは、Windows Server 2008 R2 を実行するクリーンなサーバービルドから始めることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="90c37-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="90c37-134">続行する前に、次のことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="90c37-135">Windows Server 2008 R2 Service Pack 1 および利用可能なすべての更新プログラムがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="90c37-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="90c37-136">サーバーはドメインに参加しています。</span><span class="sxs-lookup"><span data-stu-id="90c37-136">The server is domain-joined.</span></span>
- <span data-ttu-id="90c37-137">サーバーには静的 IP アドレスがあります。</span><span class="sxs-lookup"><span data-stu-id="90c37-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="90c37-138">コンピューターをドメインに参加させる方法の詳細については、「[コンピューターをドメインに参加](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)させ、ログオンする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="90c37-139">静的 IP アドレスの構成の詳細については、「[静的 Ip アドレスの構成](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="90c37-140">製品とコンポーネントのインストール</span><span class="sxs-lookup"><span data-stu-id="90c37-140">Install Products and Components</span></span>

<span data-ttu-id="90c37-141">このセクションでは、必要な製品とコンポーネントを web サーバーにインストールする手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="90c37-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="90c37-142">開始する前に、Windows Update を実行して、サーバーが完全に最新の状態になっていることを確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="90c37-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="90c37-143">この場合は、次のものをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="90c37-144">**IIS 7 推奨構成**。</span><span class="sxs-lookup"><span data-stu-id="90c37-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="90c37-145">これにより、web サーバー上で**Web サーバー (iis)** の役割が有効になり、ASP.NET アプリケーションをホストするために必要な iis モジュールとコンポーネントのセットがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="90c37-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="90c37-146">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="90c37-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="90c37-147">これは、このバージョンの .NET Framework でビルドされたアプリケーションを実行するために必要です。</span><span class="sxs-lookup"><span data-stu-id="90c37-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="90c37-148">**Web 配置ツール 2.1**以降。</span><span class="sxs-lookup"><span data-stu-id="90c37-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="90c37-149">これにより、Web 配置 (およびその基になる実行可能ファイル Msdeploy.exe) がサーバーにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="90c37-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="90c37-150">Web 配置は IIS と統合されており、web パッケージをインポートおよびエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="90c37-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="90c37-151">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="90c37-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="90c37-152">これにより、MVC 3 アプリケーションを実行するために必要なアセンブリがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="90c37-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="90c37-153">このチュートリアルでは、Web Platform Installer を使用してさまざまなコンポーネントをインストールし、構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="90c37-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="90c37-154">Web Platform Installer を使用する必要はありませんが、依存関係を自動的に検出して、常に最新の製品バージョンを確実に取得することで、インストールプロセスが簡略化されます。</span><span class="sxs-lookup"><span data-stu-id="90c37-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="90c37-155">詳細については、「 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="90c37-156">**必要な製品およびコンポーネントをインストールするには**</span><span class="sxs-lookup"><span data-stu-id="90c37-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="90c37-157">[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)をダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="90c37-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="90c37-158">インストールが完了すると、Web Platform Installer が自動的に起動します。</span><span class="sxs-lookup"><span data-stu-id="90c37-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="90c37-159">**[スタート]** メニューからいつでも Web Platform Installer を起動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="90c37-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="90c37-160">これを行うには、 **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[Microsoft Web Platform Installer]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="90c37-161">**Web Platform Installer 3.0**ウィンドウの上部にある **[Products]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="90c37-162">ウィンドウの左側のナビゲーションウィンドウで、 **[フレームワーク]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="90c37-163">**Microsoft .NET Framework 4**行に、.NET Framework がまだインストールされていない場合は、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="90c37-164">Windows Update に .NET Framework 4.0 が既にインストールされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="90c37-165">製品またはコンポーネントが既にインストールされている場合、Web Platform Installer では、 **[追加]** ボタンを、**インストールさ**れているテキストに置き換えることによってこれを示します。</span><span class="sxs-lookup"><span data-stu-id="90c37-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="90c37-166">**ASP.NET MVC 3 (Visual Studio 2010)** 行で、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="90c37-167">ナビゲーションウィンドウで、 **[サーバー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="90c37-168">**IIS 7 の推奨構成**行で、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="90c37-169">**[Web 配置ツール 2.1]** 行で、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="90c37-170">**[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-170">Click **Install**.</span></span> <span data-ttu-id="90c37-171">Web Platform Installer には、製品&#x2014;の一覧と、インストールする関連する依存&#x2014;関係が表示されます。ライセンス条項に同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="90c37-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="90c37-172">ライセンス条項を確認し、条項に同意する場合は [**同意**する] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="90c37-173">インストールが完了したら、 **[完了]** をクリックし、 **[Web Platform Installer 3.0]** ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="90c37-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="90c37-174">IIS をインストールする前に .NET Framework 4.0 をインストールした場合は、 [ASP.NET Iis Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_iis 登録ツール) を実行して、最新バージョンの ASP.NET を iis に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="90c37-175">この操作を行わないと、IIS が静的コンテンツ (HTML ファイルなど) を処理することはありませんが、ASP.NET コンテンツを参照しようとすると、 **HTTP エラー 404.0-Not Found**が返されます。</span><span class="sxs-lookup"><span data-stu-id="90c37-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="90c37-176">ASP.NET 4.0 が登録されていることを確認するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="90c37-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="90c37-177">**ASP.NET 4.0 を IIS に登録するには**</span><span class="sxs-lookup"><span data-stu-id="90c37-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="90c37-178">**[スタート]** をクリックし、「**コマンドプロンプト**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="90c37-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="90c37-179">検索結果で **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="90c37-180">コマンドプロンプトウィンドウで、 **:** ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="90c37-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="90c37-181">次のコマンドを入力し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="90c37-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="90c37-182">任意の時点で64ビットの web アプリケーションをホストする場合は、ASP.NET の64ビットバージョンを IIS に登録する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="90c37-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="90c37-183">これを行うには、コマンドプロンプトウィンドウで、 **\framework64\v4.0.30319**ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="90c37-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="90c37-184">次のコマンドを入力し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="90c37-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="90c37-185">この時点でもう一度 Windows Update を使用して、インストールした新しい製品とコンポーネントの利用可能な更新プログラムをダウンロードしてインストールすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="90c37-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="90c37-186">IIS Web サイトを構成する</span><span class="sxs-lookup"><span data-stu-id="90c37-186">Configure the IIS Website</span></span>

<span data-ttu-id="90c37-187">Web コンテンツをサーバーに展開する前に、コンテンツをホストするための IIS web サイトを作成して構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="90c37-188">Web 配置は、既存の IIS web サイトにのみ web パッケージを展開できます。web サイトを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="90c37-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="90c37-189">大まかに言えば、次のタスクを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="90c37-190">ファイルシステム上にコンテンツをホストするフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="90c37-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="90c37-191">コンテンツを提供する IIS web サイトを作成し、ローカルフォルダーに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="90c37-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="90c37-192">ローカルフォルダーのアプリケーションプール id に読み取りアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="90c37-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="90c37-193">IIS の既定の web サイトへのコンテンツのデプロイは停止されていませんが、テストシナリオやデモンストレーションシナリオ以外では、この方法はお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="90c37-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="90c37-194">運用環境をシミュレートするには、アプリケーションの要件に固有の設定を使用して、新しい IIS web サイトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="90c37-195">**IIS web サイトを作成して構成するには**</span><span class="sxs-lookup"><span data-stu-id="90c37-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="90c37-196">ローカルファイルシステムで、コンテンツを格納するフォルダーを作成します (例、 **C:\ demosite**)。</span><span class="sxs-lookup"><span data-stu-id="90c37-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="90c37-197">**[スタート]** メニューの **[管理ツール]** をポイントし、 **[インターネットインフォメーションサービス (IIS) マネージャー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="90c37-198">IIS マネージャーの **[接続]** ウィンドウで、サーバーノードを展開します (たとえば、 **PROWEB1**)。</span><span class="sxs-lookup"><span data-stu-id="90c37-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="90c37-199">**[サイト]** ノードを右クリックし、 **[Web サイトの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="90c37-200">**[サイト名]** ボックスに、IIS web サイトの名前 ( **demosite**など) を入力します。</span><span class="sxs-lookup"><span data-stu-id="90c37-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="90c37-201">**[物理パス]** ボックスに、ローカルフォルダーのパス (たとえば、「 \**c:\** 」) を入力します (または参照してください)。</span><span class="sxs-lookup"><span data-stu-id="90c37-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="90c37-202">**[ポート]** ボックスに、web サイトをホストするポート番号 ( **85**など) を入力します。</span><span class="sxs-lookup"><span data-stu-id="90c37-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="90c37-203">標準ポート番号は、HTTP の場合は80、HTTPS の場合は443です。</span><span class="sxs-lookup"><span data-stu-id="90c37-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="90c37-204">ただし、この web サイトをポート80でホストする場合は、サイトにアクセスする前に、既定の web サイトを停止する必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="90c37-205">Web サイトのドメインネームシステム (DNS) レコードを構成する場合を除き、 **[ホスト名]** ボックスは空白のままにして、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="90c37-206">運用環境では、web サイトをポート80でホストし、一致する DNS レコードと共にホストヘッダーを構成することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="90c37-207">IIS 7 でホストヘッダーを構成する方法の詳細については、「 [Web サイトのホストヘッダーを構成する (iis 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="90c37-208">Windows Server 2008 R2 の DNS サーバーの役割の詳細については、「 [Dns サーバーの概要](https://technet.microsoft.com/library/cc770392.aspx)」および「 [dns サーバー](https://technet.microsoft.com/windowsserver/dd448607)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="90c37-209">**[アクション]** ウィンドウの **[サイトの編集]** の下にある **[バインド]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="90c37-210">**[サイトバインド]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="90c37-211">**[サイトバインドの追加]** ダイアログボックスで、既存のサイト構成に合わせて**IP アドレス**と**ポート**を設定します。</span><span class="sxs-lookup"><span data-stu-id="90c37-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="90c37-212">**[ホスト名]** ボックスに、web サーバーの名前 (たとえば、 **PROWEB1**) を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="90c37-213">最初のサイトバインドでは、IP アドレスとポートまたは `http://localhost:85`を使用してサイトにローカルにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="90c37-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="90c37-214">2番目のサイトバインドを使用すると、コンピューター名 (http://proweb1:85) など) を使用して、ドメイン上の他のコンピューターからサイトにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="90c37-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="90c37-215">**[サイトバインド]** ダイアログボックスで、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="90c37-216">**[接続]** ウィンドウで、 **[アプリケーションプール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="90c37-217">**[アプリケーションプール]** ウィンドウで、アプリケーションプールの名前を右クリックし、 **[基本設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="90c37-218">既定では、アプリケーションプールの名前は web サイトの名前 ( **Demosite**など) と一致します。</span><span class="sxs-lookup"><span data-stu-id="90c37-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="90c37-219">**[.NET Framework のバージョン]** ボックスの一覧で **[.NET Framework v v4.0.30319]** を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="90c37-220">サンプルソリューションには .NET Framework 4.0 が必要です。</span><span class="sxs-lookup"><span data-stu-id="90c37-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="90c37-221">これは Web 配置全般の要件ではありません。</span><span class="sxs-lookup"><span data-stu-id="90c37-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="90c37-222">Web サイトがコンテンツを提供できるようにするには、アプリケーションプール id に、コンテンツが格納されているローカルフォルダーに対する読み取りアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="90c37-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="90c37-223">IIS 7.5 では、アプリケーションプールは既定で一意のアプリケーションプール id で実行されます (以前のバージョンの IIS とは異なり、アプリケーションプールは通常、ネットワークサービスアカウントを使用して実行されます)。</span><span class="sxs-lookup"><span data-stu-id="90c37-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="90c37-224">アプリケーションプール id は実際のユーザーアカウントではなく、ユーザーまたはグループ&#x2014;の一覧には表示されず、アプリケーションプールの起動時に動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="90c37-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="90c37-225">各アプリケーションプール id は、非表示の項目としてローカル**IIS\_IUSRS**セキュリティグループに追加されます。</span><span class="sxs-lookup"><span data-stu-id="90c37-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="90c37-226">ファイルまたはフォルダーのアプリケーションプール id にアクセス許可を付与するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="90c37-227"><strong>IIS AppPool\</strong ><em>[アプリケーションプール名]</em>( <strong>iis AppPool\DemoSite</strong>など) の形式を使用して、アプリケーションプール id に直接アクセス許可を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="90c37-227">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="90c37-228">**IIS\_IUSRS**グループにアクセス許可を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="90c37-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="90c37-229">最も一般的な方法は、ローカルの**IIS\_IUSRS**グループにアクセス許可を割り当てることです。この方法では、ファイルシステムのアクセス許可を再構成せずにアプリケーションプールを変更できるためです。</span><span class="sxs-lookup"><span data-stu-id="90c37-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="90c37-230">次の手順では、このグループベースの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="90c37-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="90c37-231">IIS 7.5 でのアプリケーションプール id の詳細については、「[アプリケーションプール id](https://go.microsoft.com/?linkid=9805123)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="90c37-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="90c37-232">**IIS web サイトのフォルダーのアクセス許可を構成するには**</span><span class="sxs-lookup"><span data-stu-id="90c37-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="90c37-233">Windows エクスプローラーで、ローカルフォルダーの場所を参照します。</span><span class="sxs-lookup"><span data-stu-id="90c37-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="90c37-234">フォルダーを右クリックし、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="90c37-235">**[セキュリティ]** タブで、 **[編集]** をクリックし、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="90c37-236">**[場所]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-236">Click **Locations**.</span></span> <span data-ttu-id="90c37-237">**[場所]** ダイアログボックスで、ローカルサーバーを選択し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="90c37-238">**[ユーザーまたはグループの選択]** ダイアログボックスで、「 **IIS\_iusrs**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="90c37-239"><em>[フォルダー名]</em>ダイアログボックス<strong>の [アクセス許可</strong>] で、新しいグループに、既定で [<strong>実行</strong>]、[<strong>フォルダーの内容の一覧表示</strong>]、および [<strong>読み取り</strong>] &amp; のアクセス許可が割り当てられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="90c37-239">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="90c37-240">これを変更せずに、[ <strong>OK]</strong>をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-240">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="90c37-241">[ <strong>OK</strong> ] をクリックして、 <em>[フォルダー名] の [</em><strong>プロパティ</strong>] ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="90c37-241">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="90c37-242">リモートエージェントサービスを無効にする</span><span class="sxs-lookup"><span data-stu-id="90c37-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="90c37-243">Web 配置をインストールすると、Web Deployment Agent サービスが自動的にインストールされ、開始されます。</span><span class="sxs-lookup"><span data-stu-id="90c37-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="90c37-244">このサービスを使用すると、リモートの場所から web パッケージをデプロイして公開することができます。</span><span class="sxs-lookup"><span data-stu-id="90c37-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="90c37-245">このシナリオではリモート展開機能を使用しないため、サービスを停止して無効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="90c37-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="90c37-246">Web パッケージを手動でインポートして展開するために、リモートエージェントサービスを停止する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="90c37-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="90c37-247">ただし、サービスを使用する予定がない場合は、サービスを停止して無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="90c37-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>

<span data-ttu-id="90c37-248">さまざまなコマンドラインユーティリティまたは Windows PowerShell コマンドレットを使用して、複数の方法でサービスを停止および無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="90c37-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="90c37-249">この手順では、UI ベースの簡単な方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="90c37-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="90c37-250">**リモートエージェントサービスを停止および無効にするには**</span><span class="sxs-lookup"><span data-stu-id="90c37-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="90c37-251">**[スタート]** メニューで、 **[管理ツール]** をポイントして、 **[サービス]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="90c37-252">サービス コンソールで、 **Web Deployment Agent サービス** 行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="90c37-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="90c37-253">**[Web Deployment Agent サービス]** を右クリックし、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="90c37-254">**[Web Deployment Agent サービスのプロパティ]** ダイアログボックスで、 **[停止]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="90c37-255">**[スタートアップの種類]** ボックスの一覧で **[無効]** を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="90c37-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="90c37-256">結論</span><span class="sxs-lookup"><span data-stu-id="90c37-256">Conclusion</span></span>

<span data-ttu-id="90c37-257">この時点で、web サーバーはオフラインの web パッケージ配置の準備ができています。</span><span class="sxs-lookup"><span data-stu-id="90c37-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="90c37-258">IIS web サイトに web パッケージをインポートする前に、次のキーポイントを確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="90c37-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="90c37-259">ASP.NET 4.0 を IIS に登録しましたか?</span><span class="sxs-lookup"><span data-stu-id="90c37-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="90c37-260">アプリケーションプール id に web サイトのソースフォルダーへの読み取りアクセス権があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="90c37-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="90c37-261">Web Deployment Agent サービスを停止しましたか?</span><span class="sxs-lookup"><span data-stu-id="90c37-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="90c37-262">[前へ](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [次へ](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="90c37-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
