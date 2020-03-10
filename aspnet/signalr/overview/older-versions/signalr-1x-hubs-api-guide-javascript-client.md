---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x Hub API ガイド-JavaScript Client |Microsoft Docs
author: bradygaster
description: このドキュメントでは、ブラウザーや Windows Store (WinJS) applic など、JavaScript クライアントで SignalR バージョン1.1 用のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431104"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="651f5-103">SignalR 1.x ハブ API ガイド - JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="651f5-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="651f5-104">[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="651f5-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="651f5-105">このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなど、JavaScript クライアントで SignalR バージョン1.1 用のハブ API を使用する方法の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="651f5-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="651f5-106">SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="651f5-107">サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="651f5-108">クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="651f5-109">SignalR は、クライアントとサーバーのすべての組み込みを処理します。</span><span class="sxs-lookup"><span data-stu-id="651f5-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="651f5-110">SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。</span><span class="sxs-lookup"><span data-stu-id="651f5-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="651f5-111">SignalR、ハブ、および永続的な接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては、[はじめに SignalR](../getting-started/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="651f5-112">概要</span><span class="sxs-lookup"><span data-stu-id="651f5-112">Overview</span></span>

<span data-ttu-id="651f5-113">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="651f5-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="651f5-114">生成されたプロキシとその機能</span><span class="sxs-lookup"><span data-stu-id="651f5-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="651f5-115">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="651f5-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="651f5-116">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="651f5-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="651f5-117">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="651f5-118">SignalR によって生成されたプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="651f5-119">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="651f5-120">$ hubConnection () によって作成されるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="651f5-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="651f5-121">Start メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="651f5-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="651f5-122">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="651f5-123">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="651f5-124">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="651f5-125">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="651f5-126">ハブクラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="651f5-127">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="651f5-128">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="651f5-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="651f5-129">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="651f5-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="651f5-130">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="651f5-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="651f5-131">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="651f5-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="651f5-132">サーバーまたは .NET クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="651f5-133">SignalR Hub API ガイド-サーバー</span><span class="sxs-lookup"><span data-stu-id="651f5-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="651f5-134">SignalR Hub API ガイド-.NET クライアント</span><span class="sxs-lookup"><span data-stu-id="651f5-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="651f5-135">API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。</span><span class="sxs-lookup"><span data-stu-id="651f5-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="651f5-136">.NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="651f5-137">生成されたプロキシとその機能</span><span class="sxs-lookup"><span data-stu-id="651f5-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="651f5-138">SignalR が生成するプロキシを使用して、または使用せずに、SignalR サービスと通信するように JavaScript クライアントをプログラミングできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="651f5-139">プロキシでは、接続に使用するコードの構文を簡略化し、サーバーが呼び出すメソッドを記述して、サーバーでメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="651f5-140">サーバーメソッドを呼び出すためのコードを記述すると、生成されたプロキシによって、ローカル関数を実行しているかのような構文を使用できるようになります。 `invoke('serverMethod', arg1, arg2)`ではなく `serverMethod(arg1, arg2)` を記述できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="651f5-141">また、生成されたプロキシ構文では、サーバーメソッド名を誤って指定した場合に、即時および intelligible のクライアント側エラーが有効になります。</span><span class="sxs-lookup"><span data-stu-id="651f5-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="651f5-142">また、プロキシを定義するファイルを手動で作成した場合は、サーバーメソッドを呼び出すコードを記述するための IntelliSense サポートを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="651f5-143">たとえば、サーバーに次のハブクラスがあるとします。</span><span class="sxs-lookup"><span data-stu-id="651f5-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="651f5-144">次のコード例は、サーバーで `NewContosoChatMessage` メソッドを呼び出し、サーバーから `addContosoChatMessageToPage` メソッドの呼び出しを受信するための JavaScript コードを示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="651f5-145">**生成されたプロキシを使用する**</span><span class="sxs-lookup"><span data-stu-id="651f5-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="651f5-146">**生成されたプロキシを使用しない場合**</span><span class="sxs-lookup"><span data-stu-id="651f5-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="651f5-147">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="651f5-147">When to use the generated proxy</span></span>

<span data-ttu-id="651f5-148">サーバーが呼び出すクライアントメソッドに対して複数のイベントハンドラーを登録する場合、生成されたプロキシを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="651f5-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="651f5-149">それ以外の場合は、コーディングの設定に基づいて、生成されたプロキシを使用するかどうかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="651f5-150">使用しない場合は、クライアントコードの `script` 要素で "signalr/hub" URL を参照する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="651f5-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="651f5-151">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="651f5-151">Client setup</span></span>

<span data-ttu-id="651f5-152">JavaScript クライアントには、jQuery および SignalR core JavaScript ファイルへの参照が必要です。</span><span class="sxs-lookup"><span data-stu-id="651f5-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="651f5-153">JQuery バージョンは、1.6.4、または1.7.2、1.8.2、1.9.1 などのメジャー以降のバージョンである必要があります。</span><span class="sxs-lookup"><span data-stu-id="651f5-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="651f5-154">生成されたプロキシを使用する場合は、SignalR によって生成されるプロキシ JavaScript ファイルへの参照も必要です。</span><span class="sxs-lookup"><span data-stu-id="651f5-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="651f5-155">次の例は、生成されたプロキシを使用する HTML ページで参照がどのように見えるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="651f5-156">これらの参照は、jQuery first、SignalR core、および SignalR proxy last という順序で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="651f5-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="651f5-157">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="651f5-158">前の例では、SignalR によって生成されるプロキシへの参照は、物理的なファイルではなく、動的に生成された JavaScript コードに対して行われます。</span><span class="sxs-lookup"><span data-stu-id="651f5-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="651f5-159">SignalR は、プロキシの JavaScript コードをその場で作成し、"/signalr/hubs" URL に応答してクライアントに提供します。</span><span class="sxs-lookup"><span data-stu-id="651f5-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="651f5-160">`MapHubs` メソッドでサーバーの SignalR 接続に別のベース URL を指定した場合、動的に生成されるプロキシファイルの URL は、"/hub" が追加されたカスタム URL になります。</span><span class="sxs-lookup"><span data-stu-id="651f5-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="651f5-161">Windows 8 (Windows ストア) JavaScript クライアントの場合は、動的に生成されたファイルではなく、物理プロキシファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="651f5-162">詳細については、このトピックの「 [SignalR generated プロキシの物理ファイルを作成する方法](#manualproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="651f5-163">ASP.NET MVC 4 Razor ビューで、チルダを使用して、プロキシファイルの参照でアプリケーションルートを参照します。</span><span class="sxs-lookup"><span data-stu-id="651f5-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="651f5-164">MVC 4 での SignalR の使用方法の詳細については、「 [With SignalR AND MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)」を参照してはじめにください。</span><span class="sxs-lookup"><span data-stu-id="651f5-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="651f5-165">ASP.NET MVC 3 Razor ビューでは、プロキシファイル参照に `Url.Content` を使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="651f5-166">ASP.NET Web フォームアプリケーションでは、プロキシファイル参照に `ResolveClientUrl` を使用するか、アプリルートの相対パス (チルダから始まる) を使用して ScriptManager で登録します。</span><span class="sxs-lookup"><span data-stu-id="651f5-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="651f5-167">一般的な規則として、CSS または JavaScript ファイルに使用する "/signalr/hubs" URL を指定する場合にも同じ方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="651f5-168">チルダを使用せずに URL を指定した場合、シナリオによっては IIS Express を使用して Visual Studio でテストしたときにアプリケーションが正常に動作しますが、完全な IIS に配置すると、404エラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="651f5-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="651f5-169">詳細については、MSDN サイトの「 [Visual Studio での Web サーバーでの ASP.NET Web プロジェクトの](https://msdn.microsoft.com/library/58wxa9w5.aspx)**ルートレベルリソースへの参照の解決**」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="651f5-170">Visual Studio 2012 でデバッグモードで web プロジェクトを実行するときに、ブラウザーとして Internet Explorer を使用している場合は、次の図に示すように、 **[スクリプトドキュメント]** の下の**ソリューションエクスプローラー**にプロキシファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![ソリューションエクスプローラーで生成された JavaScript のプロキシファイル](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="651f5-172">ファイルの内容を表示するには、 **[ハブ]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="651f5-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="651f5-173">Visual Studio 2012 および Internet Explorer を使用していない場合、またはデバッグモードになっていない場合は、"/signalR/hubs" URL を参照してファイルの内容を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="651f5-174">たとえば、サイトが `http://localhost:56699`で実行されている場合は、ブラウザーで `http://localhost:56699/SignalR/hubs` にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="651f5-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="651f5-175">SignalR によって生成されたプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="651f5-176">動的に生成されたプロキシの代わりに、プロキシコードを持つ物理ファイルを作成し、そのファイルを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="651f5-177">キャッシュやバンドル動作を制御したり、サーバーメソッドへの呼び出しをコーディングするときに IntelliSense を使用したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="651f5-178">プロキシファイルを作成するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="651f5-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="651f5-179">[SignalR](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="651f5-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="651f5-180">コマンドプロンプトを開き、SignalR ファイルが格納されている*tools*フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="651f5-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="651f5-181">Tools フォルダーは次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="651f5-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="651f5-182">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="651f5-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="651f5-183">*.Dll*へのパスは、通常、プロジェクトフォルダー内の*bin*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="651f5-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="651f5-184">このコマンドは、 *signalr*と同じフォルダーに、 *node.js*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="651f5-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="651f5-185">*サーバー .js*ファイルをプロジェクト内の適切なフォルダーに配置し、アプリケーションに合わせて名前を変更し、"signalr/hub" 参照の代わりに参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="651f5-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="651f5-186">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-186">How to establish a connection</span></span>

<span data-ttu-id="651f5-187">接続を確立するには、接続オブジェクトを作成し、プロキシを作成して、サーバーから呼び出すことができるメソッドのイベントハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="651f5-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="651f5-188">プロキシとイベントハンドラーがセットアップされたら、`start` メソッドを呼び出して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="651f5-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="651f5-189">生成されたプロキシを使用している場合は、独自のコードで接続オブジェクトを作成する必要はありません。これは、生成されたプロキシコードによって自動的に行われるためです。</span><span class="sxs-lookup"><span data-stu-id="651f5-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="651f5-190">**(生成されたプロキシを使用して) 接続を確立します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="651f5-191">**(生成されたプロキシを使用せずに) 接続を確立します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="651f5-192">このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="651f5-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="651f5-193">別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="651f5-194">通常は、`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="651f5-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="651f5-195">接続の確立後にいくつかのイベントハンドラーを登録する場合は、これを行うことができますが、`start` メソッドを呼び出す前に、少なくとも1つのイベントハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="651f5-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="651f5-196">その理由の1つは、アプリケーションに多数のハブが存在する可能性がありますが、そのうちの1つだけを使用する場合は、すべてのハブで `OnConnected` イベントをトリガーしないことです。</span><span class="sxs-lookup"><span data-stu-id="651f5-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="651f5-197">接続が確立されると、ハブのプロキシにクライアントメソッドが存在することによって、`OnConnected` イベントをトリガーするように SignalR に指示します。</span><span class="sxs-lookup"><span data-stu-id="651f5-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="651f5-198">`start` メソッドを呼び出す前にイベントハンドラーを登録しないと、ハブでメソッドを呼び出すことができますが、ハブの `OnConnected` メソッドは呼び出されず、サーバーからクライアントメソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="651f5-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="651f5-199">$ hubConnection () によって作成されるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="651f5-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="651f5-200">例からわかるように、生成されたプロキシを使用すると、`$.connection.hub` は接続オブジェクトを参照します。</span><span class="sxs-lookup"><span data-stu-id="651f5-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="651f5-201">これは、生成されたプロキシを使用していない場合に `$.hubConnection()` を呼び出すことによって得られるオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="651f5-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="651f5-202">生成されたプロキシコードは、次のステートメントを実行して、接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="651f5-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![生成されたプロキシファイルでの接続の作成](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="651f5-204">生成されたプロキシを使用している場合は、生成されたプロキシを使用していないときに接続オブジェクトで実行できる `$.connection.hub` で何でも実行できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="651f5-205">Start メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="651f5-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="651f5-206">`start` メソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="651f5-207">[JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。これは、`pipe`、`done`、`fail`などのメソッドを呼び出すことによってコールバック関数を追加できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="651f5-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="651f5-208">サーバーメソッドの呼び出しなど、接続が確立された後に実行するコードがある場合は、そのコードをコールバック関数に配置するか、コールバック関数から呼び出します。</span><span class="sxs-lookup"><span data-stu-id="651f5-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="651f5-209">`.done` のコールバックメソッドは、接続が確立された後、サーバーの `OnConnected` イベントハンドラーメソッドにあるコードの実行が完了した後に実行されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="651f5-210">前の例の "現在接続されている" ステートメントを、(`.done` コールバックではなく) `start` メソッド呼び出しの後の次のコード行として配置すると、次の例に示すように、接続が確立される前に `console.log` 行が実行されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![接続が確立された後に実行されるコードを記述する方法が正しくありません](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="651f5-212">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="651f5-213">通常、ブラウザーが `http://contoso.com`からページを読み込む場合、SignalR 接続は `http://contoso.com/signalr`の同じドメインにあります。</span><span class="sxs-lookup"><span data-stu-id="651f5-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="651f5-214">`http://contoso.com` のページが `http://fabrikam.com/signalr`に接続する場合は、ドメイン間接続が使用されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="651f5-215">セキュリティ上の理由から、ドメイン間接続は既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="651f5-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="651f5-216">ドメイン間接続を確立するには、サーバーでドメイン間接続が有効になっていることを確認し、接続オブジェクトを作成するときに接続 URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="651f5-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="651f5-217">SignalR は、 [JSONP](http://en.wikipedia.org/wiki/JSONP)や[CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)など、ドメイン間接続に適したテクノロジを使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="651f5-218">サーバーで、`MapHubs` メソッドを呼び出すときにこのオプションを選択して、ドメイン間接続を有効にします。</span><span class="sxs-lookup"><span data-stu-id="651f5-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="651f5-219">クライアントで、(生成されたプロキシを使用せずに) 接続オブジェクトを作成するとき、または (生成されたプロキシを使用して) start メソッドを呼び出す前に、URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="651f5-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="651f5-220">**ドメイン間接続 (生成されたプロキシを使用) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="651f5-221">**ドメイン間接続 (生成されたプロキシを使用しない) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="651f5-222">`$.hubConnection` コンストラクターを使用する場合、URL に `signalr` を含める必要はありません。これは、`useDefaultUrl` を `false`として指定しない限り、自動的に追加されるためです。</span><span class="sxs-lookup"><span data-stu-id="651f5-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="651f5-223">異なるエンドポイントへの複数の接続を作成できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="651f5-224">コードで `jQuery.support.cors` を true に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="651f5-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![JQuery. サポートを true に設定しない](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="651f5-226">SignalR は、JSONP または CORS の使用を処理します。</span><span class="sxs-lookup"><span data-stu-id="651f5-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="651f5-227">`jQuery.support.cors` を true に設定すると、ブラウザーが CORS をサポートしていると SignalR が想定するため、JSONP は無効になります。</span><span class="sxs-lookup"><span data-stu-id="651f5-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="651f5-228">Localhost URL に接続している場合、Internet Explorer 10 はドメイン間接続を考慮しないため、サーバーでドメイン間接続を有効にしていない場合でも、アプリケーションは IE 10 でローカルに動作します。</span><span class="sxs-lookup"><span data-stu-id="651f5-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="651f5-229">Internet Explorer 9 でドメイン間接続を使用する方法の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="651f5-230">Chrome でのクロスドメイン接続の使用の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="651f5-231">このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="651f5-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="651f5-232">別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="651f5-233">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-233">How to configure the connection</span></span>

<span data-ttu-id="651f5-234">接続を確立する前に、クエリ文字列パラメーターを指定することも、トランスポートメソッドを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="651f5-235">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-235">How to specify query string parameters</span></span>

<span data-ttu-id="651f5-236">クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="651f5-237">次の例は、クライアントコードでクエリ文字列パラメーターを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="651f5-238">**(生成されたプロキシを使用して) start メソッドを呼び出す前に、クエリ文字列の値を設定します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="651f5-239">**Start メソッドを呼び出す前に (生成されたプロキシを使用せずに) クエリ文字列の値を設定する**</span><span class="sxs-lookup"><span data-stu-id="651f5-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="651f5-240">次の例は、サーバーコードでクエリ文字列パラメーターを読み取る方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="651f5-241">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-241">How to specify the transport method</span></span>

<span data-ttu-id="651f5-242">接続プロセスの一環として、SignalR クライアントは、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定するために、通常はサーバーとネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="651f5-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="651f5-243">使用するトランスポートが既にわかっている場合は、`start` メソッドを呼び出すときにトランスポートメソッドを指定することで、このネゴシエーションプロセスを省略できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="651f5-244">**(生成されたプロキシを使用して) トランスポートメソッドを指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="651f5-245">**トランスポートメソッド (生成されたプロキシを除く) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="651f5-246">別の方法として、複数のトランスポートメソッドを SignalR で試行する順序で指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="651f5-247">**カスタムトランスポートフォールバックスキーム (生成されたプロキシを含む) を指定するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="651f5-248">**カスタムトランスポートフォールバックスキームを指定するクライアントコード (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="651f5-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="651f5-249">次の値を使用して、トランスポート方法を指定できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="651f5-250">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="651f5-250">"webSockets"</span></span>
- <span data-ttu-id="651f5-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="651f5-251">"foreverFrame"</span></span>
- <span data-ttu-id="651f5-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="651f5-252">"serverSentEvents"</span></span>
- <span data-ttu-id="651f5-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="651f5-253">"longPolling"</span></span>

<span data-ttu-id="651f5-254">次の例は、接続で使用されているトランスポートメソッドを調べる方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="651f5-255">**接続で使用されるトランスポートメソッド (生成されたプロキシを含む) を表示するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="651f5-256">**(生成されたプロキシを使用せずに) 接続で使用されるトランスポートメソッドを表示するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="651f5-257">サーバーコードでトランスポート方法を確認する方法については、「 [ASP.NET SignalR HUB API Guide-server-Context プロパティからクライアントに関する情報を取得する方法](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="651f5-258">トランスポートとフォールバックの詳細については、「 [SignalR とフォールバックの概要](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="651f5-259">ハブクラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="651f5-260">作成した各接続オブジェクトは、1つ以上のハブクラスを含む SignalR サービスへの接続に関する情報をカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="651f5-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="651f5-261">ハブクラスと通信するには、自分で作成したプロキシオブジェクト (生成されたプロキシを使用していない場合) または生成されたプロキシオブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="651f5-262">クライアントでは、プロキシ名はハブクラス名の camel 形式のバージョンです。</span><span class="sxs-lookup"><span data-stu-id="651f5-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="651f5-263">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="651f5-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="651f5-264">**サーバー上のハブクラス**</span><span class="sxs-lookup"><span data-stu-id="651f5-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="651f5-265">**ハブに対して生成されたクライアントプロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="651f5-266">**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**</span><span class="sxs-lookup"><span data-stu-id="651f5-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="651f5-267">`HubName` 属性を使用してハブクラスを装飾する場合は、大文字小文字を変更せずに正確な名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="651f5-268">**HubName 属性を持つサーバーのハブクラス**</span><span class="sxs-lookup"><span data-stu-id="651f5-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="651f5-269">**ハブに対して生成されたクライアントプロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="651f5-270">**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**</span><span class="sxs-lookup"><span data-stu-id="651f5-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="651f5-271">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="651f5-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="651f5-272">サーバーがハブから呼び出すことができるメソッドを定義するには、生成されたプロキシの `client` プロパティを使用してハブプロキシにイベントハンドラーを追加するか、生成されたプロキシを使用しない場合は `on` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="651f5-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="651f5-273">パラメーターには、複雑なオブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="651f5-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="651f5-274">`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="651f5-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="651f5-275">(`start` メソッドを呼び出した後にイベントハンドラーを追加する場合は、このドキュメントの「[接続を確立する方法](#establishconnection)」のメモを参照し、生成されたプロキシを使用せずにメソッドを定義するために示されている構文を使用します)。</span><span class="sxs-lookup"><span data-stu-id="651f5-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="651f5-276">メソッド名の一致では、大文字と小文字が区別されません。</span><span class="sxs-lookup"><span data-stu-id="651f5-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="651f5-277">たとえば、サーバー上の `Clients.All.addContosoChatMessageToPage` は、クライアントで `AddContosoChatMessageToPage`、`addContosoChatMessageToPage`、または `addcontosochatmessagetopage` を実行します。</span><span class="sxs-lookup"><span data-stu-id="651f5-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="651f5-278">**クライアントで (生成されたプロキシを使用して) メソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="651f5-279">**クライアントでメソッドを定義する別の方法 (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="651f5-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="651f5-280">**クライアントでメソッドを定義します (生成されたプロキシを使用しない場合、または start メソッドを呼び出した後にを追加する場合)**</span><span class="sxs-lookup"><span data-stu-id="651f5-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="651f5-281">**クライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="651f5-282">次の例には、メソッドパラメーターとしての複合オブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="651f5-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="651f5-283">**(生成されたプロキシを使用して) 複雑なオブジェクトを受け取るクライアントのメソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="651f5-284">**複合オブジェクト (生成されたプロキシを使用しない) を受け取るクライアントのメソッドを定義します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="651f5-285">**複合オブジェクトを定義するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="651f5-286">**複合オブジェクトを使用してクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="651f5-287">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="651f5-287">How to call server methods from the client</span></span>

<span data-ttu-id="651f5-288">クライアントからサーバーメソッドを呼び出すには、生成されたプロキシを使用していない場合は、生成されたプロキシの `server` プロパティを使用するか、ハブプロキシで `invoke` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="651f5-289">戻り値またはパラメーターは、複雑なオブジェクトにすることができます。</span><span class="sxs-lookup"><span data-stu-id="651f5-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="651f5-290">ハブのメソッド名の camel 形式のバージョンを渡します。</span><span class="sxs-lookup"><span data-stu-id="651f5-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="651f5-291">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="651f5-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="651f5-292">次の例は、戻り値を持たないサーバーメソッドを呼び出す方法と、戻り値を持つサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="651f5-293">**HubMethodName 属性のないサーバーメソッド**</span><span class="sxs-lookup"><span data-stu-id="651f5-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="651f5-294">**パラメーターで渡される複合オブジェクトを定義するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="651f5-295">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="651f5-296">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="651f5-297">`HubMethodName` 属性を使用してハブメソッドを修飾した場合は、大文字小文字を変更せずにその名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="651f5-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="651f5-298">HubMethodName 属性を持つ**サーバーメソッド**</span><span class="sxs-lookup"><span data-stu-id="651f5-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="651f5-299">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="651f5-300">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="651f5-301">前の例は、戻り値を持たないサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="651f5-302">次の例は、戻り値を持つサーバーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="651f5-303">**戻り値を持つメソッドのサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="651f5-304">戻り値**に使用されるストッククラス**</span><span class="sxs-lookup"><span data-stu-id="651f5-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="651f5-305">**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="651f5-306">**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="651f5-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="651f5-307">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="651f5-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="651f5-308">SignalR は、次のように処理できる接続の有効期間イベントを提供します。</span><span class="sxs-lookup"><span data-stu-id="651f5-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="651f5-309">`starting`: 接続を介してデータが送信される前に発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="651f5-310">`received`: 接続でデータを受信したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="651f5-311">受信したデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="651f5-311">Provides the received data.</span></span>
- <span data-ttu-id="651f5-312">`connectionSlow`: クライアントが低速または頻繁に切断される接続を検出したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="651f5-313">`reconnecting`: 基になるトランスポートが再接続を開始したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="651f5-314">`reconnected`: 基になるトランスポートが再接続されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="651f5-315">`stateChanged`: 接続状態が変化したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="651f5-316">以前の状態と新しい状態 (接続、接続、再接続、または切断) を提供します。</span><span class="sxs-lookup"><span data-stu-id="651f5-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="651f5-317">`disconnected`: 接続が切断されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="651f5-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="651f5-318">たとえば、遅延が発生する可能性がある接続の問題が発生した場合に警告メッセージを表示するには、`connectionSlow` イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="651f5-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="651f5-319">**(生成されたプロキシを使用して) connectionSlow イベントを処理します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="651f5-320">**(生成されたプロキシを使用せずに) connectionSlow イベントを処理する**</span><span class="sxs-lookup"><span data-stu-id="651f5-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="651f5-321">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="651f5-322">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="651f5-322">How to handle errors</span></span>

<span data-ttu-id="651f5-323">SignalR JavaScript クライアントには、ハンドラーを追加できる `error` イベントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="651f5-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="651f5-324">また、fail メソッドを使用して、サーバーメソッド呼び出しによって発生するエラーのハンドラーを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="651f5-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="651f5-325">サーバーで詳細なエラーメッセージを明示的に有効にしないと、エラーに関する最小限の情報が、エラーの後に SignalR によって返される例外オブジェクトに含まれます。</span><span class="sxs-lookup"><span data-stu-id="651f5-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="651f5-326">たとえば、`newContosoChatMessage` の呼び出しが失敗した場合、エラーオブジェクトのエラーメッセージには、セキュリティ上の理由により、実稼働環境でクライアントに詳細なエラーメッセージを送信する "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" が含まれます。ただし、トラブルシューティングのために詳細なエラーメッセージを有効にする場合は、サーバーで次のコードを使用してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="651f5-327">次の例は、エラーイベントのハンドラーを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="651f5-328">**(生成されたプロキシを使用して) エラーハンドラーを追加します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="651f5-329">**(生成されたプロキシを使用せずに) エラーハンドラーを追加します。**</span><span class="sxs-lookup"><span data-stu-id="651f5-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="651f5-330">次の例は、メソッドの呼び出しからエラーを処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="651f5-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="651f5-331">**メソッドの呼び出し (生成されたプロキシを使用) からのエラーを処理する**</span><span class="sxs-lookup"><span data-stu-id="651f5-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="651f5-332">**(生成されたプロキシを使用せずに) メソッド呼び出しからのエラーを処理する**</span><span class="sxs-lookup"><span data-stu-id="651f5-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="651f5-333">メソッドの呼び出しが失敗した場合は、`error` イベントも発生します。そのため、`error` メソッドハンドラー内のコードと `.fail` メソッドのコールバックが実行されます。</span><span class="sxs-lookup"><span data-stu-id="651f5-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="651f5-334">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="651f5-334">How to enable client-side logging</span></span>

<span data-ttu-id="651f5-335">接続でクライアント側のログ記録を有効にするには、接続オブジェクトの `logging` プロパティを設定してから、`start` メソッドを呼び出して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="651f5-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="651f5-336">**(生成されたプロキシを使用して) ログ記録を有効にする**</span><span class="sxs-lookup"><span data-stu-id="651f5-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="651f5-337">**(生成されたプロキシを使用しない) ログ記録を有効にする**</span><span class="sxs-lookup"><span data-stu-id="651f5-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="651f5-338">ログを表示するには、ブラウザーの開発者ツールを開き、[コンソール] タブにアクセスします。これを行う方法を示す詳細な手順とスクリーンショットを示すチュートリアルについては、「 [ASP.NET Signalr を使用したサーバーブロードキャスト-ログ記録を有効](index.md)にする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="651f5-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
