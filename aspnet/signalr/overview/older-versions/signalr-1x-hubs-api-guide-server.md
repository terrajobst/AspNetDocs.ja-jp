---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR Hub API ガイド-サーバー (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: このドキュメントでは、SignalR バージョン1.1 用の ASP.NET SignalR Hub API のサーバー側のプログラミングの概要について説明します。コードサンプル demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468130"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="30193-103">ASP.NET SignalR Hub API ガイド-サーバー (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="30193-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="30193-104">[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="30193-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="30193-105">このドキュメントでは、SignalR バージョン1.1 用の ASP.NET SignalR Hub API のサーバー側のプログラミングの概要について説明し、一般的なオプションを示すコードサンプルを示します。</span><span class="sxs-lookup"><span data-stu-id="30193-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="30193-106">SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="30193-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="30193-107">サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="30193-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="30193-108">クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="30193-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="30193-109">SignalR は、クライアントとサーバーのすべての組み込みを処理します。</span><span class="sxs-lookup"><span data-stu-id="30193-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="30193-110">SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。</span><span class="sxs-lookup"><span data-stu-id="30193-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="30193-111">SignalR、ハブ、および永続的な接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては、[はじめに SignalR](index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="30193-112">概要</span><span class="sxs-lookup"><span data-stu-id="30193-112">Overview</span></span>

<span data-ttu-id="30193-113">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="30193-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="30193-114">SignalR ルートを登録して SignalR オプションを構成する方法</span><span class="sxs-lookup"><span data-stu-id="30193-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="30193-115">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="30193-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="30193-116">SignalR オプションの構成</span><span class="sxs-lookup"><span data-stu-id="30193-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="30193-117">ハブクラスを作成して使用する方法</span><span class="sxs-lookup"><span data-stu-id="30193-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="30193-118">ハブオブジェクトの有効期間</span><span class="sxs-lookup"><span data-stu-id="30193-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="30193-119">JavaScript クライアントでのハブ名の camel 形式</span><span class="sxs-lookup"><span data-stu-id="30193-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="30193-120">複数のハブ</span><span class="sxs-lookup"><span data-stu-id="30193-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="30193-121">クライアントが呼び出すことのできるハブクラスのメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="30193-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="30193-122">JavaScript クライアントでのメソッド名の camel 形式の表記</span><span class="sxs-lookup"><span data-stu-id="30193-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="30193-123">非同期的に実行する場合</span><span class="sxs-lookup"><span data-stu-id="30193-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="30193-124">オーバーロードの定義</span><span class="sxs-lookup"><span data-stu-id="30193-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="30193-125">ハブクラスからクライアントメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="30193-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="30193-126">RPC を受信するクライアントを選択する</span><span class="sxs-lookup"><span data-stu-id="30193-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="30193-127">メソッド名に対するコンパイル時の検証がありません</span><span class="sxs-lookup"><span data-stu-id="30193-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="30193-128">大文字と小文字を区別しないメソッド名の一致</span><span class="sxs-lookup"><span data-stu-id="30193-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="30193-129">非同期実行</span><span class="sxs-lookup"><span data-stu-id="30193-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="30193-130">ハブクラスからグループメンバーシップを管理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="30193-131">Add メソッドと Remove メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="30193-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="30193-132">グループメンバーシップの永続化</span><span class="sxs-lookup"><span data-stu-id="30193-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="30193-133">シングルユーザーグループ</span><span class="sxs-lookup"><span data-stu-id="30193-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="30193-134">ハブクラスで接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="30193-135">OnConnected、Onconnected、および Onconnected が呼び出されたとき</span><span class="sxs-lookup"><span data-stu-id="30193-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="30193-136">呼び出し元の状態が設定されていません</span><span class="sxs-lookup"><span data-stu-id="30193-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="30193-137">コンテキストプロパティからクライアントに関する情報を取得する方法</span><span class="sxs-lookup"><span data-stu-id="30193-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="30193-138">クライアントとハブクラスの間で状態を渡す方法</span><span class="sxs-lookup"><span data-stu-id="30193-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="30193-139">ハブクラスでエラーを処理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="30193-140">ハブクラスの外部からクライアントメソッドを呼び出し、グループを管理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="30193-141">クライアントメソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="30193-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="30193-142">グループメンバーシップの管理</span><span class="sxs-lookup"><span data-stu-id="30193-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="30193-143">トレースを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="30193-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="30193-144">ハブパイプラインをカスタマイズする方法</span><span class="sxs-lookup"><span data-stu-id="30193-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="30193-145">クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="30193-146">SignalR Hub API ガイド-JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="30193-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="30193-147">SignalR Hub API ガイド-.NET クライアント</span><span class="sxs-lookup"><span data-stu-id="30193-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="30193-148">API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。</span><span class="sxs-lookup"><span data-stu-id="30193-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="30193-149">.NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="30193-150">SignalR ルートを登録して SignalR オプションを構成する方法</span><span class="sxs-lookup"><span data-stu-id="30193-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="30193-151">クライアントがハブへの接続に使用するルートを定義するには、アプリケーションの起動時に[Maphubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx)メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="30193-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="30193-152">`MapHubs` は、`System.Web.Routing.RouteCollection` クラスの[拡張メソッド](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="30193-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="30193-153">次の例は、 *global.asax*ファイルで SignalR hub ルートを定義する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="30193-154">SignalR 機能を ASP.NET MVC アプリケーションに追加する場合は、SignalR ルートが他のルートの前に追加されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="30193-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="30193-155">詳しくは、「[チュートリアル: SignalR と MVC 4](index.md)ではじめにます。</span><span class="sxs-lookup"><span data-stu-id="30193-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="30193-156">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="30193-156">The /signalr URL</span></span>

<span data-ttu-id="30193-157">既定では、クライアントがハブへの接続に使用するルート URL は "/signalr" です。</span><span class="sxs-lookup"><span data-stu-id="30193-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="30193-158">(この URL は、自動的に生成された JavaScript ファイルの "/signalr/hubs" URL と混同しないでください。</span><span class="sxs-lookup"><span data-stu-id="30193-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="30193-159">生成されたプロキシの詳細については、「 [SignalR HUB API Guide-JavaScript Client-生成されたプロキシとその機能](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="30193-160">このベース URL を SignalR で使用できないような状況が発生する可能性があります。たとえば、 *signalr*という名前のフォルダーがプロジェクトにあり、その名前を変更したくないとします。</span><span class="sxs-lookup"><span data-stu-id="30193-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="30193-161">その場合は、次の例に示すように、ベース URL を変更できます (サンプルコードの "/signalr" は目的の URL に置き換えてください)。</span><span class="sxs-lookup"><span data-stu-id="30193-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="30193-162">**URL を指定するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="30193-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="30193-163">**URL (生成されたプロキシを含む) を指定する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="30193-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="30193-164">**URL (生成されたプロキシを除く) を指定する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="30193-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="30193-165">**URL を指定する .NET クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="30193-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="30193-166">SignalR オプションの構成</span><span class="sxs-lookup"><span data-stu-id="30193-166">Configuring SignalR Options</span></span>

<span data-ttu-id="30193-167">`MapHubs` メソッドのオーバーロードを使用すると、カスタム URL、カスタム依存関係競合回避モジュール、および次のオプションを指定できます。</span><span class="sxs-lookup"><span data-stu-id="30193-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="30193-168">ブラウザークライアントからのクロスドメイン呼び出しを有効にします。</span><span class="sxs-lookup"><span data-stu-id="30193-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="30193-169">通常、ブラウザーが `http://contoso.com`からページを読み込む場合、SignalR 接続は `http://contoso.com/signalr`の同じドメインにあります。</span><span class="sxs-lookup"><span data-stu-id="30193-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="30193-170">`http://contoso.com` のページが `http://fabrikam.com/signalr`に接続する場合は、ドメイン間接続が使用されます。</span><span class="sxs-lookup"><span data-stu-id="30193-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="30193-171">セキュリティ上の理由から、ドメイン間接続は既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="30193-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="30193-172">詳細については、「 [ASP.NET SignalR HUB API Guide-JavaScript Client-クロスドメイン接続を確立する方法](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="30193-173">詳細なエラーメッセージを有効にします。</span><span class="sxs-lookup"><span data-stu-id="30193-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="30193-174">エラーが発生した場合、SignalR の既定の動作では、何が起こったかについての詳細がなくても、クライアントに通知メッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="30193-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="30193-175">悪意のあるユーザーがアプリケーションに対する攻撃に関する情報を使用できる可能性があるため、実稼働環境では詳細なエラー情報をクライアントに送信することはお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="30193-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="30193-176">トラブルシューティングのために、このオプションを使用して、より詳細なエラー報告を一時的に有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="30193-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="30193-177">自動的に生成された JavaScript プロキシファイルを無効にします。</span><span class="sxs-lookup"><span data-stu-id="30193-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="30193-178">既定では、ハブクラスのプロキシを含む JavaScript ファイルが、URL "/signalr/hubs" への応答として生成されます。</span><span class="sxs-lookup"><span data-stu-id="30193-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="30193-179">JavaScript プロキシを使用しない場合、またはこのファイルを手動で生成してクライアント内の物理ファイルを参照する場合は、このオプションを使用してプロキシ生成を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="30193-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="30193-180">詳細については、「 [SignalR HUB API Guide-JavaScript Client-SignalR によって生成されたプロキシの物理ファイルを作成する方法](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="30193-181">次の例は、`MapHubs` メソッドの呼び出しで SignalR 接続 URL とこれらのオプションを指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="30193-182">カスタム URL を指定するには、例の "/signalr" を使用する URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="30193-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="30193-183">ハブクラスを作成して使用する方法</span><span class="sxs-lookup"><span data-stu-id="30193-183">How to create and use Hub classes</span></span>

<span data-ttu-id="30193-184">ハブを作成するには、 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)から派生するクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="30193-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="30193-185">次の例は、チャットアプリケーションの単純なハブクラスを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="30193-186">この例では、接続されたクライアントが `NewContosoChatMessage` メソッドを呼び出すことができ、受信したデータは、接続されているすべてのクライアントにブロードキャストされます。</span><span class="sxs-lookup"><span data-stu-id="30193-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="30193-187">ハブオブジェクトの有効期間</span><span class="sxs-lookup"><span data-stu-id="30193-187">Hub object lifetime</span></span>

<span data-ttu-id="30193-188">ハブクラスをインスタンス化したり、サーバー上の独自のコードからそのメソッドを呼び出したりすることはありません。SignalR Hub パイプラインによって実行されるすべての処理です。</span><span class="sxs-lookup"><span data-stu-id="30193-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="30193-189">SignalR は、クライアントがサーバーへの接続、切断、またはメソッド呼び出しを行うときなどのハブ操作を処理する必要があるたびに、ハブクラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="30193-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="30193-190">ハブクラスのインスタンスは一時的なものであるため、次のメソッド呼び出しの状態を維持するためにそれらを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="30193-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="30193-191">サーバーがクライアントからメソッド呼び出しを受け取るたびに、ハブクラスの新しいインスタンスによってメッセージが処理されます。</span><span class="sxs-lookup"><span data-stu-id="30193-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="30193-192">複数の接続とメソッド呼び出しによって状態を維持するには、データベースなどの他のメソッド、またはハブクラスの静的変数、または `Hub`から派生していない別のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="30193-193">データをメモリに保持する場合、ハブクラスの静的変数などのメソッドを使用すると、アプリドメインがリサイクルされるときにデータが失われます。</span><span class="sxs-lookup"><span data-stu-id="30193-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="30193-194">ハブクラスの外部で実行されている独自のコードからクライアントにメッセージを送信する場合、ハブクラスのインスタンスをインスタンス化することはできませんが、ハブクラスの SignalR context オブジェクトへの参照を取得することで実行できます。</span><span class="sxs-lookup"><span data-stu-id="30193-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="30193-195">詳細については、このトピックで後述[する「クライアントメソッドを呼び出し、ハブクラスの外部からグループを管理する方法](#callfromoutsidehub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="30193-196">JavaScript クライアントでのハブ名の camel 形式</span><span class="sxs-lookup"><span data-stu-id="30193-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="30193-197">既定では、JavaScript クライアントは、camel 形式のクラス名を使用してハブを参照します。</span><span class="sxs-lookup"><span data-stu-id="30193-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="30193-198">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="30193-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="30193-199">前の例は、JavaScript コードでは `contosoChatHub` と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="30193-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="30193-200">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="30193-201">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="30193-202">クライアントに使用する別の名前を指定する場合は、`HubName` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="30193-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="30193-203">`HubName` 属性を使用する場合、JavaScript クライアントでの camel 形式の変更はありません。</span><span class="sxs-lookup"><span data-stu-id="30193-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="30193-204">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="30193-205">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="30193-206">複数のハブ</span><span class="sxs-lookup"><span data-stu-id="30193-206">Multiple Hubs</span></span>

<span data-ttu-id="30193-207">アプリケーションでは、複数のハブクラスを定義できます。</span><span class="sxs-lookup"><span data-stu-id="30193-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="30193-208">これを行うと、接続は共有されますが、グループは分離されます。</span><span class="sxs-lookup"><span data-stu-id="30193-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="30193-209">すべてのクライアントは、同じ URL を使用して、サービス ("/signalr" またはカスタム URL を指定した場合はカスタム URL) との SignalR 接続を確立し、サービスで定義されているすべてのハブに対してその接続が使用されます。</span><span class="sxs-lookup"><span data-stu-id="30193-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="30193-210">1つのクラスですべてのハブ機能を定義する場合と比較して、複数のハブでパフォーマンスの違いはありません。</span><span class="sxs-lookup"><span data-stu-id="30193-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="30193-211">すべてのハブは、同じ HTTP 要求情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="30193-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="30193-212">すべてのハブが同じ接続を共有するため、サーバーが取得する唯一の HTTP 要求情報は、SignalR 接続を確立する元の HTTP 要求に含まれるものです。</span><span class="sxs-lookup"><span data-stu-id="30193-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="30193-213">接続要求を使用してクエリ文字列を指定することによってクライアントからサーバーに情報を渡す場合、異なるハブに対して異なるクエリ文字列を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="30193-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="30193-214">すべてのハブは同じ情報を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="30193-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="30193-215">生成された JavaScript プロキシファイルには、1つのファイル内のすべてのハブのプロキシが含まれます。</span><span class="sxs-lookup"><span data-stu-id="30193-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="30193-216">JavaScript プロキシの詳細については、「 [SignalR HUB API Guide-Javascript Client-生成されたプロキシとその機能](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="30193-217">グループはハブ内で定義されます。</span><span class="sxs-lookup"><span data-stu-id="30193-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="30193-218">SignalR では、接続されたクライアントのサブセットにブロードキャストする名前付きグループを定義できます。</span><span class="sxs-lookup"><span data-stu-id="30193-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="30193-219">グループは、ハブごとに個別に保持されます。</span><span class="sxs-lookup"><span data-stu-id="30193-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="30193-220">たとえば、"Administrators" という名前のグループには、`ContosoChatHub` クラスのクライアントセットが1つ含まれており、同じグループ名が `StockTickerHub` クラスの異なるクライアントセットを参照しています。</span><span class="sxs-lookup"><span data-stu-id="30193-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="30193-221">クライアントが呼び出すことのできるハブクラスのメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="30193-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="30193-222">クライアントから呼び出すことができるようにする、ハブのメソッドを公開するには、次の例に示すようにパブリックメソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="30193-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="30193-223">任意の C# のメソッドの場合と同様に、戻り値の型とパラメーター (複合型や配列を含む) を指定できます。</span><span class="sxs-lookup"><span data-stu-id="30193-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="30193-224">パラメーターで受け取った、または呼び出し元に返されたすべてのデータは、JSON を使用してクライアントとサーバーの間で通信されます。また、SignalR は、複雑なオブジェクトとオブジェクトの配列のバインドを自動的に処理します。</span><span class="sxs-lookup"><span data-stu-id="30193-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="30193-225">JavaScript クライアントでのメソッド名の camel 形式の表記</span><span class="sxs-lookup"><span data-stu-id="30193-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="30193-226">既定では、JavaScript クライアントは、camel 形式のメソッド名を使用してハブメソッドを参照します。</span><span class="sxs-lookup"><span data-stu-id="30193-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="30193-227">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="30193-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="30193-228">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="30193-229">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="30193-230">クライアントに使用する別の名前を指定する場合は、`HubMethodName` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="30193-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="30193-231">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="30193-232">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="30193-233">非同期的に実行する場合</span><span class="sxs-lookup"><span data-stu-id="30193-233">When to execute asynchronously</span></span>

<span data-ttu-id="30193-234">メソッドが長時間実行される場合、またはデータベースの参照や web サービスの呼び出しなどの待機が必要な処理を実行する必要がある場合は、[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (戻り値 `void` の型 `T` の代わりに) [タスク&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) オブジェクトを返すことによって、ハブメソッドを非同期にします。</span><span class="sxs-lookup"><span data-stu-id="30193-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="30193-235">メソッドから `Task` オブジェクトを返すと、SignalR は `Task` が完了するまで待機してから、ラップされていない結果をクライアントに返します。そのため、クライアントでメソッド呼び出しをコーディングする方法に違いはありません。</span><span class="sxs-lookup"><span data-stu-id="30193-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="30193-236">ハブメソッドを非同期にすると、WebSocket トランスポートを使用するときに接続がブロックされることが回避されます。</span><span class="sxs-lookup"><span data-stu-id="30193-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="30193-237">ハブメソッドが同期的に実行され、トランスポートが WebSocket の場合、同じクライアントからのハブでの後続のメソッドの呼び出しは、ハブメソッドが完了するまでブロックされます。</span><span class="sxs-lookup"><span data-stu-id="30193-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="30193-238">次の例は、同期的または非同期的に実行するようにコード化された同じメソッドと、いずれかのバージョンの呼び出しに使用できる JavaScript クライアントコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="30193-239">**式**</span><span class="sxs-lookup"><span data-stu-id="30193-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="30193-240">**ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="30193-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="30193-241">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="30193-242">ASP.NET 4.5 で非同期メソッドを使用する方法の詳細については、「 [ASP.NET MVC 4 での非同期メソッドの使用](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="30193-243">オーバーロードの定義</span><span class="sxs-lookup"><span data-stu-id="30193-243">Defining Overloads</span></span>

<span data-ttu-id="30193-244">メソッドのオーバーロードを定義する場合は、各オーバーロードのパラメーターの数が異なる必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="30193-245">異なるパラメーターの型を指定するだけでオーバーロードを区別する場合、ハブクラスはコンパイルされますが、クライアントがいずれかのオーバーロードを呼び出そうとすると、実行時に SignalR サービスによって例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="30193-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="30193-246">ハブクラスからクライアントメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="30193-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="30193-247">サーバーからクライアントメソッドを呼び出すには、ハブクラスのメソッドで `Clients` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="30193-248">次の例は、すべての接続されたクライアントで `addNewMessageToPage` を呼び出すサーバーコードと、JavaScript クライアントでメソッドを定義するクライアントコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="30193-249">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="30193-250">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="30193-251">クライアントメソッドから戻り値を取得することはできません。`int x = Clients.All.add(1,1)` などの構文は機能しません。</span><span class="sxs-lookup"><span data-stu-id="30193-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="30193-252">パラメーターの複合型と配列を指定できます。</span><span class="sxs-lookup"><span data-stu-id="30193-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="30193-253">次の例では、メソッドパラメーターでクライアントに複合型を渡します。</span><span class="sxs-lookup"><span data-stu-id="30193-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="30193-254">**複合オブジェクトを使用してクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="30193-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="30193-255">**複合オブジェクトを定義するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="30193-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="30193-256">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="30193-257">RPC を受信するクライアントを選択する</span><span class="sxs-lookup"><span data-stu-id="30193-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="30193-258">Clients プロパティは、RPC を受信するクライアントを指定するためのいくつかのオプションを提供する[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="30193-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="30193-259">接続されたすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="30193-260">呼び出し元のクライアントのみ。</span><span class="sxs-lookup"><span data-stu-id="30193-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="30193-261">呼び出し元のクライアントを除くすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="30193-262">接続 ID で識別される特定のクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="30193-263">この例では、呼び出し元のクライアントで `addContosoChatMessageToPage` を呼び出し、`Clients.Caller`を使用した場合と同じ効果があります。</span><span class="sxs-lookup"><span data-stu-id="30193-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="30193-264">指定したクライアントを除くすべての接続されているクライアント。接続 ID で識別されます。</span><span class="sxs-lookup"><span data-stu-id="30193-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="30193-265">指定したグループの接続されているすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="30193-266">指定されたクライアントを除く、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。</span><span class="sxs-lookup"><span data-stu-id="30193-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="30193-267">呼び出し元のクライアントを除く、指定されたグループ内のすべての接続されているクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="30193-268">メソッド名に対するコンパイル時の検証がありません</span><span class="sxs-lookup"><span data-stu-id="30193-268">No compile-time validation for method names</span></span>

<span data-ttu-id="30193-269">指定したメソッド名は動的オブジェクトとして解釈されます。つまり、IntelliSense やコンパイル時の検証は行われません。</span><span class="sxs-lookup"><span data-stu-id="30193-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="30193-270">式は実行時に評価されます。</span><span class="sxs-lookup"><span data-stu-id="30193-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="30193-271">メソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。クライアントに名前と一致するメソッドがある場合、そのメソッドが呼び出され、パラメーター値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="30193-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="30193-272">一致するメソッドがクライアントに見つからない場合、エラーは発生しません。</span><span class="sxs-lookup"><span data-stu-id="30193-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="30193-273">クライアントメソッドを呼び出すときに、SignalR がバックグラウンドでクライアントに送信するデータの形式の詳細については、「 [SignalR の概要](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="30193-274">大文字と小文字を区別しないメソッド名の一致</span><span class="sxs-lookup"><span data-stu-id="30193-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="30193-275">メソッド名の一致では、大文字と小文字が区別されません。</span><span class="sxs-lookup"><span data-stu-id="30193-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="30193-276">たとえば、サーバー上の `Clients.All.addContosoChatMessageToPage` は、クライアントで `AddContosoChatMessageToPage`、`addcontosochatmessagetopage`、または `addContosoChatMessageToPage` を実行します。</span><span class="sxs-lookup"><span data-stu-id="30193-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="30193-277">非同期実行</span><span class="sxs-lookup"><span data-stu-id="30193-277">Asynchronous execution</span></span>

<span data-ttu-id="30193-278">呼び出すメソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="30193-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="30193-279">クライアントへのメソッド呼び出しの後に来るコードは、SignalR がクライアントへのデータの転送を完了するまで待たずにすぐに実行されます。ただし、後続のコード行がメソッドの完了を待機するように指定した場合は除きます。</span><span class="sxs-lookup"><span data-stu-id="30193-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="30193-280">次のコード例は、2つのクライアントメソッドを順番に実行する方法を示しています。1つは .NET 4.5 で動作するコードを使用し、もう1つは .NET 4 で動作するコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="30193-281">**.NET 4.5 の例**</span><span class="sxs-lookup"><span data-stu-id="30193-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="30193-282">**.NET 4 の例**</span><span class="sxs-lookup"><span data-stu-id="30193-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="30193-283">`await` または `ContinueWith` を使用して、次のコード行が実行される前にクライアントメソッドが終了するまで待機する場合、次のコード行が実行される前にクライアントが実際にメッセージを受信するという意味ではありません。</span><span class="sxs-lookup"><span data-stu-id="30193-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="30193-284">クライアントメソッド呼び出しの "完了" は、SignalR がメッセージの送信に必要なすべての処理を実行したことを意味します。</span><span class="sxs-lookup"><span data-stu-id="30193-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="30193-285">クライアントがメッセージを受信したことを確認する必要がある場合は、自分でその機構をプログラミングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="30193-286">たとえば、ハブで `MessageReceived` メソッドをコーディングすることができます。 `addContosoChatMessageToPage` また、クライアントで実行する必要のある作業を行った後 `MessageReceived` を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="30193-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="30193-287">ハブの `MessageReceived` では、元のメソッド呼び出しの実際のクライアントの受信と処理によって、どのような作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="30193-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="30193-288">文字列変数をメソッド名として使用する方法</span><span class="sxs-lookup"><span data-stu-id="30193-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="30193-289">文字列変数をメソッド名として使用してクライアントメソッドを呼び出す場合は、`Clients.All` (または `Clients.Others`、`Clients.Caller`など) を `IClientProxy` にキャストし、 [invoke (methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="30193-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="30193-290">ハブクラスからグループメンバーシップを管理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="30193-291">SignalR のグループは、接続されたクライアントの指定したサブセットにメッセージをブロードキャストする方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="30193-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="30193-292">グループには任意の数のクライアントを含めることができ、クライアントは任意の数のグループのメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="30193-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="30193-293">グループメンバーシップを管理するには、ハブクラスの `Groups` プロパティによって提供される[Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)メソッドと[Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="30193-294">次の例は、クライアントコードによって呼び出されるハブメソッドで使用される `Groups.Add` および `Groups.Remove` メソッドと、それらを呼び出す JavaScript クライアントコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="30193-295">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="30193-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="30193-296">**生成されたプロキシを使用する JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="30193-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="30193-297">明示的にグループを作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="30193-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="30193-298">実際には、`Groups.Add`への呼び出しで名前を初めて指定したときにグループが自動的に作成されます。このグループのメンバーシップから最後の接続を削除すると、グループが削除されます。</span><span class="sxs-lookup"><span data-stu-id="30193-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="30193-299">グループメンバーシップの一覧またはグループの一覧を取得するための API はありません。</span><span class="sxs-lookup"><span data-stu-id="30193-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="30193-300">SignalR は、 [pub/sub モデル](http://en.wikipedia.org/wiki/Publish/subscribe)に基づいてクライアントとグループにメッセージを送信します。サーバーは、グループまたはグループメンバーシップの一覧を保持しません。</span><span class="sxs-lookup"><span data-stu-id="30193-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="30193-301">これにより、web ファームにノードを追加するたびに、SignalR が保持するすべての状態を新しいノードに反映する必要があるため、スケーラビリティを最大化できます。</span><span class="sxs-lookup"><span data-stu-id="30193-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="30193-302">Add メソッドと Remove メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="30193-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="30193-303">`Groups.Add` メソッドと `Groups.Remove` メソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="30193-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="30193-304">クライアントをグループに追加し、グループを使用してすぐにメッセージをクライアントに送信する場合は、`Groups.Add` メソッドが最初に終了するようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="30193-305">次のコード例では、.NET 4.5 で動作するコードを使用して1つ、.NET 4 で動作するコードを使用して、その方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="30193-306">**.NET 4.5 の例**</span><span class="sxs-lookup"><span data-stu-id="30193-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="30193-307">**.NET 4 の例**</span><span class="sxs-lookup"><span data-stu-id="30193-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="30193-308">グループメンバーシップの永続化</span><span class="sxs-lookup"><span data-stu-id="30193-308">Group membership persistence</span></span>

<span data-ttu-id="30193-309">SignalR は、ユーザーではなく接続を追跡します。そのため、ユーザーが接続を確立するたびにユーザーが同じグループにいる場合は、ユーザーが新しい接続を確立するたびに `Groups.Add` を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="30193-310">接続が一時的に失われた後、SignalR が接続を自動的に復元できる場合があります。</span><span class="sxs-lookup"><span data-stu-id="30193-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="30193-311">この場合、SignalR は、新しい接続を確立するのではなく、同じ接続を復元するため、クライアントのグループメンバーシップは自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="30193-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="30193-312">これは、サーバーの再起動または障害の結果として一時的な中断が発生した場合でも可能です。これは、グループメンバーシップを含む各クライアントの接続状態がクライアントに対してラウンドトリップされるためです。</span><span class="sxs-lookup"><span data-stu-id="30193-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="30193-313">接続がタイムアウトになる前にサーバーがダウンし、新しいサーバーに置き換えられた場合、クライアントは自動的に新しいサーバーに再接続し、メンバーであるグループに再登録することができます。</span><span class="sxs-lookup"><span data-stu-id="30193-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="30193-314">接続が切断された後、または接続がタイムアウトしたとき、またはクライアントが切断されたとき (たとえば、ブラウザーが新しいページに移動したとき) に接続が自動的に復元できない場合、グループのメンバーシップは失われます。</span><span class="sxs-lookup"><span data-stu-id="30193-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="30193-315">次回ユーザーが接続するときは、新しい接続になります。</span><span class="sxs-lookup"><span data-stu-id="30193-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="30193-316">同じユーザーが新しい接続を確立するときにグループメンバーシップを維持するには、ユーザーが新しい接続を確立するたびに、アプリケーションがユーザーとグループの間の関連付けを追跡し、グループメンバーシップを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="30193-317">接続と再接続の詳細については、このトピックで後述[する「ハブクラスで接続の有効期間イベントを処理する方法](#connectionlifetime)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="30193-318">シングルユーザーグループ</span><span class="sxs-lookup"><span data-stu-id="30193-318">Single-user groups</span></span>

<span data-ttu-id="30193-319">SignalR を使用するアプリケーションは、通常、どのユーザーがメッセージを送信したか、どのユーザーがメッセージを受信する必要があるかを知るために、ユーザーと接続の間の関連付けを追跡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="30193-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="30193-320">グループは、そのために一般的に使用される2つのパターンのいずれかで使用されます。</span><span class="sxs-lookup"><span data-stu-id="30193-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="30193-321">シングルユーザーグループ。</span><span class="sxs-lookup"><span data-stu-id="30193-321">Single-user groups.</span></span>

    <span data-ttu-id="30193-322">ユーザー名をグループ名として指定し、ユーザーが接続または再接続するたびに現在の接続 ID をグループに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="30193-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="30193-323">グループに送信するユーザーにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="30193-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="30193-324">この方法の欠点は、ユーザーがオンラインであるかオフラインであるかを確認する方法がグループに提供されていないことです。</span><span class="sxs-lookup"><span data-stu-id="30193-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="30193-325">ユーザー名と接続 Id の間の関連付けを追跡します。</span><span class="sxs-lookup"><span data-stu-id="30193-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="30193-326">各ユーザー名と1つまたは複数の接続 Id の間の関連付けをディクショナリまたはデータベースに格納し、ユーザーが接続または切断するたびに格納されているデータを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="30193-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="30193-327">ユーザーにメッセージを送信するには、接続 Id を指定します。</span><span class="sxs-lookup"><span data-stu-id="30193-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="30193-328">この方法の欠点は、より多くのメモリを必要とすることです。</span><span class="sxs-lookup"><span data-stu-id="30193-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="30193-329">ハブクラスで接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="30193-330">接続の有効期間イベントを処理する一般的な理由は、ユーザーが接続されているかどうかを追跡し、ユーザー名と接続 Id の関連付けを追跡することです。</span><span class="sxs-lookup"><span data-stu-id="30193-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="30193-331">クライアントが接続または切断したときに独自のコードを実行するには、次の例に示すように、ハブクラスの `OnConnected`、`OnDisconnected`、および `OnReconnected` の仮想メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="30193-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="30193-332">OnConnected、Onconnected、および Onconnected が呼び出されたとき</span><span class="sxs-lookup"><span data-stu-id="30193-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="30193-333">ブラウザーが新しいページに移動するたびに、新しい接続を確立する必要があります。つまり、SignalR は、`OnDisconnected` メソッドを実行し、その後に `OnConnected` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="30193-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="30193-334">SignalR は、新しい接続が確立されるときに常に新しい接続 ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="30193-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="30193-335">SignalR メソッドは、接続が一時的に切断されたときに呼び出されます。これは、ケーブルが一時的に切断され、接続がタイムアウトする前に再接続された場合などです。 `OnReconnected``OnDisconnected` メソッドは、ブラウザーが新しいページに移動したときなど、クライアントが切断され、SignalR が自動的に再接続できない場合に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="30193-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="30193-336">したがって、特定のクライアントに対して考えられる一連のイベントは、`OnConnected`、`OnReconnected`、`OnDisconnected`です。または `OnConnected`、`OnDisconnected`ます。</span><span class="sxs-lookup"><span data-stu-id="30193-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="30193-337">特定の接続に対して、シーケンス `OnConnected`、`OnDisconnected`、`OnReconnected` は表示されません。</span><span class="sxs-lookup"><span data-stu-id="30193-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="30193-338">`OnDisconnected` メソッドは、サーバーがダウンしたときやアプリドメインがリサイクルされたときなど、一部のシナリオでは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="30193-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="30193-339">別のサーバーがオンラインになるか、アプリケーションドメインがリサイクルを完了すると、一部のクライアントが再接続して `OnReconnected` イベントを発生させることができる場合があります。</span><span class="sxs-lookup"><span data-stu-id="30193-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="30193-340">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="30193-341">呼び出し元の状態が設定されていません</span><span class="sxs-lookup"><span data-stu-id="30193-341">Caller state not populated</span></span>

<span data-ttu-id="30193-342">接続の有効期間イベントハンドラーメソッドは、サーバーから呼び出されます。つまり、クライアントの `state` オブジェクトに格納されているすべての状態は、サーバーの `Caller` プロパティに設定されません。</span><span class="sxs-lookup"><span data-stu-id="30193-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="30193-343">`state` オブジェクトと `Caller` プロパティの詳細については、このトピックの「[クライアントとハブクラス間で状態を渡す方法](#passstate)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="30193-344">コンテキストプロパティからクライアントに関する情報を取得する方法</span><span class="sxs-lookup"><span data-stu-id="30193-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="30193-345">クライアントに関する情報を取得するには、ハブクラスの `Context` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="30193-346">`Context` プロパティは、次の情報へのアクセスを提供する[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="30193-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="30193-347">呼び出し元クライアントの接続 ID。</span><span class="sxs-lookup"><span data-stu-id="30193-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="30193-348">接続 ID は、SignalR によって割り当てられる GUID です (独自のコードで値を指定することはできません)。</span><span class="sxs-lookup"><span data-stu-id="30193-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="30193-349">接続ごとに1つの接続 ID があり、アプリケーションに複数のハブがある場合は、すべてのハブで同じ接続 ID が使用されます。</span><span class="sxs-lookup"><span data-stu-id="30193-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="30193-350">HTTP ヘッダーデータ。</span><span class="sxs-lookup"><span data-stu-id="30193-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="30193-351">`Context.Headers`から HTTP ヘッダーを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="30193-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="30193-352">同じことに対する複数の参照があるのは、`Context.Headers` が先に作成され、`Context.Request` プロパティが後で追加され、`Context.Headers` が旧バージョンとの互換性のために保持されているためです。</span><span class="sxs-lookup"><span data-stu-id="30193-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="30193-353">文字列データをクエリします。</span><span class="sxs-lookup"><span data-stu-id="30193-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="30193-354">`Context.QueryString`からクエリ文字列データを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="30193-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="30193-355">このプロパティで取得するクエリ文字列は、SignalR 接続を確立した HTTP 要求で使用されたクエリ文字列です。</span><span class="sxs-lookup"><span data-stu-id="30193-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="30193-356">クライアントにクエリ文字列パラメーターを追加するには、接続を構成します。これは、クライアントに関するデータをクライアントからサーバーに渡す便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="30193-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="30193-357">次の例は、生成されたプロキシを使用するときに、JavaScript クライアントにクエリ文字列を追加する方法の1つを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="30193-358">クエリ文字列パラメーターの設定の詳細については、 [JavaScript](index.md)および[.NET](index.md)クライアントの API ガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="30193-359">接続に使用されるトランスポートメソッドは、SignalR によって内部的に使用される他の値と共に、クエリ文字列データで確認できます。</span><span class="sxs-lookup"><span data-stu-id="30193-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="30193-360">`transportMethod` の値は、"Websocket"、"Serverのイベント"、"" 前の Verframe "または" longPolling "になります。</span><span class="sxs-lookup"><span data-stu-id="30193-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="30193-361">`OnConnected` イベントハンドラーメソッドでこの値を確認した場合、一部のシナリオでは、最初に接続に対してネゴシエートされた最後のトランスポートメソッドではないトランスポート値が取得されることがあります。</span><span class="sxs-lookup"><span data-stu-id="30193-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="30193-362">その場合、メソッドは例外をスローし、最後のトランスポートメソッドが確立されると、後で再度呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="30193-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="30193-363">Cookie.</span><span class="sxs-lookup"><span data-stu-id="30193-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="30193-364">`Context.RequestCookies`から cookie を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="30193-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="30193-365">ユーザー情報。</span><span class="sxs-lookup"><span data-stu-id="30193-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="30193-366">要求の HttpContext オブジェクト:</span><span class="sxs-lookup"><span data-stu-id="30193-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="30193-367">このメソッドは、SignalR 接続の `HttpContext` オブジェクトを取得するために `HttpContext.Current` を取得する代わりに使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="30193-368">クライアントとハブクラスの間で状態を渡す方法</span><span class="sxs-lookup"><span data-stu-id="30193-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="30193-369">クライアントプロキシには `state` オブジェクトが用意されており、各メソッド呼び出しでサーバーに送信するデータを格納できます。</span><span class="sxs-lookup"><span data-stu-id="30193-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="30193-370">サーバーでは、クライアントによって呼び出されるハブメソッドの `Clients.Caller` プロパティで、このデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="30193-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="30193-371">`Clients.Caller` プロパティは、接続の有効期間イベントハンドラーメソッド `OnConnected`、`OnDisconnected`、および `OnReconnected`には設定されません。</span><span class="sxs-lookup"><span data-stu-id="30193-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="30193-372">`state` オブジェクトと `Clients.Caller` プロパティのデータの作成または更新は、双方向で機能します。</span><span class="sxs-lookup"><span data-stu-id="30193-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="30193-373">サーバーの値を更新して、クライアントに返されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="30193-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="30193-374">次の例は、すべてのメソッド呼び出しを使用してサーバーに送信するための状態を格納する JavaScript クライアントコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="30193-375">次の例は、.NET クライアントの同等のコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="30193-376">ハブクラスでは、`Clients.Caller` プロパティでこのデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="30193-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="30193-377">次の例は、前の例で参照されている状態を取得するコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="30193-378">状態を永続化するためのこのメカニズムは、大量のデータを対象としていません。これは、`state` または `Clients.Caller` プロパティに格納されているすべてのものが、すべてのメソッド呼び出しでラウンドトリップされるためです。</span><span class="sxs-lookup"><span data-stu-id="30193-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="30193-379">これは、ユーザー名やカウンターなどの小さな項目に便利です。</span><span class="sxs-lookup"><span data-stu-id="30193-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="30193-380">ハブクラスでエラーを処理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="30193-381">ハブクラスのメソッドで発生したエラーを処理するには、次のいずれかまたは両方の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="30193-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="30193-382">Try catch ブロックにメソッドコードをラップし、例外オブジェクトをログに記録します。</span><span class="sxs-lookup"><span data-stu-id="30193-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="30193-383">デバッグの目的でクライアントに例外を送信することはできますが、セキュリティ上の理由から、実稼働環境でクライアントに詳細情報を送信することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="30193-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="30193-384">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)メソッドを処理するハブパイプラインモジュールを作成します。</span><span class="sxs-lookup"><span data-stu-id="30193-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="30193-385">次の例は、エラーをログに記録するパイプラインモジュールを示しています。その後、モジュールをハブパイプラインに挿入する global.asax 内のコードを示します。</span><span class="sxs-lookup"><span data-stu-id="30193-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="30193-386">ハブパイプラインモジュールの詳細については、このトピックで後述[する「ハブパイプラインをカスタマイズする方法](#hubpipeline)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="30193-387">トレースを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="30193-387">How to enable tracing</span></span>

<span data-ttu-id="30193-388">サーバー側のトレースを有効にするには、次の例に示すように、web.config ファイルに system.web 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="30193-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="30193-389">Visual Studio でアプリケーションを実行すると、 **[出力]** ウィンドウにログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30193-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="30193-390">ハブクラスの外部からクライアントメソッドを呼び出し、グループを管理する方法</span><span class="sxs-lookup"><span data-stu-id="30193-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="30193-391">ハブクラスとは異なるクラスからクライアントメソッドを呼び出すには、ハブの SignalR context オブジェクトへの参照を取得し、それを使用してクライアント上のメソッドを呼び出すか、グループを管理します。</span><span class="sxs-lookup"><span data-stu-id="30193-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="30193-392">次のサンプル `StockTicker` クラスは、context オブジェクトを取得し、それをクラスのインスタンスに格納し、そのクラスインスタンスを静的プロパティに格納します。また、シングルトンクラスインスタンスのコンテキストを使用して、`StockTickerHub`という名前のハブに接続されているクライアントで `updateStockPrice` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="30193-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="30193-393">有効期間が長いオブジェクトでコンテキストを複数回使用する必要がある場合は、参照を一度取得し、毎回再度取得するのではなく保存します。</span><span class="sxs-lookup"><span data-stu-id="30193-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="30193-394">コンテキストを一度取得すると、SignalR は、ハブメソッドがクライアントメソッドの呼び出しを行うのと同じ順序で、メッセージをクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="30193-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="30193-395">ハブの SignalR コンテキストの使用方法を示すチュートリアルについては、「 [ASP.NET SignalR を使用したサーバーブロードキャスト](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="30193-396">クライアントメソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="30193-396">Calling client methods</span></span>

<span data-ttu-id="30193-397">どのクライアントが RPC を受信するかを指定できますが、ハブクラスからを呼び出す場合よりもオプションが少なくて済みます。</span><span class="sxs-lookup"><span data-stu-id="30193-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="30193-398">その理由は、コンテキストがクライアントからの特定の呼び出しに関連付けられていないため、`Clients.Others`、`Clients.Caller`、`Clients.OthersInGroup`など、現在の接続 ID に関する知識を必要とするメソッドが使用できないことです。</span><span class="sxs-lookup"><span data-stu-id="30193-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="30193-399">次のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="30193-399">The following options are available:</span></span>

- <span data-ttu-id="30193-400">接続されたすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="30193-401">接続 ID で識別される特定のクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="30193-402">指定したクライアントを除くすべての接続されているクライアント。接続 ID で識別されます。</span><span class="sxs-lookup"><span data-stu-id="30193-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="30193-403">指定したグループの接続されているすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="30193-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="30193-404">指定されたクライアントを除く、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。</span><span class="sxs-lookup"><span data-stu-id="30193-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="30193-405">ハブクラスのメソッドから非ハブクラスを呼び出す場合は、現在の接続 ID を渡し、それを `Clients.Client`、`Clients.AllExcept`、または `Clients.Group` と共に使用して、`Clients.Caller`、`Clients.Others`、または `Clients.OthersInGroup`をシミュレートすることができます。</span><span class="sxs-lookup"><span data-stu-id="30193-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="30193-406">次の例では、`MoveShapeHub` クラスが `Broadcaster` クラスに接続 ID を渡して、`Broadcaster` クラスが `Clients.Others`をシミュレートできるようにします。</span><span class="sxs-lookup"><span data-stu-id="30193-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="30193-407">グループメンバーシップの管理</span><span class="sxs-lookup"><span data-stu-id="30193-407">Managing group membership</span></span>

<span data-ttu-id="30193-408">グループを管理する場合、ハブクラスの場合と同じオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="30193-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="30193-409">クライアントをグループに追加する</span><span class="sxs-lookup"><span data-stu-id="30193-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="30193-410">クライアントをグループから削除する</span><span class="sxs-lookup"><span data-stu-id="30193-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="30193-411">ハブパイプラインをカスタマイズする方法</span><span class="sxs-lookup"><span data-stu-id="30193-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="30193-412">SignalR を使用すると、独自のコードをハブパイプラインに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="30193-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="30193-413">次の例は、クライアントから受信した各受信メソッド呼び出しとクライアントで呼び出された送信メソッド呼び出しをログに記録するカスタムハブパイプラインモジュールを示しています。</span><span class="sxs-lookup"><span data-stu-id="30193-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="30193-414">*Global.asax*ファイルの次のコードは、モジュールをハブパイプラインで実行するように登録します。</span><span class="sxs-lookup"><span data-stu-id="30193-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="30193-415">オーバーライド可能な方法は多数あります。</span><span class="sxs-lookup"><span data-stu-id="30193-415">There are many different methods that you can override.</span></span> <span data-ttu-id="30193-416">完全な一覧については、「 [HubPipelineModule メソッド](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30193-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
