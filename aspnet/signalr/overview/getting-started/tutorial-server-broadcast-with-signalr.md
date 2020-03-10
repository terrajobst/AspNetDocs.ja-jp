---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'チュートリアル: SignalR 2 を使用したサーバーブロードキャスト |Microsoft Docs'
author: tdykstra
description: このチュートリアルでは、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431242"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="ad46f-103">チュートリアル: SignalR 2 を使用したサーバーブロードキャスト</span><span class="sxs-lookup"><span data-stu-id="ad46f-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="ad46f-104">このチュートリアルでは、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="ad46f-105">サーバーブロードキャストとは、サーバーがクライアントに送信される通信を開始することを意味します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="ad46f-106">このチュートリアルで作成するアプリケーションは、サーバーブロードキャスト機能の一般的なシナリオである株式ティッカーをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="ad46f-107">サーバーは定期的に株価を更新し、接続されているすべてのクライアントに更新をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="ad46f-108">ブラウザーでは、サーバーからの通知に応じて、 **[変更]** 列と [ **%** ] 列の数値と記号が動的に変更されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="ad46f-109">同じ URL に対して追加のブラウザーを開くと、すべてのブラウザーで同じデータと同じデータの変更が同時に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Web の作成](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="ad46f-111">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="ad46f-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad46f-112">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-112">Create the project</span></span>
> * <span data-ttu-id="ad46f-113">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="ad46f-113">Set up the server code</span></span>
> * <span data-ttu-id="ad46f-114">サーバーコードを確認する</span><span class="sxs-lookup"><span data-stu-id="ad46f-114">Examine the server code</span></span>
> * <span data-ttu-id="ad46f-115">クライアントコードの設定</span><span class="sxs-lookup"><span data-stu-id="ad46f-115">Set up the client code</span></span>
> * <span data-ttu-id="ad46f-116">クライアントコードを確認する</span><span class="sxs-lookup"><span data-stu-id="ad46f-116">Examine the client code</span></span>
> * <span data-ttu-id="ad46f-117">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="ad46f-117">Test the application</span></span>
> * <span data-ttu-id="ad46f-118">ログの有効化</span><span class="sxs-lookup"><span data-stu-id="ad46f-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad46f-119">アプリケーションをビルドする手順を実行しない場合は、新しい空の ASP.NET Web アプリケーションプロジェクトに SignalR パッケージをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="ad46f-120">このチュートリアルの手順を実行せずに NuGet パッケージをインストールする場合は、 *readme.txt*ファイルに記載されている手順に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="ad46f-121">パッケージを実行するには、インストールされているパッケージの `ConfigureSignalR` メソッドを呼び出す OWIN startup クラスを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="ad46f-122">OWIN startup クラスを追加しないと、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="ad46f-123">この記事の「 [StockTicker サンプルをインストール](#install-the-stockticker-sample)する」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad46f-124">前提条件</span><span class="sxs-lookup"><span data-stu-id="ad46f-124">Prerequisites</span></span>

* <span data-ttu-id="ad46f-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。</span><span class="sxs-lookup"><span data-stu-id="ad46f-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="ad46f-126">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-126">Create the project</span></span>

<span data-ttu-id="ad46f-127">このセクションでは、Visual Studio 2017 を使用して空の ASP.NET Web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="ad46f-128">Visual Studio で、ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web の作成](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="ad46f-130">**新しい ASP.NET Web アプリケーション-SignalR**ウィンドウで、**空**のままにして [ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="ad46f-131">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="ad46f-131">Set up the server code</span></span>

<span data-ttu-id="ad46f-132">このセクションでは、サーバーで実行するコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="ad46f-133">Stock クラスを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-133">Create the Stock class</span></span>

<span data-ttu-id="ad46f-134">まず、在庫に関する情報を格納して送信するために使用する*ストック*モデルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="ad46f-135">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="ad46f-136">クラスに「 *Stock* 」という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="ad46f-137">*Stock.cs*ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="ad46f-138">株式の作成時に設定する2つのプロパティ (たとえば、Microsoft for Microsoft) と `Price`を `Symbol` します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="ad46f-139">その他のプロパティは、`Price`を設定する方法とタイミングによって異なります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="ad46f-140">初めて `Price`を設定すると、値が `DayOpen`に反映されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="ad46f-141">その後、`Price`を設定すると、アプリは `Price` と `DayOpen`の違いに基づいて `Change` と `PercentChange` のプロパティ値を計算します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="ad46f-142">Stockhub および Stockティッカークラスを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="ad46f-143">SignalR Hub API を使用して、サーバー間の対話を処理します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="ad46f-144">SignalR `Hub` クラスから派生した `StockTickerHub` クラスは、クライアントからの接続とメソッド呼び出しの受信を処理します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="ad46f-145">また、株価データを保持し、`Timer` オブジェクトを実行する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="ad46f-146">`Timer` オブジェクトは、クライアント接続に関係なく、定期的に価格の更新をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="ad46f-147">ハブは一時的なものであるため、これらの関数を `Hub` クラスに配置することはできません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="ad46f-148">アプリは、接続やクライアントからサーバーへの呼び出しなど、ハブ上の各タスクの `Hub` クラスインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="ad46f-149">そのため、株価データを保持するメカニズム、価格更新プログラムを別のクラスで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="ad46f-150">クラスに `StockTicker`という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-150">You'll name the class `StockTicker`.</span></span>

![StockTicker からのブロードキャスト](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="ad46f-152">サーバー上で実行する `StockTicker` クラスのインスタンスは1つだけなので、各 `StockTickerHub` インスタンスからシングルトン `StockTicker` インスタンスへの参照を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="ad46f-153">`StockTicker` クラスは、在庫データを持ち、更新をトリガーするため、クライアントにブロードキャストする必要がありますが、`StockTicker` は `Hub` クラスではありません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="ad46f-154">`StockTicker` クラスは、SignalR Hub 接続コンテキストオブジェクトへの参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="ad46f-155">その後、SignalR 接続コンテキストオブジェクトを使用して、クライアントにブロードキャストできます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="ad46f-156">StockTickerHub.cs の作成</span><span class="sxs-lookup"><span data-stu-id="ad46f-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="ad46f-157">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="ad46f-158">**[新しい項目の追加-SignalR]** で、[**インストールされている** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="ad46f-159">クラスに「 *Stockhub* 」という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="ad46f-160">この手順では、 *StockTickerHub.cs*クラスファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="ad46f-161">同時に、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="ad46f-162">*StockTickerHub.cs*ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="ad46f-163">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-163">Save the file.</span></span>

<span data-ttu-id="ad46f-164">このアプリでは、[ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスを使用して、クライアントがサーバーで呼び出すことができるメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="ad46f-165">1つのメソッドを定義しています: `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="ad46f-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="ad46f-166">クライアントは、最初にサーバーに接続するときに、このメソッドを呼び出して、すべての株式の一覧を現在の価格で取得します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="ad46f-167">メソッドは、メモリからデータを返すため、同期的に実行して `IEnumerable<Stock>` を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="ad46f-168">データベースの検索や web サービスの呼び出しのように、待機時間がかかる処理を実行してデータを取得する必要がある場合は、`Task<IEnumerable<Stock>>` を戻り値として指定し、非同期処理を有効にします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="ad46f-169">詳細については、「 [ASP.NET SignalR HUB API Guide-Server-非同期に実行するタイミング](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="ad46f-170">`HubName` 属性は、アプリがクライアントの JavaScript コードでハブを参照する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="ad46f-171">この属性を使用しない場合のクライアントの既定の名前は、キャメルケースバージョンのクラス名です。この場合、この例では `stockTickerHub`します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="ad46f-172">後で説明するように、`StockTicker` クラスを作成すると、そのクラスのシングルトンインスタンスが、その静的 `Instance` プロパティに作成されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="ad46f-173">`StockTicker` のシングルトンインスタンスは、接続または切断するクライアントの数に関係なく、メモリ内にあります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="ad46f-174">このインスタンスは、`GetAllStocks()` メソッドが現在の株価情報を返すために使用するものです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="ad46f-175">StockTicker.cs の作成</span><span class="sxs-lookup"><span data-stu-id="ad46f-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="ad46f-176">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="ad46f-177">クラスに「 *Stockticker* 」という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="ad46f-178">*StockTicker.cs*ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="ad46f-179">すべてのスレッドが同じ StockTicker コードのインスタンスを実行するため、StockTicker クラスはスレッドセーフである必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="ad46f-180">サーバーコードを確認する</span><span class="sxs-lookup"><span data-stu-id="ad46f-180">Examine the server code</span></span>

<span data-ttu-id="ad46f-181">サーバーコードを調べると、アプリがどのように動作するかを理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="ad46f-182">静的フィールドへのシングルトンインスタンスの格納</span><span class="sxs-lookup"><span data-stu-id="ad46f-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="ad46f-183">このコードは、`Instance` プロパティをクラスのインスタンスにバックアップする静的 `_instance` フィールドを初期化します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="ad46f-184">コンストラクターはプライベートであるため、アプリケーションが作成できるクラスの唯一のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="ad46f-185">アプリでは、`_instance` フィールドの[遅延初期化](/dotnet/framework/performance/lazy-initialization)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="ad46f-186">パフォーマンス上の理由ではありません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-186">It's not for performance reasons.</span></span> <span data-ttu-id="ad46f-187">インスタンスの作成がスレッドセーフであることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="ad46f-188">クライアントがサーバーに接続するたびに、別のスレッドで実行されている Stockkerhub クラスの新しいインスタンスが、`StockTickerHub` クラスで既に説明したように、`StockTicker.Instance` 静的プロパティから Stockティッカーシングルトンインスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="ad46f-189">ConcurrentDictionary に株式データを格納する</span><span class="sxs-lookup"><span data-stu-id="ad46f-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="ad46f-190">コンストラクターは、いくつかのサンプル株価データを使用して `_stocks` コレクションを初期化し、株式を `GetAllStocks` 返します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="ad46f-191">既に説明したように、この株式のコレクションは `StockTickerHub.GetAllStocks`によって返されます。これは、クライアントが呼び出すことができる `Hub` クラスのサーバーメソッドです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="ad46f-192">株式コレクションは、スレッドセーフの[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="ad46f-193">別の方法として、 [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、変更を行うときに明示的にディクショナリをロックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="ad46f-194">このサンプルアプリケーションでは、アプリケーションデータをメモリに格納し、アプリが `StockTicker` インスタンスを破棄するときにデータを失うことは問題ありません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="ad46f-195">実際のアプリケーションでは、データベースのようなバックエンドデータストアを操作します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="ad46f-196">株価を定期的に更新する</span><span class="sxs-lookup"><span data-stu-id="ad46f-196">Periodically updating stock prices</span></span>

<span data-ttu-id="ad46f-197">コンストラクターは、在庫価格をランダムに更新するメソッドを定期的に呼び出す `Timer` オブジェクトを開始します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="ad46f-198">`Timer` は、state パラメーターに null を渡す `UpdateStockPrices`を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="ad46f-199">価格を更新する前に、アプリは `_updateStockPricesLock` オブジェクトのロックを取得します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="ad46f-200">このコードでは、別のスレッドが既に価格を更新しているかどうかを確認し、一覧の各株式に対して `TryUpdateStockPrice` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="ad46f-201">`TryUpdateStockPrice` 方法では、株価を変更するかどうか、および変更する量を決定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="ad46f-202">株価が変化した場合、アプリは `BroadcastStockPrice` を呼び出して、接続されているすべてのクライアントに株価の変更をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="ad46f-203">スレッドセーフであることを[確認するため](https://msdn.microsoft.com/library/x13ttww7.aspx)に指定された `_updatingStockPrices` フラグ。</span><span class="sxs-lookup"><span data-stu-id="ad46f-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="ad46f-204">実際のアプリケーションでは、`TryUpdateStockPrice` メソッドによって web サービスが呼び出され、価格が検索されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="ad46f-205">このコードでは、アプリはランダムな数値ジェネレーターを使用して、変更をランダムに行います。</span><span class="sxs-lookup"><span data-stu-id="ad46f-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="ad46f-206">SignalR コンテキストを取得して、StockTicker クラスがクライアントにブロードキャストできるようにする</span><span class="sxs-lookup"><span data-stu-id="ad46f-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="ad46f-207">価格の変更は、`StockTicker` オブジェクトで行われるため、接続されているすべてのクライアントで `updateStockPrice` メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="ad46f-208">`Hub` クラスでは、クライアントメソッドを呼び出すための API がありますが、`StockTicker` は `Hub` クラスから派生しておらず、`Hub` オブジェクトへの参照を持っていません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="ad46f-209">接続されたクライアントにブロードキャストするには、`StockTicker` クラスが `StockTickerHub` クラスの SignalR context インスタンスを取得し、それを使用してクライアントのメソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="ad46f-210">このコードは、シングルトンクラスのインスタンスを作成するときに SignalR コンテキストへの参照を取得し、その参照をコンストラクターに渡し、コンストラクターがそれを `Clients` プロパティに格納します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="ad46f-211">コンテキストを1回だけ取得する理由は2つあります。コンテキストの取得はコストのかかるタスクであり、一度取得すると、クライアントに送信されるメッセージの順序がアプリによって保持されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="ad46f-212">コンテキストの `Clients` プロパティを取得し、それを `StockTickerClient` プロパティに配置すると、`Hub` クラスと同じように見えるクライアントメソッドを呼び出すためのコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="ad46f-213">たとえば、すべてのクライアントにブロードキャストするには、`Clients.All.updateStockPrice(stock)`を記述します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="ad46f-214">`BroadcastStockPrice` で呼び出されている `updateStockPrice` メソッドはまだ存在しません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="ad46f-215">クライアントで実行されるコードを記述するときに、後で追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="ad46f-216">`Clients.All` は動的なので、ここで `updateStockPrice` を参照できます。これは、アプリが実行時に式を評価することを意味します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="ad46f-217">このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。また、クライアントに `updateStockPrice`という名前のメソッドがある場合、アプリはそのメソッドを呼び出し、パラメーター値をそのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="ad46f-218">`Clients.All` は、すべてのクライアントに送信することを意味します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="ad46f-219">SignalR には、に送信するクライアントまたはクライアントのグループを指定するための他のオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="ad46f-220">詳細については、「 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="ad46f-221">SignalR ルートを登録する</span><span class="sxs-lookup"><span data-stu-id="ad46f-221">Register the SignalR route</span></span>

<span data-ttu-id="ad46f-222">サーバーは、インターセプトする URL と SignalR に送信する URL を認識している必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="ad46f-223">これを行うには、OWIN startup クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="ad46f-224">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="ad46f-225">**[新しい項目の追加-SignalR]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="ad46f-226">クラスに「 *Startup* 」という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="ad46f-227">*Startup.cs*ファイルの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="ad46f-228">これで、サーバーコードの設定が完了しました。</span><span class="sxs-lookup"><span data-stu-id="ad46f-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="ad46f-229">次のセクションでは、クライアントを設定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="ad46f-230">クライアントコードの設定</span><span class="sxs-lookup"><span data-stu-id="ad46f-230">Set up the client code</span></span>

<span data-ttu-id="ad46f-231">このセクションでは、クライアントで実行するコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="ad46f-232">HTML ページと JavaScript ファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="ad46f-233">HTML ページにデータが表示され、JavaScript ファイルによってデータが整理されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="ad46f-234">StockTicker .html を作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-234">Create StockTicker.html</span></span>

<span data-ttu-id="ad46f-235">まず、HTML クライアントを追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="ad46f-236">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="ad46f-237">ファイルに「 *Stockticker* 」という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="ad46f-238">*Stockticker .html*ファイルの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="ad46f-239">HTML では、5つの列、ヘッダー行、および5つのすべての列にまたがる1つのセルを持つデータ行を含むテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="ad46f-240">データ行に "読み込み中..." と表示されます。アプリが開始されるとすぐに。</span><span class="sxs-lookup"><span data-stu-id="ad46f-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="ad46f-241">JavaScript コードは、その行を削除し、サーバーから取得した在庫データを使用してその行の位置を追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="ad46f-242">スクリプトタグでは、次のものを指定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-242">The script tags specify:</span></span>

    * <span data-ttu-id="ad46f-243">JQuery スクリプトファイル。</span><span class="sxs-lookup"><span data-stu-id="ad46f-243">The jQuery script file.</span></span>

    * <span data-ttu-id="ad46f-244">SignalR コアスクリプトファイル。</span><span class="sxs-lookup"><span data-stu-id="ad46f-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="ad46f-245">SignalR プロキシスクリプトファイル。</span><span class="sxs-lookup"><span data-stu-id="ad46f-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="ad46f-246">後で作成する StockTicker スクリプトファイル。</span><span class="sxs-lookup"><span data-stu-id="ad46f-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="ad46f-247">アプリによって、SignalR プロキシスクリプトファイルが動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="ad46f-248">"/Signalr/hubs" URL を指定し、ハブクラス (この場合は `StockTickerHub.GetAllStocks`) のメソッドのプロキシメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="ad46f-249">必要に応じて、 [SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用して、この JavaScript ファイルを手動で生成できます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="ad46f-250">`MapHubs` メソッドの呼び出しでは、動的なファイルの作成を無効にすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="ad46f-251">**ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="ad46f-252">JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ad46f-253">パッケージマネージャーにより、SignalR スクリプトの新しいバージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="ad46f-254">コードブロック内のスクリプト参照を、プロジェクト内のスクリプトファイルのバージョンに対応するように更新します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="ad46f-255">**ソリューションエクスプローラー**で、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="ad46f-256">StockTicker を作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-256">Create StockTicker.js</span></span>

<span data-ttu-id="ad46f-257">次に、JavaScript ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="ad46f-258">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **JavaScript ファイル**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="ad46f-259">ファイルに「 *Stockticker* 」という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="ad46f-260">次のコードを*Stockticker*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="ad46f-261">クライアントコードを確認する</span><span class="sxs-lookup"><span data-stu-id="ad46f-261">Examine the client code</span></span>

<span data-ttu-id="ad46f-262">クライアントコードを確認すると、クライアントコードがサーバーコードと対話してアプリを動作させる方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="ad46f-263">接続を開始しています</span><span class="sxs-lookup"><span data-stu-id="ad46f-263">Starting the connection</span></span>

<span data-ttu-id="ad46f-264">`$.connection` は、SignalR プロキシを参照します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="ad46f-265">このコードは、`StockTickerHub` クラスのプロキシへの参照を取得し、それを `ticker` 変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="ad46f-266">プロキシ名は、`HubName` 属性によって設定された名前です。</span><span class="sxs-lookup"><span data-stu-id="ad46f-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="ad46f-267">すべての変数と関数を定義した後、ファイルの最後のコード行では、SignalR `start` 関数を呼び出して SignalR 接続を初期化します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="ad46f-268">`start` 関数は非同期に実行され、 [JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="ad46f-269">Done 関数を呼び出して、アプリが非同期アクションを終了したときに呼び出す関数を指定できます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="ad46f-270">すべての株式を取得する</span><span class="sxs-lookup"><span data-stu-id="ad46f-270">Getting all the stocks</span></span>

<span data-ttu-id="ad46f-271">`init` 関数は、サーバーで `getAllStocks` 関数を呼び出し、サーバーから返された情報を使用して、stock テーブルを更新します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="ad46f-272">既定では、サーバーでメソッド名が pascal 形式であっても、クライアントでキャメルを使用する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="ad46f-273">キャメル規則は、オブジェクトではなく、メソッドにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="ad46f-274">たとえば、`stock.symbol` や `stock.price`ではなく、`stock.Symbol` と `stock.Price`を参照しているとします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="ad46f-275">`init` メソッドでは、アプリは、`formatStock` を呼び出して `stock` オブジェクトのプロパティを書式設定し、`supplant` を呼び出して `rowTemplate` 変数内のプレースホルダーを `stock` オブジェクトのプロパティ値に置き換えることによって、サーバーから受け取った各 stock オブジェクトのテーブル行に対して HTML を作成します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="ad46f-276">その後、結果として得られる HTML は、stock テーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="ad46f-277">非同期 `start` 関数が終了した後に実行される `callback` 関数として渡すことによって、`init` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="ad46f-278">`start`を呼び出した後に別の JavaScript ステートメントとして `init` を呼び出すと、関数は失敗します。これは、start 関数が接続の確立を完了するまで待機することなく、すぐに実行されるためです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="ad46f-279">この場合、`init` 関数は、アプリがサーバー接続を確立する前に `getAllStocks` 関数の呼び出しを試みます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="ad46f-280">更新された株価の取得</span><span class="sxs-lookup"><span data-stu-id="ad46f-280">Getting updated stock prices</span></span>

<span data-ttu-id="ad46f-281">サーバーが株価の価格を変更すると、接続されたクライアントで `updateStockPrice` が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="ad46f-282">アプリケーションは、関数を `stockTicker` プロキシのクライアントプロパティに追加して、サーバーからの呼び出しで使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="ad46f-283">`updateStockPrice` 関数は、サーバーから受け取った stock オブジェクトを、`init` 関数と同じようにテーブル行に書式設定します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="ad46f-284">テーブルに行を追加する代わりに、テーブル内の株価の現在の行を検索し、その行を新しい行に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="ad46f-285">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="ad46f-285">Test the application</span></span>

<span data-ttu-id="ad46f-286">アプリをテストして、動作しているかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="ad46f-287">すべてのブラウザーウィンドウに、在庫価格が変動するライブ株価テーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="ad46f-288">ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、アプリをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![デバッグモードをオンにして [再生] を選択したユーザーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="ad46f-290">ブラウザーウィンドウが開き、**ライブ株価テーブル**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="ad46f-291">最初は、stock テーブルに "読み込み中..." と表示されます。行を入力すると、アプリによって最初の株価データが表示され、株価が変化します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="ad46f-292">ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="ad46f-293">最初の株価表示は最初のブラウザーと同じであり、同時に変更が行われます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="ad46f-294">すべてのブラウザーを閉じ、新しいブラウザーを開いて、同じ URL にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="ad46f-295">StockTicker シングルトンオブジェクトは引き続きサーバーで実行されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="ad46f-296">**ライブ株価テーブル**には、株式の変化が続いていることが示されています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="ad46f-297">最初のテーブルにゼロ変更の数値が表示されません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="ad46f-298">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="ad46f-299">ログの有効化</span><span class="sxs-lookup"><span data-stu-id="ad46f-299">Enable logging</span></span>

<span data-ttu-id="ad46f-300">SignalR には、クライアントで有効にできる組み込みのログ関数があり、トラブルシューティングに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="ad46f-301">このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポートメソッドのうち、どれがログに記録されるかを示す例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="ad46f-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket)。 IIS 8 と現在のブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="ad46f-303">[サーバーが送信](http://en.wikipedia.org/wiki/Server-sent_events)したイベント (Internet Explorer 以外のブラウザーでサポートされています)。</span><span class="sxs-lookup"><span data-stu-id="ad46f-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="ad46f-304">[永続的フレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。 Internet Explorer でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="ad46f-305">[Ajax の長いポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)(すべてのブラウザーでサポートされます)。</span><span class="sxs-lookup"><span data-stu-id="ad46f-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="ad46f-306">SignalR は、特定の接続について、サーバーとクライアントの両方でサポートされる最適なトランスポート方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="ad46f-307">*Stockticker*を開きます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="ad46f-308">次の強調表示されたコード行を追加して、ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="ad46f-309">**F5** キーを押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="ad46f-310">ブラウザーの [開発者ツール] ウィンドウを開き、コンソールを選択してログを表示します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="ad46f-311">新しい接続のトランスポートメソッドをネゴシエートする SignalR のログを表示するには、ページの更新が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="ad46f-312">Internet Explorer 10 を Windows 8 (IIS 8) で実行している場合、転送方法は**websocket**になります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="ad46f-313">Internet Explorer 10 を Windows 7 (IIS 7.5) で実行している場合、トランスポート方法は**iframe**です。</span><span class="sxs-lookup"><span data-stu-id="ad46f-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="ad46f-314">Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は**websocket**です。</span><span class="sxs-lookup"><span data-stu-id="ad46f-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="ad46f-315">Firefox では、コンソールウィンドウを取得するために、消火バグアドインをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="ad46f-316">Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方式は**サーバー側で送信**されたイベントです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="ad46f-317">StockTicker サンプルをインストールする</span><span class="sxs-lookup"><span data-stu-id="ad46f-317">Install the StockTicker sample</span></span>

<span data-ttu-id="ad46f-318">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)は、stockticker アプリケーションをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="ad46f-319">NuGet パッケージには、最初から作成した簡易バージョンよりも多くの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="ad46f-320">チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新しい機能とそれらを実装するコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad46f-321">このチュートリアルの前の手順を実行せずにパッケージをインストールする場合は、プロジェクトに OWIN startup クラスを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="ad46f-322">この手順については、NuGet パッケージ用のこの readme.txt ファイルで説明されています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="ad46f-323">SignalR NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="ad46f-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="ad46f-324">**ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="ad46f-325">**[NuGet パッケージマネージャー: SignalR]** で、 **[参照]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="ad46f-326">**[パッケージソース]** で、 **[nuget.org]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="ad46f-327">検索ボックスに「 *SignalR* 」と入力し、[ **SignalR** > **インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="ad46f-328">**ソリューションエクスプローラー**で、 *SignalR*フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="ad46f-329">SignalR パッケージをインストールすると、フォルダーとその内容が作成されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="ad46f-330">*SignalR*フォルダーで、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad46f-331">SignalR NuGet パッケージをインストールすると、 *Scripts*フォルダーにある jQuery のバージョンが変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="ad46f-332">パッケージによって*SignalR*フォルダーにインストールされる新しい*stockticker .html*ファイルは、パッケージがインストールする jquery バージョンと同期されますが、元の*stockticker*ファイルを再度実行する場合は、最初にスクリプトタグの jquery 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="ad46f-333">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="ad46f-333">Run the application</span></span>

 <span data-ttu-id="ad46f-334">最初のアプリに表示されたテーブルには便利な機能があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="ad46f-335">完全な株式ティッカーアプリケーションでは、新しい機能が表示されます。水平方向のスクロールウィンドウで、色が変化したときに色が変化する株価を表示します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="ad46f-336">**F5** キーを押して、アプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="ad46f-337">アプリを初めて実行すると、"マーケット" が "閉じています" と表示され、静的テーブルと、スクロールしていないティッカーウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="ad46f-338">**[Open Market]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-338">Select **Open Market**.</span></span>

    ![ライブティッカーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="ad46f-340">**[Live Stock ティッカー]** ボックスが水平にスクロールすると、サーバーは定期的に株価の変化を定期的にブロードキャストし始めます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="ad46f-341">株価が変化するたびに、アプリは**Live Stock テーブル**と**live stock ティッカー**の両方を更新します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="ad46f-342">株価の変化が正の場合、アプリでは背景が緑色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="ad46f-343">変更が負の場合、アプリは、赤の背景で株価を表示します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="ad46f-344">**[マーケットを閉じる]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="ad46f-345">テーブルの更新を停止します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-345">The table updates stop.</span></span>

    * <span data-ttu-id="ad46f-346">ティッカーはスクロールを停止します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="ad46f-347">**[リセット]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-347">Select **Reset**.</span></span>

    * <span data-ttu-id="ad46f-348">すべての株式データがリセットされます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-348">All stock data is reset.</span></span>

    * <span data-ttu-id="ad46f-349">アプリは、価格の変更が開始される前に初期状態を復元します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="ad46f-350">ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="ad46f-351">各ブラウザーで同じデータが同時に動的に更新されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="ad46f-352">いずれかのコントロールを選択すると、すべてのブラウザーが同時に同じように応答します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="ad46f-353">Live Stock ティッカーの表示</span><span class="sxs-lookup"><span data-stu-id="ad46f-353">Live Stock Ticker display</span></span>

<span data-ttu-id="ad46f-354">**Live Stock ティッカー**の表示は、CSS スタイルによって1行に書式設定された `<div>` 要素内の順序付けられていないリストです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="ad46f-355">このアプリでは、テーブルと同じ方法で、`<li>` テンプレート文字列内のプレースホルダーを置き換え、`<li>` 要素を `<ul>` 要素に動的に追加することによって、ティッカーを初期化して更新します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="ad46f-356">アプリには、jQuery `animate` 関数を使用したスクロール機能が含まれており、`<div>`内の順序付けられていないリストの左余白を変更します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="ad46f-357">SignalR のサンプル</span><span class="sxs-lookup"><span data-stu-id="ad46f-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="ad46f-358">Stock ティッカー HTML コードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="ad46f-359">SignalR のサンプル</span><span class="sxs-lookup"><span data-stu-id="ad46f-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="ad46f-360">Stock ティッカー CSS コードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ad46f-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="ad46f-361">SignalR SignalR (サンプルの場合)</span><span class="sxs-lookup"><span data-stu-id="ad46f-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="ad46f-362">スクロールを行う jQuery コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="ad46f-363">クライアントが呼び出すことができるサーバー上の追加のメソッド</span><span class="sxs-lookup"><span data-stu-id="ad46f-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="ad46f-364">アプリに柔軟性を追加するには、アプリが呼び出すことができる追加のメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="ad46f-365">SignalR StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="ad46f-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="ad46f-366">`StockTickerHub` クラスは、クライアントが呼び出すことができる4つの追加のメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="ad46f-367">アプリは、ページの上部にあるボタンに応答して、`OpenMarket`、`CloseMarket`、および `Reset` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="ad46f-368">これらは、すべてのクライアントに直ちに反映された状態の変更をトリガーする1つのクライアントのパターンを示しています。</span><span class="sxs-lookup"><span data-stu-id="ad46f-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="ad46f-369">これらの各メソッドは、`StockTicker` クラスのメソッドを呼び出して、市場状態の変化を引き起こし、新しい状態をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="ad46f-370">SignalR StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="ad46f-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="ad46f-371">`StockTicker` クラスでは、アプリは `MarketState` 列挙値を返す `MarketState` プロパティを使用して、市場の状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="ad46f-372">`StockTicker` クラスはスレッドセーフである必要があるため、市場の状態を変更する各メソッドは、ロックブロック内で実行します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="ad46f-373">このコードがスレッドセーフであることを確認するには、`volatile`指定された `MarketState` プロパティをバックアップする `_marketState` フィールドを使用します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="ad46f-374">`BroadcastMarketStateChange` メソッドと `BroadcastMarketReset` メソッドは、既に説明した BroadcastStockPrice メソッドに似ていますが、クライアントで定義されているさまざまなメソッドを呼び出す場合を除きます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="ad46f-375">サーバーが呼び出すことができるクライアント上の追加の関数</span><span class="sxs-lookup"><span data-stu-id="ad46f-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="ad46f-376">`updateStockPrice` 関数はテーブルとティッカーの両方の表示を処理し、`jQuery.Color` を使用して赤と緑の色をフラッシュするようになりました。</span><span class="sxs-lookup"><span data-stu-id="ad46f-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="ad46f-377">*SignalR*の新機能では、マーケットの状態に基づいてボタンを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="ad46f-378">また、 **Live Stock ティッカー**の水平スクロールも停止または開始します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="ad46f-379">`ticker.client`には多くの関数が追加されるため、アプリは[jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="ad46f-380">接続を確立した後の追加のクライアントセットアップ</span><span class="sxs-lookup"><span data-stu-id="ad46f-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="ad46f-381">クライアントが接続を確立した後、次のような作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad46f-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="ad46f-382">市場がオープンまたは閉鎖されているかどうかを調べて、適切な `marketOpened` または `marketClosed` 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad46f-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="ad46f-383">サーバーメソッドの呼び出しをボタンにアタッチします。</span><span class="sxs-lookup"><span data-stu-id="ad46f-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="ad46f-384">サーバーメソッドは、アプリによって接続が確立されるまで、ボタンには接続されません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="ad46f-385">このため、使用可能になる前に、コードがサーバーメソッドを呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="ad46f-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad46f-386">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="ad46f-386">Additional resources</span></span>

<span data-ttu-id="ad46f-387">このチュートリアルでは、サーバーから接続されているすべてのクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラミングする方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ad46f-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="ad46f-388">これで、定期的にメッセージをブロードキャストしたり、任意のクライアントからの通知に応答したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="ad46f-389">マルチスレッドシングルトンインスタンスの概念を使用すると、マルチプレーヤーのオンラインゲームシナリオでサーバーの状態を維持できます。</span><span class="sxs-lookup"><span data-stu-id="ad46f-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="ad46f-390">例については、 [SignalR に基づく ShootR ゲーム](https://github.com/NTaylorMullen/ShootR)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="ad46f-391">ピアツーピア通信のシナリオを示すチュートリアルについては、「[はじめに](introduction-to-signalr.md)と[SignalR を使用したリアルタイム更新](tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="ad46f-392">SignalR の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="ad46f-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="ad46f-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="ad46f-394">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="ad46f-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="ad46f-395">SignalR GitHub とサンプル</span><span class="sxs-lookup"><span data-stu-id="ad46f-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="ad46f-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="ad46f-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="ad46f-397">次のステップ</span><span class="sxs-lookup"><span data-stu-id="ad46f-397">Next steps</span></span>

<span data-ttu-id="ad46f-398">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="ad46f-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad46f-399">プロジェクトが作成されました</span><span class="sxs-lookup"><span data-stu-id="ad46f-399">Created the project</span></span>
> * <span data-ttu-id="ad46f-400">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="ad46f-400">Set up the server code</span></span>
> * <span data-ttu-id="ad46f-401">サーバーコードを調べています</span><span class="sxs-lookup"><span data-stu-id="ad46f-401">Examined the server code</span></span>
> * <span data-ttu-id="ad46f-402">クライアントコードの設定</span><span class="sxs-lookup"><span data-stu-id="ad46f-402">Set up the client code</span></span>
> * <span data-ttu-id="ad46f-403">クライアントコードを調べる</span><span class="sxs-lookup"><span data-stu-id="ad46f-403">Examined the client code</span></span>
> * <span data-ttu-id="ad46f-404">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="ad46f-404">Tested the application</span></span>
> * <span data-ttu-id="ad46f-405">有効なログ記録</span><span class="sxs-lookup"><span data-stu-id="ad46f-405">Enabled logging</span></span>

<span data-ttu-id="ad46f-406">次の記事に進み、ASP.NET SignalR 2 を使用するリアルタイム web アプリケーションを作成する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="ad46f-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ad46f-407">SignalR を使用してリアルタイム web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="ad46f-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
