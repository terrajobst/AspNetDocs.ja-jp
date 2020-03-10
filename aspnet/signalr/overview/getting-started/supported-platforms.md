---
uid: signalr/overview/getting-started/supported-platforms
title: サポートされているプラットフォーム |Microsoft Docs
author: bradygaster
description: この記事では、SignalR でサポートされているクライアントとサーバーについて説明します。
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450124"
---
# <a name="supported-platforms"></a><span data-ttu-id="b5ebc-103">サポートされているプラットフォーム</span><span class="sxs-lookup"><span data-stu-id="b5ebc-103">Supported Platforms</span></span>

<span data-ttu-id="b5ebc-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="b5ebc-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b5ebc-105">この記事では、SignalR でサポートされているクライアントとサーバーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="b5ebc-106">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="b5ebc-106">Questions and comments</span></span>
> 
> <span data-ttu-id="b5ebc-107">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b5ebc-108">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="b5ebc-109">SignalR は、さまざまなサーバーおよびクライアント構成でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="b5ebc-110">また、各トランスポートオプションには、独自の一連の要件があります。トランスポートのシステム要件が使用できない場合、SignalR は他のトランスポートへのフェールオーバーを正常に実行します。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="b5ebc-111">SignalR がサポートするトランスポートの詳細については、「[トランスポートとフォールバック](introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="b5ebc-112">サーバー システムの要件</span><span class="sxs-lookup"><span data-stu-id="b5ebc-112">Server system requirements</span></span>

<span data-ttu-id="b5ebc-113">SignalR サーバーコンポーネントは、さまざまなサーバー構成でホストできます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="b5ebc-114">このセクションでは、サポートされているオペレーティングシステムのバージョン、.NET framework、インターネットインフォメーションサーバー、およびその他のコンポーネントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="b5ebc-115">サポート対象のサーバー オペレーティング システム</span><span class="sxs-lookup"><span data-stu-id="b5ebc-115">Supported server operating systems</span></span>

<span data-ttu-id="b5ebc-116">SignalR サーバーコンポーネントは、次のサーバーまたはクライアントオペレーティングシステムでホストできます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="b5ebc-117">SignalR が Websocket を使用するには、Windows Server 2012、Windows Server 2016、または Windows 8 が必要であることに注意してください (WebSocket は Windows Azure Websites で使用できます。サイトの .NET framework のバージョンが4.5 に設定されていて、Web ソケットがサイトで有効になっている必要があります)。[構成] ページ)。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-117">Note that for SignalR to use WebSockets, Windows Server 2012, Windows Server 2016, or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="b5ebc-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b5ebc-118">Windows Server 2016</span></span>
- <span data-ttu-id="b5ebc-119">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b5ebc-119">Windows Server 2012</span></span>
- <span data-ttu-id="b5ebc-120">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="b5ebc-120">Windows Server 2008 r2</span></span>
- <span data-ttu-id="b5ebc-121">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b5ebc-121">Windows 10</span></span>
- <span data-ttu-id="b5ebc-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="b5ebc-122">Windows 8</span></span>
- <span data-ttu-id="b5ebc-123">Windows 7</span><span class="sxs-lookup"><span data-stu-id="b5ebc-123">Windows 7</span></span>
- <span data-ttu-id="b5ebc-124">Windows Azure</span><span class="sxs-lookup"><span data-stu-id="b5ebc-124">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="b5ebc-125">サポートされているサーバー .NET Framework バージョン</span><span class="sxs-lookup"><span data-stu-id="b5ebc-125">Supported server .NET Framework version</span></span>

<span data-ttu-id="b5ebc-126">SignalR 2 は .NET Framework 4.5 でのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-126">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="b5ebc-127">信頼性、互換性、安定性、およびパフォーマンスを向上させる更新プログラムについては、「推奨される[更新プログラム](#updates)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-127">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="b5ebc-128">サポートされているサーバー IIS のバージョン</span><span class="sxs-lookup"><span data-stu-id="b5ebc-128">Supported server IIS versions</span></span>

<span data-ttu-id="b5ebc-129">SignalR が IIS でホストされている場合、次のバージョンがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-129">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="b5ebc-130">開発用 (Windows 8 または Windows 7) のように、クライアントのオペレーティングシステムを使用する場合は、IIS または Cassini の完全バージョンを使用しないことをお勧めします。これは、接続数が10個に制限されているためです。一時的で、頻繁に再確立され、使用されなくなった直後に破棄されることはありません。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-130">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="b5ebc-131">IIS Express は、クライアントオペレーティングシステムで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-131">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="b5ebc-132">また、SignalR を使用するには、IIS 8 または IIS 8 Express を使用する必要があります。サーバーは、Windows 8、Windows Server 2012 以降を使用している必要があり、WebSocket は IIS で有効になっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-132">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="b5ebc-133">IIS で WebSocket を有効にする方法の詳細については、「 [iis 8.0 Websocket プロトコルのサポート](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-133">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="b5ebc-134">IIS 8 または IIS 8 Express。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-134">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="b5ebc-135">IIS 7 および7.5。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-135">IIS 7 and 7.5.</span></span> <span data-ttu-id="b5ebc-136">[拡張子 url](https://support.microsoft.com/kb/980368)のサポートが必要です。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-136">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="b5ebc-137">IIS は統合モードで実行されている必要があります。クラシックモードはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-137">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="b5ebc-138">サーバー送信イベントトランスポートを使用してクラシックモードで IIS を実行すると、最大30秒間のメッセージ遅延が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-138">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="b5ebc-139">ホスティングアプリケーションは、完全信頼モードで実行されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-139">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="b5ebc-140">クライアント システムの要件</span><span class="sxs-lookup"><span data-stu-id="b5ebc-140">Client system requirements</span></span>

<span data-ttu-id="b5ebc-141">SignalR は、さまざまなクライアントプラットフォームで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-141">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="b5ebc-142">ここでは、web ブラウザー、Windows デスクトップアプリケーション、Silverlight アプリケーション、およびモバイルデバイスで SignalR を使用するためのシステム要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-142">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="b5ebc-143">Web ブラウザー</span><span class="sxs-lookup"><span data-stu-id="b5ebc-143">Web browsers</span></span>

<span data-ttu-id="b5ebc-144">SignalR はさまざまな web ブラウザーで使用できますが、通常は最新の2つのバージョンのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-144">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="b5ebc-145">ブラウザーで SignalR を使用するアプリケーションでは、jQuery バージョン1.6.4 または以降のメジャーバージョン (1.7.2、1.8.2、1.9.1 など) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-145">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="b5ebc-146">SignalR は、次のブラウザーで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-146">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="b5ebc-147">Microsoft Internet Explorer のバージョン8、9、10、および11。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-147">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="b5ebc-148">最新、デスクトップ、およびモバイルバージョンがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-148">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="b5ebc-149">Mozilla Firefox: 現在のバージョン-1、Windows と Mac の両方のバージョン。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-149">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="b5ebc-150">Google Chrome: 現在のバージョン-1、Windows と Mac の両方のバージョン。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-150">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="b5ebc-151">Safari: 現在のバージョン-1、Mac と iOS の両方のバージョン。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-151">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="b5ebc-152">Opera: 現在のバージョン-1、Windows のみ。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-152">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="b5ebc-153">Android ブラウザー</span><span class="sxs-lookup"><span data-stu-id="b5ebc-153">Android browser</span></span>

<span data-ttu-id="b5ebc-154">特定のブラウザーを必要とするだけでなく、SignalR が使用するさまざまなトランスポートにも独自の要件があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-154">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="b5ebc-155">次のトランスポートは、次の構成でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-155">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="b5ebc-156">**Web ブラウザートランスポートの要件**</span><span class="sxs-lookup"><span data-stu-id="b5ebc-156">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="b5ebc-157">トランスポート</span><span class="sxs-lookup"><span data-stu-id="b5ebc-157">Transport</span></span> | <span data-ttu-id="b5ebc-158">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b5ebc-158">Internet Explorer</span></span> | <span data-ttu-id="b5ebc-159">Chrome (Windows または iOS)</span><span class="sxs-lookup"><span data-stu-id="b5ebc-159">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="b5ebc-160">Firefox</span><span class="sxs-lookup"><span data-stu-id="b5ebc-160">Firefox</span></span> | <span data-ttu-id="b5ebc-161">Safari (OSX または iOS)</span><span class="sxs-lookup"><span data-stu-id="b5ebc-161">Safari (OSX or iOS)</span></span> | <span data-ttu-id="b5ebc-162">Android</span><span class="sxs-lookup"><span data-stu-id="b5ebc-162">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b5ebc-163">WebSocket</span><span class="sxs-lookup"><span data-stu-id="b5ebc-163">WebSockets</span></span> | <span data-ttu-id="b5ebc-164">10+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-164">10+</span></span> | <span data-ttu-id="b5ebc-165">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-165">current - 1</span></span> | <span data-ttu-id="b5ebc-166">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-166">current - 1</span></span> | <span data-ttu-id="b5ebc-167">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-167">current - 1</span></span> | <span data-ttu-id="b5ebc-168">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-168">N/A</span></span> |
| <span data-ttu-id="b5ebc-169">Server-Sent Events</span><span class="sxs-lookup"><span data-stu-id="b5ebc-169">Server-Sent Events</span></span> | <span data-ttu-id="b5ebc-170">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-170">N/A</span></span> | <span data-ttu-id="b5ebc-171">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-171">current - 1</span></span> | <span data-ttu-id="b5ebc-172">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-172">current - 1</span></span> | <span data-ttu-id="b5ebc-173">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-173">current - 1</span></span> | <span data-ttu-id="b5ebc-174">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-174">N/A</span></span> |
| <span data-ttu-id="b5ebc-175">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="b5ebc-175">ForeverFrame</span></span> | <span data-ttu-id="b5ebc-176">8+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-176">8+</span></span> | <span data-ttu-id="b5ebc-177">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-177">N/A</span></span> | <span data-ttu-id="b5ebc-178">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-178">N/A</span></span> | <span data-ttu-id="b5ebc-179">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-179">N/A</span></span> | <span data-ttu-id="b5ebc-180">4.1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-180">4.1</span></span> |
| <span data-ttu-id="b5ebc-181">長いポーリング</span><span class="sxs-lookup"><span data-stu-id="b5ebc-181">Long Polling</span></span> | <span data-ttu-id="b5ebc-182">8+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-182">8+</span></span> | <span data-ttu-id="b5ebc-183">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-183">current - 1</span></span> | <span data-ttu-id="b5ebc-184">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-184">current - 1</span></span> | <span data-ttu-id="b5ebc-185">現在-1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-185">current - 1</span></span> | <span data-ttu-id="b5ebc-186">4.1</span><span class="sxs-lookup"><span data-stu-id="b5ebc-186">4.1</span></span> |

<span data-ttu-id="b5ebc-187">\*: 6 + すべての機能に必要です。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-187">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="b5ebc-188">サポートされていないブラウザー</span><span class="sxs-lookup"><span data-stu-id="b5ebc-188">Unsupported Browsers</span></span>

<span data-ttu-id="b5ebc-189">SignalR は、以前のバージョンのブラウザーでは重大な問題*が発生すること*なく実行できますが、SignalR では積極的にテストされないため、通常はバグを修正することはありません。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-189">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="b5ebc-190">Windows デスクトップアプリケーションと Silverlight アプリケーション</span><span class="sxs-lookup"><span data-stu-id="b5ebc-190">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="b5ebc-191">SignalR は、web ブラウザーでの実行に加えて、スタンドアロンの Windows クライアントアプリケーションまたは Silverlight アプリケーションでホストできます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-191">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="b5ebc-192">Windows デスクトップアプリケーションと Silverlight SignalR アプリケーションには、次のシステム要件があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-192">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="b5ebc-193">.NET 4 を使用するアプリケーションは、Windows XP SP3 以降でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-193">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="b5ebc-194">.NET Framework 4.5 を使用するアプリケーションは、Windows Vista 以降でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-194">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="b5ebc-195">オペレーティングシステムと .NET framework の要件に加えて、SignalR で使用できるトランスポートには独自の要件があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-195">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="b5ebc-196">次のトランスポートは、次の構成でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-196">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="b5ebc-197">**Windows デスクトップと Silverlight トランスポートの要件**</span><span class="sxs-lookup"><span data-stu-id="b5ebc-197">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="b5ebc-198">トランスポート</span><span class="sxs-lookup"><span data-stu-id="b5ebc-198">Transport</span></span> | <span data-ttu-id="b5ebc-199">.NET アプリケーション</span><span class="sxs-lookup"><span data-stu-id="b5ebc-199">.NET application</span></span> | <span data-ttu-id="b5ebc-200">Silverlight</span><span class="sxs-lookup"><span data-stu-id="b5ebc-200">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5ebc-201">Web ソケット</span><span class="sxs-lookup"><span data-stu-id="b5ebc-201">Web Sockets</span></span> | <span data-ttu-id="b5ebc-202">Windows 8 以降および .NET 4.5 以降</span><span class="sxs-lookup"><span data-stu-id="b5ebc-202">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="b5ebc-203">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-203">N/A</span></span> |
| <span data-ttu-id="b5ebc-204">無期限フレーム</span><span class="sxs-lookup"><span data-stu-id="b5ebc-204">Forever Frame</span></span> | <span data-ttu-id="b5ebc-205">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-205">N/A</span></span> | <span data-ttu-id="b5ebc-206">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-206">N/A</span></span> |
| <span data-ttu-id="b5ebc-207">Server-Sent Events</span><span class="sxs-lookup"><span data-stu-id="b5ebc-207">Server-Sent Events</span></span> | <span data-ttu-id="b5ebc-208">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-208">.NET 4+</span></span> | <span data-ttu-id="b5ebc-209">5+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-209">5+</span></span> |
| <span data-ttu-id="b5ebc-210">長いポーリング</span><span class="sxs-lookup"><span data-stu-id="b5ebc-210">Long Polling</span></span> | <span data-ttu-id="b5ebc-211">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-211">.NET 4+</span></span> | <span data-ttu-id="b5ebc-212">5+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-212">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="b5ebc-213">Windows ストアアプリケーションと Windows Phone アプリケーション</span><span class="sxs-lookup"><span data-stu-id="b5ebc-213">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="b5ebc-214">SignalR は、Windows ストアアプリケーションと Windows Phone 8 アプリケーションで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-214">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="b5ebc-215">次のトランスポートは、次の構成でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-215">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="b5ebc-216">**Windows ストアおよび Windows Phone トランスポートの要件**</span><span class="sxs-lookup"><span data-stu-id="b5ebc-216">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="b5ebc-217">トランスポート</span><span class="sxs-lookup"><span data-stu-id="b5ebc-217">Transport</span></span> | <span data-ttu-id="b5ebc-218">Windows ストア/.NET</span><span class="sxs-lookup"><span data-stu-id="b5ebc-218">Windows Store/ .NET</span></span> | <span data-ttu-id="b5ebc-219">Windows ストア/JavaScript</span><span class="sxs-lookup"><span data-stu-id="b5ebc-219">Windows Store/ JavaScript</span></span> | <span data-ttu-id="b5ebc-220">Windows Phone/IE</span><span class="sxs-lookup"><span data-stu-id="b5ebc-220">Windows Phone/ IE</span></span> | <span data-ttu-id="b5ebc-221">Windows Phone/ .NET</span><span class="sxs-lookup"><span data-stu-id="b5ebc-221">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b5ebc-222">WebSocket</span><span class="sxs-lookup"><span data-stu-id="b5ebc-222">WebSockets</span></span> | <span data-ttu-id="b5ebc-223">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-223">N/A</span></span> | <span data-ttu-id="b5ebc-224">Win8 +</span><span class="sxs-lookup"><span data-stu-id="b5ebc-224">Win8+</span></span> | <span data-ttu-id="b5ebc-225">8+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-225">8+</span></span> | <span data-ttu-id="b5ebc-226">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-226">N/A</span></span> |
| <span data-ttu-id="b5ebc-227">無期限フレーム</span><span class="sxs-lookup"><span data-stu-id="b5ebc-227">Forever Frame</span></span> | <span data-ttu-id="b5ebc-228">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-228">N/A</span></span> | <span data-ttu-id="b5ebc-229">Win8 +</span><span class="sxs-lookup"><span data-stu-id="b5ebc-229">Win8+</span></span> | <span data-ttu-id="b5ebc-230">7.5+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-230">7.5+</span></span> | <span data-ttu-id="b5ebc-231">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-231">N/A</span></span> |
| <span data-ttu-id="b5ebc-232">Server-Sent Events</span><span class="sxs-lookup"><span data-stu-id="b5ebc-232">Server-Sent Events</span></span> | <span data-ttu-id="b5ebc-233">Win8 +</span><span class="sxs-lookup"><span data-stu-id="b5ebc-233">Win8+</span></span> | <span data-ttu-id="b5ebc-234">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-234">N/A</span></span> | <span data-ttu-id="b5ebc-235">該当なし</span><span class="sxs-lookup"><span data-stu-id="b5ebc-235">N/A</span></span> | <span data-ttu-id="b5ebc-236">8+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-236">8+</span></span> |
| <span data-ttu-id="b5ebc-237">長いポーリング</span><span class="sxs-lookup"><span data-stu-id="b5ebc-237">Long Polling</span></span> | <span data-ttu-id="b5ebc-238">Win8 +</span><span class="sxs-lookup"><span data-stu-id="b5ebc-238">Win8+</span></span> | <span data-ttu-id="b5ebc-239">Win8 +</span><span class="sxs-lookup"><span data-stu-id="b5ebc-239">Win8+</span></span> | <span data-ttu-id="b5ebc-240">7.5+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-240">7.5+</span></span> | <span data-ttu-id="b5ebc-241">8+</span><span class="sxs-lookup"><span data-stu-id="b5ebc-241">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="b5ebc-242">推奨される更新プログラム</span><span class="sxs-lookup"><span data-stu-id="b5ebc-242">Recommended Updates</span></span>

<span data-ttu-id="b5ebc-243">SignalR サーバーには、次の更新プログラムをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-243">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="b5ebc-244">.NET Framework 4.5 の更新プログラムは、[こちらで](https://support.microsoft.com/kb/2750149)入手できます。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-244">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="b5ebc-245">Microsoft は、ASP.NET の Qfe を定期的にリリースします。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-245">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="b5ebc-246">これらは、使用可能なものとして適用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ebc-246">These should be applied as available.</span></span>
