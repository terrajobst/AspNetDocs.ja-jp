---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Samples |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472348"
---
# <a name="katana-samples"></a><span data-ttu-id="53d7e-102">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="53d7e-102">Katana Samples</span></span>

<span data-ttu-id="53d7e-103">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="53d7e-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="53d7e-104">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="53d7e-104">Katana Samples</span></span>

<span data-ttu-id="53d7e-105">**ASP.NET Route サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="53d7e-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="53d7e-106">一部のアプリケーションでは、非 OWIN コンポーネントと共に、ASP.NET ルート テーブル内の OWIN コンポーネントをフックするでしょう。</span><span class="sxs-lookup"><span data-stu-id="53d7e-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="53d7e-107">このサンプルでは、Owin によって提供される RouteCollection 拡張メソッド Mアポストロフィ Winpath と Mアポストロフィ Winroute の使用方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="53d7e-108">**パイプラインの分岐サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="53d7e-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="53d7e-109">OWIN 要求処理パイプラインは、線形である必要はありません。分岐して、さまざまな方法で要求を処理することができます。</span><span class="sxs-lookup"><span data-stu-id="53d7e-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="53d7e-110">このサンプルでは、要求パスまたはその他の要求データ (ヘッダーなど) に基づいて分岐パイプラインを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="53d7e-111">これらのコンポーネントは、Owin nuget パッケージで入手できます。</span><span class="sxs-lookup"><span data-stu-id="53d7e-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="53d7e-112">**カスタムサーバーサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="53d7e-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="53d7e-113">自己ホスト OWIN の場合にカスタム OWIN サーバーを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="53d7e-114">**埋め込みサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="53d7e-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="53d7e-115">一部の OWIN サーバーは、独自のプロセス内で実行できます (&quot;自己ホスト型&quot;)。</span><span class="sxs-lookup"><span data-stu-id="53d7e-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="53d7e-116">このサンプルでは、Owin nuget パッケージによって提供されるツールを使用して OWIN アプリケーションを起動する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="53d7e-117">**HelloWorld サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="53d7e-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="53d7e-118">OWIN は、さまざまなサーバー間でのアプリケーションの移植性を実現する HTTP サーバー API の抽象化です。</span><span class="sxs-lookup"><span data-stu-id="53d7e-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="53d7e-119">このサンプルでは、未加工の OWIN 抽象化に関するいくつかの**単純なラッパー**を使用して Hello World アプリケーションを作成し、ASP.NET などの web サーバーで実行する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="53d7e-120">**Hello World RAW OWIN サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="53d7e-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="53d7e-121">このサンプルでは、**未加工**の OWIN 抽象化を使用して Hello World アプリケーションを作成し、Asp.Net などの web サーバーで実行する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="53d7e-122">**SignalR サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="53d7e-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="53d7e-123">OWIN/Katana を使用して SignalR を自己ホストする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="53d7e-124">自己ホスト SignalR の詳細については、「[チュートリアル: SignalR 自己ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="53d7e-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="53d7e-125">**静的ファイルのサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="53d7e-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="53d7e-126">OWIN/Katana を使用して静的ファイルの HTTP 要求をサポートする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="53d7e-127">**WEB API** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="53d7e-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="53d7e-128">このサンプルでは、IIS で OWIN をホストし、Web API を OWIN パイプラインに追加する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="53d7e-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="53d7e-129">**Web Socket サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="53d7e-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="53d7e-130">OWIN クラスを使用して、Web ソケットをサポートする方法を示し[ます。](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="53d7e-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
