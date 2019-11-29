---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR | の概要Microsoft Docs
author: bradygaster
description: この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 11b494b4839c646b018098c76a8a9ae0a2169757
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600490"
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="888b2-103">SignalR 入門</span><span class="sxs-lookup"><span data-stu-id="888b2-103">Introduction to SignalR</span></span>

<span data-ttu-id="888b2-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="888b2-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="888b2-105">この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="888b2-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="888b2-106">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="888b2-106">Questions and comments</span></span>
> 
> <span data-ttu-id="888b2-107">このチュートリアルの気に入った点と、ページの下部にあるコメントで改善できることについて、フィードバックをお寄せください。</span><span class="sxs-lookup"><span data-stu-id="888b2-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="888b2-108">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="888b2-109">SignalR とは</span><span class="sxs-lookup"><span data-stu-id="888b2-109">What is SignalR?</span></span>

<span data-ttu-id="888b2-110">ASP.NET SignalR は、リアルタイム web 機能をアプリケーションに追加するプロセスを簡略化する ASP.NET 開発者向けのライブラリです。</span><span class="sxs-lookup"><span data-stu-id="888b2-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="888b2-111">リアルタイム web 機能を使用すると、クライアントが新しいデータを要求するのをサーバーが待機するのではなく、接続されているクライアントにコンテンツをプッシュすることができるようになります。</span><span class="sxs-lookup"><span data-stu-id="888b2-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="888b2-112">SignalR を使用すると、ASP.NET アプリケーションに任意の種類の "リアルタイム" web 機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="888b2-113">多くの場合、チャットは例として使用されますが、さらに多くのことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="888b2-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="888b2-114">ユーザーが新しいデータを表示するために web ページを更新するたびに、またはページが[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装して新しいデータを取得すると、SignalR を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="888b2-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="888b2-115">例としては、ダッシュボードとアプリケーションの監視、コラボレーションアプリケーション (ドキュメントの同時編集など)、ジョブの進行状況の更新、リアルタイムフォームなどがあります。</span><span class="sxs-lookup"><span data-stu-id="888b2-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="888b2-116">また、SignalR は、リアルタイムゲームなど、サーバーからの高頻度の更新を必要とする、まったく新しい種類の web アプリケーションを有効にします。</span><span class="sxs-lookup"><span data-stu-id="888b2-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="888b2-117">SignalR は、サーバーからクライアントへのリモートプロシージャコール (RPC) を作成するためのシンプルな API を提供します。この API は、クライアントブラウザー (およびその他のクライアントプラットフォーム) で、サーバー側の .NET コードから JavaScript 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="888b2-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="888b2-118">SignalR には、接続管理用の API (接続イベントや切断イベントなど) や、接続のグループ化も含まれます。</span><span class="sxs-lookup"><span data-stu-id="888b2-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="888b2-120">SignalR は、接続管理を自動的に処理し、チャットルームなど、接続されているすべてのクライアントに同時にメッセージをブロードキャストすることができます。</span><span class="sxs-lookup"><span data-stu-id="888b2-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="888b2-121">また、特定のクライアントにメッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="888b2-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="888b2-122">クライアントとサーバー間の接続は永続的です。これは、通信ごとに再確立される従来の HTTP 接続とは異なります。</span><span class="sxs-lookup"><span data-stu-id="888b2-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="888b2-123">SignalR では、"サーバープッシュ" 機能がサポートされています。この機能では、現在、web 上で共通の要求-応答モデルではなく、リモートプロシージャコール (RPC) を使用して、サーバーコードからブラウザーでクライアントコードを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="888b2-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="888b2-124">SignalR アプリケーションは、Service Bus、SQL Server または[Redis](http://redis.io)を使用して、数千のクライアントにスケールアウトできます。</span><span class="sxs-lookup"><span data-stu-id="888b2-124">SignalR applications can scale out to thousands of clients using Service Bus, SQL Server or [Redis](http://redis.io).</span></span>

<span data-ttu-id="888b2-125">SignalR はオープンソースであり、 [GitHub](https://github.com/signalr)を介してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="888b2-125">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="888b2-126">SignalR と WebSocket</span><span class="sxs-lookup"><span data-stu-id="888b2-126">SignalR and WebSocket</span></span>

<span data-ttu-id="888b2-127">SignalR は、使用可能な場合は新しい WebSocket トランスポートを使用し、必要に応じて古いトランスポートにフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="888b2-127">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="888b2-128">確かに WebSocket を直接使用してアプリを記述することもできますが、SignalR を使用すると、実装する必要のある多くの追加機能が既に実行されていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="888b2-128">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="888b2-129">最も重要なことは、これは、古いクライアント用に別のコードパスを作成することを心配することなく、WebSocket を利用するようにアプリをコーディングできることを意味します。</span><span class="sxs-lookup"><span data-stu-id="888b2-129">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="888b2-130">また、SignalR は、基になるトランスポートの変更をサポートするために SignalR が更新されるため、WebSocket のバージョン間の一貫性のあるインターフェイスをアプリケーションに提供するため、WebSocket の更新について心配する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="888b2-130">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="888b2-131">トランスポートとフォールバック</span><span class="sxs-lookup"><span data-stu-id="888b2-131">Transports and fallbacks</span></span>

<span data-ttu-id="888b2-132">SignalR は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。</span><span class="sxs-lookup"><span data-stu-id="888b2-132">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="888b2-133">SignalR 接続は HTTP として起動し、使用可能な場合は WebSocket 接続に昇格します。</span><span class="sxs-lookup"><span data-stu-id="888b2-133">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="888b2-134">WebSocket は、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の完全な双方向通信など) を備えているため、SignalR に最適なトランスポートですが、最も厳しい要件: WebSocket では、サーバーが Windows Server 2012 または Windows 8 を使用していること、および .NET Framework 4.5 が必要です。</span><span class="sxs-lookup"><span data-stu-id="888b2-134">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="888b2-135">これらの要件が満たされていない場合、SignalR は他のトランスポートを使用して接続を試行します。</span><span class="sxs-lookup"><span data-stu-id="888b2-135">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="888b2-136">HTML 5 トランスポート</span><span class="sxs-lookup"><span data-stu-id="888b2-136">HTML 5 transports</span></span>

<span data-ttu-id="888b2-137">これらのトランスポートは、 [HTML 5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。</span><span class="sxs-lookup"><span data-stu-id="888b2-137">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="888b2-138">クライアントのブラウザーが HTML 5 標準をサポートしていない場合は、古いトランスポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-138">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="888b2-139">**Websocket** (サーバーとブラウザーの両方が websocket をサポートできることを示している場合)。</span><span class="sxs-lookup"><span data-stu-id="888b2-139">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="888b2-140">WebSocket は、クライアントとサーバーの間に真の永続的な双方向の接続を確立する唯一のトランスポートです。</span><span class="sxs-lookup"><span data-stu-id="888b2-140">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="888b2-141">ただし、WebSocket には、最も厳しい要件もあります。これは、最新バージョンの Microsoft Internet Explorer、Google Chrome、Mozilla Firefox でのみ完全にサポートされており、Opera や Safari などの他のブラウザーでは部分的な実装のみがあります。</span><span class="sxs-lookup"><span data-stu-id="888b2-141">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="888b2-142">**サーバー送信イベント**。 EventSource とも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、これは基本的に Internet Explorer を除くすべてのブラウザーです)。</span><span class="sxs-lookup"><span data-stu-id="888b2-142">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="888b2-143">コメットのトランスポート</span><span class="sxs-lookup"><span data-stu-id="888b2-143">Comet transports</span></span>

<span data-ttu-id="888b2-144">次のトランスポートは、[コメット](http://en.wikipedia.org/wiki/Comet_(programming))web アプリケーションモデルに基づいています。このモデルでは、ブラウザーまたは他のクライアントが長い形式の HTTP 要求を保持しています。これは、サーバーがクライアントにデータをプッシュするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-144">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="888b2-145">**無期限フレーム**(Internet Explorer の場合のみ)。</span><span class="sxs-lookup"><span data-stu-id="888b2-145">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="888b2-146">永続的なフレームでは、未表示の IFrame が作成されます。これにより、サーバー上の完了していないエンドポイントへの要求が行われます。</span><span class="sxs-lookup"><span data-stu-id="888b2-146">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="888b2-147">サーバーは、直ちに実行されるクライアントに対してスクリプトを継続的に送信し、サーバーからクライアントへの一方向のリアルタイム接続を提供します。</span><span class="sxs-lookup"><span data-stu-id="888b2-147">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="888b2-148">クライアントからサーバーへの接続では、サーバーとクライアント間の接続を別々に使用します。標準の HTTP 要求と同様に、送信する必要があるデータごとに新しい接続が作成されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-148">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="888b2-149">**Ajax 長時間ポーリング**。</span><span class="sxs-lookup"><span data-stu-id="888b2-149">**Ajax long polling**.</span></span> <span data-ttu-id="888b2-150">長いポーリングでは永続的な接続は作成されませんが、サーバーが応答するまで開いたままになっている要求を使用してサーバーをポーリングし、その時点で接続が閉じられ、新しい接続が直ちに要求されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-150">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="888b2-151">これにより、接続がリセットされるまでの待機時間が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="888b2-151">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="888b2-152">構成でサポートされているトランスポートの詳細については、「[サポートされ](supported-platforms.md)ているプラットフォーム」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="888b2-152">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="888b2-153">トランスポートの選択プロセス</span><span class="sxs-lookup"><span data-stu-id="888b2-153">Transport selection process</span></span>

<span data-ttu-id="888b2-154">次の一覧は、SignalR が使用するトランスポートを決定するために使用する手順を示しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-154">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="888b2-155">ブラウザーが Internet Explorer 8 以前である場合は、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-155">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="888b2-156">JSONP が構成されている場合 (つまり、接続が開始されたときに `jsonp` パラメーターが `true` に設定されている場合)、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-156">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="888b2-157">クロスドメイン接続が行われている場合 (つまり、SignalR エンドポイントがホストページと同じドメインにない場合)、次の条件を満たす場合に WebSocket が使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-157">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="888b2-158">クライアントは CORS (クロスオリジンリソース共有) をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="888b2-158">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="888b2-159">CORS をサポートするクライアントの詳細については、「 [cors at caniuse.com](http://www.caniuse.com/CORS)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="888b2-159">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="888b2-160">クライアントが WebSocket をサポートする</span><span class="sxs-lookup"><span data-stu-id="888b2-160">The client supports WebSocket</span></span>
   - <span data-ttu-id="888b2-161">サーバーは WebSocket をサポートします。</span><span class="sxs-lookup"><span data-stu-id="888b2-161">The server supports WebSocket</span></span>

     <span data-ttu-id="888b2-162">これらの条件のいずれかが満たされていない場合は、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-162">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="888b2-163">ドメイン間接続の詳細については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="888b2-163">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="888b2-164">JSONP が構成されておらず、接続がドメインを越えていない場合は、クライアントとサーバーの両方でサポートされている場合、WebSocket が使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-164">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="888b2-165">クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合は、サーバーの送信イベントが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-165">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="888b2-166">サーバー送信イベントが使用できない場合、永続的なフレームが試行されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-166">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="888b2-167">永続的なフレームが失敗した場合は、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-167">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="888b2-168">トランスポートの監視</span><span class="sxs-lookup"><span data-stu-id="888b2-168">Monitoring transports</span></span>

<span data-ttu-id="888b2-169">ハブでログ記録を有効にし、ブラウザーでコンソールウィンドウを開くことによって、アプリケーションで使用されているトランスポートを特定できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-169">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="888b2-170">ブラウザーでハブのイベントのログ記録を有効にするには、クライアントアプリケーションに次のコマンドを追加します。</span><span class="sxs-lookup"><span data-stu-id="888b2-170">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="888b2-171">Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="888b2-171">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer のコンソール](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="888b2-173">Chrome で、Ctrl キーと Shift キーを押しながら J キーを押してコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="888b2-173">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome のコンソール](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="888b2-175">コンソールを開いてログを有効にすると、SignalR によって使用されているトランスポートを確認できるようになります。</span><span class="sxs-lookup"><span data-stu-id="888b2-175">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![WebSocket トランスポートが表示されている Internet Explorer のコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="888b2-177">トランスポートの指定</span><span class="sxs-lookup"><span data-stu-id="888b2-177">Specifying a transport</span></span>

<span data-ttu-id="888b2-178">トランスポートをネゴシエートするには、一定の時間とクライアント/サーバーのリソースを必要とします。</span><span class="sxs-lookup"><span data-stu-id="888b2-178">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="888b2-179">クライアント機能が既知の場合は、クライアント接続が開始されたときにトランスポートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-179">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="888b2-180">次のコードスニペットは、クライアントが他のプロトコルをサポートしていないことが判明した場合に使用されるように、Ajax の長いポーリングトランスポートを使用して接続を開始する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-180">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="888b2-181">クライアントが特定のトランスポートを順番に試行するようにする場合は、フォールバックの順序を指定できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-181">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="888b2-182">次のコードスニペットは、WebSocket を試行し、それを失敗させて、長いポーリングに直接移動する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-182">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="888b2-183">トランスポートを指定するための文字列定数は、次のように定義されています。</span><span class="sxs-lookup"><span data-stu-id="888b2-183">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="888b2-184">接続とハブ</span><span class="sxs-lookup"><span data-stu-id="888b2-184">Connections and Hubs</span></span>

<span data-ttu-id="888b2-185">SignalR API には、クライアントとサーバー間の通信用に、永続的な接続とハブの2つのモデルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="888b2-185">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="888b2-186">接続は、単一受信者、グループ化、またはブロードキャストメッセージを送信するための単純なエンドポイントを表します。</span><span class="sxs-lookup"><span data-stu-id="888b2-186">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="888b2-187">永続接続 API (.NET コードでは PersistentConnection クラスによって表されます) を使用すると、開発者は SignalR が公開する低レベル通信プロトコルに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="888b2-187">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="888b2-188">接続の通信モデルを使用すると、Windows Communication Foundation などの接続ベースの Api を使用している開発者にとってはなじみがありません。</span><span class="sxs-lookup"><span data-stu-id="888b2-188">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="888b2-189">ハブは、接続 API に基づいて構築されたより高度なパイプラインで、クライアントとサーバーが互いにメソッドを直接呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="888b2-189">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="888b2-190">SignalR はマジックでの場合と同様にコンピューターの境界を越えたディスパッチを処理し、クライアントがローカルメソッドと同様に簡単にサーバー上のメソッドを呼び出すことができるようにします。また、その逆も可能です。</span><span class="sxs-lookup"><span data-stu-id="888b2-190">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="888b2-191">ハブ通信モデルを使用すると、.NET リモート処理などのリモート呼び出し Api を使用している開発者にとってなじみがあります。</span><span class="sxs-lookup"><span data-stu-id="888b2-191">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="888b2-192">ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡して、モデルバインドを有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="888b2-192">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="888b2-193">アーキテクチャの図</span><span class="sxs-lookup"><span data-stu-id="888b2-193">Architecture diagram</span></span>

<span data-ttu-id="888b2-194">次の図は、ハブ、永続的な接続、およびトランスポートに使用される基になるテクノロジの関係を示しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-194">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![Api、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="888b2-196">ハブのしくみ</span><span class="sxs-lookup"><span data-stu-id="888b2-196">How Hubs work</span></span>

<span data-ttu-id="888b2-197">サーバー側のコードがクライアントでメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むアクティブなトランスポート全体にパケットが送信されます (オブジェクトがメソッドパラメーターとして送信された場合は、JSON を使用してシリアル化されます)。</span><span class="sxs-lookup"><span data-stu-id="888b2-197">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="888b2-198">次に、クライアントは、メソッド名をクライアント側コードで定義されているメソッドと照合します。</span><span class="sxs-lookup"><span data-stu-id="888b2-198">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="888b2-199">一致するものがある場合は、逆シリアル化されたパラメーターデータを使用してクライアントメソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-199">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="888b2-200">メソッドの呼び出しは、Fiddler などのツールを使用して監視でき[ます。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="888b2-200">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="888b2-201">次の図は、Fiddler の [ログ] ウィンドウで SignalR サーバーから web ブラウザークライアントに送信されるメソッド呼び出しを示しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-201">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="888b2-202">メソッド呼び出しは `MoveShapeHub`と呼ばれるハブから送信され、呼び出されるメソッドは `updateShape`と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="888b2-202">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR トラフィックを示す Fiddler ログの表示](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="888b2-204">この例では、ハブ名は `H` パラメーターで識別されます。メソッド名は `M` パラメーターで識別され、メソッドに送信されるデータは `A` パラメーターで識別されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-204">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="888b2-205">このメッセージを生成したアプリケーションは、[高頻度のリアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。</span><span class="sxs-lookup"><span data-stu-id="888b2-205">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="888b2-206">通信モデルの選択</span><span class="sxs-lookup"><span data-stu-id="888b2-206">Choosing a communication model</span></span>

<span data-ttu-id="888b2-207">ほとんどのアプリケーションでは、ハブ API を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="888b2-207">Most applications should use the Hubs API.</span></span> <span data-ttu-id="888b2-208">Connections API は、次のような状況で使用できます。</span><span class="sxs-lookup"><span data-stu-id="888b2-208">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="888b2-209">実際に送信されるメッセージの形式を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="888b2-209">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="888b2-210">開発者は、リモート呼び出しモデルではなく、メッセージングとディスパッチモデルを使用することを推奨しています。</span><span class="sxs-lookup"><span data-stu-id="888b2-210">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="888b2-211">メッセージングモデルを使用する既存のアプリケーションは、SignalR を使用するように移植されています。</span><span class="sxs-lookup"><span data-stu-id="888b2-211">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
