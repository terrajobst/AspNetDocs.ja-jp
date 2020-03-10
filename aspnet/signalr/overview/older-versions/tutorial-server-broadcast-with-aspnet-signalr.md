---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 'チュートリアル: ASP.NET SignalR 1.x を使用したサーバーブロードキャスト |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。 サーバーブロードキャストは、communic...
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467932"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a><span data-ttu-id="d8a6b-104">チュートリアル: ASP.NET SignalR 1.x を使用したサーバーブロードキャスト</span><span class="sxs-lookup"><span data-stu-id="d8a6b-104">Tutorial: Server Broadcast with ASP.NET SignalR 1.x</span></span>

<span data-ttu-id="d8a6b-105">[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d8a6b-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d8a6b-106">このチュートリアルでは、ASP.NET SignalR を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide server broadcast functionality.</span></span> <span data-ttu-id="d8a6b-107">サーバーブロードキャストとは、クライアントに送信される通信がサーバーによって開始されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="d8a6b-108">このシナリオでは、クライアントに送信される通信が1つまたは複数のクライアントによって開始される、チャットアプリケーションなどのピアツーピアシナリオとは異なるプログラミングアプローチが必要です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="d8a6b-109">このチュートリアルで作成するアプリケーションは、サーバーブロードキャスト機能の一般的なシナリオである株式ティッカーをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="d8a6b-110">このチュートリアルのコメントは歓迎しています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-110">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="d8a6b-111">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-111">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="d8a6b-112">概要</span><span class="sxs-lookup"><span data-stu-id="d8a6b-112">Overview</span></span>

<span data-ttu-id="d8a6b-113">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet パッケージは、サンプルのシミュレートされた株式ティッカーアプリケーションを Visual Studio プロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-113">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span> <span data-ttu-id="d8a6b-114">このチュートリアルの最初の部分では、そのアプリケーションの簡略化されたバージョンをゼロから作成します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-114">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="d8a6b-115">このチュートリアルの残りの部分では、NuGet パッケージをインストールし、作成する追加機能とコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-115">In the remainder of the tutorial, you'll install the NuGet package and review the additional features and code that it creates.</span></span>

<span data-ttu-id="d8a6b-116">Stock ティッカーアプリケーションは、サーバーからすべての接続されたクライアントへの通知を定期的に "プッシュ" またはブロードキャストする、一種のリアルタイムアプリケーションの代表です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-116">The stock ticker application is a representative of a kind of real-time application in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span>

<span data-ttu-id="d8a6b-117">このチュートリアルの最初の部分で作成するアプリケーションには、在庫データを含むグリッドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-117">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker の初期バージョン](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

<span data-ttu-id="d8a6b-119">定期的にサーバーは株価をランダムに更新し、接続されているすべてのクライアントに更新をプッシュします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-119">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="d8a6b-120">ブラウザーでは、サーバーからの通知に応じて、 **[変更]** 列と [ **%** ] 列の数値と記号が動的に変更されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-120">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="d8a6b-121">同じ URL に対して追加のブラウザーを開くと、すべてのブラウザーで同じデータと同じデータの変更が同時に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-121">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="d8a6b-122">このチュートリアルは、次のセクションで構成されています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-122">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="d8a6b-123">前提条件</span><span class="sxs-lookup"><span data-stu-id="d8a6b-123">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="d8a6b-124">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-124">Create the project</span></span>](#createproject)
- [<span data-ttu-id="d8a6b-125">SignalR NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-125">Add the SignalR NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="d8a6b-126">サーバーコードの設定</span><span class="sxs-lookup"><span data-stu-id="d8a6b-126">Set up the server code</span></span>](#server)
- [<span data-ttu-id="d8a6b-127">クライアントコードの設定</span><span class="sxs-lookup"><span data-stu-id="d8a6b-127">Set up the client code</span></span>](#client)
- [<span data-ttu-id="d8a6b-128">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="d8a6b-128">Test the application</span></span>](#test)
- [<span data-ttu-id="d8a6b-129">ログ記録を有効化する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-129">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="d8a6b-130">完全な StockTicker サンプルをインストールして確認する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-130">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="d8a6b-131">次の手順</span><span class="sxs-lookup"><span data-stu-id="d8a6b-131">Next steps</span></span>](#nextsteps)

> [!NOTE]
> <span data-ttu-id="d8a6b-132">アプリケーションをビルドする手順を実行しない場合は、新しい**空の ASP.NET Web アプリケーション**プロジェクトに SignalR パッケージをインストールし、これらの手順を読んでコードの説明を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-132">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new **Empty ASP.NET Web Application** project, and read through these steps to get explanations of the code.</span></span> <span data-ttu-id="d8a6b-133">このチュートリアルの最初の部分では、SignalR コードのサブセットについて説明します。2番目の部分では、SignalR パッケージの追加機能の主な機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-133">The first part of the tutorial covers a subset of the SignalR.Sample code, and the second part explains key features of the additional functionality in the SignalR.Sample package.</span></span>

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="d8a6b-134">前提条件</span><span class="sxs-lookup"><span data-stu-id="d8a6b-134">Prerequisites</span></span>

<span data-ttu-id="d8a6b-135">開始する前に、コンピューターに Visual Studio 2012 または 2010 SP1 がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-135">Before you start, make sure that you have Visual Studio 2012 or 2010 SP1 installed on your computer.</span></span> <span data-ttu-id="d8a6b-136">Visual Studio をお持ちでない場合は、無料の Visual Studio 2012 Express for Web を入手するには、 [ASP.NET のダウンロード](https://www.asp.net/downloads)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-136">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express for Web.</span></span>

<span data-ttu-id="d8a6b-137">Visual Studio 2010 を使用している場合は、 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-137">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="d8a6b-138">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-138">Create the project</span></span>

1. <span data-ttu-id="d8a6b-139">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-139">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="d8a6b-140">**[新しいプロジェクト]** ダイアログボックスの [ **C#** **テンプレート**] で展開し、 **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-140">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="d8a6b-141">**[ASP.NET 空の Web アプリケーション]** テンプレートを選択し、プロジェクトに*SignalR*という名前を指定して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-141">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![New Project dialog box](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a><span data-ttu-id="d8a6b-143">SignalR NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-143">Add the SignalR NuGet Packages</span></span>

### <a name="add-the-signalr-and-jquery-nuget-packages"></a><span data-ttu-id="d8a6b-144">SignalR および JQuery NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-144">Add the SignalR and JQuery NuGet Packages</span></span>

<span data-ttu-id="d8a6b-145">NuGet パッケージをインストールすることによって、SignalR 機能をプロジェクトに追加できます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-145">You can add SignalR functionality to a project by installing a NuGet package.</span></span>

1. <span data-ttu-id="d8a6b-146">[ツール] をクリックします。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-146">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="d8a6b-147">パッケージマネージャーで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-147">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    <span data-ttu-id="d8a6b-148">SignalR パッケージは、他のいくつかの NuGet パッケージを依存関係としてインストールします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-148">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="d8a6b-149">インストールが完了すると、ASP.NET アプリケーションで SignalR を使用するために必要なすべてのサーバーおよびクライアントコンポーネントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-149">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="d8a6b-150">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-150">Set up the server code</span></span>

<span data-ttu-id="d8a6b-151">このセクションでは、サーバーで実行するコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-151">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="d8a6b-152">Stock クラスを作成する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-152">Create the Stock class</span></span>

<span data-ttu-id="d8a6b-153">まず、在庫に関する情報を格納して送信するために使用するストックモデルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-153">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="d8a6b-154">プロジェクトフォルダーに新しいクラスファイルを作成し、 *Stock.cs*という名前を付けて、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-154">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    <span data-ttu-id="d8a6b-155">株式の作成時に設定する2つのプロパティは、記号 (たとえば、Microsoft の場合は MSFT) と価格です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-155">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="d8a6b-156">その他のプロパティは、価格を設定する方法とタイミングによって異なります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-156">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="d8a6b-157">価格を初めて設定すると、値は DayOpen に反映されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-157">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="d8a6b-158">Price を設定した後に、Change プロパティと PercentChange プロパティの値は、Price と DayOpen の差に基づいて計算されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-158">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="d8a6b-159">StockTicker および Stockticker クラスを作成する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-159">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="d8a6b-160">SignalR Hub API を使用して、サーバー間の対話を処理します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-160">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="d8a6b-161">SignalR Hub クラスから派生する StockTickerHub クラスは、クライアントからの接続の受信とメソッドの呼び出しを処理します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-161">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="d8a6b-162">また、在庫データを保持し、タイマーオブジェクトを実行して、クライアント接続とは関係なく、定期的に価格更新をトリガーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-162">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="d8a6b-163">ハブインスタンスは一時的なものであるため、これらの関数をハブクラスに配置することはできません。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-163">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="d8a6b-164">ハブクラスのインスタンスは、接続や、クライアントからサーバーへの呼び出しなど、ハブ上の各操作に対して作成されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-164">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="d8a6b-165">そのため、株価データを保持するメカニズム、価格の更新、価格更新のブロードキャストは、別のクラスで実行する必要があります。このクラスには、StockTicker という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-165">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![StockTicker からのブロードキャスト](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

<span data-ttu-id="d8a6b-167">サーバー上で実行される StockTicker クラスのインスタンスは1つだけなので、各 Stockticker インスタンスからシングルトン StockTicker インスタンスへの参照を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-167">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="d8a6b-168">StockTicker クラスは、在庫データを持ち、更新をトリガーするため、クライアントにブロードキャストできる必要がありますが、StockTicker はハブクラスではありません。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-168">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="d8a6b-169">そのため、StockTicker クラスは、SignalR Hub 接続コンテキストオブジェクトへの参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-169">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="d8a6b-170">その後、SignalR 接続コンテキストオブジェクトを使用して、クライアントにブロードキャストできます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-170">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="d8a6b-171">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[新しい項目の追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-171">In **Solution Explorer**, right-click the project and click **Add New Item**.</span></span>
2. <span data-ttu-id="d8a6b-172">[ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=279941)がインストールされた visual Studio 2012 を使用している場合は、 **[ビジュアルC# ]** の下にある **[Web]** をクリックし、 **SignalR Hub クラス**項目テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-172">If you have Visual Studio 2012 with the [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=279941), click **Web** under **Visual C#** and select the **SignalR Hub Class** item template.</span></span> <span data-ttu-id="d8a6b-173">それ以外の場合は、 **[クラス]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-173">Otherwise, select the **Class** template.</span></span>
3. <span data-ttu-id="d8a6b-174">新しいクラスに*StockTickerHub.cs*という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-174">Name the new class *StockTickerHub.cs*, and then click **Add**.</span></span>

    ![StockTickerHub.cs の追加](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. <span data-ttu-id="d8a6b-176">テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-176">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    <span data-ttu-id="d8a6b-177">[ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスは、クライアントがサーバーで呼び出すことができるメソッドを定義するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-177">The [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="d8a6b-178">1つのメソッドを定義しています: `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-178">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="d8a6b-179">クライアントは、最初にサーバーに接続するときに、このメソッドを呼び出して、すべての株式の一覧を現在の価格で取得します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-179">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="d8a6b-180">メソッドは、メモリからデータを返すため、同期的に実行し、`IEnumerable<Stock>` を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-180">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="d8a6b-181">データベース参照や web サービス呼び出しなど、待機する必要のある処理を実行してデータを取得する必要がある場合は、`Task<IEnumerable<Stock>>` を戻り値として指定して、非同期処理を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-181">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="d8a6b-182">詳細については、「 [ASP.NET SignalR HUB API Guide-Server-非同期に実行するタイミング](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-182">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](index.md).</span></span>

    <span data-ttu-id="d8a6b-183">HubName 属性は、クライアントの JavaScript コードでハブを参照する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-183">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="d8a6b-184">この属性を使用しない場合のクライアントの既定の名前は、camel 形式のクラス名です。この場合、この例では、"Stock" になります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-184">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="d8a6b-185">後で説明するように、StockTicker クラスを作成すると、そのクラスのシングルトンインスタンスが静的インスタンスプロパティに作成されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-185">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="d8a6b-186">接続または切断するクライアントの数に関係なく、StockTicker のシングルトンインスタンスはメモリに残ります。そのインスタンスは、GetAllStocks メソッドが現在の株価情報を返すために使用するものです。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-186">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
5. <span data-ttu-id="d8a6b-187">プロジェクトフォルダーに新しいクラスファイルを作成し、 *StockTicker.cs*という名前を付けて、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-187">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    <span data-ttu-id="d8a6b-188">複数のスレッドが同じ StockTicker コードのインスタンスを実行するため、StockTicker クラスを threadsafe する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-188">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="d8a6b-189">静的フィールドへのシングルトンインスタンスの格納</span><span class="sxs-lookup"><span data-stu-id="d8a6b-189">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="d8a6b-190">このコードは、インスタンスプロパティをクラスのインスタンスとバックする静的 \_インスタンスフィールドを初期化します。これは、コンストラクターがプライベートとしてマークされているため、作成可能なクラスの唯一のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-190">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="d8a6b-191">[遅延初期化](https://msdn.microsoft.com/library/dd997286.aspx)は、パフォーマンス上の理由ではなく、\_インスタンスフィールドに使用されますが、インスタンスの作成が threadsafe されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-191">[Lazy initialization](https://msdn.microsoft.com/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    <span data-ttu-id="d8a6b-192">クライアントがサーバーに接続するたびに、別のスレッドで実行されている StockTickerHub クラスの新しいインスタンスが、StockTickerHub クラスで既に説明したように、stockティッカーシングルトンインスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-192">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="d8a6b-193">ConcurrentDictionary に株式データを格納する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-193">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="d8a6b-194">コンストラクターは、いくつかのサンプル株式データを使用して \_の株式コレクションを初期化し、GetAllStocks は株式を返します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-194">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="d8a6b-195">既に説明したように、この株式のコレクションは、クライアントが呼び出すことのできるハブクラスのサーバーメソッドである GetAllStocks によって返されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-195">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    <span data-ttu-id="d8a6b-196">株式コレクションは、スレッドセーフの[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-196">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="d8a6b-197">別の方法として、 [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、変更を行うときに明示的にディクショナリをロックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-197">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="d8a6b-198">このサンプルアプリケーションでは、アプリケーションデータをメモリに格納し、StockTicker インスタンスが破棄されたときにデータを失わせることができます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-198">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="d8a6b-199">実際のアプリケーションでは、データベースなどのバックエンドデータストアを使用します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-199">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="d8a6b-200">株価を定期的に更新する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-200">Periodically updating stock prices</span></span>

    <span data-ttu-id="d8a6b-201">コンストラクターは、在庫価格をランダムに更新するメソッドを定期的に呼び出すタイマーオブジェクトを開始します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-201">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    <span data-ttu-id="d8a6b-202">UpdateStockPrices は、state パラメーターに null を渡すタイマーによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-202">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="d8a6b-203">価格を更新する前に、\_updateStockPricesLock オブジェクトに対してロックが取得されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-203">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="d8a6b-204">このコードでは、別のスレッドが既に価格を更新しているかどうかを確認し、一覧の各株式で TryUpdateStockPrice を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-204">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="d8a6b-205">TryUpdateStockPrice メソッドは、株価を変更するかどうか、および変更する量を決定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-205">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="d8a6b-206">株価が変更された場合、BroadcastStockPrice が呼び出され、すべての接続されたクライアントに株価の変更がブロードキャストされます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-206">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="d8a6b-207">\_updatingStockPrices フラグは、threadsafe にアクセスできるように、 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)としてマークされています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-207">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    <span data-ttu-id="d8a6b-208">実際のアプリケーションでは、TryUpdateStockPrice メソッドは web サービスを呼び出して価格を検索します。このコードでは、ランダムな数値ジェネレーターを使用して、変更をランダムに行います。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-208">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="d8a6b-209">SignalR コンテキストを取得して、StockTicker クラスがクライアントにブロードキャストできるようにする</span><span class="sxs-lookup"><span data-stu-id="d8a6b-209">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="d8a6b-210">ここでは、価格の変更は StockTicker オブジェクトで行われるため、接続されているすべてのクライアントで updateStockPrice メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-210">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="d8a6b-211">ハブクラスでは、クライアントメソッドを呼び出すための API がありますが、StockTicker はハブクラスから派生しておらず、どのハブオブジェクトへの参照も持っていません。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-211">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="d8a6b-212">したがって、接続されたクライアントにブロードキャストするために、StockTicker クラスは、Stockticker クラスの SignalR context インスタンスを取得し、それを使用してクライアントでメソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-212">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="d8a6b-213">このコードは、シングルトンクラスのインスタンスを作成するときに SignalR コンテキストへの参照を取得し、その参照をコンストラクターに渡し、コンストラクターがそれをクライアントプロパティに格納します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-213">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="d8a6b-214">コンテキストを一度だけ取得する理由は2つあります。コンテキストの取得は負荷の高い操作であるため、一度取得すると、クライアントに送信されるメッセージの順序が確実に維持されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-214">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    <span data-ttu-id="d8a6b-215">コンテキストのクライアントプロパティを取得し、それを Stockclients クライアントプロパティに格納すると、ハブクラスと同じように見えるクライアントメソッドを呼び出すためのコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-215">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="d8a6b-216">たとえば、すべてのクライアントにブロードキャストするには、クライアントを作成します。すべての updateStockPrice (stock).</span><span class="sxs-lookup"><span data-stu-id="d8a6b-216">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="d8a6b-217">BroadcastStockPrice で呼び出されている updateStockPrice メソッドはまだ存在しません。クライアントで実行されるコードを記述するときに、後で追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-217">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="d8a6b-218">クライアントが動的であるため、ここでは updateStockPrice を参照できます。これは、実行時に式が評価されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-218">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="d8a6b-219">このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。クライアントに updateStockPrice という名前のメソッドがある場合は、そのメソッドが呼び出され、パラメーター値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-219">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="d8a6b-220">クライアント。 All はすべてのクライアントに送信することを意味します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-220">Clients.All means send to all clients.</span></span> <span data-ttu-id="d8a6b-221">SignalR には、に送信するクライアントまたはクライアントのグループを指定するための他のオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-221">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="d8a6b-222">詳細については、「 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-222">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="d8a6b-223">SignalR ルートを登録する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-223">Register the SignalR route</span></span>

<span data-ttu-id="d8a6b-224">サーバーは、インターセプトする URL と SignalR に送信する URL を認識している必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-224">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="d8a6b-225">そのためには、 *global.asax*ファイルにいくつかのコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-225">To do that you'll add some code to the *Global.asax* file.</span></span>

1. <span data-ttu-id="d8a6b-226">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[新しい項目の追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-226">In **Solution Explorer**, right-click the project, and then click **Add New Item**.</span></span>
2. <span data-ttu-id="d8a6b-227">**グローバルアプリケーションクラス**項目テンプレートを選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-227">Select the **Global Application Class** item template, and then click **Add**.</span></span>

    ![Global.asax の追加](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. <span data-ttu-id="d8a6b-229">SignalR route 登録コードをアプリケーション\_の開始メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-229">Add the SignalR route registration code to the Application\_Start method:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    <span data-ttu-id="d8a6b-230">既定では、すべての SignalR トラフィックのベース URL は "/signalr" で、"/signalr/hubs" は、アプリケーション内のすべてのハブのプロキシを定義する動的に生成された JavaScript ファイルを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-230">By default, the base URL for all SignalR traffic is "/signalr", and "/signalr/hubs" is used to retrieve a dynamically generated JavaScript file that defines proxies for all the Hubs you have in your application.</span></span> <span data-ttu-id="d8a6b-231">MapHubs メソッドには、 [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)クラスのインスタンスで別のベース URL と特定の SignalR オプションを指定できるオーバーロードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-231">The MapHubs method includes overloads that let you specify a different base URL and certain SignalR options in an instance of the [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) class.</span></span>
4. <span data-ttu-id="d8a6b-232">ファイルの先頭に using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-232">Add a using statement at the top of the file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. <span data-ttu-id="d8a6b-233">*Global.asax*ファイルを保存して閉じ、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-233">Save and close the *Global.asax* file, and build the project.</span></span>

<span data-ttu-id="d8a6b-234">これで、サーバーコードの設定が完了しました。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-234">You have now completed setting up the server code.</span></span> <span data-ttu-id="d8a6b-235">次のセクションでは、クライアントを設定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-235">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="d8a6b-236">クライアントコードの設定</span><span class="sxs-lookup"><span data-stu-id="d8a6b-236">Set up the client code</span></span>

1. <span data-ttu-id="d8a6b-237">プロジェクトフォルダーに新しい HTML ファイルを作成し、「 *Stockticker .html*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-237">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="d8a6b-238">テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-238">Replace the template code with the following code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    <span data-ttu-id="d8a6b-239">HTML では、5つの列、ヘッダー行、および5つのすべての列にまたがる1つのセルを持つデータ行を含むテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-239">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="d8a6b-240">データ行に "読み込み中..." と表示されます。とは、アプリケーションの起動時にすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-240">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="d8a6b-241">JavaScript コードは、その行を削除し、サーバーから取得した在庫データを使用してその行の位置を追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="d8a6b-242">スクリプトタグは、jQuery スクリプトファイル、SignalR コアスクリプトファイル、SignalR プロキシスクリプトファイル、および後で作成する StockTicker スクリプトファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-242">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="d8a6b-243">"/Signalr/hubs" URL を指定する SignalR proxy スクリプトファイルが動的に生成され、ハブクラス (この場合は GetAllStocks) のメソッドのプロキシメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-243">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="d8a6b-244">必要に応じて、 [SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用してこの JavaScript ファイルを手動で生成し、maphubs メソッド呼び出しでの動的ファイル作成を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-244">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
   > <span data-ttu-id="d8a6b-245">*Stockticker .html*の JavaScript ファイル参照が正しいことを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-245">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="d8a6b-246">つまり、スクリプトタグの jQuery バージョン (例では 1.8.2) がプロジェクトの*scripts*フォルダー内の jquery バージョンと同じであることを確認し、スクリプトタグの SignalR バージョンがプロジェクトの*Scripts*フォルダーの SignalR バージョンと同じであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-246">That is, make sure that the jQuery version in your script tag (1.8.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="d8a6b-247">必要に応じて、スクリプトタグ内のファイル名を変更します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-247">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="d8a6b-248">**ソリューションエクスプローラー**で、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-248">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="d8a6b-249">プロジェクトフォルダーに新しい JavaScript ファイルを作成し、*という名前*を指定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-249">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="d8a6b-250">テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-250">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    <span data-ttu-id="d8a6b-251">$. connection は、SignalR プロキシを参照します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-251">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="d8a6b-252">このコードは、Stockhub クラスのプロキシへの参照を取得し、それをティッカー変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-252">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="d8a6b-253">プロキシ名は、[HubName] 属性によって設定された名前です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-253">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    <span data-ttu-id="d8a6b-254">すべての変数と関数が定義された後、ファイル内の最後のコード行は、SignalR start 関数を呼び出すことによって SignalR 接続を初期化します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-254">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="d8a6b-255">Start 関数は非同期に実行され、 [JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。つまり、done 関数を呼び出して、非同期操作の完了時に呼び出す関数を指定できます。「」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-255">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    <span data-ttu-id="d8a6b-256">Init 関数は、サーバー上で getAllStocks 関数を呼び出し、サーバーから返された情報を使用して、stock テーブルを更新します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-256">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="d8a6b-257">既定では、クライアントで camel 形式の文字種を使用する必要があることに注意してください。ただし、サーバーでは、メソッド名は pascal 形式です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-257">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="d8a6b-258">Camel 形式の規則は、オブジェクトではなく、メソッドにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-258">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="d8a6b-259">たとえば、stock を参照します。シンボルと株価。株価、証券、株価はありません。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-259">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    <span data-ttu-id="d8a6b-260">クライアントで pascal 形式の表記を使用する場合、またはまったく異なる方法名を使用する場合は、HubName 属性を使用してハブクラス自体を修飾するのと同じ方法で、ハブメソッドを HubMethodName 属性で修飾できます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-260">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="d8a6b-261">Init メソッドでは、formatStock を呼び出して stock オブジェクトのプロパティを書式設定することによって、サーバーから受信した各 stock オブジェクトに対してテーブル行の HTML が作成されます。次に、代わりを呼び出して ( *Stockticker*の先頭で定義されている)、stock オブジェクトのプロパティ値で行テンプレート変数のプレースホルダーを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-261">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="d8a6b-262">その後、結果として得られる HTML は、stock テーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-262">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="d8a6b-263">Init を呼び出すには、非同期の開始関数が完了した後に実行されるコールバック関数としてを渡します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-263">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="d8a6b-264">Start を呼び出した後に別の JavaScript ステートメントとして init を呼び出した場合、関数は失敗します。これは、start 関数が接続の確立を完了するまで待機することなく、すぐに実行されるためです。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-264">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="d8a6b-265">その場合、init 関数は、サーバー接続が確立される前に、getAllStocks 関数を呼び出そうとします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-265">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="d8a6b-266">サーバーが株価の価格を変更すると、接続されているクライアントで updateStockPrice が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-266">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="d8a6b-267">関数は、サーバーからの呼び出しで使用できるようにするために、stockTicker プロキシのクライアントプロパティに追加されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-267">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    <span data-ttu-id="d8a6b-268">UpdateStockPrice 関数は、サーバーから受け取った stock オブジェクトを、init 関数と同じようにテーブルの行に書式設定します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-268">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="d8a6b-269">ただし、テーブルに行を追加するのではなく、テーブル内の株価の現在の行を検索し、その行を新しい行に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-269">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="d8a6b-270">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="d8a6b-270">Test the application</span></span>

1. <span data-ttu-id="d8a6b-271">F5 キーを押してデバッグ モードでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-271">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="d8a6b-272">Stock テーブルでは、最初に "読み込み中..." と表示されます。行を入力すると、最初の株式データが表示されます。その後、株価が変化します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-272">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![読み込み](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![最初のストックテーブル](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![サーバーから変更を受信する株価テーブル](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. <span data-ttu-id="d8a6b-276">ブラウザーのアドレスバーから URL をコピーして、1つまたは複数の新しいブラウザーウィンドウに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-276">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="d8a6b-277">最初の株価表示は最初のブラウザーと同じであり、同時に変更が行われます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-277">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="d8a6b-278">すべてのブラウザーを閉じて新しいブラウザーを開き、同じ URL にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-278">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="d8a6b-279">StockTicker シングルトンオブジェクトは引き続きサーバーで実行されているので、stock テーブルの表示では、株式の変更が継続されていることが示されています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-279">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="d8a6b-280">(最初のテーブルにゼロ変更の数値が表示されません)。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-280">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="d8a6b-281">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-281">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="d8a6b-282">ログの有効化</span><span class="sxs-lookup"><span data-stu-id="d8a6b-282">Enable logging</span></span>

<span data-ttu-id="d8a6b-283">SignalR には、クライアントで有効にできる組み込みのログ関数があり、トラブルシューティングに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-283">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="d8a6b-284">このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポートメソッドのうち、どれがログによってどのように表示されるかを示す例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-284">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="d8a6b-285">[Websocket](http://en.wikipedia.org/wiki/WebSocket)。 IIS 8 と現在のブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-285">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="d8a6b-286">[サーバーが送信](http://en.wikipedia.org/wiki/Server-sent_events)したイベント (Internet Explorer 以外のブラウザーでサポートされています)。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-286">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="d8a6b-287">[永続的フレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。 Internet Explorer でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-287">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="d8a6b-288">[Ajax の長いポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)(すべてのブラウザーでサポートされます)。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-288">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="d8a6b-289">SignalR は、特定の接続について、サーバーとクライアントの両方でサポートされる最適なトランスポート方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-289">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="d8a6b-290">*Stockticker js*を開き、ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にするコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-290">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. <span data-ttu-id="d8a6b-291">F5 キーを押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-291">Press F5 to run the project.</span></span>
3. <span data-ttu-id="d8a6b-292">ブラウザーの [開発者ツール] ウィンドウを開き、コンソールを選択してログを表示します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-292">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="d8a6b-293">新しい接続のトランスポートメソッドをネゴシエートする Signalr のログを表示するには、ページの更新が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-293">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="d8a6b-294">Internet Explorer 10 を Windows 8 (IIS 8) で実行している場合、転送方法は Websocket になります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-294">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 コンソール](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    <span data-ttu-id="d8a6b-296">Internet Explorer 10 を Windows 7 (IIS 7.5) で実行している場合、トランスポート方法は iframe です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-296">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 コンソール、IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    <span data-ttu-id="d8a6b-298">Firefox では、コンソールウィンドウを取得するために、消火バグアドインをインストールします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-298">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="d8a6b-299">Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は Websocket です。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-299">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    <span data-ttu-id="d8a6b-301">Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方法はサーバーから送信されたイベントです。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-301">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 コンソール](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="d8a6b-303">完全な StockTicker サンプルをインストールして確認する</span><span class="sxs-lookup"><span data-stu-id="d8a6b-303">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="d8a6b-304">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet パッケージによってインストールされる stockticker アプリケーションには、最初から作成した簡易バージョンよりも多くの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-304">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="d8a6b-305">チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新しい機能とそれらを実装するコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-305">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="d8a6b-306">SignalR NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="d8a6b-306">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="d8a6b-307">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-307">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="d8a6b-308">**[NuGet パッケージの管理]** ダイアログボックスで、 **[オンライン]** をクリックし、 **[オンライン検索]** ボックスに「 *SignalR* 」と入力して、 **SignalR**パッケージの **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-308">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![SignalR パッケージをインストールします。](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. <span data-ttu-id="d8a6b-310">*Global.asax*ファイルで、Routetable. ルート. maphubs (); をコメントアウトします。アプリケーション\_の開始メソッドで前に追加した行。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-310">In the *Global.asax* file, comment out the RouteTable.Routes.MapHubs(); line that you added earlier in the Application\_Start method.</span></span>

    <span data-ttu-id="d8a6b-311">SignalR パッケージは、 *\_アプリ*に SignalR ルートを登録するため、 *global.asax*のコードは不要になりました。これは、ファイルを起動します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-311">The code in *Global.asax* is no longer needed because the SignalR.Sample package registers the SignalR route in the *App\_Start/RegisterHubs.cs* file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    <span data-ttu-id="d8a6b-312">アセンブリ属性によって参照される WebActivator クラスは、SignalR パッケージの依存関係としてインストールされる WebActivatorEx NuGet パッケージに含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-312">The WebActivator class that is referenced by the assembly attribute is included in the WebActivatorEx NuGet package, which is installed as a dependency of the SignalR.Sample package.</span></span>
4. <span data-ttu-id="d8a6b-313">**ソリューションエクスプローラー**で、SignalR パッケージをインストールすることによって作成された*SignalR*フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-313">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
5. <span data-ttu-id="d8a6b-314">*SignalR*フォルダーで、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-314">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8a6b-315">SignalR NuGet パッケージをインストールすると、 *Scripts*フォルダーにある jQuery のバージョンが変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-315">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="d8a6b-316">パッケージによって*SignalR*フォルダーにインストールされる新しい*stockticker .html*ファイルは、パッケージがインストールする jquery バージョンと同期されますが、元の*stockticker*ファイルを再度実行する場合は、最初にスクリプトタグの jquery 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-316">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d8a6b-317">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="d8a6b-317">Run the application</span></span>

1. <span data-ttu-id="d8a6b-318">F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-318">Press F5 to run the application.</span></span>

    <span data-ttu-id="d8a6b-319">先ほど見たグリッドに加えて、完全な株式ティッカーアプリケーションでは、同じ在庫データを表示する水平スクロールウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-319">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="d8a6b-320">アプリケーションを初めて実行すると、"market" が "closed" になり、静的グリッドと、スクロールしていないティッカーウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-320">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 画面の開始](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    <span data-ttu-id="d8a6b-322">**[Open Market]** をクリックすると、 **[Live stock ティッカー]** ボックスが水平方向にスクロールし、サーバーが定期的に株価の変更を定期的にブロードキャストするようになります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-322">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="d8a6b-323">株価が変化するたびに、 **Live Stock テーブル**グリッドと**live stock ティッカー**ボックスの両方が更新されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-323">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="d8a6b-324">株価の変化が正の場合は、株価が緑で表示され、変更が負の場合は、株価が赤の背景で表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-324">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker アプリ, マーケットオープン](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    <span data-ttu-id="d8a6b-326">**[マーケットを閉じる]** ボタンをクリックすると、変更が停止し、ティッカースクロールが停止します。 **[リセット]** ボタンをクリックすると、価格の変更が開始される前に、すべての株式データが初期状態にリセットされます</span><span class="sxs-lookup"><span data-stu-id="d8a6b-326">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="d8a6b-327">ブラウザーウィンドウをさらに開いて同じ URL にアクセスすると、各ブラウザーで同じデータが同時に動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-327">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="d8a6b-328">いずれかのボタンをクリックすると、すべてのブラウザーが同時に同じように応答します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-328">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="d8a6b-329">Live Stock ティッカーの表示</span><span class="sxs-lookup"><span data-stu-id="d8a6b-329">Live Stock Ticker display</span></span>

<span data-ttu-id="d8a6b-330">**Live Stock ティッカー**の表示は、div 要素内の順序付けられていないリストで、CSS スタイルによって1行に書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-330">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="d8a6b-331">このティッカーは、テーブルと同じ方法で初期化および更新されます。 &lt;li&gt; テンプレート文字列のプレースホルダーを置換し、&lt;li&gt; 要素を &lt;ul&gt; 要素に動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-331">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="d8a6b-332">スクロールは、div 内の順序付けられていないリストの左余白を変更する jQuery アニメーション関数を使用して実行されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-332">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="d8a6b-333">Stock ティッカー HTML:</span><span class="sxs-lookup"><span data-stu-id="d8a6b-333">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

<span data-ttu-id="d8a6b-334">Stock ティッカー CSS:</span><span class="sxs-lookup"><span data-stu-id="d8a6b-334">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

<span data-ttu-id="d8a6b-335">スクロールを行う jQuery コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-335">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="d8a6b-336">クライアントが呼び出すことができるサーバー上の追加のメソッド</span><span class="sxs-lookup"><span data-stu-id="d8a6b-336">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="d8a6b-337">Stockhub クラスは、クライアントが呼び出すことのできる4つの追加のメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-337">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

<span data-ttu-id="d8a6b-338">OpenMarket、CloseMarket、Reset は、ページの上部にあるボタンへの応答として呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-338">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="d8a6b-339">この例では、1つのクライアントが、すべてのクライアントに直ちに伝達される状態の変更をトリガーするパターンを示します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-339">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="d8a6b-340">これらの各メソッドは、市場の状態の変化に影響を与える StockTicker クラスのメソッドを呼び出し、新しい状態をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-340">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="d8a6b-341">StockTicker クラスでは、MarketState 列挙値を返す MarketState プロパティによって、市場の状態が維持されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-341">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

<span data-ttu-id="d8a6b-342">StockTicker クラスは threadsafe する必要があるため、次のようにして、市場の状態を変更する各メソッドがロックブロック内で実行されます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-342">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

<span data-ttu-id="d8a6b-343">このコードが threadsafe であることを確認するために、MarketState プロパティをバックする \_marketState フィールドは volatile としてマークされています。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-343">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

<span data-ttu-id="d8a6b-344">BroadcastMarketStateChange メソッドと BroadcastMarketReset メソッドは、既に説明した BroadcastStockPrice メソッドに似ていますが、クライアントで定義されているさまざまなメソッドを呼び出す点が異なります。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-344">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="d8a6b-345">サーバーが呼び出すことができるクライアント上の追加の関数</span><span class="sxs-lookup"><span data-stu-id="d8a6b-345">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="d8a6b-346">UpdateStockPrice 関数は、グリッドとティッカーの両方の表示を処理するようになりました。また、jQuery 色を使用して赤と緑の色をフラッシュします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-346">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="d8a6b-347">*SignalR*の新しい関数では、市場の状態に基づいてボタンを有効または無効にし、ティッカーウィンドウの水平スクロールを停止または開始します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-347">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="d8a6b-348">複数の関数がティッカー. client に追加されるため、 [jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-348">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="d8a6b-349">接続を確立した後の追加のクライアントセットアップ</span><span class="sxs-lookup"><span data-stu-id="d8a6b-349">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="d8a6b-350">クライアントが接続を確立した後、適切な marketOpened または marketClosed 関数を呼び出すために市場が開いているか閉じられたかを確認し、サーバーメソッドの呼び出しをボタンにアタッチします。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-350">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

<span data-ttu-id="d8a6b-351">サーバーメソッドは、接続が確立されるまで、ボタンには接続されません。そのため、コードは、使用可能になる前にサーバーメソッドを呼び出すことができません。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-351">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="d8a6b-352">次のステップ</span><span class="sxs-lookup"><span data-stu-id="d8a6b-352">Next steps</span></span>

<span data-ttu-id="d8a6b-353">このチュートリアルでは、定期的に、または任意のクライアントからの通知に応答して、サーバーからすべての接続されたクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラミングする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-353">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="d8a6b-354">マルチスレッドシングルトンインスタンスを使用してサーバーの状態を維持するパターンは、マルチプレーヤーのオンラインゲームのシナリオでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-354">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="d8a6b-355">例について[は、SignalR に基づく ShootR ゲーム](https://github.com/NTaylorMullen/ShootR)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-355">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="d8a6b-356">ピアツーピア通信のシナリオを示すチュートリアルについては、「[はじめに](index.md)と[SignalR を使用したリアルタイム更新](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-356">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](index.md) and [Real-Time Updating with SignalR](index.md).</span></span>

<span data-ttu-id="d8a6b-357">より高度な SignalR 開発の概念については、次のサイトで SignalR ソースコードとリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8a6b-357">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="d8a6b-358">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="d8a6b-358">ASP.NET SignalR</span></span>](https://asp.net/signalr/)
- [<span data-ttu-id="d8a6b-359">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="d8a6b-359">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="d8a6b-360">SignalR Github とサンプル</span><span class="sxs-lookup"><span data-stu-id="d8a6b-360">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="d8a6b-361">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="d8a6b-361">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
