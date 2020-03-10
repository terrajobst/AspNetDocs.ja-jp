---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR Tracing の有効化 |Microsoft Docs
author: bradygaster
description: このドキュメントでは、SignalR サーバーとクライアントのトレースを有効にして構成する方法について説明します。 トレースを使用すると、イベントに関する診断情報を表示できます...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467440"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="26825-104">SignalR トレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="26825-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="26825-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="26825-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="26825-106">このドキュメントでは、SignalR サーバーとクライアントのトレースを有効にして構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="26825-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="26825-107">トレースを使用すると、SignalR アプリケーションのイベントに関する診断情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="26825-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="26825-108">このトピックは、最初は、パトリック Fletcher によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="26825-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="26825-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="26825-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="26825-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="26825-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="26825-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="26825-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="26825-112">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="26825-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="26825-113">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="26825-113">Questions and comments</span></span>
>
> <span data-ttu-id="26825-114">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="26825-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="26825-115">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="26825-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="26825-116">トレースを有効にすると、SignalR アプリケーションによってイベントのログエントリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="26825-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="26825-117">クライアントとサーバーの両方からイベントをログに記録できます。</span><span class="sxs-lookup"><span data-stu-id="26825-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="26825-118">サーバー上のトレースでは、接続、スケールアウトプロバイダー、およびメッセージバスイベントがログに記録されます。</span><span class="sxs-lookup"><span data-stu-id="26825-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="26825-119">クライアントでのトレースでは、接続イベントがログに記録されます。</span><span class="sxs-lookup"><span data-stu-id="26825-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="26825-120">SignalR 2.1 以降では、クライアントのトレースによってハブ呼び出しメッセージの完全な内容がログに記録されます。</span><span class="sxs-lookup"><span data-stu-id="26825-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="26825-121">内容</span><span class="sxs-lookup"><span data-stu-id="26825-121">Contents</span></span>

- [<span data-ttu-id="26825-122">サーバーでトレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="26825-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="26825-123">サーバーイベントをテキストファイルに記録する</span><span class="sxs-lookup"><span data-stu-id="26825-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="26825-124">イベントログへのサーバーイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="26825-125">.NET クライアントでのトレースの有効化 (Windows デスクトップアプリ)</span><span class="sxs-lookup"><span data-stu-id="26825-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="26825-126">コンソールへのデスクトップクライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="26825-127">デスクトップクライアントのイベントをテキストファイルに記録する</span><span class="sxs-lookup"><span data-stu-id="26825-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="26825-128">Windows Phone 8 クライアントでトレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="26825-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="26825-129">UI への Windows Phone クライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="26825-130">デバッグコンソールへの Windows Phone クライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="26825-131">JavaScript クライアントでのトレースの有効化</span><span class="sxs-lookup"><span data-stu-id="26825-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="26825-132">サーバーでトレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="26825-132">Enabling tracing on the server</span></span>

<span data-ttu-id="26825-133">アプリケーションの構成ファイル内のサーバーでトレースを有効にします (プロジェクトの種類に応じて App.config または web.config のいずれか)。ログに記録するイベントのカテゴリを指定します。</span><span class="sxs-lookup"><span data-stu-id="26825-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="26825-134">構成ファイルでは、 [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)の実装を使用して、イベントをテキストファイル、Windows イベントログ、またはカスタムログに記録するかどうかも指定します。</span><span class="sxs-lookup"><span data-stu-id="26825-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="26825-135">サーバーイベントカテゴリには、次のような種類のメッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="26825-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="26825-136">source</span><span class="sxs-lookup"><span data-stu-id="26825-136">Source</span></span> | <span data-ttu-id="26825-137">メッセージ</span><span class="sxs-lookup"><span data-stu-id="26825-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="26825-138">SignalR</span><span class="sxs-lookup"><span data-stu-id="26825-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="26825-139">SQL メッセージバスのスケールアウトプロバイダーのセットアップ、データベース操作、エラー、およびタイムアウトイベント</span><span class="sxs-lookup"><span data-stu-id="26825-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="26825-140">SignalR. ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="26825-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="26825-141">Service bus スケールアウトプロバイダーのトピックの作成とサブスクリプション、エラー、およびメッセージングイベント</span><span class="sxs-lookup"><span data-stu-id="26825-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="26825-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="26825-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="26825-143">Redis スケールアウトプロバイダーの接続、切断、およびエラーイベント</span><span class="sxs-lookup"><span data-stu-id="26825-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="26825-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="26825-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="26825-145">スケールアウトメッセージングイベント</span><span class="sxs-lookup"><span data-stu-id="26825-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="26825-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="26825-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="26825-147">WebSocket トランスポート接続、切断、メッセージング、およびエラーイベント</span><span class="sxs-lookup"><span data-stu-id="26825-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="26825-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="26825-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="26825-149">Server送信イベントトランスポート接続、切断、メッセージング、およびエラーイベント</span><span class="sxs-lookup"><span data-stu-id="26825-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="26825-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="26825-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="26825-151">事前にフレーム転送接続、切断、メッセージング、およびエラーイベントを送信する</span><span class="sxs-lookup"><span data-stu-id="26825-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="26825-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="26825-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="26825-153">LongPolling トランスポート接続、切断、メッセージング、およびエラーイベント</span><span class="sxs-lookup"><span data-stu-id="26825-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="26825-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="26825-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="26825-155">Transport 接続、切断、および keepalive イベント</span><span class="sxs-lookup"><span data-stu-id="26825-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="26825-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="26825-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="26825-157">ハブ検出イベント</span><span class="sxs-lookup"><span data-stu-id="26825-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="26825-158">サーバーイベントをテキストファイルに記録する</span><span class="sxs-lookup"><span data-stu-id="26825-158">Logging server events to text files</span></span>

<span data-ttu-id="26825-159">次のコードは、イベントの各カテゴリのトレースを有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="26825-160">このサンプルでは、イベントをテキストファイルに記録するようにアプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="26825-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="26825-161">**トレースを有効にするための XML サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="26825-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="26825-162">上記のコードでは、`SignalRSwitch` エントリは、指定されたログに送信されるイベントに使用される[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx)を指定します。</span><span class="sxs-lookup"><span data-stu-id="26825-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="26825-163">この場合、これは `Verbose` に設定されます。これは、すべてのデバッグメッセージとトレースメッセージがログに記録されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="26825-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="26825-164">次の出力は、上の構成ファイルを使用するアプリケーションの `transports.log.txt` ファイルのエントリを示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="26825-165">新しい接続、削除された接続、およびトランスポートハートビートイベントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="26825-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="26825-166">イベントログへのサーバーイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-166">Logging server events to the event log</span></span>

<span data-ttu-id="26825-167">テキストファイルではなくイベントログにイベントを記録するには、[`sharedListeners`] ノードのエントリの値を変更します。</span><span class="sxs-lookup"><span data-stu-id="26825-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="26825-168">次のコードは、サーバーイベントをイベントログに記録する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="26825-169">**イベントログにイベントを記録するための XML サーバーコード**</span><span class="sxs-lookup"><span data-stu-id="26825-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="26825-170">次に示すように、イベントはアプリケーションログに記録され、イベントビューアーを通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="26825-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![SignalR ログを示すイベントビューアー](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="26825-172">イベントログを使用する場合は、 **TraceLevel**を**Error**に設定して、メッセージの数を管理可能な状態にします。</span><span class="sxs-lookup"><span data-stu-id="26825-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="26825-173">.NET クライアントでのトレースの有効化 (Windows デスクトップアプリ)</span><span class="sxs-lookup"><span data-stu-id="26825-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="26825-174">.NET クライアントは、 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)の実装を使用して、イベントをコンソール、テキストファイル、またはカスタムログに記録できます。</span><span class="sxs-lookup"><span data-stu-id="26825-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="26825-175">.NET クライアントでログ記録を有効にするには、接続の `TraceLevel` プロパティを[TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx)値に設定し、`TraceWriter` プロパティを有効な[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)インスタンスに設定します。</span><span class="sxs-lookup"><span data-stu-id="26825-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="26825-176">コンソールへのデスクトップクライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="26825-177">次C#のコードは、.net クライアントのイベントをコンソールに記録する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="26825-178">デスクトップクライアントのイベントをテキストファイルに記録する</span><span class="sxs-lookup"><span data-stu-id="26825-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="26825-179">次C#のコードは、.net クライアントのイベントをテキストファイルに記録する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="26825-180">次の出力は、上の構成ファイルを使用するアプリケーションの `ClientLog.txt` ファイルのエントリを示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="26825-181">サーバーに接続しているクライアントと、`addMessage`と呼ばれるクライアントメソッドを呼び出すハブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="26825-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="26825-182">Windows Phone 8 クライアントでトレースを有効にする</span><span class="sxs-lookup"><span data-stu-id="26825-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="26825-183">Windows Phone アプリ用の SignalR アプリケーションでは、デスクトップアプリと同じ .NET クライアントが使用されますが、[コンソールの Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)と、 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)を使用したファイルへの書き込みは使用できません。</span><span class="sxs-lookup"><span data-stu-id="26825-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="26825-184">代わりに、トレース用に[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)のカスタム実装を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26825-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="26825-185">UI への Windows Phone クライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="26825-186">[SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip)には、`TextBlockWriter`と呼ばれるカスタムの[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)実装を使用して、トレース出力を[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)に書き込む Windows Phone サンプルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="26825-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="26825-187">このクラスは、 **samples/SignalR**プロジェクトにあります。このクラスは、WP8 プロジェクトにあります。</span><span class="sxs-lookup"><span data-stu-id="26825-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="26825-188">`TextBlockWriter`のインスタンスを作成するときに、現在の[SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)と、トレース出力に使用する[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)を作成する[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)を渡します。</span><span class="sxs-lookup"><span data-stu-id="26825-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="26825-189">次に、渡された[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)に作成された新しい[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)にトレース出力が書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="26825-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="26825-190">デバッグコンソールへの Windows Phone クライアントイベントのログ記録</span><span class="sxs-lookup"><span data-stu-id="26825-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="26825-191">出力を UI ではなくデバッグコンソールに送信するには、[デバッグ] ウィンドウに書き込む[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)の実装を作成し、接続の[tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx)プロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="26825-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="26825-192">トレース情報は、Visual Studio の [デバッグ] ウィンドウに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="26825-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="26825-193">JavaScript クライアントでのトレースの有効化</span><span class="sxs-lookup"><span data-stu-id="26825-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="26825-194">接続でクライアント側のログ記録を有効にするには、接続オブジェクトの `logging` プロパティを設定してから、`start` メソッドを呼び出して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="26825-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="26825-195">**ブラウザーコンソールへのトレースを有効にするためのクライアント JavaScript コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="26825-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="26825-196">**ブラウザーコンソールへのトレースを有効にするためのクライアント JavaScript コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="26825-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="26825-197">トレースが有効になっている場合、JavaScript クライアントは、ブラウザーコンソールにイベントを記録します。</span><span class="sxs-lookup"><span data-stu-id="26825-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="26825-198">ブラウザーコンソールにアクセスするには、「 [Monitoring トランスポート](../getting-started/introduction-to-signalr.md#MonitoringTransports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26825-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="26825-199">次のスクリーンショットは、トレースが有効になっている SignalR JavaScript クライアントを示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="26825-200">次の図は、ブラウザーコンソールでの接続とハブの呼び出しイベントを示しています。</span><span class="sxs-lookup"><span data-stu-id="26825-200">It shows connection and hub invocation events in the browser console:</span></span>

![ブラウザーコンソールでの SignalR トレースイベント](enabling-signalr-tracing/_static/image4.png)
