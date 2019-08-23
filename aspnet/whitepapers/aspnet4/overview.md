---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 および Visual Studio 2010 Web 開発の概要 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、the.NET Framework 4 および Visual Studio 2010 に含まれる ASP.NET の新機能の多くの概要について説明します。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 8c93952adb33d1ce7008ebff9d032a71eb2a5f74
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995401"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="918d6-103">ASP.NET 4 と Visual Studio 2010 Web 開発の概要</span><span class="sxs-lookup"><span data-stu-id="918d6-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>

> <span data-ttu-id="918d6-104">このドキュメントでは、the.NET Framework 4 および Visual Studio 2010 に含まれる ASP.NET の新機能の多くの概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="918d6-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="918d6-105">このホワイトペーパーをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="918d6-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

<span data-ttu-id="918d6-106">**目次**</span><span class="sxs-lookup"><span data-stu-id="918d6-106">**Contents**</span></span>

<span data-ttu-id="918d6-107">**[コアサービス](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="918d6-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
<span data-ttu-id="918d6-108">Web.config[ファイルのリファクタリング](#0.2__Toc253429239 "_Toc253429239")</span><span class="sxs-lookup"><span data-stu-id="918d6-108">[Web.config File Refactoring](#0.2__Toc253429239 "_Toc253429239")</span></span>  
[<span data-ttu-id="918d6-109">拡張可能な出力キャッシュ</span><span class="sxs-lookup"><span data-stu-id="918d6-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="918d6-110">Web アプリケーションの自動起動</span><span class="sxs-lookup"><span data-stu-id="918d6-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="918d6-111">ページを永続的にリダイレクトする</span><span class="sxs-lookup"><span data-stu-id="918d6-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="918d6-112">セッション状態の圧縮</span><span class="sxs-lookup"><span data-stu-id="918d6-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="918d6-113">許容される url の範囲を拡張する</span><span class="sxs-lookup"><span data-stu-id="918d6-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="918d6-114">拡張可能な要求の検証</span><span class="sxs-lookup"><span data-stu-id="918d6-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="918d6-115">オブジェクトキャッシュとオブジェクトキャッシュの拡張性</span><span class="sxs-lookup"><span data-stu-id="918d6-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="918d6-116">Extensible HTML、URL、および HTTP ヘッダーエンコード</span><span class="sxs-lookup"><span data-stu-id="918d6-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="918d6-117">1 つのワーカープロセスにおける個々のアプリケーションのパフォーマンス監視</span><span class="sxs-lookup"><span data-stu-id="918d6-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="918d6-118">Multi-Targeting</span><span class="sxs-lookup"><span data-stu-id="918d6-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="918d6-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="918d6-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="918d6-120">Web フォームと MVC に含まれる jQuery</span><span class="sxs-lookup"><span data-stu-id="918d6-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="918d6-121">Content Delivery Network サポート</span><span class="sxs-lookup"><span data-stu-id="918d6-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="918d6-122">ScriptManager の明示的なスクリプト</span><span class="sxs-lookup"><span data-stu-id="918d6-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="918d6-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="918d6-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="918d6-124">メタタグを MetaDescription プロパティとページに設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="918d6-125">個々のコントロールのビューステートを有効にする</span><span class="sxs-lookup"><span data-stu-id="918d6-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="918d6-126">ブラウザー機能の変更点</span><span class="sxs-lookup"><span data-stu-id="918d6-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="918d6-127">ASP.NET 4 でのルーティング</span><span class="sxs-lookup"><span data-stu-id="918d6-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="918d6-128">クライアント id の設定</span><span class="sxs-lookup"><span data-stu-id="918d6-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="918d6-129">データコントロールでの行選択の保持</span><span class="sxs-lookup"><span data-stu-id="918d6-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="918d6-130">ASP.NET Chart コントロール</span><span class="sxs-lookup"><span data-stu-id="918d6-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="918d6-131">QueryExtender コントロールを使用したデータのフィルター処理</span><span class="sxs-lookup"><span data-stu-id="918d6-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
<span data-ttu-id="918d6-132">[Html エンコード]されたコード式(#0.2__Toc253429265 "_Toc253429265")</span><span class="sxs-lookup"><span data-stu-id="918d6-132">[Html Encoded Code Expressions](#0.2__Toc253429265 "_Toc253429265")</span></span>  
[<span data-ttu-id="918d6-133">プロジェクトテンプレートの変更</span><span class="sxs-lookup"><span data-stu-id="918d6-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="918d6-134">CSS の機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="918d6-135">非表示フィールドの周囲の Div 要素の非表示</span><span class="sxs-lookup"><span data-stu-id="918d6-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="918d6-136">テンプレートコントロール用の外部テーブルのレンダリング</span><span class="sxs-lookup"><span data-stu-id="918d6-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="918d6-137">ListView コントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="918d6-138">CheckBoxList と RadioButtonList のコントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="918d6-139">メニューコントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="918d6-140">Wizard および CreateUserWizard コントロール 56</span><span class="sxs-lookup"><span data-stu-id="918d6-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="918d6-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="918d6-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="918d6-142">区分のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="918d6-143">データ注釈属性の検証のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="918d6-144">テンプレートヘルパー</span><span class="sxs-lookup"><span data-stu-id="918d6-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="918d6-145">**[動的データ](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="918d6-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="918d6-146">既存のプロジェクトの動的データを有効にする</span><span class="sxs-lookup"><span data-stu-id="918d6-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="918d6-147">宣言型の DynamicDataManager コントロール構文</span><span class="sxs-lookup"><span data-stu-id="918d6-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="918d6-148">エンティティテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="918d6-149">Url と電子メールアドレスの新しいフィールドテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="918d6-150">DynamicHyperLink コントロールを使用したリンクの作成</span><span class="sxs-lookup"><span data-stu-id="918d6-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="918d6-151">データモデルでの継承のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="918d6-152">多対多リレーションシップのサポート (Entity Framework のみ)</span><span class="sxs-lookup"><span data-stu-id="918d6-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="918d6-153">表示およびサポートの列挙型を制御する新しい属性</span><span class="sxs-lookup"><span data-stu-id="918d6-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
<span data-ttu-id="918d6-154">[フィルターの強化]されたサポート(#0.2__Toc253429287 "_Toc253429287")</span><span class="sxs-lookup"><span data-stu-id="918d6-154">[Enhanced Support for Filters](#0.2__Toc253429287 "_Toc253429287")</span></span>

<span data-ttu-id="918d6-155">**[Visual Studio 2010 の Web 開発の機能強化](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="918d6-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="918d6-156">CSS 互換性の向上</span><span class="sxs-lookup"><span data-stu-id="918d6-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="918d6-157">HTML および JavaScript のスニペット</span><span class="sxs-lookup"><span data-stu-id="918d6-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="918d6-158">JavaScript IntelliSense の機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="918d6-159">**[Visual Studio 2010 を使用した Web アプリケーションのデプロイ](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="918d6-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="918d6-160">Web パッケージ</span><span class="sxs-lookup"><span data-stu-id="918d6-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
<span data-ttu-id="918d6-161">Web.config[変換](#0.2__Toc253429294 "_Toc253429294")</span><span class="sxs-lookup"><span data-stu-id="918d6-161">[Web.config Transformation](#0.2__Toc253429294 "_Toc253429294")</span></span>  
[<span data-ttu-id="918d6-162">データベースの配置</span><span class="sxs-lookup"><span data-stu-id="918d6-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="918d6-163">ワンクリックによる Web アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="918d6-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="918d6-164">Resources</span><span class="sxs-lookup"><span data-stu-id="918d6-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="918d6-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="918d6-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="918d6-166">コアサービス</span><span class="sxs-lookup"><span data-stu-id="918d6-166">Core Services</span></span>

<span data-ttu-id="918d6-167">ASP.NET 4 では、出力キャッシュやセッション状態ストレージなどのコア ASP.NET サービスを向上させる多くの機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="918d6-168">Web.config ファイルのリファクタリング</span><span class="sxs-lookup"><span data-stu-id="918d6-168">Web.config File Refactoring</span></span>

<span data-ttu-id="918d6-169">Web アプリケーションの構成を含むファイルは、Ajax、ルーティング、IIS7との統合などの新機能が追加されたため、.NETFrameworkのいくつかのリリースで大幅に増加しています。`Web.config`</span><span class="sxs-lookup"><span data-stu-id="918d6-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="918d6-170">これにより、Visual Studio のようなツールを使用せずに、新しい Web アプリケーションを構成したり、起動したりすることが難しくなりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="918d6-171">.Net Framework 4 では、主要な構成要素が`machine.config`ファイルに移動され、アプリケーションはこれらの設定を継承するようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="918d6-172">これにより`Web.config` 、ASP.NET 4 アプリケーション内のファイルを空にするか、次の行だけを含めることができます。これは、アプリケーションが対象とするフレームワークのバージョンを Visual Studio に対して指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="918d6-173">拡張可能な出力キャッシュ</span><span class="sxs-lookup"><span data-stu-id="918d6-173">Extensible Output Caching</span></span>

<span data-ttu-id="918d6-174">ASP.NET 1.0 がリリースされてから、出力キャッシュによって、生成されたページ、コントロール、および HTTP 応答の出力をメモリに格納できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="918d6-175">後続の Web 要求では、ASP.NET は、出力をゼロから再生成するのではなく、メモリから生成された出力を取得することで、コンテンツをより迅速に提供できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="918d6-176">ただし、この方法には制限があります。生成されたコンテンツは常にメモリに格納される必要があり、大量のトラフィックが発生しているサーバーでは、出力キャッシュによって消費されるメモリが Web アプリケーションの他の部分からのメモリ要求と競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="918d6-177">ASP.NET 4 では、出力キャッシュに拡張ポイントを追加して、1つまたは複数のカスタム出力キャッシュプロバイダーを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="918d6-178">出力キャッシュプロバイダーは、任意のストレージ機構を使用して HTML コンテンツを永続化できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="918d6-179">これにより、ローカルまたはリモートのディスク、クラウドストレージ、および分散キャッシュエンジンを含むさまざまな永続化メカニズムに対して、カスタムの出力キャッシュプロバイダーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="918d6-180">カスタム出力キャッシュプロバイダーは、新しい system.servicemodel*プロバイダー*型から派生したクラスとして作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="918d6-181">次の例に示すように、 `Web.config` *outputCache*要素の新しい*providers*サブセクションを使用して、ファイルでプロバイダーを構成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="918d6-182">ASP.NET 4 の既定では、すべての HTTP 応答、表示ページ、およびコントロールは、前の例で示したように、メモリ内の出力キャッシュを使用します。前の例では、 *defaultprovider を*属性が AspNetInternalProvider に設定されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="918d6-183">*Defaultprovider を*に別のプロバイダー名を指定することで、Web アプリケーションに使用される既定の出力キャッシュプロバイダーを変更できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="918d6-184">さらに、1つのコントロールと要求ごとに異なる出力キャッシュプロバイダーを選択できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="918d6-185">さまざまな Web ユーザーコントロールに対して別の出力キャッシュプロバイダーを選択する最も簡単な方法は、次の例に示すように、コントロールディレクティブで新しい*providerName*属性を使用して宣言的に実行することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="918d6-186">HTTP 要求に別の出力キャッシュプロバイダーを指定する場合は、もう少し作業が必要です。</span><span class="sxs-lookup"><span data-stu-id="918d6-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="918d6-187">プロバイダーを宣言によって指定する代わりに、 `Global.asax`ファイルの新しい*getouputcacheprovidername*メソッドをオーバーライドして、特定の要求に対して使用するプロバイダーをプログラムで指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="918d6-188">その方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="918d6-189">ASP.NET 4 に対する出力キャッシュプロバイダーの拡張機能が追加されたため、Web サイトに対してより積極的でインテリジェントな出力キャッシュ戦略を推進できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="918d6-190">たとえば、サイトの "上位 10" ページをメモリにキャッシュし、ディスク上のトラフィックを減らすページをキャッシュできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="918d6-191">または、表示されたページのさまざまな組み合わせをキャッシュできますが、分散キャッシュを使用して、フロントエンド Web サーバーからメモリ消費がオフロードされるようにします。</span><span class="sxs-lookup"><span data-stu-id="918d6-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="918d6-192">Web アプリケーションの自動起動</span><span class="sxs-lookup"><span data-stu-id="918d6-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="918d6-193">一部の Web アプリケーションでは、最初の要求を提供する前に、大量のデータを読み込んだり、高負荷の初期化処理を実行したりする必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="918d6-194">以前のバージョンの ASP.NET では、このような状況では、ASP.NET アプリケーションを "ウェイクアップ" するカスタムアプローチを考案し、 `Global.asax`ファイルの*アプリケーション\_読み込み*メソッド中に初期化コードを実行する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="918d6-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="918d6-195">Windows Server 2008 R2 の IIS 7.5 で ASP.NET 4 が実行されている場合、このシナリオに直接対処する*自動開始*という新しいスケーラビリティ機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="918d6-196">自動開始機能は、アプリケーションプールを起動し、ASP.NET アプリケーションを初期化して、HTTP 要求を受け入れるための制御されたアプローチを提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="918d6-197">Iis 7.5 用の IIS アプリケーションのウォームアップモジュール</span><span class="sxs-lookup"><span data-stu-id="918d6-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="918d6-198">IIS チームは、IIS 7.5 用のアプリケーションのウォームアップモジュールの最初のベータテストバージョンをリリースしました。</span><span class="sxs-lookup"><span data-stu-id="918d6-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="918d6-199">これにより、前に説明したよりも簡単にアプリケーションを準備できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="918d6-200">カスタムコードを記述する代わりに、Web アプリケーションがネットワークからの要求を受け入れる前に実行するリソースの Url を指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="918d6-201">このウォームアップは、iis サービスの開始時に発生します (IIS アプリケーションプールを*Always running*として構成した場合)。また、iis ワーカープロセスがリサイクルされるときにも発生します。</span><span class="sxs-lookup"><span data-stu-id="918d6-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="918d6-202">リサイクル中、古い IIS ワーカープロセスは、新たに起動されたワーカープロセスが完全に動作するようになってから、アプリケーションで中断やその他の問題が発生しないようにします。</span><span class="sxs-lookup"><span data-stu-id="918d6-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="918d6-203">このモジュールは、バージョン2.0 以降の任意のバージョンの ASP.NET で動作することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="918d6-204">詳細については、IIS.net Web サイトの「[アプリケーションのウォームアップ](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="918d6-205">ウォームアップ機能の使用方法を示すチュートリアルについては、IIS.net Web サイトの「 [IIS 7.5 アプリケーションのウォームアップモジュールでのはじめに](https://www.iis.net/learn/manage)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>

<span data-ttu-id="918d6-206">自動開始機能を使用するには、iis 管理者が、 `applicationHost.config`ファイルの次の構成を使用して、自動的に開始されるように iis 7.5 のアプリケーションプールを設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="918d6-207">1つのアプリケーションプールに複数のアプリケーションを含めることができるため、 `applicationHost.config`ファイルの次の構成を使用して個々のアプリケーションを自動的に開始するように指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="918d6-208">Iis 7.5 サーバーがコールドスタートされるか、個々のアプリケーションプールがリサイクルされるときに、iis 7.5 は`applicationHost.config`ファイル内の情報を使用して、どの Web アプリケーションを自動的に開始する必要があるかを判断します。</span><span class="sxs-lookup"><span data-stu-id="918d6-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="918d6-209">自動開始用にマークされているアプリケーションごとに、IIS 7.5 は ASP.NET 4 に要求を送信して、アプリケーションが一時的に HTTP 要求を受け付けない状態でアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="918d6-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="918d6-210">この状態になると、ASP.NET は*Serviceautostartprovider*属性で定義されている型 (前の例で示したように) をインスタンス化し、そのパブリックエントリポイントを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="918d6-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="918d6-211">次の例に示すように、 *IProcessHostPreloadClient*インターフェイスを実装することによって、必要なエントリポイントでマネージ自動開始型を作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="918d6-212">*プリロード*メソッドで初期化コードを実行し、メソッドから制御が戻った後、ASP.NET アプリケーションは要求を処理する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="918d6-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="918d6-213">IIS .5 と ASP.NET 4 に自動開始する機能が追加されたため、最初の HTTP 要求を処理する前に、コストの高いアプリケーションの初期化を実行するための明確なアプローチができました。</span><span class="sxs-lookup"><span data-stu-id="918d6-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="918d6-214">たとえば、新しい自動開始機能を使用してアプリケーションを初期化し、アプリケーションが初期化され、HTTP トラフィックを受け入れる準備ができたことをロードバランサーに通知することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="918d6-215">ページを永続的にリダイレクトする</span><span class="sxs-lookup"><span data-stu-id="918d6-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="918d6-216">Web アプリケーションでは、時間の経過と共にページやその他のコンテンツを移動するのが一般的です。これにより、検索エンジンに古いリンクが蓄積される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="918d6-217">ASP.NET では、開発者は、要求を新しい URL に転送するために、を使用して以前の Url への要求を処理しました *。*</span><span class="sxs-lookup"><span data-stu-id="918d6-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="918d6-218">ただし、*リダイレクト*メソッドは Http 302 Found (一時的なリダイレクト) 応答を発行します。これにより、ユーザーが古い url にアクセスしようとしたときに http ラウンドトリップが追加されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="918d6-219">ASP.NET 4 は、次の例に示すように、永続的に移動された HTTP 301 を簡単に発行できるようにする新しい*Redirectpermanent*ヘルパーメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="918d6-220">永続的なリダイレクトを認識する検索エンジンとその他のユーザーエージェントは、コンテンツに関連付けられている新しい URL を格納します。これにより、一時的なリダイレクトのためにブラウザーによって行われる不要なラウンドトリップが不要になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="918d6-221">セッション状態の圧縮</span><span class="sxs-lookup"><span data-stu-id="918d6-221">Shrinking Session State</span></span>

<span data-ttu-id="918d6-222">ASP.NET には、Web ファーム全体にセッション状態を格納するための既定のオプションが2つ用意されています。アウトプロセスセッション状態サーバーを呼び出すセッション状態プロバイダーと、データを Microsoft SQL Server データベースに格納するセッション状態プロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="918d6-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="918d6-223">どちらのオプションでも、Web アプリケーションのワーカープロセスの外部に状態情報が格納されるため、リモートストレージに送信する前にセッション状態をシリアル化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="918d6-224">開発者がセッション状態で保存する情報の量によっては、シリアル化されたデータのサイズが非常に大きくなることがあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="918d6-225">ASP.NET 4 では、両方の種類のアウトプロセスセッション状態プロバイダーに新しい圧縮オプションが導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="918d6-226">次の例に示されている*compressionEnabled*構成オプションが*true*に設定されている場合、ASP.NET は、.NET Framework *GZipStream*クラスを使用して、シリアル化されたセッション状態を圧縮 (および圧縮解除) します.</span><span class="sxs-lookup"><span data-stu-id="918d6-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="918d6-227">`Web.config`ファイルに新しい属性を追加するだけで、Web サーバー上に予備の CPU サイクルがあるアプリケーションでは、シリアル化されたセッション状態データのサイズを大幅に削減することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="918d6-228">許容される Url の範囲を拡張する</span><span class="sxs-lookup"><span data-stu-id="918d6-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="918d6-229">ASP.NET 4 では、アプリケーションの Url のサイズを拡張するための新しいオプションが導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="918d6-230">以前のバージョンのでは、NTFS ファイルパスの制限に基づいて、制約された URL パスの長さを260文字に ASP.NET していました。</span><span class="sxs-lookup"><span data-stu-id="918d6-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="918d6-231">ASP.NET 4 では、2つの新しい*httpRuntime*構成属性を使用して、アプリケーションに合わせてこの制限を増やす (または減らす) ことができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="918d6-232">次の例では、これらの新しい属性を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="918d6-233">長いまたは短いパス (プロトコル、サーバー名、クエリ文字列を含まない URL の部分) を許可するには、 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性を変更します。</span><span class="sxs-lookup"><span data-stu-id="918d6-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="918d6-234">より長いまたは短いクエリ文字列を許可するには、 *[Maxquerystringlength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性の値を変更します。</span><span class="sxs-lookup"><span data-stu-id="918d6-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="918d6-235">ASP.NET 4 では、URL 文字チェックで使用される文字を構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="918d6-236">ASP.NET が URL のパス部分で無効な文字を検出すると、要求が拒否され、HTTP 400 エラーが発行されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="918d6-237">以前のバージョンの ASP.NET では、URL 文字のチェックは固定された文字セットに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="918d6-238">ASP.NET 4 では、次の例に示すように、 *httpRuntime* configuration 要素の新しい*Requestpathinvalidcharacters*属性を使用して、有効な文字のセットをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidCharacters* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="918d6-239">既定では、 *Requestpathinvalidcharacters*属性は8文字を無効として定義します。</span><span class="sxs-lookup"><span data-stu-id="918d6-239">By default, the *requestPathInvalidCharacters* attribute defines eight characters as invalid.</span></span> <span data-ttu-id="918d6-240">( *Requestpathinvalidcharacters*に既定で割り当てられている文字列で&lt;は、 `Web.config`ファイルは XML ファイルであるため&gt;、より小さい ()&amp;、より大きい ()、アンパサンド () の各文字がエンコードされます)。必要に応じて、無効な文字のセットをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-240">(In the string that is assigned to *requestPathInvalidCharacters* by default, the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="918d6-241">注 ASP.NET 4 は、IETF から0x1F への ASCII 範囲の文字を含む URL パスを常に拒否します。これは、IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) の RFC 2396 で定義されている url 文字が無効であるためです。</span><span class="sxs-lookup"><span data-stu-id="918d6-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="918d6-242">IIS 6 以降を実行する Windows Server のバージョンでは、http.sys プロトコルデバイスドライバーは、これらの文字で Url を自動的に拒否します。</span><span class="sxs-lookup"><span data-stu-id="918d6-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="918d6-243">拡張可能な要求の検証</span><span class="sxs-lookup"><span data-stu-id="918d6-243">Extensible Request Validation</span></span>

<span data-ttu-id="918d6-244">ASP.NET 要求の検証では、クロスサイトスクリプティング (XSS) 攻撃で一般的に使用される文字列について、受信 HTTP 要求データを検索します。</span><span class="sxs-lookup"><span data-stu-id="918d6-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="918d6-245">潜在的な XSS 文字列が検出された場合、要求の検証は疑わしい文字列にフラグを指定し、エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="918d6-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="918d6-246">組み込みの要求検証では、XSS 攻撃で使用される最も一般的な文字列を検出した場合にのみ、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="918d6-247">以前に XSS 検証をより積極的に実行しようとすると、誤検知が多くなりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="918d6-248">ただし、顧客は、より積極的な要求の検証や、特定のページまたは特定の種類の要求に対して XSS チェックを意図的に緩和する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="918d6-249">ASP.NET 4 では、要求検証機能が拡張され、カスタムの要求検証ロジックを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="918d6-250">要求の検証を拡張するには、新しい httpRuntime 型から派生するクラスを作成し、そのカスタム型を使用するように ( `Web.config`ファイルのセクションで) アプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="918d6-251">次の例は、カスタムの要求検証クラスを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="918d6-252">新しい*Requestvalidationtype*属性には、カスタム要求の検証を提供するクラスを指定する標準 .NET Framework 型識別子文字列が必要です。</span><span class="sxs-lookup"><span data-stu-id="918d6-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="918d6-253">各要求に対して、ASP.NET はカスタム型を呼び出して、受信 HTTP 要求データの各部分を処理します。</span><span class="sxs-lookup"><span data-stu-id="918d6-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="918d6-254">受信 URL、すべての HTTP ヘッダー (cookie とカスタムヘッダーの両方)、およびエンティティ本体は、次の例に示すようなカスタム要求検証クラスによってすべて検査できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="918d6-255">受信 HTTP データの一部を検査しない場合は、要求検証クラスをフォールバックして、ASP.NET の既定の要求の検証を実行するだけで base を呼び出すことができます *。IsValidRequestString。*</span><span class="sxs-lookup"><span data-stu-id="918d6-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="918d6-256">オブジェクトキャッシュとオブジェクトキャッシュの拡張性</span><span class="sxs-lookup"><span data-stu-id="918d6-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="918d6-257">最初のリリース以降、ASP.NET には強力なメモリ内オブジェクトキャッシュ () が含まれていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="918d6-258">キャッシュの実装は、非 Web アプリケーションで使用されていることがよくありました。</span><span class="sxs-lookup"><span data-stu-id="918d6-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="918d6-259">ただし、ASP.NET オブジェクトキャッシュを使用できるようにするために、Windows フォームまた`System.Web.dll`は WPF アプリケーションがへの参照を含めるのは厄介です。</span><span class="sxs-lookup"><span data-stu-id="918d6-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="918d6-260">すべてのアプリケーションでキャッシュを使用できるようにするために、.NET Framework 4 では新しいアセンブリ、新しい名前空間、いくつかの基本型、および具体的なキャッシュ実装が導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="918d6-261">新しい`System.Runtime.Caching.dll`アセンブリには、新しいキャッシュ API が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="918d6-262">名前空間には、クラスの2つのコアセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="918d6-263">任意の種類のカスタムキャッシュ実装を構築するための基盤を提供する抽象型。</span><span class="sxs-lookup"><span data-stu-id="918d6-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="918d6-264">具体的なメモリ内オブジェクトキャッシュの実装 (system.string*キャッシュ*クラス) を実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="918d6-265">新しい*Memorycache*クラスは ASP.NET キャッシュに密接に基づいてモデル化されており、内部キャッシュエンジンのロジックの多くを ASP.NET と共有しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="918d6-266">カスタムキャッシュの開発をサポートするために、ASP.NET のパブリックキャッシュ api が更新されましたが、この*キャッシュ*オブジェクトを使用している場合は、新しい api での使い慣れた概念がわかります。</span><span class="sxs-lookup"><span data-stu-id="918d6-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="918d6-267">新しい*Memorycache*クラスとサポートする基本 api の詳細については、ドキュメント全体が必要になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="918d6-268">ただし、次の例は、新しいキャッシュ API のしくみを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="918d6-269">この例は、に`System.Web.dll`依存することなく Windows フォームアプリケーション用に記述されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="918d6-270">Extensible HTML、URL、および HTTP ヘッダーエンコード</span><span class="sxs-lookup"><span data-stu-id="918d6-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="918d6-271">ASP.NET 4 では、次の一般的なテキストエンコードタスク用のカスタムエンコードルーチンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="918d6-272">HTML エンコード。</span><span class="sxs-lookup"><span data-stu-id="918d6-272">HTML encoding.</span></span>
- <span data-ttu-id="918d6-273">URL エンコード。</span><span class="sxs-lookup"><span data-stu-id="918d6-273">URL encoding.</span></span>
- <span data-ttu-id="918d6-274">HTML 属性のエンコード。</span><span class="sxs-lookup"><span data-stu-id="918d6-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="918d6-275">送信 HTTP ヘッダーをエンコードしています。</span><span class="sxs-lookup"><span data-stu-id="918d6-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="918d6-276">カスタムエンコーダーを作成するには、次の例に示すように、新しい ASP.NET 型から派生して、 `Web.config`ファイルの*httpRuntime*セクションでカスタム型を使用するように構成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="918d6-277">カスタムエンコーダーが構成されると、ASP.NET クラスまたは*HttpUtility*クラスのパブリックエンコードメソッドが呼び出されるたびに、カスタムエンコード実装が自動的に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="918d6-278">これにより、Web 開発チームの1つの部分で、アグレッシブな文字エンコーディングを実装するカスタムエンコーダーを作成できます。一方、Web 開発チームの残りの部分では、引き続きパブリック ASP.NET encoding Api を使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="918d6-279">*HttpRuntime*要素でカスタムエンコーダーを一元的に構成することで、パブリック ASP.NET encoding api からのすべてのテキストエンコード呼び出しがカスタムエンコーダー経由でルーティングされることが保証されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="918d6-280">1つのワーカープロセスにおける個々のアプリケーションのパフォーマンス監視</span><span class="sxs-lookup"><span data-stu-id="918d6-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="918d6-281">1台のサーバーでホストできる Web サイトの数を増やすために、多くのホスト側は、1つのワーカープロセスで複数の ASP.NET アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="918d6-282">ただし、複数のアプリケーションが1つの共有ワーカープロセスを使用している場合、サーバー管理者は、問題が発生している個々のアプリケーションを特定するのが困難です。</span><span class="sxs-lookup"><span data-stu-id="918d6-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="918d6-283">ASP.NET 4 は、CLR によって導入された新しいリソース監視機能を活用しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="918d6-284">この機能を有効にするには、 `aspnet.config`構成ファイルに次の XML 構成スニペットを追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="918d6-285">`aspnet.config`ファイルが .NET Framework がインストールされているディレクトリにあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="918d6-286">ファイルで`Web.config`はありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-286">It is not the `Web.config` file.</span></span>

<span data-ttu-id="918d6-287">*AppDomainResourceMonitoring*機能が有効になっている場合、"ASP.NET Applications" パフォーマンスカテゴリには、[ *% マネージプロセッサ時間*] と [*使用されたマネージメモリ*] の2つの新しいパフォーマンスカウンターが用意されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="918d6-288">これらのパフォーマンスカウンターはどちらも、新しい CLR アプリケーションドメインリソース管理機能を使用して、個々の ASP.NET アプリケーションの推定 CPU 時間とマネージメモリ使用率を追跡します。</span><span class="sxs-lookup"><span data-stu-id="918d6-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="918d6-289">その結果、ASP.NET 4 では、管理者は1つのワーカープロセスで実行されている個々のアプリケーションのリソース消費量をより詳細に表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="918d6-290">マルチ ターゲット</span><span class="sxs-lookup"><span data-stu-id="918d6-290">Multi-Targeting</span></span>

<span data-ttu-id="918d6-291">.NET Framework の特定のバージョンを対象とするアプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="918d6-292">ASP.NET 4 では、 `Web.config`ファイルの*コンパイル*要素の新しい属性を使用して、.NET Framework 4 以降を対象にすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="918d6-293">.NET Framework 4 を明示的に対象として*い*て、オプションの要素`Web.config`をファイルに含める場合 (たとえば、system.string のエントリ)、これらの要素は .NET Framework 4 に対して適切である必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="918d6-294">(.NET Framework 4 を明示的に対象にしていない場合、ターゲットフレームワークは`Web.config`ファイル内のエントリがないことから推測されます)。</span><span class="sxs-lookup"><span data-stu-id="918d6-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="918d6-295">次の例は、 `Web.config`ファイルの*コンパイル*要素での*targetframework*属性の使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="918d6-296">.NET Framework の特定のバージョンを対象とする場合は、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="918d6-297">.NET Framework 4 アプリケーションプールでは、ファイルに`Web.config` *targetframework* `Web.config`属性が含まれていない場合、またはファイルが見つからない場合、ASP.NET ビルドシステムはターゲットとして .NET Framework 4 を想定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="918d6-298">(.NET Framework 4 で実行されるように、アプリケーションのコーディングを変更することが必要になる場合があります)。</span><span class="sxs-lookup"><span data-stu-id="918d6-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="918d6-299">*Targetframework*属性を含め、*システムの codeDom*要素が`Web.config`ファイルで定義されている場合、このファイルには .NET Framework 4 の正しいエントリが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="918d6-300">*Aspnet\_コンパイラ*コマンドを使用して、アプリケーション (ビルド環境など) をプリコンパイルする場合は、ターゲットフレームワークに対して正しいバージョンの*aspnet\_コンパイラ*コマンドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="918d6-301">.NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) に同梱されているコンパイラを使用して、.NET Framework 3.5 以前のバージョン用にコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="918d6-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="918d6-302">.NET Framework 4 に付属するコンパイラを使用して、そのフレームワークを使用して、またはそれ以降のバージョンを使用して作成されたアプリケーションをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="918d6-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="918d6-303">実行時に、コンパイラはコンピューターにインストールされている最新のフレームワークアセンブリ (したがって GAC 内) を使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="918d6-304">後でフレームワークに対して更新が行われた場合 (たとえば、仮定のバージョン4.1 がインストールされている場合)、 *targetframework*属性が下位バージョン (4.0 など) を対象としていても、新しいバージョンのフレームワークの機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="918d6-305">(ただし、Visual Studio 2010 のデザイン時、または*aspnet\_コンパイラ*コマンドを使用すると、フレームワークの新しい機能を使用するとコンパイラエラーが発生します)。</span><span class="sxs-lookup"><span data-stu-id="918d6-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="918d6-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="918d6-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="918d6-307">Web フォームと MVC に含まれる jQuery</span><span class="sxs-lookup"><span data-stu-id="918d6-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="918d6-308">Web フォームと MVC の両方に対応した Visual Studio テンプレートには、オープンソースの jQuery ライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="918d6-309">新しい web サイトまたはプロジェクトを作成すると、次の3つのファイルを含む Scripts フォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="918d6-310">jQuery-1.4.1 –ユーザーが判読できる、わかりやすいバージョンの jQuery ライブラリ。</span><span class="sxs-lookup"><span data-stu-id="918d6-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="918d6-311">jQuery-14.1:、jQuery ライブラリの縮小版です。</span><span class="sxs-lookup"><span data-stu-id="918d6-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="918d6-312">jQuery-は、jQuery ライブラリの Intellisense ドキュメントファイルを対象としています。</span><span class="sxs-lookup"><span data-stu-id="918d6-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="918d6-313">アプリケーションの開発中に、指定されていないバージョンの jQuery を含めます。</span><span class="sxs-lookup"><span data-stu-id="918d6-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="918d6-314">運用アプリケーション用の jQuery の縮小版を含めます。</span><span class="sxs-lookup"><span data-stu-id="918d6-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="918d6-315">たとえば、次の Web フォームページでは、jQuery を使用して、フォーカスがあるときに ASP.NET TextBox コントロールの背景色を黄色に変更する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="918d6-316">Content Delivery Network サポート</span><span class="sxs-lookup"><span data-stu-id="918d6-316">Content Delivery Network Support</span></span>

<span data-ttu-id="918d6-317">Microsoft Ajax Content Delivery Network (CDN) を使用すると、ASP.NET Ajax および jQuery スクリプトを Web アプリケーションに簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="918d6-318">たとえば、次のような Ajax.microsoft.com を指す`<script>`タグをページに追加するだけで、jQuery ライブラリの使用を開始できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="918d6-319">Microsoft Ajax CDN を利用することで、Ajax アプリケーションのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="918d6-320">Microsoft Ajax CDN の内容は、世界中のサーバーにキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="918d6-321">さらに、Microsoft Ajax CDN を使用すると、ブラウザーは、異なるドメインに配置されている Web サイトに対してキャッシュされた JavaScript ファイルを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="918d6-322">Microsoft Ajax Content Delivery Network は、Secure Sockets Layer を使用して web ページを提供する必要がある場合に、SSL (HTTPS) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="918d6-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="918d6-323">CDN が使用できない場合は、フォールバックを実装します。</span><span class="sxs-lookup"><span data-stu-id="918d6-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="918d6-324">フォールバックをテストします。</span><span class="sxs-lookup"><span data-stu-id="918d6-324">Test the fallback.</span></span>

<span data-ttu-id="918d6-325">Microsoft Ajax CDN の詳細については、次の web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="918d6-326">ASP.NET ScriptManager は、Microsoft Ajax CDN をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="918d6-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="918d6-327">1つのプロパティ (EnableCdn プロパティ) を設定するだけで、CDN からすべての ASP.NET framework JavaScript ファイルを取得できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="918d6-328">EnableCdn プロパティを true に設定すると、ASP.NET フレームワークは、検証および UpdatePanel に使用されるすべての JavaScript ファイルを含むすべての ASP.NET framework JavaScript ファイルを CDN から取得します。</span><span class="sxs-lookup"><span data-stu-id="918d6-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="918d6-329">この1つのプロパティを設定すると、web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="918d6-330">Webresource.axd 属性を使用して、独自の JavaScript ファイルの CDN パスを設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="918d6-331">新しい CdnPath プロパティは、EnableCdn プロパティを true に設定したときに使用される CDN へのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="918d6-332">ScriptManager の明示的なスクリプト</span><span class="sxs-lookup"><span data-stu-id="918d6-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="918d6-333">以前は、ASP.NET ScriptManger を使用した場合、モノリシック ASP.NET Ajax ライブラリ全体を読み込む必要がありました。</span><span class="sxs-lookup"><span data-stu-id="918d6-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="918d6-334">AjaxFrameworkMode の新しいプロパティを利用することで、ASP.NET Ajax ライブラリのどのコンポーネントが読み込まれるかを厳密に制御し、必要な ASP.NET Ajax ライブラリのコンポーネントのみを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="918d6-335">AjaxFrameworkMode プロパティには、次の値を設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="918d6-336">有効-ScriptManager コントロールに Microsoftajax.js スクリプトファイルが自動的に含まれることを指定します。これは、すべてのコアフレームワークスクリプト (レガシ動作) の結合されたスクリプトファイルです。</span><span class="sxs-lookup"><span data-stu-id="918d6-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="918d6-337">Disabled-Microsoft Ajax スクリプトのすべての機能が無効になっていること、および ScriptManager コントロールがスクリプトを自動的に参照していないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="918d6-338">Explicit--ページに必要な個別のフレームワークコアスクリプトファイルへのスクリプト参照を明示的に含めること、および各スクリプトファイルに必要な依存関係への参照を含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="918d6-339">たとえば、AjaxFrameworkMode プロパティを明示的な値に設定した場合は、必要な特定の ASP.NET Ajax コンポーネントスクリプトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="918d6-340">Web フォーム</span><span class="sxs-lookup"><span data-stu-id="918d6-340">Web Forms</span></span>

<span data-ttu-id="918d6-341">ASP.NET 1.0 のリリース以降、Web フォームは ASP.NET のコア機能になっています。</span><span class="sxs-lookup"><span data-stu-id="918d6-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="918d6-342">ASP.NET 4 のこの領域には、次のような多くの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="918d6-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="918d6-343">*メタ*タグを設定する機能。</span><span class="sxs-lookup"><span data-stu-id="918d6-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="918d6-344">ビューステートをより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-344">More control over view state.</span></span>
- <span data-ttu-id="918d6-345">ブラウザー機能を簡単に操作できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="918d6-346">Web フォームでの ASP.NET ルーティングの使用のサポート。</span><span class="sxs-lookup"><span data-stu-id="918d6-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="918d6-347">生成された Id をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-347">More control over generated IDs.</span></span>
- <span data-ttu-id="918d6-348">選択された行をデータコントロールで永続化する機能。</span><span class="sxs-lookup"><span data-stu-id="918d6-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="918d6-349">*FormView*コントロールと*ListView*コントロールでのレンダリングされた HTML の詳細な制御。</span><span class="sxs-lookup"><span data-stu-id="918d6-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="918d6-350">データソースコントロールのフィルター処理のサポート。</span><span class="sxs-lookup"><span data-stu-id="918d6-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="918d6-351">メタタグを MetaDescription プロパティとページに設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="918d6-352">ASP.NET 4 は、*ページ*クラスに*メタキーワード*と*MetaDescription*の2つのプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="918d6-353">これら2つのプロパティは、次の例に示すように、ページ内の対応する*メタ*タグを表します。</span><span class="sxs-lookup"><span data-stu-id="918d6-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="918d6-354">これら2つのプロパティは、ページの*Title*プロパティと同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="918d6-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="918d6-355">次の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="918d6-355">They follow these rules:</span></span>

1. <span data-ttu-id="918d6-356">*Head*要素に、プロパティ名に一致する*メタ*タグがない場合 (つまり、 *MetaDescription*の場合は name = "keywords ")、これらのプロパティは設定されていないことを意味します。) が表示されると、*メタ*タグがページに追加されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="918d6-357">これらの名前を持つ*メタ*タグが既に存在する場合、これらのプロパティは既存のタグの内容の get および set メソッドとして機能します。</span><span class="sxs-lookup"><span data-stu-id="918d6-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="918d6-358">これらのプロパティは実行時に設定できます。これにより、データベースまたは他のソースからコンテンツを取得できます。また、タグを動的に設定して、特定のページの内容を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="918d6-359">次の例のように、Web フォームページのマークアップの上部にある *@ Page*ディレクティブで*Keywords*および*Description*プロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="918d6-360">これにより、ページで既に宣言されている*メタ*タグの内容がオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="918d6-361">Description *meta*タグの内容は、Google での検索リストのプレビューを改善するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="918d6-362">(詳細については、Google 作り直し Central ブログの「 [meta description を使用したスニペットの改善](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)」を参照してください)。Google と Windows Live Search では、キーワードの内容を何も使用しませんが、他の検索エンジンでは使用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="918d6-363">詳細については、検索エンジンガイド Web サイトの「 [Meta Keywords アドバイス](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="918d6-364">これらの新しいプロパティは単純な機能ですが、これらのプロパティを手動で追加したり、独自のコードを記述して*meta*タグを作成したりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="918d6-365">個々のコントロールのビューステートを有効にする</span><span class="sxs-lookup"><span data-stu-id="918d6-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="918d6-366">既定では、ページに対してビューステートが有効になっています。これにより、ページ上の各コントロールは、アプリケーションで必要でない場合でも、ビューステートを保存する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="918d6-367">ビューステートデータは、ページによって生成されるマークアップに含まれ、クライアントへのページの送信とポストバックにかかる時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="918d6-368">必要以上に多くのビューステートを格納すると、パフォーマンスが大幅に低下する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="918d6-369">以前のバージョンの ASP.NET では、開発者はページサイズを減らすために個々のコントロールのビューステートを無効にすることができましたが、個別のコントロールに対して明示的に行う必要がありました。</span><span class="sxs-lookup"><span data-stu-id="918d6-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="918d6-370">ASP.NET 4 では、Web サーバーコントロールに*Viewstatemode*プロパティが含まれています。このプロパティを使用すると、ビューステートを既定で無効にして、ページに必要なコントロールに対してのみ有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="918d6-371">*Viewstatemode*プロパティは、次の3つの値を持つ列挙を受け取ります。*Enabled*、 *Disabled*、および*Inherit*。</span><span class="sxs-lookup"><span data-stu-id="918d6-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="918d6-372">*Enabled*は、そのコントロールおよび*継承*するように設定されている子コントロール、または何も設定されていない子コントロールのビューステートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="918d6-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="918d6-373">*Disabled*はビューステートを無効にし、*継承*はコントロールが親コントロールから*viewstatemode*設定を使用することを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="918d6-374">*Viewstatemode*プロパティがどのように機能するかを次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="918d6-375">次のページのコントロールのマークアップとコードには、 *Viewstatemode*プロパティの値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="918d6-376">ご覧のように、このコードは PlaceHolder1 コントロールのビューステートを無効にします。</span><span class="sxs-lookup"><span data-stu-id="918d6-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="918d6-377">子 label1 コントロールは、このプロパティ値を継承します (コントロールの*Viewstatemode*の既定値は*Inherit*です)。したがって、ビューステートは保存されません。</span><span class="sxs-lookup"><span data-stu-id="918d6-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="918d6-378">PlaceHolder2 コントロールでは、 *Viewstatemode*が Enabled に設定されて*いる*ため、label2 はこのプロパティを継承し、ビューステートを保存します。</span><span class="sxs-lookup"><span data-stu-id="918d6-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="918d6-379">ページが最初に読み込まれるときに、両方の*ラベル*コントロールの*Text*プロパティが文字列 "[DynamicValue]" に設定されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="918d6-380">これらの設定の効果は、ページが初めて読み込まれるときに、ブラウザーに次の出力が表示されることです。</span><span class="sxs-lookup"><span data-stu-id="918d6-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="918d6-381">無効に`: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="918d6-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="918d6-382">Enabled`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="918d6-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="918d6-383">ただし、ポストバック後、次の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="918d6-384">無効に`: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="918d6-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="918d6-385">Enabled`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="918d6-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="918d6-386">Label1 コントロール ( *Viewstatemode*値が*Disabled*に設定されている) は、コードで設定された値を保持していません。</span><span class="sxs-lookup"><span data-stu-id="918d6-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="918d6-387">ただし、label2 コントロール ( *Viewstatemode*値が Enabled に設定され*て*いる) は、その状態を保持しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="918d6-388">次の例のように、 *@ Page*ディレクティブで*viewstatemode*を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="918d6-389">*Page*クラスは、別のコントロールです。これは、ページ内の他のすべてのコントロールの親コントロールとして機能します。</span><span class="sxs-lookup"><span data-stu-id="918d6-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="918d6-390">*Page*のインスタンスに対して*viewstatemode*の既定値が*有効になっ*ています。</span><span class="sxs-lookup"><span data-stu-id="918d6-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="918d6-391">コントロールが既定で*継承*するため、 *viewstatemode*を page レベルまたは control level に設定しない限り、コントロールは*Enabled*プロパティ値を継承します。</span><span class="sxs-lookup"><span data-stu-id="918d6-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="918d6-392">*Viewstatemode*プロパティの値は、 *enableviewstate*プロパティが*true*に設定されている場合にのみビューステートを維持するかどうかを決定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="918d6-393">*Enableviewstate*プロパティが*false*に設定されている場合、 *viewstatemode*が*有効*に設定されていても、ビューステートは維持されません。</span><span class="sxs-lookup"><span data-stu-id="918d6-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="918d6-394">この機能を使用するには、マスターページの*ContentPlaceHolder*コントロールを使用することをお勧めします。この場合、マスターページの*Viewstatemode*を*無効*に設定し、 *ContentPlaceHolder*コントロールに対して個別に有効にすることができます。ビューステートを必要とするコントロールを含みます。</span><span class="sxs-lookup"><span data-stu-id="918d6-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="918d6-395">ブラウザー機能の変更点</span><span class="sxs-lookup"><span data-stu-id="918d6-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="918d6-396">ASP.NET は、*ブラウザー機能*と呼ばれる機能を使用してサイトを参照するためにユーザーが使用しているブラウザーの機能を決定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="918d6-397">ブラウザーの機能は、 *Httpbrowsercapabilities*オブジェクト (*要求*によって公開されます) によって表されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="918d6-398">たとえば、 *Httpbrowsercapabilities*オブジェクトを使用して、現在のブラウザーの型とバージョンが JavaScript の特定のバージョンをサポートしているかどうかを判断できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="918d6-399">または、 *Httpbrowsercapabilities*オブジェクトを使用して、要求がモバイルデバイスから送信されたものかどうかを判断することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="918d6-400">*Httpbrowsercapabilities*オブジェクトは、一連のブラウザー定義ファイルによって駆動されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="918d6-401">これらのファイルには、特定のブラウザーの機能に関する情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="918d6-402">ASP.NET 4 では、これらのブラウザー定義ファイルが更新され、最近導入されたブラウザーとデバイス (Google Chrome、モーション BlackBerry スマートフォン、Apple iPhone など) に関する情報が含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="918d6-403">次の一覧に、新しいブラウザー定義ファイルを示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="918d6-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-404">*blackberry.browser*</span></span>
- <span data-ttu-id="918d6-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-405">*chrome.browser*</span></span>
- <span data-ttu-id="918d6-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-406">*Default.browser*</span></span>
- <span data-ttu-id="918d6-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-407">*firefox.browser*</span></span>
- <span data-ttu-id="918d6-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-408">*gateway.browser*</span></span>
- <span data-ttu-id="918d6-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-409">*generic.browser*</span></span>
- <span data-ttu-id="918d6-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-410">*ie.browser*</span></span>
- <span data-ttu-id="918d6-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-411">*iemobile.browser*</span></span>
- <span data-ttu-id="918d6-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-412">*iphone.browser*</span></span>
- <span data-ttu-id="918d6-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-413">*opera.browser*</span></span>
- <span data-ttu-id="918d6-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="918d6-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="918d6-415">ブラウザー機能プロバイダーの使用</span><span class="sxs-lookup"><span data-stu-id="918d6-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="918d6-416">ASP.NET バージョン 3.5 Service Pack 1 では、次の方法でブラウザーに用意されている機能を定義できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="918d6-417">コンピューターレベルでは、次のフォルダーに XML `.browser`ファイルを作成または更新します。</span><span class="sxs-lookup"><span data-stu-id="918d6-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="918d6-418">ブラウザー機能を定義したら、Visual Studio コマンドプロンプトから次のコマンドを実行して、ブラウザー機能アセンブリをリビルドし、GAC に追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="918d6-419">個々のアプリケーションについては、 `.browser`アプリケーションの`App_Browsers`フォルダーにファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="918d6-420">これらの方法では、XML ファイルを変更する必要があります。また、コンピューターレベルの変更の場合は、\_aspnet regbrowsers プロセスを実行した後でアプリケーションを再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="918d6-421">ASP.NET 4 には、*ブラウザー機能プロバイダー*と呼ばれる機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="918d6-422">名前が示すように、これによってプロバイダーを作成し、独自のコードを使用してブラウザーの機能を決定することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="918d6-423">実際には、開発者がカスタムブラウザー機能を定義していないことがよくあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="918d6-424">ブラウザーファイルを更新するのは困難ですが、更新プロセスはかなり複雑であり、ファイルの`.browser` XML 構文は使用および定義が複雑になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="918d6-425">一般的なブラウザー定義の構文、または最新のブラウザー定義が含まれているデータベース、またはこのようなデータベースの Web サービスでも、この処理がはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="918d6-426">新しいブラウザー機能プロバイダーの機能により、これらのシナリオが可能になり、サードパーティの開発者にとって実用的になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="918d6-427">新しい ASP.NET 4 ブラウザー機能プロバイダー機能を使用するには、2つの主な方法があります。 ASP.NET browser 機能定義機能を拡張するか、全体を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="918d6-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="918d6-428">以下のセクションでは、最初に機能を置き換える方法と、その機能を拡張する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="918d6-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="918d6-429">ASP.NET Browser 機能の置き換え</span><span class="sxs-lookup"><span data-stu-id="918d6-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="918d6-430">ASP.NET browser 機能の定義機能を完全に置き換えるには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="918d6-431">次の例のように、 *HttpCapabilitiesProvider*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするプロバイダークラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="918d6-432">この例のコードでは、ブラウザーという名前の機能だけを指定し、その機能を MyCustomBrowser に設定する新しい*Httpbrowsercapabilities*オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="918d6-433">プロバイダーをアプリケーションに登録します。</span><span class="sxs-lookup"><span data-stu-id="918d6-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="918d6-434">アプリケーションでプロバイダーを使用するに`Web.config`は、*プロバイダー*の属性をまたは`Machine.config`ファイルの*browsercaps*セクションに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="918d6-435">(特定のモバイルデバイスのフォルダーなど、アプリケーション内の特定のディレクトリの*場所*要素にプロバイダー属性を定義することもできます)。次の例は、構成ファイルで*provider*属性を設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="918d6-436">新しいブラウザー機能の定義を登録するもう1つの方法は、次の例に示すようにコードを使用することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="918d6-437">このコードは、 `Global.asax`ファイルの*アプリケーション\_開始*イベントで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="918d6-438">*BrowserCapabilitiesProvider*クラスの変更は、アプリケーション内のコードを実行する前に行う必要があります。これにより、キャッシュが解決済みの*使用*オブジェクトに対して有効な状態のままになるようにします。</span><span class="sxs-lookup"><span data-stu-id="918d6-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="918d6-439">HttpBrowserCapabilities オブジェクトをキャッシュしています</span><span class="sxs-lookup"><span data-stu-id="918d6-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="918d6-440">前の例には1つの問題があります。これは、 *Httpbrowsercapabilities*オブジェクトを取得するために、カスタムプロバイダーが呼び出されるたびにコードが実行されることを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="918d6-441">これは、要求のたびに複数回発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="918d6-442">この例では、プロバイダーのコードはそれほど多くありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="918d6-443">ただし、 *Httpbrowsercapabilities*オブジェクトを取得するためにカスタムプロバイダーのコードが大きな作業を実行する場合は、パフォーマンスに影響する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="918d6-444">これが行われないようにするには、 *Httpbrowsercapabilities*オブジェクトをキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="918d6-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="918d6-445">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="918d6-445">Follow these steps:</span></span>

1. <span data-ttu-id="918d6-446">次の例のように、 *HttpCapabilitiesProvider*から派生するクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="918d6-447">この例では、コードはカスタム BuildCacheKey メソッドを呼び出すことによってキャッシュキーを生成し、カスタム GetCacheTime メソッドを呼び出すことによってキャッシュの時間を取得します。</span><span class="sxs-lookup"><span data-stu-id="918d6-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="918d6-448">次に、解決された*Httpbrowsercapabilities*オブジェクトをキャッシュに追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="918d6-449">オブジェクトはキャッシュから取得して、カスタムプロバイダーを使用する後続の要求で再利用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="918d6-450">前の手順の説明に従って、プロバイダーをアプリケーションに登録します。</span><span class="sxs-lookup"><span data-stu-id="918d6-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="918d6-451">ASP.NET Browser 機能の拡張機能</span><span class="sxs-lookup"><span data-stu-id="918d6-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="918d6-452">前のセクションでは、ASP.NET 4 で新しい*Httpbrowsercapabilities*オブジェクトを作成する方法について説明しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="918d6-453">また、ASP.NET に既に存在するものに新しいブラウザー機能の定義を追加して、ASP.NET ブラウザー機能の機能を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="918d6-454">これは、XML ブラウザー定義を使用せずに行うことができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="918d6-455">次の手順では、その方法を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="918d6-456">次の例に示すように、 *HttpCapabilitiesEvaluator*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="918d6-457">このコードでは、まず、ASP.NET ブラウザーの機能を使用してブラウザーを識別します。</span><span class="sxs-lookup"><span data-stu-id="918d6-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="918d6-458">ただし、要求で定義されている情報に基づいてブラウザーが識別されない場合 (つまり、 *Httpbrowsercapabilities*オブジェクトの*browser*プロパティが "Unknown" という文字列の場合)、このコードはカスタムプロバイダーを呼び出します (MyBrowserCapabilitiesEvaluator) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="918d6-459">前の例で説明したように、プロバイダーをアプリケーションに登録します。</span><span class="sxs-lookup"><span data-stu-id="918d6-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="918d6-460">既存の機能の定義に新しい機能を追加してブラウザー機能の機能を拡張する</span><span class="sxs-lookup"><span data-stu-id="918d6-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="918d6-461">カスタムブラウザー定義プロバイダーを作成し、新しいブラウザー定義を動的に作成するだけでなく、既存のブラウザー定義を拡張して機能を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="918d6-462">これにより、必要なものに近い定義を使用できますが、いくつかの機能がありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="918d6-463">そのためには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="918d6-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="918d6-464">次の例に示すように、 *HttpCapabilitiesEvaluator*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="918d6-465">このコード例では、既存の ASP.NET *HttpCapabilitiesEvaluator*クラスを拡張し、次のコードを使用して、現在の要求定義と一致する*httpbrowsercapabilities*オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="918d6-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="918d6-466">このコードでは、このブラウザーの機能を追加または変更できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="918d6-467">新しいブラウザー機能を指定するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="918d6-468">*使用*オブジェクトの*Capabilities*プロパティによって公開される*IDictionary*オブジェクトに、キーと値のペアを追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="918d6-469">前の例では、コードによってマルチタッチという名前の機能が追加され、値が*true*になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="918d6-470">*使用*オブジェクトの既存のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="918d6-471">前の例では、コードによって*Frames*プロパティが*true*に設定されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="918d6-472">このプロパティは、 *Capabilities*プロパティによって公開される*IDictionary*オブジェクトのアクセサーにすぎません。</span><span class="sxs-lookup"><span data-stu-id="918d6-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="918d6-473">注このモデルは、コントロールアダプターを含む*Httpbrowsercapabilities*の任意のプロパティに適用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="918d6-474">前の手順で説明したように、プロバイダーをアプリケーションに登録します。</span><span class="sxs-lookup"><span data-stu-id="918d6-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="918d6-475">ASP.NET 4 でのルーティング</span><span class="sxs-lookup"><span data-stu-id="918d6-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="918d6-476">ASP.NET 4 では、Web フォームでのルーティングを使用するための組み込みサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="918d6-477">ルーティングを使用すると、物理ファイルにマップされていない要求 Url を受け入れるようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="918d6-478">代わりに、ルーティングを使用して、ユーザーにとって意味のある Url を定義し、アプリケーションの検索エンジン最適化 (SEO) に役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="918d6-479">たとえば、既存のアプリケーションに製品カテゴリを表示するページの URL は、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="918d6-480">ルーティングを使用すると、次の URL を使用して同じ情報を表示するようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="918d6-481">ルーティングは、ASP.NET 3.5 SP1 以降で利用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="918d6-482">(ASP.NET 3.5 SP1 でルーティングを使用する方法の例については、(http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "このエントリの")「 [routing With WebForms]Title」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="918d6-483">Phil Haack のブログをご覧ください。)ただし、ASP.NET 4 には、ルーティングを使用しやすくするための機能がいくつか含まれています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="918d6-484">*PageRouteHandler*クラス。ルートを定義するときに使用する単純な HTTP ハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="918d6-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="918d6-485">クラスは、要求のルーティング先のページにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="918d6-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="918d6-486">新しいプロパティは、 *httprequest*と*ページの routedata*です。これは、 *httprequest データ*オブジェクトのプロキシです。</span><span class="sxs-lookup"><span data-stu-id="918d6-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="918d6-487">これらのプロパティを使用すると、ルートから渡された情報に簡単にアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="918d6-488">次の新しい式ビルダーは、次の新しい式ビルダーで定義されています。このビルダーおよび*system.web.* .</span><span class="sxs-lookup"><span data-stu-id="918d6-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="918d6-489">*Routeurl*。 ASP.NET サーバーコントロール内のルート url に対応する url を作成する簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="918d6-490">*Routevalue*。 *RouteContext*オブジェクトから情報を抽出する簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="918d6-491">*Routeparameter*クラスを使用すると、 *RouteContext*オブジェクトに含まれるデータをデータソースコントロールのクエリに簡単に渡すことができます ( [*formparameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)に似ています)。</span><span class="sxs-lookup"><span data-stu-id="918d6-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="918d6-492">Web フォームページのルーティング</span><span class="sxs-lookup"><span data-stu-id="918d6-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="918d6-493">次の例は、 *route*クラスの new *MapPageRoute*メソッドを使用して、Web フォームのルートを定義する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="918d6-494">ASP.NET 4 では、 *MapPageRoute*メソッドが導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="918d6-495">次の例は、前の例で示した SearchRoute 定義に相当しますが、 *PageRouteHandler*クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="918d6-496">この例のコードでは、ルートを物理ページ (最初のルート`~/search.aspx`では) にマップします。</span><span class="sxs-lookup"><span data-stu-id="918d6-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="918d6-497">また、最初のルート定義では、searchterm という名前のパラメーターを URL から抽出し、ページに渡す必要があることも指定しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="918d6-498">*MapPageRoute*メソッドでは、次のメソッドオーバーロードがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="918d6-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span><span class="sxs-lookup"><span data-stu-id="918d6-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="918d6-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span><span class="sxs-lookup"><span data-stu-id="918d6-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="918d6-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span><span class="sxs-lookup"><span data-stu-id="918d6-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="918d6-502">*Checkphysicalurlaccess*パラメーターは、ルーティング先の物理ページ (この場合は default.aspx) のセキュリティアクセス許可、および受信 URL (この場合は search/{searchterm}) に対するアクセス許可をルートがチェックするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="918d6-503">*Checkphysicalurlaccess*の値が*false*の場合は、受信 URL のアクセス許可だけがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="918d6-504">これらのアクセス許可は、 `Web.config`次のような設定を使用してファイルで定義されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="918d6-505">この例の構成では、管理者ロールに属し`search.aspx`ているユーザーを除くすべてのユーザーについて、物理ページへのアクセスが拒否されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="918d6-506">*Checkphysicalurlaccess*パラメーターが*true* (既定値) に設定されている場合、物理ページの検索はそのロールのユーザーに制限されているので、管理者ユーザーのみが URL にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="918d6-507">*Checkphysicalurlaccess*が*false*に設定されていて、サイトが前の例のように構成されている場合、認証されたすべてのユーザーは URL にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="918d6-508">Web フォームページでのルーティング情報の読み取り</span><span class="sxs-lookup"><span data-stu-id="918d6-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="918d6-509">Web フォームの物理ページのコードでは、次の2つの新しいプロパティを使用して、ルーティングによって URL から抽出された情報 (または別のオブジェクトによって*Routedata*オブジェクトに追加されたその他の情報) にアクセスできます。*HttpRequest*および*ページの routedata*。</span><span class="sxs-lookup"><span data-stu-id="918d6-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="918d6-510">(*ページの RouteData*は、 *HttpRequest. routedata routedata*をラップします)。次の例では、*ページの RouteData*を使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="918d6-511">このコードは、前の例のルートで定義されているように、searchterm パラメーターに渡された値を抽出します。</span><span class="sxs-lookup"><span data-stu-id="918d6-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="918d6-512">次の要求 URL について考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="918d6-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="918d6-513">この要求が行われると、 `search.aspx`ページに "scott" という単語が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="918d6-514">マークアップでのルーティング情報へのアクセス</span><span class="sxs-lookup"><span data-stu-id="918d6-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="918d6-515">前のセクションで説明したメソッドは、Web フォームページのコードでルートデータを取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="918d6-516">また、同じ情報にアクセスできるように、マークアップで式を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="918d6-517">式ビルダーは、宣言型コードを操作するための強力で洗練された方法です。</span><span class="sxs-lookup"><span data-stu-id="918d6-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="918d6-518">(詳細については、Phil Haack のブログの「[カスタム式ビルダーを使用した Express](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)の入力」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="918d6-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="918d6-519">ASP.NET 4 には、Web フォームルーティング用の2つの新しい式ビルダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="918d6-520">次の例は、これらの使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="918d6-521">この例では、 *routeurl*式を使用して、ルートパラメーターに基づく URL を定義しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="918d6-522">これにより、完全な URL をマークアップにハードコーディングする必要がなくなり、後で URL 構造を変更しても、このリンクを変更する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="918d6-523">このマークアップでは、前に定義したルートに基づいて、次の URL が生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="918d6-524">ASP.NET は、入力パラメーターに基づいて、正しいルートを自動的に処理します (つまり、正しい URL を生成します)。</span><span class="sxs-lookup"><span data-stu-id="918d6-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="918d6-525">また、式にルート名を含めることもできます。これにより、使用するルートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="918d6-526">*Routevalue*式を使用する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="918d6-527">このコントロールを含むページを実行すると、ラベルに "scott" という値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="918d6-528">*Routevalue*式を使用すると、マークアップでルートデータを簡単に使用できるようになります。また、マークアップでは、より複雑なページの routevalue ["x"] 構文を使用する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="918d6-529">データソース管理パラメーターにルートデータを使用する</span><span class="sxs-lookup"><span data-stu-id="918d6-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="918d6-530">*Routeparameter*クラスを使用すると、データソースコントロール内のクエリのパラメーター値としてルートデータを指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="918d6-531">これは、次の例に示すように、クラスと[よく似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)ています。</span><span class="sxs-lookup"><span data-stu-id="918d6-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="918d6-532">ルート パラメーターの searchterm の値が使用しての例では、@companynameパラメーター、 *選択* ステートメント。</span><span class="sxs-lookup"><span data-stu-id="918d6-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the *Select* statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="918d6-533">クライアント Id の設定</span><span class="sxs-lookup"><span data-stu-id="918d6-533">Setting Client IDs</span></span>

<span data-ttu-id="918d6-534">新しい*Clientidmode*プロパティは、ASP.NET の長期間の問題に対処します。つまり、コントロールがレンダリングする要素の*id*属性を作成する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="918d6-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="918d6-535">アプリケーションにこれらの要素を参照するクライアントスクリプトが含まれている場合は、表示される要素の*id*属性を知っておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="918d6-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="918d6-536">Web サーバーコントロール用に表示される HTML の*id*属性は、コントロールの*ClientID*プロパティに基づいて生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="918d6-537">ASP.NET 4 までは、 *ClientID*プロパティから*id*属性を生成するアルゴリズムは、名前付けコンテナー (存在する場合) と id を連結し、(データコントロールと同様に) 繰り返し制御する場合にプレフィックスとシーケンシャルを追加する必要がありました。少数.</span><span class="sxs-lookup"><span data-stu-id="918d6-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="918d6-538">これは、ページ内のコントロールの Id が一意であることが常に保証されていますが、アルゴリズムによって、予測不可能な制御 Id が生成されたため、クライアントスクリプトでの参照が困難になっていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="918d6-539">新しい*Clientidmode*プロパティを使用すると、コントロールに対してクライアント ID を生成する方法をより正確に指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="918d6-540">ページなど、任意のコントロールに対して*Clientidmode*プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="918d6-541">設定できる設定は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="918d6-541">Possible settings are the following:</span></span>

- <span data-ttu-id="918d6-542">*Autoid* –これは、以前のバージョンの ASP.NET で使用されていた*ClientID*プロパティ値を生成するためのアルゴリズムに相当します。</span><span class="sxs-lookup"><span data-stu-id="918d6-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="918d6-543">*Static* – *ClientID*値が親名前付けコンテナーの id を連結せずに id と同じになるように指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="918d6-544">これは、Web ユーザーコントロールで役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="918d6-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="918d6-545">Web ユーザーコントロールはさまざまなページに配置でき、異なるコンテナーコントロールに配置される可能性があるため、ID 値がどのようになるかを予測できないため、 *Autoid*アルゴリズムを使用するコントロールのクライアントスクリプトを記述するのが困難な場合があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="918d6-546">*予測可能*-このオプションは、主にテンプレートの繰り返しを使用するデータコントロールで使用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="918d6-547">コントロールの名前付けコンテナーの ID プロパティを連結しますが、生成される*ClientID*値には、"ctlxxx" のような文字列は含まれません。</span><span class="sxs-lookup"><span data-stu-id="918d6-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="918d6-548">この設定は、コントロールの*ClientIDRowSuffix*プロパティと組み合わせて使用できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="918d6-549">*ClientIDRowSuffix*プロパティをデータフィールドの名前に設定し、そのフィールドの値を、生成された*ClientID*値のサフィックスとして使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="918d6-550">通常は、データレコードの主キーを*ClientIDRowSuffix*値として使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="918d6-551">*継承*–この設定は、コントロールの既定の動作です。これは、コントロールの ID 生成が親と同じであることを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="918d6-552">*Clientidmode*プロパティは、ページレベルで設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="918d6-553">これにより、現在のページ内のすべてのコントロールの既定の*Clientidmode*値が定義されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="918d6-554">ページレベルの既定の*Clientidmode*値は*autoid*で、コントロールレベルの既定の*Clientidmode*値は*Inherit*です。</span><span class="sxs-lookup"><span data-stu-id="918d6-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="918d6-555">その結果、コードのどこでもこのプロパティを設定しなかった場合、すべてのコントロールが既定で*Autoid*アルゴリズムになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="918d6-556">次の例に示すように、 *@ page*ディレクティブでページレベルの値を設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="918d6-557">また、構成ファイルで、コンピューター (コンピューター) レベルまたはアプリケーションレベルのいずれかで、 *Clientidmode*値を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="918d6-558">これにより、アプリケーション内のすべてのページのすべてのコントロールに対する既定の*Clientidmode*設定が定義されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="918d6-559">コンピューターレベルで値を設定すると、そのコンピューター上のすべての Web サイトの既定の*Clientidmode*設定が定義されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="918d6-560">次の例は、構成ファイルの*Clientidmode*設定を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="918d6-561">前述のように、 *ClientID*プロパティの値は、コントロールの親の名前付けコンテナーから派生します。</span><span class="sxs-lookup"><span data-stu-id="918d6-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="918d6-562">マスターページを使用している場合など、一部のシナリオでは、コントロールは次のレンダリングされた HTML のような Id で終了することがあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="918d6-563">場合でも、*入力*マークアップに示される要素 (から、 *テキスト ボックス*コントロール) 2 つの名前付けコンテナーは、ページの深さ (入れ子になった*ContentPlaceholder*コントロール)、マスター ページが処理されるため、最終結果は、次のようにコントロール ID です。</span><span class="sxs-lookup"><span data-stu-id="918d6-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="918d6-564">この ID はページ内で一意であることが保証されていますが、ほとんどの場合、この ID は不必要に長くなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="918d6-565">レンダリングされた ID の長さを減らし、ID の生成方法をより細かく制御できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="918d6-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="918d6-566">(たとえば、"ctlxxx" プレフィックスを削除する場合など)。これを実現する最も簡単な方法は、次の例に示すように、 *Clientidmode*プロパティを設定することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="918d6-567">このサンプルでは、最も外側の*Namingpanel*要素に対して*Clientidmode*プロパティが*Static*に設定され、内側の*Namingpanel*要素に対して*予測可能*に設定されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="918d6-568">これらの設定により、次のマークアップが生成されます (ページの残りの部分とマスターページは、前の例と同じであると見なされます)。</span><span class="sxs-lookup"><span data-stu-id="918d6-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="918d6-569">*静的*な設定では、最も外側の*namingpanel*要素内の任意のコントロールの名前付け階層をリセットし、生成された ID から ContentPlaceHolder id と id を除去する効果があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="918d6-570">(レンダリングされた要素の*name*属性は影響を受けないため、通常の ASP.NET 機能はイベントやビューステートなどのために保持されます)。名前付け階層をリセットする副作用として、 *Namingpanel*要素のマークアップを別の*ContentPlaceholder*コントロールに移動したとしても、レンダリングされたクライアント id は変わりません。</span><span class="sxs-lookup"><span data-stu-id="918d6-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="918d6-571">表示されるコントロール Id が一意であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="918d6-572">そうでない場合は、 *document.getelementbyid*関数など、個々の HTML 要素に対して一意の id を必要とする機能を中断できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="918d6-573">データバインドコントロールでの予測可能なクライアント Id の作成</span><span class="sxs-lookup"><span data-stu-id="918d6-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="918d6-574">レガシアルゴリズムによってデータバインドリストコントロールに生成される*ClientID*値は、長くなる可能性があり、実際には予測できません。</span><span class="sxs-lookup"><span data-stu-id="918d6-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="918d6-575">*Clientidmode*機能は、これらの id の生成方法をより細かく制御するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="918d6-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="918d6-576">次の例のマークアップには、 *ListView*コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="918d6-577">前の例では、 *Clientidmode*プロパティと*RowClientIDRowSuffix*プロパティがマークアップで設定されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="918d6-578">*ClientIDRowSuffix*プロパティはデータバインドコントロールでのみ使用でき、その動作は使用しているコントロールによって異なります。</span><span class="sxs-lookup"><span data-stu-id="918d6-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="918d6-579">違いは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="918d6-579">The differences are these:</span></span>

- <span data-ttu-id="918d6-580">*GridView*コントロール—データソース内の1つまたは複数の列の名前を指定できます。この名前は実行時に組み合わされ、クライアント id が作成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="918d6-581">たとえば、 *RowClientIDRowSuffix*を "ProductName, ProductId" に設定した場合、レンダリングされた要素のコントロール id の形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="918d6-582">*ListView*コントロール—クライアント ID に追加されるデータソース内の1つの列を指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="918d6-583">たとえば、 *ClientIDRowSuffix*を "ProductName" に設定した場合、レンダリングされるコントロール id の形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="918d6-584">この場合、後続の1は、現在のデータ項目の製品 ID から派生します。</span><span class="sxs-lookup"><span data-stu-id="918d6-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="918d6-585">*Repeater*コントロール: このコントロールは、 *ClientIDRowSuffix*プロパティをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="918d6-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="918d6-586">*Repeater*コントロールでは、現在の行のインデックスが使用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="918d6-587">*Repeater*コントロールで ClientIDMode = "予測可能" を使用すると、次の形式のクライアント id が生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="918d6-588">末尾の0は、現在の行のインデックスです。</span><span class="sxs-lookup"><span data-stu-id="918d6-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="918d6-589">*FormView*コントロールと*DetailsView*コントロールには複数の行が表示されないため、 *ClientIDRowSuffix*プロパティをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="918d6-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="918d6-590">データコントロールでの行選択の保持</span><span class="sxs-lookup"><span data-stu-id="918d6-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="918d6-591">*GridView*コントロールと*ListView*コントロールを使用して、ユーザーが行を選択できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="918d6-592">以前のバージョンの ASP.NET では、ページの行インデックスに基づいて選択が行われていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="918d6-593">たとえば、ページ1の3番目の項目を選択し、ページ2に移動すると、そのページの3番目の項目が選択されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="918d6-594">永続化の選択は、最初は .NET Framework 3.5 SP1 の動的データプロジェクトでのみサポートされていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="918d6-595">この機能が有効になっている場合、現在選択されている項目は項目のデータキーに基づきます。</span><span class="sxs-lookup"><span data-stu-id="918d6-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="918d6-596">これは、ページ1の3番目の行を選択し、ページ2に移動した場合、ページ2で何も選択されていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="918d6-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="918d6-597">ページ1に戻ると、3番目の行が選択されたままになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="918d6-598">次の例に示すように、 *EnablePersistedSelection*プロパティを使用すると、すべてのプロジェクトの*GridView*コントロールと*ListView*コントロールで、永続化された選択がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="918d6-599">ASP.NET Chart コントロール</span><span class="sxs-lookup"><span data-stu-id="918d6-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="918d6-600">ASP.NET *Chart*コントロールは、.NET Framework 内のデータ可視化オファリングを拡張します。</span><span class="sxs-lookup"><span data-stu-id="918d6-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="918d6-601">*グラフ*コントロールを使用すると、複雑な統計分析や財務分析のための直感的で視覚的に説得力のあるグラフを持つ ASP.NET ページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="918d6-602">ASP.NET *Chart*コントロールは .NET Framework バージョン 3.5 SP1 リリースのアドオンとして導入され、.NET Framework 4 リリースの一部になっています。</span><span class="sxs-lookup"><span data-stu-id="918d6-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="918d6-603">コントロールには、次の機能があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-603">The control includes the following features:</span></span>

- <span data-ttu-id="918d6-604">35 種類のグラフ</span><span class="sxs-lookup"><span data-stu-id="918d6-604">35 distinct chart types.</span></span>
- <span data-ttu-id="918d6-605">グラフ領域、タイトル、凡例、および注釈の数に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="918d6-606">すべてのグラフ要素のさまざまな外観設定。</span><span class="sxs-lookup"><span data-stu-id="918d6-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="918d6-607">ほとんどの種類のグラフでは、3-d がサポートしています。</span><span class="sxs-lookup"><span data-stu-id="918d6-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="918d6-608">データポイントを自動的に収めることができるスマートデータラベル。</span><span class="sxs-lookup"><span data-stu-id="918d6-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="918d6-609">ストリップライン、スケール区切り、および対数目盛り。</span><span class="sxs-lookup"><span data-stu-id="918d6-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="918d6-610">データの分析と変換に使用できる 50 を超える財務式および統計式。</span><span class="sxs-lookup"><span data-stu-id="918d6-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="918d6-611">グラフデータの単純なバインドと操作。</span><span class="sxs-lookup"><span data-stu-id="918d6-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="918d6-612">日付、時刻、通貨などの一般的なデータ形式のサポート。</span><span class="sxs-lookup"><span data-stu-id="918d6-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="918d6-613">Ajax を使用したクライアントクリックイベントなど、対話機能とイベントドリブンカスタマイズのサポート。</span><span class="sxs-lookup"><span data-stu-id="918d6-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="918d6-614">状態管理。</span><span class="sxs-lookup"><span data-stu-id="918d6-614">State management.</span></span>
- <span data-ttu-id="918d6-615">バイナリ ストリーム転送。</span><span class="sxs-lookup"><span data-stu-id="918d6-615">Binary streaming.</span></span>

<span data-ttu-id="918d6-616">次の図は、ASP.NET Chart コントロールによって生成される財務グラフの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="918d6-617">図 2: ASP.NET Chart コントロールの例</span><span class="sxs-lookup"><span data-stu-id="918d6-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="918d6-618">ASP.NET Chart コントロールの使用方法の例については、MSDN Web サイトの「 [Microsoft Chart コントロールのサンプル環境](https://go.microsoft.com/fwlink/?LinkId=128300)」ページでサンプルコードをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="918d6-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="918d6-619">コミュニティコンテンツのその他のサンプルについては、[グラフコントロールフォーラム](https://go.microsoft.com/fwlink/?LinkId=128713)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="918d6-620">ASP.NET ページへのグラフコントロールの追加</span><span class="sxs-lookup"><span data-stu-id="918d6-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="918d6-621">次の例は、マークアップを使用して ASP.NET ページに*グラフ*コントロールを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="918d6-622">この例では、*グラフ*コントロールによって、静的なデータポイントの縦棒グラフが生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="918d6-623">3-d グラフの使用</span><span class="sxs-lookup"><span data-stu-id="918d6-623">Using 3-D Charts</span></span>

<span data-ttu-id="918d6-624">*グラフ*コントロールには、グラフ領域の特性を定義する*ChartArea*オブジェクトを含むことができる、 *chartareas*コレクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="918d6-625">たとえば、グラフ領域に3-d を使用するには、次の例のように*Area3DStyle*プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="918d6-626">次の図は、*横棒*グラフの4つの系列を含む3-d グラフを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="918d6-627">図 3:3-d 横棒グラフ</span><span class="sxs-lookup"><span data-stu-id="918d6-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="918d6-628">スケール区切りと対数スケールの使用</span><span class="sxs-lookup"><span data-stu-id="918d6-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="918d6-629">スケール区切りと対数スケールは、グラフに洗練を追加するための2つの追加方法です。</span><span class="sxs-lookup"><span data-stu-id="918d6-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="918d6-630">これらの機能は、グラフ領域の各軸に固有です。</span><span class="sxs-lookup"><span data-stu-id="918d6-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="918d6-631">たとえば、グラフ領域の主軸の Y 軸でこれらの機能を使用するには、 *ChartArea*オブジェクトで*AxisY*プロパティと*scalebreakstyle*プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="918d6-632">次のスニペットは、主軸の Y 軸でスケール区切りを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="918d6-633">次の図は、スケール区切りが有効になっている Y 軸を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="918d6-634">図 4: スケール区切り</span><span class="sxs-lookup"><span data-stu-id="918d6-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="918d6-635">QueryExtender コントロールを使用したデータのフィルター処理</span><span class="sxs-lookup"><span data-stu-id="918d6-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="918d6-636">データドリブン Web ページを作成する開発者にとって非常に一般的なタスクは、データをフィルター処理することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="918d6-637">これは従来、データソースコントロールで*Where*句を構築することによって行われていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="918d6-638">この方法は複雑になる場合があります。場合によっては、 *Where*構文を使用しても、基になるデータベースのすべての機能を利用できないことがあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="918d6-639">フィルター処理を容易にするために、ASP.NET 4 に新しい*Queryextender*コントロールが追加されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="918d6-640">これらのコントロールによって返されるデータをフィルター処理するために、このコントロールを*EntityDataSource*または*LinqDataSource*コントロールに追加できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="918d6-641">*Queryextender*コントロールは LINQ に依存しているため、データがページに送信される前にデータベースサーバーにフィルターが適用されるため、非常に効率的な操作になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="918d6-642">*Queryextender*コントロールでは、さまざまなフィルターオプションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="918d6-643">以下のセクションでは、これらのオプションについて説明し、それらの使用方法の例を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="918d6-644">検索</span><span class="sxs-lookup"><span data-stu-id="918d6-644">Search</span></span>

<span data-ttu-id="918d6-645">検索オプションの場合、 *Queryextender*コントロールは、指定されたフィールド内で検索を実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="918d6-646">次の例では、コントロールは TextBoxSearch コントロールに入力されたテキストを使用し、 *LinqDataSource*コントロールから返さ`ProductName`れ`Supplier.CompanyName`たデータの列と列の内容を検索します。</span><span class="sxs-lookup"><span data-stu-id="918d6-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="918d6-647">範囲</span><span class="sxs-lookup"><span data-stu-id="918d6-647">Range</span></span>

<span data-ttu-id="918d6-648">Range オプションは検索オプションに似ていますが、範囲を定義する値のペアを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="918d6-649">次の例では、 *queryextender*コントロールは、 `UnitPrice` *LinqDataSource*コントロールから返されたデータ内の列を検索します。</span><span class="sxs-lookup"><span data-stu-id="918d6-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="918d6-650">範囲は、ページ上の TextBoxFrom コントロールと TextBoxTo コントロールから読み取られます。</span><span class="sxs-lookup"><span data-stu-id="918d6-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="918d6-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="918d6-651">PropertyExpression</span></span>

<span data-ttu-id="918d6-652">[プロパティ式] オプションを使用すると、プロパティ値の比較を定義できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="918d6-653">式が*true*に評価された場合、検査対象のデータが返されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="918d6-654">次の例では、 *queryextender*コントロールは、 `Discontinued`列のデータをページ上の CheckBoxDiscontinued コントロールの値と比較することによってデータをフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="918d6-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="918d6-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="918d6-655">CustomExpression</span></span>

<span data-ttu-id="918d6-656">最後に、 *Queryextender*コントロールで使用するカスタム式を指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="918d6-657">このオプションを使用すると、カスタムフィルターロジックを定義するページ内の関数を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="918d6-658">次の例は、 *Queryextender*コントロールでカスタム式を宣言によって指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="918d6-659">次の例は、 *Queryextender*コントロールによって呼び出されるカスタム関数を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="918d6-660">この場合、 *Where*句を含むデータベースクエリを使用する代わりに、コードは LINQ クエリを使用してデータをフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="918d6-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="918d6-661">これらの例では、一度に*Queryextender*コントロールで使用されている式が1つだけ表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="918d6-662">ただし、 *Queryextender*コントロール内には複数の式を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="918d6-663">Html エンコードされたコード式</span><span class="sxs-lookup"><span data-stu-id="918d6-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="918d6-664">一部の ASP.NET サイト (特に ASP.NET MVC) では、 `<%`構文 (多くの場合、"code ナゲット" と呼ばれます) を使用して応答にテキストを書き込むことに大きく依存して=  `expression %>`います。</span><span class="sxs-lookup"><span data-stu-id="918d6-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="918d6-665">コード式を使用する場合、テキストを HTML エンコードするのは簡単ではありません。テキストがユーザー入力からのものである場合、ページは XSS (クロスサイトスクリプティング) 攻撃に対して開いたままにすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="918d6-666">ASP.NET 4 では、コード式の次の新しい構文が導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="918d6-667">この構文では、応答への書き込み時に既定で HTML エンコーディングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="918d6-668">この新しい式は、実質的に次のように変換されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="918d6-669">たとえば、 &lt;%:要求 ["userinput"]%&gt; *要求 ["userinput"]* の値に対して HTML エンコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="918d6-670">この機能の目的は、古い構文のすべてのインスタンスを新しい構文に置き換えることができるようにすることです。これにより、使用するすべての手順を強制的に決定する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="918d6-671">ただし、出力されるテキストが HTML または既にエンコードされている場合もあります。この場合、エンコードが2倍になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="918d6-672">このような場合、ASP.NET 4 では、具象実装である*Htmlstring*と共に、新しいインターフェイス*ihtmlstring*が導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="918d6-673">これらの型のインスタンスを使用すると、戻り値が既に HTML として表示されるように適切にエンコード (または検証) されることを示すことができます。したがって、値は HTML エンコードされないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="918d6-674">たとえば、次のは HTML エンコードされていてはなりません。</span><span class="sxs-lookup"><span data-stu-id="918d6-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="918d6-675">ASP.NET MVC 2 ヘルパーメソッドは、この新しい構文で動作するように更新され、ASP.NET 4 を実行している場合にのみ、二重にエンコードされないようになっています。</span><span class="sxs-lookup"><span data-stu-id="918d6-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="918d6-676">ASP.NET 3.5 SP1 を使用してアプリケーションを実行する場合、この新しい構文は機能しません。</span><span class="sxs-lookup"><span data-stu-id="918d6-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="918d6-677">これによって、XSS 攻撃からの保護が保証されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="918d6-678">たとえば、引用符で囲まれていない属性値を使用する HTML には、依然として脆弱なユーザー入力を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="918d6-679">ASP.NET controls と ASP.NET MVC のヘルパーの出力には、常に引用符で囲んだ属性値が含まれていることに注意してください。これは推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="918d6-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="918d6-680">同様に、この構文では、ユーザー入力に基づいて JavaScript 文字列を作成する場合など、JavaScript のエンコードは実行されません。</span><span class="sxs-lookup"><span data-stu-id="918d6-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="918d6-681">プロジェクトテンプレートの変更</span><span class="sxs-lookup"><span data-stu-id="918d6-681">Project Template Changes</span></span>

<span data-ttu-id="918d6-682">以前のバージョンの ASP.NET では、Visual Studio を使用して新しい web サイトプロジェクトまたは web アプリケーションプロジェクトを作成すると、次に示すように、結果と`Web.config`して得ら`App_Data`れるプロジェクトには default.aspx ページ、既定のファイル、およびフォルダーのみが含まれます。図表</span><span class="sxs-lookup"><span data-stu-id="918d6-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="918d6-683">Visual Studio では、次の図に示すように、まったくファイルが含まれていない空の Web サイトプロジェクトタイプもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="918d6-684">その結果、初級者にとって、実稼働 Web アプリケーションを構築する方法についてのガイダンスはほとんどありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="918d6-685">このため、ASP.NET 4 では、空の Web アプリケーションプロジェクト用に1つ、Web アプリケーションと Web サイトプロジェクト用にそれぞれ1つずつ、3つの新しいテンプレートが導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="918d6-686">空の Web アプリケーションテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-686">Empty Web Application Template</span></span>

<span data-ttu-id="918d6-687">名前が示すように、空の Web アプリケーションテンプレートは、ダウンダウンされた Web アプリケーションプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="918d6-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="918d6-688">このプロジェクトテンプレートは、次の図に示すように、Visual Studio の [新しいプロジェクト] ダイアログボックスから選択します。</span><span class="sxs-lookup"><span data-stu-id="918d6-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="918d6-689">([クリックすると、フルサイズの画像が表示](overview/_static/image8.png)される)</span><span class="sxs-lookup"><span data-stu-id="918d6-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="918d6-690">空の ASP.NET Web アプリケーションを作成すると、Visual Studio によって次のフォルダーレイアウトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="918d6-691">これは、以前のバージョンの ASP.NET の空の Web サイトレイアウトに似ていますが、例外が1つあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="918d6-692">Visual studio 2010 では、空の web アプリケーションと空の web サイトプロジェクトに`Web.config`は、プロジェクトが対象としているフレームワークを識別するために visual Studio で使用される情報を含む次の最小限のファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="918d6-693">この*Targetframework*プロパティがない場合、Visual Studio では、古いアプリケーションを開くときに互換性を維持するために、既定で .NET Framework 2.0 を対象とします。</span><span class="sxs-lookup"><span data-stu-id="918d6-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="918d6-694">Web アプリケーションと Web サイトプロジェクトのテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="918d6-695">Visual Studio 2010 に付属するその他の2つの新しいプロジェクトテンプレートには、大幅な変更が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="918d6-696">次の図は、新しい Web アプリケーションプロジェクトを作成するときに作成されるプロジェクトのレイアウトを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="918d6-697">(Web サイトプロジェクトのレイアウトは実質的には同じです)。</span><span class="sxs-lookup"><span data-stu-id="918d6-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="918d6-698">プロジェクトには、以前のバージョンでは作成されなかった多数のファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="918d6-699">また、新しい Web アプリケーションプロジェクトは、基本メンバーシップ機能を使用して構成されます。これにより、新しいアプリケーションへのアクセスのセキュリティ保護をすぐに開始できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="918d6-700">このインクルードのため、 `Web.config`新しいプロジェクトのファイルには、メンバーシップ、ロール、およびプロファイルを構成するために使用されるエントリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="918d6-701">次の例は、 `Web.config`新しい Web アプリケーションプロジェクトのファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="918d6-702">(この例では、 *roleManager*は無効になっています)。</span><span class="sxs-lookup"><span data-stu-id="918d6-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="918d6-703">([クリックすると、フルサイズの画像が表示](overview/_static/image14.png)される)</span><span class="sxs-lookup"><span data-stu-id="918d6-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="918d6-704">このプロジェクトには、 `Web.config` `Account`ディレクトリ内の2番目のファイルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="918d6-705">2番目の構成ファイルは、ログインしていないユーザーの ChangePassword ページへのアクセスをセキュリティで保護する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="918d6-706">次の例は、2番目`Web.config`のファイルの内容を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="918d6-707">新しいプロジェクトテンプレートに既定で作成されるページには、以前のバージョンよりも多くのコンテンツが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="918d6-708">プロジェクトには既定のマスターページと CSS ファイルが含まれており、既定のページ (default.aspx) は既定でマスターページを使用するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="918d6-709">その結果、Web アプリケーションまたは Web サイトを初めて実行するときに、既定の (ホーム) ページが既に機能していることになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="918d6-710">実際には、新しい MVC アプリケーションを起動するときに表示される既定のページに似ています。</span><span class="sxs-lookup"><span data-stu-id="918d6-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="918d6-711">([クリックすると、フルサイズの画像が表示](overview/_static/image18.png)される)</span><span class="sxs-lookup"><span data-stu-id="918d6-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="918d6-712">プロジェクトテンプレートに対するこれらの変更の目的は、新しい Web アプリケーションの構築を開始する方法に関するガイダンスを提供することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="918d6-713">意味的に正しい、厳密な XHTML 1.0 準拠のマークアップ、および CSS を使用して指定されたレイアウトでは、テンプレートのページは ASP.NET 4 Web アプリケーションを構築するためのベストプラクティスを表します。</span><span class="sxs-lookup"><span data-stu-id="918d6-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="918d6-714">既定のページには、簡単にカスタマイズできる2列のレイアウトもあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="918d6-715">たとえば、新しい Web アプリケーションでは、一部の色を変更し、My ASP.NET アプリケーションロゴの代わりに会社のロゴを挿入するとします。</span><span class="sxs-lookup"><span data-stu-id="918d6-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="918d6-716">これを行うには、ロゴイメージ`Content`を格納するための新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="918d6-717">このページに画像を追加するには、次の`Site.Master`例のように、ファイルを開き、My ASP.NET Application のテキストが定義されている場所を見つけて、 *src*属性が新しいロゴイメージに設定されている*イメージ*要素で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="918d6-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="918d6-718">([クリックすると、フルサイズの画像が表示](overview/_static/image22.png)される)</span><span class="sxs-lookup"><span data-stu-id="918d6-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="918d6-719">その後、サイトの .css ファイルに移動し、CSS クラス定義を変更して、ページの背景色やヘッダーの背景色を変更できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="918d6-720">これらの変更の結果として、カスタマイズされたホームページをごくわずかな労力で表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="918d6-721">([クリックすると、フルサイズの画像が表示](overview/_static/image25.png)される)</span><span class="sxs-lookup"><span data-stu-id="918d6-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="918d6-722">CSS の機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-722">CSS Improvements</span></span>

<span data-ttu-id="918d6-723">ASP.NET 4 の主要な作業領域の1つは、最新の HTML 標準に準拠した HTML のレンダリングに役立ちました。</span><span class="sxs-lookup"><span data-stu-id="918d6-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="918d6-724">これには、ASP.NET Web サーバーコントロールが CSS スタイルを使用する方法の変更が含まれます。</span><span class="sxs-lookup"><span data-stu-id="918d6-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="918d6-725">レンダリングの互換性設定</span><span class="sxs-lookup"><span data-stu-id="918d6-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="918d6-726">既定では、Web アプリケーションまたは Web サイトが .NET Framework 4 を対象とする場合、 *pages*要素の*controlRenderingCompatibilityVersion*属性は "4.0" に設定されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="918d6-727">この要素はコンピューターレベル`Web.config`のファイルで定義され、既定ではすべての ASP.NET 4 アプリケーションに適用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="918d6-728">*ControlRenderingCompatibility*の値は文字列であり、今後のリリースで新しいバージョンの定義が可能になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="918d6-729">現在のリリースでは、このプロパティで次の値がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="918d6-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="918d6-730">"3.5".</span></span> <span data-ttu-id="918d6-731">この設定は、従来の表示とマークアップを示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="918d6-732">コントロールによってレンダリングされるマークアップは 100% 後方互換性があり、 *xhtmlConformance*プロパティの設定が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="918d6-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="918d6-733">"4.0".</span></span> <span data-ttu-id="918d6-734">プロパティにこの設定が含まれている場合、ASP.NET Web サーバーコントロールは次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="918d6-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="918d6-735">*XhtmlConformance*プロパティは、常に "Strict" として扱われます。</span><span class="sxs-lookup"><span data-stu-id="918d6-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="918d6-736">その結果、コントロールは XHTML 1.0 Strict マークアップをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="918d6-737">非入力コントロールを無効にすると、無効なスタイルが表示できなくなります。</span><span class="sxs-lookup"><span data-stu-id="918d6-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="918d6-738">非表示フィールドの周囲の*div*要素には、ユーザーが作成した CSS 規則に干渉しないようにスタイルが適用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="918d6-739">メニューコントロールは、意味的に正しい、アクセシビリティガイドラインに準拠しているマークアップをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="918d6-740">検証コントロールは、インラインスタイルをレンダリングしません。</span><span class="sxs-lookup"><span data-stu-id="918d6-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="918d6-741">以前に表示された border = "0" (ASP.NET *Table*コントロールから派生したコントロールと ASP.NET *Image*コントロール) がこの属性をレンダリングしないコントロール。</span><span class="sxs-lookup"><span data-stu-id="918d6-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="918d6-742">無効化 (コントロールを)</span><span class="sxs-lookup"><span data-stu-id="918d6-742">Disabling Controls</span></span>

<span data-ttu-id="918d6-743">ASP.NET 3.5 SP1 以前のバージョンでは、*有効になっている*プロパティが*false*に設定されているコントロールに対して、フレームワークによって、*無効になっ*た属性が HTML マークアップでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="918d6-744">ただし、HTML 4.01 仕様によれば、*入力*要素のみがこの属性を持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="918d6-745">ASP.NET 4 では、次の例に示すように、 *controlRenderingCompatibilityVersion*プロパティを "3.5" に設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-745">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="918d6-746">次のような*ラベル*コントロールのマークアップを作成すると、コントロールが無効になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="918d6-747">*ラベル*コントロールでは、次の HTML が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="918d6-748">ASP.NET 4 では、 *controlRenderingCompatibilityVersion*を "4.0" に設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-748">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* to "4.0".</span></span> <span data-ttu-id="918d6-749">その場合、コントロールの*Enabled*プロパティが*false*に設定されていると、*入力*要素を表示するコントロールのみが、*無効*な属性をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="918d6-750">代わりに HTML*入力*要素をレンダリングしないコントロールでは、コントロールの無効な検索を定義するために使用できる CSS クラスを参照する*クラス*属性がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="918d6-751">たとえば、前の例で示した*ラベル*コントロールでは、次のマークアップが生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="918d6-752">このコントロールに対して指定されたクラスの既定値は "aspNetDisabled" です。</span><span class="sxs-lookup"><span data-stu-id="918d6-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="918d6-753">ただし、 *WebControl*クラスの static *DisabledCssClass*静的プロパティを設定することによって、この既定値を変更できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="918d6-754">コントロールの開発者にとって、特定のコントロールに使用する動作は、 *SupportsDisabledAttribute*プロパティを使用して定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="918d6-755">非表示フィールドの周囲の div 要素の非表示</span><span class="sxs-lookup"><span data-stu-id="918d6-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="918d6-756">ASP.NET 2.0 以降のバージョンでは、XHTML 標準に準拠するために、 *div*要素内にシステム固有の非表示フィールド (ビューステート情報を格納するために使用される*非表示*の要素など) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="918d6-757">ただし、これにより、CSS ルールがページ上の*div*要素に影響を与える場合に問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="918d6-758">たとえば、非表示の*div*要素に関するページに1ピクセルの線が表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="918d6-759">ASP.NET 4 では、ASP.NET によって生成された隠しフィールドを囲む*div*要素は、次の例のように CSS クラス参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="918d6-760">その後、次の例のように、ASP.NET によって生成された*非表示*の要素にのみ適用される CSS クラスを定義できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="918d6-761">テンプレートコントロール用の外部テーブルのレンダリング</span><span class="sxs-lookup"><span data-stu-id="918d6-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="918d6-762">既定では、テンプレートをサポートする次の ASP.NET Web サーバーコントロールは、インラインスタイルを適用するために使用される外部テーブルに自動的にラップされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="918d6-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="918d6-763">*FormView*</span></span>
- <span data-ttu-id="918d6-764">*Login*</span><span class="sxs-lookup"><span data-stu-id="918d6-764">*Login*</span></span>
- <span data-ttu-id="918d6-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="918d6-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="918d6-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="918d6-766">*ChangePassword*</span></span>
- <span data-ttu-id="918d6-767">*画面*</span><span class="sxs-lookup"><span data-stu-id="918d6-767">*Wizard*</span></span>
- <span data-ttu-id="918d6-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="918d6-768">*CreateUserWizard*</span></span>

<span data-ttu-id="918d6-769">*Renderoutertable*という名前の新しいプロパティがこれらのコントロールに追加され、外部テーブルをマークアップから削除できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="918d6-770">たとえば、次の*FormView*コントロールの例を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="918d6-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="918d6-771">このマークアップは、HTML テーブルを含むページに次の出力をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="918d6-772">テーブルが表示されないようにするには、次の例に示すように、 *FormView*コントロールの*renderoutertable*プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="918d6-773">前の例では、 *table*、 *tr*、および*td*要素を使用せずに、次の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="918d6-774">Content</span><span class="sxs-lookup"><span data-stu-id="918d6-774">Content</span></span>

<span data-ttu-id="918d6-775">この拡張機能を使用すると、コントロールによって予期しないタグがレンダリングされないため、コントロールのコンテンツのスタイルを CSS で簡単に設定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="918d6-776">この変更により、Visual Studio 2010 デザイナーのオートフォーマット関数のサポートが無効になります。これは、オートフォーマットオプションによって生成されるスタイル属性をホストできる*table*要素がなくなったためです。</span><span class="sxs-lookup"><span data-stu-id="918d6-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="918d6-777">ListView コントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-777">ListView Control Enhancements</span></span>

<span data-ttu-id="918d6-778">*ListView*コントロールは、ASP.NET 4 で使いやすくなっています。</span><span class="sxs-lookup"><span data-stu-id="918d6-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="918d6-779">以前のバージョンのコントロールでは、既知の ID を持つサーバーコントロールを含むレイアウトテンプレートを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="918d6-780">次のマークアップは、ASP.NET 3.5 で*ListView*コントロールを使用する一般的な例を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="918d6-781">ASP.NET 4 では、 *ListView*コントロールにレイアウトテンプレートは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="918d6-782">前の例で示したマークアップは、次のマークアップに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="918d6-783">CheckBoxList と RadioButtonList のコントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="918d6-784">ASP.NET 3.5 では、次の2つの設定を使用して、 *CheckBoxList*と*RadioButtonList*のレイアウトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="918d6-785">*Flow*。</span><span class="sxs-lookup"><span data-stu-id="918d6-785">*Flow*.</span></span> <span data-ttu-id="918d6-786">コントロールは、コンテンツを格納するために*スパン*要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="918d6-787">*テーブル*。</span><span class="sxs-lookup"><span data-stu-id="918d6-787">*Table*.</span></span> <span data-ttu-id="918d6-788">コントロールは、その内容を格納する*table*要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="918d6-789">次の例では、これらの各コントロールのマークアップを示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="918d6-790">既定では、コントロールは次のような HTML を表示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="918d6-791">これらのコントロールには項目のリストが含まれているので、意味のある正しい HTML を表示するには、HTML リスト (*li*) 要素を使用して内容をレンダリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="918d6-792">これにより、ユーザーは補助的なテクノロジを使用して Web ページを読みやすくなり、CSS を使用してコントロールのスタイルを簡単にすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="918d6-793">ASP.NET 4 では、 *CheckBoxList*および*RadioButtonList*コントロールで、 *RepeatLayout*プロパティの次の新しい値がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="918d6-794">*OrderedList* –コンテンツは*ol*要素内の*li*要素としてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="918d6-795">*Unorderedlist レイアウト*–コンテンツは、 *ul*要素内の*li*要素としてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="918d6-796">これらの新しい値を使用する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="918d6-797">上記のマークアップでは、次の HTML が生成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="918d6-798">注*RepeatLayout*を*OrderedList*または*unorderedlist レイアウト*に設定すると、 *repeatdirection*プロパティを使用できなくなります。また、マークアップまたはコード内でプロパティが設定されている場合は、実行時に例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="918d6-799">これらのコントロールのビジュアルレイアウトは、代わりに CSS を使用して定義されているため、プロパティには値がありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="918d6-800">メニューコントロールの機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-800">Menu Control Improvements</span></span>

<span data-ttu-id="918d6-801">ASP.NET 4 より前の*メニュー*コントロールでは、一連の HTML テーブルが表示されていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="918d6-802">これにより、インラインプロパティの設定以外で CSS スタイルを適用することが難しくなりました。また、アクセシビリティ標準に準拠していませんでした。</span><span class="sxs-lookup"><span data-stu-id="918d6-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="918d6-803">ASP.NET 4 では、コントロールは、順序付けられていないリストとリストの要素で構成されるセマンティックマークアップを使用して HTML をレンダリングするようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="918d6-804">次の例は、*メニュー*コントロールの ASP.NET ページのマークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="918d6-805">ページがレンダリングされると、コントロールは次の HTML を生成します (わかりやすくするために*onclick*コードは省略されています)。</span><span class="sxs-lookup"><span data-stu-id="918d6-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="918d6-806">レンダリングの機能強化に加えて、フォーカス管理を使用してメニューのキーボードナビゲーションが改善されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="918d6-807">*メニュー*コントロールがフォーカスを取得すると、方向キーを使用して要素を移動できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="918d6-808">また、*メニュー*コントロールは、アクセシビリティを向上させるためにメニュー[の](http://www.w3.org/TR/wai-aria-practices/#menu "aria ガイドライン")を使用して、アクセス可能なリッチインターネットアプリケーション (ARIA) ロールおよび属性をアタッチするようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="918d6-809">メニューコントロールのスタイルは、表示されている HTML 要素を含む行ではなく、ページの上部にあるスタイルブロックで表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="918d6-810">コントロールのスタイルを完全に制御する場合は、新しい*Includeスタイルブロック*プロパティを*false*に設定できます。この場合、スタイルブロックは出力されません。</span><span class="sxs-lookup"><span data-stu-id="918d6-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="918d6-811">このプロパティを使用する方法の1つは、Visual Studio デザイナーのオートフォーマット機能を使用してメニューの外観を設定することです。</span><span class="sxs-lookup"><span data-stu-id="918d6-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="918d6-812">その後、ページを実行してページソースを開き、レンダリングされたスタイルブロックを外部 CSS ファイルにコピーできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="918d6-813">Visual Studio で、スタイルを元に戻し、 *Includeスタイルブロック*を*false*に設定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="918d6-814">その結果、メニューの外観は、外部スタイルシートのスタイルを使用して定義されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="918d6-815">ウィザードと CreateUserWizard のコントロール</span><span class="sxs-lookup"><span data-stu-id="918d6-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="918d6-816">ASP.NET *Wizard*および*CreateUserWizard*コントロールは、レンダリングする HTML を定義できるテンプレートをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="918d6-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="918d6-817">(*CreateUserWizard*は*ウィザード*から派生します。)完全にテンプレート化された*CreateUserWizard*コントロールのマークアップの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="918d6-818">コントロールは、次のような HTML をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="918d6-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="918d6-819">ASP.NET 3.5 SP1 では、テンプレートの内容を変更することはできますが、*ウィザード*コントロールの出力の制御は制限されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="918d6-820">ASP.NET 4 では、 *LayoutTemplate*テンプレートを作成し、(予約された名前を使用して)*プレースホルダー*コントロールを挿入して、*ウィザードコントロール*のレンダリング方法を指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="918d6-821">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="918d6-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="918d6-822">この例では、 *LayoutTemplate*要素に次の名前付きプレースホルダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="918d6-823">*Headerplaceholder* –実行時に、 *system.windows.controls.headereditemscontrol.headertemplate*要素の内容に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="918d6-824">*Sidebarplaceholder* –実行時に、これは*sidebarplaceholder*要素の内容に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="918d6-825">*Wizardstepplaceholder* –実行時に、これは*wizardstepplaceholder*要素の内容に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="918d6-826">*Navigationplaceholder* –実行時に、定義したナビゲーションテンプレートに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="918d6-827">プレースホルダーを使用する例のマークアップでは、次の HTML が表示されます (テンプレートで実際に定義されていないコンテンツは含まれません)。</span><span class="sxs-lookup"><span data-stu-id="918d6-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="918d6-828">現在ユーザー定義されていない HTML は*span*要素だけです。</span><span class="sxs-lookup"><span data-stu-id="918d6-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="918d6-829">(今後のリリースでは、 *span*要素がレンダリングされないことを想定しています)。これにより、*ウィザード*コントロールによって生成されるすべてのコンテンツを完全に制御できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="918d6-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="918d6-830">ASP.NET MVC</span></span>

<span data-ttu-id="918d6-831">ASP.NET MVC は、3.5 年 3 2009 月に ASP.NET SP1 のアドオンフレームワークとして導入されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="918d6-832">Visual Studio 2010 には、新しい機能を含む ASP.NET MVC 2 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="918d6-833">区分のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-833">Areas Support</span></span>

<span data-ttu-id="918d6-834">区分を使用すると、他のセクションからの相対分離で、コントローラーとビューを大規模なアプリケーションのセクションにグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="918d6-835">各領域は、メインアプリケーションで参照できる個別の ASP.NET MVC プロジェクトとして実装できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="918d6-836">これにより、大規模なアプリケーションを構築する際の複雑さを管理し、複数のチームが1つのアプリケーションで共同作業を簡単に行えるようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="918d6-837">データ注釈属性の検証のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="918d6-838">*Dataannotations*属性を使用すると、メタデータ属性を使用して、検証ロジックをモデルにアタッチできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="918d6-839">*Dataannotations*属性は、ASP.NET 3.5 SP1 の ASP.NET 動的データで導入されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="918d6-840">これらの属性は、既定のモデルバインダーに統合されており、ユーザー入力を検証するためのメタデータドリブンの手段を提供しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="918d6-841">テンプレートヘルパー</span><span class="sxs-lookup"><span data-stu-id="918d6-841">Templated Helpers</span></span>

<span data-ttu-id="918d6-842">テンプレートヘルパーを使用すると、編集および表示テンプレートをデータ型に自動的に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="918d6-843">たとえば、テンプレートヘルパーを使用して、日付の選択 UI 要素が*システムの DateTime*値に対して自動的に表示されるように指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="918d6-844">これは、ASP.NET 動的データのフィールドテンプレートに似ています。</span><span class="sxs-lookup"><span data-stu-id="918d6-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="918d6-845">ヘルパーメソッドの*html. editorfor*および*html. displayfor*は、標準データ型を表示するための組み込みのサポートと、複数のプロパティを持つ複雑なオブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="918d6-846">また、 *DisplayName*や*ScaffoldColumn*などのデータ注釈属性を*ビューモデル*オブジェクトに適用できるようにすることで、レンダリングをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="918d6-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="918d6-847">多くの場合、UI ヘルパーからの出力をさらにカスタマイズし、生成される内容を完全に制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="918d6-848">ヘルパーメソッドの*html. Editorfor* *.html*は、テンプレート機構を使用してこれをサポートしています。これにより、表示される出力をオーバーライドおよび制御できる外部テンプレートを定義できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="918d6-849">テンプレートは、クラスごとに個別にレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="918d6-850">動的データ</span><span class="sxs-lookup"><span data-stu-id="918d6-850">Dynamic Data</span></span>

<span data-ttu-id="918d6-851">動的データは、2008 .NET Framework 3.5 SP1 リリースで導入されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="918d6-852">この機能には、次のようなデータドリブンアプリケーションを作成するための多くの拡張機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="918d6-853">データドリブンの Web サイトをすばやく構築するための RAD エクスペリエンス。</span><span class="sxs-lookup"><span data-stu-id="918d6-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="918d6-854">データモデルで定義されている制約に基づく自動検証。</span><span class="sxs-lookup"><span data-stu-id="918d6-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="918d6-855">動的データプロジェクトの一部であるフィールドテンプレートを使用して、 *GridView*コントロールおよび*DetailsView*コントロールのフィールドに対して生成されたマークアップを簡単に変更する機能。</span><span class="sxs-lookup"><span data-stu-id="918d6-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="918d6-856">注詳細については、MSDN ライブラリの[動的データのドキュメント](https://msdn.microsoft.com/library/cc488545.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="918d6-857">ASP.NET 4 では、開発者がデータ主導の Web サイトをすばやく構築できるように、動的データが強化されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="918d6-858">既存のプロジェクトの動的データを有効にする</span><span class="sxs-lookup"><span data-stu-id="918d6-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="918d6-859">.NET Framework 3.5 SP1 に同梱されている動的データ機能には、次のような新機能があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="918d6-860">フィールドテンプレート–データバインドコントロール用のデータ型ベースのテンプレートを提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="918d6-861">フィールドテンプレートを使用すると、各フィールドのテンプレートフィールドを使用する場合よりも、データコントロールの外観を簡単にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="918d6-862">検証–動的データを使用すると、データクラスの属性を使用して、必須フィールド、範囲チェック、型チェック、正規表現を使用したパターン一致、カスタム検証などの一般的なシナリオの検証を指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="918d6-863">検証は、データコントロールによって適用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="918d6-864">ただし、これらの機能には次の要件があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="918d6-865">データアクセス層は Entity Framework または LINQ to SQL に基づいている必要がありました。</span><span class="sxs-lookup"><span data-stu-id="918d6-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="918d6-866">これらの機能でサポートされているデータソースコントロールは、 *EntityDataSource*コントロールまたは*LinqDataSource*コントロールのみです。</span><span class="sxs-lookup"><span data-stu-id="918d6-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="918d6-867">機能には、動的データまたは動的データエンティティテンプレートを使用して作成された Web プロジェクトが必要でした。この機能をサポートするために必要なすべてのファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="918d6-868">ASP.NET 4 での動的データサポートの主な目的は、ASP.NET アプリケーションに対して動的データの新しい機能を有効にすることです。</span><span class="sxs-lookup"><span data-stu-id="918d6-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="918d6-869">次の例は、既存のページで動的データ機能を利用できるコントロールのマークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="918d6-870">ページのコードでは、これらのコントロールの動的データサポートを有効にするために、次のコードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="918d6-871">*GridView*コントロールが編集モードの場合、動的データ入力されたデータが適切な形式であるかどうかが自動的に検証されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="918d6-872">そうでない場合は、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="918d6-873">この機能には、挿入モードの既定値を指定できるなど、他の利点もあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="918d6-874">動的データない場合は、フィールドの既定値を実装するには、イベントにアタッチし、( *FindControl*を使用して) コントロールを見つけて、その値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="918d6-875">ASP.NET 4 では、 *EnableDynamicData*呼び出しで、次の例に示すように、オブジェクトの任意のフィールドに既定値を渡すことができる2番目のパラメーターがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="918d6-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="918d6-876">宣言型の DynamicDataManager コントロール構文</span><span class="sxs-lookup"><span data-stu-id="918d6-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="918d6-877">*DynamicDataManager*コントロールが拡張され、コードだけではなく、ASP.NET のほとんどのコントロールと同様に、宣言によって構成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="918d6-878">*DynamicDataManager*コントロールのマークアップは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="918d6-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="918d6-879">このマークアップにより、 *DynamicDataManager*コントロールの*DataControls*セクションで参照されている GridView1 コントロールの動的データ動作が有効になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="918d6-880">エンティティテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-880">Entity Templates</span></span>

<span data-ttu-id="918d6-881">エンティティテンプレートを使用すると、カスタムページを作成しなくても、データのレイアウトをカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="918d6-882">ページテンプレートは、 *FormView*コントロール (以前のバージョンの動的データのページテンプレートで使用される*DetailsView*コントロールではなく) と、エンティティテンプレートをレンダリングするための*DynamicEntity*コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="918d6-883">これにより、動的データによって表示されるマークアップをより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="918d6-884">次の一覧は、エンティティテンプレートを含む新しいプロジェクトディレクトリレイアウトを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="918d6-885">ディレクトリ`EntityTemplate`には、データモデルオブジェクトを表示するためのテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="918d6-886">既定では、オブジェクトは`Default.ascx`テンプレートを使用してレンダリングされます。これは、ASP.NET 3.5 SP1 の動的データによって使用される*DetailsView*コントロールによって作成されたマークアップと同じように表示されるマークアップを提供します。</span><span class="sxs-lookup"><span data-stu-id="918d6-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="918d6-887">次の例は、 `Default.ascx`コントロールのマークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="918d6-888">既定のテンプレートを編集して、サイト全体のルックアンドフィールを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="918d6-889">表示、編集、および挿入操作のためのテンプレートがあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="918d6-890">オブジェクトの外観を変更するために、データオブジェクトの名前に基づいて新しいテンプレートを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="918d6-891">たとえば、次のテンプレートを追加できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="918d6-892">テンプレートには、次のマークアップが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="918d6-893">新しいエンティティテンプレートは、新しい*DynamicEntity*コントロールを使用してページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="918d6-894">実行時に、このコントロールはエンティティテンプレートの内容に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="918d6-895">次のマークアップは 、エンティティテンプレートを`Detail.aspx`使用するページテンプレートの FormView コントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="918d6-896">マークアップの*DynamicEntity*要素に注目してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="918d6-897">Url と電子メールアドレスの新しいフィールドテンプレート</span><span class="sxs-lookup"><span data-stu-id="918d6-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="918d6-898">ASP.NET 4 では、とという2つの`EmailAddress.ascx`新しい`Url.ascx`組み込みフィールドテンプレートが導入されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="918d6-899">これらのテンプレートは、 *DataType*属性を使用して*EmailAddress*または*Url*としてマークされているフィールドに使用されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="918d6-900">*EmailAddress*オブジェクトの場合、フィールドは*mailto:* プロトコルを使用して作成されるハイパーリンクとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="918d6-901">ユーザーがリンクをクリックすると、ユーザーの電子メールクライアントが開き、スケルトンメッセージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="918d6-902">*Url*として型指定されたオブジェクトは、通常のハイパーリンクとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="918d6-903">次の例は、フィールドをマークする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="918d6-904">DynamicHyperLink コントロールを使用したリンクの作成</span><span class="sxs-lookup"><span data-stu-id="918d6-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="918d6-905">動的データでは、.NET Framework 3.5 SP1 で追加された新しいルーティング機能を使用して、エンドユーザーが Web サイトにアクセスしたときに表示される Url を制御します。</span><span class="sxs-lookup"><span data-stu-id="918d6-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="918d6-906">新しい*DynamicHyperLink*コントロールを使用すると、動的データサイト内のページへのリンクを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="918d6-907">次の例は、 *DynamicHyperLink*コントロールの使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="918d6-908">このマークアップは、 `Products` `Global.asax`ファイルで定義されているルートに基づいて、テーブルのリストページを指すリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="918d6-909">コントロールは、動的データページの基になっている既定のテーブル名を自動的に使用します。</span><span class="sxs-lookup"><span data-stu-id="918d6-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="918d6-910">データモデルでの継承のサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="918d6-911">Entity Framework と LINQ to SQL はどちらも、データモデルの継承をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="918d6-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="918d6-912">この例としては、 `InsurancePolicy`テーブルがあるデータベースが挙げられます。</span><span class="sxs-lookup"><span data-stu-id="918d6-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="918d6-913">また、と同じ`CarPolicy`フィールド`HousePolicy` `InsurancePolicy`を持ち、さらにフィールドを追加するテーブルが含まれている場合もあります。</span><span class="sxs-lookup"><span data-stu-id="918d6-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="918d6-914">動的データは、データモデル内の継承されたオブジェクトを理解し、継承されたテーブルのスキャフォールディングをサポートするように変更されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="918d6-915">多対多リレーションシップのサポート (Entity Framework のみ)</span><span class="sxs-lookup"><span data-stu-id="918d6-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="918d6-916">Entity Framework には、テーブル間の多対多リレーションシップの豊富なサポートがあります。これは、*エンティティ*オブジェクトのコレクションとしてリレーションシップを公開することによって実装されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="918d6-917">多`ManyToMany.ascx`対`ManyToMany_Edit.ascx`多リレーションシップに関係するデータを表示および編集するためのサポートを提供するために、新しいテンプレートとフィールドテンプレートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="918d6-918">表示およびサポートの列挙型を制御する新しい属性</span><span class="sxs-lookup"><span data-stu-id="918d6-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="918d6-919">*Displayattribute*が追加され、フィールドの表示方法をさらに制御できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="918d6-920">以前のバージョンの動的データの*DisplayName*属性では、フィールドのキャプションとして使用される名前を変更できました。</span><span class="sxs-lookup"><span data-stu-id="918d6-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="918d6-921">新しい*Displayattribute*クラスを使用すると、フィールドを表示する順序や、フィールドをフィルターとして使用するかどうかなど、フィールドを表示するためのオプションをさらに指定できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="918d6-922">また、この属性は、 *GridView*コントロールのラベル、 *DetailsView*コントロールで使用される名前、フィールドのヘルプテキスト、フィールドに使用される透かし (フィールドがテキスト入力を受け入れる場合) に使用される名前を個別に制御します。</span><span class="sxs-lookup"><span data-stu-id="918d6-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="918d6-923">*EnumDataTypeAttribute*クラスが追加され、フィールドを列挙型にマップできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="918d6-924">この属性をフィールドに適用する場合は、列挙型を指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="918d6-925">動的データは、新しい`Enumeration.ascx`フィールドテンプレートを使用して、列挙値を表示および編集するための UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="918d6-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="918d6-926">このテンプレートでは、データベースの値が列挙体の名前にマップされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="918d6-927">フィルターの強化されたサポート</span><span class="sxs-lookup"><span data-stu-id="918d6-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="918d6-928">動的データ1.0 には、ブール型の列と外部キー列の組み込みフィルターが付属しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="918d6-929">フィルターでは、表示されているかどうかを指定することはできませんでした。</span><span class="sxs-lookup"><span data-stu-id="918d6-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="918d6-930">新しい*displayattribute*属性では、列をフィルターとして表示するかどうかを制御できるようにすることで、これらの問題の両方に対処します。</span><span class="sxs-lookup"><span data-stu-id="918d6-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="918d6-931">さらに拡張機能として、Web フォームの新しい(#0.2__QueryExtender "queryextender")機能[を使用するために、]フィルター処理のサポートが再作成されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="918d6-932">これにより、フィルターを作成する際に、フィルターを使用するデータソースコントロールに関する知識を必要としません。</span><span class="sxs-lookup"><span data-stu-id="918d6-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="918d6-933">これらの拡張機能と共に、フィルターもテンプレートコントロールに設定されています。これにより、新しいフィルターを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="918d6-934">最後に、前に説明した*Displayattribute*クラスを使用すると、既定のフィルターを上書きできます。これと同じように、 *UIHint*では、列の既定のフィールドテンプレートをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="918d6-935">Visual Studio 2010 の Web 開発の機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="918d6-936">Visual Studio 2010 での Web 開発が強化され、CSS 互換性が向上し、HTML および ASP.NET マークアップスニペットと新しい動的 IntelliSense JavaScript による生産性が向上しました。</span><span class="sxs-lookup"><span data-stu-id="918d6-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="918d6-937">CSS 互換性の向上</span><span class="sxs-lookup"><span data-stu-id="918d6-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="918d6-938">Visual Studio 2010 の Visual Web Developer designer が更新され、CSS 2.1 標準準拠が向上しました。</span><span class="sxs-lookup"><span data-stu-id="918d6-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="918d6-939">デザイナーでは、HTML ソースの整合性が維持され、以前のバージョンの Visual Studio よりも堅牢になります。</span><span class="sxs-lookup"><span data-stu-id="918d6-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="918d6-940">内部的には、レンダリング、レイアウト、および保守性における将来の機能強化を向上させるために、アーキテクチャが改善されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="918d6-941">HTML および JavaScript のスニペット</span><span class="sxs-lookup"><span data-stu-id="918d6-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="918d6-942">HTML エディターでは、IntelliSense によってタグ名がオートコンプリートされます。</span><span class="sxs-lookup"><span data-stu-id="918d6-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="918d6-943">IntelliSense のスニペット機能は、タグ全体を自動的に補完します。</span><span class="sxs-lookup"><span data-stu-id="918d6-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="918d6-944">Visual Studio 2010 では、JavaScript で IntelliSense スニペットがサポートさC#れており、以前のバージョンの visual studio でサポートされていた Visual Basic とともにサポートされていました。</span><span class="sxs-lookup"><span data-stu-id="918d6-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="918d6-945">Visual Studio 2010 には、必要な属性 (runat = "server" など) とタグに固有の共通属性 ( *ID*、 *DataSourceID* *など) を含む、一般的な ASP.NET と HTML タグをオートコンプリートするのに役立つ、200を超えるスニペットが含まれています。ControlToValidate*、*テキスト*)。</span><span class="sxs-lookup"><span data-stu-id="918d6-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="918d6-946">追加のスニペットをダウンロードすることも、ユーザー自身またはチームが一般的なタスクに使用するマークアップのブロックをカプセル化する独自のスニペットを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="918d6-947">JavaScript IntelliSense の機能強化</span><span class="sxs-lookup"><span data-stu-id="918d6-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="918d6-948">Visual 2010 では、より充実した編集エクスペリエンスを提供するために、JavaScript IntelliSense が再設計されました。</span><span class="sxs-lookup"><span data-stu-id="918d6-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="918d6-949">IntelliSense は、 *Registernamespace*などのメソッドによって動的に生成されたオブジェクト、および他の JavaScript フレームワークで使用される同様の手法を認識するようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="918d6-950">スクリプトの大規模なライブラリを分析し、処理の遅延がほとんどまたはまったくない IntelliSense を表示するようにパフォーマンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="918d6-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="918d6-951">ほとんどすべてのサードパーティライブラリをサポートし、さまざまなコーディングスタイルをサポートするために、互換性が飛躍的に向上しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="918d6-952">ドキュメントコメントは入力時に解析されるようになり、IntelliSense によってすぐに利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="918d6-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="918d6-953">Visual Studio 2010 を使用した Web アプリケーションのデプロイ</span><span class="sxs-lookup"><span data-stu-id="918d6-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="918d6-954">ASP.NET 開発者は、Web アプリケーションをデプロイするときに、次のような問題が発生していることがよくわかります。</span><span class="sxs-lookup"><span data-stu-id="918d6-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="918d6-955">共有ホスティングサイトに配置するには、FTP などのテクノロジが必要ですが、これは低速になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="918d6-956">また、データベースを構成するための SQL スクリプトの実行などのタスクを手動で実行する必要があります。また、仮想ディレクトリフォルダーをアプリケーションとして構成するなど、IIS 設定を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="918d6-957">エンタープライズ環境では、管理者は Web アプリケーションファイルの展開に加えて、ASP.NET 構成ファイルと IIS 設定を頻繁に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="918d6-958">データベース管理者は、アプリケーションデータベースを実行するために、一連の SQL スクリプトを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="918d6-959">このようなインストールには手間がかかり、多くの場合、完了までに数時間かかるため、慎重に文書化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="918d6-960">Visual Studio 2010 には、これらの問題に対処し、Web アプリケーションをシームレスにデプロイできるテクノロジが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="918d6-961">これらのテクノロジの1つは、IIS Web 配置ツール (Msdeploy.exe) です。</span><span class="sxs-lookup"><span data-stu-id="918d6-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="918d6-962">Visual Studio 2010 の Web 配置機能には、次の主な領域があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="918d6-963">Web パッケージ</span><span class="sxs-lookup"><span data-stu-id="918d6-963">Web packaging</span></span>
- <span data-ttu-id="918d6-964">Web.config 変換</span><span class="sxs-lookup"><span data-stu-id="918d6-964">Web.config transformation</span></span>
- <span data-ttu-id="918d6-965">データベースの配置</span><span class="sxs-lookup"><span data-stu-id="918d6-965">Database deployment</span></span>
- <span data-ttu-id="918d6-966">ワンクリックによる Web アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="918d6-966">One-click publish for Web applications</span></span>

<span data-ttu-id="918d6-967">以下のセクションでは、これらの機能について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="918d6-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="918d6-968">Web パッケージ</span><span class="sxs-lookup"><span data-stu-id="918d6-968">Web Packaging</span></span>

<span data-ttu-id="918d6-969">Visual Studio 2010 では、Msdeploy.exe ツールを使用して、アプリケーションの圧縮 (.zip) ファイルを作成します。このファイルを*Web パッケージ*と呼びます。</span><span class="sxs-lookup"><span data-stu-id="918d6-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="918d6-970">パッケージファイルには、アプリケーションに関するメタデータに加え、次のコンテンツが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="918d6-971">IIS 設定。アプリケーションプールの設定、エラーページの設定などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="918d6-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="918d6-972">実際の Web コンテンツ。 Web ページ、ユーザーコントロール、静的コンテンツ (画像と HTML ファイル) などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="918d6-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="918d6-973">データベーススキーマとデータを SQL Server します。</span><span class="sxs-lookup"><span data-stu-id="918d6-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="918d6-974">セキュリティ証明書、GAC にインストールするコンポーネント、レジストリ設定など。</span><span class="sxs-lookup"><span data-stu-id="918d6-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="918d6-975">Web パッケージは任意のサーバーにコピーし、IIS マネージャーを使用して手動でインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="918d6-976">また、自動展開の場合は、コマンドラインコマンドまたはデプロイ Api を使用してパッケージをインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="918d6-977">Visual Studio 2010 には、Web パッケージを作成するための組み込みの MSBuild タスクとターゲットが用意されています。</span><span class="sxs-lookup"><span data-stu-id="918d6-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="918d6-978">詳細については、MSDN Web サイトの「 [ASP.NET Web Application Project Deployment の概要](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)」および「Vishal Joshi のブログで[web パッケージを作成する必要がある 10 + 20 の理由](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="918d6-979">Web.config 変換</span><span class="sxs-lookup"><span data-stu-id="918d6-979">Web.config Transformation</span></span>

<span data-ttu-id="918d6-980">Web アプリケーションの配置の場合、Visual Studio 2010 では[XML ドキュメント変換 (xdt)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)が導入されています`Web.config` 。これは、開発設定から運用設定にファイルを変換できる機能です。</span><span class="sxs-lookup"><span data-stu-id="918d6-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="918d6-981">変換の設定は、、 `web.debug.config` `web.release.config`などという名前の変換ファイルで指定されます。</span><span class="sxs-lookup"><span data-stu-id="918d6-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="918d6-982">(これらのファイルの名前は MSBuild の構成と一致します)。変換ファイルには、配置`Web.config`されたファイルに対して行う必要がある変更のみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="918d6-983">変更は、単純な構文を使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="918d6-984">次の例は、リリース構成の`web.release.config`配置用に生成される可能性があるファイルの一部を示しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="918d6-985">この例の Replace キーワードは、デプロイ時に、 `Web.config`ファイル内の connectionString ノードが、例に示されている値に置き換えられることを指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="918d6-986">詳細については、MSDN <a id="0.2_a"></a> web サイトおよび[web デプロイの「web[アプリケーションプロジェクトの配置の web.config 変換構文](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)」を参照してください。Vishal Joshi のブログ](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)の web.config 変換。</span><span class="sxs-lookup"><span data-stu-id="918d6-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="918d6-987">データベースの配置</span><span class="sxs-lookup"><span data-stu-id="918d6-987">Database Deployment</span></span>

<span data-ttu-id="918d6-988">Visual Studio 2010 配置パッケージには SQL Server データベースへの依存関係を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="918d6-989">パッケージ定義の一部として、ソースデータベースの接続文字列を指定します。</span><span class="sxs-lookup"><span data-stu-id="918d6-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="918d6-990">Web パッケージを作成すると、Visual Studio 2010 はデータベーススキーマの SQL スクリプトと、必要に応じてデータを作成してから、パッケージに追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="918d6-991">また、カスタムの SQL スクリプトを提供し、サーバーで実行する順序を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="918d6-992">デプロイ時には、対象サーバーに適した接続文字列を指定します。配置プロセスでは、この接続文字列を使用して、データベーススキーマを作成するスクリプトを実行し、データを追加します。</span><span class="sxs-lookup"><span data-stu-id="918d6-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="918d6-993">また、ワンクリック発行を使用して、アプリケーションがリモート共有ホスティングサイトに発行されたときに、データベースを直接発行するように配置を構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="918d6-994">詳細については、「[方法 :MSDN web サイトの「web アプリケーションプロジェクト](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)を使用してデータベースを配置する」および「Vishal Joshi のブログで[VS 2010 を使用](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)してデータベースを配置する」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="918d6-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="918d6-995">ワンクリックによる Web アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="918d6-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="918d6-996">また、Visual Studio 2010 では、IIS リモート管理サービスを使用して、Web アプリケーションをリモートサーバーに発行することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="918d6-997">ホスティングアカウントまたはテストサーバーまたはステージングサーバーの発行プロファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="918d6-998">各プロファイルは、適切な資格情報を安全に保存できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="918d6-999">その後、Web ワンクリック発行ツールバーを使用して、1回のクリックで任意の対象サーバーに配置できます。</span><span class="sxs-lookup"><span data-stu-id="918d6-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="918d6-1000">Visual Studio 2010 では、MSBuild コマンドラインを使用して発行することもできます。</span><span class="sxs-lookup"><span data-stu-id="918d6-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="918d6-1001">これにより、チームビルド環境を構成して、継続的インテグレーションモデルに発行を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="918d6-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="918d6-1002">詳細については、「[方法 :ワンクリック発行を使用して web アプリケーションプロジェクトを配置](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)し、MSDN Web サイトと web 1 で Web 配置して、Vishal Joshi のブログで[[publish with VS 2010] をクリック](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)します。</span><span class="sxs-lookup"><span data-stu-id="918d6-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="918d6-1003">Visual Studio 2010 で Web アプリケーションのデプロイに関するビデオプレゼンテーションを表示するには、Vishal Joshi のブログの[Web Developer preview の VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="918d6-1004">リソース</span><span class="sxs-lookup"><span data-stu-id="918d6-1004">Resources</span></span>

<span data-ttu-id="918d6-1005">次の Web サイトでは、ASP.NET 4 および Visual Studio 2010 に関する追加情報を提供しています。</span><span class="sxs-lookup"><span data-stu-id="918d6-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="918d6-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN Web サイトの ASP.NET 4 に関する公式ドキュメント。</span><span class="sxs-lookup"><span data-stu-id="918d6-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="918d6-1007">[https://www.asp.net/](https://www.asp.net/)— ASP.NET チーム独自の Web サイト。</span><span class="sxs-lookup"><span data-stu-id="918d6-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="918d6-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)および[ASP.NET 動的データコンテンツマップ](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-ASP.NET チームサイトのオンラインリソースと ASP.NET 動的データの公式ドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="918d6-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="918d6-1009">[https://www.asp.net/ajax/](../../ajax/index.md)— ASP.NET Ajax 開発用のメイン Web リソース。</span><span class="sxs-lookup"><span data-stu-id="918d6-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="918d6-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/)-Visual Web Developer チームのブログ。 Visual Studio 2010 の機能に関する情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="918d6-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="918d6-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET のプレビューリリースのメイン Web リソースです。</span><span class="sxs-lookup"><span data-stu-id="918d6-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="918d6-1012">免責情報</span><span class="sxs-lookup"><span data-stu-id="918d6-1012">Disclaimer</span></span>

<span data-ttu-id="918d6-1013">このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="918d6-1014">このドキュメントに記載されている情報は、説明されている問題に関する Microsoft Corporation の発行日時点における最新の見解を表します。</span><span class="sxs-lookup"><span data-stu-id="918d6-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="918d6-1015">マイクロソフトは変化する市場の状況に対応する必要があるため、本ドキュメントをマイクロソフトの確約と解釈することはできず、発行日以降は、提示されている情報の正確性を保証できません。</span><span class="sxs-lookup"><span data-stu-id="918d6-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="918d6-1016">このホワイト ペーパーは、情報提供のみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="918d6-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="918d6-1017">マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。</span><span class="sxs-lookup"><span data-stu-id="918d6-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="918d6-1018">お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。</span><span class="sxs-lookup"><span data-stu-id="918d6-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="918d6-1019">このドキュメントのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。ただしこれは、著作権法上のお客様の権利を制限するものではありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="918d6-1020">マイクロソフトは、このドキュメントに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="918d6-1021">別途マイクロソフトのライセンス契約上に明示の規定のない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。</span><span class="sxs-lookup"><span data-stu-id="918d6-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="918d6-1022">特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人名、場所、およびイベントは架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールとは一切関係ありません。アドレス、ロゴ、人物、場所、またはイベントが想定されているか、または推測する必要があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="918d6-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="918d6-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="918d6-1024">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="918d6-1024">All rights reserved.</span></span>

<span data-ttu-id="918d6-1025">Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。</span><span class="sxs-lookup"><span data-stu-id="918d6-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="918d6-1026">本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。</span><span class="sxs-lookup"><span data-stu-id="918d6-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
