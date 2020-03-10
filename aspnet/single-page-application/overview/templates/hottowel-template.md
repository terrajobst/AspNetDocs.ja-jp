---
uid: single-page-application/overview/templates/hottowel-template
title: ホットタオルテンプレート |Microsoft Docs
author: madskristensen
description: ホットタオルテンプレート
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467140"
---
# <a name="hot-towel-template"></a><span data-ttu-id="c6399-103">Hot Towel テンプレート</span><span class="sxs-lookup"><span data-stu-id="c6399-103">Hot Towel template</span></span>

<span data-ttu-id="c6399-104">[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="c6399-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="c6399-105">ホットタオル MVC テンプレートは John Papa によって作成されます。</span><span class="sxs-lookup"><span data-stu-id="c6399-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="c6399-106">ダウンロードするバージョンの選択:</span><span class="sxs-lookup"><span data-stu-id="c6399-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="c6399-107">Visual Studio 2012 用のホットペーパー MVC テンプレート</span><span class="sxs-lookup"><span data-stu-id="c6399-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="c6399-108">Visual Studio 2013 用のホットタオル MVC テンプレート</span><span class="sxs-lookup"><span data-stu-id="c6399-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="c6399-109">ホットタオル: SPA にアクセスしないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6399-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="c6399-110">SPA を構築するが、どこから開始するかを決定できない場合は、</span><span class="sxs-lookup"><span data-stu-id="c6399-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="c6399-111">ホットタオルを使用して、数秒で SPA とすべてのツールを構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6399-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="c6399-112">ホットタオルでは、ASP.NET を使用してシングルページアプリケーション (SPA) を構築するための開始点として優れています。</span><span class="sxs-lookup"><span data-stu-id="c6399-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="c6399-113">すぐに使えるように、コードのモジュール形式の構造、ビューのナビゲーション、データバインディング、豊富なデータ管理、シンプルで洗練されたスタイル設定を提供しています。</span><span class="sxs-lookup"><span data-stu-id="c6399-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="c6399-114">ホットタオルは SPA を構築するために必要なすべての機能を備えているので、アプリに集中することができます。</span><span class="sxs-lookup"><span data-stu-id="c6399-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="c6399-115">詳細については[、John Papa のビデオ、チュートリアル、Pluralsight コース](http://johnpapa.net/spa?vsix)からの SPA の構築に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c6399-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="c6399-116">アプリケーション構造</span><span class="sxs-lookup"><span data-stu-id="c6399-116">Application Structure</span></span>

<span data-ttu-id="c6399-117">ホットタオル SPA には、アプリケーションを定義する JavaScript および HTML ファイルを含むアプリフォルダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="c6399-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="c6399-118">アプリフォルダー内:</span><span class="sxs-lookup"><span data-stu-id="c6399-118">Inside the App folder:</span></span>

- <span data-ttu-id="c6399-119">durandal</span><span class="sxs-lookup"><span data-stu-id="c6399-119">durandal</span></span>
- <span data-ttu-id="c6399-120">services</span><span class="sxs-lookup"><span data-stu-id="c6399-120">services</span></span>
- <span data-ttu-id="c6399-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="c6399-121">viewmodels</span></span>
- <span data-ttu-id="c6399-122">views</span><span class="sxs-lookup"><span data-stu-id="c6399-122">views</span></span>

<span data-ttu-id="c6399-123">アプリフォルダーには、モジュールのコレクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="c6399-124">これらのモジュールは、機能をカプセル化し、他のモジュールとの依存関係を宣言します。</span><span class="sxs-lookup"><span data-stu-id="c6399-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="c6399-125">Views フォルダーには、アプリケーションの HTML が含まれています。また、viewmodel フォルダーには、ビューのプレゼンテーションロジック (共通 MVVM パターン) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="c6399-126">Services フォルダーは、アプリケーションで必要になる可能性のある一般的なサービス (HTTP データの取得やローカルストレージの相互作用など) を格納するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="c6399-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="c6399-127">複数の viewmodel では、サービスモジュールのコードを再利用するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="c6399-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="c6399-128">ASP.NET MVC サーバー側のアプリケーション構造</span><span class="sxs-lookup"><span data-stu-id="c6399-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="c6399-129">ホットタオルは、使い慣れた強力な ASP.NET MVC 構造を基盤としています。</span><span class="sxs-lookup"><span data-stu-id="c6399-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="c6399-130">アプリ\_開始</span><span class="sxs-lookup"><span data-stu-id="c6399-130">App\_Start</span></span>
- <span data-ttu-id="c6399-131">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="c6399-131">Content</span></span>
- <span data-ttu-id="c6399-132">コントローラー</span><span class="sxs-lookup"><span data-stu-id="c6399-132">Controllers</span></span>
- <span data-ttu-id="c6399-133">モデル</span><span class="sxs-lookup"><span data-stu-id="c6399-133">Models</span></span>
- <span data-ttu-id="c6399-134">スクリプト</span><span class="sxs-lookup"><span data-stu-id="c6399-134">Scripts</span></span>
- <span data-ttu-id="c6399-135">ビュー</span><span class="sxs-lookup"><span data-stu-id="c6399-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="c6399-136">おすすめのライブラリ</span><span class="sxs-lookup"><span data-stu-id="c6399-136">Featured Libraries</span></span>

- <span data-ttu-id="c6399-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="c6399-137">ASP.NET MVC</span></span>
- <span data-ttu-id="c6399-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c6399-138">ASP.NET Web API</span></span>
- <span data-ttu-id="c6399-139">ASP.NET Web Optimization-バンドルと縮小</span><span class="sxs-lookup"><span data-stu-id="c6399-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="c6399-140">簡単な[.js](http://Breezejs.com) -豊富なデータ管理</span><span class="sxs-lookup"><span data-stu-id="c6399-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="c6399-141">[Durandal](http://Durandaljs.com) -ナビゲーションとビューのコンポジション</span><span class="sxs-lookup"><span data-stu-id="c6399-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="c6399-142">[ノックアウト](http://Knockoutjs.com)-データバインディング</span><span class="sxs-lookup"><span data-stu-id="c6399-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="c6399-143">[必要な .js](http://requirejs.org) -AMD および optimization によるモジュール性</span><span class="sxs-lookup"><span data-stu-id="c6399-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="c6399-144">[Toastr](http://jpapa.me/c7toastr) -ポップアップメッセージ</span><span class="sxs-lookup"><span data-stu-id="c6399-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="c6399-145">[Twitter のブートストラップ](https://twitter.github.com/bootstrap/)-堅牢な CSS スタイル</span><span class="sxs-lookup"><span data-stu-id="c6399-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="c6399-146">Visual Studio 2012 ホットタオルの SPA テンプレートを使用したインストール</span><span class="sxs-lookup"><span data-stu-id="c6399-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="c6399-147">ホットタオルは、Visual Studio 2012 テンプレートとしてインストールできます。</span><span class="sxs-lookup"><span data-stu-id="c6399-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="c6399-148">`File` | `New Project` をクリックし、`ASP.NET MVC 4 Web Application` を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6399-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="c6399-149">次に、"ホットタオルシングルページアプリケーション" テンプレートを選択し、を実行します。</span><span class="sxs-lookup"><span data-stu-id="c6399-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="c6399-150">NuGet パッケージを使用したインストール</span><span class="sxs-lookup"><span data-stu-id="c6399-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="c6399-151">また、Hot タオルは、既存の空の ASP.NET MVC プロジェクトを補強する NuGet パッケージでもあります。</span><span class="sxs-lookup"><span data-stu-id="c6399-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="c6399-152">Nuget を使用してインストールするだけで、を実行します。</span><span class="sxs-lookup"><span data-stu-id="c6399-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="c6399-153">ホットタオルでビルドするにはどうすればいいですか。</span><span class="sxs-lookup"><span data-stu-id="c6399-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="c6399-154">単にコードの追加を開始します。</span><span class="sxs-lookup"><span data-stu-id="c6399-154">Simply start adding code!</span></span>

1. <span data-ttu-id="c6399-155">独自のサーバー側コードを追加します (できれば Entity Framework と WebAPI)。</span><span class="sxs-lookup"><span data-stu-id="c6399-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="c6399-156">`App/views` フォルダーへのビューの追加</span><span class="sxs-lookup"><span data-stu-id="c6399-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="c6399-157">`App/viewmodels` フォルダーに viewmodel を追加する</span><span class="sxs-lookup"><span data-stu-id="c6399-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="c6399-158">新しいビューに HTML およびノックアウトデータバインドを追加する</span><span class="sxs-lookup"><span data-stu-id="c6399-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="c6399-159">`shell.js` のナビゲーションルートを更新する</span><span class="sxs-lookup"><span data-stu-id="c6399-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="c6399-160">HTML/JavaScript のチュートリアル</span><span class="sxs-lookup"><span data-stu-id="c6399-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="c6399-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="c6399-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="c6399-162">index. cshtml は、MVC アプリケーションの開始ルートおよびビューです。</span><span class="sxs-lookup"><span data-stu-id="c6399-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="c6399-163">これには、すべての標準的なメタタグ、css リンク、および必要とされる JavaScript の参照が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="c6399-164">本文には、要求されたときにすべてのコンテンツ (ビュー) が配置される1つの `<div>` が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="c6399-165">`@Scripts.Render` は、`main.js` ファイルに格納されているアプリケーションのコードの開始ポイントを実行するために、必要な .js を使用します。</span><span class="sxs-lookup"><span data-stu-id="c6399-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="c6399-166">スプラッシュスクリーンは、アプリの読み込み中にスプラッシュスクリーンを作成する方法を示すために用意されています。</span><span class="sxs-lookup"><span data-stu-id="c6399-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="c6399-167">アプリ/メイン js</span><span class="sxs-lookup"><span data-stu-id="c6399-167">App/main.js</span></span>

<span data-ttu-id="c6399-168">`main.js` ファイルには、アプリが読み込まれるとすぐに実行されるコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="c6399-169">ここでは、ナビゲーションルートを定義し、スタートアップビューを設定し、アプリケーションのデータの準備などの設定/ブートストラップを実行します。</span><span class="sxs-lookup"><span data-stu-id="c6399-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="c6399-170">`main.js` ファイルは、アプリケーションの起動を開始するために役立ついくつかの durandal のモジュールを定義します。</span><span class="sxs-lookup"><span data-stu-id="c6399-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="c6399-171">Define ステートメントを使用すると、モジュールの依存関係を解決して、関数で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c6399-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="c6399-172">まず、デバッグメッセージが有効になります。これにより、アプリケーションがコンソールウィンドウに対して実行しているイベントに関するメッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="c6399-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="c6399-173">アプリの開始コードは、アプリケーションを起動するように durandal framework に指示します。</span><span class="sxs-lookup"><span data-stu-id="c6399-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="c6399-174">規則は、durandal がすべてのビューを認識し、viewmodel が同じ名前付きフォルダーにそれぞれ含まれるように設定されています。</span><span class="sxs-lookup"><span data-stu-id="c6399-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="c6399-175">最後に、定義済みの `entrance` アニメーションを使用して、`app.setRoot` によって `shell` が読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c6399-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="c6399-176">ビュー</span><span class="sxs-lookup"><span data-stu-id="c6399-176">Views</span></span>

<span data-ttu-id="c6399-177">ビューは `App/views` フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="c6399-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="c6399-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="c6399-178">shell.html</span></span>

<span data-ttu-id="c6399-179">`shell.html` には、HTML のマスターレイアウトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="c6399-180">他のすべてのビューは、`shell` ビューの側のどこかに構成されます。</span><span class="sxs-lookup"><span data-stu-id="c6399-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="c6399-181">ホットタオルは、ヘッダー、コンテンツ領域、およびフッターという3つの領域を持つ `shell` を提供します。</span><span class="sxs-lookup"><span data-stu-id="c6399-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="c6399-182">これらの各リージョンには、要求されたときに他のビューのコンテンツと共に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c6399-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="c6399-183">ヘッダーとフッターの `compose` バインドは、`nav` ビューと `footer` ビューを指すように、ホットタオルでハードコーディングされます。</span><span class="sxs-lookup"><span data-stu-id="c6399-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="c6399-184">セクション `#content` の作成バインドは、`router` モジュールのアクティブな項目にバインドされます。</span><span class="sxs-lookup"><span data-stu-id="c6399-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="c6399-185">つまり、ナビゲーションリンクをクリックすると、対応するビューがこの領域に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c6399-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="c6399-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="c6399-186">nav.html</span></span>

<span data-ttu-id="c6399-187">`nav.html` には、SPA のナビゲーションリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="c6399-188">たとえば、メニュー構造を配置できます。</span><span class="sxs-lookup"><span data-stu-id="c6399-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="c6399-189">多くの場合、これは、`shell.js`で定義したナビゲーションを表示するために、`router` モジュールへの (ノックアウトを使用した) データバインドです。</span><span class="sxs-lookup"><span data-stu-id="c6399-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="c6399-190">ノックアウトは、データバインド属性を検索し、それらを `shell` ビューモデルにバインドして、ナビゲーションルートを表示したり、`router` モジュールがあるビューから別のビューに移動しているときに (Twitter ブートストラップを使用して) progressbar を表示したりします (`router.isNavigating`を参照)。</span><span class="sxs-lookup"><span data-stu-id="c6399-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="c6399-191">home .html と details .html</span><span class="sxs-lookup"><span data-stu-id="c6399-191">home.html and details.html</span></span>

<span data-ttu-id="c6399-192">これらのビューには、カスタムビューの HTML が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="c6399-193">`nav` ビューのメニューの [`home`] リンクをクリックすると、`home` ビューが `shell` ビューのコンテンツ領域に配置されます。</span><span class="sxs-lookup"><span data-stu-id="c6399-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="c6399-194">これらのビューは、独自のカスタムビューに拡張することも、置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="c6399-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="c6399-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="c6399-195">footer.html</span></span>

<span data-ttu-id="c6399-196">`footer.html` には、`shell` ビューの下部にあるフッターに表示される HTML が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="c6399-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="c6399-197">ViewModels</span></span>

<span data-ttu-id="c6399-198">Viewmodel フォルダー `App/viewmodels` にあります。</span><span class="sxs-lookup"><span data-stu-id="c6399-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="c6399-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="c6399-199">shell.js</span></span>

<span data-ttu-id="c6399-200">`shell` ビューモデルには、`shell` ビューにバインドされているプロパティおよび関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="c6399-201">多くの場合、メニューナビゲーションバインドが見つかります (`router.mapNav` ロジックを参照)。</span><span class="sxs-lookup"><span data-stu-id="c6399-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="c6399-202">home .js と details js</span><span class="sxs-lookup"><span data-stu-id="c6399-202">home.js and details.js</span></span>

<span data-ttu-id="c6399-203">これらの viewmodel には、`home` ビューにバインドされているプロパティおよび関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6399-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="c6399-204">また、ビューのプレゼンテーションロジックも含まれており、データとビューの間の接着です。</span><span class="sxs-lookup"><span data-stu-id="c6399-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="c6399-205">サービス</span><span class="sxs-lookup"><span data-stu-id="c6399-205">Services</span></span>

<span data-ttu-id="c6399-206">サービスは、App/services フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="c6399-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="c6399-207">リモートデータの取得と送信を行う dataservice モジュールなどの今後のサービスを配置するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="c6399-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="c6399-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="c6399-208">logger.js</span></span>

<span data-ttu-id="c6399-209">ホットタオルでは、services フォルダーに `logger` モジュールが提供されます。</span><span class="sxs-lookup"><span data-stu-id="c6399-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="c6399-210">`logger` モジュールは、コンソールにメッセージを記録する場合と、ユーザーにポップアップで表示する場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="c6399-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
