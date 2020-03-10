---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hub API ガイド-JavaScript Client |Microsoft Docs
author: bradygaster
description: このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなどの JavaScript クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431290"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="c8953-103">ASP.NET SignalR Hub API ガイド-JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="c8953-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c8953-104">このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなど、JavaScript クライアントで SignalR version 2 用のハブ API を使用する方法の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="c8953-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="c8953-105">SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="c8953-106">サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="c8953-107">クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="c8953-108">SignalR は、クライアントとサーバーのすべての組み込みを処理します。</span><span class="sxs-lookup"><span data-stu-id="c8953-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="c8953-109">SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。</span><span class="sxs-lookup"><span data-stu-id="c8953-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="c8953-110">SignalR、ハブ、および永続的な接続の概要については、「 [SignalR の概要](../getting-started/introduction-to-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c8953-111">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="c8953-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c8953-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c8953-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="c8953-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c8953-113">.NET 4.5</span></span>
> - <span data-ttu-id="c8953-114">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="c8953-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c8953-115">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="c8953-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c8953-116">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c8953-117">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="c8953-117">Questions and comments</span></span>
>
> <span data-ttu-id="c8953-118">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="c8953-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c8953-119">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c8953-120">概要</span><span class="sxs-lookup"><span data-stu-id="c8953-120">Overview</span></span>

<span data-ttu-id="c8953-121">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="c8953-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="c8953-122">生成されたプロキシとその機能</span><span class="sxs-lookup"><span data-stu-id="c8953-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="c8953-123">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="c8953-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="c8953-124">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c8953-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="c8953-125">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="c8953-126">SignalR によって生成されたプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="c8953-127">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="c8953-128">$ hubConnection () によって作成されるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="c8953-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="c8953-129">Start メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="c8953-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="c8953-130">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="c8953-131">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="c8953-132">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="c8953-133">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="c8953-134">ハブクラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="c8953-135">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="c8953-136">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="c8953-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="c8953-137">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="c8953-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="c8953-138">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="c8953-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="c8953-139">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="c8953-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="c8953-140">サーバーまたは .NET クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="c8953-141">SignalR Hub API ガイド-サーバー</span><span class="sxs-lookup"><span data-stu-id="c8953-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="c8953-142">SignalR Hub API ガイド-.NET クライアント</span><span class="sxs-lookup"><span data-stu-id="c8953-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="c8953-143">SignalR 2 サーバーコンポーネントは .NET 4.5 でのみ使用できます (ただし、.net 4.0 の SignalR 2 用の .NET クライアントはあります)。</span><span class="sxs-lookup"><span data-stu-id="c8953-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="c8953-144">生成されたプロキシとその機能</span><span class="sxs-lookup"><span data-stu-id="c8953-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="c8953-145">SignalR が生成するプロキシを使用して、または使用せずに、SignalR サービスと通信するように JavaScript クライアントをプログラミングできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="c8953-146">プロキシでは、接続に使用するコードの構文を簡略化し、サーバーが呼び出すメソッドを記述して、サーバーでメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="c8953-147">サーバーメソッドを呼び出すためのコードを記述すると、生成されたプロキシによって、ローカル関数を実行しているかのような構文を使用できるようになります。 `invoke('serverMethod', arg1, arg2)`ではなく `serverMethod(arg1, arg2)` を記述できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="c8953-148">また、生成されたプロキシ構文では、サーバーメソッド名を誤って指定した場合に、即時および intelligible のクライアント側エラーが有効になります。</span><span class="sxs-lookup"><span data-stu-id="c8953-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="c8953-149">また、プロキシを定義するファイルを手動で作成した場合は、サーバーメソッドを呼び出すコードを記述するための IntelliSense サポートを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="c8953-150">たとえば、サーバーに次のハブクラスがあるとします。</span><span class="sxs-lookup"><span data-stu-id="c8953-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="c8953-151">次のコード例は、サーバーで `NewContosoChatMessage` メソッドを呼び出し、サーバーから `addContosoChatMessageToPage` メソッドの呼び出しを受信するための JavaScript コードを示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="c8953-152">**生成されたプロキシを使用する**</span><span class="sxs-lookup"><span data-stu-id="c8953-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="c8953-153">**生成されたプロキシを使用しない場合**</span><span class="sxs-lookup"><span data-stu-id="c8953-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="c8953-154">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="c8953-154">When to use the generated proxy</span></span>

<span data-ttu-id="c8953-155">サーバーが呼び出すクライアントメソッドに対して複数のイベントハンドラーを登録する場合、生成されたプロキシを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="c8953-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="c8953-156">それ以外の場合は、コーディングの設定に基づいて、生成されたプロキシを使用するかどうかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="c8953-157">使用しない場合は、クライアントコードの `script` 要素で "signalr/hub" URL を参照する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c8953-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="c8953-158">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c8953-158">Client setup</span></span>

<span data-ttu-id="c8953-159">JavaScript クライアントには、jQuery および SignalR core JavaScript ファイルへの参照が必要です。</span><span class="sxs-lookup"><span data-stu-id="c8953-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="c8953-160">JQuery バージョンは、1.6.4、または1.7.2、1.8.2、1.9.1 などのメジャー以降のバージョンである必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8953-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="c8953-161">生成されたプロキシを使用する場合は、SignalR によって生成されるプロキシ JavaScript ファイルへの参照も必要です。</span><span class="sxs-lookup"><span data-stu-id="c8953-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="c8953-162">次の例は、生成されたプロキシを使用する HTML ページで参照がどのように見えるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="c8953-163">これらの参照は、jQuery first、SignalR core、および SignalR proxy last という順序で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8953-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="c8953-164">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="c8953-165">前の例では、SignalR によって生成されるプロキシへの参照は、物理的なファイルではなく、動的に生成された JavaScript コードに対して行われます。</span><span class="sxs-lookup"><span data-stu-id="c8953-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="c8953-166">SignalR は、プロキシの JavaScript コードをその場で作成し、"/signalr/hubs" URL に応答してクライアントに提供します。</span><span class="sxs-lookup"><span data-stu-id="c8953-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="c8953-167">`MapSignalR` メソッドでサーバーの SignalR 接続に別のベース URL を指定した場合、動的に生成されるプロキシファイルの URL は、"/hub" が追加されたカスタム URL になります。</span><span class="sxs-lookup"><span data-stu-id="c8953-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="c8953-168">Windows 8 (Windows ストア) JavaScript クライアントの場合は、動的に生成されたファイルではなく、物理プロキシファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="c8953-169">詳細については、このトピックの「 [SignalR generated プロキシの物理ファイルを作成する方法](#manualproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="c8953-170">ASP.NET MVC 4 または 5 Razor ビューで、チルダを使用して、プロキシファイルの参照でアプリケーションルートを参照します。</span><span class="sxs-lookup"><span data-stu-id="c8953-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="c8953-171">MVC 5 での SignalR の使用の詳細については、「 [With SignalR AND MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してはじめにください。</span><span class="sxs-lookup"><span data-stu-id="c8953-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="c8953-172">ASP.NET MVC 3 Razor ビューでは、プロキシファイル参照に `Url.Content` を使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="c8953-173">ASP.NET Web フォームアプリケーションでは、プロキシファイル参照に `ResolveClientUrl` を使用するか、アプリルートの相対パス (チルダから始まる) を使用して ScriptManager で登録します。</span><span class="sxs-lookup"><span data-stu-id="c8953-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="c8953-174">一般的な規則として、CSS または JavaScript ファイルに使用する "/signalr/hubs" URL を指定する場合にも同じ方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="c8953-175">チルダを使用せずに URL を指定した場合、シナリオによっては IIS Express を使用して Visual Studio でテストしたときにアプリケーションが正常に動作しますが、完全な IIS に配置すると、404エラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="c8953-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="c8953-176">詳細については、MSDN サイトの「 [Visual Studio での Web サーバーでの ASP.NET Web プロジェクトの](https://msdn.microsoft.com/library/58wxa9w5.aspx)**ルートレベルリソースへの参照の解決**」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="c8953-177">Visual Studio 2017 でデバッグモードで web プロジェクトを実行するときに、ブラウザーとして Internet Explorer を使用すると、 **[スクリプト]** の下の**ソリューションエクスプローラー**にプロキシファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="c8953-178">ファイルの内容を表示するには、 **[ハブ]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c8953-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="c8953-179">Visual Studio 2012 または2013と Internet Explorer を使用していない場合、またはデバッグモードになっていない場合は、"/signalR/hubs" URL を参照してファイルの内容を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="c8953-180">たとえば、サイトが `http://localhost:56699`で実行されている場合は、ブラウザーで `http://localhost:56699/SignalR/hubs` にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c8953-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="c8953-181">SignalR によって生成されたプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="c8953-182">動的に生成されたプロキシの代わりに、プロキシコードを持つ物理ファイルを作成し、そのファイルを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="c8953-183">キャッシュやバンドル動作を制御したり、サーバーメソッドへの呼び出しをコーディングするときに IntelliSense を使用したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="c8953-184">プロキシファイルを作成するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c8953-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="c8953-185">[SignalR](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="c8953-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="c8953-186">コマンドプロンプトを開き、SignalR ファイルが格納されている*tools*フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="c8953-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="c8953-187">Tools フォルダーは次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="c8953-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="c8953-188">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="c8953-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="c8953-189">*.Dll*へのパスは、通常、プロジェクトフォルダー内の*bin*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="c8953-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="c8953-190">このコマンドは、 *signalr*と同じフォルダーに、 *node.js*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c8953-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="c8953-191">*サーバー .js*ファイルをプロジェクト内の適切なフォルダーに配置し、アプリケーションに合わせて名前を変更し、"signalr/hub" 参照の代わりに参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="c8953-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="c8953-192">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-192">How to establish a connection</span></span>

<span data-ttu-id="c8953-193">接続を確立するには、接続オブジェクトを作成し、プロキシを作成して、サーバーから呼び出すことができるメソッドのイベントハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8953-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="c8953-194">プロキシとイベントハンドラーがセットアップされたら、`start` メソッドを呼び出して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="c8953-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="c8953-195">生成されたプロキシを使用している場合は、独自のコードで接続オブジェクトを作成する必要はありません。これは、生成されたプロキシコードによって自動的に行われるためです。</span><span class="sxs-lookup"><span data-stu-id="c8953-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="c8953-196">**(生成されたプロキシを使用して) 接続を確立します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="c8953-197">**(生成されたプロキシを使用せずに) 接続を確立します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="c8953-198">このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="c8953-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c8953-199">別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="c8953-200">既定では、ハブの場所は現在のサーバーです。別のサーバーに接続している場合は、次の例に示すように、`start` メソッドを呼び出す前に URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="c8953-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="c8953-201">通常は、`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="c8953-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="c8953-202">接続の確立後にいくつかのイベントハンドラーを登録する場合は、これを行うことができますが、`start` メソッドを呼び出す前に、少なくとも1つのイベントハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8953-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="c8953-203">その理由の1つは、アプリケーションに多数のハブが存在する可能性がありますが、そのうちの1つだけを使用する場合は、すべてのハブで `OnConnected` イベントをトリガーしないことです。</span><span class="sxs-lookup"><span data-stu-id="c8953-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="c8953-204">接続が確立されると、ハブのプロキシにクライアントメソッドが存在することによって、`OnConnected` イベントをトリガーするように SignalR に指示します。</span><span class="sxs-lookup"><span data-stu-id="c8953-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="c8953-205">`start` メソッドを呼び出す前にイベントハンドラーを登録しないと、ハブでメソッドを呼び出すことができますが、ハブの `OnConnected` メソッドは呼び出されず、サーバーからクライアントメソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="c8953-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="c8953-206">$ hubConnection () によって作成されるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="c8953-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="c8953-207">例からわかるように、生成されたプロキシを使用すると、`$.connection.hub` は接続オブジェクトを参照します。</span><span class="sxs-lookup"><span data-stu-id="c8953-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="c8953-208">これは、生成されたプロキシを使用していない場合に `$.hubConnection()` を呼び出すことによって得られるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="c8953-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="c8953-209">生成されたプロキシコードは、次のステートメントを実行して、接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="c8953-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![生成されたプロキシファイルでの接続の作成](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="c8953-211">生成されたプロキシを使用している場合は、生成されたプロキシを使用していないときに接続オブジェクトで実行できる `$.connection.hub` で何でも実行できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="c8953-212">Start メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="c8953-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="c8953-213">`start` メソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="c8953-214">[JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。これは、`pipe`、`done`、`fail`などのメソッドを呼び出すことによってコールバック関数を追加できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c8953-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="c8953-215">サーバーメソッドの呼び出しなど、接続が確立された後に実行するコードがある場合は、そのコードをコールバック関数に配置するか、コールバック関数から呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c8953-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="c8953-216">`.done` のコールバックメソッドは、接続が確立された後、サーバーの `OnConnected` イベントハンドラーメソッドにあるコードの実行が完了した後に実行されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="c8953-217">前の例の "現在接続されている" ステートメントを、(`.done` コールバックではなく) `start` メソッド呼び出しの後の次のコード行として配置すると、次の例に示すように、接続が確立される前に `console.log` 行が実行されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![接続が確立された後に実行されるコードを記述する方法が正しくありません](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="c8953-219">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="c8953-220">通常、ブラウザーが `http://contoso.com`からページを読み込む場合、SignalR 接続は `http://contoso.com/signalr`の同じドメインにあります。</span><span class="sxs-lookup"><span data-stu-id="c8953-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="c8953-221">`http://contoso.com` のページが `http://fabrikam.com/signalr`に接続する場合は、ドメイン間接続が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="c8953-222">セキュリティ上の理由から、ドメイン間接続は既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="c8953-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="c8953-223">SignalR 1.x では、クロスドメイン要求は単一の EnableCrossDomain フラグによって制御されていました。</span><span class="sxs-lookup"><span data-stu-id="c8953-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="c8953-224">このフラグは、JSONP 要求と CORS 要求の両方を制御します。</span><span class="sxs-lookup"><span data-stu-id="c8953-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="c8953-225">柔軟性を高めるため、すべての CORS サポートは SignalR のサーバーコンポーネントから削除されています (ブラウザーがサポートしていることが検出された場合、JavaScript クライアントは引き続き CORS を使用します)。また、これらのシナリオをサポートするために新しい OWIN ミドルウェアを利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c8953-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="c8953-226">クライアントで JSONP が必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように、`HubConfiguration` オブジェクトの `EnableJSONP` を `true`に設定して、明示的に有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8953-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="c8953-227">JSONP は、CORS よりも安全性が低いため、既定では無効になっています。</span><span class="sxs-lookup"><span data-stu-id="c8953-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="c8953-228">**プロジェクトに Owin を追加し**ます。このライブラリをインストールするには、パッケージマネージャーコンソールで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c8953-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="c8953-229">このコマンドにより、2.1.0 バージョンのパッケージがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="c8953-230">UseCors の呼び出し</span><span class="sxs-lookup"><span data-stu-id="c8953-230">Calling UseCors</span></span>

 <span data-ttu-id="c8953-231">次のコードスニペットは、SignalR 2 でドメイン間接続を実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="c8953-232">**SignalR 2 でのクロスドメイン要求の実装**</span><span class="sxs-lookup"><span data-stu-id="c8953-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="c8953-233">次のコードは、SignalR 2 プロジェクトで CORS または JSONP を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="c8953-234">このコードサンプルでは、`MapSignalR`ではなく `Map` と `RunSignalR` を使用して、CORS ミドルウェアが、cors のサポートを必要とする SignalR 要求 (`MapSignalR`で指定されたパスのすべてのトラフィックではなく) に対してのみ実行されるようにします。マップは、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要があるその他のミドルウェアにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="c8953-235">コードで `jQuery.support.cors` を true に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="c8953-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![JQuery. サポートを true に設定しない](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="c8953-237">SignalR は CORS の使用を処理します。</span><span class="sxs-lookup"><span data-stu-id="c8953-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="c8953-238">`jQuery.support.cors` を true に設定すると、ブラウザーが CORS をサポートしていると SignalR が想定するため、JSONP は無効になります。</span><span class="sxs-lookup"><span data-stu-id="c8953-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="c8953-239">Localhost URL に接続している場合、Internet Explorer 10 はドメイン間接続を考慮しないため、サーバーでドメイン間接続を有効にしていない場合でも、アプリケーションは IE 10 でローカルに動作します。</span><span class="sxs-lookup"><span data-stu-id="c8953-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="c8953-240">Internet Explorer 9 でドメイン間接続を使用する方法の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="c8953-241">Chrome でのクロスドメイン接続の使用の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="c8953-242">このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="c8953-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c8953-243">別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="c8953-244">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-244">How to configure the connection</span></span>

<span data-ttu-id="c8953-245">接続を確立する前に、クエリ文字列パラメーターを指定することも、トランスポートメソッドを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="c8953-246">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-246">How to specify query string parameters</span></span>

<span data-ttu-id="c8953-247">クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="c8953-248">次の例は、クライアントコードでクエリ文字列パラメーターを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="c8953-249">**(生成されたプロキシを使用して) start メソッドを呼び出す前に、クエリ文字列の値を設定します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="c8953-250">**Start メソッドを呼び出す前に (生成されたプロキシを使用せずに) クエリ文字列の値を設定する**</span><span class="sxs-lookup"><span data-stu-id="c8953-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="c8953-251">次の例は、サーバーコードでクエリ文字列パラメーターを読み取る方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="c8953-252">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-252">How to specify the transport method</span></span>

<span data-ttu-id="c8953-253">接続プロセスの一環として、SignalR クライアントは、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定するために、通常はサーバーとネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="c8953-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="c8953-254">使用するトランスポートが既にわかっている場合は、`start` メソッドを呼び出すときにトランスポートメソッドを指定することで、このネゴシエーションプロセスを省略できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="c8953-255">**(生成されたプロキシを使用して) トランスポートメソッドを指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="c8953-256">**トランスポートメソッド (生成されたプロキシを除く) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="c8953-257">別の方法として、複数のトランスポートメソッドを SignalR で試行する順序で指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="c8953-258">**カスタムトランスポートフォールバックスキーム (生成されたプロキシを含む) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="c8953-259">**カスタムトランスポートフォールバックスキームを指定するクライアントコード (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="c8953-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="c8953-260">次の値を使用して、トランスポート方法を指定できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="c8953-261">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="c8953-261">"webSockets"</span></span>
- <span data-ttu-id="c8953-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="c8953-262">"foreverFrame"</span></span>
- <span data-ttu-id="c8953-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="c8953-263">"serverSentEvents"</span></span>
- <span data-ttu-id="c8953-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="c8953-264">"longPolling"</span></span>

<span data-ttu-id="c8953-265">次の例は、接続で使用されているトランスポートメソッドを調べる方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="c8953-266">**接続で使用されるトランスポートメソッド (生成されたプロキシを含む) を表示するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="c8953-267">**(生成されたプロキシを使用せずに) 接続で使用されるトランスポートメソッドを表示するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="c8953-268">サーバーコードでトランスポート方法を確認する方法については、「 [ASP.NET SignalR HUB API Guide-server-Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="c8953-269">トランスポートとフォールバックの詳細については、「 [SignalR とフォールバックの概要](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="c8953-270">ハブクラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="c8953-271">作成した各接続オブジェクトは、1つ以上のハブクラスを含む SignalR サービスへの接続に関する情報をカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="c8953-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="c8953-272">ハブクラスと通信するには、自分で作成したプロキシオブジェクト (生成されたプロキシを使用していない場合) または生成されたプロキシオブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="c8953-273">クライアントでは、プロキシ名はハブクラス名の camel 形式のバージョンです。</span><span class="sxs-lookup"><span data-stu-id="c8953-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="c8953-274">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="c8953-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="c8953-275">**サーバー上のハブクラス**</span><span class="sxs-lookup"><span data-stu-id="c8953-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="c8953-276">**ハブに対して生成されたクライアントプロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="c8953-277">**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**</span><span class="sxs-lookup"><span data-stu-id="c8953-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="c8953-278">`HubName` 属性を使用してハブクラスを装飾する場合は、大文字小文字を変更せずに正確な名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="c8953-279">**HubName 属性を持つサーバーのハブクラス**</span><span class="sxs-lookup"><span data-stu-id="c8953-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="c8953-280">**ハブに対して生成されたクライアントプロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="c8953-281">**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**</span><span class="sxs-lookup"><span data-stu-id="c8953-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c8953-282">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="c8953-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="c8953-283">サーバーがハブから呼び出すことができるメソッドを定義するには、生成されたプロキシの `client` プロパティを使用してハブプロキシにイベントハンドラーを追加するか、生成されたプロキシを使用しない場合は `on` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c8953-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="c8953-284">パラメーターには、複雑なオブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c8953-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="c8953-285">`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c8953-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="c8953-286">(`start` メソッドを呼び出した後にイベントハンドラーを追加する場合は、このドキュメントの「[接続を確立する方法](#establishconnection)」のメモを参照し、生成されたプロキシを使用せずにメソッドを定義するために示されている構文を使用します)。</span><span class="sxs-lookup"><span data-stu-id="c8953-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="c8953-287">メソッド名の一致では、大文字と小文字が区別されません。</span><span class="sxs-lookup"><span data-stu-id="c8953-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="c8953-288">たとえば、サーバー上の `Clients.All.addContosoChatMessageToPage` は、クライアントで `AddContosoChatMessageToPage`、`addContosoChatMessageToPage`、または `addcontosochatmessagetopage` を実行します。</span><span class="sxs-lookup"><span data-stu-id="c8953-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="c8953-289">**クライアントで (生成されたプロキシを使用して) メソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="c8953-290">**クライアントでメソッドを定義する別の方法 (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="c8953-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="c8953-291">**クライアントでメソッドを定義します (生成されたプロキシを使用しない場合、または start メソッドを呼び出した後にを追加する場合)**</span><span class="sxs-lookup"><span data-stu-id="c8953-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="c8953-292">**クライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="c8953-293">次の例には、メソッドパラメーターとしての複合オブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c8953-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="c8953-294">**(生成されたプロキシを使用して) 複雑なオブジェクトを受け取るクライアントのメソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="c8953-295">**複合オブジェクト (生成されたプロキシを使用しない) を受け取るクライアントのメソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="c8953-296">**複合オブジェクトを定義するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="c8953-297">**複合オブジェクトを使用してクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="c8953-298">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="c8953-298">How to call server methods from the client</span></span>

<span data-ttu-id="c8953-299">クライアントからサーバーメソッドを呼び出すには、生成されたプロキシを使用していない場合は、生成されたプロキシの `server` プロパティを使用するか、ハブプロキシで `invoke` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="c8953-300">戻り値またはパラメーターは、複雑なオブジェクトにすることができます。</span><span class="sxs-lookup"><span data-stu-id="c8953-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="c8953-301">ハブのメソッド名の camel 形式のバージョンを渡します。</span><span class="sxs-lookup"><span data-stu-id="c8953-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="c8953-302">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="c8953-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="c8953-303">次の例は、戻り値を持たないサーバーメソッドを呼び出す方法と、戻り値を持つサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="c8953-304">**HubMethodName 属性のないサーバーメソッド**</span><span class="sxs-lookup"><span data-stu-id="c8953-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="c8953-305">**パラメーターで渡される複合オブジェクトを定義するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="c8953-306">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="c8953-307">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="c8953-308">`HubMethodName` 属性を使用してハブメソッドを修飾した場合は、大文字小文字を変更せずにその名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="c8953-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="c8953-309">HubMethodName 属性を持つ**サーバーメソッド**</span><span class="sxs-lookup"><span data-stu-id="c8953-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="c8953-310">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="c8953-311">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="c8953-312">前の例は、戻り値を持たないサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="c8953-313">次の例は、戻り値を持つサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="c8953-314">**戻り値を持つメソッドのサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="c8953-315">戻り値**に使用されるストッククラス**</span><span class="sxs-lookup"><span data-stu-id="c8953-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="c8953-316">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="c8953-317">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c8953-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="c8953-318">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="c8953-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="c8953-319">SignalR は、次のように処理できる接続の有効期間イベントを提供します。</span><span class="sxs-lookup"><span data-stu-id="c8953-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="c8953-320">`starting`: 接続を介してデータが送信される前に発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="c8953-321">`received`: 接続でデータを受信したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="c8953-322">受信したデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="c8953-322">Provides the received data.</span></span>
- <span data-ttu-id="c8953-323">`connectionSlow`: クライアントが低速または頻繁に切断される接続を検出したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="c8953-324">`reconnecting`: 基になるトランスポートが再接続を開始したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="c8953-325">`reconnected`: 基になるトランスポートが再接続されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="c8953-326">`stateChanged`: 接続状態が変化したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="c8953-327">以前の状態と新しい状態 (接続、接続、再接続、または切断) を提供します。</span><span class="sxs-lookup"><span data-stu-id="c8953-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="c8953-328">`disconnected`: 接続が切断されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c8953-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="c8953-329">たとえば、遅延が発生する可能性がある接続の問題が発生した場合に警告メッセージを表示するには、`connectionSlow` イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="c8953-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="c8953-330">**(生成されたプロキシを使用して) connectionSlow イベントを処理します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="c8953-331">**(生成されたプロキシを使用せずに) connectionSlow イベントを処理する**</span><span class="sxs-lookup"><span data-stu-id="c8953-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="c8953-332">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="c8953-333">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="c8953-333">How to handle errors</span></span>

<span data-ttu-id="c8953-334">SignalR JavaScript クライアントには、ハンドラーを追加できる `error` イベントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="c8953-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="c8953-335">また、fail メソッドを使用して、サーバーメソッド呼び出しによって発生するエラーのハンドラーを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="c8953-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="c8953-336">サーバーで詳細なエラーメッセージを明示的に有効にしないと、エラーに関する最小限の情報が、エラーの後に SignalR によって返される例外オブジェクトに含まれます。</span><span class="sxs-lookup"><span data-stu-id="c8953-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="c8953-337">たとえば、`newContosoChatMessage` の呼び出しが失敗した場合、エラーオブジェクトのエラーメッセージには、セキュリティ上の理由により、実稼働環境でクライアントに詳細なエラーメッセージを送信する "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" が含まれます。ただし、トラブルシューティングのために詳細なエラーメッセージを有効にする場合は、サーバーで次のコードを使用してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="c8953-338">次の例は、エラーイベントのハンドラーを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="c8953-339">**(生成されたプロキシを使用して) エラーハンドラーを追加します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="c8953-340">**(生成されたプロキシを使用せずに) エラーハンドラーを追加します。**</span><span class="sxs-lookup"><span data-stu-id="c8953-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="c8953-341">次の例は、メソッドの呼び出しからエラーを処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8953-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="c8953-342">**メソッドの呼び出し (生成されたプロキシを使用) からのエラーを処理する**</span><span class="sxs-lookup"><span data-stu-id="c8953-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="c8953-343">**(生成されたプロキシを使用せずに) メソッド呼び出しからのエラーを処理する**</span><span class="sxs-lookup"><span data-stu-id="c8953-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="c8953-344">メソッドの呼び出しが失敗した場合は、`error` イベントも発生します。そのため、`error` メソッドハンドラー内のコードと `.fail` メソッドのコールバックが実行されます。</span><span class="sxs-lookup"><span data-stu-id="c8953-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="c8953-345">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="c8953-345">How to enable client-side logging</span></span>

<span data-ttu-id="c8953-346">接続でクライアント側のログ記録を有効にするには、接続オブジェクトの `logging` プロパティを設定してから、`start` メソッドを呼び出して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="c8953-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="c8953-347">**(生成されたプロキシを使用して) ログ記録を有効にする**</span><span class="sxs-lookup"><span data-stu-id="c8953-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="c8953-348">**(生成されたプロキシを使用しない) ログ記録を有効にする**</span><span class="sxs-lookup"><span data-stu-id="c8953-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="c8953-349">ログを表示するには、ブラウザーの開発者ツールを開き、[コンソール] タブにアクセスします。これを行う方法を示す詳細な手順とスクリーンショットを示すチュートリアルについては、「 [ASP.NET Signalr を使用したサーバーブロードキャスト-ログ記録を有効](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)にする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c8953-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
