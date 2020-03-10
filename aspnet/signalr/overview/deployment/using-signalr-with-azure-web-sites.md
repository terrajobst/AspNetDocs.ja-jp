---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service | の Web Apps での SignalR の使用Microsoft Docs
author: bradygaster
description: このドキュメントでは Microsoft Azure で実行される SignalR アプリケーションを構成する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョン Visual Studio 2013 または Vis...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450184"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="20aa2-104">Azure App Service の Web アプリで SignalR を使用する</span><span class="sxs-lookup"><span data-stu-id="20aa2-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="20aa2-105">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="20aa2-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="20aa2-106">このドキュメントでは Microsoft Azure で実行される SignalR アプリケーションを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="20aa2-107">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="20aa2-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="20aa2-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)または Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="20aa2-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="20aa2-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="20aa2-109">.NET 4.5</span></span>
> - <span data-ttu-id="20aa2-110">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="20aa2-110">SignalR version 2</span></span>
> - <span data-ttu-id="20aa2-111">Visual Studio 2013 または2012用の Azure SDK 2.3</span><span class="sxs-lookup"><span data-stu-id="20aa2-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="20aa2-112">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="20aa2-112">Questions and comments</span></span>
>
> <span data-ttu-id="20aa2-113">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="20aa2-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="20aa2-114">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)、または[Microsoft Azure フォーラム](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)に投稿することができます。</span><span class="sxs-lookup"><span data-stu-id="20aa2-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="20aa2-115">目次</span><span class="sxs-lookup"><span data-stu-id="20aa2-115">Table of Contents</span></span>

- [<span data-ttu-id="20aa2-116">はじめに</span><span class="sxs-lookup"><span data-stu-id="20aa2-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="20aa2-117">Azure App Service するための SignalR Web アプリのデプロイ</span><span class="sxs-lookup"><span data-stu-id="20aa2-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="20aa2-118">Azure App Service での Websocket の有効化</span><span class="sxs-lookup"><span data-stu-id="20aa2-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="20aa2-119">Azure Redis Cache バックプレーンの使用</span><span class="sxs-lookup"><span data-stu-id="20aa2-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="20aa2-120">次の手順</span><span class="sxs-lookup"><span data-stu-id="20aa2-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="20aa2-121">はじめに</span><span class="sxs-lookup"><span data-stu-id="20aa2-121">Introduction</span></span>

<span data-ttu-id="20aa2-122">ASP.NET SignalR を使用すると、サーバーと web クライアントまたは .NET クライアントの間に新しいレベルの対話性をもたらすことができます。</span><span class="sxs-lookup"><span data-stu-id="20aa2-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="20aa2-123">Azure でホストされている場合、SignalR アプリケーションは、クラウドで実行されている高可用性、拡張性、およびパフォーマンスに優れた環境を活用できます。</span><span class="sxs-lookup"><span data-stu-id="20aa2-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="20aa2-124">Azure App Service するための SignalR Web アプリのデプロイ</span><span class="sxs-lookup"><span data-stu-id="20aa2-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="20aa2-125">SignalR は、アプリケーションを Azure にデプロイしたり、オンプレミスのサーバーにデプロイしたりするために、特定の複雑さを追加することはありません。</span><span class="sxs-lookup"><span data-stu-id="20aa2-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="20aa2-126">SignalR を使用するアプリケーションは、構成やその他の設定を変更することなく Azure でホストできます (ただし、Websocket のサポートについては、以下[の Azure App Service で websocket を有効](#websocket)にする方法に関する説明を参照してください)。このチュートリアルでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションを Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="20aa2-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="20aa2-127">**前提条件**</span><span class="sxs-lookup"><span data-stu-id="20aa2-127">**Prerequisites**</span></span>

- <span data-ttu-id="20aa2-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="20aa2-128">Visual Studio 2013.</span></span> <span data-ttu-id="20aa2-129">Visual Studio をお持ちでない場合は、Azure SDK のインストールに Visual Studio 2013 Express for Web が含まれています。</span><span class="sxs-lookup"><span data-stu-id="20aa2-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="20aa2-130">[Visual Studio 2013 の場合は AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 、 [Visual Studio 2012 の場合は azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。</span><span class="sxs-lookup"><span data-stu-id="20aa2-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="20aa2-131">このチュートリアルを完了するには、Azure サブスクリプションが必要です。</span><span class="sxs-lookup"><span data-stu-id="20aa2-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="20aa2-132">[MSDN サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)にすることも、[試用版サブスクリプションにサインアップ](https://azure.microsoft.com/pricing/free-trial/)することもできます。</span><span class="sxs-lookup"><span data-stu-id="20aa2-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="20aa2-133">SignalR web アプリを Azure にデプロイする</span><span class="sxs-lookup"><span data-stu-id="20aa2-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="20aa2-134">[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)を完了するか、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)から完成したプロジェクトをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="20aa2-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="20aa2-135">Visual Studio で、 **[ビルド]** 、 **[Publish SignalR Chat]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="20aa2-136">[Web の発行] ダイアログで、[Windows Azure Websites] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Azure Websites の選択](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="20aa2-138">Microsoft アカウントにサインインしていない場合は、既存の Web サイトの選択 ダイアログボックスで **サインイン...** をクリックし、サインインします。</span><span class="sxs-lookup"><span data-stu-id="20aa2-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![既存の Web サイトの選択](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure へのサインイン](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="20aa2-141">既存の Web サイトの選択 ダイアログボックスで、**新規** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20aa2-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![[新しい Web サイト]](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="20aa2-143">[Windows Azure でのサイトの作成] ダイアログボックスで、一意のアプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="20aa2-144">[リージョン] ボックスの一覧で、最も近いリージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="20aa2-145">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="20aa2-145">Click **Create**.</span></span>

    ![Azure でのサイトの作成](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="20aa2-147">Web の発行 ダイアログで、**発行** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20aa2-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![サイトの発行](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="20aa2-149">アプリの発行が完了すると、Azure App Service Web Apps でホストされている SignalR Chat アプリケーションがブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="20aa2-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![ブラウザーでサイトを開く](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="20aa2-151">Azure App Service Web Apps で Websocket を有効にする</span><span class="sxs-lookup"><span data-stu-id="20aa2-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="20aa2-152">SignalR アプリケーションで使用するには、web アプリで Websocket を明示的に有効にする必要があります。それ以外の場合は、他のプロトコルが使用されます (詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="20aa2-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="20aa2-153">Azure App Service Web Apps で Websocket を使用するには、Web アプリの [構成] セクションで有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="20aa2-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="20aa2-154">これを行うには、 [Azure 管理ポータル](https://manage.windowsazure.com/)で web アプリを開き、[構成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![[Configure (構成)] タブ](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="20aa2-156">[構成] ページの上部で、web アプリに .NET 4.5 が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework バージョン4.5 設定](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="20aa2-158">構成 ページの  **websocket** 設定で、**オン** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Websocket の設定: オン](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="20aa2-160">構成ページの下部にある **[保存]** を選択して変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="20aa2-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![設定の保存](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="20aa2-162">Azure Redis Cache バックプレーンの使用</span><span class="sxs-lookup"><span data-stu-id="20aa2-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="20aa2-163">Web アプリに複数のインスタンスを使用し、それらのインスタンスのユーザーが相互に対話する必要がある場合 (たとえば、1つのインスタンスで作成されたチャットメッセージが、他のインスタンスに接続されているユーザーに到着する可能性がある場合)、 [Azure Redis Cache バックプレーン](../performance/scaleout-with-redis.md)をアプリケーションに実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20aa2-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="20aa2-164">次の手順</span><span class="sxs-lookup"><span data-stu-id="20aa2-164">Next Steps</span></span>

<span data-ttu-id="20aa2-165">Azure App Service の Web Apps の詳細については、「 [Web Apps の概要](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20aa2-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
