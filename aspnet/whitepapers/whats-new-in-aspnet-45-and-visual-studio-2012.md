---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 と Visual Studio 2012 における新機能 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、ASP.NET 4.5 で導入される新機能と強化された機能について説明します。 また、web 開発に加えられた機能強化についても説明します。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422734"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="008d3-104">ASP.NET 4.5 と Visual Studio 2012 における新機能</span><span class="sxs-lookup"><span data-stu-id="008d3-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="008d3-105">このドキュメントでは、ASP.NET 4.5 で導入される新機能と強化された機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="008d3-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="008d3-106">また、Visual Studio 2012 で web 開発を行う際の改善点についても説明します。</span><span class="sxs-lookup"><span data-stu-id="008d3-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="008d3-107">このドキュメントは、当初、2012年2月29日に発行されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="008d3-108">ASP.NET Core ランタイムとフレームワーク</span><span class="sxs-lookup"><span data-stu-id="008d3-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="008d3-109">HTTP 要求と応答の非同期的な読み取りと書き込み</span><span class="sxs-lookup"><span data-stu-id="008d3-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="008d3-110">HttpRequest の処理の機能強化</span><span class="sxs-lookup"><span data-stu-id="008d3-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="008d3-111">応答を非同期的にフラッシュする</span><span class="sxs-lookup"><span data-stu-id="008d3-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="008d3-112">*Await*および*タスク*ベースの非同期モジュールとハンドラーのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="008d3-113">非同期 HTTP モジュール</span><span class="sxs-lookup"><span data-stu-id="008d3-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="008d3-114">非同期 HTTP ハンドラー</span><span class="sxs-lookup"><span data-stu-id="008d3-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="008d3-115">新しい ASP.NET 要求の検証機能</span><span class="sxs-lookup"><span data-stu-id="008d3-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="008d3-116">遅延 ("lazy") 要求の検証</span><span class="sxs-lookup"><span data-stu-id="008d3-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="008d3-117">未検証要求のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="008d3-118">アンチ Xss ライブラリ</span><span class="sxs-lookup"><span data-stu-id="008d3-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="008d3-119">Websocket プロトコルのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="008d3-120">バンドルと縮小</span><span class="sxs-lookup"><span data-stu-id="008d3-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="008d3-121">Web ホスティングのパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="008d3-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="008d3-122">主要なパフォーマンス要因</span><span class="sxs-lookup"><span data-stu-id="008d3-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="008d3-123">新しいパフォーマンス機能の要件</span><span class="sxs-lookup"><span data-stu-id="008d3-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="008d3-124">共通アセンブリの共有</span><span class="sxs-lookup"><span data-stu-id="008d3-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="008d3-125">高速起動のためのマルチコア JIT コンパイルの使用</span><span class="sxs-lookup"><span data-stu-id="008d3-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="008d3-126">メモリ用に最適化するためのガベージコレクションのチューニング</span><span class="sxs-lookup"><span data-stu-id="008d3-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="008d3-127">Web アプリケーションのプリフェッチ</span><span class="sxs-lookup"><span data-stu-id="008d3-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="008d3-128">ASP.NET Web フォーム</span><span class="sxs-lookup"><span data-stu-id="008d3-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="008d3-129">厳密に型指定されたデータ コントロール</span><span class="sxs-lookup"><span data-stu-id="008d3-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="008d3-130">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="008d3-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="008d3-131">データの選択</span><span class="sxs-lookup"><span data-stu-id="008d3-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="008d3-132">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="008d3-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="008d3-133">コントロールの値によるフィルター処理</span><span class="sxs-lookup"><span data-stu-id="008d3-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="008d3-134">HTML エンコードされたデータバインディング式</span><span class="sxs-lookup"><span data-stu-id="008d3-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="008d3-135">控えめに検証</span><span class="sxs-lookup"><span data-stu-id="008d3-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="008d3-136">HTML5 の更新プログラム</span><span class="sxs-lookup"><span data-stu-id="008d3-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="008d3-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="008d3-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="008d3-138">ASP.NET Web ページ2</span><span class="sxs-lookup"><span data-stu-id="008d3-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="008d3-139">Visual Studio 2012 リリース候補</span><span class="sxs-lookup"><span data-stu-id="008d3-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="008d3-140">Visual Studio 2010 と Visual Studio 2012 リリース候補間のプロジェクト共有 (プロジェクト互換性)</span><span class="sxs-lookup"><span data-stu-id="008d3-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="008d3-141">ASP.NET 4.5 Web サイトテンプレートの構成の変更</span><span class="sxs-lookup"><span data-stu-id="008d3-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="008d3-142">ASP.NET ルーティング用の IIS 7 でのネイティブサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="008d3-143">HTML エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="008d3-144">スマートタスク</span><span class="sxs-lookup"><span data-stu-id="008d3-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="008d3-145">WAI-ARIA のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="008d3-146">新しい HTML5 スニペット</span><span class="sxs-lookup"><span data-stu-id="008d3-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="008d3-147">ユーザーコントロールに抽出</span><span class="sxs-lookup"><span data-stu-id="008d3-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="008d3-148">属性のコードナゲットの IntelliSense</span><span class="sxs-lookup"><span data-stu-id="008d3-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="008d3-149">開始タグまたは終了タグの名前を変更するときに、一致するタグの名前を自動的に変更する</span><span class="sxs-lookup"><span data-stu-id="008d3-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="008d3-150">イベントハンドラーの生成</span><span class="sxs-lookup"><span data-stu-id="008d3-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="008d3-151">スマートインデント</span><span class="sxs-lookup"><span data-stu-id="008d3-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="008d3-152">ステートメント入力候補を自動的に減らす</span><span class="sxs-lookup"><span data-stu-id="008d3-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="008d3-153">JavaScript エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="008d3-154">コードのアウトライン</span><span class="sxs-lookup"><span data-stu-id="008d3-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="008d3-155">中かっこの一致</span><span class="sxs-lookup"><span data-stu-id="008d3-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="008d3-156">定義に移動</span><span class="sxs-lookup"><span data-stu-id="008d3-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="008d3-157">ECMAScript5 のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="008d3-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="008d3-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="008d3-159">VSDOC 署名のオーバーロード</span><span class="sxs-lookup"><span data-stu-id="008d3-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="008d3-160">暗黙の参照</span><span class="sxs-lookup"><span data-stu-id="008d3-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="008d3-161">CSS エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="008d3-162">ステートメント入力候補を自動的に減らす</span><span class="sxs-lookup"><span data-stu-id="008d3-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="008d3-163">階層インデント。</span><span class="sxs-lookup"><span data-stu-id="008d3-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="008d3-164">CSS ハックのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="008d3-165">ベンダー固有のスキーマ (-moz-,-webkit)</span><span class="sxs-lookup"><span data-stu-id="008d3-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="008d3-166">コメントとコメント解除のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="008d3-167">カラーピッカー</span><span class="sxs-lookup"><span data-stu-id="008d3-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="008d3-168">スニペット</span><span class="sxs-lookup"><span data-stu-id="008d3-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="008d3-169">カスタム領域</span><span class="sxs-lookup"><span data-stu-id="008d3-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="008d3-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="008d3-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="008d3-171">発行</span><span class="sxs-lookup"><span data-stu-id="008d3-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="008d3-172">発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="008d3-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="008d3-173">ASP.NET のプリコンパイルとマージ</span><span class="sxs-lookup"><span data-stu-id="008d3-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="008d3-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="008d3-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="008d3-175">免責事項</span><span class="sxs-lookup"><span data-stu-id="008d3-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="008d3-176">ASP.NET Core ランタイムとフレームワーク</span><span class="sxs-lookup"><span data-stu-id="008d3-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="008d3-177">HTTP 要求と応答の非同期的な読み取りと書き込み</span><span class="sxs-lookup"><span data-stu-id="008d3-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="008d3-178">ASP.NET 4 では、 *GetBufferlessInputStream*メソッドを使用して HTTP 要求エンティティをストリームとして読み取る機能が導入されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="008d3-179">このメソッドは、要求エンティティへのストリームアクセスを提供しました。</span><span class="sxs-lookup"><span data-stu-id="008d3-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="008d3-180">ただし、同期的に実行され、要求の間、スレッドに関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="008d3-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="008d3-181">ASP.NET 4.5 では、HTTP 要求エンティティでストリームを非同期的に読み取る機能、および非同期的にフラッシュする機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="008d3-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="008d3-182">また、ASP.NET 4.5 には、HTTP 要求エンティティをダブルバッファーする機能があります。これにより、.aspx ページハンドラーや ASP.NET MVC コントローラーなどの下流の HTTP ハンドラーとの統合が容易になります。</span><span class="sxs-lookup"><span data-stu-id="008d3-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="008d3-183">HttpRequest の処理の機能強化</span><span class="sxs-lookup"><span data-stu-id="008d3-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="008d3-184">*GetBufferlessInputStream*から ASP.NET 4.5 によって返されるストリーム参照は、同期と非同期の両方の読み取りメソッドをサポートします。</span><span class="sxs-lookup"><span data-stu-id="008d3-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="008d3-185">*GetBufferlessInputStream*から返された*ストリーム*オブジェクトは、system.io.stream.beginread メソッドと EndRead メソッドの両方を実装するようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="008d3-186">非同期*ストリーム*メソッドを使用すると、要求エンティティをチャンク単位で非同期に読み取ることができ、ASP.NET では非同期読み取りループの各反復処理の間で現在のスレッドが解放されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="008d3-187">また、ASP.NET 4.5 には、要求エンティティを読み取るためのコンパニオンメソッドも追加されています。 *httprequest.getbufferedinputstream*です。</span><span class="sxs-lookup"><span data-stu-id="008d3-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="008d3-188">この新しいオーバーロードは、同期読み取りと非同期読み取りの両方をサポートする*GetBufferlessInputStream*のように動作します。</span><span class="sxs-lookup"><span data-stu-id="008d3-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="008d3-189">ただし、読み取り時には、 *httprequest.getbufferedinputstream*もエンティティバイトを ASP.NET 内部バッファーにコピーして、下流のモジュールとハンドラーが引き続き要求エンティティにアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="008d3-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="008d3-190">たとえば、パイプライン内の上流コードによって、 *httprequest.getbufferedinputstream*を使用して要求エンティティが既に読み取られている場合でも、 *Httprequest*または*httprequest*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="008d3-191">これにより、要求に対して非同期処理を実行することができます (たとえば、データベースへの大きなファイルのアップロードをストリーミングする) が、後で .aspx ページと MVC ASP.NET コントローラーを引き続き実行できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="008d3-192">応答を非同期的にフラッシュする</span><span class="sxs-lookup"><span data-stu-id="008d3-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="008d3-193">HTTP クライアントに応答を送信すると、クライアントが遠く離れたり、低帯域幅で接続したりすると、かなりの時間がかかることがあります。</span><span class="sxs-lookup"><span data-stu-id="008d3-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="008d3-194">通常、ASP.NET は、アプリケーションによって作成された応答バイトをバッファーします。</span><span class="sxs-lookup"><span data-stu-id="008d3-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="008d3-195">次に、ASP.NET は、要求処理の最後に、未収バッファーの1回の送信操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="008d3-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="008d3-196">バッファーされた応答が大きい場合 (たとえば、大きなファイルをクライアントにストリーミングする場合) は、 *httpresponse.cache*を定期的に呼び出して、バッファリングされた出力をクライアントに送信し、メモリ使用量を制御したままにしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="008d3-197">ただし、 *flush*は同期呼び出しであるため、*フラッシュ*を繰り返し呼び出すと、長時間実行される可能性のある要求の間、スレッドが引き続き使用されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="008d3-198">ASP.NET 4.5 では、 *httpresponse.cache*クラスの*Beginflush*および*endflush*メソッドを使用して非同期的にフラッシュを実行するためのサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="008d3-199">これらのメソッドを使用すると、オペレーティングシステムのスレッドを使用せずにクライアントにデータを段階的に送信する非同期モジュールと非同期ハンドラーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="008d3-200">*Beginflush*呼び出しと*endflush*呼び出しの間で、ASP.NET は現在のスレッドを解放します。</span><span class="sxs-lookup"><span data-stu-id="008d3-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="008d3-201">これにより、実行時間の長い HTTP ダウンロードをサポートするために必要なアクティブなスレッドの合計数が大幅に削減されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="008d3-202">*Await*および*タスク*ベースの非同期モジュールとハンドラーのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="008d3-203">.NET Framework 4 では、*タスク*と呼ばれる非同期プログラミングの概念が導入されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="008d3-204">タスクは *、タスクの種類と*、*システム*の名前空間の関連する型によって表されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="008d3-205">.NET Framework 4.5 は、*タスク*オブジェクトの操作を単純にするコンパイラの機能強化により、この点に基づいています。</span><span class="sxs-lookup"><span data-stu-id="008d3-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="008d3-206">.NET Framework 4.5 では、コンパイラは*await*と*async*という2つの新しいキーワードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="008d3-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="008d3-207">*Await*キーワードは、コードの一部を非同期に待機する必要があることを示す構文の省略形です。</span><span class="sxs-lookup"><span data-stu-id="008d3-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="008d3-208">*Async*キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。</span><span class="sxs-lookup"><span data-stu-id="008d3-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="008d3-209">*Await*、 *async*、 *Task*オブジェクトを組み合わせることにより、.net 4.5 で非同期コードを簡単に記述できるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="008d3-210">ASP.NET 4.5 では、新しいコンパイラの機能強化を使用して非同期 HTTP モジュールと非同期 HTTP ハンドラーを記述できる新しい Api により、これらの簡素化がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="008d3-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="008d3-211">非同期 HTTP モジュール</span><span class="sxs-lookup"><span data-stu-id="008d3-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="008d3-212">*タスク*オブジェクトを返すメソッド内で非同期処理を実行するとします。</span><span class="sxs-lookup"><span data-stu-id="008d3-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="008d3-213">次のコード例では、非同期呼び出しを行って Microsoft ホームページをダウンロードする非同期メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="008d3-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="008d3-214">メソッドシグネチャで*async*キーワードが使用されていること、および*Downloadstringtaskasync*への*await*呼び出しが使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="008d3-215">ここで .NET Framework 記述する必要があるのは、ダウンロードの完了を待機している間、呼び出し履歴のアンワインドが自動的に処理され、ダウンロードが完了した後に自動的にコールスタックが復元されることだけです。</span><span class="sxs-lookup"><span data-stu-id="008d3-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="008d3-216">ここで、非同期の ASP.NET HTTP モジュールでこの非同期メソッドを使用するとします。</span><span class="sxs-lookup"><span data-stu-id="008d3-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="008d3-217">ASP.NET 4.5 には、ASP.NET HTTP パイプラインによって公開されている古い非同期プログラミングモデルとタスクベースの非同期メソッドを統合するために使用できるヘルパーメソッド (*EventHandlerTaskAsyncHelper*) と新しいデリゲート型 (*TaskEventHandler*) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="008d3-218">この例では、次の方法を示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="008d3-219">非同期 HTTP ハンドラー</span><span class="sxs-lookup"><span data-stu-id="008d3-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="008d3-220">ASP.NET で非同期ハンドラーを記述する従来のアプローチは、 *IHttpAsyncHandler*インターフェイスを実装することです。</span><span class="sxs-lookup"><span data-stu-id="008d3-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="008d3-221">ASP.NET 4.5 では、から派生できる*HttpTaskAsyncHandler*非同期基本型が導入されています。これにより、非同期ハンドラーの記述が非常に簡単になります。</span><span class="sxs-lookup"><span data-stu-id="008d3-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="008d3-222">*HttpTaskAsyncHandler*型は abstract であり、 *processrequestasync*メソッドをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="008d3-223">内部的には、ASP.NET は、ASP.NET パイプラインによって使用される古い非同期プログラミングモデルと*Processrequestasync*の戻り値の署名 ( *Task*オブジェクト) を統合します。</span><span class="sxs-lookup"><span data-stu-id="008d3-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="008d3-224">次の例は、非同期 HTTP ハンドラーの実装の一部として*タスク*と*await*を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="008d3-225">新しい ASP.NET 要求の検証機能</span><span class="sxs-lookup"><span data-stu-id="008d3-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="008d3-226">既定では、ASP.NET は要求の検証を実行し、フィールド、ヘッダー、cookie などのマークアップまたはスクリプトを検索する要求を調べます。</span><span class="sxs-lookup"><span data-stu-id="008d3-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="008d3-227">いずれかが検出されると、ASP.NET は例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="008d3-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="008d3-228">これは、潜在的なクロスサイトスクリプティング攻撃に対する防御の1行目として機能します。</span><span class="sxs-lookup"><span data-stu-id="008d3-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="008d3-229">ASP.NET 4.5 を使用すると、未検証要求データを選択的に簡単に読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="008d3-230">また、ASP.NET 4.5 では、従来は外部ライブラリであった一般的なアンチ Xss ライブラリも統合されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="008d3-231">開発者は、アプリケーションの要求の検証を選択的にオフにすることを頻繁に要求されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="008d3-232">たとえば、アプリケーションがフォーラムソフトウェアの場合、HTML 形式のフォーラムの投稿とコメントをユーザーが送信できるようにする必要がありますが、それでも、要求の検証では他のすべてが確認されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="008d3-233">ASP.NET 4.5 では、未検証入力を選択して簡単に操作できるようにする2つの機能が導入されています: 遅延 ("lazy") 要求の検証と未検証要求データへのアクセス。</span><span class="sxs-lookup"><span data-stu-id="008d3-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="008d3-234">遅延 ("lazy") 要求の検証</span><span class="sxs-lookup"><span data-stu-id="008d3-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="008d3-235">ASP.NET 4.5 では、既定ですべての要求データが要求の検証の対象となります。</span><span class="sxs-lookup"><span data-stu-id="008d3-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="008d3-236">ただし、要求データに実際にアクセスするまで、要求の検証を遅延するようにアプリケーションを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="008d3-237">(これは、特定のデータシナリオの遅延読み込みのような用語に基づいて、レイジー要求の検証と呼ばれることもあります)。次の例に示すように、 *httpRUntime*要素で*requestvalidationmode*属性を4.5 に設定することにより、web.config ファイルで遅延検証を使用するようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="008d3-238">要求の検証モードが4.5 に設定されている場合、要求の検証は特定の要求値に対してのみトリガーされ、コードがその値にアクセスしたときにのみトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="008d3-239">たとえば、コードが要求の値を取得した場合は、form コレクション内のその要素に対してのみ、要求の検証が呼び出されます。フォーム ["フォーラム\_post"]。</span><span class="sxs-lookup"><span data-stu-id="008d3-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="008d3-240">*フォーム*コレクション内の他の要素は検証されません。</span><span class="sxs-lookup"><span data-stu-id="008d3-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="008d3-241">以前のバージョンの ASP.NET では、コレクション内のいずれかの要素にアクセスしたときに、要求コレクション全体に対して要求の検証がトリガーされました。</span><span class="sxs-lookup"><span data-stu-id="008d3-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="008d3-242">新しい動作により、さまざまなアプリケーションコンポーネントが、他の部分で要求の検証をトリガーすることなく、さまざまな要求データを簡単に確認できるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="008d3-243">未検証要求のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-243">Support for unvalidated requests</span></span>

<span data-ttu-id="008d3-244">遅延要求の検証だけでは、要求の検証を選択的にバイパスする問題は解決されません。</span><span class="sxs-lookup"><span data-stu-id="008d3-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="008d3-245">Request. Form ["フォーラム\_post"] の呼び出しでは、その特定の要求値に対して要求の検証がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="008d3-246">ただし、そのフィールドでマークアップを許可する必要があるため、検証をトリガーせずにこのフィールドにアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="008d3-247">これを可能にするために、ASP.NET 4.5 では、要求データへの未検証アクセスがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="008d3-248">ASP.NET 4.5 には、 *HttpRequest*クラスの新しい*未検証*collection プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="008d3-249">このコレクションは、*フォーム*、 *QueryString*、 *cookie*、 *Url*など、要求データのすべての共通値へのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="008d3-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="008d3-250">フォーラムの例を使用して、未検証 request データを読み取ることができるようにするには、まず、新しい要求の検証モードを使用するようにアプリケーションを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="008d3-251">次に、*未検証*プロパティを使用して、未検証 form 値を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="008d3-252">セキュリティ-*未検証の要求データを慎重に使用します。*</span><span class="sxs-lookup"><span data-stu-id="008d3-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="008d3-253">ASP.NET 4.5 では、未検証要求のプロパティとコレクションが追加され、非常に特殊な未検証要求データに簡単にアクセスできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="008d3-254">ただし、危険なテキストがユーザーに表示されないようにするには、未加工の要求データに対してカスタム検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="008d3-255">アンチ Xss ライブラリ</span><span class="sxs-lookup"><span data-stu-id="008d3-255">AntiXSS Library</span></span>

<span data-ttu-id="008d3-256">Microsoft のアンチ Xss ライブラリが普及しているため、ASP.NET 4.5 には、そのライブラリのバージョン4.0 からのコアエンコードルーチンが組み込まれました。</span><span class="sxs-lookup"><span data-stu-id="008d3-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="008d3-257">エンコーディングルーチンは、新しい*system.web. web.config*名前空間の*アンチ Xssenプログラマ*の型によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="008d3-258">型で実装されている任意の静的エンコードメソッドを呼び出すことによって、*アンチ Xssenプログラマ*型を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="008d3-259">ただし、新しいアンチ XSS ルーチンを使用するための最も簡単な方法は、既定では、ASP.NET アプリケーションが*アンチ Xssenプログラマ*クラスを使用するように構成することです。</span><span class="sxs-lookup"><span data-stu-id="008d3-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="008d3-260">これを行うには、次の属性を web.config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="008d3-261">*EncoderType*属性が*アンチ Xssenプログラマ*型を使用するように設定されている場合、ASP.NET のすべての出力エンコードは、新しいエンコードルーチンを自動的に使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="008d3-262">これらは、ASP.NET 4.5 に組み込まれている外部アンチ Xss ライブラリの部分です。</span><span class="sxs-lookup"><span data-stu-id="008d3-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="008d3-263">*HtmlEncode*、 *HtmlFormUrlEncode*、 *htmlattributeencode*</span><span class="sxs-lookup"><span data-stu-id="008d3-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="008d3-264">*Xmlattributeencode*と*xmlencode*</span><span class="sxs-lookup"><span data-stu-id="008d3-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="008d3-265">*UrlEncode*と*urlpathencode* (new)</span><span class="sxs-lookup"><span data-stu-id="008d3-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="008d3-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="008d3-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="008d3-267">Websocket プロトコルのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="008d3-268">Websocket プロトコルは、標準ベースのネットワークプロトコルで、クライアントとサーバーの間で HTTP 経由のセキュリティで保護されたリアルタイムの双方向通信を確立する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="008d3-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="008d3-269">マイクロソフトは、IETF と W3C 標準の両方の本文を使用して、プロトコルの定義を支援してきました。</span><span class="sxs-lookup"><span data-stu-id="008d3-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="008d3-270">Websocket プロトコルは、ブラウザーだけでなく、すべてのクライアントでサポートされており、Microsoft は、クライアントとモバイルの両方のオペレーティングシステムで Websocket プロトコルをサポートする多くのリソースに投資しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="008d3-271">Websocket プロトコルを使用すると、クライアントとサーバーの間で実行時間の長いデータ転送を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="008d3-272">たとえば、チャットアプリケーションを作成する方がはるかに簡単です。クライアントとサーバーの間で実行時間の長い接続を確立できるからです。</span><span class="sxs-lookup"><span data-stu-id="008d3-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="008d3-273">ソケットの動作をシミュレートするために、定期的なポーリングや HTTP の長いポーリングなどの回避策を使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="008d3-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="008d3-274">ASP.NET 4.5 と IIS 8 には、低レベルの Websocket サポートが含まれており、ASP.NET 開発者は、Websocket オブジェクトで文字列とバイナリデータの両方を非同期的に読み取り、書き込みを行うために、マネージ Api を使用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="008d3-275">ASP.NET 4.5 には、Websocket プロトコルを操作するための型を含む新しい名前空間が*あります。*</span><span class="sxs-lookup"><span data-stu-id="008d3-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="008d3-276">ブラウザークライアントは、次の例に示すように、ASP.NET アプリケーションの URL を指す DOM *WebSocket*オブジェクトを作成することによって、websocket 接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="008d3-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="008d3-277">任意の種類のモジュールまたはハンドラーを使用して、ASP.NET に Websocket エンドポイントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="008d3-278">前の例では、.ashx ファイルを使用してハンドラーを簡単に作成できるため、.ashx ファイルが使用されていました。</span><span class="sxs-lookup"><span data-stu-id="008d3-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="008d3-279">Websocket プロトコルによれば、ASP.NET アプリケーションは、要求を HTTP GET 要求から Websocket 要求にアップグレードすることを示すことによって、クライアントの Websocket 要求を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="008d3-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="008d3-280">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="008d3-281">*AcceptWebSocketRequest*メソッドは、ASP.NET が現在の HTTP 要求をアンワインドしてから、関数デリゲートに制御を転送するため、関数デリゲートを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="008d3-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="008d3-282">概念的には、この方法は、バックグラウンド処理を実行するスレッド開始デリゲートを定義する、 *thread*の使用方法と似ています。</span><span class="sxs-lookup"><span data-stu-id="008d3-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="008d3-283">ASP.NET が完了し、クライアントが Websocket ハンドシェイクを正常に完了すると、ASP.NET はデリゲートを呼び出し、Websocket アプリケーションは実行を開始します。</span><span class="sxs-lookup"><span data-stu-id="008d3-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="008d3-284">次のコード例は、ASP.NET で組み込みの Websocket サポートを使用する単純な echo アプリケーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="008d3-285">*Await*キーワードと非同期タスクベースの操作に対する .net 4.5 のサポートは、websocket アプリケーションの作成に適しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="008d3-286">このコード例は、Websocket 要求が ASP.NET 内で完全に非同期に実行されることを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="008d3-287">アプリケーションは、await ソケットを呼び出すことによって、メッセージがクライアントから送信されるのを非同期に待機し*ます。ReceiveAsync*。</span><span class="sxs-lookup"><span data-stu-id="008d3-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="008d3-288">同様に、await ソケットを呼び出すことによって、クライアントに非同期メッセージを送信することもでき*ます。SendAsync*。</span><span class="sxs-lookup"><span data-stu-id="008d3-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="008d3-289">ブラウザーでは、アプリケーションは*onmessage*関数を介して websocket メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="008d3-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="008d3-290">ブラウザーからメッセージを送信するには、次の例に示すように、 *WebSocket* DOM 型の*send*メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="008d3-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="008d3-291">今後、この機能の更新プログラムがリリースされる可能性があります。これにより、Websocket アプリケーションのこのリリースで必要な低レベルのコーディングの一部が抽象化されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="008d3-292">バンドル化と縮小</span><span class="sxs-lookup"><span data-stu-id="008d3-292">Bundling and Minification</span></span>

<span data-ttu-id="008d3-293">バンドルを使用すると、個々の JavaScript ファイルと CSS ファイルを1つのファイルとして扱うことができるバンドルにまとめることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="008d3-294">不要な空白文字やその他の文字を削除することによって、では、JavaScript ファイルと CSS ファイルを縮小します。</span><span class="sxs-lookup"><span data-stu-id="008d3-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="008d3-295">これらの機能は、Web フォーム、ASP.NET MVC、および Web ページで動作します。</span><span class="sxs-lookup"><span data-stu-id="008d3-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="008d3-296">バンドルは、バンドルクラスまたはその子クラスである ScriptBundle とスタイルバンドルを使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="008d3-297">バンドルのインスタンスを構成すると、そのバンドルをグローバル BundleCollection インスタンスに追加するだけで、受信要求で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="008d3-298">既定のテンプレートでは、バンドルの構成は BundleConfig ファイルで実行されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="008d3-299">この既定の構成では、テンプレートで使用されるすべてのコアスクリプトと css ファイルのバンドルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="008d3-300">バンドルは、考えられるいくつかのヘルパーメソッドのいずれかを使用して、ビュー内から参照されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="008d3-301">デバッグモードとリリースモードでのバンドルのさまざまなマークアップのレンダリングをサポートするために、ScriptBundle クラスとスタイルバンドルクラスには、ヘルパーメソッドである Render が用意されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="008d3-302">デバッグモードの場合、Render はバンドル内の各リソースのマークアップを生成します。</span><span class="sxs-lookup"><span data-stu-id="008d3-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="008d3-303">リリースモードでは、Render はバンドル全体に対して1つのマークアップ要素を生成します。</span><span class="sxs-lookup"><span data-stu-id="008d3-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="008d3-304">デバッグモードとリリースモードを切り替えるには、次のように web.config でコンパイル要素の debug 属性を変更します。</span><span class="sxs-lookup"><span data-stu-id="008d3-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="008d3-305">また、最適化を有効または無効にするには、Bundletable.enableoptimization ときプロパティを使用して直接設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="008d3-306">ファイルがバンドルされている場合は、最初にアルファベット順 (**ソリューションエクスプローラー**に表示されます) に並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="008d3-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="008d3-307">次に、既知のライブラリとそのカスタム拡張 (jQuery、MooTools、Dojo など) が最初に読み込まれるように整理されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="008d3-308">たとえば、上記のスクリプトフォルダーのバンドルの最終的な順序は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="008d3-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="008d3-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="008d3-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="008d3-310">jquery-ui.js</span></span>
3. <span data-ttu-id="008d3-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="008d3-311">jquery.tools.js</span></span>
4. <span data-ttu-id="008d3-312">.js</span><span class="sxs-lookup"><span data-stu-id="008d3-312">a.js</span></span>

<span data-ttu-id="008d3-313">また、CSS ファイルはアルファベット順に並べ替えられた後、再構成され、.css とノーマライズが他のファイルよりも前に来るようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="008d3-314">上に示したスタイルフォルダーのバンドルの最終的な並べ替えは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="008d3-315">reset.css</span><span class="sxs-lookup"><span data-stu-id="008d3-315">reset.css</span></span>
2. <span data-ttu-id="008d3-316">content.css</span><span class="sxs-lookup"><span data-stu-id="008d3-316">content.css</span></span>
3. <span data-ttu-id="008d3-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="008d3-317">forms.css</span></span>
4. <span data-ttu-id="008d3-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="008d3-318">globals.css</span></span>
5. <span data-ttu-id="008d3-319">menu .css</span><span class="sxs-lookup"><span data-stu-id="008d3-319">menu.css</span></span>
6. <span data-ttu-id="008d3-320">styles.css</span><span class="sxs-lookup"><span data-stu-id="008d3-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="008d3-321">Web ホスティングのパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="008d3-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="008d3-322">.NET Framework 4.5 と Windows 8 では、web サーバーワークロードのパフォーマンスを大幅に向上させるのに役立つ機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="008d3-323">これには、減少 (最大35%) が含まれます。ASP.NET を使用する web ホスティングサイトの起動時間とメモリフットプリントの両方。</span><span class="sxs-lookup"><span data-stu-id="008d3-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="008d3-324">主要なパフォーマンス要因</span><span class="sxs-lookup"><span data-stu-id="008d3-324">Key performance factors</span></span>

<span data-ttu-id="008d3-325">理想的には、すべての web サイトがアクティブでメモリ内にあり、次の要求にすばやく応答できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="008d3-326">サイトの応答性に影響する要因は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="008d3-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="008d3-327">アプリケーションプールがリサイクルされた後にサイトが再起動するまでにかかる時間。</span><span class="sxs-lookup"><span data-stu-id="008d3-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="008d3-328">これは、サイトアセンブリがメモリ内に存在しなくなったときに、サイトの web サーバープロセスを起動するためにかかる時間です。</span><span class="sxs-lookup"><span data-stu-id="008d3-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="008d3-329">(プラットフォームアセンブリは、他のサイトで使用されているため、まだメモリ内にあります)。このような状況は、"コールドサイト、ウォームフレームワークスタートアップ"、または "コールドサイトスタートアップ" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="008d3-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="008d3-330">サイトがどの程度のメモリを占有しているか。</span><span class="sxs-lookup"><span data-stu-id="008d3-330">How much memory the site occupies.</span></span> <span data-ttu-id="008d3-331">この用語は、"サイトごとのメモリ消費" または "非共有の作業セット" です。</span><span class="sxs-lookup"><span data-stu-id="008d3-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="008d3-332">これらの要因の両方に重点を置いた新しいパフォーマンスの向上。</span><span class="sxs-lookup"><span data-stu-id="008d3-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="008d3-333">新しいパフォーマンス機能の要件</span><span class="sxs-lookup"><span data-stu-id="008d3-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="008d3-334">新しい機能の要件は、次のカテゴリに分けることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="008d3-335">.NET Framework 4 で実行される機能強化。</span><span class="sxs-lookup"><span data-stu-id="008d3-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="008d3-336">.NET Framework 4.5 が必要であるが、Windows の任意のバージョンで実行できる機能強化。</span><span class="sxs-lookup"><span data-stu-id="008d3-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="008d3-337">Windows 8 で実行されている .NET Framework 4.5 でのみ利用できる機能強化。</span><span class="sxs-lookup"><span data-stu-id="008d3-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="008d3-338">パフォーマンスは、有効にできる改善レベルごとに増加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="008d3-339">.NET Framework 4.5 の機能強化の一部では、他のシナリオにも適用される、より広範なパフォーマンス機能を利用しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="008d3-340">共通アセンブリの共有</span><span class="sxs-lookup"><span data-stu-id="008d3-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="008d3-341">**要件**: .NET Framework 4 および Visual Studio 11 DEVELOPER Preview SDK</span><span class="sxs-lookup"><span data-stu-id="008d3-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="008d3-342">サーバー上の異なるサイトでは、多くの場合、同じヘルパーアセンブリ (たとえば、スタートキットやサンプルアプリケーションのアセンブリ) を使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="008d3-343">各サイトには、Bin ディレクトリ内にこれらのアセンブリの独自のコピーがあります。</span><span class="sxs-lookup"><span data-stu-id="008d3-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="008d3-344">アセンブリのオブジェクトコードは同一ですが、物理的には独立したアセンブリなので、各アセンブリはコールドサイトの起動中に個別に読み取られ、メモリ内に個別に保持される必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="008d3-345">新しいインターン機能によって、このような非効率性が解決され、RAM の要件と読み込み時間が短縮されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="008d3-346">インターンを使用すると、Windows はファイルシステム内の各アセンブリのコピーを1つ保持できます。また、サイトの Bin フォルダー内の個々のアセンブリは、単一のコピーへのシンボリックリンクに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="008d3-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="008d3-347">個々のサイトに個別のバージョンのアセンブリが必要な場合は、シンボリックリンクがアセンブリの新しいバージョンに置き換えられ、そのサイトのみが影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="008d3-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="008d3-348">シンボリックリンクを使用してアセンブリを共有するには、aspnet\_という名前の新しいツールが必要です。これにより、インターンアセンブリのストアを作成して管理できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="008d3-349">これは、Visual Studio 11 Developer Preview SDK の一部として提供されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="008d3-350">(ただし、最新の[更新プログラム](https://support.microsoft.com/kb/2468871)がインストールされていることを前提として、.NET Framework 4 のみがインストールされているシステムで動作します)。</span><span class="sxs-lookup"><span data-stu-id="008d3-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="008d3-351">対象となるすべてのアセンブリがインターン化されていることを確認するには、aspnet\_を定期的に実行します (たとえば、定期的なタスクとして1週間に1回)。</span><span class="sxs-lookup"><span data-stu-id="008d3-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="008d3-352">一般的な用途は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="008d3-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="008d3-353">すべてのオプションを表示するには、引数を指定せずにツールを実行します。</span><span class="sxs-lookup"><span data-stu-id="008d3-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="008d3-354">高速起動のためのマルチコア JIT コンパイルの使用</span><span class="sxs-lookup"><span data-stu-id="008d3-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="008d3-355">**要件**: .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="008d3-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="008d3-356">コールドサイトを起動する場合、アセンブリをディスクから読み取る必要があるだけでなく、サイトを JIT コンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="008d3-357">複雑なサイトの場合、これによって大幅な遅延が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="008d3-358">.NET Framework 4.5 の新しい汎用手法により、使用可能なプロセッサコア全体に JIT コンパイルを分散することで、これらの遅延が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="008d3-359">これは、以前にサイトを起動したときに収集された情報を使用して、可能な限り早く実行されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="008d3-360">この[機能は、](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) system.string メソッドによって実装されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="008d3-361">ASP.NET では、複数のコアを使用した JIT コンパイルが既定で有効になっているため、この機能を利用するために何もする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="008d3-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="008d3-362">この機能を無効にする場合は、web.config ファイルで次の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="008d3-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="008d3-363">メモリ用に最適化するためのガベージコレクションのチューニング</span><span class="sxs-lookup"><span data-stu-id="008d3-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="008d3-364">**要件**: .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="008d3-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="008d3-365">サイトが実行されると、ガベージコレクター (GC) ヒープの使用は、メモリの消費に大きな影響をもたらす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="008d3-366">.NET Framework GC では、ガベージコレクターと同様に、CPU 時間 (コレクションの頻度と意味) とメモリ使用量 (新しいオブジェクト、解放されたオブジェクト、または解放可能なオブジェクトに使用される追加の領域) との間でトレードオフを行います。</span><span class="sxs-lookup"><span data-stu-id="008d3-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="008d3-367">以前のリリースでは、適切なバランスを実現するために GC を構成する方法についてのガイダンスを提供しています (たとえば、「 [ASP.NET 2.0/3.5 共有ホスティング構成](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="008d3-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="008d3-368">.NET Framework 4.5 では、複数のスタンドアロン設定ではなく、以前に推奨されていたすべての GC 設定と、サイトごとのパフォーマンスを向上する新しいチューニングを有効にする、ワークロード定義の構成設定を使用できます。ワーキングセット。</span><span class="sxs-lookup"><span data-stu-id="008d3-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="008d3-369">GC メモリのチューニングを有効にするには、Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config ファイルに次の設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="008d3-370">(Aspnet の変更に関する前のガイダンスに慣れている場合は、この設定が古い設定に置き換わることに注意してください。たとえば、gcServer や gcConcurrent などを設定する必要はありません。古い設定を削除する必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="008d3-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="008d3-371">Web アプリケーションのプリフェッチ</span><span class="sxs-lookup"><span data-stu-id="008d3-371">Prefetching for web applications</span></span>

<span data-ttu-id="008d3-372">**要件**: Windows 8 で実行されている .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="008d3-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="008d3-373">いくつかのリリースでは、Windows には、アプリケーションの起動に伴うディスク読み取りコストを削減する[prefetcher](http://en.wikipedia.org/wiki/Prefetcher)と呼ばれるテクノロジが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="008d3-374">コールドスタートはクライアントアプリケーションの主な問題であるため、このテクノロジは、サーバーにとって不可欠なコンポーネントのみを含む Windows Server には含まれていません。</span><span class="sxs-lookup"><span data-stu-id="008d3-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="008d3-375">プリフェッチは、Windows Server の最新バージョンで使用できるようになりました。これにより、個々の web サイトの起動を最適化できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="008d3-376">Windows Server の場合、prefetcher は既定では有効になっていません。</span><span class="sxs-lookup"><span data-stu-id="008d3-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="008d3-377">高密度 web ホスティング用に prefetcher を有効にして構成するには、コマンドラインで次のコマンドセットを実行します。</span><span class="sxs-lookup"><span data-stu-id="008d3-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="008d3-378">次に、prefetcher と ASP.NET アプリケーションを統合するために、web.config ファイルに次のを追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="008d3-379">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="008d3-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="008d3-380">厳密に型指定されたデータ コントロール</span><span class="sxs-lookup"><span data-stu-id="008d3-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="008d3-381">ASP.NET 4.5 では、Web フォームにデータを操作するための機能強化が含まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="008d3-382">1つ目の改善点は、厳密に型指定されたデータコントロールです。</span><span class="sxs-lookup"><span data-stu-id="008d3-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="008d3-383">以前のバージョンの ASP.NET の Web フォームコントロールでは、 *Eval*とデータバインディング式を使用してデータバインド値を表示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="008d3-384">双方向のデータバインディングの場合は、 *Bind*を使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="008d3-385">実行時に、これらの呼び出しは、リフレクションを使用して指定されたメンバーの値を読み取り、結果をマークアップに表示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="008d3-386">この方法を使用すると、任意の整形されていないデータに対して簡単にデータをバインドできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="008d3-387">ただし、このようなデータバインディング式では、メンバー名の IntelliSense、ナビゲーション (定義への移動など)、またはこれらの名前のコンパイル時チェックなどの機能をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="008d3-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="008d3-388">この問題に対処するために、ASP.NET 4.5 では、コントロールがバインドされているデータのデータ型を宣言する機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="008d3-389">これは、新しい*ItemType*プロパティを使用して行います。</span><span class="sxs-lookup"><span data-stu-id="008d3-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="008d3-390">このプロパティを設定すると、 *Item*と*BindItem*の2つの新しい型指定された変数が、データバインド式のスコープで使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="008d3-391">変数は厳密に型指定されているため、Visual Studio の開発エクスペリエンスのすべての利点が得られます。</span><span class="sxs-lookup"><span data-stu-id="008d3-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="008d3-392">双方向のデータバインディング式の場合は、 *BindItem*変数を使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="008d3-393">データバインディングをサポートする ASP.NET Web フォームフレームワークのほとんどのコントロールは、 *ItemType*プロパティをサポートするように更新されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="008d3-394">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="008d3-394">Model Binding</span></span>

<span data-ttu-id="008d3-395">モデルバインドは、コード中心のデータアクセスを操作するために、ASP.NET Web フォームコントロールのデータバインディングを拡張します。</span><span class="sxs-lookup"><span data-stu-id="008d3-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="008d3-396">*ObjectDataSource*コントロールの概念と、ASP.NET MVC のモデルバインドの概念が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="008d3-397">データの選択</span><span class="sxs-lookup"><span data-stu-id="008d3-397">Selecting data</span></span>

<span data-ttu-id="008d3-398">モデルバインドを使用してデータを選択するようにデータコントロールを構成するには、コントロールの*SelectMethod*プロパティを、ページのコード内のメソッドの名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="008d3-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="008d3-399">データコントロールは、ページライフサイクルの適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。</span><span class="sxs-lookup"><span data-stu-id="008d3-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="008d3-400">*DataBind*メソッドを明示的に呼び出す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="008d3-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="008d3-401">次の例では、 *GridView*コントロールは*GetCategories*という名前のメソッドを使用するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="008d3-402">*GetCategories*メソッドは、ページのコードで作成します。</span><span class="sxs-lookup"><span data-stu-id="008d3-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="008d3-403">単純な select 操作の場合、メソッドはパラメーターを必要とせず、 *IEnumerable*または*IQueryable*オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="008d3-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="008d3-404">新しい*ItemType*プロパティが設定されている場合 (前述の厳密に型指定された[データコントロール](#_Toc318097386)で説明されているように、厳密に型指定されたデータバインディング式を有効にする)、これらのインターフェイスのジェネリックバージョンを *&gt;&lt;* *&gt;&lt;* 返す必要があります。これは、 *itemtype*プロパティの型 ( *iqueryable&lt;Category&gt;* など) と一致する*t*パラメーターを</span><span class="sxs-lookup"><span data-stu-id="008d3-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="008d3-405">次の例は、 *GetCategories*メソッドのコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="008d3-406">この例では、Northwind サンプルデータベースで Entity Framework Code First モデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="008d3-407">このコードにより、 *Include*メソッドを使用して各カテゴリの関連製品の詳細が返されるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="008d3-408">(これにより、マークアップ内の*TemplateField*要素に、各カテゴリの製品数が表示されます。 [n + 1 を選択](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)する必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="008d3-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="008d3-409">ページを実行すると、 *GridView*コントロールは*GetCategories*メソッドを自動的に呼び出し、構成されたフィールドを使用して返されたデータをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="008d3-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="008d3-410">Select メソッドは*IQueryable*オブジェクトを返すため、 *GridView*コントロールはクエリを実行する前にさらに操作できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="008d3-411">たとえば、 *GridView*コントロールでは、返された*IQueryable*オブジェクトを実行する前に、並べ替えとページングを行うためのクエリ式を追加できます。これにより、基になる LINQ プロバイダーによってこれらの操作が実行されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="008d3-412">この場合、Entity Framework によって、これらの操作がデータベースで確実に実行されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="008d3-413">次の例は、並べ替えとページングを可能にするために変更された*GridView*コントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="008d3-414">これで、ページの実行時に、コントロールは現在のデータページだけが表示され、選択された列によって並べ替えられていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="008d3-415">返されたデータをフィルター処理するには、select メソッドにパラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="008d3-416">これらのパラメーターは、実行時にモデルバインディングによって設定されます。また、これらのパラメーターを使用して、データを返す前にクエリを変更できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="008d3-417">たとえば、クエリ文字列にキーワードを入力して、ユーザーが製品をフィルター処理できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="008d3-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="008d3-418">パラメーターをメソッドに追加し、パラメーター値を使用するようにコードを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="008d3-419">このコードには、*キーワード*に値が指定されている場合は*Where*式が含まれ、その後クエリ結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="008d3-420">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="008d3-420">Value providers</span></span>

<span data-ttu-id="008d3-421">前の例は、*キーワード*パラメーターの値の取得元の場所に固有のものではありませんでした。</span><span class="sxs-lookup"><span data-stu-id="008d3-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="008d3-422">この情報を示すために、パラメーター属性を使用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="008d3-423">この例では、 *System.web binding*名前空間にある*querystringattribute*クラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="008d3-424">これにより、モデルバインドは、クエリ文字列から実行時に*キーワード*パラメーターに値をバインドしようとするように指示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="008d3-425">(この場合、型変換の実行が必要になることがありますが、この場合はそうではありません)。値を指定できず、型が null 非許容である場合は、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="008d3-426">これらのメソッドの値のソースは、値プロバイダーと呼ばれ、使用する値プロバイダーを示すパラメーター属性は、値プロバイダー属性と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="008d3-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="008d3-427">Web フォームには、Web フォームアプリケーションでのユーザー入力のすべての一般的なソース (クエリ文字列、cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイルプロパティなど) に関する値プロバイダーと対応する属性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="008d3-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="008d3-428">カスタム値プロバイダーを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-428">You can also write custom value providers.</span></span>

<span data-ttu-id="008d3-429">既定では、値プロバイダーコレクション内の値を検索するためのキーとしてパラメーター名が使用されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="008d3-430">この例のコードでは、キーワードという名前のクエリ文字列値が検索されます (たとえば、~/default.aspx? keyword = chef)。</span><span class="sxs-lookup"><span data-stu-id="008d3-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="008d3-431">パラメーター属性に引数として渡すことによって、カスタムキーを指定できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="008d3-432">たとえば、q という名前のクエリ文字列変数の値を使用するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="008d3-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="008d3-433">このメソッドがページのコード内にある場合、ユーザーはクエリ文字列を使用してキーワードを渡すことによって結果をフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="008d3-434">モデルバインドでは、値の読み取り、null 値のチェック、適切な型への変換の試行、変換が成功したかどうかの確認、最後にの値の使用など、手作業でコーディングする必要がある多くのタスクが実行されます。照会.</span><span class="sxs-lookup"><span data-stu-id="008d3-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="008d3-435">モデルバインドを使用すると、コードがはるかに少なくなり、アプリケーション全体で機能を再利用することができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="008d3-436">コントロールの値によるフィルター処理</span><span class="sxs-lookup"><span data-stu-id="008d3-436">Filtering by values from a control</span></span>

<span data-ttu-id="008d3-437">例を拡張して、ユーザーがドロップダウンリストからフィルター値を選択できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="008d3-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="008d3-438">次のドロップダウンリストをマークアップに追加し、 *SelectMethod*プロパティを使用して別のメソッドからデータを取得するように構成します。</span><span class="sxs-lookup"><span data-stu-id="008d3-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="008d3-439">通常は、 *EmptyDataTemplate*要素を*GridView*コントロールに追加して、一致する製品が見つからない場合にコントロールがメッセージを表示するようにします。</span><span class="sxs-lookup"><span data-stu-id="008d3-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="008d3-440">ページコードで、ドロップダウンリストの新しい select メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="008d3-441">最後に、 *Getproducts* select メソッドを更新して、選択したカテゴリの ID を含む新しいパラメーターをドロップダウンリストから取得します。</span><span class="sxs-lookup"><span data-stu-id="008d3-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="008d3-442">ページが実行されると、ユーザーはドロップダウンリストからカテゴリを選択できるようになり、フィルター処理されたデータを表示するために*GridView*コントロールが自動的に再バインドされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="008d3-443">これが可能なのは、モデルバインドが select メソッドのパラメーターの値を追跡し、ポストバック後にパラメーター値が変更されたかどうかを検出するためです。</span><span class="sxs-lookup"><span data-stu-id="008d3-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="008d3-444">その場合、モデルバインドによって、関連付けられたデータコントロールが強制的にデータに再バインドされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="008d3-445">HTML エンコードされたデータバインディング式</span><span class="sxs-lookup"><span data-stu-id="008d3-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="008d3-446">データバインディング式の結果を HTML エンコードできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="008d3-447">コロン (:) を追加します。データバインディング式をマークする &lt;% # プレフィックスの末尾。</span><span class="sxs-lookup"><span data-stu-id="008d3-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="008d3-448">控えめに検証</span><span class="sxs-lookup"><span data-stu-id="008d3-448">Unobtrusive Validation</span></span>

<span data-ttu-id="008d3-449">クライアント側の検証ロジックに控えめな JavaScript を使用するように、組み込みの検証コントロールを構成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="008d3-450">これにより、ページマークアップでインラインでレンダリングされる JavaScript の量が大幅に減少し、ページ全体のサイズが縮小されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="008d3-451">次のいずれかの方法で、控えめな JavaScript をバリデーターコントロール用に構成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="008d3-452">次の設定を Web.config ファイルの *&lt;appSettings&gt;* 要素に追加することでグローバルに行うことができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="008d3-453">静的な*UnobtrusiveValidationMode*プロパティを*UnobtrusiveValidationMode*に設定することによってグローバルに実行します (通常は、*アプリケーション\_* 、global.asax ファイルの Start メソッド)。</span><span class="sxs-lookup"><span data-stu-id="008d3-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="008d3-454">*ページクラスの*new *UnobtrusiveValidationMode*プロパティを*UnobtrusiveValidationMode*に設定して、ページに対して個別に設定します。</span><span class="sxs-lookup"><span data-stu-id="008d3-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="008d3-455">HTML5 の更新プログラム</span><span class="sxs-lookup"><span data-stu-id="008d3-455">HTML5 Updates</span></span>

<span data-ttu-id="008d3-456">HTML5 の新機能を利用するために、Web フォームサーバーコントロールにいくつかの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="008d3-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="008d3-457">*TextBox*コントロールの*TextMode*プロパティが更新され、 *email*や*datetime*などの新しい HTML5 入力型がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="008d3-458">*FileUpload*コントロールで、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="008d3-459">検証コントロールは、HTML5 入力要素の検証をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="008d3-460">URL を表す属性を持つ新しい HTML5 要素では、runat = "server" がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="008d3-461">その結果、URL パスで ASP.NET 規則を使用できます。たとえば、~ 演算子を使用すると、アプリケーションルートを表すことができます (&lt;video runat = "server" src = "~/myvideo"/&gt;)。</span><span class="sxs-lookup"><span data-stu-id="008d3-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="008d3-462">*UpdatePanel*コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="008d3-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="008d3-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="008d3-464">ASP.NET MVC 4 Beta が Visual Studio 11 Beta に含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="008d3-465">ASP.NET MVC は、モデルビューコントローラー (MVC) パターンを利用することで、高度なテストが可能な、保守しやすい Web アプリケーションを開発するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="008d3-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="008d3-466">ASP.NET MVC 4 を使用すると、モバイル Web 用のアプリケーションの構築が容易になり、ASP.NET Web API が含まれます。これにより、任意のデバイスに接続できる HTTP サービスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="008d3-467">詳細については、 [ASP.NET MVC 4 リリースノート](mvc4-release-notes.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="008d3-468">ASP.NET Web ページ 2</span><span class="sxs-lookup"><span data-stu-id="008d3-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="008d3-469">次のような新機能があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-469">New features include the following:</span></span>

- <span data-ttu-id="008d3-470">新規および更新されたサイトテンプレート。</span><span class="sxs-lookup"><span data-stu-id="008d3-470">New and updated site templates.</span></span>
- <span data-ttu-id="008d3-471">*検証*ヘルパーを使用して、サーバー側およびクライアント側の検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="008d3-472">アセットマネージャーを使用してスクリプトを登録する機能。</span><span class="sxs-lookup"><span data-stu-id="008d3-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="008d3-473">OAuth および OpenID を使用した Facebook およびその他のサイトからのログインの有効化。</span><span class="sxs-lookup"><span data-stu-id="008d3-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="008d3-474">*Maps*ヘルパーを使用してマップを追加します。</span><span class="sxs-lookup"><span data-stu-id="008d3-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="008d3-475">Web ページアプリケーションをサイドバイサイドで実行する。</span><span class="sxs-lookup"><span data-stu-id="008d3-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="008d3-476">モバイルデバイスのレンダリングページ。</span><span class="sxs-lookup"><span data-stu-id="008d3-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="008d3-477">これらの機能とページ全体のコード例の詳細については、 [Web ページ 2 Beta のトップ機能](https://go.microsoft.com/fwlink/?LinkID=227824)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="008d3-478">Visual Web Developer 11 Beta</span><span class="sxs-lookup"><span data-stu-id="008d3-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="008d3-479">このセクションでは、Visual Web Developer 11 Beta および Visual Studio 2012 リリース候補での web 開発の機能強化について説明します。</span><span class="sxs-lookup"><span data-stu-id="008d3-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="008d3-480">Visual Studio 2010 と Visual Studio 2012 リリース候補間のプロジェクト共有 (プロジェクト互換性)</span><span class="sxs-lookup"><span data-stu-id="008d3-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="008d3-481">Visual Studio 2012 リリース候補が表示されるまで、新しいバージョンの Visual Studio で既存のプロジェクトを開くと、変換ウィザードが起動します。</span><span class="sxs-lookup"><span data-stu-id="008d3-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="008d3-482">これにより、プロジェクトとソリューションのコンテンツ (アセット) を旧バージョンと互換性のない新しい形式にアップグレードすることが強制されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="008d3-483">そのため、変換後に、以前のバージョンの Visual Studio でプロジェクトを開くことができませんでした。</span><span class="sxs-lookup"><span data-stu-id="008d3-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="008d3-484">多くのお客様は、これが適切なアプローチではなかったことを伝えてきました。</span><span class="sxs-lookup"><span data-stu-id="008d3-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="008d3-485">Visual Studio 11 Beta では、Visual Studio 2010 SP1 でのプロジェクトとソリューションの共有がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="008d3-486">これは、Visual Studio 2012 リリース候補で2010プロジェクトを開いた場合でも、Visual Studio 2010 SP1 でプロジェクトを開くことができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="008d3-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="008d3-487">いくつかの種類のプロジェクトは、Visual Studio 2010 SP1 と Visual Studio 2012 リリース候補間で共有することはできません。</span><span class="sxs-lookup"><span data-stu-id="008d3-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="008d3-488">これには、いくつかの古いプロジェクト (ASP.NET MVC 2 プロジェクトなど) や特別な目的 (セットアッププロジェクトなど) のプロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="008d3-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="008d3-489">Visual studio 11 Beta で Visual Studio 2010 SP1 Web プロジェクトを初めて開くと、次のプロパティがプロジェクトファイルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="008d3-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="008d3-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="008d3-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="008d3-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="008d3-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="008d3-492">OldToolsVersion</span></span>
- <span data-ttu-id="008d3-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="008d3-493">VisualStudioVersion</span></span>
- <span data-ttu-id="008d3-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="008d3-494">VSToolsPath</span></span>

<span data-ttu-id="008d3-495">FileUpgradeFlags、UpgradeBackupLocation、および OldToolsVersion は、プロジェクトファイルをアップグレードするプロセスによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="008d3-496">Visual Studio 2010 では、プロジェクトの操作には影響しません。</span><span class="sxs-lookup"><span data-stu-id="008d3-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="008d3-497">VisualStudioVersion は、現在のプロジェクトの Visual Studio のバージョンを示す MSBuild 4.5 で使用される新しいプロパティです。</span><span class="sxs-lookup"><span data-stu-id="008d3-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="008d3-498">このプロパティは、MSBuild 4.0 (Visual Studio 2010 SP1 で使用される MSBuild のバージョン) には存在しないため、既定値をプロジェクトファイルに挿入します。</span><span class="sxs-lookup"><span data-stu-id="008d3-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="008d3-499">VSToolsPath プロパティは、MSBuildExtensionsPath32 設定で表されるパスからインポートする正しい .targets ファイルを決定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="008d3-500">Import 要素に関連するいくつかの変更もあります。</span><span class="sxs-lookup"><span data-stu-id="008d3-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="008d3-501">これらの変更は、両方のバージョンの Visual Studio 間の互換性をサポートするために必要です。</span><span class="sxs-lookup"><span data-stu-id="008d3-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="008d3-502">2つの異なるコンピューター上の Visual Studio 2010 SP1 と Visual Studio 11 Beta の間でプロジェクトを共有する場合、およびプロジェクトに App\_Data フォルダー内のローカルデータベースが含まれている場合は、データベースで使用される SQL Server のバージョンが両方のコンピューターにインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="008d3-503">ASP.NET 4.5 Web サイトテンプレートの構成の変更</span><span class="sxs-lookup"><span data-stu-id="008d3-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="008d3-504">Visual Studio 2012 リリース候補の web サイトテンプレートを使用して作成されたサイト*の既定の web.config ファイル*には、次のような変更が加えられました。</span><span class="sxs-lookup"><span data-stu-id="008d3-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="008d3-505">`<httpRuntime>` 要素で、`encoderType` 属性が既定で設定され、ASP.NET に追加されたアンチ Xss 型が使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="008d3-506">詳細については、「 [xss」ライブラリ](#_Toc318097382)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="008d3-507">また `<httpRuntime>` 要素では、`requestValidationMode` 属性は "4.5" に設定されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="008d3-508">つまり、既定では、要求の検証は、遅延 ("レイジー") 検証を使用するように構成されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="008d3-509">詳細については、「 [New ASP.NET Request Validation Features](#_Toc318097379)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="008d3-510">`<system.webServer>` セクションの `<modules>` 要素には、`runAllManagedModulesForAllRequests` 属性が含まれていません。</span><span class="sxs-lookup"><span data-stu-id="008d3-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="008d3-511">(既定値は false です)。これは、SP1 に更新されていないバージョンの IIS 7 を使用している場合、新しいサイトでのルーティングに問題がある可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="008d3-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="008d3-512">詳細については、「 [ASP.NET Routing の IIS 7 のネイティブサポート](#Native_Support_In_IIS7_For_ASPNET_Routine)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="008d3-513">これらの変更は、既存のアプリケーションには影響しません。</span><span class="sxs-lookup"><span data-stu-id="008d3-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="008d3-514">ただし、新しいテンプレートを使用して ASP.NET 4.5 用に作成した既存の web サイトと新しい web サイトの動作の違いを表している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="008d3-515">ASP.NET ルーティング用の IIS 7 でのネイティブサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="008d3-516">このように ASP.NET を変更することはできませんが、SP1 更新プログラムが適用されていないバージョンの IIS 7 を使用している場合に影響を与える可能性がある新しい web サイトプロジェクトのテンプレートが変更されました。</span><span class="sxs-lookup"><span data-stu-id="008d3-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="008d3-517">ASP.NET では、ルーティングをサポートするために、次の構成設定をアプリケーションに追加できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="008d3-518">**RunallmanagedASP.NET Forallrequests**が true の場合、url に *.aspx*、 *mvc*、または同様の拡張子がない場合でも、`http://mysite/myapp/home` のような url はに移動します。</span><span class="sxs-lookup"><span data-stu-id="008d3-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="008d3-519">IIS 7 に対して行われた更新により、 **Runallmanagedモジュール Forallrequests**が不要になり、ASP.NET ルーティングがネイティブでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="008d3-520">(更新プログラムの詳細については、Microsoft サポートの記事で、[特定の iis 7.0 または iis 7.5 ハンドラーが、url の末尾がピリオドではない要求を処理](https://support.microsoft.com/kb/980368)できるようにする更新プログラムについて説明しています)。</span><span class="sxs-lookup"><span data-stu-id="008d3-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="008d3-521">Web サイトが IIS 7 で実行されており、IIS が更新されている場合は、 **Runallmanagedモジュール Forallrequests**を true に設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="008d3-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="008d3-522">実際には、要求に不要な処理オーバーヘッドが追加されるため、true に設定することは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="008d3-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="008d3-523">この設定が true の場合、 *.htm*、 *.jpg*、およびその他の静的ファイルの要求も含め、すべての要求が ASP.NET 要求パイプラインを経由します。</span><span class="sxs-lookup"><span data-stu-id="008d3-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="008d3-524">Visual Studio 2012 RC に用意されているテンプレートを使用して新しい ASP.NET 4.5 web サイトを作成した場合、web サイトの構成に**Runallmanagedモジュール Forallrequests**設定は含まれません。</span><span class="sxs-lookup"><span data-stu-id="008d3-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="008d3-525">これは、既定では false に設定されていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="008d3-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="008d3-526">SP1 がインストールされていない状態で Windows 7 で web サイトを実行すると、IIS 7 には必要な更新プログラムが含まれません。</span><span class="sxs-lookup"><span data-stu-id="008d3-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="008d3-527">その結果、ルーティングは機能しなくなり、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="008d3-528">ルーティングが機能しない問題が発生した場合は、次のいずれかの操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="008d3-529">Windows 7 を SP1 に更新します。これにより、IIS 7 に更新プログラムが追加されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="008d3-530">前述の Microsoft サポートの記事で説明されている更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="008d3-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="008d3-531">その web サイトの Web.config ファイルで**Runallmanagedモジュール Forallrequests**を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="008d3-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="008d3-532">これにより、要求にオーバーヘッドがいくつか追加されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="008d3-533">HTML エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="008d3-534">スマートタスク</span><span class="sxs-lookup"><span data-stu-id="008d3-534">Smart Tasks</span></span>

<span data-ttu-id="008d3-535">デザインビューでは、多くの場合、サーバーコントロールの複雑なプロパティを設定するためのダイアログボックスとウィザードが関連付けられています。</span><span class="sxs-lookup"><span data-stu-id="008d3-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="008d3-536">たとえば、特別なダイアログボックスを使用して、 *Repeater*コントロールにデータソースを追加したり、 *GridView*コントロールに列を追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="008d3-537">ただし、複合プロパティのこの種の UI ヘルプは、ソースビューでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="008d3-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="008d3-538">そのため、Visual Studio 11 では、ソースビューのスマートタスクが導入されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="008d3-539">スマートタスクは、および Visual Basic エディターで一般的に使用されるC#機能のコンテキストに対応したショートカットです。</span><span class="sxs-lookup"><span data-stu-id="008d3-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="008d3-540">ASP.NET Web フォームコントロールでは、挿入ポイントが要素内にある場合、スマートタスクは、サーバータグに小さいグリフとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="008d3-541">グリフをクリックするか、CTRL +. キーを押すとスマートタスクが拡張されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="008d3-542">(ドット)。コードエディターと同様です。</span><span class="sxs-lookup"><span data-stu-id="008d3-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="008d3-543">次に、デザインビューのスマートタスクに似たショートカットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="008d3-544">たとえば、前の図のスマートタスクは、GridView タスクのオプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="008d3-545">[列の編集] を選択すると、次のダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="008d3-546">ダイアログボックスに入力すると、デザインビューで設定できるものと同じプロパティが設定されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="008d3-547">[OK] をクリックすると、コントロールのマークアップが新しい設定で更新されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="008d3-548">WAI-ARIA のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-548">WAI-ARIA support</span></span>

<span data-ttu-id="008d3-549">アクセス可能な web サイトの作成がますます重要になっています。</span><span class="sxs-lookup"><span data-stu-id="008d3-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="008d3-550">[WAI アクセシビリティ標準](http://www.w3.org/WAI/intro/aria)では、開発者がアクセス可能な web サイトを作成する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="008d3-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="008d3-551">この standard は、Visual Studio で完全にサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="008d3-552">たとえば、 *role*属性には IntelliSense が完全に含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="008d3-553">また、WAI 標準では、 *aria*というプレフィックスが付いた属性も導入されています。これにより、HTML5 ドキュメントにセマンティクスを追加できるようになります。</span><span class="sxs-lookup"><span data-stu-id="008d3-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="008d3-554">Visual Studio*では、* 次の aria 属性も完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="008d3-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="008d3-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="008d3-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="008d3-556">新しい HTML5 スニペット</span><span class="sxs-lookup"><span data-stu-id="008d3-556">New HTML5 snippets</span></span>

<span data-ttu-id="008d3-557">一般的に使用される HTML5 マークアップをより迅速かつ簡単に記述できるように、Visual Studio には多くのスニペットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="008d3-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="008d3-558">ビデオスニペットの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="008d3-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="008d3-559">スニペットを呼び出すには、IntelliSense で要素が選択されたときに Tab キーを2回押します。</span><span class="sxs-lookup"><span data-stu-id="008d3-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="008d3-560">これにより、カスタマイズできるスニペットが生成されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="008d3-561">ユーザーコントロールに抽出</span><span class="sxs-lookup"><span data-stu-id="008d3-561">Extract to user control</span></span>

<span data-ttu-id="008d3-562">大規模な web ページでは、個々の部分をユーザーコントロールに移動することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="008d3-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="008d3-563">このリファクタリング形式を使用すると、ページの読みやすさを向上させることができ、ページの構造を簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="008d3-564">これを簡単にするために、ソースビューで Web フォームページを編集するときに、ページ内のテキストを選択して右クリックし、[ユーザーコントロールに抽出] を選択できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="008d3-565">属性のコードナゲットの IntelliSense</span><span class="sxs-lookup"><span data-stu-id="008d3-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="008d3-566">Visual Studio では、すべてのページまたはコントロールにサーバー側のコードナゲットの IntelliSense が常に用意されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="008d3-567">Visual Studio には、HTML 属性でコードナゲットの IntelliSense も含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="008d3-568">これにより、データバインディング式を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="008d3-569">開始タグまたは終了タグの名前を変更するときに、一致するタグの名前を自動的に変更する</span><span class="sxs-lookup"><span data-stu-id="008d3-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="008d3-570">HTML 要素の名前を変更すると (たとえば、 *div*タグが*ヘッダー*タグになるように変更した場合)、対応する開始タグまたは終了タグもリアルタイムで変更されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="008d3-571">これにより、終了タグの変更や間違ったタグの変更を忘れた場合に、エラーを回避できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="008d3-572">イベントハンドラーの生成</span><span class="sxs-lookup"><span data-stu-id="008d3-572">Event handler generation</span></span>

<span data-ttu-id="008d3-573">Visual Studio にソースビューの機能が追加され、イベントハンドラーを作成して手動でバインドできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="008d3-574">ソースビューでイベント名を編集している場合は、IntelliSense によって &lt;新しいイベント&gt;が表示されます。これにより、正しいシグネチャを持つページのコードにイベントハンドラーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="008d3-575">既定では、イベントハンドラーは、イベント処理メソッドの名前としてコントロールの ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="008d3-576">結果のイベントハンドラーは次のようになります (この例C#では)。</span><span class="sxs-lookup"><span data-stu-id="008d3-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="008d3-577">スマートインデント</span><span class="sxs-lookup"><span data-stu-id="008d3-577">Smart indent</span></span>

<span data-ttu-id="008d3-578">空の HTML 要素内で Enter キーを押すと、エディターによって、カーソル位置が右側に配置されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="008d3-579">この場所で Enter キーを押すと、終了タグが下へ移動して、開始タグと一致するようにインデントされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="008d3-580">挿入ポイントもインデントされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="008d3-581">ステートメント入力候補を自動的に減らす</span><span class="sxs-lookup"><span data-stu-id="008d3-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="008d3-582">Visual Studio の IntelliSense の一覧が、関連するオプションのみを表示するように入力した内容に基づいてフィルター処理されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="008d3-583">IntelliSense では、IntelliSense の一覧内の個々の単語のタイトルケースに基づいてフィルター処理も行います。</span><span class="sxs-lookup"><span data-stu-id="008d3-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="008d3-584">たとえば、「dl」と入力すると、dl と asp: DataList の両方が表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="008d3-585">この機能により、既知の要素に対してステートメントの入力候補が高速になります。</span><span class="sxs-lookup"><span data-stu-id="008d3-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="008d3-586">JavaScript エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-586">JavaScript Editor</span></span>

<span data-ttu-id="008d3-587">Visual Studio 2012 リリース候補の JavaScript エディターはまったく新しいものであり、Visual Studio での JavaScript の操作エクスペリエンスが大幅に向上しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="008d3-588">コードのアウトライン表示</span><span class="sxs-lookup"><span data-stu-id="008d3-588">Code outlining</span></span>

<span data-ttu-id="008d3-589">すべての関数に対してアウトライン領域が自動的に作成されるようになりました。これにより、現在のフォーカスに関連しないファイルの一部を折りたたむことができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="008d3-590">かっこの一致</span><span class="sxs-lookup"><span data-stu-id="008d3-590">Brace matching</span></span>

<span data-ttu-id="008d3-591">左中かっこまたは右中かっこに挿入ポイントを配置すると、エディターによって一致するものが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="008d3-592">定義に移動</span><span class="sxs-lookup"><span data-stu-id="008d3-592">Go to Definition</span></span>

<span data-ttu-id="008d3-593">[定義へ移動] コマンドを使用すると、関数または変数のソースに移動できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="008d3-594">ECMAScript5 のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-594">ECMAScript5 support</span></span>

<span data-ttu-id="008d3-595">このエディターは、JavaScript 言語を記述する最新バージョンである ECMAScript5 の新しい構文と Api をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="008d3-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="008d3-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="008d3-596">DOM IntelliSense</span></span>

<span data-ttu-id="008d3-597">DOM Api 用の IntelliSense が改善され、 *Queryselector*、DOM Storage、クロスドキュメントメッセージング、 *canvas*などの多くの新しい HTML5 api がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="008d3-598">DOM IntelliSense は、ネイティブタイプライブラリ定義ではなく、単一の単純な JavaScript ファイルによって駆動されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="008d3-599">これにより、拡張や置換を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="008d3-600">VSDOC 署名のオーバーロード</span><span class="sxs-lookup"><span data-stu-id="008d3-600">VSDOC signature overloads</span></span>

<span data-ttu-id="008d3-601">次の例に示すように、新しい *&lt;signature&gt;* 要素を使用して、JavaScript 関数の個別のオーバーロードに対して詳細な IntelliSense コメントを宣言できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="008d3-602">暗黙の参照</span><span class="sxs-lookup"><span data-stu-id="008d3-602">Implicit references</span></span>

<span data-ttu-id="008d3-603">特定の JavaScript ファイルまたはブロックが参照するファイルの一覧に暗黙的に含まれる JavaScript ファイルを中央のリストに追加できるようになりました。つまり、そのコンテンツに対して IntelliSense を利用できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="008d3-604">たとえば、ファイルの中央のリストに jQuery ファイルを追加することができます。また、明示的に参照しているかどうかにかかわらず、ファイルの JavaScript ブロックで jQuery 関数の IntelliSense を利用できます (///&lt;reference/&gt;を使用します)。</span><span class="sxs-lookup"><span data-stu-id="008d3-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="008d3-605">CSS エディター</span><span class="sxs-lookup"><span data-stu-id="008d3-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="008d3-606">ステートメント入力候補を自動的に減らす</span><span class="sxs-lookup"><span data-stu-id="008d3-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="008d3-607">CSS の IntelliSense の一覧は、選択したスキーマでサポートされている CSS プロパティと値に基づいてフィルター処理されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="008d3-608">IntelliSense では、case 検索のタイトルもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="008d3-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="008d3-609">階層インデント</span><span class="sxs-lookup"><span data-stu-id="008d3-609">Hierarchical indentation</span></span>

<span data-ttu-id="008d3-610">CSS エディターは、階層的なルールを表示するためにインデントを使用します。これにより、カスケードルールが論理的に編成される方法の概要が示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="008d3-611">次の例では、セレクター #list がリストのカスケード子であるため、インデントされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="008d3-612">次の例は、より複雑な継承を示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="008d3-613">ルールのインデントは、親ルールによって決定されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="008d3-614">階層インデントは既定で有効になっていますが、[オプション] ダイアログボックス (メニューバーの [ツール]、[オプション]) を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="008d3-615">CSS ハックのサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-615">CSS hacks support</span></span>

<span data-ttu-id="008d3-616">何百もの実世界の CSS ファイルを分析することで、CSS ハッキングが非常に一般的であることがわかります。また、Visual Studio で最も広く使用されているものがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="008d3-617">このサポートには、IntelliSense と、star (\*) プロパティとアンダースコア (\_) プロパティのハッキングの検証が含まれます。</span><span class="sxs-lookup"><span data-stu-id="008d3-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="008d3-618">一般的なセレクターハックもサポートされているので、適用された場合でも階層インデントが維持されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="008d3-619">Internet Explorer 7 のターゲットとして使用される一般的なセレクターハックは、セレクターを*先頭に子と html で\** します。</span><span class="sxs-lookup"><span data-stu-id="008d3-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="008d3-620">この規則を使用すると、階層的なインデントが維持されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="008d3-621">ベンダー固有のスキーマ (-moz-,-webkit)</span><span class="sxs-lookup"><span data-stu-id="008d3-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="008d3-622">CSS3 には、異なるタイミングで異なるブラウザーによって実装された多数のプロパティが導入されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="008d3-623">これまで、開発者は、ベンダー固有の構文を使用して特定のブラウザーをコーディングしていました。</span><span class="sxs-lookup"><span data-stu-id="008d3-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="008d3-624">これらのブラウザー固有のプロパティは、IntelliSense に含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="008d3-625">コメントとコメント解除のサポート</span><span class="sxs-lookup"><span data-stu-id="008d3-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="008d3-626">コードエディターで使用するのと同じショートカットを使用して、CSS ルールのコメント化とコメント解除を行うことができるようになりました (Ctrl + K、C からコメント、Ctrl + K、コメントを解除します)。</span><span class="sxs-lookup"><span data-stu-id="008d3-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="008d3-627">Color picker</span><span class="sxs-lookup"><span data-stu-id="008d3-627">Color picker</span></span>

<span data-ttu-id="008d3-628">以前のバージョンの Visual Studio では、色に関連する属性の IntelliSense は、名前付きの色の値のドロップダウンリストで設定されていました。</span><span class="sxs-lookup"><span data-stu-id="008d3-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="008d3-629">この一覧は、フル機能のカラーピッカーに置き換えられました。</span><span class="sxs-lookup"><span data-stu-id="008d3-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="008d3-630">色の値を入力すると、カラーピッカーが自動的に表示され、以前に使用した色の一覧が表示され、その後に既定のカラーパレットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="008d3-631">マウスまたはキーボードを使用して色を選択できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="008d3-632">一覧は、完全なカラーピッカーに展開できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="008d3-633">ピッカーを使用すると、不透明度スライダーを移動したときに任意の色を RGBA に自動的に変換することで、アルファチャネルを制御できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="008d3-634">スニペット</span><span class="sxs-lookup"><span data-stu-id="008d3-634">Snippets</span></span>

<span data-ttu-id="008d3-635">CSS エディターのスニペットを使用すると、クロスブラウザースタイルを簡単かつ迅速に作成できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="008d3-636">ブラウザー固有の設定を必要とする多くの CSS3 プロパティがスニペットにロールアウトされました。</span><span class="sxs-lookup"><span data-stu-id="008d3-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="008d3-637">CSS スニペットでは、IntelliSense の一覧を示すアットマーク (@) を入力することによって、(CSS3 メディアクエリなどの) 高度なシナリオをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="008d3-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="008d3-638">@media 値を選択して Tab キーを押すと、CSS エディターによって次のスニペットが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="008d3-639">コードのスニペットと同様に、独自の CSS スニペットを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="008d3-640">カスタム領域</span><span class="sxs-lookup"><span data-stu-id="008d3-640">Custom regions</span></span>

<span data-ttu-id="008d3-641">コードエディターで既に使用可能な名前付きコード領域を CSS 編集に使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="008d3-642">これにより、関連するスタイルブロックを簡単にグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="008d3-643">領域が折りたたまれると、リージョンの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="008d3-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="008d3-644">Page Inspector</span></span>

<span data-ttu-id="008d3-645">Page Inspector は、Visual Studio IDE で web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) をレンダリングするツールであり、ソースコードと結果の出力の両方を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="008d3-646">ASP.NET ページでは、Page Inspector を使用して、ブラウザーに表示される HTML マークアップを生成したサーバー側コードを確認できます。</span><span class="sxs-lookup"><span data-stu-id="008d3-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="008d3-647">Page Inspector の詳細については、次のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="008d3-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="008d3-648">[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)での Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="008d3-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="008d3-649">[ASP.NET Web フォーム](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)での Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="008d3-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="008d3-650">発行</span><span class="sxs-lookup"><span data-stu-id="008d3-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="008d3-651">発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="008d3-651">Publish profiles</span></span>

<span data-ttu-id="008d3-652">Visual Studio 2010 では、Web アプリケーションプロジェクトの公開情報はバージョン管理に保存されず、他のユーザーと共有するように設計されていません。</span><span class="sxs-lookup"><span data-stu-id="008d3-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="008d3-653">Visual Studio 2012 リリース候補では、発行プロファイルの形式が変更されています。</span><span class="sxs-lookup"><span data-stu-id="008d3-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="008d3-654">これにより、チームの成果物が作成され、MSBuild に基づくビルドから簡単に利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="008d3-655">ビルド構成情報は [発行] ダイアログボックスに表示されるので、発行前にビルド構成を簡単に切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="008d3-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="008d3-656">発行プロファイルは、PublishProfiles フォルダーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="008d3-657">フォルダーの場所は、使用しているプログラミング言語によって異なります。</span><span class="sxs-lookup"><span data-stu-id="008d3-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="008d3-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="008d3-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="008d3-659">Visual Basic: マイプロジェクト \ 発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="008d3-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="008d3-660">各プロファイルは MSBuild ファイルです。</span><span class="sxs-lookup"><span data-stu-id="008d3-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="008d3-661">発行時に、このファイルはプロジェクトの MSBuild ファイルにインポートされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="008d3-662">Visual Studio 2010 では、発行またはパッケージプロセスを変更する場合、カスタマイズを**ProjectName**. wpp. .targets という名前のファイルに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="008d3-663">これはまだサポートされていますが、カスタマイズを発行プロファイル自体に配置できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="008d3-664">このようにして、カスタマイズはそのプロファイルに対してのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="008d3-665">MSBuild から発行プロファイルを利用することもできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="008d3-666">これを行うには、プロジェクトをビルドするときに次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="008d3-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="008d3-667">プロジェクトの .csproj 値はプロジェクトのパスであり、ProfileName は発行するプロファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="008d3-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="008d3-668">または、 *publishprofile*プロパティのプロファイル名を渡す代わりに、発行プロファイルへの完全パスを渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="008d3-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="008d3-669">ASP.NET のプリコンパイルとマージ</span><span class="sxs-lookup"><span data-stu-id="008d3-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="008d3-670">Web アプリケーションプロジェクトの場合、Visual Studio 2012 リリース候補では、プロジェクトの発行時またはパッケージ化時にサイトのコンテンツをプリコンパイルおよびマージできる [Web のパッケージ化/発行] ページにオプションが追加されます。</span><span class="sxs-lookup"><span data-stu-id="008d3-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="008d3-671">これらのオプションを表示するには、ソリューションエクスプローラーでプロジェクトを右クリックし、[プロパティ] をクリックします。次に、[Web のパッケージ化/発行] プロパティページをクリックします。</span><span class="sxs-lookup"><span data-stu-id="008d3-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="008d3-672">次の図は、[公開前にこのアプリケーションをプリコンパイルする] オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="008d3-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="008d3-673">このオプションを選択すると、web アプリケーションを発行またはパッケージ化するたびに、Visual Studio によってアプリケーションがプリコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="008d3-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="008d3-674">サイトのプリコンパイル方法またはアセンブリのマージ方法を制御する場合は、[詳細設定] ボタンをクリックして、これらのオプションを構成します。</span><span class="sxs-lookup"><span data-stu-id="008d3-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="008d3-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="008d3-675">IIS Express</span></span>

<span data-ttu-id="008d3-676">Visual Studio で web プロジェクトをテストするための既定の web サーバーが IIS Express されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="008d3-677">Visual Studio 開発サーバーは、開発時にローカル web サーバーに対してもオプションですが、IIS Express が推奨されるサーバーになりました。</span><span class="sxs-lookup"><span data-stu-id="008d3-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="008d3-678">Visual Studio 11 Beta での IIS Express の使用経験は、Visual Studio 2010 SP1 での使用方法と非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="008d3-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="008d3-679">免責事項</span><span class="sxs-lookup"><span data-stu-id="008d3-679">Disclaimer</span></span>

<span data-ttu-id="008d3-680">このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="008d3-681">このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。</span><span class="sxs-lookup"><span data-stu-id="008d3-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="008d3-682">Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。</span><span class="sxs-lookup"><span data-stu-id="008d3-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="008d3-683">このホワイト ペーパーは、情報提供のみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="008d3-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="008d3-684">マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。</span><span class="sxs-lookup"><span data-stu-id="008d3-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="008d3-685">お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。</span><span class="sxs-lookup"><span data-stu-id="008d3-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="008d3-686">このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。</span><span class="sxs-lookup"><span data-stu-id="008d3-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="008d3-687">Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="008d3-688">別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。</span><span class="sxs-lookup"><span data-stu-id="008d3-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="008d3-689">特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人名、場所、およびイベントは架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールとは一切関係ありません。アドレス、ロゴ、人物、場所、またはイベントが想定されているか、または推測する必要があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="008d3-690">(C) 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="008d3-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="008d3-691">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="008d3-691">All rights reserved.</span></span>

<span data-ttu-id="008d3-692">Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。</span><span class="sxs-lookup"><span data-stu-id="008d3-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="008d3-693">本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。</span><span class="sxs-lookup"><span data-stu-id="008d3-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
