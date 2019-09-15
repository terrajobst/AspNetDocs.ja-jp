---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: Visual Studio を使用した ASP.NET Web デプロイ:テストに配置しています |Microsoft Docs
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: c45003325832258466a787bc589bf40e844248a2
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985853"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="5cb4e-103">Visual Studio を使用した ASP.NET Web デプロイ:テスト環境に配置する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>

<span data-ttu-id="5cb4e-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5cb4e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="5cb4e-105">このチュートリアルシリーズでは、Visual Studio 2017 を使用して Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service するために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-105">This tutorial series shows how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider using Visual Studio 2017.</span></span> <span data-ttu-id="5cb4e-106">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-106">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="5cb4e-107">現在のバージョンの Azure へのデプロイについては、「 [azure で ASP.NET Core web アプリを作成](/azure/app-service/app-service-web-get-started-dotnet)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-107">For a current version of deploying to Azure, see [Create an ASP.NET Core web app in Azure](/azure/app-service/app-service-web-get-started-dotnet).</span></span>

## <a name="overview"></a><span data-ttu-id="5cb4e-108">概要</span><span class="sxs-lookup"><span data-stu-id="5cb4e-108">Overview</span></span>

<span data-ttu-id="5cb4e-109">このチュートリアルでは、ローカルコンピューター上のインターネットインフォメーションサーバー (IIS) に ASP.NET web アプリケーションを展開します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-109">In this tutorial, you'll deploy an ASP.NET web application to Internet Information Server (IIS) on your local computer.</span></span>

<span data-ttu-id="5cb4e-110">一般に、アプリケーションを開発する場合は、Visual Studio で実行してテストします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-110">Generally when you develop an application, you run it and test it in Visual Studio.</span></span> <span data-ttu-id="5cb4e-111">既定では、Visual Studio 2017 の web アプリケーションプロジェクトでは、開発用 web サーバーとして IIS Express が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-111">By default, web application projects in Visual Studio 2017 use IIS Express as the development web server.</span></span> <span data-ttu-id="5cb4e-112">IIS Express は、Visual Studio 2017 が既定で使用する Visual Studio 開発サーバー (Cassini とも呼ばれます) よりも完全な IIS と同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2017 uses by default.</span></span> <span data-ttu-id="5cb4e-113">ただし、開発 web サーバーは IIS とまったく同じように動作しません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="5cb4e-114">その結果、Visual Studio でアプリを正常に実行してテストすることはできますが、IIS に配置すると失敗します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-114">Consequently, an app could run and test correctly in Visual Studio but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="5cb4e-115">アプリケーションを確実にテストするには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-115">You can reliably test your application in two ways:</span></span>

1. <span data-ttu-id="5cb4e-116">後で運用環境に配置する場合と同じプロセスを使用して、開発用コンピューター上の IIS にアプリケーションを配置します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-116">Deploy your application to IIS on your development computer using the same process that you'll use later to deploy it to your production environment.</span></span>

   <span data-ttu-id="5cb4e-117">Web プロジェクトを実行するときに IIS を使用するように Visual Studio を構成できますが、それでも配置プロセスはテストされません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-117">You can configure Visual Studio to use IIS when you run a web project, but that wouldn't test your deployment process.</span></span> <span data-ttu-id="5cb4e-118">このメソッドは、デプロイプロセスを検証し、IIS でアプリケーションが正しく実行されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-118">This method validates your deployment process and that your application runs correctly under IIS.</span></span>

2. <span data-ttu-id="5cb4e-119">実稼働環境と同様に、アプリケーションをテスト環境にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-119">Deploy your application to a test environment similar to your production environment.</span></span> 
 
   <span data-ttu-id="5cb4e-120">これらのチュートリアルの運用環境は、Azure App Service で Web Apps ます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-120">The production environment for these tutorials is Web Apps in Azure App Service.</span></span> <span data-ttu-id="5cb4e-121">理想的なテスト環境は、Azure サービスで作成された追加の web アプリです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-121">The ideal test environment is an additional web app created in the Azure Service.</span></span> <span data-ttu-id="5cb4e-122">運用 web アプリと同じように設定されますが、テストにのみ使用します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-122">Though it would be set up the same way as a production web app, you would only use it for testing.</span></span>

<span data-ttu-id="5cb4e-123">オプション2は、テスト方法として最も信頼性の高い方法です。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-123">Option 2 is the most reliable way to test.</span></span> <span data-ttu-id="5cb4e-124">オプション2を使用する場合、必ずしもオプション1を使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-124">If you use option 2, you don't necessarily need to use option 1.</span></span> <span data-ttu-id="5cb4e-125">ただし、サードパーティのホスティングプロバイダーにデプロイする場合は、オプション2が実現できないか、コストがかかる可能性があります。そのため、このチュートリアルシリーズでは両方の方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-125">However if you're deploying to a third-party hosting provider, option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="5cb4e-126">オプション2のガイダンスについては、「[運用環境へのデプロイ](deploying-to-production.md)」チュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-126">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="5cb4e-127">Visual Studio で web サーバーを使用する方法の詳細については、「 [Visual studio の Web サーバー」を](https://msdn.microsoft.com/library/58wxa9w5.aspx)参照してください。 ASP.NET web プロジェクトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-127">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="5cb4e-128">促すチュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-128">Reminder: If you receive an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="download-the-contoso-university-starter-project"></a><span data-ttu-id="5cb4e-129">Contoso 大学 starter プロジェクトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="5cb4e-129">Download the Contoso University starter project</span></span>

<span data-ttu-id="5cb4e-130">Contoso 大学の Visual Studio starter ソリューションとプロジェクトをダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-130">Download and install the Contoso University Visual Studio starter solution and project.</span></span> <span data-ttu-id="5cb4e-131">このソリューションには、完成したチュートリアルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-131">This solution contains the completed tutorial.</span></span> 

[<span data-ttu-id="5cb4e-132">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="5cb4e-132">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a><span data-ttu-id="5cb4e-133">IIS のインストール</span><span class="sxs-lookup"><span data-stu-id="5cb4e-133">Install IIS</span></span>

<span data-ttu-id="5cb4e-134">開発用コンピューター上の IIS に配置するには、IIS と Web 配置がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-134">To deploy to IIS on your development computer, confirm that IIS and Web Deploy are installed.</span></span> <span data-ttu-id="5cb4e-135">既定では、Visual Studio は Web 配置をインストールしますが、IIS は既定の Windows 10、Windows 8、または Windows 7 の構成には含まれていません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-135">By default, Visual Studio installs Web Deploy, but IIS isn't included in the default Windows 10, Windows 8, or Windows 7 configuration.</span></span> <span data-ttu-id="5cb4e-136">既に IIS をインストールしており、既定のアプリケーションプールが既に .NET 4 に設定されている場合は、[次のセクション](#sqlexpress)に進みます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-136">If you've already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="5cb4e-137">IIS と Web 配置をインストールするには、 [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx)を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-137">It's recommended you use the [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) to install IIS and Web Deploy.</span></span> <span data-ttu-id="5cb4e-138">WPI は、IIS を含む推奨される IIS 構成をインストールし、必要に応じて前提条件を Web 配置します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-138">WPI installs a recommended IIS configuration that includes IIS and Web Deploy prerequisites if necessary.</span></span>

   <span data-ttu-id="5cb4e-139">IIS、Web 配置、または必要なコンポーネントのいずれかが既にインストールされている場合は、不足しているものだけが WPI によってインストールされます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-139">If you've already installed IIS, Web Deploy, or any of their required components, the WPI installs only what is missing.</span></span>

   * <span data-ttu-id="5cb4e-140">Web Platform Installer を使用して、IIS と Web 配置をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-140">Use the Web Platform Installer to install IIS and Web Deploy:</span></span>
    
     ![WPI を使用して IIS をインストールする](deploying-to-iis/_static/image30.png)

     ![WPI を使用して Web 配置をインストールする](deploying-to-iis/_static/image31.png)

     <span data-ttu-id="5cb4e-143">IIS 7 がインストールされることを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-143">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="5cb4e-144">このリンクは、Windows 8 の IIS 8 で機能します。ただし、Windows 8 以降では、次の手順を実行して、ASP.NET 4.7 がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-144">The link works for IIS 8 in Windows 8; but for Windows 8 and later, go through the following steps to make sure that ASP.NET 4.7 is installed:</span></span>

   * <span data-ttu-id="5cb4e-145">[**コントロールパネル]**  > の **[プログラム** > **と機能** > ] **[Windows の機能の有効化または無効化**] を開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-145">Open **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off**.</span></span>

   * <span data-ttu-id="5cb4e-146">**インターネットインフォメーションサービス**、 **World Wide Web Services**、**アプリケーション開発機能**を展開します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-146">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   
   * <span data-ttu-id="5cb4e-147">**ASP.NET 4.7**が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-147">Confirm that **ASP.NET 4.7** is selected.</span></span>

     ![ASP.NET 4.7 を選択します](deploying-to-iis/_static/image1a.png)

   * <span data-ttu-id="5cb4e-149">**World Wide Web サービス**と**IIS 管理コンソール**が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-149">Confirm that **World Wide Web Services** and **IIS Management Console** is selected.</span></span> <span data-ttu-id="5cb4e-150">IIS と IIS マネージャーがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-150">This installs IIS and IIS Manager.</span></span>
    
     ![World Wide Web サービスの選択](deploying-to-iis/_static/image24.png)    
  
   * <span data-ttu-id="5cb4e-152">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-152">Select **OK**.</span></span> <span data-ttu-id="5cb4e-153">インストールが行われていることを示すダイアログボックスメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-153">Dialog box messages indicating installation is taking place appear.</span></span>

<span data-ttu-id="5cb4e-154">IIS をインストールした後、 **Iis マネージャー**を実行して、.NET Framework バージョン4が既定のアプリケーションプールに割り当てられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-154">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="5cb4e-155">WINDOWS + R キーを押して、[ファイルの**実行**] ダイアログボックスを開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-155">Press WINDOWS+R to open the **Run** dialog box.</span></span>

   <span data-ttu-id="5cb4e-156">(Windows 8 以降では、**スタート**ページで「run」と入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-156">(On Windows 8 or later, enter "run" on the **Start** page.</span></span> <span data-ttu-id="5cb4e-157">Windows 7 では、 **[スタート]** メニューから **[実行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-157">In Windows 7, select **Run** from the **Start** menu.</span></span> <span data-ttu-id="5cb4e-158">**[実行]** が **[スタート]** メニューにない場合は、タスクバーを右クリックし、 **[プロパティ]** を選択します。 [**スタート] メニュー**を選択し、 **[カスタマイズ]** をクリックして、 **[コマンドの実行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-158">If **Run** isn't in the **Start** menu, right-click the taskbar, select **Properties**, select the **Start Menu** tab, select **Customize**, and select **Run command**.)</span></span>

2. <span data-ttu-id="5cb4e-159">「Inetmgr.exe」と入力し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-159">Enter "inetmgr" and select **OK**.</span></span>

3. <span data-ttu-id="5cb4e-160">**[接続]** ウィンドウで、サーバーノードを展開し、 **[アプリケーションプール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-160">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="5cb4e-161">次の図に示すように、 **[アプリケーションプール]** ウィンドウで、 **DefaultAppPool**が .net framework version 4 に割り当てられている場合は、次のセクションに進みます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-161">In the **Application Pools** pane if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

   ![Inetmgr_showing_ 4.0 プール (_d)](deploying-to-iis/_static/image5a.png)

4. <span data-ttu-id="5cb4e-163">2つのアプリケーションプールのみが表示され、両方が .NET Framework 2.0 に設定されている場合は、IIS に ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-163">If you see only two application pools and both are set to .NET Framework 2.0, install ASP.NET 4 in IIS.</span></span>

   <span data-ttu-id="5cb4e-164">Windows 8 以降の場合は、前のセクションの手順「ASP.NET 4.7 がインストールされていることを確認するには」を参照してください。または、「 [windows 8 および Windows Server 2012 に ASP.NET 4.5 をインストールする方法](https://support.microsoft.com/kb/2736284)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-164">For Windows 8 or later, see the previous section's instructions for making sure that ASP.NET 4.7 is installed or see [How to install ASP.NET 4.5 on Windows 8 and Windows Server 2012](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="5cb4e-165">Windows 7 の場合は、Windows の **[スタート]** メニューの **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックして、コマンドプロンプトウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-165">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="5cb4e-166">次のコマンドを使用して、 [aspnet\_iis 登録ツール](https://msdn.microsoft.com/library/k6h9cz8h.aspx)を実行し、IIS に ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-166">Run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS using the following commands.</span></span> <span data-ttu-id="5cb4e-167">(32 ビットシステムでは、"Framework64" を "Framework" に置き換えます)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-167">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   <span data-ttu-id="5cb4e-168">このコマンドは .NET Framework 4 の新しいアプリケーションプールを作成しますが、既定のアプリケーションプールは2.0 に設定されたままになります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-168">This command creates new application pools for the .NET Framework 4, but the default application pool will remain set to 2.0.</span></span> <span data-ttu-id="5cb4e-169">.NET 4 を対象とするアプリケーションをそのアプリケーションプールに配置しているため、アプリケーションプールを .NET 4 に変更します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-169">You're deploying an application that targets .NET 4 to that application pool, so change the application pool to .NET 4.</span></span>

5. <span data-ttu-id="5cb4e-170">**IIS マネージャー**を閉じた場合は、もう一度実行し、サーバーノードを展開して、 **[アプリケーションプール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-170">If you closed **IIS Manager**, run it again, expand the server node, and select **Application Pools**.</span></span>

6. <span data-ttu-id="5cb4e-171">**[アプリケーションプール]** ウィンドウで、 **[DefaultAppPool]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-171">In the **Application Pools** pane, select **DefaultAppPool**.</span></span> <span data-ttu-id="5cb4e-172">**[操作]** ウィンドウで、 **[基本設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-172">In the **Actions** pane, select **Basic Settings**.</span></span>

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. <span data-ttu-id="5cb4e-174">**[アプリケーションプールの編集]** ダイアログボックスで、 **.net clr バージョン**を **.net clr v v4.0.30319**に変更します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-174">In the **Edit Application Pool** dialog box, change the **.NET CLR version** to **.NET CLR v4.0.30319**.</span></span> <span data-ttu-id="5cb4e-175">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-175">Select **OK**.</span></span>

   ![Selecting_ _4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

<span data-ttu-id="5cb4e-177">これで、IIS に web アプリケーションを発行する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-177">You're now ready to publish a web application to IIS.</span></span> <span data-ttu-id="5cb4e-178">ただし、まず、テスト用のデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-178">First, however, create databases for testing.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="5cb4e-179">SQL Server Express のインストール</span><span class="sxs-lookup"><span data-stu-id="5cb4e-179">Install SQL Server Express</span></span>

<span data-ttu-id="5cb4e-180">LocalDB は IIS で動作するように設計されていないため、テスト環境には SQL Server Express がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-180">LocalDB isn't designed to work in IIS, so your test environment has to have SQL Server Express installed.</span></span> <span data-ttu-id="5cb4e-181">SQL Server Express Visual Studio 2010 を使用している場合は、既定でインストールされています。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-181">If you're using Visual Studio 2010 SQL Server Express, it's already installed by default.</span></span> <span data-ttu-id="5cb4e-182">Visual Studio 2012 以降を使用している場合は、SQL Server Express をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-182">If you're using Visual Studio 2012 or later, install SQL Server Express.</span></span>

<span data-ttu-id="5cb4e-183">SQL Server Express をインストールするには、ダウンロードセンター [からダウンロードしてインストールします。Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-183">To install SQL Server Express, download and install it from [Download Center: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span></span> 

<span data-ttu-id="5cb4e-184">SQL Server インストールセンターの最初のページで、**新規 SQL Server スタンドアロンインストールを実行するか、既存のインストールに機能を追加**して、既定の選択肢を受け入れる指示に従います。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-184">On the first page of the SQL Server Installation Center, select **New SQL Server stand-alone installation or add features to an existing installation** and follow the instructions accepting the default choices.</span></span> <span data-ttu-id="5cb4e-185">インストールウィザードで、既定の設定をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-185">In the installation wizard, accept the default settings.</span></span> <span data-ttu-id="5cb4e-186">インストールオプションの詳細については、「インストール[ウィザードからの SQL Server のインストール (セットアップ)](https://msdn.microsoft.com/library/ms143219.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-186">For more information about installation options, see [Install SQL Server from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="5cb4e-187">テスト環境用の SQL Server Express データベースを作成する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-187">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="5cb4e-188">Contoso 大学のアプリケーションには、次の2つのデータベースがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-188">The Contoso University application has two databases:</span></span> 

1. <span data-ttu-id="5cb4e-189">メンバーシップデータベース</span><span class="sxs-lookup"><span data-stu-id="5cb4e-189">Membership database</span></span> 
2. <span data-ttu-id="5cb4e-190">アプリケーションデータベース</span><span class="sxs-lookup"><span data-stu-id="5cb4e-190">Application database</span></span> 

<span data-ttu-id="5cb4e-191">これらのデータベースは、2つの異なるデータベースまたは1つのデータベースに配置できます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-191">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="5cb4e-192">これらを組み合わせると、データベースの結合が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-192">Combining them makes database joins between them easier.</span></span> 

<span data-ttu-id="5cb4e-193">サードパーティのホスティングプロバイダーにデプロイする場合は、ホスティングプランによって、それらを結合する理由が提供されることもあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-193">If you're deploying to a third-party hosting provider, your hosting plan might also give you a reason to combine them.</span></span> <span data-ttu-id="5cb4e-194">たとえば、プロバイダーは複数のデータベースに対してより多くの料金を請求する場合や、複数のデータベースを許可しない場合があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-194">For example, the provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="5cb4e-195">このチュートリアルでは、テスト環境の2つのデータベースと、ステージング環境と運用環境の1つのデータベースに配置します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-195">In this tutorial, you'll deploy to two databases in the test environment and to one database in the staging and production environments.</span></span>

<span data-ttu-id="5cb4e-196">Visual Studio の **表示** メニューで、**サーバーエクスプローラー** (visual Web Developer では**データベースエクスプローラー** ) を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-196">From the **View** menu in Visual Studio, select **Server Explorer** (**Database Explorer** in Visual Web Developer).</span></span> <span data-ttu-id="5cb4e-197">**[データ接続]** を右クリックし、 **[新しい SQL Server データベースの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-197">Right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="5cb4e-199">**[新しい SQL Server データベースの作成]** ダイアログボックスで、 **[サーバー名]** ボックスに「.\SQLExpress」と入力し、 **[新しいデータベース名]** ボックスに「ContosoUniversity」と入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-199">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box.</span></span> <span data-ttu-id="5cb4e-200">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-200">Select **OK**.</span></span>

![Aspnet の作成-ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="5cb4e-202">同じ手順に従って、という名前`ContosoUniversity`の新しい SQL Server Express School データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-202">Follow the same procedure to create a new SQL Server Express School database named `ContosoUniversity`.</span></span>

<span data-ttu-id="5cb4e-203">**サーバーエクスプローラー**には、2つの新しいデータベースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-203">**Server Explorer** shows the two new databases.</span></span>

![サーバーエクスプローラーの新しいデータベース](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="5cb4e-205">新しいデータベースの grant スクリプトを作成する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-205">Create a grant script for the new databases</span></span>

<span data-ttu-id="5cb4e-206">開発用コンピューターの IIS でアプリケーションを実行すると、アプリケーションは既定のアプリケーションプールの資格情報を使用してデータベースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-206">When the application runs in IIS on your development computer, the application uses the default application pool's credentials to access the database.</span></span> <span data-ttu-id="5cb4e-207">ただし、既定では、アプリケーションプールには、データベースを開くためのアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-207">However, by default, the application pool doesn't have permission to open the databases.</span></span> <span data-ttu-id="5cb4e-208">これは、そのアクセス許可を付与するスクリプトを実行する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-208">This means you need to run a script to grant that permission.</span></span> <span data-ttu-id="5cb4e-209">このセクションでは、そのスクリプトを作成し、後で実行して、アプリケーションが IIS で実行されているときにデータベースを開けるようにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-209">In this section, you'll create that script and run it later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="5cb4e-210">テキストエディターで、次の SQL コマンドを新しいファイルにコピーし、 *Grant .sql*として保存します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-210">In a text editor, copy the following SQL commands into a new file and save it as *Grant.sql*.</span></span> 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

<span data-ttu-id="5cb4e-211">Visual Studio で、Contoso 大学ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-211">In Visual Studio, open the Contoso University solution.</span></span> <span data-ttu-id="5cb4e-212">(プロジェクトのいずれかではなく) ソリューションを右クリックし、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-212">Right-click the solution (not one of the projects), and select **Add**.</span></span> <span data-ttu-id="5cb4e-213">**[既存の項目]** を選択し、を参照して *.sql*を指定し、それを開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-213">Select **Existing Item**, browse to *Grant.sql*, and open it.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb4e-214">このスクリプトは、このチュートリアルで指定されているように、Windows 10、Windows 8、または Windows 7 の IIS 設定を使用して、SQL Server Express 2012 以降とで動作するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-214">This script is designed to work with SQL Server Express 2012 or later and with the IIS settings in Windows 10, Windows 8, or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="5cb4e-215">異なるバージョンの SQL Server または Windows を使用している場合、またはコンピューターに IIS を別の方法でセットアップする場合は、このスクリプトの変更が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-215">If you're using a different version of SQL Server or Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="5cb4e-216">SQL Server スクリプトの詳細については、「 [SQL Server オンラインブック](https://go.microsoft.com/fwlink/?LinkId=132511)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-216">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> <span data-ttu-id="5cb4e-217">**セキュリティ**に関する注意このスクリプトは`db_owner` 、実行時にデータベースにアクセスする権限をユーザーに付与します。これは、運用環境で使用するものです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-217">**Security Note** This script gives `db_owner` permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="5cb4e-218">場合によっては、完全なデータベーススキーマ更新権限を持つユーザーを配置に対してのみ指定し、データの読み取りと書き込みのみを行う権限を持つ別のユーザーを実行時に指定することができます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-218">In some scenarios, you might want to specify a user that has full database schema update permissions only for deployment and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="5cb4e-219">詳細については、このチュートリアルで後述する「 [Code First Migrations に対する web.config の自動変更のレビュー](#reviewingmigrations) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-219">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="5cb4e-220">アプリケーションデータベースで grant スクリプトを実行する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-220">Run the grant script in the application database</span></span>

<span data-ttu-id="5cb4e-221">データベースの配置で[Dbdacfx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)プロバイダーが使用されるため、配置時にメンバーシップデータベースで許可スクリプトを実行するように発行プロファイルを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-221">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) provider.</span></span> <span data-ttu-id="5cb4e-222">Code First Migrations の配置中にスクリプトを実行することはできません。これは、アプリケーションデータベースを配置する方法です。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-222">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="5cb4e-223">これは、アプリケーションデータベースに配置する前に、スクリプトを手動で実行する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-223">This means you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="5cb4e-224">Visual Studio で、前の手順で作成した*Grant .sql*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-224">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>

2. <span data-ttu-id="5cb4e-225">**[接続]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-225">Select **Connect**.</span></span> 

    ![[接続] ボタン](deploying-to-iis/_static/image11.png)

3. <span data-ttu-id="5cb4e-227">**[サーバーへの接続]** ダイアログボックスで、**サーバー名**として「 *.\SQLExpress* 」と入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-227">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**.</span></span> <span data-ttu-id="5cb4e-228">**[接続]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-228">Select **Connect**.</span></span>

4. <span data-ttu-id="5cb4e-229">データベース ボックスの一覧で  **ContosoUniversity** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-229">In the database drop-down list select **ContosoUniversity**.</span></span> <span data-ttu-id="5cb4e-230">**[実行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-230">Select **Execute**.</span></span> 

   ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="5cb4e-231">アプリケーションの実行時にデータベーステーブルを作成するための Code First Migrations のために、既定のアプリケーションプール id には、アプリケーションデータベースに対する十分なアクセス許可が与えられます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-231">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="5cb4e-232">IIS に公開する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-232">Publish to IIS</span></span>

<span data-ttu-id="5cb4e-233">Visual Studio と Web 配置を使用して IIS に配置できる方法はいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-233">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

* <span data-ttu-id="5cb4e-234">Visual Studio のワンクリック発行を使用します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-234">Use Visual Studio one-click publish.</span></span>
* <span data-ttu-id="5cb4e-235">コマンドラインから発行します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-235">Publish from the command line.</span></span>
* <span data-ttu-id="5cb4e-236">展開パッケージを作成し、IIS マネージャーを使用してインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-236">Create a deployment package and install it using IIS Manager.</span></span> <span data-ttu-id="5cb4e-237">パッケージには、IIS にサイトをインストールするために必要なすべてのファイルとメタデータを含む .zip ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-237">The package has a .zip file with all the files and metadata required to install a site in IIS.</span></span>
* <span data-ttu-id="5cb4e-238">展開パッケージを作成し、コマンドラインを使用してインストールします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-238">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="5cb4e-239">デプロイタスクを自動化するように Visual Studio を設定する前のチュートリアルで実行したプロセスは、これらのすべての方法に適用されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-239">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="5cb4e-240">これらのチュートリアルでは、最初の2つの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-240">In these tutorials, you'll use the first two methods.</span></span> <span data-ttu-id="5cb4e-241">配置パッケージの使用方法の詳細については、「web[配置パッケージを作成およびインストール](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-241">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="5cb4e-242">発行する前に、管理者モードで Visual Studio を実行していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-242">Before publishing, make sure that you're running Visual Studio in administrator mode.</span></span> <span data-ttu-id="5cb4e-243">タイトルバーに **(管理者)** が表示されない場合は、Visual Studio を閉じます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-243">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="5cb4e-244">Windows 8 (またはそれ以降) の**スタート**ページまたは windows 7 の **[スタート]** メニューで、Visual Studio アイコンを右クリックし、 **[管理者として実行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-244">In the Windows 8 (or later) **Start** page or the Windows 7 **Start** menu, right-click the Visual Studio icon and select **Run as Administrator**.</span></span> <span data-ttu-id="5cb4e-245">ローカルコンピューター上の IIS に発行する場合、管理者モードは発行にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-245">Administrator mode is only required for publishing when you're publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="5cb4e-246">発行プロファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-246">Create the publish profile</span></span>

1. <span data-ttu-id="5cb4e-247">**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクト ( **ContosoUniversity**プロジェクトではありません) を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-247">In **Solution Explorer**, right-click the **ContosoUniversity** project (not the **ContosoUniversity.DAL** project).</span></span> <span data-ttu-id="5cb4e-248">**[発行]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-248">Select **Publish**.</span></span> <span data-ttu-id="5cb4e-249">**[発行]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-249">The **Publish** page appears.</span></span>

2. <span data-ttu-id="5cb4e-250">**[新しいプロファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-250">Select **New Profile**.</span></span> <span data-ttu-id="5cb4e-251">**[発行先の選択]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-251">The **Pick a publish target** dialog box appears.</span></span>

3. <span data-ttu-id="5cb4e-252">**[IIS、FTP など]** を選択します。 **[プロファイルの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-252">Select **IIS, FTP, etc**. Select **Create Profile**.</span></span> <span data-ttu-id="5cb4e-253">**発行**ウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-253">The **Publish** wizard appears.</span></span>

   ![Web の発行ウィザードの [プロファイル] タブ](deploying-to-iis/_static/image26.png)

4. <span data-ttu-id="5cb4e-255">**[発行方法]** ドロップダウンメニューから、 **[Web 配置]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-255">From the **Publish method** drop-down menu, select **Web Deploy**.</span></span>

5. <span data-ttu-id="5cb4e-256">**[サーバー]** に「 *localhost*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-256">For **Server**, enter *localhost*.</span></span>

6. <span data-ttu-id="5cb4e-257">**[サイト名]** に「 *Default Web Site/ContosoUniversity」と*入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-257">For **Site name**, enter *Default Web Site/ContosoUniversity*.</span></span>

7. <span data-ttu-id="5cb4e-258">**[宛先 URL]** に *http://localhost/ContosoUniversity* 「」と入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-258">For **Destination URL**, enter *http://localhost/ContosoUniversity*.</span></span>

   <span data-ttu-id="5cb4e-259">**送信先 URL**の設定は必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-259">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="5cb4e-260">Visual Studio がアプリケーションの配置を完了すると、既定のブラウザーが自動的にこの URL に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-260">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="5cb4e-261">配置後にブラウザーが自動的に開かないようにする場合は、このボックスを空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-261">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

8. <span data-ttu-id="5cb4e-262">**[接続の検証]** を選択して、設定が正しいことを確認し、ローカルコンピューターの IIS に接続できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-262">Select **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

   <span data-ttu-id="5cb4e-263">緑色のチェックマークは、接続が成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-263">A green check mark verifies that the connection is successful.</span></span>

   ![Web の発行ウィザードの [接続] タブ](deploying-to-iis/_static/image27.png)

9. <span data-ttu-id="5cb4e-265">**[次]** へ を選択して、 **[設定]** タブに進みます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-265">Select **Next** to advance to the **Settings** tab.</span></span>

10. <span data-ttu-id="5cb4e-266">**[構成]** ボックスの一覧で、配置するビルド構成を指定します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-266">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="5cb4e-267">**リリース**の既定値に設定したままにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-267">Leave it set to the default value of **Release**.</span></span> <span data-ttu-id="5cb4e-268">このチュートリアルでは、デバッグビルドを配置しません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-268">You won't be deploying Debug builds in this tutorial.</span></span>

11. <span data-ttu-id="5cb4e-269">[**ファイルの発行オプション]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-269">Expand **File Publish Options**.</span></span> <span data-ttu-id="5cb4e-270">[**アプリ\_データ] フォルダーから [除外するファイル**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-270">Select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="5cb4e-271">テスト環境では、アプリケーションは、アプリケーション *\_データ*フォルダー内の .mdf ファイルではなく、ローカル SQL Server Express インスタンスに作成したデータベースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-271">In the test environment, the application accesses the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>

12. <span data-ttu-id="5cb4e-272">[**発行時にプリコンパイル**を解除し、**ターゲットで追加ファイルを削除**する] チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-272">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![[設定] タブのファイル発行オプション](deploying-to-iis/_static/image15a.png)

    <span data-ttu-id="5cb4e-274">プリコンパイルは、主に大規模なサイトに便利なオプションです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-274">Precompiling is an option that is useful mainly for large sites.</span></span> <span data-ttu-id="5cb4e-275">サイトが発行された後にページが初めて要求されたときに、起動時間を短縮することができます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-275">It can reduce startup time the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="5cb4e-276">追加のファイルを削除する必要はありません。これは最初の展開なので、コピー先のフォルダーにファイルがまだ存在しないためです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-276">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5cb4e-277">同じサイトへの後続の配置のために [**転送先で追加のファイルを削除**する] を選択した場合は、展開する前にどのファイルが削除されるかを事前に確認できるように、プレビュー機能を使用してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-277">If you select **Remove additional files at destination** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="5cb4e-278">期待される動作は、Web 配置が、プロジェクトで削除された移行先サーバー上のファイルを削除することです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-278">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="5cb4e-279">ただし、コピー元とコピー先のフォルダーの下のフォルダー構造全体が比較されます。また、場合によっては、削除したくないファイルが削除される Web 配置があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-279">However, the entire folder structure under the source and destination folders is compared; and in some scenarios, Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="5cb4e-280">たとえば、ルートフォルダーにプロジェクトを配置するときに、サーバーのサブフォルダーに web アプリケーションがある場合、サブフォルダーは削除されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-280">For example if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="5cb4e-281">Contoso.com のメインサイト用に1つのプロジェクトがあり、contoso.com/blog にブログ用の別のプロジェクトがあるとします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-281">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="5cb4e-282">ブログアプリケーションはサブフォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-282">The blog application is in a subfolder.</span></span> <span data-ttu-id="5cb4e-283">メインサイトの展開時に [**ターゲットで追加ファイルを削除**する] を選択すると、ブログアプリケーションが削除されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-283">If you select **Remove additional files at destination** when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="5cb4e-284">別の例では、\_アプリデータフォルダーが予期せず削除される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-284">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="5cb4e-285">SQL Server Compact などの一部のデータベースでは、アプリケーション\_データフォルダーにデータベースファイルが格納されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-285">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="5cb4e-286">最初の配置の後、以降の配置ではデータベースファイルをコピーしないようにするため、[パッケージ/発行 Web] タブで [ **\_アプリデータを除外**する] を選択します。この操作を実行すると、[**変換先で追加のファイルを削除**する] を選択\_した場合、次回の発行時にデータベースファイルとアプリデータフォルダー自体が削除されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-286">After the initial deployment, you don't want to keep copying the database files in subsequent deployments, so you select  **Exclude App\_Data** on the Package/Publish Web tab. After you do that if you have **Remove additional files at destination** selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="5cb4e-287">メンバーシップデータベースの配置を構成する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-287">Configure deployment for the membership database</span></span>

<span data-ttu-id="5cb4e-288">次の手順は、ダイアログボックスの **[データベース]** セクションの**defaultconnection**データベースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-288">The following steps apply to the **DefaultConnection** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="5cb4e-289">**[リモート接続文字列]** ボックスに、新しい SQL Server Express メンバーシップデータベースを指す次の接続文字列を入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-289">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   <span data-ttu-id="5cb4e-290">配置プロセスでは、配置された Web.config ファイルにこの接続文字列を格納します。これは、この接続文字列を**実行時に使用する**ためです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-290">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="5cb4e-291">**サーバーエクスプローラー**から接続文字列を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-291">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="5cb4e-292">**サーバーエクスプローラー**で、 **[データ接続]** を展開し、  **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**データベースを選択します。次に、 **[プロパティ]** ウィンドウで**接続文字列をコピーします。** 値。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-292">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="5cb4e-293">この接続文字列には、を削除`Pooling=False`できる1つの追加設定があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-293">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>

2. <span data-ttu-id="5cb4e-294">**[データベースの更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-294">Select **Update database**.</span></span>

   <span data-ttu-id="5cb4e-295">これにより、配置中にデータベーススキーマが転送先データベースに作成されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-295">This causes the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="5cb4e-296">次のステップでは、実行する必要がある追加のスクリプトを指定します。1つは、既定のアプリケーションプールへのデータベースアクセスを許可するスクリプト、もう1つはデータを配置するスクリプトです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-296">In next steps, you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>

3. <span data-ttu-id="5cb4e-297">**[データベースの更新の構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-297">Select **Configure database updates**.</span></span>
 
4. <span data-ttu-id="5cb4e-298">**[データベースの更新の構成]** ダイアログボックスで、 **[SQL スクリプトの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-298">In the **Configure Database Updates** dialog box, select **Add SQL Script**.</span></span> <span data-ttu-id="5cb4e-299">先ほどソリューションフォルダーに保存した*Grant .sql*スクリプトに移動します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-299">Navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>

5. <span data-ttu-id="5cb4e-300">*Aspnet-data-dev*スクリプトを追加するには、この手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-300">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

   ![メンバーシップデータベースのデータベースの更新の構成](deploying-to-iis/_static/image16.png)

6. <span data-ttu-id="5cb4e-302">**[閉じる]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-302">Select **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="5cb4e-303">アプリケーションデータベースの展開の構成</span><span class="sxs-lookup"><span data-stu-id="5cb4e-303">Configure deployment for the application database</span></span>

<span data-ttu-id="5cb4e-304">`DbContext` Visual Studio が Entity Framework クラスを検出すると、データベース セクションにエントリが作成されます。このエントリには、データベースの**更新** チェックボックスではなく **Code First Migrations の実行** チェックボックスがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-304">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="5cb4e-305">このチュートリアルでは、このチェックボックスを使用して Code First Migrations 展開を指定します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-305">For this tutorial, you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="5cb4e-306">場合によっては、 `DbContext`データベースを使用していても、データベースを配置するために移行ではなく dbdacfx プロバイダーを使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-306">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="5cb4e-307">そのような場合は、MSDN の ASP.NET Web デプロイに関する FAQ で、「[移行せずに Code First データベースをデプロイする操作方法](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-307">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="5cb4e-308">次の手順は、ダイアログボックスの **[データベース]** セクションの**schoolcontext.cs**データベースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-308">The following steps apply to the **SchoolContext** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="5cb4e-309">**[リモート接続文字列]** ボックスに、新しい SQL Server Express アプリケーションデータベースを指す次の接続文字列を入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-309">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   <span data-ttu-id="5cb4e-310">配置プロセスでは、配置された Web.config ファイルにこの接続文字列を格納します。これは、この接続文字列を**実行時に使用する**ためです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-310">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

   <span data-ttu-id="5cb4e-311">また、メンバーシップデータベースの接続文字列と同じ方法で、**サーバーエクスプローラー**からアプリケーションデータベースの接続文字列を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-311">You can also get the application database connection string from **Server Explorer** in the same way you got the membership database connection string.</span></span>

2. <span data-ttu-id="5cb4e-312">**[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-312">Select **Execute Code First Migrations (runs on application start)**.</span></span>

   <span data-ttu-id="5cb4e-313">このオプションを選択すると、配置プロセスによって、配置された`MigrateDatabaseToLatestVersion` web.config ファイルが初期化子を指定するように構成されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-313">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="5cb4e-314">この初期化子は、配置後にアプリケーションが初めてデータベースにアクセスしたときに、データベースを最新バージョンに自動的に更新します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-314">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="5cb4e-315">発行プロファイルの変換を構成する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-315">Configure publish profile transforms</span></span>

1. <span data-ttu-id="5cb4e-316">**[閉じる]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-316">Select **Close**.</span></span> <span data-ttu-id="5cb4e-317">変更を保存するかどうかを確認するメッセージが表示されたら、[**はい]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-317">Select **Yes** when you are asked if you want to save changes.</span></span>

2. <span data-ttu-id="5cb4e-318">**ソリューションエクスプローラー**で、 **[プロパティ]** 、 **[publishprofiles]** の順に展開します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-318">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>

3. <span data-ttu-id="5cb4e-319">[ *Customprofile. pubxml* ] を右クリックし、名前を「 *Test pubxml*」に変更します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-319">Right-click *CustomProfile.pubxml* and rename it *Test.pubxml*.</span></span>

4. <span data-ttu-id="5cb4e-320">[ *Pubxml*] を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-320">Right-click *Test.pubxml*.</span></span> <span data-ttu-id="5cb4e-321">**[構成の変換の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-321">Select **Add Config Transform**.</span></span>

   ![[構成変換の追加] メニュー](deploying-to-iis/_static/image17.png)

   <span data-ttu-id="5cb4e-323">Visual Studio は、 *web.config*変換ファイルを作成して開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-323">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>

5. <span data-ttu-id="5cb4e-324">*Web.config 変換ファイル*で、開始構成タグの直後に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-324">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="5cb4e-325">テスト発行プロファイルを使用すると、この変換によって環境インジケーターが "Test" に設定されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-325">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="5cb4e-326">デプロイされたサイトでは、"Contoso 大学" H1 見出しの後に "(Test)" と表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-326">In the deployed site, you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>

6. <span data-ttu-id="5cb4e-327">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-327">Save and close the file.</span></span>

7. <span data-ttu-id="5cb4e-328">*Web.config ファイルを*右クリックし、 **[プレビューの変換]** を選択して、コード化した変換によって予想される変更が生成されるようにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-328">Right-click the *Web.Test.config* file and select **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="5cb4e-329">Web.config の**プレビュー**ウィンドウには、 *web.config 変換と* *web.config 変換の*両方を適用した結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-329">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="5cb4e-330">デプロイの更新をプレビューする</span><span class="sxs-lookup"><span data-stu-id="5cb4e-330">Preview the deployment updates</span></span>

1. <span data-ttu-id="5cb4e-331">Web の**発行**ウィザードをもう一度開きます (ContosoUniversity プロジェクトを右クリックし、 **[発行]** 、 **[プレビュー]** の順に選択します)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-331">Open the **Publish Web** wizard again (right-click the ContosoUniversity project, select **Publish**, then **Preview**).</span></span>

2. <span data-ttu-id="5cb4e-332">**[プレビュー]** ダイアログボックスで **[プレビューの開始]** を選択すると、コピーされるファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-332">In the **Preview** dialog box, select **Start Preview** to see a list of the files that will be copied.</span></span> 

   ![発行のプレビュー](deploying-to-iis/_static/image29.png)

   <span data-ttu-id="5cb4e-334">また、[データベースの**プレビュー** ] リンクを選択して、メンバーシップデータベースで実行されるスクリプトを確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-334">You can also select the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="5cb4e-335">(Code First Migrations 配置に対して実行されるスクリプトはありません。そのため、アプリケーションデータベースをプレビューすることはできません)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-335">(No scripts are run for Code First Migrations deployment, so there's nothing to preview for the application database.)</span></span>

3. <span data-ttu-id="5cb4e-336">**[発行]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-336">Select **Publish**.</span></span>

   <span data-ttu-id="5cb4e-337">Visual Studio が管理者モードでない場合は、アクセス許可のエラーメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-337">If Visual Studio is not in administrator mode, you might get a permissions error message.</span></span> <span data-ttu-id="5cb4e-338">その場合は、Visual Studio を閉じて、管理者モードで開き、もう一度発行してみてください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-338">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

   <span data-ttu-id="5cb4e-339">Visual Studio が管理者モードの場合、 **[出力]** ウィンドウは成功したビルドと発行を報告します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-339">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   <span data-ttu-id="5cb4e-341">発行プロファイルの **[接続]** タブの **[送信先 url]** ボックスに url を入力した場合は、コンピューターの IIS で実行されている Contoso 大学のホームページがブラウザーによって自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-341">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on your computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="5cb4e-342">テスト環境でテストする</span><span class="sxs-lookup"><span data-stu-id="5cb4e-342">Test in the test environment</span></span>

<span data-ttu-id="5cb4e-343">環境インジケーターには、"(Dev)" ではなく "(Test)" と表示されます。これは、環境インジケーターの*web.config 変換が*成功したことを示しています。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-343">Notice that the environment indicator shows "(Test)" instead of "(Dev)," which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="5cb4e-344">インストラクターページを実行し**て、Code First**がインストラクターのデータでデータベースをシード処理したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-344">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="5cb4e-345">このページを選択すると、Code First によってデータベースが作成され、メソッドが`Seed`実行されるため、読み込みに数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-345">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="5cb4e-346">(これは、アプリケーションがデータベースにアクセスしようとしていないためにホームページを使用していた場合には行われませんでした)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-346">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="5cb4e-347">**[Students]** タブを選択して、デプロイされたデータベースに学生がいないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-347">Select the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="5cb4e-348">**学生**メニューから **[学生の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-348">Select **Add Students** from the **Students** menu.</span></span> <span data-ttu-id="5cb4e-349">学生を追加し、 **[Students]** ページで新しい学生を表示します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-349">Add a student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="5cb4e-350">これにより、データベースへの書き込みが正常に完了したことが確認されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-350">This verifies that you can successfully write to the database.</span></span>

<span data-ttu-id="5cb4e-351">**[コース]** メニューの **[クレジットの更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-351">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="5cb4e-352">**[更新プログラムのクレジット]** ページには管理者権限が必要であるため、 **[ログイン]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-352">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="5cb4e-353">前の手順で作成した管理者アカウントの資格情報を入力します ("admin" と "devpwd")。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-353">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="5cb4e-354">**[更新プログラムのクレジット]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-354">The **Update Credits** page is displayed.</span></span> <span data-ttu-id="5cb4e-355">これにより、前のチュートリアルで作成した管理者アカウントがテスト環境に正しく配置されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-355">This verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="5cb4e-356">*C:\inetpub\wwwroot\ContosoUniversity*フォルダー内に、プレースホルダーファイルのみを含む*ELMAH*フォルダーが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-356">Verify that an *ELMAH* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="5cb4e-357">Code First Migrations の web.config の自動変更を確認する</span><span class="sxs-lookup"><span data-stu-id="5cb4e-357">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="5cb4e-358">デプロイされたアプリケーションの*web.config*ファイルを*C:\inetpub\wwwroot\ContosoUniversity*で開き、データベースを最新バージョンに自動的に更新するように配置プロセスが構成さ Code First Migrations れている場所を確認できます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-358">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="5cb4e-359">また、配置プロセスでは、データベーススキーマを更新するために排他的に使用する Code First Migrations 用の新しい接続文字列も作成しました。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-359">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 接続文字列](deploying-to-iis/_static/image22.png)

<span data-ttu-id="5cb4e-361">この追加の接続文字列を使用すると、データベーススキーマの更新用に1つのユーザーアカウントを指定し、アプリケーションデータアクセスに別のユーザーアカウントを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-361">This additional connection string enables you to specify one user account for database schema updates and a different user account for application data access.</span></span> <span data-ttu-id="5cb4e-362">たとえば、db **\_所有者**ロールを Code First Migrations **\_** に割り当て、db datareader **\_ロールを**アプリケーションに割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-362">For example, you could assign the **db\_owner** role to Code First Migrations and **db\_datareader** with **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="5cb4e-363">これは、アプリケーション内の悪意のある可能性のあるコードによってデータベーススキーマが変更されないようにする、一般的な多層防御パターンです。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-363">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="5cb4e-364">(たとえば、SQL インジェクション攻撃が成功した場合に発生する可能性があります)。これらのチュートリアルでは、このパターンは使用しません。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-364">(For example, this might happen in a successful SQL injection attack.) These tutorials don't use this pattern.</span></span> <span data-ttu-id="5cb4e-365">このパターンをシナリオに実装するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-365">To implement this pattern in your scenario, take these steps:</span></span>

1. <span data-ttu-id="5cb4e-366">Web の**発行**ウィザードの **[設定]** タブで、完全なデータベーススキーマ更新権限を持つユーザーを指定する接続文字列を入力します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-366">In the **Publish Web** wizard under the **Settings** tab, enter the connection string that specifies a user with full database schema update permissions.</span></span> <span data-ttu-id="5cb4e-367">**[実行時にこの接続文字列を使用する]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-367">Clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="5cb4e-368">配置された web.config ファイルで、これが`DatabasePublish`接続文字列になります。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-368">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>

2. <span data-ttu-id="5cb4e-369">アプリケーションで実行時に使用する接続文字列の Web.config ファイル変換を作成します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-369">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="5cb4e-370">まとめ</span><span class="sxs-lookup"><span data-stu-id="5cb4e-370">Summary</span></span>

<span data-ttu-id="5cb4e-371">これで、開発用コンピューター上の IIS にアプリケーションを配置し、そこでテストしました。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-371">You've now deployed your application to IIS on your development computer and tested it there.</span></span>

![テストのホームページ](deploying-to-iis/_static/image23.png)

<span data-ttu-id="5cb4e-373">これにより、展開プロセスによって、アプリケーションのコンテンツが適切な場所にコピーされたことが確認されます (展開する必要のないファイルは除外されます)。また、展開時に IIS が正しく構成されていることを Web 配置ます。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-373">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy) and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="5cb4e-374">次のチュートリアルでは、まだ完了していない配置タスクを検索するテストをもう1つ実行します。この場合、 *Elm ah*フォルダーのフォルダーアクセス許可を設定します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-374">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elm ah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="5cb4e-375">詳細情報</span><span class="sxs-lookup"><span data-stu-id="5cb4e-375">More information</span></span>

<span data-ttu-id="5cb4e-376">Visual Studio で IIS または IIS Express を実行する方法の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-376">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="5cb4e-377">IIS.net サイトの[IIS Express の概要](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-377">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="5cb4e-378">Scott Guthrie のブログで[IIS Express を紹介](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-378">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="5cb4e-379">[ASP.NET Web プロジェクトのための Visual Studio の Web サーバー](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-379">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="5cb4e-380">[IIS と](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)ASP.NET サイトの ASP.NET 開発サーバーの主な相違点。</span><span class="sxs-lookup"><span data-stu-id="5cb4e-380">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="5cb4e-381">アプリケーションが中程度の信頼で実行されている場合に発生する可能性がある問題の詳細については、Rolla サイトの4人の担当者に[おける中程度の信頼での ASP.NET アプリケーションのホスティング](http://www.4guysfromrolla.com/articles/100307-1.aspx)</span><span class="sxs-lookup"><span data-stu-id="5cb4e-381">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the four Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5cb4e-382">[前へ](project-properties.md)
> [次へ](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="5cb4e-382">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
