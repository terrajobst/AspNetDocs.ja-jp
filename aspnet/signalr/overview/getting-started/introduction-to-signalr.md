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
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431098"
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="7b7cd-103">SignalR 入門</span><span class="sxs-lookup"><span data-stu-id="7b7cd-103">Introduction to SignalR</span></span>

<span data-ttu-id="7b7cd-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="7b7cd-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="7b7cd-105">この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="7b7cd-106">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="7b7cd-106">Questions and comments</span></span>
> 
> <span data-ttu-id="7b7cd-107">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="7b7cd-108">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="7b7cd-109">SignalR とは何か</span><span class="sxs-lookup"><span data-stu-id="7b7cd-109">What is SignalR?</span></span>

<span data-ttu-id="7b7cd-110">ASP.NET SignalR は、リアルタイム Web 機能をアプリケーションに追加するプロセスを簡素化する ASP.NET 開発者向けのライブラリです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="7b7cd-111">リアルタイム Web 機能とは、サーバーがクライアントからの新しいデータ要求を待つのではなく、サーバー コードが接続クライアントに対して利用可能になったコンテンツを瞬時にプッシュできる機能です。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="7b7cd-112">SignalR は、ASP.NET アプリケーションに何らかの「リアルタイム」Web 機能を追加するために使用することができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="7b7cd-113">よくチャットが例として使用されますが、もっと多くのことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="7b7cd-114">ユーザーが新しいデータを表示するために web ページを更新するたびに、またはページが[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装して新しいデータを取得すると、SignalR を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="7b7cd-115">サンプルとしては、ダッシュ ボード アプリケーションや監視アプリケーション、コラボレーション アプリケーション (ドキュメントの同時編集など)、ジョブの進行状況の更新プログラム、およびリアルタイム フォームが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="7b7cd-116">SignalR はリアルタイム ゲームなど、サーバーから高頻度で更新を必要とするまったく新しいタイプの Web アプリケーションを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="7b7cd-117">SignalR は、サーバー側の .NET コードからクライアント ブラウザー (およびその他のクライアント プラットフォーム) に JavaScript 関数を呼び出す、サーバーからクライアントへのリモート プロシージャ コール (RPC) を作成するための単純な API を提供します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="7b7cd-118">SignalR には、接続管理 (イベントの接続や切断など) やグループ接続のための API も含まれます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="7b7cd-120">SignalR では、自動的に接続管理を処理し、チャット ルームのように、接続されているすべてのクライアントへのメッセージを同時に配信できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="7b7cd-121">また、特定のクライアントにメッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="7b7cd-122">クライアントとサーバー間の接続は、通信ごとに再確立される従来の HTTP 接続とは異なり永続的です。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="7b7cd-123">SignalR は「サーバー プッシュ」機能をサポートしています。この機能では、現在 Web において一般的な要求 - 応答モデルではなく、リモート プロシージャ コール (RPC) を使用して、サーバー コードによってブラウザー内のクライアント コードを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="7b7cd-124">SignalR アプリケーションは、組み込みの、サードパーティのスケールアウトプロバイダーを使用して、何千ものクライアントにスケールアウトできます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="7b7cd-125">組み込みプロバイダーには次のものがあります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-125">Built-in providers include:</span></span>
* [<span data-ttu-id="7b7cd-126">Service Bus</span><span class="sxs-lookup"><span data-stu-id="7b7cd-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="7b7cd-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7b7cd-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="7b7cd-128">Redis</span><span class="sxs-lookup"><span data-stu-id="7b7cd-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="7b7cd-129">サードパーティプロバイダーには次のものがあります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-129">Third-party providers include:</span></span>
* <span data-ttu-id="7b7cd-130">[Ncache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="7b7cd-131">SignalR はオープンソースであり、 [GitHub](https://github.com/signalr)を介してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="7b7cd-132">SignalR と WebSocket</span><span class="sxs-lookup"><span data-stu-id="7b7cd-132">SignalR and WebSocket</span></span>

<span data-ttu-id="7b7cd-133">SignalR では、使用可能な場合は新しい WebSocket トランスポートを使用し、必要に応じて、古いトランスポートにフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="7b7cd-134">WebSocket を直接使用してアプリを作成することはできますが、SignalR を使用するメリットは、実装する必要のある他の機能の多くが既に作成されているという点です。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="7b7cd-135">これにより、最も重要な事ととして、古いクライアントのために個別のコード パスを作成することなく、WebSocket を活用できるようにアプリをコーディングすることができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="7b7cd-136">SignalR は基本トランスポートの変更をサポートするために更新され、異なるバージョンの WebSocket でもアプリケーションにおいて一貫したインターフェイスが提供されるため、SignalR は WebSocket の更新に関する心配からユーザーを解放します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="7b7cd-137">トランスポートとフォールバック</span><span class="sxs-lookup"><span data-stu-id="7b7cd-137">Transports and fallbacks</span></span>

<span data-ttu-id="7b7cd-138">SignalR は、クライアントとサーバー間のリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="7b7cd-139">SignalR 接続は HTTP として起動し、WebSocket 接続が可能な場合は WebSocket 接続となります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-139">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="7b7cd-140">WebSocket は、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の全二重通信など) が備わっているため、SignalR の理想的なトランスポートですが、細かい要件があります。WebSocket では、Windows Server 2012 または Windows 8、および .NET Framework 4.5 を使用するサーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-140">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="7b7cd-141">これらの要件が満たされない場合、SignalR は、接続するために他のトランスポートの使用を試みます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-141">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="7b7cd-142">HTML 5 トランスポート</span><span class="sxs-lookup"><span data-stu-id="7b7cd-142">HTML 5 transports</span></span>

<span data-ttu-id="7b7cd-143">これらのトランスポートは、 [HTML 5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-143">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="7b7cd-144">クライアントのブラウザーが HTML 5 標準をサポートしていない場合は、古いトランスポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-144">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="7b7cd-145">**Websocket** (サーバーとブラウザーの両方が websocket をサポートできることを示している場合)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-145">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="7b7cd-146">WebSocket は、クライアントとサーバー間の通信における真に永続的な双方向接続を確立するためのトランスポートです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-146">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="7b7cd-147">ただし、WebSocket には細かい要件もあります。WebSocket は Microsoft Internet Explorer、Google Chrome、Mozilla Firefox の最新のバージョンでのみ完全にサポートされ、Opera や Safari などの他のブラウザーでは部分的にしか実装されません。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-147">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="7b7cd-148">**サーバー送信イベント**。 EventSource とも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、これは基本的に Internet Explorer を除くすべてのブラウザーです)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-148">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="7b7cd-149">コメットのトランスポート</span><span class="sxs-lookup"><span data-stu-id="7b7cd-149">Comet transports</span></span>

<span data-ttu-id="7b7cd-150">次のトランスポートは、[コメット](http://en.wikipedia.org/wiki/Comet_(programming))web アプリケーションモデルに基づいています。このモデルでは、ブラウザーまたは他のクライアントが長い形式の HTTP 要求を保持しています。これは、サーバーがクライアントにデータをプッシュするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-150">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="7b7cd-151">**無期限フレーム**(Internet Explorer の場合のみ)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-151">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="7b7cd-152">Forever Frame は、サーバー上のエンドポイントへの要求が完了しない非表示の IFrame を作成します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-152">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="7b7cd-153">サーバーは、すぐに実行されるスクリプトを継続的にクライアントに送信し、サーバーからクライアントへの一方向のリアルタイム接続を提供します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-153">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="7b7cd-154">クライアントからサーバーへの接続は、サーバーからクライアントとは異なる接続を使用し、標準の HTTP 要求のように、送信する必要のあるデータがあるたびに新しい接続が作成されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-154">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="7b7cd-155">**Ajax 長時間ポーリング**。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-155">**Ajax long polling**.</span></span> <span data-ttu-id="7b7cd-156">Long Polling では永続的な接続は作成されませんが、サーバーが応答を完了するまで開いたままの要求でサーバーをポーリングします。接続が閉じられたら即座に新しい接続が要求されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-156">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="7b7cd-157">これにより、接続がリセットされるまでの待機時間が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-157">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="7b7cd-158">構成でサポートされているトランスポートの詳細については、「[サポートされ](supported-platforms.md)ているプラットフォーム」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-158">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="7b7cd-159">トランスポート選択のプロセス</span><span class="sxs-lookup"><span data-stu-id="7b7cd-159">Transport selection process</span></span>

<span data-ttu-id="7b7cd-160">SignalR が使用するトランスポートを決定する手順を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-160">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="7b7cd-161">ブラウザーが Internet Explorer 8 またはそれ以前の場合は、Long Polling が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-161">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="7b7cd-162">JSONP が構成されている場合 (つまり、接続が開始されたときに `jsonp` パラメーターが `true` に設定されている場合)、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-162">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="7b7cd-163">クロス ドメイン接続が確立されている場合 (つまり、SignalR エンドポイントが、ホスティング ページと同じドメインにない)、次の条件が満たされた場合に WebSocket が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-163">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="7b7cd-164">クライアントが CORS (クロス オリジン リソース共有) をサポートしている。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-164">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="7b7cd-165">CORS をサポートするクライアントの詳細については、「 [cors at caniuse.com](http://www.caniuse.com/CORS)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-165">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="7b7cd-166">クライアントが WebSocket をサポートしている。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-166">The client supports WebSocket</span></span>
   - <span data-ttu-id="7b7cd-167">サーバーが WebSocket をサポートしている。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-167">The server supports WebSocket</span></span>

     <span data-ttu-id="7b7cd-168">これらの条件のいずれかが満たされていない場合は、Long Polling が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-168">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="7b7cd-169">ドメイン間接続の詳細については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-169">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="7b7cd-170">JSONP が設定されておらず、ドメイン間接続でない場合は WebSocket が使用されます (クライアントとサーバーの両方がサポートしている場合)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-170">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="7b7cd-171">クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合は Server Sent Events が使用されます (利用可能に場合)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-171">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="7b7cd-172">サーバー送信イベントが使用できない場合、永続的なフレームが試行されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-172">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="7b7cd-173">永続的なフレームが失敗した場合は、長いポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-173">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="7b7cd-174">トランスポートの監視</span><span class="sxs-lookup"><span data-stu-id="7b7cd-174">Monitoring transports</span></span>

<span data-ttu-id="7b7cd-175">ハブでログを有効にし、ブラウザーでコンソール ウィンドウを開くことによって、アプリケーションで使用されているトランスポートを特定できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-175">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="7b7cd-176">ブラウザーでハブのイベントのログ記録を有効にするには、クライアントアプリケーションに次のコマンドを追加します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-176">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="7b7cd-177">Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-177">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer のコンソール](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="7b7cd-179">Chrome で、Ctrl キーと Shift キーを押しながら J キーを押してコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-179">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome のコンソール](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="7b7cd-181">コンソールが開いた状態で、ログが有効な場合は、SignalR で利用されているトランスポートを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-181">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![WebSocket トランスポートが表示されている Internet Explorer のコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="7b7cd-183">トランスポートの指定</span><span class="sxs-lookup"><span data-stu-id="7b7cd-183">Specifying a transport</span></span>

<span data-ttu-id="7b7cd-184">トランスポートのネゴシエートには一定の時間を要し、クライアントとサーバーの一定量のリソースを使用します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-184">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="7b7cd-185">クライアントの機能が分かっている場合は、クライアント接続が開始された時点でトランスポートを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-185">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="7b7cd-186">次のコード スニペットでは、クラインが他のプロトコルをサポートしていないことが分かっている場合にも使用される、Ajax Long Polling のトランスポートを使用して接続を開始する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-186">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="7b7cd-187">クライアントが特定のトランスポートを順番に試行するようにする場合は、フォールバック順序を指定できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-187">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="7b7cd-188">次のコード スニペットは、WebSocket を試し、失敗した場合、Long Polling に直接移行する例を示します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-188">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="7b7cd-189">トランスポートを指定するための文字列定数は、次のように定義されています。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-189">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="7b7cd-190">接続とハブ</span><span class="sxs-lookup"><span data-stu-id="7b7cd-190">Connections and Hubs</span></span>

<span data-ttu-id="7b7cd-191">SignalR API には、クライアントとサーバー間の通信用に、永続的な接続とハブの2つのモデルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-191">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="7b7cd-192">接続は、単一受信者メッセージ、グループ化メッセージ、またはブロードキャスト メッセージを送信するための単純なエンドポイントを表します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-192">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="7b7cd-193">固定接続 API (PersistentConnection クラスによって .NET コードで表される) は、SignalR が公開している低レベルの通信プロトコルへの直接アクセスを開発者に提供します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-193">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="7b7cd-194">接続の通信モデルは、Windows Communication Foundation などの接続に基づく API を使用したことのある開発者にとって使いやすいものです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-194">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="7b7cd-195">ハブは、クライアントとサーバーが相互に直接メソッドを呼び出すことができるようにする接続 API に基づいて構築されたより高度なパイプラインです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-195">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="7b7cd-196">SignalR は、マシンの境界でのディスパッチを魔法のように行い、クライアントがローカルのメソッドのように簡単にサーバーでメソッドを呼び出せるようにします (またはその逆)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-196">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="7b7cd-197">ハブ通信モデルは、.NET Remoting などのリモート呼び出し API を使用したことのある開発者にとって使いやすいものです。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-197">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="7b7cd-198">また、ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡すことができ、モデルのバインディングが可能になります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-198">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="7b7cd-199">アーキテクチャの図</span><span class="sxs-lookup"><span data-stu-id="7b7cd-199">Architecture diagram</span></span>

<span data-ttu-id="7b7cd-200">次の図は、ハブ、永続的な接続、およびトランスポートに使用される基になるテクノロジの関係を示しています。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-200">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![Api、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="7b7cd-202">ハブのしくみ</span><span class="sxs-lookup"><span data-stu-id="7b7cd-202">How Hubs work</span></span>

<span data-ttu-id="7b7cd-203">サーバー側コードでは、クライアントでメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むパケットがアクティブなトランスポート経由で送信されます (オブジェクトがメソッド パラメーターとして送信される場合、JSON を使用してシリアル化されます)。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-203">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="7b7cd-204">次にクライアントは、メソッド名をクライアント側のコードで定義されているメソッドと一致させます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-204">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="7b7cd-205">一致するものがある場合は、逆シリアル化されたパラメーターデータを使用してクライアントメソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-205">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="7b7cd-206">メソッドの呼び出しは、Fiddler などのツールを使用して監視でき[ます。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="7b7cd-206">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="7b7cd-207">次のイメージは、Fiddler の [ログ] ウィンドウで、SignalR サーバーから Web ブラウザー クライアントに送信されたメソッドの呼び出しを示します。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-207">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="7b7cd-208">メソッド呼び出しは `MoveShapeHub`と呼ばれるハブから送信され、呼び出されるメソッドは `updateShape`と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-208">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR トラフィックを示す Fiddler ログの表示](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="7b7cd-210">この例では、ハブ名は `H` パラメーターで識別されます。メソッド名は `M` パラメーターで識別され、メソッドに送信されるデータは `A` パラメーターで識別されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-210">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="7b7cd-211">このメッセージを生成したアプリケーションは、[高頻度のリアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-211">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="7b7cd-212">通信モデルの選択</span><span class="sxs-lookup"><span data-stu-id="7b7cd-212">Choosing a communication model</span></span>

<span data-ttu-id="7b7cd-213">ほとんどのアプリケーションでは、ハブ API を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-213">Most applications should use the Hubs API.</span></span> <span data-ttu-id="7b7cd-214">接続 API は次の状況で使用できます。</span><span class="sxs-lookup"><span data-stu-id="7b7cd-214">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="7b7cd-215">実際の送信メッセージの形式を指定する必要がある</span><span class="sxs-lookup"><span data-stu-id="7b7cd-215">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="7b7cd-216">開発者が、リモート呼び出しモデルではなく、メッセージおよびディスパッチ モデルを利用する事を推奨している</span><span class="sxs-lookup"><span data-stu-id="7b7cd-216">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="7b7cd-217">メッセージングモデルを使用する既存のアプリケーションが SignalR を使用するように移植されている</span><span class="sxs-lookup"><span data-stu-id="7b7cd-217">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
