---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR のトラブルシューティング |Microsoft Docs
author: bradygaster
description: この記事では、SignalR アプリケーションの開発に関する一般的な問題について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: bcd273d839aed64ad2712eb503dd1942a2d4e355
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467434"
---
# <a name="signalr-troubleshooting"></a><span data-ttu-id="01236-103">SignalR トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="01236-103">SignalR Troubleshooting</span></span>

<span data-ttu-id="01236-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="01236-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="01236-105">このドキュメントでは、SignalR に関する一般的なトラブルシューティングの問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-105">This document describes common troubleshooting issues with SignalR.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="01236-106">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="01236-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="01236-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="01236-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="01236-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="01236-108">.NET 4.5</span></span>
> - <span data-ttu-id="01236-109">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="01236-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="01236-110">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="01236-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="01236-111">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="01236-112">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="01236-112">Questions and comments</span></span>
>
> <span data-ttu-id="01236-113">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="01236-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="01236-114">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="01236-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="01236-115">このドキュメントには、次のセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="01236-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="01236-116">クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない</span><span class="sxs-lookup"><span data-stu-id="01236-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="01236-117">IIS websocket を ping/するように構成して、配信不能なクライアントを検出する</span><span class="sxs-lookup"><span data-stu-id="01236-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="01236-118">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="01236-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="01236-119">コンパイルとサーバー側のエラー</span><span class="sxs-lookup"><span data-stu-id="01236-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="01236-120">Visual Studio の問題</span><span class="sxs-lookup"><span data-stu-id="01236-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="01236-121">インターネットインフォメーションサービスの問題</span><span class="sxs-lookup"><span data-stu-id="01236-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="01236-122">Microsoft Azure の問題</span><span class="sxs-lookup"><span data-stu-id="01236-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="01236-123">クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない</span><span class="sxs-lookup"><span data-stu-id="01236-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="01236-124">ここでは、クライアントとサーバーの間でメソッド呼び出しが失敗し、意味のあるエラーメッセージが表示されない場合に発生する可能性のある原因について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="01236-125">SignalR アプリケーションでは、クライアントが実装するメソッドに関する情報はサーバーにありません。サーバーがクライアントメソッドを呼び出すと、メソッド名とパラメーターデータがクライアントに送信され、メソッドは、サーバーが指定した形式で存在する場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="01236-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="01236-126">一致するメソッドがクライアントに見つからない場合は、何も起こりません。サーバーでエラーメッセージは生成されません。</span><span class="sxs-lookup"><span data-stu-id="01236-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="01236-127">呼び出されていないクライアントメソッドをさらに詳しく調査するには、ハブで start メソッドを呼び出してから、サーバーからの呼び出しを確認する前に、ログ記録を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="01236-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="01236-128">JavaScript アプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (javascript クライアントバージョン)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="01236-129">.NET クライアントアプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (.Net クライアントのバージョン)](../guide-to-the-api/hubs-api-guide-net-client.md#logging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="01236-130">間違った方法、不適切なメソッドシグネチャ、または間違ったハブ名</span><span class="sxs-lookup"><span data-stu-id="01236-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="01236-131">呼び出されたメソッドの名前またはシグネチャがクライアントの適切なメソッドと完全に一致しない場合、呼び出しは失敗します。</span><span class="sxs-lookup"><span data-stu-id="01236-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="01236-132">サーバーによって呼び出されたメソッド名がクライアント上のメソッドの名前と一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="01236-133">また、SignalR は、JavaScript に適した camel 形式のメソッドを使用してハブプロキシを作成します。そのため、サーバー上で `SendMessage` というメソッドをクライアントプロキシで `sendMessage` と呼びます。</span><span class="sxs-lookup"><span data-stu-id="01236-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="01236-134">サーバー側コードで `HubName` 属性を使用する場合は、使用されている名前が、クライアントでハブの作成に使用された名前と一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="01236-135">`HubName` 属性を使用しない場合は、JavaScript クライアントのハブの名前が camel 形式であることを確認します。たとえば、ChatHub の代わりに chatHub のようにします。</span><span class="sxs-lookup"><span data-stu-id="01236-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="01236-136">クライアントでメソッド名が重複しています</span><span class="sxs-lookup"><span data-stu-id="01236-136">Duplicate method name on client</span></span>

<span data-ttu-id="01236-137">大文字と小文字のみが異なる、クライアントに重複するメソッドがないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="01236-138">クライアントアプリケーションに `sendMessage`というメソッドがある場合は、`SendMessage` と呼ばれるメソッドも存在しないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="01236-139">クライアントに JSON パーサーがありません</span><span class="sxs-lookup"><span data-stu-id="01236-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="01236-140">SignalR を使用するには、サーバーとクライアント間の呼び出しをシリアル化するために JSON パーサーが存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="01236-141">クライアントに組み込みの JSON パーサー (Internet Explorer 7 など) がない場合は、アプリケーションに1つを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="01236-142">JSON パーサーは[こちら](http://nuget.org/packages/json2)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="01236-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="01236-143">Hub と PersistentConnection 構文の混在</span><span class="sxs-lookup"><span data-stu-id="01236-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="01236-144">SignalR は、2つの通信モデル (ハブと PersistentConnections) を使用します。</span><span class="sxs-lookup"><span data-stu-id="01236-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="01236-145">これら2つの通信モデルを呼び出すための構文は、クライアントコードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="01236-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="01236-146">サーバーコードにハブを追加した場合は、すべてのクライアントコードで適切なハブ構文が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="01236-147">**JavaScript クライアントで PersistentConnection を作成する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-147">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="01236-148">**Javascript クライアントでハブプロキシを作成する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-148">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="01236-149">**C#ルートを PersistentConnection にマップするサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="01236-149">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="01236-150">**C#ハブまたは複数のアプリケーションがある場合は複数のハブにルートをマップするサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="01236-150">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="01236-151">サブスクリプションが追加される前に接続が開始されました</span><span class="sxs-lookup"><span data-stu-id="01236-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="01236-152">サーバーから呼び出すことができるメソッドがプロキシに追加される前にハブの接続が開始されると、メッセージは受信されません。</span><span class="sxs-lookup"><span data-stu-id="01236-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="01236-153">次の JavaScript コードはハブを適切に起動しません。</span><span class="sxs-lookup"><span data-stu-id="01236-153">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="01236-154">**ハブメッセージの受信を許可しない JavaScript クライアントコードが正しくありません**</span><span class="sxs-lookup"><span data-stu-id="01236-154">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="01236-155">代わりに、Start を呼び出す前にメソッドサブスクリプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="01236-155">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="01236-156">**ハブにサブスクリプションを正しく追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-156">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="01236-157">ハブプロキシにメソッド名がありません</span><span class="sxs-lookup"><span data-stu-id="01236-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="01236-158">サーバーで定義されているメソッドがクライアントでサブスクライブされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="01236-159">サーバーによってメソッドが定義されている場合でも、クライアントプロキシに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="01236-160">メソッドは、次の方法でクライアントプロキシに追加できます (このメソッドは、ハブではなく、ハブの `client` メンバーに追加されることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="01236-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="01236-161">**ハブプロキシにメソッドを追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-161">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="01236-162">ハブまたはハブのメソッドがパブリックとして宣言されていません</span><span class="sxs-lookup"><span data-stu-id="01236-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="01236-163">クライアントで表示されるようにするには、ハブの実装とメソッドを `public`として宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="01236-164">別のアプリケーションからのハブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="01236-164">Accessing hub from a different application</span></span>

<span data-ttu-id="01236-165">SignalR Hub にアクセスできるのは、SignalR クライアントを実装するアプリケーションのみです。</span><span class="sxs-lookup"><span data-stu-id="01236-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="01236-166">SignalR は、他の通信ライブラリ (SOAP や WCF web サービスなど) と相互運用することはできません。ターゲットプラットフォームに使用できる SignalR クライアントがない場合は、サーバーのエンドポイントに直接アクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="01236-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="01236-167">手動によるデータのシリアル化</span><span class="sxs-lookup"><span data-stu-id="01236-167">Manually serializing data</span></span>

<span data-ttu-id="01236-168">SignalR は自動的に JSON を使用してメソッドのパラメーターをシリアル化します。自分で行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="01236-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="01236-169">OnDisconnected 関数のクライアントでリモートハブのメソッドが実行されませんでした</span><span class="sxs-lookup"><span data-stu-id="01236-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="01236-170">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-170">This behavior is by design.</span></span> <span data-ttu-id="01236-171">`OnDisconnected` が呼び出されると、ハブは既に `Disconnected` 状態に入っています。これにより、これ以上ハブメソッドを呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="01236-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="01236-172">**C#OnDisconnected イベントでコードを正しく実行するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="01236-172">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="01236-173">OnDisconnect が一貫した時刻に起動しない</span><span class="sxs-lookup"><span data-stu-id="01236-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="01236-174">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-174">This behavior is by design.</span></span> <span data-ttu-id="01236-175">ユーザーがアクティブな SignalR 接続を使用してページから移動しようとすると、SignalR クライアントは、クライアント接続が停止されることをサーバーに通知します。</span><span class="sxs-lookup"><span data-stu-id="01236-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="01236-176">SignalR クライアントのベストエフォート試行がサーバーへの接続に失敗した場合、後で構成可能な `DisconnectTimeout` 後に、`OnDisconnected` イベントが発生するまで、サーバーは接続を破棄します。</span><span class="sxs-lookup"><span data-stu-id="01236-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="01236-177">SignalR クライアントのベストエフォートの試行が成功すると、`OnDisconnected` イベントが直ちに発生します。</span><span class="sxs-lookup"><span data-stu-id="01236-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="01236-178">`DisconnectTimeout` 設定の設定の詳細については、「[接続の有効期間イベントの処理: 切断タイムアウト](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="01236-179">接続数の上限に達しました</span><span class="sxs-lookup"><span data-stu-id="01236-179">Connection limit reached</span></span>

<span data-ttu-id="01236-180">Windows 7 などのクライアントオペレーティングシステムで IIS の完全バージョンを使用する場合は、10接続の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="01236-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="01236-181">クライアント OS を使用する場合は、この制限を回避するために、代わりに IIS Express を使用します。</span><span class="sxs-lookup"><span data-stu-id="01236-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="01236-182">ドメイン間接続が適切に設定されていません</span><span class="sxs-lookup"><span data-stu-id="01236-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="01236-183">ドメイン間接続 (SignalR URL がホスティングページと同じドメインにない接続) が正しく設定されていない場合、接続はエラーメッセージなしで失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="01236-184">ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="01236-185">NTLM を使用した接続 (Active Directory) が .NET クライアントで動作しない</span><span class="sxs-lookup"><span data-stu-id="01236-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="01236-186">接続が正しく構成されていない場合、ドメインセキュリティを使用する .NET クライアントアプリケーションの接続が失敗することがあります。</span><span class="sxs-lookup"><span data-stu-id="01236-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="01236-187">ドメイン環境で SignalR を使用するには、必要な接続プロパティを次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="01236-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="01236-188">**C#接続資格情報を実装するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-188">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="01236-189">IIS websocket を ping/するように構成して、配信不能なクライアントを検出する</span><span class="sxs-lookup"><span data-stu-id="01236-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="01236-190">SignalR サーバーは、クライアントが動作していないかどうかを認識せず、接続エラー (つまり `OnClose` コールバック) について、基になる websocket からの通知に依存します。</span><span class="sxs-lookup"><span data-stu-id="01236-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the `OnClose` callback.</span></span> <span data-ttu-id="01236-191">この問題に対する解決策の1つは、ping/を実行するように IIS websocket を構成することです。</span><span class="sxs-lookup"><span data-stu-id="01236-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="01236-192">これにより、予期せずに切断された場合に接続が閉じられるようになります。</span><span class="sxs-lookup"><span data-stu-id="01236-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="01236-193">詳細については、[この stackoverflow の投稿](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="01236-194">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="01236-194">Other connection issues</span></span>

<span data-ttu-id="01236-195">このセクションでは、接続中に発生する特定の現象またはエラーメッセージの原因と解決方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="01236-196">"データを送信する前に開始する必要があります" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="01236-197">このエラーは、接続が開始される前にコードが SignalR オブジェクトを参照する場合によく見られます。</span><span class="sxs-lookup"><span data-stu-id="01236-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="01236-198">サーバーで定義されているメソッドを呼び出すのと同様に、ハンドラーの wireup とを、接続の完了後に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="01236-199">`Start` の呼び出しが非同期であるため、呼び出しの後のコードを実行してから完了することができます。</span><span class="sxs-lookup"><span data-stu-id="01236-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="01236-200">接続が完全に開始された後にハンドラーを追加する最善の方法は、start メソッドにパラメーターとして渡されるコールバック関数にそれらを配置することです。</span><span class="sxs-lookup"><span data-stu-id="01236-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="01236-201">**SignalR オブジェクトを参照するイベントハンドラーを正しく追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="01236-201">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="01236-202">このエラーは、SignalR オブジェクトがまだ参照されている間に接続が停止した場合にも表示されます。</span><span class="sxs-lookup"><span data-stu-id="01236-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="01236-203">"301 が永続的に移動されました" または "302 を一時的に移動" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="01236-204">このエラーは、プロジェクトに SignalR という名前のフォルダーが含まれている場合に発生する可能性があります。これにより、自動的に作成されたプロキシが妨げられます。</span><span class="sxs-lookup"><span data-stu-id="01236-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="01236-205">このエラーを回避するには、アプリケーションで `SignalR` という名前のフォルダーを使用しないようにするか、自動プロキシ生成をオフにします。</span><span class="sxs-lookup"><span data-stu-id="01236-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="01236-206">[生成されたプロキシとその](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)詳細については、「」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="01236-207">.NET または Silverlight クライアントで "403 の許可されていません" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="01236-208">このエラーは、ドメイン間通信が正しく有効になっていないクロスドメイン環境で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="01236-209">ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="01236-210">Silverlight クライアントでドメイン間接続を確立する方法については、「 [silverlight クライアントからのクロスドメイン](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)接続」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="01236-211">"404 が見つかりません" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-211">"404 Not Found" error</span></span>

<span data-ttu-id="01236-212">この問題にはいくつかの原因があります。</span><span class="sxs-lookup"><span data-stu-id="01236-212">There are several causes for this issue.</span></span> <span data-ttu-id="01236-213">次のすべてを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-213">Verify all of the following:</span></span>

- <span data-ttu-id="01236-214">**ハブプロキシアドレスの参照が正しくフォーマットされていません:** このエラーは、生成されたハブプロキシアドレスへの参照が正しく書式設定されていない場合によく発生します。</span><span class="sxs-lookup"><span data-stu-id="01236-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="01236-215">ハブアドレスへの参照が適切に作成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="01236-216">詳細について[は、「動的に生成されたプロキシを参照する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="01236-217">**ハブルートを追加する前に、アプリケーションにルートを追加します。** アプリケーションで他のルートを使用する場合は、追加された最初のルートが `MapSignalR`の呼び出しであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="01236-218">**拡張子 url の更新なしで IIS 7 または7.5 を使用する場合:** IIS 7 または7.5 を使用するには、サーバーが `/signalr/hubs`でハブの定義にアクセスできるように、拡張子 Url の更新が必要です。</span><span class="sxs-lookup"><span data-stu-id="01236-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="01236-219">更新プログラムについては、[こちら](https://support.microsoft.com/kb/980368)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-219">The update can be found [here](https://support.microsoft.com/kb/980368).</span></span>
- <span data-ttu-id="01236-220">**IIS キャッシュが古くなっているか、破損しています:** キャッシュの内容が古くなっていないことを確認するには、PowerShell ウィンドウで次のコマンドを入力してキャッシュをクリアします。</span><span class="sxs-lookup"><span data-stu-id="01236-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="01236-221">"500 内部サーバーエラー"</span><span class="sxs-lookup"><span data-stu-id="01236-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="01236-222">これは非常に一般的なエラーであり、さまざまな原因が考えられます。</span><span class="sxs-lookup"><span data-stu-id="01236-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="01236-223">エラーの詳細は、サーバーのイベントログに表示されるか、またはサーバーのデバッグによって検出されます。</span><span class="sxs-lookup"><span data-stu-id="01236-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="01236-224">詳細なエラー情報を取得するには、サーバーで詳細なエラーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="01236-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="01236-225">詳細については、「 [Hub クラスでエラーを処理する方法](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="01236-226">このエラーは、ファイアウォールまたはプロキシが適切に構成されていないために、要求ヘッダーの書き換えが発生した場合にもよく見られます。</span><span class="sxs-lookup"><span data-stu-id="01236-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="01236-227">この問題を解決するには、ファイアウォールまたはプロキシでポート80が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="01236-228">"予期しない応答コード: 500"</span><span class="sxs-lookup"><span data-stu-id="01236-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="01236-229">このエラーは、アプリケーションで使用されている .NET framework のバージョンが、Web.config で指定されているバージョンと一致しない場合に発生する可能性があります。この問題を解決するには、アプリケーション設定と Web.config ファイルの両方で .NET 4.5 が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="01236-230">"TypeError: &lt;hubType&gt; が定義されていません" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="01236-231">このエラーは、`MapSignalR` の呼び出しが正しく行われない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="01236-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="01236-232">詳細については[、「How to Register SignalR ミドルウェア」および「Configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="01236-233">JsonSerializationException がユーザーコードによって処理されませんでした</span><span class="sxs-lookup"><span data-stu-id="01236-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="01236-234">メソッドに送信するパラメーターに、シリアル化できない型 (ファイルハンドルやデータベース接続など) が含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="01236-235">クライアントに送信したくないサーバー側オブジェクト (セキュリティのため、またはシリアル化の理由) でメンバーを使用する必要がある場合は、`JSONIgnore` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="01236-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="01236-236">"プロトコルエラー: 不明なトランスポート" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="01236-237">このエラーは、SignalR が使用するトランスポートをクライアントがサポートしていない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="01236-238">SignalR で使用できるブラウザーの詳細については[、「トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="01236-239">"JavaScript Hub プロキシの生成が無効になりました。"</span><span class="sxs-lookup"><span data-stu-id="01236-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="01236-240">このエラーは、`signalr/hubs`で動的に生成されたプロキシへの参照も含め、`DisableJavaScriptProxies` が設定されている場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="01236-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="01236-241">プロキシを手動で作成する方法の詳細については、「[生成されたプロキシとその機能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="01236-242">"接続 ID の形式が正しくありません" または "active SignalR 接続中にユーザー id を変更できません" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="01236-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="01236-243">このエラーは、認証が使用されていて、接続が停止される前にクライアントがログアウトされている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="01236-244">この問題を解決するには、クライアントをログに記録する前に、SignalR 接続を停止します。</span><span class="sxs-lookup"><span data-stu-id="01236-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="01236-245">"キャッチされていないエラー: SignalR: jQuery が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="01236-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="01236-246">SignalR ファイルの前に jQuery が参照されていることを確認してください。 "エラー</span><span class="sxs-lookup"><span data-stu-id="01236-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="01236-247">SignalR JavaScript クライアントでは、jQuery を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="01236-248">JQuery への参照が正しいこと、使用されているパスが有効であること、および jQuery への参照が SignalR への参照の前にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="01236-249">"キャッチされていない TypeError: プロパティ '&lt;プロパティ&gt;' undefined ' エラーを読み取ることができません</span><span class="sxs-lookup"><span data-stu-id="01236-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="01236-250">このエラーは、jQuery またはハブプロキシが正しく参照されていない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="01236-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="01236-251">JQuery とハブプロキシへの参照が正しいこと、使用されているパスが有効であること、および jQuery への参照がハブプロキシへの参照の前にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="01236-252">ハブプロキシへの既定の参照は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="01236-252">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="01236-253">**ハブプロキシを正しく参照する HTML クライアント側コード**</span><span class="sxs-lookup"><span data-stu-id="01236-253">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="01236-254">"RuntimeBinderException はユーザーコードによって処理されませんでした" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="01236-255">このエラーは、`Hub.On` の不適切なオーバーロードが使用されている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="01236-256">メソッドに戻り値がある場合は、戻り値の型をジェネリック型パラメーターとして指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="01236-257">**クライアントで定義されたメソッド (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="01236-257">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="01236-258">接続 ID が一致していないか、ページ読み込み間の接続が壊れています</span><span class="sxs-lookup"><span data-stu-id="01236-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="01236-259">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-259">This behavior is by design.</span></span> <span data-ttu-id="01236-260">ハブオブジェクトはページオブジェクトでホストされるため、ページが更新されるとハブは破棄されます。</span><span class="sxs-lookup"><span data-stu-id="01236-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="01236-261">複数ページアプリケーションでは、ページの読み込み間で一貫性を保つために、ユーザーと接続 Id の間の関連付けを維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="01236-262">接続 Id は、`ConcurrentDictionary` オブジェクトまたはデータベースのいずれかのサーバーに格納できます。</span><span class="sxs-lookup"><span data-stu-id="01236-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="01236-263">"値を null にすることはできません" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-263">"Value cannot be null" error</span></span>

<span data-ttu-id="01236-264">オプションのパラメーターを使用したサーバー側のメソッドは、現在サポートされていません。省略可能なパラメーターを省略すると、メソッドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="01236-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="01236-265">詳細については、「[省略可能なパラメーター](https://github.com/SignalR/SignalR/issues/324)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="01236-266">"&lt;のアドレス&gt;" Firefox ではサーバーへの接続を確立できません "というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="01236-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="01236-267">WebSocket トランスポートのネゴシエーションが失敗し、代わりに別のトランスポートが使用されている場合、このエラーメッセージは、消火バグで確認できます。</span><span class="sxs-lookup"><span data-stu-id="01236-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="01236-268">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="01236-269">".NET クライアントアプリケーションの検証手順によると、リモート証明書が無効です" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="01236-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="01236-270">サーバーにカスタムクライアント証明書が必要な場合は、要求が行われる前に接続に x509certificate を追加できます。</span><span class="sxs-lookup"><span data-stu-id="01236-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="01236-271">`Connection.AddClientCertificate`を使用して、証明書を接続に追加します。</span><span class="sxs-lookup"><span data-stu-id="01236-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="01236-272">認証のタイムアウト後に接続が切断する</span><span class="sxs-lookup"><span data-stu-id="01236-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="01236-273">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-273">This behavior is by design.</span></span> <span data-ttu-id="01236-274">接続がアクティブな間は、認証資格情報を変更できません。資格情報を更新するには、接続を停止して再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="01236-275">JQuery Mobile を使用すると、OnConnected が2回呼び出されます</span><span class="sxs-lookup"><span data-stu-id="01236-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="01236-276">jQuery Mobile の `initializePage` 関数は、各ページのスクリプトを強制的に再実行し、2つ目の接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="01236-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="01236-277">この問題の解決策は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="01236-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="01236-278">JavaScript ファイルの前に jQuery Mobile への参照を含めます。</span><span class="sxs-lookup"><span data-stu-id="01236-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="01236-279">`$.mobile.autoInitializePage = false`を設定して、`initializePage` 関数を無効にします。</span><span class="sxs-lookup"><span data-stu-id="01236-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="01236-280">接続を開始する前に、ページの初期化が完了するのを待ちます。</span><span class="sxs-lookup"><span data-stu-id="01236-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="01236-281">Silverlight アプリケーションでは、サーバー送信イベントを使用してメッセージが遅延されます。</span><span class="sxs-lookup"><span data-stu-id="01236-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="01236-282">Silverlight でサーバー送信イベントを使用すると、メッセージが遅延します。</span><span class="sxs-lookup"><span data-stu-id="01236-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="01236-283">代わりに、長いポーリングを強制的に使用するには、接続を開始するときに次のようにします。</span><span class="sxs-lookup"><span data-stu-id="01236-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="01236-284">永続的フレームプロトコルを使用する "アクセス許可が拒否されました"</span><span class="sxs-lookup"><span data-stu-id="01236-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="01236-285">これは、[ここで](https://github.com/SignalR/SignalR/issues/1963)説明されている既知の問題です。</span><span class="sxs-lookup"><span data-stu-id="01236-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="01236-286">この現象は、最新の JQuery ライブラリを使用して表示される場合があります。この回避策は、アプリケーションを JQuery 1.8.2 にダウングレードすることです。</span><span class="sxs-lookup"><span data-stu-id="01236-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="01236-287">"InvalidOperationException: 有効な web ソケット要求ではありません。</span><span class="sxs-lookup"><span data-stu-id="01236-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="01236-288">このエラーは、WebSocket プロトコルが使用されているが、ネットワークプロキシが要求ヘッダーを変更している場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="01236-289">この問題を解決するには、ポート80で WebSocket を許可するようにプロキシを構成します。</span><span class="sxs-lookup"><span data-stu-id="01236-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="01236-290">"例外: クライアントがサーバーでメソッドを呼び出すときに、メソッド名&gt; メソッドを &lt;解決できませんでした。</span><span class="sxs-lookup"><span data-stu-id="01236-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="01236-291">このエラーは、配列などの JSON ペイロードでは検出できないデータ型を使用した場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="01236-292">この回避策は、IList など、JSON で検出できるデータ型を使用することです。</span><span class="sxs-lookup"><span data-stu-id="01236-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="01236-293">詳細については、「 [.Net クライアントが配列パラメーターを使用してハブメソッドを呼び出すことができません](https://github.com/SignalR/SignalR/issues/2672)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="01236-294">コンパイルとサーバー側のエラー</span><span class="sxs-lookup"><span data-stu-id="01236-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="01236-295">次のセクションでは、コンパイラとサーバー側のランタイムエラーに対して考えられる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span>

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="01236-296">ハブインスタンスへの参照が null です</span><span class="sxs-lookup"><span data-stu-id="01236-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="01236-297">ハブインスタンスは接続ごとに作成されるため、自分でコード内にハブのインスタンスを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="01236-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="01236-298">ハブ自体の外部からハブのメソッドを呼び出す方法については、ハブコンテキストへの参照を取得する方法について、「[クライアントメソッドを呼び出し、ハブクラスの外部からグループを管理する方法](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="01236-299">HTTPContext. Current. Session が null です</span><span class="sxs-lookup"><span data-stu-id="01236-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="01236-300">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-300">This behavior is by design.</span></span> <span data-ttu-id="01236-301">セッション状態を有効にすると双方向メッセージングが中断するため、SignalR は ASP.NET セッション状態をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="01236-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="01236-302">オーバーライドする適切なメソッドがありません</span><span class="sxs-lookup"><span data-stu-id="01236-302">No suitable method to override</span></span>

<span data-ttu-id="01236-303">以前のドキュメントまたはブログのコードを使用している場合は、このエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="01236-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="01236-304">変更または非推奨とされたメソッド (`OnConnectedAsync`など) の名前を参照していないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="01236-305">HostContextExtensions. WebSocketServerUrl は null です</span><span class="sxs-lookup"><span data-stu-id="01236-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="01236-306">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-306">This behavior is by design.</span></span> <span data-ttu-id="01236-307">このメンバーは非推奨とされます。使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="01236-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="01236-308">"' Signalr ' という名前のルートは既にルートコレクションに含まれています" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="01236-309">このエラーは、アプリケーションによって `MapSignalR` が2回呼び出された場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="01236-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="01236-310">アプリケーションの例としては、Startup クラスで `MapSignalR` を直接呼び出すものがあります。他のユーザーは、ラッパークラスで呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="01236-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="01236-311">アプリケーションで両方が実行されていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="01236-312">WebSocket が使用されていません</span><span class="sxs-lookup"><span data-stu-id="01236-312">WebSocket is not used</span></span>

<span data-ttu-id="01236-313">サーバーとクライアントが WebSocket ([サポートされているプラットフォーム](../getting-started/supported-platforms.md)のドキュメントに記載されています) の要件を満たしていることを確認した場合は、サーバーで websocket を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="01236-314">この手順については、[こちら](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="01236-315">$. 接続が定義されていません</span><span class="sxs-lookup"><span data-stu-id="01236-315">$.connection is undefined</span></span>

<span data-ttu-id="01236-316">このエラーは、ページ上のスクリプトが正しく読み込まれていないか、ハブプロキシに到達できないか、または正しくアクセスされていないことを示します。</span><span class="sxs-lookup"><span data-stu-id="01236-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="01236-317">ページ上のスクリプト参照がプロジェクトに読み込まれたスクリプトに対応していること、およびサーバーの実行中にブラウザーで/signalr/hubs にアクセスできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="01236-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="01236-318">動的な式のコンパイルに必要な1つ以上の型が見つかりません</span><span class="sxs-lookup"><span data-stu-id="01236-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="01236-319">このエラーは、`Microsoft.CSharp` ライブラリがないことを示します。</span><span class="sxs-lookup"><span data-stu-id="01236-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="01236-320">[**アセンブリ-&gt;Framework** ] タブで追加します。</span><span class="sxs-lookup"><span data-stu-id="01236-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="01236-321">Visual Basic または厳密に型指定されたハブで、呼び出し元の状態にクライアントからアクセスすることはできません。"型 ' タスクの (オブジェクトの) ' から型 ' String ' への変換は無効です" エラー</span><span class="sxs-lookup"><span data-stu-id="01236-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="01236-322">Visual Basic または厳密に型指定されたハブで呼び出し元の状態にアクセスするには、`Clients.Caller`ではなく、`Clients.CallerState` プロパティ (SignalR 2.1 で導入) を使用します。</span><span class="sxs-lookup"><span data-stu-id="01236-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="01236-323">Visual Studio の問題</span><span class="sxs-lookup"><span data-stu-id="01236-323">Visual Studio issues</span></span>

<span data-ttu-id="01236-324">このセクションでは、Visual Studio で発生した問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="01236-325">スクリプトドキュメントノードがソリューションエクスプローラーに表示されない</span><span class="sxs-lookup"><span data-stu-id="01236-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="01236-326">このチュートリアルの一部では、デバッグ中にソリューションエクスプローラーの [スクリプトドキュメント] ノードに移動します。</span><span class="sxs-lookup"><span data-stu-id="01236-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="01236-327">このノードは JavaScript デバッガーによって生成され、Internet Explorer でブラウザークライアントをデバッグしているときにのみ表示されます。Chrome または Firefox が使用されている場合、ノードは表示されません。</span><span class="sxs-lookup"><span data-stu-id="01236-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="01236-328">また、Silverlight デバッガーなど、別のクライアントデバッガーが実行されている場合も、JavaScript デバッガーは実行されません。</span><span class="sxs-lookup"><span data-stu-id="01236-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="01236-329">SignalR が Visual Studio 2008 以前で動作しない</span><span class="sxs-lookup"><span data-stu-id="01236-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="01236-330">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="01236-330">This behavior is by design.</span></span> <span data-ttu-id="01236-331">SignalR には .NET Framework 4 以降が必要です。そのためには、Visual Studio 2010 以降で SignalR アプリケーションを開発する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="01236-332">SignalR のサーバーコンポーネントには .NET Framework 4.5 が必要です。</span><span class="sxs-lookup"><span data-stu-id="01236-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="01236-333">IIS の問題</span><span class="sxs-lookup"><span data-stu-id="01236-333">IIS issues</span></span>

<span data-ttu-id="01236-334">ここでは、インターネットインフォメーションサービスに関する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="01236-335">SignalR は Visual Studio 開発サーバー上で動作しますが、IIS では機能しません。</span><span class="sxs-lookup"><span data-stu-id="01236-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="01236-336">SignalR は IIS 7.0 および7.5 でサポートされていますが、拡張子 Url のサポートは追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01236-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="01236-337">拡張子 Url のサポートを追加するには、「」を参照してください[https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="01236-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="01236-338">SignalR を使用するには、ASP.NET をサーバーにインストールする必要があります (既定では、ASP.NET は IIS にインストールされていません)。</span><span class="sxs-lookup"><span data-stu-id="01236-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="01236-339">ASP.NET をインストールするには、「 [ASP.NET のダウンロード](https://www.asp.net/downloads)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01236-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="01236-340">Microsoft Azure の問題</span><span class="sxs-lookup"><span data-stu-id="01236-340">Microsoft Azure issues</span></span>

<span data-ttu-id="01236-341">ここでは、Microsoft Azure に関する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="01236-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="01236-342">Azure Worker ロールで SignalR をホストするときの FileLoadException</span><span class="sxs-lookup"><span data-stu-id="01236-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="01236-343">Azure ワーカーロールで SignalR をホストすると、"ファイルまたはアセンブリ ' Owin, Version = 2.0.0.0 ' を読み込むことができませんでした" という例外が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01236-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="01236-344">これは、NuGet の既知の問題です。バインドリダイレクトは、Azure ワーカーロールプロジェクトに自動的に追加されません。</span><span class="sxs-lookup"><span data-stu-id="01236-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="01236-345">この問題を解決するには、バインドリダイレクトを手動で追加します。</span><span class="sxs-lookup"><span data-stu-id="01236-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="01236-346">ワーカーロールプロジェクトの `app.config` ファイルに次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="01236-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="01236-347">トピック名を変更した後、Azure バックプレーンでメッセージが受信されない</span><span class="sxs-lookup"><span data-stu-id="01236-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="01236-348">Azure バックプレーンによって使用されるトピックは、内部的に管理されます。ユーザーが構成できるようにするためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="01236-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
