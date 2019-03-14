---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana サンプル |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: b8ce2b40a19e0429f1ccedb03b8f829582652d24
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056399"
---
<a name="katana-samples"></a><span data-ttu-id="09c26-102">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="09c26-102">Katana Samples</span></span>
====================
<span data-ttu-id="09c26-103">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="09c26-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="09c26-104">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="09c26-104">Katana Samples</span></span>

<span data-ttu-id="09c26-105">**ASP.NET ルーティング サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="09c26-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="09c26-106">一部のアプリケーションでは、非 OWIN コンポーネントと共に、ASP.NET ルート テーブル内の OWIN コンポーネントをフックするでしょう。</span><span class="sxs-lookup"><span data-stu-id="09c26-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="09c26-107">このサンプルでは、MapOwinPath と Microsoft.Owin.Host.SystemWeb によって提供される MapOwinRoute RouteCollection 拡張メソッドを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="09c26-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="09c26-108">**サンプル パイプラインを分岐** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="09c26-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="09c26-109">OWIN 要求処理パイプラインが線形にする必要はありません、それらをさまざまな方法で要求を処理する分岐できます。</span><span class="sxs-lookup"><span data-stu-id="09c26-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="09c26-110">このサンプルでは、要求のパスやヘッダーなどの他の要求データに基づいて分岐のパイプラインを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="09c26-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="09c26-111">これらのコンポーネント、Microsoft.Owin.Mapping nuget パッケージで利用できます。</span><span class="sxs-lookup"><span data-stu-id="09c26-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="09c26-112">**カスタム サーバー サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="09c26-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="09c26-113">自己ホストするときに、カスタムの OWIN サーバーを使用する方法を示しています。 OWIN します。</span><span class="sxs-lookup"><span data-stu-id="09c26-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="09c26-114">**サンプルの埋め込み** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="09c26-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="09c26-115">OWIN サーバーによっては、独自のプロセス内で実行できます (&quot;セルフホステッド&quot;)。</span><span class="sxs-lookup"><span data-stu-id="09c26-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="09c26-116">このサンプルでは、Microsoft.Owin.Hosting nuget パッケージによって提供されるツールを使用して、OWIN アプリケーションを起動する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="09c26-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="09c26-117">**HelloWorld サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="09c26-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="09c26-118">OWIN は、HTTP サーバーのさまざまなサーバー間でアプリケーションの移植性をできるようにする抽象化された API です。</span><span class="sxs-lookup"><span data-stu-id="09c26-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="09c26-119">このサンプルは、いくつかを使用して Hello World アプリケーションを作成する方法を示します。**単純なラッパー** ASP.NET などの web サーバーで、生の OWIN 抽象化と実行を囲む。</span><span class="sxs-lookup"><span data-stu-id="09c26-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="09c26-120">**Hello World の生の OWIN サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="09c26-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="09c26-121">このサンプルを使用して Hello World アプリケーションを記述する方法、**生**OWIN 抽象化し、ASP.NET などの web サーバーで実行します。</span><span class="sxs-lookup"><span data-stu-id="09c26-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="09c26-122">**SignalR サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="09c26-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="09c26-123">OWIN を使用して SignalR を自己ホストする方法を示します/Katana します。</span><span class="sxs-lookup"><span data-stu-id="09c26-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="09c26-124">SignalR の自己ホストの詳細については、次を参照してください。[チュートリアル。SignalR セルフホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)します。</span><span class="sxs-lookup"><span data-stu-id="09c26-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="09c26-125">**静的ファイルのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="09c26-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="09c26-126">OWIN を使用して静的ファイルの HTTP 要求をサポートする方法を示します/Katana します。</span><span class="sxs-lookup"><span data-stu-id="09c26-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="09c26-127">**Web API** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="09c26-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="09c26-128">このサンプルでは、IIS で OWIN をホストし、Web API を OWIN パイプラインに追加する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="09c26-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="09c26-129">**Web ソケットのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="09c26-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="09c26-130">使用して、OWIN で Web ソケットをサポートする方法を示しています、 [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)クラス。</span><span class="sxs-lookup"><span data-stu-id="09c26-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
