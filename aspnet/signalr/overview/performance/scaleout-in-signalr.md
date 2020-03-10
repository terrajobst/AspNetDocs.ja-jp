---
uid: signalr/overview/performance/scaleout-in-signalr
title: SignalR のスケールアウトの概要 |Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14dc22f99a43b566903c59fb23b7d419350f4a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467782"
---
# <a name="introduction-to-scaleout-in-signalr"></a><span data-ttu-id="bdba8-103">SignalR のスケールアウト入門</span><span class="sxs-lookup"><span data-stu-id="bdba8-103">Introduction to Scaleout in SignalR</span></span>

<span data-ttu-id="bdba8-104">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="bdba8-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="bdba8-105">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="bdba8-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="bdba8-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bdba8-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="bdba8-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="bdba8-107">.NET 4.5</span></span>
> - <span data-ttu-id="bdba8-108">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="bdba8-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="bdba8-109">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="bdba8-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="bdba8-110">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdba8-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="bdba8-111">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="bdba8-111">Questions and comments</span></span>
>
> <span data-ttu-id="bdba8-112">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="bdba8-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="bdba8-113">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="bdba8-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="bdba8-114">一般に、web アプリケーションを拡張するには、*スケールアップ*と*スケールアウト*の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-114">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="bdba8-115">スケールアップとは、より大規模なサーバー (またはより大きな VM) を使用して、より多くの RAM、Cpu などを使用することです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-115">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="bdba8-116">Scale out は、負荷を処理するためにサーバーを追加することを意味します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-116">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="bdba8-117">スケールアップの問題は、コンピューターのサイズの上限に達することです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-117">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="bdba8-118">それ以外の場合は、スケールアウトする必要があります。ただし、スケールアウトすると、クライアントは別のサーバーにルーティングされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-118">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="bdba8-119">1つのサーバーに接続されているクライアントは、別のサーバーから送信されたメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="bdba8-119">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="bdba8-120">1つの解決策は、*バックプレーン*と呼ばれるコンポーネントを使用して、サーバー間でメッセージを転送することです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-120">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="bdba8-121">バックプレーンが有効になっている場合、各アプリケーションインスタンスはバックプレーンにメッセージを送信し、バックプレーンはそれらを他のアプリケーションインスタンスに転送します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-121">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="bdba8-122">(エレクトロニクスでは、バックプレーンは並列コネクタのグループです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-122">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="bdba8-123">例えとして、SignalR バックプレーンは複数のサーバーを接続します)。</span><span class="sxs-lookup"><span data-stu-id="bdba8-123">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="bdba8-124">現在、SignalR には次の3つの背面があります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-124">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="bdba8-125">**Azure Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="bdba8-125">**Azure Service Bus**.</span></span> <span data-ttu-id="bdba8-126">Service Bus は、疎結合された方法でコンポーネントがメッセージを送信できるようにするメッセージングインフラストラクチャです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-126">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="bdba8-127">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="bdba8-127">**Redis**.</span></span> <span data-ttu-id="bdba8-128">Redis は、メモリ内のキーと値のストアです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-128">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="bdba8-129">Redis は、メッセージを送信するためのパブリッシュ/サブスクライブ ("pub/sub") パターンをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="bdba8-129">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="bdba8-130">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="bdba8-130">**SQL Server**.</span></span> <span data-ttu-id="bdba8-131">SQL Server バックプレーンは、SQL テーブルにメッセージを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="bdba8-131">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="bdba8-132">バックプレーンは、効率的なメッセージングのために Service Broker を使用します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-132">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="bdba8-133">ただし、Service Broker が有効になっていない場合にも機能します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-133">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="bdba8-134">アプリケーションを Azure にデプロイする場合は、 [Azure Redis Cache](https://azure.microsoft.com/services/cache/)を使用した Redis バックプレーンの使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="bdba8-134">If you deploy your application on Azure, consider using the Redis backplane using [Azure Redis Cache](https://azure.microsoft.com/services/cache/).</span></span> <span data-ttu-id="bdba8-135">独自のサーバーファームにデプロイする場合は、SQL Server または Redis 背面を検討してください。</span><span class="sxs-lookup"><span data-stu-id="bdba8-135">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="bdba8-136">次のトピックには、各バックプレーンの手順に関するチュートリアルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bdba8-136">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="bdba8-137">Azure Service Bus による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="bdba8-137">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="bdba8-138">Redis による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="bdba8-138">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="bdba8-139">SQL Server による SignalR スケールアウト</span><span class="sxs-lookup"><span data-stu-id="bdba8-139">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="bdba8-140">実装</span><span class="sxs-lookup"><span data-stu-id="bdba8-140">Implementation</span></span>

<span data-ttu-id="bdba8-141">SignalR では、すべてのメッセージがメッセージバスを介して送信されます。</span><span class="sxs-lookup"><span data-stu-id="bdba8-141">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="bdba8-142">メッセージバスは、パブリッシュ/サブスクライブの抽象化を提供する[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-142">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="bdba8-143">背面は、既定の**IMessageBus**をそのバックプレーン用に設計されたバスに置き換えることによって機能します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-143">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="bdba8-144">たとえば、Redis のメッセージバスは[Redismessagebus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)で、redis [pub/sub](http://redis.io/topics/pubsub)メカニズムを使用してメッセージを送受信します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-144">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="bdba8-145">各サーバーインスタンスは、バスを介してバックプレーンに接続します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-145">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="bdba8-146">メッセージが送信されると、バックプレーンに送られ、バックプレーンがすべてのサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-146">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="bdba8-147">サーバーがバックプレーンからメッセージを取得すると、メッセージはローカルキャッシュに格納されます。</span><span class="sxs-lookup"><span data-stu-id="bdba8-147">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="bdba8-148">サーバーは、ローカルキャッシュからクライアントにメッセージを配信します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-148">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="bdba8-149">クライアント接続ごとに、カーソルを使用して、メッセージストリームの読み取りにおけるクライアントの進行状況が追跡されます。</span><span class="sxs-lookup"><span data-stu-id="bdba8-149">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="bdba8-150">(カーソルはメッセージストリーム内の位置を表します)。クライアントが切断された後に再接続すると、クライアントのカーソル値の後に到着したメッセージをバスに要求します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-150">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="bdba8-151">接続で[長いポーリング](../getting-started/introduction-to-signalr.md#transports)が使用されている場合も同じことが起こります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-151">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="bdba8-152">長いポーリング要求が完了すると、クライアントは新しい接続を開き、カーソルの後に到着したメッセージを要求します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-152">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="bdba8-153">カーソルメカニズムは、再接続時にクライアントが別のサーバーにルーティングされている場合でも機能します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-153">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="bdba8-154">バックプレーンは、すべてのサーバーを認識しており、クライアントが接続しているサーバーには関係ありません。</span><span class="sxs-lookup"><span data-stu-id="bdba8-154">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="bdba8-155">制限事項</span><span class="sxs-lookup"><span data-stu-id="bdba8-155">Limitations</span></span>

<span data-ttu-id="bdba8-156">バックプレーンを使用する場合、最大メッセージスループットは、クライアントが単一のサーバーノードに直接通信する場合よりも低くなります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-156">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="bdba8-157">これは、バックプレーンがすべてのメッセージをすべてのノードに転送するため、バックプレーンがボトルネックになる可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-157">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="bdba8-158">この制限が問題になるかどうかは、アプリケーションによって異なります。</span><span class="sxs-lookup"><span data-stu-id="bdba8-158">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="bdba8-159">たとえば、一般的な SignalR シナリオを次に示します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-159">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="bdba8-160">[サーバーブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)(stock ティッカーなど): 背面は、このシナリオに適しています。これは、サーバーがメッセージの送信速度を制御するためです。</span><span class="sxs-lookup"><span data-stu-id="bdba8-160">[Server broadcast](../getting-started/tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="bdba8-161">[クライアント対クライアント](../getting-started/tutorial-getting-started-with-signalr.md)(チャットなど): このシナリオでは、メッセージの数がクライアントの数に合わせてスケーリングされる場合、バックプレーンはボトルネックになる可能性があります。これは、より多くのクライアントが参加したときにメッセージの割合が増加した場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-161">[Client-to-client](../getting-started/tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="bdba8-162">[高頻度リアル](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)タイム (リアルタイムゲームなど): このシナリオでは、バックプレーンはお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="bdba8-162">[High-frequency realtime](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="bdba8-163">SignalR のスケールアウトのトレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="bdba8-163">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="bdba8-164">背面のトレースを有効にするには、次のセクションを web.config ファイルのルート**構成**要素の下に追加します。</span><span class="sxs-lookup"><span data-stu-id="bdba8-164">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
