---
uid: signalr/overview/performance/signalr-performance
title: SignalR Performance |Microsoft Docs
author: bradygaster
description: SignalR パフォーマンス
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449860"
---
# <a name="signalr-performance"></a><span data-ttu-id="20d1b-103">SignalR パフォーマンス</span><span class="sxs-lookup"><span data-stu-id="20d1b-103">SignalR Performance</span></span>

<span data-ttu-id="20d1b-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="20d1b-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="20d1b-105">このトピックでは、SignalR アプリケーションのパフォーマンスを設計、測定、および向上させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="20d1b-106">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="20d1b-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="20d1b-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="20d1b-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="20d1b-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="20d1b-108">.NET 4.5</span></span>
> - <span data-ttu-id="20d1b-109">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="20d1b-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="20d1b-110">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="20d1b-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="20d1b-111">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="20d1b-112">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="20d1b-112">Questions and comments</span></span>
>
> <span data-ttu-id="20d1b-113">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="20d1b-114">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="20d1b-115">SignalR のパフォーマンスとスケーリングに関する最新のプレゼンテーションについては、「 [ASP.NET SignalR を使用したリアルタイム Web のスケーリング](https://channel9.msdn.com/Events/Build/2013/3-502)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="20d1b-116">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="20d1b-117">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="20d1b-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="20d1b-118">パフォーマンスを向上するための SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="20d1b-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="20d1b-119">パフォーマンスの問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="20d1b-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="20d1b-120">SignalR パフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="20d1b-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="20d1b-121">その他のパフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="20d1b-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="20d1b-122">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="20d1b-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="20d1b-123">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="20d1b-123">Design considerations</span></span>

<span data-ttu-id="20d1b-124">このセクションでは、不要なネットワークトラフィックを生成することによってパフォーマンスが阻害されないように、SignalR アプリケーションの設計時に実装できるパターンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="20d1b-125">メッセージ頻度の調整</span><span class="sxs-lookup"><span data-stu-id="20d1b-125">Throttling message frequency</span></span>

<span data-ttu-id="20d1b-126">高頻度 (リアルタイムゲームアプリケーションなど) でメッセージを送信するアプリケーションでも、ほとんどのアプリケーションでは、1秒間に数個を超えるメッセージを送信する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="20d1b-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="20d1b-127">各クライアントによって生成されるトラフィックの量を減らすために、メッセージループを実装して、メッセージをキューに配置し、一定の頻度よりも頻繁にメッセージを送信しないようにすることができます (つまり、その時間内にメッセージがある場合は、1秒ごとにメッセージが送信されます)。送信される terval。</span><span class="sxs-lookup"><span data-stu-id="20d1b-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="20d1b-128">クライアントとサーバーの両方から特定の速度にメッセージを調整するサンプルアプリケーションについては、「 [SignalR を使用した高頻度のリアルタイム](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="20d1b-129">メッセージサイズの縮小</span><span class="sxs-lookup"><span data-stu-id="20d1b-129">Reducing message size</span></span>

<span data-ttu-id="20d1b-130">シリアル化されたオブジェクトのサイズを小さくすることで、SignalR メッセージのサイズを小さくすることができます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="20d1b-131">サーバーコードで、送信する必要のないプロパティを含むオブジェクトを送信する場合は、`JsonIgnore` 属性を使用してこれらのプロパティをシリアル化できないようにします。</span><span class="sxs-lookup"><span data-stu-id="20d1b-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="20d1b-132">プロパティの名前もメッセージに格納されます。プロパティの名前は、`JsonProperty` 属性を使用して短縮できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="20d1b-133">次のコードサンプルは、プロパティをクライアントに送信しないようにする方法と、プロパティ名を短縮する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="20d1b-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="20d1b-134">**クライアントに送信されるデータから除外する JsonIgnore 属性と、メッセージサイズを減らすための Jsonignore 属性を示す .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="20d1b-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="20d1b-135">クライアントコードで読みやすさと保守性を維持するために、省略されたプロパティ名は、メッセージの受信後にわかりやすい名前に再マップできます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="20d1b-136">次のコードサンプルでは、メッセージコントラクト (マッピング) を定義し、`reMap` 関数を使用して最適化されたメッセージクラスにコントラクトを適用することによって、短い名前を長いものに再マップする方法の1つを示します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="20d1b-137">**短縮されたプロパティ名を人間が判読できる名前に再マップするクライアント側の JavaScript コード**</span><span class="sxs-lookup"><span data-stu-id="20d1b-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="20d1b-138">同じ方法を使用して、クライアントからサーバーへのメッセージでも名前を短縮できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="20d1b-139">メッセージオブジェクトのメモリフットプリント (つまり、メッセージに使用されるメモリの量) を減らすことで、パフォーマンスを向上させることもできます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="20d1b-140">たとえば、`int` の範囲全体が不要な場合は、代わりに `short` または `byte` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="20d1b-141">メッセージはサーバーメモリ内のメッセージバスに格納されるため、メッセージのサイズを小さくすると、サーバーのメモリの問題に対処することもできます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="20d1b-142">パフォーマンスを向上するための SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="20d1b-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="20d1b-143">SignalR アプリケーションでパフォーマンスを向上させるために、次の構成設定を使用してサーバーをチューニングできます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="20d1b-144">ASP.NET アプリケーションのパフォーマンスを向上させる方法に関する一般的な情報については、「 [ASP.NET パフォーマンスの向上](https://msdn.microsoft.com/library/ff647787.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="20d1b-145">**SignalR の構成設定**</span><span class="sxs-lookup"><span data-stu-id="20d1b-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="20d1b-146">**Defaultmessagebuffersize**: 既定では、SignalR は、接続ごとに1000のメッセージを各ハブのメモリに保持します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="20d1b-147">サイズの大きいメッセージが使用されている場合は、この値を小さくすることで緩和できるメモリの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="20d1b-148">この設定は、ASP.NET アプリケーションの `Application_Start` イベントハンドラー、または自己ホスト型アプリケーションの OWIN startup クラスの `Configuration` メソッドで設定できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="20d1b-149">次のサンプルでは、使用されるサーバーメモリの量を減らすために、アプリケーションのメモリフットプリントを削減するために、この値を小さくする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="20d1b-150">**既定のメッセージバッファーサイズを減らすための Startup.cs の .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="20d1b-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="20d1b-151">**IIS 構成の設定**</span><span class="sxs-lookup"><span data-stu-id="20d1b-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="20d1b-152">**アプリケーションあたりの最大同時要求**数: 同時 IIS 要求の数を増やすと、要求の処理に使用できるサーバーリソースが増加します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="20d1b-153">既定値は5000です。この設定を増やすには、管理者特権のコマンドプロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="20d1b-154">**ApplicationPool QueueLength**: これは、アプリケーションプールの http.sys キューに対する要求の最大数です。</span><span class="sxs-lookup"><span data-stu-id="20d1b-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="20d1b-155">キューがいっぱいになると、新しい要求は 503 "サービスを利用できません" という応答を受信します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="20d1b-156">既定値は 1000 です。</span><span class="sxs-lookup"><span data-stu-id="20d1b-156">The default value is 1000.</span></span>

    <span data-ttu-id="20d1b-157">アプリケーションをホストするアプリケーションプールでワーカープロセスのキューの長さを短くすると、メモリリソースが節約されます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="20d1b-158">詳細については、「[アプリケーションプールの管理、チューニング、および構成](https://technet.microsoft.com/library/cc745955.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="20d1b-159">**ASP.NET の構成設定**</span><span class="sxs-lookup"><span data-stu-id="20d1b-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="20d1b-160">このセクションには、`aspnet.config` ファイルで設定できる構成設定が含まれています。</span><span class="sxs-lookup"><span data-stu-id="20d1b-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="20d1b-161">このファイルは、プラットフォームに応じて、次の2つの場所のいずれかにあります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="20d1b-162">SignalR のパフォーマンスを向上させる ASP.NET 設定には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="20d1b-163">**CPU あたりの最大同時要求数**: この設定を増やすと、パフォーマンスのボトルネックが軽減される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="20d1b-164">この設定を増やすには、次の構成設定を `aspnet.config` ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="20d1b-165">**要求キューの制限**: 接続の合計数が `maxConcurrentRequestsPerCPU` 設定を超えると、ASP.NET はキューを使用して要求の調整を開始します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="20d1b-166">キューのサイズを大きくするには、`requestQueueLimit` 設定を大きくします。</span><span class="sxs-lookup"><span data-stu-id="20d1b-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="20d1b-167">これを行うには、次の構成設定を `config/machine.config` の `processModel` ノードに追加します (`aspnet.config`ではありません)。</span><span class="sxs-lookup"><span data-stu-id="20d1b-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="20d1b-168">パフォーマンスに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="20d1b-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="20d1b-169">ここでは、アプリケーションのパフォーマンスのボトルネックを検出する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="20d1b-170">WebSocket が使用されていることを確認しています</span><span class="sxs-lookup"><span data-stu-id="20d1b-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="20d1b-171">SignalR ではクライアントとサーバー間の通信にさまざまなトランスポートを使用できますが、WebSocket ではパフォーマンスが大幅に向上します。クライアントとサーバーがそれをサポートする場合は、この機能を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="20d1b-172">クライアントとサーバーが WebSocket の要件を満たしているかどうかを判断するには、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="20d1b-173">アプリケーションで使用されているトランスポートを確認するには、ブラウザー開発者ツールを使用し、ログを調べて、接続に使用されているトランスポートを確認します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="20d1b-174">Internet Explorer と Chrome でブラウザー開発ツールを使用する方法の詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="20d1b-175">SignalR パフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="20d1b-175">Using SignalR performance counters</span></span>

<span data-ttu-id="20d1b-176">このセクションでは、`Microsoft.AspNet.SignalR.Utils` パッケージに含まれる SignalR パフォーマンスカウンターを有効にして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="20d1b-177">Signalr のインストール</span><span class="sxs-lookup"><span data-stu-id="20d1b-177">Installing signalr.exe</span></span>

<span data-ttu-id="20d1b-178">パフォーマンスカウンターは、SignalR というユーティリティを使用してサーバーに追加できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="20d1b-179">このユーティリティをインストールするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="20d1b-180">Visual Studio で、 **[ツール]**  >  **[nuget パッケージマネージャー]**  >  **[ソリューションの nuget パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="20d1b-181">**Signalr**を検索し、[インストール] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="20d1b-182">使用許諾契約書に同意して、パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="20d1b-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="20d1b-183">SignalR は `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="20d1b-184">SignalR を使用したパフォーマンスカウンターのインストール</span><span class="sxs-lookup"><span data-stu-id="20d1b-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="20d1b-185">SignalR パフォーマンスカウンターをインストールするには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="20d1b-186">SignalR パフォーマンスカウンターを削除するには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="20d1b-187">SignalR パフォーマンスカウンター</span><span class="sxs-lookup"><span data-stu-id="20d1b-187">SignalR Performance counters</span></span>

<span data-ttu-id="20d1b-188">ユーティリティパッケージでは、次のパフォーマンスカウンターがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="20d1b-189">"Total" カウンターは、最後のアプリケーションプールまたはサーバーの再起動以降に発生したイベントの数を計測します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="20d1b-190">**接続メトリック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-190">**Connection metrics**</span></span>

<span data-ttu-id="20d1b-191">次のメトリックは、発生した接続の有効期間イベントを測定します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="20d1b-192">詳細については、「[接続の有効期間イベントの理解と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="20d1b-193">**接続された接続**</span><span class="sxs-lookup"><span data-stu-id="20d1b-193">**Connections Connected**</span></span>
- <span data-ttu-id="20d1b-194">**再接続した接続**</span><span class="sxs-lookup"><span data-stu-id="20d1b-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="20d1b-195">**切断された接続**</span><span class="sxs-lookup"><span data-stu-id="20d1b-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="20d1b-196">**現在の接続**</span><span class="sxs-lookup"><span data-stu-id="20d1b-196">**Connections Current**</span></span>

<span data-ttu-id="20d1b-197">**メッセージメトリック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-197">**Message metrics**</span></span>

<span data-ttu-id="20d1b-198">次のメトリックは、SignalR によって生成されるメッセージトラフィックを測定します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="20d1b-199">**受信した接続メッセージの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="20d1b-200">**送信された接続メッセージの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="20d1b-201">**1秒あたりの受信接続メッセージ数**</span><span class="sxs-lookup"><span data-stu-id="20d1b-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="20d1b-202">**送信された接続メッセージ数/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="20d1b-203">**メッセージバスメトリック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-203">**Message bus metrics**</span></span>

<span data-ttu-id="20d1b-204">次のメトリックは、内部 SignalR メッセージバスを通過するトラフィックを測定します。このキューは、すべての受信および送信 SignalR メッセージが配置されます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="20d1b-205">メッセージは、送信またはブロードキャストされるときに**公開**されます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="20d1b-206">このコンテキストの**サブスクライバー**は、メッセージバスのサブスクリプションです。これは、クライアントの数にサーバー自体を加えた数と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d1b-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="20d1b-207">**割り当てら**れたワーカーは、アクティブな接続にデータを送信するコンポーネントです。**ビジー状態のワーカー**は、メッセージをアクティブに送信しているものです。</span><span class="sxs-lookup"><span data-stu-id="20d1b-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="20d1b-208">**メッセージバスメッセージ受信合計数**</span><span class="sxs-lookup"><span data-stu-id="20d1b-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="20d1b-209">**1秒あたりのメッセージバスメッセージ受信数**</span><span class="sxs-lookup"><span data-stu-id="20d1b-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="20d1b-210">**メッセージバスメッセージの公開総数**</span><span class="sxs-lookup"><span data-stu-id="20d1b-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="20d1b-211">**公開されたメッセージバスメッセージ数/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="20d1b-212">**現在のメッセージバスサブスクライバー**</span><span class="sxs-lookup"><span data-stu-id="20d1b-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="20d1b-213">**メッセージバスサブスクライバーの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="20d1b-214">**メッセージバスサブスクライバー数/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="20d1b-215">**メッセージバスで割り当てられたワーカー**</span><span class="sxs-lookup"><span data-stu-id="20d1b-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="20d1b-216">**メッセージバスビジーワーカー**</span><span class="sxs-lookup"><span data-stu-id="20d1b-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="20d1b-217">**現在のメッセージバストピック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="20d1b-218">**エラーのメトリック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-218">**Error metrics**</span></span>

<span data-ttu-id="20d1b-219">次のメトリックは、SignalR メッセージトラフィックによって生成されるエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="20d1b-220">ハブの**解決**エラーは、ハブまたはハブのメソッドを解決できない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="20d1b-221">ハブの**呼び出し**エラーは、ハブメソッドの呼び出し中にスローされる例外です。</span><span class="sxs-lookup"><span data-stu-id="20d1b-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="20d1b-222">**トランスポート**エラーは、HTTP 要求または応答の間にスローされた接続エラーです。</span><span class="sxs-lookup"><span data-stu-id="20d1b-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="20d1b-223">**エラー: すべての合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-223">**Errors: All Total**</span></span>
- <span data-ttu-id="20d1b-224">**エラー: すべて/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="20d1b-225">**エラー: ハブの解決の合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="20d1b-226">**エラー: 1 秒あたりのハブの解決**</span><span class="sxs-lookup"><span data-stu-id="20d1b-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="20d1b-227">**エラー: ハブ呼び出しの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="20d1b-228">**エラー: 1 秒あたりのハブ呼び出し数**</span><span class="sxs-lookup"><span data-stu-id="20d1b-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="20d1b-229">**エラー: トランスポートの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="20d1b-230">**エラー: トランスポート/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="20d1b-231">**スケールアウトメトリック**</span><span class="sxs-lookup"><span data-stu-id="20d1b-231">**Scaleout metrics**</span></span>

<span data-ttu-id="20d1b-232">次のメトリックは、スケールアウトプロバイダーによって生成されたトラフィックとエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="20d1b-233">このコンテキストの**ストリーム**は、スケールアウトプロバイダーによって使用されるスケール単位です。これは、SQL Server が使用されている場合はテーブル、Service Bus が使用されている場合はトピック、Redis が使用されている場合はサブスクリプションです。</span><span class="sxs-lookup"><span data-stu-id="20d1b-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="20d1b-234">各ストリームは、順次読み取りおよび書き込み操作を保証します。1つのストリームは、スケールのボトルネックとなる可能性があるため、そのボトルネックを減らすために、ストリームの数を増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="20d1b-235">複数のストリームが使用されている場合、SignalR は、特定の接続から送信されたメッセージが順番になるように、これらのストリーム間でメッセージを自動的に分散します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="20d1b-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定は、SignalR によって管理されるスケールアウト送信キューの長さを制御します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="20d1b-237">0より大きい値に設定すると、送信キュー内のすべてのメッセージが、構成済みのメッセージングバックプレーンに一度に1つずつ送信されます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="20d1b-238">キューのサイズが構成された長さを超えた場合、キュー内のメッセージの数が再度設定されるまで、その後の送信の呼び出しはすぐに[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)で失敗します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="20d1b-239">実装された背面には、通常独自のキューまたはフロー制御が設定されているため、既定では、キューは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="20d1b-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="20d1b-240">SQL Server の場合、接続プールは、一度に行われる送信の数を効果的に制限します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="20d1b-241">既定では、SQL Server と Redis には1つのストリームのみが使用され、Service Bus には5つのストリームが使用され、キューは無効になりますが、SQL Server と Service Bus で構成を使用してこれらの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="20d1b-242">**SQL Server バックプレーンのテーブル数とキューの長さを構成するための .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="20d1b-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="20d1b-243">**Service Bus バックプレーンのトピック数とキューの長さを構成するための .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="20d1b-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="20d1b-244">**バッファリング**ストリームは、エラー状態になったストリームです。ストリームが faulted 状態の場合、バックプレーンに送信されるすべてのメッセージは、ストリームがエラーにならなくなるまで直ちに失敗します。</span><span class="sxs-lookup"><span data-stu-id="20d1b-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="20d1b-245">**送信キューの長さ**は、投稿されているがまだ送信されていないメッセージの数です。</span><span class="sxs-lookup"><span data-stu-id="20d1b-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="20d1b-246">**スケールアウトされたメッセージバスメッセージ受信数/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="20d1b-247">**スケールアウトストリームの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="20d1b-248">**スケールアウトストリームを開く**</span><span class="sxs-lookup"><span data-stu-id="20d1b-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="20d1b-249">**スケールアウトストリームのバッファリング**</span><span class="sxs-lookup"><span data-stu-id="20d1b-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="20d1b-250">**スケールアウトエラーの合計**</span><span class="sxs-lookup"><span data-stu-id="20d1b-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="20d1b-251">**スケールアウトエラー/秒**</span><span class="sxs-lookup"><span data-stu-id="20d1b-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="20d1b-252">**スケールアウト送信キューの長さ**</span><span class="sxs-lookup"><span data-stu-id="20d1b-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="20d1b-253">これらのカウンターで測定される内容の詳細については、「 [SignalR のスケールアウトと Azure Service Bus](scaleout-with-windows-azure-service-bus.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="20d1b-254">その他のパフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="20d1b-254">Using other performance counters</span></span>

<span data-ttu-id="20d1b-255">次のパフォーマンスカウンターは、アプリケーションのパフォーマンスの監視にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="20d1b-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="20d1b-256">**[メモリ]**</span><span class="sxs-lookup"><span data-stu-id="20d1b-256">**Memory**</span></span>

- <span data-ttu-id="20d1b-257">.NET CLR メモリ\\すべてのヒープ内のバイト数 (w3wp.exe 用)</span><span class="sxs-lookup"><span data-stu-id="20d1b-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="20d1b-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="20d1b-258">**ASP.NET**</span></span>

- <span data-ttu-id="20d1b-259">ASP.NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="20d1b-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="20d1b-260">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="20d1b-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="20d1b-261">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="20d1b-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="20d1b-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="20d1b-262">**CPU**</span></span>

- <span data-ttu-id="20d1b-263">プロセッサ情報、プロセッサ時間</span><span class="sxs-lookup"><span data-stu-id="20d1b-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="20d1b-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="20d1b-264">**TCP/IP**</span></span>

- <span data-ttu-id="20d1b-265">確立された TCPv6/接続</span><span class="sxs-lookup"><span data-stu-id="20d1b-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="20d1b-266">確立された TCPv4/接続</span><span class="sxs-lookup"><span data-stu-id="20d1b-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="20d1b-267">**Web サービス**</span><span class="sxs-lookup"><span data-stu-id="20d1b-267">**Web Service**</span></span>

- <span data-ttu-id="20d1b-268">Web サービス \ 現在の接続</span><span class="sxs-lookup"><span data-stu-id="20d1b-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="20d1b-269">Web サービス \ 最大接続数</span><span class="sxs-lookup"><span data-stu-id="20d1b-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="20d1b-270">**スレッド化**</span><span class="sxs-lookup"><span data-stu-id="20d1b-270">**Threading**</span></span>

- <span data-ttu-id="20d1b-271">.NET CLR ロックとスレッド\\現在の論理スレッドの数</span><span class="sxs-lookup"><span data-stu-id="20d1b-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="20d1b-272">.NET CLR ロックとスレッド\\現在の物理スレッドの数</span><span class="sxs-lookup"><span data-stu-id="20d1b-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="20d1b-273">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="20d1b-273">Other Resources</span></span>

<span data-ttu-id="20d1b-274">ASP.NET のパフォーマンスの監視とチューニングの詳細については、次のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d1b-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="20d1b-275">[ASP.NET のパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="20d1b-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="20d1b-276">IIS 7.5、IIS 7.0、および IIS 6.0 での ASP.NET スレッドの使用</span><span class="sxs-lookup"><span data-stu-id="20d1b-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="20d1b-277">&lt;applicationPool&gt; 要素 (Web 設定)</span><span class="sxs-lookup"><span data-stu-id="20d1b-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
