---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hub API ガイド-.NET クライアント (C#) |Microsoft Docs
author: bradygaster
description: このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、短所など、.NET クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467404"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="c7bbc-103">ASP.NET SignalR Hub API ガイド-.NET クライアント (C#)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c7bbc-104">このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、コンソールアプリケーションなど、.NET クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="c7bbc-105">SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="c7bbc-106">サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="c7bbc-107">クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="c7bbc-108">SignalR は、クライアントとサーバーのすべての組み込みを処理します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="c7bbc-109">SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="c7bbc-110">SignalR、ハブ、および永続的な接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては、[はじめに SignalR](../getting-started/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c7bbc-111">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="c7bbc-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c7bbc-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c7bbc-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="c7bbc-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c7bbc-113">.NET 4.5</span></span>
> - <span data-ttu-id="c7bbc-114">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="c7bbc-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c7bbc-115">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="c7bbc-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c7bbc-116">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c7bbc-117">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="c7bbc-117">Questions and comments</span></span>
>
> <span data-ttu-id="c7bbc-118">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c7bbc-119">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c7bbc-120">概要</span><span class="sxs-lookup"><span data-stu-id="c7bbc-120">Overview</span></span>

<span data-ttu-id="c7bbc-121">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="c7bbc-122">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c7bbc-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="c7bbc-123">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="c7bbc-124">Silverlight クライアントからのクロスドメイン接続</span><span class="sxs-lookup"><span data-stu-id="c7bbc-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="c7bbc-125">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="c7bbc-126">WPF クライアントで同時接続の最大数を設定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="c7bbc-127">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="c7bbc-128">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="c7bbc-129">HTTP ヘッダーを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="c7bbc-130">クライアント証明書を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="c7bbc-131">ハブプロキシの作成方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="c7bbc-132">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="c7bbc-133">パラメーターのないメソッド</span><span class="sxs-lookup"><span data-stu-id="c7bbc-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="c7bbc-134">パラメーターを持つメソッド、パラメーターの型の指定</span><span class="sxs-lookup"><span data-stu-id="c7bbc-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="c7bbc-135">パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="c7bbc-136">ハンドラーを削除する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="c7bbc-137">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="c7bbc-138">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="c7bbc-139">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="c7bbc-140">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="c7bbc-141">サーバーが呼び出すことができるクライアントメソッドの WPF、Silverlight、コンソールアプリケーションのコードサンプル</span><span class="sxs-lookup"><span data-stu-id="c7bbc-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="c7bbc-142">.NET クライアントプロジェクトのサンプルについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="c7bbc-143">[gustavo-SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com on (WinRT、Silverlight、コンソールアプリの例)。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="c7bbc-144">[DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GITHUB.COM (WPF の例)。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="c7bbc-145">[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (コンソールアプリの例) を使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="c7bbc-146">サーバーまたは JavaScript クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="c7bbc-147">SignalR Hub API ガイド-サーバー</span><span class="sxs-lookup"><span data-stu-id="c7bbc-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="c7bbc-148">SignalR Hub API ガイド-JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="c7bbc-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="c7bbc-149">API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="c7bbc-150">.NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="c7bbc-151">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c7bbc-151">Client setup</span></span>

<span data-ttu-id="c7bbc-152">[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet パッケージをインストールします ( [SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)パッケージではありません)。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="c7bbc-153">このパッケージは、.NET 4 と .NET 4.5 の両方に対して、WinRT、Silverlight、WPF、コンソールアプリケーション、および Windows Phone クライアントをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="c7bbc-154">クライアントにインストールされている SignalR のバージョンが、サーバー上のバージョンと異なる場合、SignalR は多くの場合、差分に適合することができます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="c7bbc-155">たとえば、SignalR version 2 を実行しているサーバーは、バージョン2がインストールされているクライアントだけでなく、1.1 がインストールされているクライアントをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="c7bbc-156">サーバー上のバージョンとクライアントのバージョンの違いが大きすぎる場合、またはクライアントがサーバーより新しい場合、SignalR は、クライアントが接続を確立しようとすると `InvalidOperationException` 例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="c7bbc-157">エラーメッセージは "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" です。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="c7bbc-158">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-158">How to establish a connection</span></span>

<span data-ttu-id="c7bbc-159">接続を確立するには、`HubConnection` オブジェクトを作成し、プロキシを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="c7bbc-160">接続を確立するには、`HubConnection` オブジェクトの `Start` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="c7bbc-161">JavaScript クライアントの場合は、`Start` メソッドを呼び出して接続を確立する前に、少なくとも1つのイベントハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="c7bbc-162">これは、.NET クライアントには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="c7bbc-163">JavaScript クライアントの場合、生成されたプロキシコードは、サーバー上に存在するすべてのハブのプロキシを自動的に作成し、ハンドラーを登録することは、クライアントが使用するハブを指定する方法です。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="c7bbc-164">ただし、.NET クライアントの場合はハブプロキシを手動で作成するので、SignalR はプロキシを作成するハブを使用することを前提としています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="c7bbc-165">このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c7bbc-166">別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="c7bbc-167">`Start` メソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="c7bbc-168">接続が確立されるまで後続のコード行が実行されないようにするには、ASP.NET 4.5 非同期メソッドで `await` を使用するか、同期メソッドで `.Wait()` します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="c7bbc-169">WinRT クライアントでは `.Wait()` を使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="c7bbc-170">Silverlight クライアントからのクロスドメイン接続</span><span class="sxs-lookup"><span data-stu-id="c7bbc-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="c7bbc-171">Silverlight クライアントからのクロスドメイン接続を有効にする方法については、「[ドメインの境界を越えてサービスを利用可能](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)にする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="c7bbc-172">接続を構成する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-172">How to configure the connection</span></span>

<span data-ttu-id="c7bbc-173">接続を確立する前に、次のいずれかのオプションを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="c7bbc-174">同時接続数の制限。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="c7bbc-175">クエリ文字列パラメーター。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-175">Query string parameters.</span></span>
- <span data-ttu-id="c7bbc-176">トランスポートメソッド。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-176">The transport method.</span></span>
- <span data-ttu-id="c7bbc-177">HTTP ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-177">HTTP headers.</span></span>
- <span data-ttu-id="c7bbc-178">クライアント証明書。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="c7bbc-179">WPF クライアントで同時接続の最大数を設定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="c7bbc-180">WPF クライアントでは、同時接続の最大数を既定値の2から増やすことが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="c7bbc-181">推奨値は10です。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="c7bbc-182">詳細については、「 [Servicepointmanager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="c7bbc-183">クエリ文字列パラメーターを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-183">How to specify query string parameters</span></span>

<span data-ttu-id="c7bbc-184">クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="c7bbc-185">次の例は、クライアントコードでクエリ文字列パラメーターを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="c7bbc-186">次の例は、サーバーコードでクエリ文字列パラメーターを読み取る方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="c7bbc-187">トランスポート方法を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-187">How to specify the transport method</span></span>

<span data-ttu-id="c7bbc-188">接続プロセスの一環として、SignalR クライアントは、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定するために、通常はサーバーとネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="c7bbc-189">使用するトランスポートが既にわかっている場合は、このネゴシエーションプロセスを省略できます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="c7bbc-190">トランスポートメソッドを指定するには、トランスポートオブジェクトを Start メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="c7bbc-191">次の例は、クライアントコードでトランスポートメソッドを指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="c7bbc-192">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)名前空間には、トランスポートを指定するために使用できる次のクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="c7bbc-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="c7bbc-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="c7bbc-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (サーバーとクライアントの両方で .net 4.5 が使用されている場合にのみ使用可能)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="c7bbc-196">[Autotransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (クライアントとサーバーの両方でサポートされている最適なトランスポートを自動的に選択します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="c7bbc-197">これは既定のトランスポートです。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-197">This is the default transport.</span></span> <span data-ttu-id="c7bbc-198">このを `Start` メソッドに渡すことは、何も渡していないのと同じ効果があります)。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="c7bbc-199">このリストには、ブラウザーでのみ使用されているため、この一覧には、事前にフレームトランスポートが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="c7bbc-200">サーバーコードでトランスポート方法を確認する方法については、「 [ASP.NET SignalR HUB API Guide-server-Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="c7bbc-201">トランスポートとフォールバックの詳細については、「 [SignalR とフォールバックの概要](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="c7bbc-202">HTTP ヘッダーを指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-202">How to specify HTTP headers</span></span>

<span data-ttu-id="c7bbc-203">HTTP ヘッダーを設定するには、connection オブジェクトの `Headers` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="c7bbc-204">次の例は、HTTP ヘッダーを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="c7bbc-205">クライアント証明書を指定する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-205">How to specify client certificates</span></span>

<span data-ttu-id="c7bbc-206">クライアント証明書を追加するには、接続オブジェクトの `AddClientCertificate` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="c7bbc-207">ハブプロキシの作成方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-207">How to create the Hub proxy</span></span>

<span data-ttu-id="c7bbc-208">ハブがサーバーから呼び出すことができるメソッドを定義し、サーバーのハブでメソッドを呼び出すためには、接続オブジェクトで `CreateHubProxy` を呼び出して、ハブのプロキシを作成します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="c7bbc-209">`CreateHubProxy` に渡す文字列は、ハブクラスの名前、またはサーバーで使用されていた場合は `HubName` 属性によって指定された名前です。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="c7bbc-210">名前が一致するかどうかを判断する際、大文字と小文字は区別されません。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="c7bbc-211">**サーバー上のハブクラス**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="c7bbc-212">**ハブクラスのクライアントプロキシを作成する**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="c7bbc-213">`HubName` 属性を使用してハブクラスを装飾する場合は、その名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="c7bbc-214">**サーバー上のハブクラス**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="c7bbc-215">**ハブクラスのクライアントプロキシを作成する**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="c7bbc-216">同じ `hubName`で複数回 `HubConnection.CreateHubProxy` を呼び出すと、キャッシュされた同じ `IHubProxy` オブジェクトが取得されます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c7bbc-217">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="c7bbc-218">サーバーが呼び出すことができるメソッドを定義するには、プロキシの `On` メソッドを使用してイベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="c7bbc-219">メソッド名の一致では、大文字と小文字が区別されません。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="c7bbc-220">たとえば、サーバー上の `Clients.All.UpdateStockPrice` は、クライアントで `updateStockPrice`、`updatestockprice`、または `UpdateStockPrice` を実行します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="c7bbc-221">UI を更新するためのメソッドコードを記述する方法については、クライアントプラットフォームによって要件が異なります。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="c7bbc-222">ここでは、WinRT (Windows ストア .NET) クライアントの例を示します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="c7bbc-223">WPF、Silverlight、コンソールアプリケーションの例については、[このトピックで後述する別のセクション](#wpfsl)で説明します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="c7bbc-224">パラメーターのないメソッド</span><span class="sxs-lookup"><span data-stu-id="c7bbc-224">Methods without parameters</span></span>

<span data-ttu-id="c7bbc-225">処理しているメソッドにパラメーターがない場合は、`On` メソッドの非ジェネリックオーバーロードを使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="c7bbc-226">**パラメーターを指定せずにクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="c7bbc-227">**パラメーターのないサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照してください](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c7bbc-228">パラメーターを使用したメソッドとパラメーターの型の指定</span><span class="sxs-lookup"><span data-stu-id="c7bbc-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="c7bbc-229">処理中のメソッドにパラメーターがある場合は、`On` メソッドのジェネリック型としてパラメーターの型を指定します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="c7bbc-230">`On` メソッドの汎用的なオーバーロードによって、最大8個のパラメーター (Windows Phone 7 では 4) を指定できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="c7bbc-231">次の例では、1つのパラメーターが `UpdateStockPrice` メソッドに送信されます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="c7bbc-232">**パラメーターを使用してクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="c7bbc-233">**パラメーターに使用されるストッククラス**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="c7bbc-234">**パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照してください](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c7bbc-235">パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="c7bbc-236">`On` メソッドのジェネリック型としてパラメーターを指定する代わりに、パラメーターを動的オブジェクトとして指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="c7bbc-237">**パラメーターを使用してクライアントメソッドを呼び出すサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="c7bbc-238">**パラメーターに使用されるストッククラス**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="c7bbc-239">**パラメーターの動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="c7bbc-240">ハンドラーを削除する方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-240">How to remove a handler</span></span>

<span data-ttu-id="c7bbc-241">ハンドラーを削除するには、その `Dispose` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="c7bbc-242">**サーバーから呼び出されるメソッドのクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="c7bbc-243">**ハンドラーを削除するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="c7bbc-244">クライアントからサーバーメソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-244">How to call server methods from the client</span></span>

<span data-ttu-id="c7bbc-245">サーバーでメソッドを呼び出すには、ハブプロキシで `Invoke` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="c7bbc-246">サーバーメソッドに戻り値がない場合は、`Invoke` メソッドの非ジェネリックオーバーロードを使用します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="c7bbc-247">**戻り値のないメソッドのサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="c7bbc-248">**戻り値を持たないメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="c7bbc-249">サーバーメソッドに戻り値がある場合は、`Invoke` メソッドのジェネリック型として戻り値の型を指定します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="c7bbc-250">**戻り値を持ち、複合型パラメーターを受け取るメソッドのサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="c7bbc-251">**パラメーターと戻り値に使用されるストッククラス**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="c7bbc-252">**ASP.NET 4.5 async メソッドで戻り値を持ち、複合型パラメーターを取るメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="c7bbc-253">**同期メソッドで戻り値を持ち、複合型パラメーターを受け取るメソッドを呼び出すクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="c7bbc-254">`Invoke` メソッドは非同期的に実行され、`Task` オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="c7bbc-255">`await` または `.Wait()`を指定しない場合は、呼び出すメソッドが実行を終了する前に、次のコード行が実行されます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="c7bbc-256">接続の有効期間イベントの処理方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="c7bbc-257">SignalR は、次のように処理できる接続の有効期間イベントを提供します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="c7bbc-258">`Received`: 接続でデータを受信したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="c7bbc-259">受信したデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-259">Provides the received data.</span></span>
- <span data-ttu-id="c7bbc-260">`ConnectionSlow`: クライアントが低速または頻繁に切断される接続を検出したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="c7bbc-261">`Reconnecting`: 基になるトランスポートが再接続を開始したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="c7bbc-262">`Reconnected`: 基になるトランスポートが再接続されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="c7bbc-263">`StateChanged`: 接続状態が変化したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="c7bbc-264">以前の状態と新しい状態を提供します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-264">Provides the old state and the new state.</span></span> <span data-ttu-id="c7bbc-265">接続状態の値の詳細については、「 [Connectionstate 列挙型](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="c7bbc-266">`Closed`: 接続が切断されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="c7bbc-267">たとえば、致命的ではないが、断続的な接続の問題 (パフォーマンスの低下や頻繁に接続の切断など) が発生した場合に、警告メッセージを表示するには、`ConnectionSlow` イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="c7bbc-268">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="c7bbc-269">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-269">How to handle errors</span></span>

<span data-ttu-id="c7bbc-270">サーバーで詳細なエラーメッセージを明示的に有効にしないと、エラーに関する最小限の情報が、エラーの後に SignalR によって返される例外オブジェクトに含まれます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="c7bbc-271">たとえば、`newContosoChatMessage` の呼び出しが失敗した場合、エラーオブジェクトのエラーメッセージには、セキュリティ上の理由により、実稼働環境でクライアントに詳細なエラーメッセージを送信する "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" が含まれます。ただし、トラブルシューティングのために詳細なエラーメッセージを有効にする場合は、サーバーで次のコードを使用してください。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="c7bbc-272">SignalR が発生するエラーを処理するには、connection オブジェクトに `Error` イベントのハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="c7bbc-273">メソッドの呼び出しで発生したエラーを処理するには、try-catch ブロックでコードをラップします。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="c7bbc-274">クライアント側のログ記録を有効にする方法</span><span class="sxs-lookup"><span data-stu-id="c7bbc-274">How to enable client-side logging</span></span>

<span data-ttu-id="c7bbc-275">クライアント側のログ記録を有効にするには、接続オブジェクトの `TraceLevel` と `TraceWriter` のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="c7bbc-276">サーバーが呼び出すことができるクライアントメソッドの WPF、Silverlight、コンソールアプリケーションのコードサンプル</span><span class="sxs-lookup"><span data-stu-id="c7bbc-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="c7bbc-277">サーバーが呼び出すことができるクライアントメソッドを定義するために、前に示したコードサンプルは WinRT クライアントに適用されます。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="c7bbc-278">次のサンプルは、WPF、Silverlight、およびコンソールアプリケーションクライアントの同等のコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="c7bbc-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="c7bbc-279">パラメーターのないメソッド</span><span class="sxs-lookup"><span data-stu-id="c7bbc-279">Methods without parameters</span></span>

<span data-ttu-id="c7bbc-280">**パラメーターを指定せずにサーバーから呼び出されるメソッドの WPF クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="c7bbc-281">**パラメーターを指定せずにサーバーから呼び出されるメソッドの Silverlight クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="c7bbc-282">**パラメーターを指定せずにサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c7bbc-283">パラメーターを使用したメソッドとパラメーターの型の指定</span><span class="sxs-lookup"><span data-stu-id="c7bbc-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="c7bbc-284">**パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="c7bbc-285">**パラメーターを使用してサーバーから呼び出されるメソッドの Silverlight クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="c7bbc-286">**パラメーターを使用してサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c7bbc-287">パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)</span><span class="sxs-lookup"><span data-stu-id="c7bbc-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="c7bbc-288">**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="c7bbc-289">**パラメーターの動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの Silverlight クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="c7bbc-290">**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="c7bbc-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
