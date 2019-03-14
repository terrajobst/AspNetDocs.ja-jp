---
title: Razor コンポーネントのホスティング モデル
author: guardrex
description: クライアント側 Blazor とサーバー側の ASP.NET Core で Razor コンポーネント ホスティング モデルを理解します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042439"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="3e0c1-103">Razor コンポーネントのホスティング モデル</span><span class="sxs-lookup"><span data-stu-id="3e0c1-103">Razor Components hosting models</span></span>

<span data-ttu-id="3e0c1-104">によって[Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="3e0c1-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="3e0c1-105">Razor のコンポーネントは、クライアント側で実行するように設計 web フレームワーク WebAssembly ベースの .NET ランタイム上のブラウザーで (*Blazor*) または ASP.NET Core でのサーバー側 (*ASP.NET Core の Razor コンポーネント*)。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-105">Razor Components is a web framework designed to run client-side in the browser on a WebAssembly-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="3e0c1-106">ホスティング モデルでは、アプリおよびコンポーネントのモデルに関係なく*は同じまま*します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="3e0c1-107">この記事では、使用可能なホスティング モデルについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-107">This article discusses the available hosting models.</span></span>

## <a name="client-side-hosting-model"></a><span data-ttu-id="3e0c1-108">クライアント側のホスティング モデル</span><span class="sxs-lookup"><span data-stu-id="3e0c1-108">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="3e0c1-109">Blazor のプリンシパルのホスティング モデルは、ブラウザーで実行されているクライアント側です。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-109">The principal hosting model for Blazor is running client-side in the browser.</span></span> <span data-ttu-id="3e0c1-110">このモデルで Blazor アプリ、その依存関係、および .NET ランタイムがブラウザーにダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-110">In this model, the Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="3e0c1-111">アプリがブラウザー UI スレッド上で直接実行されます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-111">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="3e0c1-112">すべての UI の更新とイベントの処理は、同じプロセス内で発生します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-112">All UI updates and event handling happens within the same process.</span></span> <span data-ttu-id="3e0c1-113">アプリの資産をどのような web サーバーが推奨を使用して静的ファイルとしてデプロイできます (を参照してください[ホストを展開および](xref:host-and-deploy/razor-components/index))。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-113">The app assets can be deployed as static files using whatever web server is preferred (see [Host and deploy](xref:host-and-deploy/razor-components/index)).</span></span>

![Blazor クライアント側:Blazor アプリは、ブラウザー内での UI スレッドで実行されます。](hosting-models/_static/client-side.png)

<span data-ttu-id="3e0c1-115">クライアント側のホスティング モデルを使用して Blazor アプリを作成するには、使用、 **Blazor**または **(ASP.NET Core のホストされる) Blazor**プロジェクト テンプレート (`blazor`または`blazorhosted`テンプレート、を使用する場合[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド プロンプトでコマンド)。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-115">To create a Blazor app using the client-side hosting model, use the **Blazor** or **Blazor (ASP.NET Core Hosted)** project templates (`blazor` or `blazorhosted` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command at a command prompt).</span></span> <span data-ttu-id="3e0c1-116">含まれる*blazor.webassembly.js*ハンドルのスクリプトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-116">The included *blazor.webassembly.js* script handles:</span></span>

* <span data-ttu-id="3e0c1-117">.NET ランタイムで、アプリとその依存関係をダウンロードしています。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-117">Downloading the .NET runtime, the app, and its dependencies.</span></span>
* <span data-ttu-id="3e0c1-118">アプリを実行するランタイムを初期化します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-118">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="3e0c1-119">クライアント側のホスティング モデルでは、いくつかの利点を提供します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-119">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="3e0c1-120">クライアント側 Blazor:</span><span class="sxs-lookup"><span data-stu-id="3e0c1-120">Client-side Blazor:</span></span>

* <span data-ttu-id="3e0c1-121">.NET サーバー側の依存関係がありません。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-121">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="3e0c1-122">リッチな対話型の UI があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-122">Has a rich interactive UI.</span></span>
* <span data-ttu-id="3e0c1-123">クライアント リソースと機能を完全に活用します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-123">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="3e0c1-124">オフロードは、サーバーからクライアントに機能します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-124">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="3e0c1-125">オフライン シナリオをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-125">Supports offline scenarios.</span></span>

<span data-ttu-id="3e0c1-126">クライアント側のホストには欠点があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-126">There are downsides to client-side hosting.</span></span> <span data-ttu-id="3e0c1-127">クライアント側 Blazor:</span><span class="sxs-lookup"><span data-stu-id="3e0c1-127">Client-side Blazor:</span></span>

* <span data-ttu-id="3e0c1-128">アプリをブラウザーの機能に制限されます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-128">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="3e0c1-129">対応クライアントのハードウェアとソフトウェア (たとえば、WebAssembly サポート) が必要です。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-129">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="3e0c1-130">より大きなダウンロード サイズと読み込み時間長くアプリ。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-130">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="3e0c1-131">.NET ランタイムおよびツールのサポート (たとえば、.NET Standard のサポートとデバッグに制限あり) を成熟させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-131">Has less mature .NET runtime and tooling support (for example, limitations in .NET Standard support and debugging).</span></span>

<span data-ttu-id="3e0c1-132">Visual Studio が含まれています、 **Blazor (ホストされる ASP.NET Core)** WebAssembly で実行し、ASP.NET Core サーバーでホストされている Blazor アプリを作成するためのプロジェクト テンプレート。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-132">Visual Studio includes the **Blazor (ASP.NET Core hosted)** project template for creating a Blazor app that runs on WebAssembly and is hosted on an ASP.NET Core server.</span></span> <span data-ttu-id="3e0c1-133">ASP.NET Core アプリは Blazor アプリをクライアントに機能しますが、別のプロセスは、それ以外の場合。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-133">The ASP.NET Core app serves the Blazor app to clients but is otherwise a separate process.</span></span> <span data-ttu-id="3e0c1-134">クライアント側の Blazor アプリは、Web API の呼び出しまたは SignalR 接続を使用してネットワーク経由でサーバーと対話できます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-134">The client-side Blazor app can interact with the server over the network using Web API calls or SignalR connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e0c1-135">クライアント側の Blazor アプリは、IIS サブ アプリとしてホストされる ASP.NET Core アプリによって処理されますが、ASP.NET Core モジュールの継承されたハンドラーを無効にします。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-135">If a client-side Blazor app is served by an ASP.NET Core app hosted as an IIS sub-app, disable the inherited ASP.NET Core Module handler.</span></span> <span data-ttu-id="3e0c1-136">Blazor アプリのアプリ ベース パスを設定*index.html*サブアプリを IIS で構成するときに使用される IIS エイリアスをファイル。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-136">Set the app base path in the Blazor app's *index.html* file to the IIS alias used when configuring the sub-app in IIS.</span></span>
>
> <span data-ttu-id="3e0c1-137">詳細については、次を参照してください。[アプリ ベース パス](xref:host-and-deploy/razor-components/index#app-base-path)します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-137">For more information, see [App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="3e0c1-138">サーバー側のホスティング モデル</span><span class="sxs-lookup"><span data-stu-id="3e0c1-138">Server-side hosting model</span></span>

<span data-ttu-id="3e0c1-139">ASP.NET Core の Razor コンポーネント サーバー側のホスティング モデルでは、アプリは、ASP.NET Core アプリ内からサーバーで実行されます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-139">In the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="3e0c1-140">UI の更新、イベント処理、JavaScript の呼び出しは、SignalR 接続経由で処理されます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-140">UI updates, event handling, and JavaScript calls are handled over a SignalR connection.</span></span>

![ASP.NET Core Razor コンポーネント サーバー側:ブラウザーでは、SignalR 接続経由でサーバー (ASP.NET Core アプリの内部でホストされている) アプリと対話します。](hosting-models/_static/server-side.png)

<span data-ttu-id="3e0c1-142">サーバー側のホスティング モデルを使用して Razor コンポーネント アプリを作成するには、使用、 **Blazor (ASP.NET Core ではサーバー側)** テンプレート (`blazorserver`を使用する場合[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド プロンプトで)。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-142">To create a Razor Components app using the server-side hosting model, use the **Blazor (Server-side in ASP.NET Core)** template (`blazorserver` when using [dotnet new](/dotnet/core/tools/dotnet-new) at a command prompt).</span></span> <span data-ttu-id="3e0c1-143">ASP.NET Core アプリは、Razor コンポーネント サーバー側のアプリをホストし、クライアントが接続する SignalR エンドポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-143">An ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="3e0c1-144">ASP.NET Core アプリを参照して、アプリの`Startup`クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-144">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="3e0c1-145">サーバー側コンポーネントの Razor サービス。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-145">Server-side Razor Components services.</span></span>
* <span data-ttu-id="3e0c1-146">要求パイプラインを処理するアプリです。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-146">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="3e0c1-147">*Blazor.server.js*スクリプト&dagger;クライアント接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-147">The *blazor.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="3e0c1-148">永続化および (たとえば、失われたネットワーク接続の場合は) 発生時に必要なアプリの状態を復元するアプリの役目です。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-148">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="3e0c1-149">サーバー側のホスティング モデルには、いくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-149">The server-side hosting model offers several benefits:</span></span>

* <span data-ttu-id="3e0c1-150">.NET を使用して、全体のアプリを作成することができますとC#コンポーネント モデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-150">Allows you to write your entire app with .NET and C# using the component model.</span></span>
* <span data-ttu-id="3e0c1-151">により、機能豊富な対話型実現し、不要なページ更新を回避できます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-151">Provides a rich interactive feel and avoids unnecessary page refreshes.</span></span>
* <span data-ttu-id="3e0c1-152">クライアント側の Blazor アプリよりもアプリのサイズが大幅に小さくなりますがあり、非常に高速に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-152">Has a significantly smaller app size than a client-side Blazor app and loads much faster.</span></span>
* <span data-ttu-id="3e0c1-153">コンポーネント ロジックは、.NET Core の互換性のある Api の使用など、サーバーの機能のフル活用できます。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-153">Component logic can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="3e0c1-154">既存の .NET tooling、デバッグなどが期待どおりに動作するため、サーバー上で .NET Core で実行します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-154">Runs on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="3e0c1-155">シン クライアントと連動 (たとえば、WebAssembly とリソースをサポートしないブラウザーがデバイスを制限する)。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-155">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>

<span data-ttu-id="3e0c1-156">サーバー側のホストには欠点があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-156">There are downsides to server-side hosting:</span></span>

* <span data-ttu-id="3e0c1-157">待機時間があります。すべてのユーザー操作には、ネットワーク ホップが必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-157">Has higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="3e0c1-158">オフライン サポートにはありません。クライアント接続に失敗した場合、アプリは稼働を停止します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-158">Offers no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="3e0c1-159">スケーラビリティに少なくなっています。サーバーは、複数のクライアント接続を管理し、クライアントの状態を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-159">Has reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="3e0c1-160">アプリを処理するために、ASP.NET Core サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-160">Requires an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="3e0c1-161">(たとえば、CDN) からサーバーなしの展開は、ことはできません。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="3e0c1-162">&dagger;*Blazor.server.js*スクリプトは、次のパスに発行: *bin/{デバッグ |リリース}/{ターゲット フレームワーク}/publish/{アプリケーション名}。アプリ/dist/フレームワーク (_f)* します。</span><span class="sxs-lookup"><span data-stu-id="3e0c1-162">&dagger;The *blazor.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
