---
uid: signalr/overview/older-versions/signalr-performance
title: SignalR パフォーマンス (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: SignalR パフォーマンス
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468106"
---
# <a name="signalr-performance-signalr-1x"></a><span data-ttu-id="8d81d-103">SignalR パフォーマンス (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="8d81d-103">SignalR Performance (SignalR 1.x)</span></span>

<span data-ttu-id="8d81d-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="8d81d-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="8d81d-105">このトピックでは、SignalR アプリケーションのパフォーマンスを設計、測定、および向上させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>

<span data-ttu-id="8d81d-106">SignalR のパフォーマンスとスケーリングに関する最新のプレゼンテーションについては、「 [ASP.NET SignalR を使用したリアルタイム Web のスケーリング](https://channel9.msdn.com/Events/Build/2013/3-502)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="8d81d-107">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="8d81d-108">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="8d81d-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="8d81d-109">パフォーマンスを向上するための SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="8d81d-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="8d81d-110">パフォーマンスの問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="8d81d-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="8d81d-111">SignalR パフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="8d81d-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="8d81d-112">その他のパフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="8d81d-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="8d81d-113">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="8d81d-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="8d81d-114">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="8d81d-114">Design considerations</span></span>

<span data-ttu-id="8d81d-115">このセクションでは、不要なネットワークトラフィックを生成することによってパフォーマンスが阻害されないように、SignalR アプリケーションの設計時に実装できるパターンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="8d81d-116">メッセージ頻度の調整</span><span class="sxs-lookup"><span data-stu-id="8d81d-116">Throttling message frequency</span></span>

<span data-ttu-id="8d81d-117">高頻度 (リアルタイムゲームアプリケーションなど) でメッセージを送信するアプリケーションでも、ほとんどのアプリケーションでは、1秒間に数個を超えるメッセージを送信する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="8d81d-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="8d81d-118">各クライアントによって生成されるトラフィックの量を減らすために、メッセージループを実装して、メッセージをキューに配置し、一定の頻度よりも頻繁にメッセージを送信しないようにすることができます (つまり、その時間内にメッセージがある場合は、1秒ごとにメッセージが送信されます)。送信される terval。</span><span class="sxs-lookup"><span data-stu-id="8d81d-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="8d81d-119">クライアントとサーバーの両方から特定の速度にメッセージを調整するサンプルアプリケーションについては、「 [SignalR を使用した高頻度のリアルタイム](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="8d81d-120">メッセージサイズの縮小</span><span class="sxs-lookup"><span data-stu-id="8d81d-120">Reducing message size</span></span>

<span data-ttu-id="8d81d-121">シリアル化されたオブジェクトのサイズを小さくすることで、SignalR メッセージのサイズを小さくすることができます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="8d81d-122">サーバーコードで、送信する必要のないプロパティを含むオブジェクトを送信する場合は、`JsonIgnore` 属性を使用してこれらのプロパティをシリアル化できないようにします。</span><span class="sxs-lookup"><span data-stu-id="8d81d-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="8d81d-123">プロパティの名前もメッセージに格納されます。プロパティの名前は、`JsonProperty` 属性を使用して短縮できます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="8d81d-124">次のコードサンプルは、プロパティをクライアントに送信しないようにする方法と、プロパティ名を短縮する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8d81d-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="8d81d-125">**クライアントに送信されるデータから除外する JsonIgnore 属性と、メッセージサイズを減らすための Jsonignore 属性を示す .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="8d81d-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="8d81d-126">クライアントコードで読みやすさと保守性を維持するために、省略されたプロパティ名は、メッセージの受信後にわかりやすい名前に再マップできます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="8d81d-127">次のコードサンプルでは、メッセージコントラクト (マッピング) を定義し、`reMap` 関数を使用して最適化されたメッセージクラスにコントラクトを適用することによって、短い名前を長いものに再マップする方法の1つを示します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="8d81d-128">**短縮されたプロパティ名を人間が判読できる名前に再マップするクライアント側の JavaScript コード**</span><span class="sxs-lookup"><span data-stu-id="8d81d-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="8d81d-129">同じ方法を使用して、クライアントからサーバーへのメッセージでも名前を短縮できます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="8d81d-130">メッセージオブジェクトのメモリフットプリント (つまり、メッセージに使用されるメモリの量) を減らすことで、パフォーマンスを向上させることもできます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="8d81d-131">たとえば、`int` の範囲全体が不要な場合は、代わりに `short` または `byte` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="8d81d-132">メッセージはサーバーメモリ内のメッセージバスに格納されるため、メッセージのサイズを小さくすると、サーバーのメモリの問題に対処することもできます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="8d81d-133">パフォーマンスを向上するための SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="8d81d-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="8d81d-134">SignalR アプリケーションでパフォーマンスを向上させるために、次の構成設定を使用してサーバーをチューニングできます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="8d81d-135">ASP.NET アプリケーションのパフォーマンスを向上させる方法に関する一般的な情報については、「 [ASP.NET パフォーマンスの向上](https://msdn.microsoft.com/library/ff647787.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="8d81d-136">**SignalR の構成設定**</span><span class="sxs-lookup"><span data-stu-id="8d81d-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="8d81d-137">**Defaultmessagebuffersize**: 既定では、SignalR は、接続ごとに1000のメッセージを各ハブのメモリに保持します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="8d81d-138">サイズの大きいメッセージが使用されている場合は、この値を小さくすることで緩和できるメモリの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="8d81d-139">この設定は、ASP.NET アプリケーションの `Application_Start` イベントハンドラー、または自己ホスト型アプリケーションの OWIN startup クラスの `Configuration` メソッドで設定できます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="8d81d-140">次のサンプルでは、使用されるサーバーメモリの量を減らすために、アプリケーションのメモリフットプリントを削減するために、この値を小さくする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="8d81d-141">**既定のメッセージバッファーサイズを減らすための global.asax の .NET サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="8d81d-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="8d81d-142">**IIS 構成の設定**</span><span class="sxs-lookup"><span data-stu-id="8d81d-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="8d81d-143">**アプリケーションあたりの最大同時要求**数: 同時 IIS 要求の数を増やすと、要求の処理に使用できるサーバーリソースが増加します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="8d81d-144">既定値は5000です。この設定を増やすには、管理者特権のコマンドプロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="8d81d-145">**ASP.NET の構成設定**</span><span class="sxs-lookup"><span data-stu-id="8d81d-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="8d81d-146">このセクションには、`aspnet.config` ファイルで設定できる構成設定が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d81d-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="8d81d-147">このファイルは、プラットフォームに応じて、次の2つの場所のいずれかにあります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="8d81d-148">SignalR のパフォーマンスを向上させる ASP.NET 設定には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="8d81d-149">**CPU あたりの最大同時要求数**: この設定を増やすと、パフォーマンスのボトルネックが軽減される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="8d81d-150">この設定を増やすには、次の構成設定を `aspnet.config` ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="8d81d-151">**要求キューの制限**: 接続の合計数が `maxConcurrentRequestsPerCPU` 設定を超えると、ASP.NET はキューを使用して要求の調整を開始します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="8d81d-152">キューのサイズを大きくするには、`requestQueueLimit` 設定を大きくします。</span><span class="sxs-lookup"><span data-stu-id="8d81d-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="8d81d-153">これを行うには、次の構成設定を `config/machine.config` の `processModel` ノードに追加します (`aspnet.config`ではありません)。</span><span class="sxs-lookup"><span data-stu-id="8d81d-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="8d81d-154">パフォーマンスに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="8d81d-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="8d81d-155">ここでは、アプリケーションのパフォーマンスのボトルネックを検出する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="8d81d-156">WebSocket が使用されていることを確認しています</span><span class="sxs-lookup"><span data-stu-id="8d81d-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="8d81d-157">SignalR ではクライアントとサーバー間の通信にさまざまなトランスポートを使用できますが、WebSocket ではパフォーマンスが大幅に向上します。クライアントとサーバーがそれをサポートする場合は、この機能を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="8d81d-158">クライアントとサーバーが WebSocket の要件を満たしているかどうかを判断するには、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="8d81d-159">アプリケーションで使用されているトランスポートを確認するには、ブラウザー開発者ツールを使用し、ログを調べて、接続に使用されているトランスポートを確認します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="8d81d-160">Internet Explorer と Chrome でブラウザー開発ツールを使用する方法の詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="8d81d-161">SignalR パフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="8d81d-161">Using SignalR performance counters</span></span>

<span data-ttu-id="8d81d-162">このセクションでは、`Microsoft.AspNet.SignalR.Utils` パッケージに含まれる SignalR パフォーマンスカウンターを有効にして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="8d81d-163">Signalr のインストール</span><span class="sxs-lookup"><span data-stu-id="8d81d-163">Installing signalr.exe</span></span>

<span data-ttu-id="8d81d-164">パフォーマンスカウンターは、SignalR というユーティリティを使用してサーバーに追加できます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-164">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="8d81d-165">このユーティリティをインストールするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="8d81d-166">Visual Studio で、 **[ツール]**  >  **[nuget パッケージマネージャー]**  >  **[ソリューションの nuget パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="8d81d-167">**Signalr**を検索し、[インストール] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="8d81d-168">使用許諾契約書に同意して、パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8d81d-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="8d81d-169">SignalR は `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="8d81d-170">SignalR を使用したパフォーマンスカウンターのインストール</span><span class="sxs-lookup"><span data-stu-id="8d81d-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="8d81d-171">SignalR パフォーマンスカウンターをインストールするには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="8d81d-172">SignalR パフォーマンスカウンターを削除するには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="8d81d-173">SignalR パフォーマンスカウンター</span><span class="sxs-lookup"><span data-stu-id="8d81d-173">SignalR Performance counters</span></span>

<span data-ttu-id="8d81d-174">ユーティリティパッケージでは、次のパフォーマンスカウンターがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-174">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="8d81d-175">"Total" カウンターは、最後のアプリケーションプールまたはサーバーの再起動以降に発生したイベントの数を計測します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="8d81d-176">**接続メトリック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-176">**Connection metrics**</span></span>

<span data-ttu-id="8d81d-177">次のメトリックは、発生した接続の有効期間イベントを測定します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="8d81d-178">詳細については、「[接続の有効期間イベントの理解と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="8d81d-179">**接続された接続**</span><span class="sxs-lookup"><span data-stu-id="8d81d-179">**Connections Connected**</span></span>
- <span data-ttu-id="8d81d-180">**再接続した接続**</span><span class="sxs-lookup"><span data-stu-id="8d81d-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="8d81d-181">**切断された接続**</span><span class="sxs-lookup"><span data-stu-id="8d81d-181">**Connections Disconnected**</span></span>
- <span data-ttu-id="8d81d-182">**現在の接続**</span><span class="sxs-lookup"><span data-stu-id="8d81d-182">**Connections Current**</span></span>

<span data-ttu-id="8d81d-183">**メッセージメトリック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-183">**Message metrics**</span></span>

<span data-ttu-id="8d81d-184">次のメトリックは、SignalR によって生成されるメッセージトラフィックを測定します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="8d81d-185">**受信した接続メッセージの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="8d81d-186">**送信された接続メッセージの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="8d81d-187">**1秒あたりの受信接続メッセージ数**</span><span class="sxs-lookup"><span data-stu-id="8d81d-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="8d81d-188">**送信された接続メッセージ数/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="8d81d-189">**メッセージバスメトリック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-189">**Message bus metrics**</span></span>

<span data-ttu-id="8d81d-190">次のメトリックは、内部 SignalR メッセージバスを通過するトラフィックを測定します。このキューは、すべての受信および送信 SignalR メッセージが配置されます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="8d81d-191">メッセージは、送信またはブロードキャストされるときに**公開**されます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="8d81d-192">このコンテキストの**サブスクライバー**は、メッセージバスのサブスクリプションです。これは、クライアントの数にサーバー自体を加えた数と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d81d-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="8d81d-193">**割り当てら**れたワーカーは、アクティブな接続にデータを送信するコンポーネントです。**ビジー状態のワーカー**は、メッセージをアクティブに送信しているものです。</span><span class="sxs-lookup"><span data-stu-id="8d81d-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="8d81d-194">**メッセージバスメッセージ受信合計数**</span><span class="sxs-lookup"><span data-stu-id="8d81d-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="8d81d-195">**1秒あたりのメッセージバスメッセージ受信数**</span><span class="sxs-lookup"><span data-stu-id="8d81d-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="8d81d-196">**メッセージバスメッセージの公開総数**</span><span class="sxs-lookup"><span data-stu-id="8d81d-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="8d81d-197">**公開されたメッセージバスメッセージ数/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="8d81d-198">**現在のメッセージバスサブスクライバー**</span><span class="sxs-lookup"><span data-stu-id="8d81d-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="8d81d-199">**メッセージバスサブスクライバーの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="8d81d-200">**メッセージバスサブスクライバー数/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="8d81d-201">**メッセージバスで割り当てられたワーカー**</span><span class="sxs-lookup"><span data-stu-id="8d81d-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="8d81d-202">**メッセージバスビジーワーカー**</span><span class="sxs-lookup"><span data-stu-id="8d81d-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="8d81d-203">**現在のメッセージバストピック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="8d81d-204">**エラーのメトリック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-204">**Error metrics**</span></span>

<span data-ttu-id="8d81d-205">次のメトリックは、SignalR メッセージトラフィックによって生成されるエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="8d81d-206">ハブの**解決**エラーは、ハブまたはハブのメソッドを解決できない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="8d81d-207">ハブの**呼び出し**エラーは、ハブメソッドの呼び出し中にスローされる例外です。</span><span class="sxs-lookup"><span data-stu-id="8d81d-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="8d81d-208">**トランスポート**エラーは、HTTP 要求または応答の間にスローされた接続エラーです。</span><span class="sxs-lookup"><span data-stu-id="8d81d-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="8d81d-209">**エラー: すべての合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-209">**Errors: All Total**</span></span>
- <span data-ttu-id="8d81d-210">**エラー: すべて/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="8d81d-211">**エラー: ハブの解決の合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="8d81d-212">**エラー: 1 秒あたりのハブの解決**</span><span class="sxs-lookup"><span data-stu-id="8d81d-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="8d81d-213">**エラー: ハブ呼び出しの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="8d81d-214">**エラー: 1 秒あたりのハブ呼び出し数**</span><span class="sxs-lookup"><span data-stu-id="8d81d-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="8d81d-215">**エラー: トランスポートの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="8d81d-216">**エラー: トランスポート/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="8d81d-217">**スケールアウトメトリック**</span><span class="sxs-lookup"><span data-stu-id="8d81d-217">**Scaleout metrics**</span></span>

<span data-ttu-id="8d81d-218">次のメトリックは、スケールアウトプロバイダーによって生成されたトラフィックとエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="8d81d-219">このコンテキストの**ストリーム**は、スケールアウトプロバイダーによって使用されるスケール単位です。これは、SQL Server が使用されている場合はテーブル、Service Bus が使用されている場合はトピック、Redis が使用されている場合はサブスクリプションです。</span><span class="sxs-lookup"><span data-stu-id="8d81d-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="8d81d-220">既定では、1つのストリームのみが使用されますが、これは SQL Server と Service Bus の構成を使用して増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="8d81d-221">**バッファリング**ストリームは、エラー状態になったストリームです。ストリームが faulted 状態の場合、バックプレーンに送信されるすべてのメッセージは、ストリームがエラーにならなくなるまで直ちに失敗します。</span><span class="sxs-lookup"><span data-stu-id="8d81d-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="8d81d-222">**送信キューの長さ**は、投稿されているがまだ送信されていないメッセージの数です。</span><span class="sxs-lookup"><span data-stu-id="8d81d-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="8d81d-223">**スケールアウトされたメッセージバスメッセージ受信数/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="8d81d-224">**スケールアウトストリームの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="8d81d-225">**スケールアウトストリームを開く**</span><span class="sxs-lookup"><span data-stu-id="8d81d-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="8d81d-226">**スケールアウトストリームのバッファリング**</span><span class="sxs-lookup"><span data-stu-id="8d81d-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="8d81d-227">**スケールアウトエラーの合計**</span><span class="sxs-lookup"><span data-stu-id="8d81d-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="8d81d-228">**スケールアウトエラー/秒**</span><span class="sxs-lookup"><span data-stu-id="8d81d-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="8d81d-229">**スケールアウト送信キューの長さ**</span><span class="sxs-lookup"><span data-stu-id="8d81d-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="8d81d-230">これらのカウンターで測定される内容の詳細については、「 [SignalR のスケールアウトと Azure Service Bus](scaleout-with-windows-azure-service-bus.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="8d81d-231">その他のパフォーマンスカウンターの使用</span><span class="sxs-lookup"><span data-stu-id="8d81d-231">Using other performance counters</span></span>

<span data-ttu-id="8d81d-232">次のパフォーマンスカウンターは、アプリケーションのパフォーマンスの監視にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8d81d-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="8d81d-233">**[メモリ]**</span><span class="sxs-lookup"><span data-stu-id="8d81d-233">**Memory**</span></span>

- <span data-ttu-id="8d81d-234">すべてのヒープ内の .NET CLR メモリ # バイト (w3wp.exe 用)</span><span class="sxs-lookup"><span data-stu-id="8d81d-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="8d81d-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="8d81d-235">**ASP.NET**</span></span>

- <span data-ttu-id="8d81d-236">ASP.NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="8d81d-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="8d81d-237">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="8d81d-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="8d81d-238">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="8d81d-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="8d81d-239">**CPU**</span><span class="sxs-lookup"><span data-stu-id="8d81d-239">**CPU**</span></span>

- <span data-ttu-id="8d81d-240">プロセッサ情報、プロセッサ時間</span><span class="sxs-lookup"><span data-stu-id="8d81d-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="8d81d-241">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="8d81d-241">**TCP/IP**</span></span>

- <span data-ttu-id="8d81d-242">確立された TCPv6/接続</span><span class="sxs-lookup"><span data-stu-id="8d81d-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="8d81d-243">確立された TCPv4/接続</span><span class="sxs-lookup"><span data-stu-id="8d81d-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="8d81d-244">**Web サービス**</span><span class="sxs-lookup"><span data-stu-id="8d81d-244">**Web Service**</span></span>

- <span data-ttu-id="8d81d-245">Web サービス \ 現在の接続</span><span class="sxs-lookup"><span data-stu-id="8d81d-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="8d81d-246">Web サービス \ 最大接続数</span><span class="sxs-lookup"><span data-stu-id="8d81d-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="8d81d-247">**スレッド化**</span><span class="sxs-lookup"><span data-stu-id="8d81d-247">**Threading**</span></span>

- <span data-ttu-id="8d81d-248">現在の論理スレッドの .NET CLR LocksAndThreads\#</span><span class="sxs-lookup"><span data-stu-id="8d81d-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="8d81d-249">現在の物理スレッドの\# .NET CLR LocksAnd スレッド</span><span class="sxs-lookup"><span data-stu-id="8d81d-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="8d81d-250">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="8d81d-250">Other Resources</span></span>

<span data-ttu-id="8d81d-251">ASP.NET のパフォーマンスの監視とチューニングの詳細については、次のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d81d-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="8d81d-252">[ASP.NET のパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="8d81d-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="8d81d-253">IIS 7.5、IIS 7.0、および IIS 6.0 での ASP.NET スレッドの使用</span><span class="sxs-lookup"><span data-stu-id="8d81d-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="8d81d-254">&lt;applicationPool&gt; 要素 (Web 設定)</span><span class="sxs-lookup"><span data-stu-id="8d81d-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
