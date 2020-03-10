---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'チュートリアル: SignalR セルフホスト |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、自己ホスト型 SignalR 2 サーバーを作成する方法と、JavaScript クライアントを使用してそれに接続する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョン...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450166"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="e7ab3-104">チュートリアル: SignalR 自己ホスト</span><span class="sxs-lookup"><span data-stu-id="e7ab3-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="e7ab3-105">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="e7ab3-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="e7ab3-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="e7ab3-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="e7ab3-107">このチュートリアルでは、自己ホスト型 SignalR 2 サーバーを作成する方法と、JavaScript クライアントを使用してそれに接続する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e7ab3-108">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="e7ab3-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="e7ab3-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e7ab3-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="e7ab3-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e7ab3-110">.NET 4.5</span></span>
> - <span data-ttu-id="e7ab3-111">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="e7ab3-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="e7ab3-112">このチュートリアルでの Visual Studio 2012 の使用</span><span class="sxs-lookup"><span data-stu-id="e7ab3-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="e7ab3-113">このチュートリアルで Visual Studio 2012 を使用するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="e7ab3-114">[パッケージマネージャー](http://docs.nuget.org/docs/start-here/installing-nuget)を最新バージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="e7ab3-115">[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="e7ab3-116">Web Platform Installer で、 **Visual Studio 2012 の ASP.NET and Web Tools 2013.1**を検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="e7ab3-117">これにより、 **Hub**などの SignalR クラスの Visual Studio テンプレートがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="e7ab3-118">一部のテンプレート ( **OWIN Startup クラス**など) は使用できません。これらの場合は、代わりにクラスファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="e7ab3-119">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="e7ab3-119">Questions and comments</span></span>
>
> <span data-ttu-id="e7ab3-120">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e7ab3-121">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="e7ab3-122">概要</span><span class="sxs-lookup"><span data-stu-id="e7ab3-122">Overview</span></span>

<span data-ttu-id="e7ab3-123">SignalR サーバーは通常、IIS の ASP.NET アプリケーションでホストされますが、自己ホストライブラリを使用して自己ホスト型 (コンソールアプリケーションや Windows サービスなど) にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="e7ab3-124">このライブラリは、すべての SignalR 2 と同様に、OWIN ([Open Web Interface for .net](http://owin.org)) 上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="e7ab3-125">OWIN は、.NET web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="e7ab3-126">OWIN は、サーバーから web アプリケーションを分離します。これにより、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするために OWIN が理想的になります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="e7ab3-127">IIS でホストしない理由には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="e7ab3-128">Iis を使用しない既存のサーバーファームなど、IIS が利用できないか望ましくない環境。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="e7ab3-129">IIS のパフォーマンスのオーバーヘッドを回避する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="e7ab3-130">SignalR 機能は、Windows サービス、Azure ワーカーロール、またはその他のプロセスで実行される既存のアプリケーションに追加されます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="e7ab3-131">パフォーマンス上の理由により、ソリューションが自己ホストとして開発されている場合は、IIS でホストされているアプリケーションをテストしてパフォーマンスの利点を確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="e7ab3-132">このチュートリアルは、次のセクションで構成されています。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="e7ab3-133">サーバーの作成</span><span class="sxs-lookup"><span data-stu-id="e7ab3-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="e7ab3-134">JavaScript クライアントを使用したサーバーへのアクセス</span><span class="sxs-lookup"><span data-stu-id="e7ab3-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="e7ab3-135">サーバーの作成</span><span class="sxs-lookup"><span data-stu-id="e7ab3-135">Creating the server</span></span>

<span data-ttu-id="e7ab3-136">このチュートリアルでは、コンソールアプリケーションでホストされているサーバーを作成しますが、サーバーは、Windows サービスや Azure worker ロールなどの任意の種類のプロセスでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="e7ab3-137">Windows サービスで SignalR サーバーをホストするためのサンプルコードについては、「 [Windows サービスでの自己ホスト SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="e7ab3-138">管理者特権で Visual Studio 2013 を開きます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="e7ab3-139">**[ファイル]** 、 **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="e7ab3-140">**[テンプレート]** ウィンドウで、**ビジュアルC#** ノードの下にある **[Windows]** を選択し、 **[コンソールアプリケーション]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="e7ab3-141">新しいプロジェクトに "SignalRSelfHost" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="e7ab3-142">**[ツール]**  >  **[nuget パッケージマネージャー]**  >  **[パッケージマネージャーコンソール]** の順に選択して、nuget パッケージマネージャーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="e7ab3-143">パッケージマネージャーコンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="e7ab3-144">このコマンドは、SignalR 2 の自己ホストライブラリをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="e7ab3-145">パッケージマネージャーコンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="e7ab3-146">このコマンドは、Owin ライブラリをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="e7ab3-147">このライブラリは、ドメイン間のサポートに使用されます。これは、SignalR をホストするアプリケーションと、異なるドメインの web ページクライアントに必要です。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="e7ab3-148">SignalR サーバーと web クライアントを別のポートでホストするため、これは、これらのコンポーネント間の通信に対してクロスドメインを有効にする必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="e7ab3-149">Program.cs の内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="e7ab3-150">上記のコードには、次の3つのクラスがあります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="e7ab3-151">実行のプライマリパスを定義する**Main**メソッドを含む**プログラム**。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="e7ab3-152">このメソッドでは、 **Startup**という種類の web アプリケーションが、指定された URL (`http://localhost:8080`) で開始されます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="e7ab3-153">エンドポイントでセキュリティが必要な場合は、SSL を実装できます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="e7ab3-154">詳細については[、「方法: SSL 証明書を使用してポートを構成する](https://msdn.microsoft.com/library/ms733791.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="e7ab3-155">SignalR サーバーの構成を含むクラス (**このチュートリアル**で使用される唯一の構成は `UseCors`) と、`MapSignalR`への呼び出しで、プロジェクト内の任意のハブオブジェクトのルートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="e7ab3-156">**Myhub**。アプリケーションがクライアントに提供する SignalR Hub クラスです。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="e7ab3-157">このクラスには、**送信**される1つのメソッドがあります。このメソッドは、クライアントがを呼び出して、接続されている他のすべてのクライアントにメッセージをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="e7ab3-158">アプリケーションをコンパイルして実行します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-158">Compile and run the application.</span></span> <span data-ttu-id="e7ab3-159">サーバーが実行されているアドレスは、コンソールウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="e7ab3-160">例外 `System.Reflection.TargetInvocationException was unhandled`で実行が失敗した場合は、管理者特権で Visual Studio を再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="e7ab3-161">次のセクションに進む前に、アプリケーションを停止します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="e7ab3-162">JavaScript クライアントを使用したサーバーへのアクセス</span><span class="sxs-lookup"><span data-stu-id="e7ab3-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="e7ab3-163">このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)と同じ JavaScript クライアントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="e7ab3-164">クライアントに対して変更を1つだけ行います。これは、ハブの URL を明示的に定義するためのものです。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="e7ab3-165">自己ホスト型アプリケーションでは、サーバーが接続 URL と (リバースプロキシおよびロードバランサーによる) 同じアドレスにあるとは限りません。そのため、URL を明示的に定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="e7ab3-166">**ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="e7ab3-167">**[Web]** ノードを選択し、 **[ASP.NET web アプリケーション]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="e7ab3-168">プロジェクトに "JavascriptClient" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="e7ab3-169">**空**のテンプレートを選択し、残りのオプションは選択解除したままにします。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="e7ab3-170">**[プロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="e7ab3-171">パッケージマネージャーコンソールで、 **[既定のプロジェクト]** ドロップダウンで "JavascriptClient" プロジェクトを選択し、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="e7ab3-172">このコマンドを実行すると、クライアントに必要な SignalR および JQuery ライブラリがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="e7ab3-173">プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="e7ab3-174">**[Web]** ノードを選択し、[HTML ページ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="e7ab3-175">ページに「 **Default .html**」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="e7ab3-176">新しい HTML ページの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="e7ab3-177">ここで参照されているスクリプトが、プロジェクトの Scripts フォルダー内のスクリプトと一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="e7ab3-178">次のコード (上記のコードサンプルで強調表示されています) は、「SignalR バージョン 2 beta」にコードをアップグレードするだけでなく、入門チュートリアルで使用したクライアントに対する追加のコードです。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="e7ab3-179">このコード行は、サーバー上の SignalR のベース接続 URL を明示的に設定します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="e7ab3-180">ソリューションを右クリックし、 **[スタートアッププロジェクトの設定]** ... を選択します。 **[マルチスタートアッププロジェクト]** オプションボタンを選択し、両方のプロジェクトの **[アクション]** を **[開始]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="e7ab3-181">"Default .html" を右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="e7ab3-182">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-182">Run the application.</span></span> <span data-ttu-id="e7ab3-183">サーバーとページが起動します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-183">The server and page will launch.</span></span> <span data-ttu-id="e7ab3-184">サーバーが起動する前にページが読み込まれた場合は、web ページの再読み込みが必要になることがあります (または、デバッガーで **[続行]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="e7ab3-185">ブラウザーで、プロンプトが表示されたらユーザー名を入力します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="e7ab3-186">ページの URL を別のブラウザータブまたはウィンドウにコピーし、別のユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="e7ab3-187">はじめにのチュートリアルのように、ブラウザーウィンドウ間でメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="e7ab3-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
