---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 リリースノートの ASP.NET and Web Tools |Microsoft Docs
author: microsoft
description: このドキュメントでは、Visual Studio 2013 の ASP.NET and Web Tools のリリースについて説明します。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449524"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="5409a-103">Visual Studio 2013 の ASP.NET と Web ツールのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="5409a-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="5409a-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5409a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5409a-105">このドキュメントでは、Visual Studio 2013 の ASP.NET and Web Tools のリリースについて説明します。</span><span class="sxs-lookup"><span data-stu-id="5409a-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="5409a-106">内容</span><span class="sxs-lookup"><span data-stu-id="5409a-106">Contents</span></span>

- [<span data-ttu-id="5409a-107">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="5409a-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="5409a-108">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="5409a-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="5409a-109">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="5409a-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="5409a-110">Visual Studio 2013 の ASP.NET and Web Tools の新機能</span><span class="sxs-lookup"><span data-stu-id="5409a-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="5409a-111">1つの ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5409a-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="5409a-112">新しい Web プロジェクトのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="5409a-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="5409a-113">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="5409a-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="5409a-114">ブラウザー リンク</span><span class="sxs-lookup"><span data-stu-id="5409a-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="5409a-115">Visual Studio Web エディターの機能強化</span><span class="sxs-lookup"><span data-stu-id="5409a-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="5409a-116">Visual Studio での Azure App Service Web Apps のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="5409a-117">Web 発行の機能強化</span><span class="sxs-lookup"><span data-stu-id="5409a-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="5409a-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5409a-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="5409a-119">ASP.NET Web フォーム</span><span class="sxs-lookup"><span data-stu-id="5409a-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="5409a-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="5409a-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="5409a-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="5409a-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="5409a-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="5409a-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="5409a-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5409a-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="5409a-124">Microsoft OWIN コンポーネント</span><span class="sxs-lookup"><span data-stu-id="5409a-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="5409a-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5409a-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="5409a-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="5409a-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="5409a-127">ASP.NET アプリの中断</span><span class="sxs-lookup"><span data-stu-id="5409a-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="5409a-128">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="5409a-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="5409a-129">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="5409a-129">Installation Notes</span></span>

<span data-ttu-id="5409a-130">Visual Studio 2013 の ASP.NET and Web Tools はメインインストーラーにバンドルされており、[ここで](https://www.asp.net/downloads)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="5409a-131">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="5409a-131">Documentation</span></span>

<span data-ttu-id="5409a-132">[ASP.NET の Web サイト](https://www.asp.net/)から、Visual Studio 2013 の ASP.NET and Web Tools に関するチュートリアルやその他の情報を入手できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="5409a-133">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="5409a-133">Software Requirements</span></span>

<span data-ttu-id="5409a-134">ASP.NET and Web Tools には Visual Studio 2013 が必要です。</span><span class="sxs-lookup"><span data-stu-id="5409a-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="5409a-135">Visual Studio 2013 の ASP.NET and Web Tools の新機能</span><span class="sxs-lookup"><span data-stu-id="5409a-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="5409a-136">以下のセクションでは、リリースで導入された機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="5409a-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="5409a-137">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5409a-137">One ASP.NET</span></span>

<span data-ttu-id="5409a-138">Visual Studio 2013 のリリースでは、ASP.NET テクノロジの使用経験を統合するための手順を実行しました。これによって、必要なものを簡単に組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="5409a-139">たとえば、MVC を使用してプロジェクトを開始し、後で web フォームページをプロジェクトに簡単に追加したり、web フォームプロジェクトのスキャフォールディング Web Api を追加したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="5409a-140">ASP.NET の1つは、ASP.NET で気に入っていることを開発者が簡単に実行できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="5409a-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="5409a-141">どのテクノロジを選択した場合でも、1つの ASP.NET の信頼された基盤となるフレームワークを使用して、自信を持って構築できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="5409a-142">新しい Web プロジェクトのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="5409a-142">New Web Project Experience</span></span>

<span data-ttu-id="5409a-143">Visual Studio 2013 で新しい web プロジェクトを作成するためのエクスペリエンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="5409a-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="5409a-144">**[New ASP.NET Web プロジェクト]** ダイアログでは、必要なプロジェクトの種類を選択したり、テクノロジ (web フォーム、MVC、web API) の任意の組み合わせを構成したり、認証オプションを構成したり、単体テストプロジェクトを追加したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新しい ASP.NET プロジェクト](release-notes/_static/image1.png)

<span data-ttu-id="5409a-146">新しいダイアログボックスでは、多くのテンプレートの既定の認証オプションを変更できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="5409a-147">たとえば、ASP.NET Web フォームプロジェクトを作成するときに、次のいずれかのオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="5409a-148">[認証なし]</span><span class="sxs-lookup"><span data-stu-id="5409a-148">No Authentication</span></span>
- <span data-ttu-id="5409a-149">個々のユーザーアカウント (ASP.NET メンバーシップまたはソーシャルプロバイダーのログイン)</span><span class="sxs-lookup"><span data-stu-id="5409a-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="5409a-150">組織アカウント (インターネットアプリケーションの Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5409a-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="5409a-151">Windows 認証 (イントラネットアプリケーションでの Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5409a-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![認証オプション](release-notes/_static/image2.png)

<span data-ttu-id="5409a-153">Web プロジェクトを作成するための新しいプロセスの詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="5409a-154">新しい認証オプションの詳細については、このドキュメントの後半の「 [ASP.NET Identity](#TOC8) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="5409a-155">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="5409a-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="5409a-156">ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="5409a-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="5409a-157">これにより、データモデルと対話する定型コードをプロジェクトに簡単に追加できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="5409a-158">以前のバージョンの Visual Studio では、スキャフォールディングは ASP.NET MVC プロジェクトに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="5409a-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="5409a-159">Visual Studio 2013 では、Web フォームを含む任意の ASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="5409a-160">Visual Studio 2013 は、現在、Web フォームプロジェクトのページの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加することで、Web フォームでスキャフォールディングを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="5409a-161">Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。</span><span class="sxs-lookup"><span data-stu-id="5409a-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="5409a-162">スキャフォールディングを使用する場合は、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5409a-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="5409a-163">たとえば、ASP.NET の Web フォームプロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な NuGet パッケージと参照がプロジェクトに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="5409a-164">MVC スキャフォールディングを Web フォームプロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログウィンドウで **[Mvc 5 の依存関係]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5409a-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="5409a-165">MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。</span><span class="sxs-lookup"><span data-stu-id="5409a-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="5409a-166">[最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="5409a-167">[完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="5409a-168">非同期コントローラーのスキャフォールディングのサポートには、Entity Framework 6 の新しい非同期機能が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="5409a-169">詳細とチュートリアルについては、「 [ASP.NET スキャフォールディングの概要](aspnet-scaffolding-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="5409a-170">Browser Link – browser と Visual Studio の間の SignalR チャネル</span><span class="sxs-lookup"><span data-stu-id="5409a-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="5409a-171">新しい[ブラウザーリンク](using-browser-link.md)機能を使用すると、複数のブラウザーを Visual Studio に接続し、ツールバーのボタンをクリックしてすべてを更新できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="5409a-172">モバイルエミュレーターを含む複数のブラウザーを開発サイトに接続し、[更新] をクリックすると、すべてのブラウザーを同時に更新できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="5409a-173">ブラウザーリンクでは、開発者がブラウザーリンク拡張機能を作成できるようにする API も公開されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="5409a-174">開発者が Browser Link API を利用できるようにすることで、Visual Studio と接続されている任意のブラウザーの間の境界を越える非常に高度なシナリオを作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="5409a-175">Web Essentials は API を利用して、Visual Studio とブラウザーの開発者ツールの間に統合されたエクスペリエンスを作成し、モバイルエミュレーターをリモートで制御します。</span><span class="sxs-lookup"><span data-stu-id="5409a-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="5409a-176">Visual Studio Web エディターの機能強化</span><span class="sxs-lookup"><span data-stu-id="5409a-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="5409a-177">Visual Studio 2013 には、Razor ファイル用の新しい HTML エディターと、web アプリケーションの HTML ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="5409a-178">新しい HTML エディターには、HTML5 に基づく単一の統合スキーマが用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="5409a-179">これには、かっこの自動補完、jQuery UI と AngularJS 属性の IntelliSense、属性の IntelliSense のグループ化、ID とクラス名の Intellisense、およびパフォーマンスの向上、書式設定、およびスマートタグの追加などの機能強化が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="5409a-180">次のスクリーンショットは、HTML エディターでブートストラップ属性の IntelliSense を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML エディターでの Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="5409a-182">また Visual Studio 2013 には、CoffeeScript と LESS エディターの両方が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="5409a-183">LESS エディターには、CSS エディターのすべての優れた機能が用意されており、@import チェーン内のすべてのドキュメントにわたって、変数と mixin のための特定の Intellisense が用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="5409a-184">Visual Studio での Azure App Service Web Apps のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="5409a-185">Azure SDK for .NET 2.2 の Visual Studio 2013 では、**サーバーエクスプローラー**を使用してリモート web アプリと直接やり取りできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="5409a-186">Azure アカウントにサインインしたり、新しい web アプリを作成したり、アプリを構成したり、リアルタイムログを表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="5409a-187">SDK 2.2 がリリースされるとすぐに、Azure でリモートでデバッグモードで実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="5409a-188">Azure App Service Web Apps の新機能のほとんどは、Azure SDK for .NET の現在のリリースをインストールするときに Visual Studio 2012 でも動作します。</span><span class="sxs-lookup"><span data-stu-id="5409a-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="5409a-189">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="5409a-190">Azure App Service で ASP.NET web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5409a-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="5409a-191">Visual Studio を使用した Azure App Service での Web アプリのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="5409a-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="5409a-192">Web 発行の機能強化</span><span class="sxs-lookup"><span data-stu-id="5409a-192">Web Publish Enhancements</span></span>

<span data-ttu-id="5409a-193">Visual Studio 2013 には、Web 公開の新機能と強化された機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="5409a-194">いくつかを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5409a-194">Here are a few of them:</span></span>

- <span data-ttu-id="5409a-195">Web.config[ファイルの暗号化](https://go.microsoft.com/fwlink/?LinkId=325529)を簡単に自動化できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="5409a-196">(このリンクと、次の2つのポイントは、10/17 の当日に予定されていない可能性がある MSDN のドキュメントを示しています)。</span><span class="sxs-lookup"><span data-stu-id="5409a-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="5409a-197">[デプロイ中にアプリケーションをオフラインにする操作を](https://go.microsoft.com/fwlink/?LinkId=325530)簡単に自動化できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="5409a-198">サーバーにコピーするファイルを決定するために、[最終更新日ではなくファイルチェックサムを使用](https://go.microsoft.com/fwlink/?LinkId=325531)するように Web 配置を構成します。</span><span class="sxs-lookup"><span data-stu-id="5409a-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="5409a-199">FTP またはファイルシステムの発行方法を使用している場合は、(Web.config を含む) 個々の選択したファイルをすばやく発行します。また、Web 配置を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="5409a-200">ASP.NET web デプロイの詳細については、 [ASP.NET サイト](https://go.microsoft.com/fwlink/?LinkId=322027)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="5409a-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5409a-201">NuGet 2.7</span></span>

<span data-ttu-id="5409a-202">NuGet 2.7 には新機能の豊富なセットが含まれています。詳細については、「 [nuget 2.7 のリリースノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="5409a-203">このバージョンの NuGet では、パッケージをダウンロードするために NuGet のパッケージ復元機能に明示的に同意する必要もなくなります。</span><span class="sxs-lookup"><span data-stu-id="5409a-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="5409a-204">NuGet をインストールすることにより、同意 (および NuGet の [基本設定] ダイアログの関連するチェックボックス) が許可されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="5409a-205">既定では、パッケージの復元が正常に機能するようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="5409a-206">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="5409a-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="5409a-207">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5409a-207">One ASP.NET</span></span>

<span data-ttu-id="5409a-208">Web フォームプロジェクトテンプレートは、新しい1つの ASP.NET エクスペリエンスとシームレスに統合されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="5409a-209">Web フォームプロジェクトに MVC と Web API のサポートを追加できます。また、ASP.NET プロジェクト作成ウィザードを使用して認証を構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="5409a-210">詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="5409a-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5409a-211">ASP.NET Identity</span></span>

<span data-ttu-id="5409a-212">Web フォームプロジェクトテンプレートでは、新しい ASP.NET Identity framework がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5409a-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="5409a-213">さらに、テンプレートでは、Web フォームイントラネットプロジェクトの作成がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="5409a-214">詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の[認証方法](creating-web-projects-in-visual-studio.md#auth)に関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="5409a-215">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="5409a-215">Bootstrap</span></span>

<span data-ttu-id="5409a-216">Web フォームテンプレートでは、[ブートストラップ](http://twitter.github.io/bootstrap/)を使用して、外観と応答性が向上し、簡単にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="5409a-217">詳細については、 [Visual Studio 2013 web プロジェクトテンプレート](creating-web-projects-in-visual-studio.md#bootstrap)の「ブートストラップ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="5409a-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="5409a-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="5409a-219">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5409a-219">One ASP.NET</span></span>

<span data-ttu-id="5409a-220">Web MVC プロジェクトテンプレートは、新しい1つの ASP.NET エクスペリエンスとシームレスに統合されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="5409a-221">1つの ASP.NET プロジェクト作成ウィザードを使用して、MVC プロジェクトをカスタマイズし、認証を構成することができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="5409a-222">MVC 5 を ASP.NET する入門用のチュートリアルについては、「 [ASP.NET mvc 5 を使用](../../../mvc/overview/getting-started/introduction/getting-started.md)したはじめに」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="5409a-223">Mvc 4 プロジェクトを MVC 5 にアップグレードする方法については、「 [ASP.NET mvc 4 と WEB Api プロジェクトを ASP.NET mvc 5 および WEB api 2 にアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="5409a-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5409a-224">ASP.NET Identity</span></span>

<span data-ttu-id="5409a-225">MVC プロジェクトテンプレートは、認証と id 管理に ASP.NET Identity を使用するように更新されました。</span><span class="sxs-lookup"><span data-stu-id="5409a-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="5409a-226">Facebook と Google の認証および新しいメンバーシップ API を使用するチュートリアルについては、「 [facebook と Google OAuth2 を使用した ASP.NET mvc 5 アプリの作成](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)」と「[認証と SQL DB を使用した ASP.NET mvc アプリ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)の作成」と「Azure App Service へのデプロイ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="5409a-227">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="5409a-227">Bootstrap</span></span>

<span data-ttu-id="5409a-228">MVC プロジェクトテンプレートは、[ブートストラップ](http://getbootstrap.com/)を使用するように更新され、簡単にカスタマイズできる外観と応答性を備えています。</span><span class="sxs-lookup"><span data-stu-id="5409a-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="5409a-229">詳細については、 [Visual Studio 2013 web プロジェクトテンプレート](creating-web-projects-in-visual-studio.md#bootstrap)の「ブートストラップ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="5409a-230">認証フィルター</span><span class="sxs-lookup"><span data-stu-id="5409a-230">Authentication filters</span></span>

<span data-ttu-id="5409a-231">認証フィルターは、ASP.NET MVC の新しい種類のフィルターで、ASP.NET MVC パイプラインの承認フィルターの前に実行されます。また、アクションごと、コントローラー単位、またはすべてのコントローラーに対してグローバルに認証ロジックを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="5409a-232">認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="5409a-233">認証フィルターでは、承認されていない要求に応答して認証チャレンジを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="5409a-234">フィルターのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="5409a-234">Filter overrides</span></span>

<span data-ttu-id="5409a-235">オーバーライドフィルターを指定することにより、特定のアクションメソッドまたはコントローラーに適用するフィルターを上書きできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="5409a-236">上書きフィルターでは、特定のスコープ (action または controller) に対して実行しないフィルターの種類のセットを指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="5409a-237">これにより、グローバルに適用されるフィルターを構成してから、特定のグローバルフィルターを特定のアクションまたはコントローラーに適用しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="5409a-238">属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="5409a-238">Attribute routing</span></span>

<span data-ttu-id="5409a-239">ASP.NET MVC は、 [http://attributerouting.net](http://attributerouting.net)の作成者である Tim mccall による貢献のおかげで、属性ルーティングをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="5409a-240">属性ルーティングを使用すると、アクションとコントローラーに注釈を付けることによって、ルートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="5409a-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="5409a-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="5409a-242">属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="5409a-242">Attribute routing</span></span>

<span data-ttu-id="5409a-243">ASP.NET Web API は、 [http://attributerouting.net](http://attributerouting.net)の作成者である Tim mccall による貢献のおかげで、属性ルーティングをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="5409a-244">属性ルーティングでは、次のようにアクションとコントローラーに注釈を付けることで、Web API のルートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="5409a-245">属性ルーティングを使用すると、web API の Uri をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="5409a-246">たとえば、1つの API コントローラーを使用してリソース階層を簡単に定義できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="5409a-247">属性ルーティングでは、省略可能なパラメーター、既定値、およびルート制約を指定するための便利な構文も提供されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="5409a-248">属性ルーティングの詳細については、「 [WEB API 2 での属性ルーティング](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="5409a-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="5409a-249">OAuth 2.0</span></span>

<span data-ttu-id="5409a-250">Web API とシングルページアプリケーションプロジェクトテンプレートで、OAuth 2.0 を使用した承認がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="5409a-251">OAuth 2.0 は、保護されたリソースへのクライアントアクセスを承認するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="5409a-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="5409a-252">これは、ブラウザーやモバイルデバイスなど、さまざまなクライアントで機能します。</span><span class="sxs-lookup"><span data-stu-id="5409a-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="5409a-253">OAuth 2.0 のサポートは、ベアラー認証用の Microsoft OWIN コンポーネントによって提供される新しいセキュリティミドルウェアと、承認サーバーロールの実装に基づいています。</span><span class="sxs-lookup"><span data-stu-id="5409a-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="5409a-254">または、Windows Server 2012 R2 の Azure Active Directory や ADFS など、組織の承認サーバーを使用してクライアントを承認することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="5409a-255">OData の機能強化</span><span class="sxs-lookup"><span data-stu-id="5409a-255">OData Improvements</span></span>

<span data-ttu-id="5409a-256">**$Select、$expand、$batch、および $value のサポート**</span><span class="sxs-lookup"><span data-stu-id="5409a-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="5409a-257">ASP.NET Web API OData で $select、$expand、および $value が完全にサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="5409a-258">また、要求のバッチ処理と変更セットの処理に $batch を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="5409a-259">$Select オプションと $expand オプションを使用すると、OData エンドポイントから返されるデータの構造を変更できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="5409a-260">詳細については、「 [WEB API OData での $select と $expand サポートの概要](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="5409a-261">**拡張機能の向上**</span><span class="sxs-lookup"><span data-stu-id="5409a-261">**Improved extensibility**</span></span>

<span data-ttu-id="5409a-262">OData フォーマッタを拡張できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="5409a-263">Atom エントリメタデータを追加したり、名前付きストリームとメディアリンクエントリをサポートしたり、インスタンス注釈を追加したり、リンクの生成方法をカスタマイズしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="5409a-264">**種類-less サポート**</span><span class="sxs-lookup"><span data-stu-id="5409a-264">**Type-less support**</span></span>

<span data-ttu-id="5409a-265">エンティティ型に CLR 型を定義しなくても、OData サービスを構築できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="5409a-266">代わりに、odata コントローラーは、OData フォーマッタのシリアル化/逆シリアル化である**Iedmobject**インスタンスを取得または返すことができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="5409a-267">**既存のモデルを再利用する**</span><span class="sxs-lookup"><span data-stu-id="5409a-267">**Reuse an existing model**</span></span>

<span data-ttu-id="5409a-268">既に既存の entity data model (EDM) を使用している場合は、新しい entity data model を作成するのではなく、直接再利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="5409a-269">たとえば、Entity Framework を使用している場合、EF がビルドする EDM を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="5409a-270">バッチ処理の要求</span><span class="sxs-lookup"><span data-stu-id="5409a-270">Request Batching</span></span>

<span data-ttu-id="5409a-271">要求のバッチ処理では、複数の操作を1つの HTTP POST 要求に結合して、ネットワークトラフィックを減らし、よりスムーズで高いなユーザーインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="5409a-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="5409a-272">ASP.NET Web API は、要求バッチ処理のためのいくつかの方法をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="5409a-273">OData サービスの $batch エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="5409a-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="5409a-274">複数の要求を1つの MIME マルチパート要求にパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="5409a-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="5409a-275">カスタムバッチ形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="5409a-275">Use a custom batching format.</span></span>

<span data-ttu-id="5409a-276">要求のバッチ処理を有効にするには、バッチハンドラーを含むルートを Web API 構成に追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="5409a-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="5409a-277">また、要求または順番に実行するかどうかを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="5409a-278">ポータブル ASP.NET Web API クライアント</span><span class="sxs-lookup"><span data-stu-id="5409a-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="5409a-279">ASP.NET Web API クライアントを使用して、Windows ストアで動作するポータブルクラスライブラリを作成し、8つのアプリケーションを Windows Phone できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="5409a-280">また、クライアントとサーバー間で共有できるポータブルフォーマッタを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="5409a-281">テストの容易性の向上</span><span class="sxs-lookup"><span data-stu-id="5409a-281">Improved Testability</span></span>

<span data-ttu-id="5409a-282">Web API 2 を使用すると、API コントローラーの単体テストがはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5409a-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="5409a-283">要求メッセージと構成を使用して API コントローラーをインスタンス化し、テストするアクションメソッドを呼び出すだけです。</span><span class="sxs-lookup"><span data-stu-id="5409a-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="5409a-284">また、リンク生成を実行するアクションメソッドの**Urlhelper**クラスを簡単にモックできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="5409a-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="5409a-285">IHttpActionResult</span></span>

<span data-ttu-id="5409a-286">IHttpActionResult を実装して、Web API アクションメソッドの結果をカプセル化できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="5409a-287">Web API アクションメソッドから返された IHttpActionResult は、結果の応答メッセージを生成するために ASP.NET Web API ランタイムによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="5409a-288">Web api の実装の単体テストを簡単にするために、任意の Web API アクションから IHttpActionResult を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="5409a-289">便宜上、特定のステータスコード、書式設定されたコンテンツ、またはコンテンツをネゴシエートした応答を返す結果を含む、いくつかの IHttpActionResult 実装がすぐに用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="5409a-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="5409a-290">HttpRequestContext</span></span>

<span data-ttu-id="5409a-291">新しい**Httprequestcontext**は、要求に関連付けられているが、要求からすぐには利用できない状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="5409a-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="5409a-292">たとえば、 **Httprequestcontext**を使用して、ルートデータ、要求に関連付けられているプリンシパル、クライアント証明書、 **urlhelper** 、および仮想パスのルートを取得できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="5409a-293">単体テストのために、 **Httprequestcontext**を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="5409a-294">要求のプリンシパルは、 **thread.currentprincipal**に依存するのではなく、要求でフローされるので、Web API パイプライン内にある間、要求の有効期間中にプリンシパルを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="5409a-295">CORS</span><span class="sxs-lookup"><span data-stu-id="5409a-295">CORS</span></span>

<span data-ttu-id="5409a-296">Brock Allen によるもう1つの優れた投稿により、ASP.NET はクロスオリジン要求共有 (CORS) を完全にサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="5409a-297">ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="5409a-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="5409a-298">[CORS](http://www.w3.org/TR/cors/)は、サーバーが同じオリジンポリシーを緩めることを可能にする W3C 標準です。</span><span class="sxs-lookup"><span data-stu-id="5409a-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="5409a-299">CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="5409a-300">Web API 2 では、プレフライト要求の自動処理を含む CORS がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="5409a-301">詳細については、 [ASP.NET Web API でのクロスオリジン要求の有効化](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)に関する文書を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="5409a-302">認証フィルター</span><span class="sxs-lookup"><span data-stu-id="5409a-302">Authentication Filters</span></span>

<span data-ttu-id="5409a-303">認証フィルターは、ASP.NET Web API パイプラインの承認フィルターの前に実行される ASP.NET Web API の新しい種類のフィルターであり、アクションごと、コントローラー単位、またはすべてのコントローラーに対してグローバルに認証ロジックを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="5409a-304">認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="5409a-305">認証フィルターでは、承認されていない要求に応答して認証チャレンジを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="5409a-306">フィルターのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="5409a-306">Filter Overrides</span></span>

<span data-ttu-id="5409a-307">オーバーライドフィルターを指定することにより、特定のアクションメソッドまたはコントローラーに適用するフィルターを上書きできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="5409a-308">オーバーライドフィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="5409a-309">これにより、グローバルフィルターを追加できますが、特定のアクションまたはコントローラーから除外することができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="5409a-310">OWIN の統合</span><span class="sxs-lookup"><span data-stu-id="5409a-310">OWIN Integration</span></span>

<span data-ttu-id="5409a-311">ASP.NET Web API は OWIN を完全にサポートするようになり、任意の OWIN 対応ホストで実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="5409a-312">また、OWIN 認証システムとの統合を提供する**Hostauthenticationfilter**も含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="5409a-313">OWIN 統合では、SignalR などの他の OWIN ミドルウェアと共に、独自のプロセスで Web API を自己ホストできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="5409a-314">詳細については、「 [USE OWIN To Self Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="5409a-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="5409a-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="5409a-316">以下のセクションでは、SignalR 2.0 の機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="5409a-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="5409a-317">OWIN 上に構築</span><span class="sxs-lookup"><span data-stu-id="5409a-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="5409a-318">MapHubs と Maphubs が MapSignalR になりました</span><span class="sxs-lookup"><span data-stu-id="5409a-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="5409a-319">ドメイン間サポート</span><span class="sxs-lookup"><span data-stu-id="5409a-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="5409a-320">Monotouch.dialog とモノ Id を使用した iOS および Android のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="5409a-321">ポータブル .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="5409a-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="5409a-322">新しい自己ホストパッケージ</span><span class="sxs-lookup"><span data-stu-id="5409a-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="5409a-323">下位互換性のあるサーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="5409a-324">.NET 4.0 のサーバーサポートを削除しました</span><span class="sxs-lookup"><span data-stu-id="5409a-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="5409a-325">クライアントとグループの一覧へのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="5409a-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="5409a-326">特定のユーザーへのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="5409a-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="5409a-327">より優れたエラー処理のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="5409a-328">ハブの単体テストの簡素化</span><span class="sxs-lookup"><span data-stu-id="5409a-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="5409a-329">JavaScript のエラー処理</span><span class="sxs-lookup"><span data-stu-id="5409a-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="5409a-330">既存の1.x プロジェクトを SignalR 2.0 にアップグレードする方法の例については、「 [SignalR 1.X プロジェクトをアップグレード](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="5409a-331">OWIN 上に構築</span><span class="sxs-lookup"><span data-stu-id="5409a-331">Built on OWIN</span></span>

<span data-ttu-id="5409a-332">SignalR 2.0 は[、OWIN (Open Web Interface for .net)](http://owin.org/)で完全に構築されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="5409a-333">この変更により、web ホストアプリケーションと自己ホスト型 SignalR アプリケーションの間で SignalR のセットアッププロセスの一貫性が大幅に向上しますが、多くの API 変更も必要でした。</span><span class="sxs-lookup"><span data-stu-id="5409a-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="5409a-334">MapHubs と Maphubs が MapSignalR になりました</span><span class="sxs-lookup"><span data-stu-id="5409a-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="5409a-335">OWIN 標準との互換性のために、これらのメソッドの名前が `MapSignalR`に変更されました。</span><span class="sxs-lookup"><span data-stu-id="5409a-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="5409a-336">パラメーターを指定せずに `MapSignalR` 呼び出されると、すべてのハブがマップされます (バージョン1.x の `MapHubs` と同様)。個々の**PersistentConnection**オブジェクトをマップするには、型パラメーターとして接続の種類を指定し、最初の引数として接続の URL 拡張子を指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="5409a-337">`MapSignalR` メソッドは、Owin startup クラスで呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="5409a-338">Visual Studio 2013 には、Owin startup クラス用の新しいテンプレートが含まれています。このテンプレートを使用するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="5409a-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="5409a-339">プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="5409a-339">Right-click on the project</span></span>
2. <span data-ttu-id="5409a-340">**[追加]** 、 **[新しい項目]** の選択...</span><span class="sxs-lookup"><span data-stu-id="5409a-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="5409a-341">**[Owin Startup クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5409a-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="5409a-342">新しいクラスに**Startup.cs**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="5409a-343">**Web アプリケーション**では、次に示すように、web.config ファイルの [アプリケーションの設定] ノードのエントリを使用して、`MapSignalR` メソッドを含む Owin startup クラスが Owin のスタートアッププロセスに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="5409a-344">**自己ホスト型アプリケーション**では、Startup クラスは `WebApp.Start` メソッドの型パラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="5409a-345">**SignalR 1.x でのハブと接続のマッピング (web アプリケーションのグローバルアプリケーションファイルから):**</span><span class="sxs-lookup"><span data-stu-id="5409a-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="5409a-346">**SignalR 2.0 でのハブと接続のマッピング (Owin スタートアップクラスファイルから):**</span><span class="sxs-lookup"><span data-stu-id="5409a-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="5409a-347">**自己ホスト型アプリケーション**では、次に示すように、Startup クラスが `WebApp.Start` メソッドの型パラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="5409a-348">ドメイン間サポート</span><span class="sxs-lookup"><span data-stu-id="5409a-348">Cross-Domain Support</span></span>

<span data-ttu-id="5409a-349">SignalR 1.x では、クロスドメイン要求は単一の EnableCrossDomain フラグによって制御されていました。</span><span class="sxs-lookup"><span data-stu-id="5409a-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="5409a-350">このフラグは、JSONP 要求と CORS 要求の両方を制御します。</span><span class="sxs-lookup"><span data-stu-id="5409a-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="5409a-351">柔軟性を高めるため、すべての CORS サポートは SignalR のサーバーコンポーネントから削除されています (ブラウザーがサポートしていることが検出された場合、JavaScript クライアントは引き続き CORS を使用します)。また、これらのシナリオをサポートするために新しい OWIN ミドルウェアを利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="5409a-352">SignalR 2.0 では、クライアントで JSONP が必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように、`HubConfiguration` オブジェクトの `EnableJSONP` を `true`に設定することによって、明示的に有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="5409a-353">JSONP は、CORS よりも安全性が低いため、既定では無効になっています。</span><span class="sxs-lookup"><span data-stu-id="5409a-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="5409a-354">新しい CORS ミドルウェアを SignalR 2.0 に追加するには、次のセクションに示すように、`Microsoft.Owin.Cors` ライブラリをプロジェクトに追加し、SignalR ミドルウェアの前に `UseCors` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5409a-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="5409a-355">**プロジェクトへの Owin の追加**: このライブラリをインストールするには、パッケージマネージャーコンソールで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5409a-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="5409a-356">このコマンドにより、2.0.0 バージョンのパッケージがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="5409a-357">**UseCors の呼び出し**</span><span class="sxs-lookup"><span data-stu-id="5409a-357">**Calling UseCors**</span></span>

<span data-ttu-id="5409a-358">次のコードスニペットは、SignalR 1.x と2.0 でドメイン間接続を実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="5409a-359">**SignalR 1.x でのクロスドメイン要求の実装 (グローバルアプリケーションファイルから)**</span><span class="sxs-lookup"><span data-stu-id="5409a-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="5409a-360">**SignalR 2.0 でのクロスドメイン要求の実装 ( C#コードファイルから)**</span><span class="sxs-lookup"><span data-stu-id="5409a-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="5409a-361">次のコードは、SignalR 2.0 プロジェクトで CORS または JSONP を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="5409a-362">このコードサンプルでは、`MapSignalR`ではなく `Map` と `RunSignalR` を使用して、CORS ミドルウェアが、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要のある SignalR 要求に対してのみ実行されるようにします (`MapSignalR`で指定されたパスのすべてのトラフィックではありません `Map`)。</span><span class="sxs-lookup"><span data-stu-id="5409a-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="5409a-363">Monotouch.dialog とモノ Id を使用した iOS および Android のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="5409a-364">[Xamarin ライブラリ](https://xamarin.com/)の monotouch.dialog コンポーネントとモノ id コンポーネントを使用する IOS および Android クライアントのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="5409a-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="5409a-365">使用方法の詳細については、「 [Xamarin コンポーネントの使用](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="5409a-366">これらのコンポーネントは、SignalR RTW リリースが利用可能になったときに、 [Xamarin ストア](https://store.xamarin.com/)で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="5409a-367"># # # ポータブル .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="5409a-367">### Portable .NET client</span></span>

<span data-ttu-id="5409a-368">クロスプラットフォームの開発を容易にするために、Silverlight、WinRT、および Windows Phone クライアントは、次のプラットフォームをサポートする1つのポータブル .NET クライアントに置き換えられています。</span><span class="sxs-lookup"><span data-stu-id="5409a-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="5409a-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5409a-369">NET 4.5</span></span>
- <span data-ttu-id="5409a-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="5409a-370">Silverlight 5</span></span>
- <span data-ttu-id="5409a-371">WinRT (Windows ストアアプリ用 .NET)</span><span class="sxs-lookup"><span data-stu-id="5409a-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="5409a-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="5409a-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="5409a-373">新しい自己ホストパッケージ</span><span class="sxs-lookup"><span data-stu-id="5409a-373">New Self-Host Package</span></span>

<span data-ttu-id="5409a-374">SignalR 自己ホスト (web サーバーでホストされるのではなく、プロセスまたは他のアプリケーションでホストされている SignalR アプリケーション) の使用を簡単に始めることができる NuGet パッケージが用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="5409a-375">SignalR 1.x でビルドされた自己ホストプロジェクトをアップグレードするには、SignalR パッケージを削除してから、SignalR パッケージを追加した後に追加します。</span><span class="sxs-lookup"><span data-stu-id="5409a-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="5409a-376">自己ホストパッケージの概要については、「[チュートリアル: SignalR 自己ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="5409a-377">下位互換性のあるサーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-377">Backward-compatible server support</span></span>

<span data-ttu-id="5409a-378">以前のバージョンの SignalR では、クライアントとサーバーで使用されている SignalR パッケージのバージョンが同一である必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="5409a-379">更新が困難なシッククライアントアプリケーションをサポートするために、SignalR 2.0 では、古いクライアントでの新しいサーバーバージョンの使用がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="5409a-380">**注: SignalR 2.0 では、以前のバージョンでビルドされたサーバーを新しいクライアントでサポートしていません。**</span><span class="sxs-lookup"><span data-stu-id="5409a-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="5409a-381">.NET 4.0 のサーバーサポートを削除しました</span><span class="sxs-lookup"><span data-stu-id="5409a-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="5409a-382">SignalR 2.0 では、.NET 4.0 とのサーバー相互運用性のサポートが削除されました。</span><span class="sxs-lookup"><span data-stu-id="5409a-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="5409a-383">.NET 4.5 は、SignalR 2.0 サーバーで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="5409a-384">引き続き、SignalR 2.0 用の .NET 4.0 クライアントがあります。</span><span class="sxs-lookup"><span data-stu-id="5409a-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="5409a-385">クライアントとグループの一覧へのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="5409a-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="5409a-386">SignalR 2.0 では、クライアント Id とグループ Id の一覧を使用してメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="5409a-387">次のコードスニペットは、この方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="5409a-388">**PersistentConnection を使用して、クライアントとグループの一覧にメッセージを送信する**</span><span class="sxs-lookup"><span data-stu-id="5409a-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="5409a-389">**ハブを使用して、クライアントとグループの一覧にメッセージを送信する**</span><span class="sxs-lookup"><span data-stu-id="5409a-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="5409a-390">特定のユーザーへのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="5409a-390">Sending a message to a specific user</span></span>

<span data-ttu-id="5409a-391">この機能を使用すると、ユーザーは新しいインターフェイス IUserIdProvider を使用して、IRequest に基づいてユーザー Id を指定できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="5409a-392">**IUserIdProvider インターフェイス**</span><span class="sxs-lookup"><span data-stu-id="5409a-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="5409a-393">既定では、ユーザーの IPrincipal.Identity.Name をユーザー名として使用する実装が存在します。</span><span class="sxs-lookup"><span data-stu-id="5409a-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="5409a-394">ハブでは、新しい API を使用して、これらのユーザーにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="5409a-395">**クライアント. User API の使用**</span><span class="sxs-lookup"><span data-stu-id="5409a-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="5409a-396">より優れたエラー処理のサポート</span><span class="sxs-lookup"><span data-stu-id="5409a-396">Better Error Handling Support</span></span>

<span data-ttu-id="5409a-397">ユーザーは、任意のハブ呼び出しから**HubException**をスローできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="5409a-398">**HubException**のコンストラクターは、文字列メッセージとオブジェクトの追加のエラーデータを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="5409a-399">SignalR は、例外を自動的にシリアル化し、それをクライアントに送信します。これは、ハブメソッドの呼び出しを拒否/失敗するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="5409a-400">[**詳細なハブ例外を表示する]** 設定は、クライアントに送信される**HubException**には影響しません。常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="5409a-401">**HubException をクライアントに送信する方法を示すサーバー側コード**</span><span class="sxs-lookup"><span data-stu-id="5409a-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="5409a-402">**サーバーから送信された HubException への応答を示す JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="5409a-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="5409a-403">**サーバーから送信された HubException への応答を示す .NET クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="5409a-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="5409a-404">ハブの単体テストの簡素化</span><span class="sxs-lookup"><span data-stu-id="5409a-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="5409a-405">SignalR 2.0 には、モッククライアント側の呼び出しの作成を容易にするハブで `IHubCallerConnectionContext` というインターフェイスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="5409a-406">次のコードスニペットは、一般的なテストハーネス[xUnit.net](https://github.com/xunit/xunit)と[moq](https://code.google.com/p/moq/)でこのインターフェイスを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="5409a-407">**XUnit.net を使用した SignalR の単体テスト**</span><span class="sxs-lookup"><span data-stu-id="5409a-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="5409a-408">**Moq を使用した SignalR の単体テスト**</span><span class="sxs-lookup"><span data-stu-id="5409a-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="5409a-409">JavaScript のエラー処理</span><span class="sxs-lookup"><span data-stu-id="5409a-409">JavaScript error handling</span></span>

<span data-ttu-id="5409a-410">SignalR 2.0 では、すべての JavaScript エラー処理コールバックで、生の文字列ではなく JavaScript エラーオブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="5409a-411">これにより、SignalR は、より豊富な情報をエラーハンドラーに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="5409a-412">内部例外は、エラーの `source` プロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="5409a-413">**Start. Fail 例外を処理する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="5409a-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="5409a-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5409a-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="5409a-415">新しい ASP.NET メンバーシップシステム</span><span class="sxs-lookup"><span data-stu-id="5409a-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="5409a-416">ASP.NET Identity は、ASP.NET アプリケーションの新しいメンバーシップシステムです。</span><span class="sxs-lookup"><span data-stu-id="5409a-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="5409a-417">ASP.NET Identity を使用すると、ユーザー固有のプロファイルデータをアプリケーションデータに簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="5409a-418">ASP.NET Identity では、アプリケーションでユーザープロファイルの永続性モデルを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="5409a-419">データは SQL Server データベースまたは別のデータストア (Azure Storage テーブルなどの NoSQL データストア) に格納できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="5409a-420">詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**における[個々のユーザーアカウント](creating-web-projects-in-visual-studio.md#indauth)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="5409a-421">クレーム ベースの認証</span><span class="sxs-lookup"><span data-stu-id="5409a-421">Claims-based authentication</span></span>

<span data-ttu-id="5409a-422">ASP.NET は、信頼性情報ベースの認証をサポートするようになりました。この認証では、ユーザーの id は信頼された発行者からのクレームのセットとして表されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="5409a-423">ユーザーは、アプリケーションデータベースで保持されているユーザー名とパスワードを使用して、またはソーシャル id プロバイダー (Microsoft アカウント、Facebook、Google、Twitter など) を使用するか、または Azure Active Directory を使用して組織アカウントを使用して認証できます。Active Directory フェデレーションサービス (AD FS) (ADFS)。</span><span class="sxs-lookup"><span data-stu-id="5409a-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="5409a-424">Azure Active Directory と Windows Server Active Directory との統合</span><span class="sxs-lookup"><span data-stu-id="5409a-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="5409a-425">認証に Azure Active Directory または Windows Server Active Directory (AD) を使用する ASP.NET プロジェクトを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="5409a-426">詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の「[組織アカウント](creating-web-projects-in-visual-studio.md#orgauth)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="5409a-427">OWIN の統合</span><span class="sxs-lookup"><span data-stu-id="5409a-427">OWIN Integration</span></span>

<span data-ttu-id="5409a-428">ASP.NET 認証は、任意の OWIN ベースのホストで使用できる OWIN ミドルウェアに基づいています。</span><span class="sxs-lookup"><span data-stu-id="5409a-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="5409a-429">OWIN の詳細については、次の[MICROSOFT OWIN Components](#TOC7)のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="5409a-430">Microsoft OWIN コンポーネント</span><span class="sxs-lookup"><span data-stu-id="5409a-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="5409a-431">[Open Web Interface for .net](http://owin.org/) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="5409a-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="5409a-432">OWIN は、web アプリケーションをサーバーから分離することで、web アプリケーションをホストに依存しないようにします。</span><span class="sxs-lookup"><span data-stu-id="5409a-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="5409a-433">たとえば、IIS で OWIN ベースの web アプリケーションをホストしたり、カスタムプロセスで自己ホストしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="5409a-434">Microsoft OWIN コンポーネント (Katana プロジェクトとも呼ばれます) で導入された変更には、新しいサーバーおよびホストコンポーネント、新しいヘルパーライブラリとミドルウェア、新しい認証ミドルウェアが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5409a-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="5409a-435">OWIN と Katana の詳細については、「 [OWIN および Katana の新機能](../../../aspnet/overview/owin-and-katana/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="5409a-436">**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションを IIS クラシックモードで実行することはできません。統合モードで実行する必要があります。**</span><span class="sxs-lookup"><span data-stu-id="5409a-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="5409a-437">**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは完全信頼で実行する必要があります。**</span><span class="sxs-lookup"><span data-stu-id="5409a-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="5409a-438">新しいサーバーとホスト</span><span class="sxs-lookup"><span data-stu-id="5409a-438">New Servers and Hosts</span></span>

<span data-ttu-id="5409a-439">このリリースでは、自己ホストのシナリオを可能にするために新しいコンポーネントが追加されました。</span><span class="sxs-lookup"><span data-stu-id="5409a-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="5409a-440">これらのコンポーネントには、次の NuGet パッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5409a-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="5409a-441">**Owin. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="5409a-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="5409a-442">**HttpListener**を使用して HTTP 要求をリッスンし、それらを OWIN パイプラインに送信する OWIN サーバーを提供します。</span><span class="sxs-lookup"><span data-stu-id="5409a-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="5409a-443">**Owin**には、コンソールアプリケーションや Windows サービスなどのカスタムプロセスで Owin パイプラインを自己ホストする開発者向けのライブラリが用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="5409a-444">**Owinhost**。</span><span class="sxs-lookup"><span data-stu-id="5409a-444">**OwinHost**.</span></span> <span data-ttu-id="5409a-445">には `Microsoft.Owin.Hosting` をラップするスタンドアロンの実行可能ファイルが用意されています。これにより、カスタムホストアプリケーションを作成しなくても、OWIN パイプラインを自己ホストできます。</span><span class="sxs-lookup"><span data-stu-id="5409a-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="5409a-446">さらに、`Microsoft.Owin.Host.SystemWeb` パッケージでは、ミドルウェアが**Systemweb**サーバーにヒントを提供できるようになりました。これは、特定の ASP.NET パイプラインステージの間にミドルウェアを呼び出す必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="5409a-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="5409a-447">この機能は、ASP.NET パイプラインの早い段階で実行される認証ミドルウェアに特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5409a-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="5409a-448">ヘルパーライブラリとミドルウェア</span><span class="sxs-lookup"><span data-stu-id="5409a-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="5409a-449">OWIN 仕様の関数と型の定義のみを使用して OWIN コンポーネントを記述することもできますが、新しい `Microsoft.Owin` パッケージでは、よりわかりやすい抽象化のセットが提供されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="5409a-450">このパッケージは、以前のいくつかのパッケージ (`Owin.Extensions`、`Owin.Types`など) を単一の適切に構造化されたオブジェクトモデルに結合して、他の OWIN コンポーネントで簡単に使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="5409a-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="5409a-451">実際、Microsoft OWIN コンポーネントの大部分は、このパッケージを使用するようになりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="5409a-452">[OWIN](http://www.owin.org)アプリケーションを IIS クラシックモードで実行することはできません。統合モードで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="5409a-453">[OWIN](http://www.owin.org)アプリケーションは完全信頼で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="5409a-454">このリリースには、Owin パッケージも含まれています。これには、実行中の OWIN アプリケーションを検証するミドルウェア、およびエラーを調査するためのエラーページミドルウェアが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="5409a-455">認証コンポーネント</span><span class="sxs-lookup"><span data-stu-id="5409a-455">Authentication Components</span></span>

<span data-ttu-id="5409a-456">次の認証コンポーネントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5409a-456">The following authentication components are available.</span></span>

- <span data-ttu-id="5409a-457">**Owin**します。</span><span class="sxs-lookup"><span data-stu-id="5409a-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="5409a-458">オンプレミスまたはクラウドベースのディレクトリサービスを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="5409a-459">**Owin** cookie を使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="5409a-460">このパッケージは、以前は `Microsoft.Owin.Security.Forms`という名前でした。</span><span class="sxs-lookup"><span data-stu-id="5409a-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="5409a-461">**Owin**は、Facebook の OAuth ベースのサービスを使用した認証を可能にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="5409a-462">**Owin** Google の OpenID ベースのサービスを使用して認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="5409a-463">**Owin**は jwt トークンを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="5409a-464">**Owin** microsoft アカウントを使用して認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="5409a-465">**Owin**します。</span><span class="sxs-lookup"><span data-stu-id="5409a-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="5409a-466">には、ベアラートークンを認証するための、OAuth 承認サーバーとミドルウェアが用意されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="5409a-467">**Owin**は、Twitter の OAuth ベースのサービスを使用した認証を可能にします。</span><span class="sxs-lookup"><span data-stu-id="5409a-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="5409a-468">このリリースには、クロスオリジン HTTP 要求を処理するためのミドルウェアを含む `Microsoft.Owin.Cors` パッケージも含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="5409a-469">JWT 署名のサポートは、Visual Studio 2013 の最終バージョンでは削除されています。</span><span class="sxs-lookup"><span data-stu-id="5409a-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="5409a-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5409a-470">Entity Framework 6</span></span>

<span data-ttu-id="5409a-471">Entity Framework 6 の新機能とその他の変更点の一覧については、「 [Entity Framework バージョンの履歴](https://msdn.com/data/jj574253)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="5409a-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="5409a-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="5409a-473">ASP.NET Razor 3 には、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5409a-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="5409a-474">タブ編集のサポート。</span><span class="sxs-lookup"><span data-stu-id="5409a-474">Support for Tab editing.</span></span> <span data-ttu-id="5409a-475">以前は、**タブを保持**する オプションを使用すると、Visual Studio の **ドキュメントのフォーマット** コマンド、自動インデント、および 自動書式設定 は正常に動作しませんでした。</span><span class="sxs-lookup"><span data-stu-id="5409a-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="5409a-476">この変更により、タブ書式設定用の Razor コードの Visual Studio の書式設定が修正します。</span><span class="sxs-lookup"><span data-stu-id="5409a-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="5409a-477">リンクを生成するときの URL 書き換え規則のサポート。</span><span class="sxs-lookup"><span data-stu-id="5409a-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="5409a-478">透過的セキュリティ属性の削除。</span><span class="sxs-lookup"><span data-stu-id="5409a-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="5409a-479">これは互換性に影響する変更であり、Razor 3 は MVC4 以前と互換性がありませんが、Razor 2 は MVC5 または MVC5 に対してコンパイルされたアセンブリと互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="5409a-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="5409a-480">プレリリース版からの Visual Studio 2013 で修正された Razor 3 の問題については、[こちら](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="5409a-481">ASP.NET アプリの中断</span><span class="sxs-lookup"><span data-stu-id="5409a-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="5409a-482">ASP.NET App Suspend は、1台のコンピューターで多数の ASP.NET サイトをホストするためのユーザーエクスペリエンスと経済モデルを根本的に変更する、.NET Framework 4.5.1 のゲーム変更機能です。</span><span class="sxs-lookup"><span data-stu-id="5409a-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="5409a-483">詳細については、「 [ASP.NET App Suspend –応答性の高い共有 .net web ホスティング](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="5409a-484">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="5409a-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="5409a-485">このセクションでは、Visual Studio 2013 の ASP.NET and Web Tools における既知の問題と重大な変更について説明します。</span><span class="sxs-lookup"><span data-stu-id="5409a-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="5409a-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="5409a-486">NuGet</span></span>

- <span data-ttu-id="5409a-487">[新しいパッケージの復元は、SLN ファイルを使用すると Mono で機能しません](https://nuget.codeplex.com/workitem/3596)。今後の nuget のダウンロードと[nuget.exe パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="5409a-488">[新しいパッケージの復元は、Wix プロジェクトでは機能しません](https://nuget.codeplex.com/workitem/3598)。今後の nuget のダウンロードと[nuget.exe パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="5409a-489">[自動パッケージ復元は、ソリューションフォルダーの下にあるプロジェクトに対しては機能しません](https://nuget.codeplex.com/workitem/3625)。 NuGet 2.8 で修正されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="5409a-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="5409a-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="5409a-491">`$select` と `$expand`のサポートが追加されたため、`ODataQueryOptions<T>.ApplyTo(IQueryable)` `IQueryable<T>` は常に返されません。</span><span class="sxs-lookup"><span data-stu-id="5409a-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="5409a-492">`ODataQueryOptions<T>` の前のサンプルでは、`ApplyTo` から `IQueryable<T>`に戻り値が常にキャストされています。</span><span class="sxs-lookup"><span data-stu-id="5409a-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="5409a-493">これは、以前にサポートしていたクエリオプション (`$filter`、`$orderby`、`$skip`、`$top`) によってクエリの構造が変更されないため、これまでに動作しました。</span><span class="sxs-lookup"><span data-stu-id="5409a-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="5409a-494">これで `$expand` `$select` がサポートされるようになり、`ApplyTo` からの戻り値が常に `IQueryable<T>` されることはなくなりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="5409a-495">前に示したサンプルコードを使用している場合は、クライアントが `$select` と `$expand`を送信しない場合は動作を続行します。</span><span class="sxs-lookup"><span data-stu-id="5409a-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="5409a-496">ただし、`$select` と `$expand` をサポートする場合は、そのコードをこのコードに変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="5409a-497">**要求の Url または RequestContext。 Url は、バッチ要求の実行中に null になります。**</span><span class="sxs-lookup"><span data-stu-id="5409a-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="5409a-498">バッチ処理のシナリオでは、 **Urlhelper**は、**要求の Url**または**RequestContext**からアクセスした場合に null になります。</span><span class="sxs-lookup"><span data-stu-id="5409a-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="5409a-499">現在、この問題はここで追跡されています: [Batchrequestcontext。バッチ処理要求の Url が null](http://aspnetwebstack.codeplex.com/workitem/1301)です。</span><span class="sxs-lookup"><span data-stu-id="5409a-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="5409a-500">この問題を回避するには、次の例のように**Urlhelper**の新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="5409a-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="5409a-501">**UrlHelper の新しいインスタンスを作成しています**</span><span class="sxs-lookup"><span data-stu-id="5409a-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="5409a-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="5409a-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="5409a-503">MVC5 と OrgAuth を使用しているときに、検証を行うビューがある場合、データをビューにポストすると、次のエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="5409a-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="5409a-504">**Error**:</span><span class="sxs-lookup"><span data-stu-id="5409a-504">**Error**:</span></span>

    <span data-ttu-id="5409a-505">*'/' アプリケーションでサーバーエラーが発生しています。*</span><span class="sxs-lookup"><span data-stu-id="5409a-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="5409a-506"><em>型 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' または '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' のクレームが、指定された ClaimsIdentity に存在しませんでした。要求ベースの認証による偽造防止トークンのサポートを有効にするには、構成された要求プロバイダーが、生成した ClaimsIdentity インスタンスに対して両方の要求を提供していることを確認してください。構成された要求プロバイダーが、一意の識別子として別の要求の種類を使用する場合は、静的なプロパティの UniqueClaimTypeIdentifier を設定することによって構成できます。</em></span><span class="sxs-lookup"><span data-stu-id="5409a-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="5409a-507">**回避策**:</span><span class="sxs-lookup"><span data-stu-id="5409a-507">**Workaround**:</span></span>

    <span data-ttu-id="5409a-508">Global.asax に次の行を追加して修正します。</span><span class="sxs-lookup"><span data-stu-id="5409a-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="5409a-509">これは、次のリリースで修正されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="5409a-510">MVC4 アプリを MVC5 にアップグレードしたら、ソリューションをビルドして起動します。</span><span class="sxs-lookup"><span data-stu-id="5409a-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="5409a-511">次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-511">You should see the following error:</span></span>

    <span data-ttu-id="5409a-512">あるこのセクションは、[B] System.web. Web.config......................................</span><span class="sxs-lookup"><span data-stu-id="5409a-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="5409a-513">は、場所 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ ' のコンテキスト ' Default ' にある ' System.web. Web. Razor, Version = 2.0.0.0, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' から生成されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="5409a-514">型 B の生成元は、' 3.0.0.0, Version =, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' というコンテキストで、場所 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_62の既定値 ' になります. ' を指定します。</span><span class="sxs-lookup"><span data-stu-id="5409a-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="5409a-515">上記のエラーを修正するには、プロジェクトの*すべて*の web.config ファイル (Views フォルダー内のファイルを含む) を開き、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="5409a-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="5409a-516">"4.0.0.0" のバージョン "" のすべての出現箇所を "5.0.0.0" に更新します。</span><span class="sxs-lookup"><span data-stu-id="5409a-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="5409a-517">"3.0.0.0" のバージョン "2.0.0.0" のすべての出現箇所を更新し、&quot; を&quot; &quot;して &quot;、"" に変更します。また、</span><span class="sxs-lookup"><span data-stu-id="5409a-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="5409a-518">たとえば、上記の変更を行った後、アセンブリのバインドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="5409a-519">Mvc 4 プロジェクトを MVC 5 にアップグレードする方法については、「 [ASP.NET mvc 4 と WEB Api プロジェクトを ASP.NET mvc 5 および WEB api 2 にアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5409a-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="5409a-520">JQuery の控えめな検証でクライアント側の検証を使用する場合、型 = ' number ' の HTML 入力要素の検証メッセージが正しくないことがあります。</span><span class="sxs-lookup"><span data-stu-id="5409a-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="5409a-521">正しいメッセージではなく有効な数値が入力されている場合は、必要な値 ("Age フィールドが必要") の検証エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="5409a-522">この問題は、Create ビューと Edit ビューで整数プロパティを持つモデルのスキャフォールディングコードでよく見られます。</span><span class="sxs-lookup"><span data-stu-id="5409a-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="5409a-523">この問題を回避するには、エディターヘルパーを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="5409a-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="5409a-524">変更後:</span><span class="sxs-lookup"><span data-stu-id="5409a-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="5409a-525">ASP.NET MVC 5 では、部分信頼はサポートされなくなりました。</span><span class="sxs-lookup"><span data-stu-id="5409a-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="5409a-526">MVC または WebAPI バイナリにリンクするプロジェクトでは、 [Securitytransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性と[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="5409a-527">これらの属性を削除すると、次のようなコンパイラエラーが発生しなくなります。</span><span class="sxs-lookup"><span data-stu-id="5409a-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="5409a-528">この結果、同じアプリケーションで4.0 および5.0 アセンブリを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="5409a-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="5409a-529">すべてを5.0 に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="5409a-530">Web サイトがイントラネットゾーンでホストされている場合、Facebook の承認を持つ SPA テンプレートで IE が不安定になることがある</span><span class="sxs-lookup"><span data-stu-id="5409a-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="5409a-531">SPA テンプレートは、Facebook との外部ログインを提供します。</span><span class="sxs-lookup"><span data-stu-id="5409a-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="5409a-532">テンプレートを使用して作成したプロジェクトがローカルで実行されている場合、サインインすると、IE がクラッシュする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="5409a-533">解決方法:</span><span class="sxs-lookup"><span data-stu-id="5409a-533">Solution:</span></span>

1. <span data-ttu-id="5409a-534">Web サイトをインターネットゾーンでホストします。もしくは</span><span class="sxs-lookup"><span data-stu-id="5409a-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="5409a-535">IE 以外のブラウザーでシナリオをテストします。</span><span class="sxs-lookup"><span data-stu-id="5409a-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="5409a-536">Web フォームのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="5409a-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="5409a-537">Web フォームのスキャフォールディングは VS2013 から削除され、Visual Studio の今後の更新プログラムで使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5409a-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="5409a-538">ただし、MVC の依存関係を追加し、MVC のスキャフォールディングを生成することで、Web フォームプロジェクト内でスキャフォールディングを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="5409a-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="5409a-539">プロジェクトには、Web フォームと MVC の組み合わせが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5409a-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="5409a-540">MVC を Web フォームプロジェクトに追加するには、新しいスキャフォールディングアイテムを追加し、 **[mvc 5 の依存関係]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5409a-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="5409a-541">すべてのコンテンツファイル (スクリプトなど) が必要かどうかに応じて、[最小] または [完全] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5409a-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="5409a-542">次に、MVC のスキャフォールディング item を追加します。これにより、プロジェクトにビューとコントローラーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="5409a-543">MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー</span><span class="sxs-lookup"><span data-stu-id="5409a-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="5409a-544">スキャフォールディング項目をプロジェクトに追加したときにエラーが発生した場合は、プロジェクトが不整合な状態のままになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5409a-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="5409a-545">スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどのその他の変更はロールバックされません。</span><span class="sxs-lookup"><span data-stu-id="5409a-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="5409a-546">ルーティング構成の変更がロールバックされた場合、スキャフォールディング items に移動すると、ユーザーには HTTP 404 エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="5409a-547">対処法:</span><span class="sxs-lookup"><span data-stu-id="5409a-547">Workaround:</span></span>

- <span data-ttu-id="5409a-548">MVC のこのエラーを修正するには、新しいスキャフォールディング項目を追加し、[MVC 5 の依存関係] ([最小] または [完全]) を選択します。</span><span class="sxs-lookup"><span data-stu-id="5409a-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="5409a-549">このプロセスによって、必要なすべての変更がプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5409a-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="5409a-550">このエラーを解決するには、次のように Web API を使用します。</span><span class="sxs-lookup"><span data-stu-id="5409a-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="5409a-551">Webapiconfig.cs クラスをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="5409a-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="5409a-552">次に示すように、global.asax で Webapiconfig.cs をアプリケーション\_に構成します。</span><span class="sxs-lookup"><span data-stu-id="5409a-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
