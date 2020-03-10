---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET and Web Tools 2013.1 for Visual Studio 2012 のリリースノート |Microsoft Docs
author: microsoft
description: このドキュメントでは、Visual Studio 2012 用の ASP.NET and Web Tools 2013.1 のリリースについて説明します。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467104"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="106dc-103">Visual Studio 2012 の ASP.NET と Web 2013.1 ツールのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="106dc-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="106dc-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="106dc-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="106dc-105">このドキュメントでは、Visual Studio 2012 用の ASP.NET and Web Tools 2013.1 のリリースについて説明します。</span><span class="sxs-lookup"><span data-stu-id="106dc-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="106dc-106">内容</span><span class="sxs-lookup"><span data-stu-id="106dc-106">Contents</span></span>

- [<span data-ttu-id="106dc-107">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="106dc-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="106dc-108">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="106dc-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="106dc-109">ASP.NET and Web Tools 2013.1 の新機能 (Visual Studio 2012 用)</span><span class="sxs-lookup"><span data-stu-id="106dc-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="106dc-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="106dc-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="106dc-111">テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="106dc-112">ASP.NET MVC 5 テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="106dc-113">ASP.NET Web API 2 テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="106dc-114">項目テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="106dc-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="106dc-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="106dc-116">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="106dc-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="106dc-117">Razor エディター</span><span class="sxs-lookup"><span data-stu-id="106dc-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="106dc-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="106dc-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="106dc-119">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="106dc-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="106dc-120">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="106dc-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="106dc-121">MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー</span><span class="sxs-lookup"><span data-stu-id="106dc-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="106dc-122">スキャフォールディング項目を追加した後、Web 用の Visual Studio Express 2012 が動作を停止する</span><span class="sxs-lookup"><span data-stu-id="106dc-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="106dc-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="106dc-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="106dc-124">Browse を使用して、または F5 キーを使用して cshtml ファイルを表示すると、サーバーエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="106dc-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="106dc-125">Url の書き換えとチルダ (~)</span><span class="sxs-lookup"><span data-stu-id="106dc-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="106dc-126">テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="106dc-127">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="106dc-127">Installation Notes</span></span>

<span data-ttu-id="106dc-128">[インストール](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)Visual Studio 2012 の場合は ASP.NET and Web Tools 2013.1。</span><span class="sxs-lookup"><span data-stu-id="106dc-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="106dc-129">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="106dc-129">Software Requirements</span></span>

<span data-ttu-id="106dc-130">Visual Studio 2012 を使用しているか、Web 用に Visual Studio Express 2012 が必要です。</span><span class="sxs-lookup"><span data-stu-id="106dc-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="106dc-131">ASP.NET and Web Tools 2013.1 の新機能 (Visual Studio 2012 用)</span><span class="sxs-lookup"><span data-stu-id="106dc-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="106dc-132">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="106dc-132">Bootstrap</span></span>

<span data-ttu-id="106dc-133">MVC 5 コントローラーとビューをスキャフォールディングした場合、ビューのマークアップでは[ブートストラップ](http://getbootstrap.com/)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="106dc-134">テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="106dc-135">ASP.NET MVC 5 テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="106dc-136">新しい MVC 5 テンプレートを追加しました。</span><span class="sxs-lookup"><span data-stu-id="106dc-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="106dc-137">最新の MVC 5 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。</span><span class="sxs-lookup"><span data-stu-id="106dc-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="106dc-138">ASP.NET Web API 2 テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="106dc-139">新しい Web API 2 テンプレートを追加しました。</span><span class="sxs-lookup"><span data-stu-id="106dc-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="106dc-140">最新の Web API 2 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。</span><span class="sxs-lookup"><span data-stu-id="106dc-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="106dc-141">項目テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-141">Item Templates</span></span>

<span data-ttu-id="106dc-142">MVC 5 ビュー、Web ページ (Razor 3)、および Web API 2 コントローラー用の新しい項目テンプレートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="106dc-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="106dc-143">新しい項目を追加するときに、関連する NuGet パッケージをプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="106dc-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="106dc-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="106dc-144">Entity Framework 6</span></span>

<span data-ttu-id="106dc-145">Entity Framework を使用して MVC または Web API コントローラーをスキャフォールディングする場合は、フレームワーク6を使用します。</span><span class="sxs-lookup"><span data-stu-id="106dc-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="106dc-146">Entity Framework の詳細については、 [Entity Framework のバージョン履歴](https://msdn.com/data/jj574253)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="106dc-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="106dc-147">Entity Framework 6 Tools for Visual Studio 2012 をダウンロードしてインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="106dc-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="106dc-148">「 [Get Entity Framework](https://msdn.com/data/ee712906#tooling)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="106dc-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="106dc-149">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="106dc-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="106dc-150">ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="106dc-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="106dc-151">これにより、データモデルと対話する定型コードをプロジェクトに簡単に追加できるようになります。</span><span class="sxs-lookup"><span data-stu-id="106dc-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="106dc-152">以前のバージョンの Visual Studio では、スキャフォールディングは ASP.NET MVC プロジェクトに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="106dc-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="106dc-153">この更新プログラムでは、Web フォームを含む任意の ASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="106dc-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="106dc-154">この更新プログラムは、Web フォームプロジェクトのページの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加することで、Web フォームでスキャフォールディングを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="106dc-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="106dc-155">Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。</span><span class="sxs-lookup"><span data-stu-id="106dc-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="106dc-156">スキャフォールディングを使用する場合は、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="106dc-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="106dc-157">たとえば、ASP.NET の Web フォームプロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な NuGet パッケージと参照がプロジェクトに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="106dc-158">MVC スキャフォールディングを Web フォームプロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログウィンドウで **[Mvc 5 の依存関係]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="106dc-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="106dc-159">MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。</span><span class="sxs-lookup"><span data-stu-id="106dc-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="106dc-160">[最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="106dc-161">[完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="106dc-162">非同期コントローラーのスキャフォールディングのサポートには、Entity Framework 6 の新しい非同期機能が使用されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="106dc-163">詳細とチュートリアルについては、「 [ASP.NET スキャフォールディングの概要](../2013/aspnet-scaffolding-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="106dc-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="106dc-164">これらのチュートリアルでは Visual Studio 2013 を使用したスキャフォールディングを示していますが、Visual Studio 2012 の ASP.NET and Web Tools 2013.1 にも適用できます。</span><span class="sxs-lookup"><span data-stu-id="106dc-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="106dc-165">Razor エディター</span><span class="sxs-lookup"><span data-stu-id="106dc-165">Razor Editor</span></span>

<span data-ttu-id="106dc-166">この更新プログラムでは、Visual Studio 2012 で Razor 3 ツール/編集がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="106dc-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="106dc-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="106dc-167">NuGet 2.7</span></span>

<span data-ttu-id="106dc-168">NuGet 2.7 には新機能の豊富なセットが含まれています。詳細については、「 [nuget 2.7 のリリースノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="106dc-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="106dc-169">このバージョンの NuGet では、不足しているパッケージの復元を NuGet に明示的に許可する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="106dc-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="106dc-170">NuGet 2.7 をインストールすると、ユーザーは、不足しているパッケージを自動的に復元することに同意したことになります。</span><span class="sxs-lookup"><span data-stu-id="106dc-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="106dc-171">ユーザーは、Visual Studio の NuGet 設定を使用して、パッケージの復元を明示的に無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="106dc-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="106dc-172">この変更により、パッケージの復元のしくみが簡略化されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="106dc-173">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="106dc-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="106dc-174">ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="106dc-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="106dc-175">MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー</span><span class="sxs-lookup"><span data-stu-id="106dc-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="106dc-176">スキャフォールディング項目をプロジェクトに追加するときにエラーが発生した場合は、プロジェクトが不整合な状態のままになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="106dc-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="106dc-177">スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどのその他の変更はロールバックされません。</span><span class="sxs-lookup"><span data-stu-id="106dc-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="106dc-178">ルーティング構成の変更がロールバックされた場合、スキャフォールディング items に移動すると、ユーザーには HTTP 404 エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="106dc-179">MVC のこのエラーを修正するには、新しいスキャフォールディング項目を追加し、[MVC 5 の依存関係] ([最小] または [完全]) を選択します。</span><span class="sxs-lookup"><span data-stu-id="106dc-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="106dc-180">このプロセスによって、必要なすべての変更がプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="106dc-181">このエラーを解決するには、次のように Web API を使用します。</span><span class="sxs-lookup"><span data-stu-id="106dc-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="106dc-182">次の Webapiconfig.cs クラスをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="106dc-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="106dc-183">次に示すように、global.asax で Webapiconfig.cs をアプリケーション\_に構成します。</span><span class="sxs-lookup"><span data-stu-id="106dc-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="106dc-184">スキャフォールディング項目を追加した後、Web 用の Visual Studio Express 2012 が動作を停止する</span><span class="sxs-lookup"><span data-stu-id="106dc-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="106dc-185">Entity Framework (Web API 2 コントローラーなど) を使用してスキャフォールディング item を Entity Framework を使用して追加した後、Web 用の Visual Studio Express 2012 が動作しなくなった場合は、Visual Studio Express がアセンブリのネイティブイメージを読み込むことができなかった可能性があります。System.web. 拡張子に依存します。</span><span class="sxs-lookup"><span data-stu-id="106dc-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="106dc-186">この問題を解決するには、Visual Studio Express を構成して、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="106dc-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="106dc-187">管理者モードでコマンドプロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="106dc-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="106dc-188">%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE または% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (64 ビット Windows の場合) にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="106dc-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="106dc-189">テキストエディターで VWDExpress を開きます。</span><span class="sxs-lookup"><span data-stu-id="106dc-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="106dc-190">&lt;構成&gt;の下に次の行を追加し /&lt;runtime&gt; 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="106dc-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="106dc-191">Web 用に 2012 Visual Studio Express を再起動します。</span><span class="sxs-lookup"><span data-stu-id="106dc-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="106dc-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="106dc-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="106dc-193">Browse を使用して、または F5 キーを使用して cshtml ファイルを表示すると、サーバーエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="106dc-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="106dc-194">Visual Studio 2012 で MVC 5 プロジェクトを作成した場合 (Visual Studio 2013 で作成された MVC 5 プロジェクトで Visual Studio 2012 を開いている場合)、Browse With または F5 を使用して cshtml ファイルを表示しようとすると、 **'/' アプリケーションで-Server error**というエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="106dc-195">サーバーが `http://localhost:XXXX/Views/../XXXX.cshtml` に移動しようとしています</span><span class="sxs-lookup"><span data-stu-id="106dc-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="106dc-196">この問題を解決するには、プロジェクトの **[開始アクション]** 設定を [**特定] ページ**に変更します。</span><span class="sxs-lookup"><span data-stu-id="106dc-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="106dc-197">ページの値を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="106dc-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="106dc-198">この変更を行った後、F5 キーを押すと、アプリケーションのルート (`http://localhost:XXXX`) に移動します。</span><span class="sxs-lookup"><span data-stu-id="106dc-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="106dc-199">この動作は Visual Studio 2013 の MVC 5 プロジェクトの動作と同じではありません。**現在のページ**の設定によって、開いているページが起動します。</span><span class="sxs-lookup"><span data-stu-id="106dc-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="106dc-200">Url の書き換えとチルダ (~)</span><span class="sxs-lookup"><span data-stu-id="106dc-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="106dc-201">ASP.NET Razor 3 または ASP.NET MVC 5 にアップグレードした後、URL リライトを使用していると、チルダ (~) 表記が正しく機能しなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="106dc-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="106dc-202">URL 書き換えは、&lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;などの HTML 要素のチルダ (~) 表記に影響します。その結果、チルダはルートディレクトリにマップされなくなります。</span><span class="sxs-lookup"><span data-stu-id="106dc-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="106dc-203">たとえば、 **asp.net/content**の要求を**asp.net**に書き換えると、href = "~/content/"/&gt; &lt;の href 属性は、 **/** ではなく、/ **content/content/** に解決されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="106dc-204">この変更を行わないようにするには、各 Web ページまたは**アプリケーション\_BeginRequest**内の**IIS\_** にある、IIS によって書き換えられたコンテキストを false に設定します。</span><span class="sxs-lookup"><span data-stu-id="106dc-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="106dc-205">テンプレート</span><span class="sxs-lookup"><span data-stu-id="106dc-205">Templates</span></span>

<span data-ttu-id="106dc-206">Windows 8.1 または Windows Server 2012 R2 で Visual Studio 2012 を使用して ASP.NET MVC プロジェクトを作成すると、Visual Studio に "ASP.NET 4.5 の Web [url] の構成に失敗しました" というエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="106dc-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![構成エラー](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="106dc-208">このエラーが表示されるのは、Visual Studio 2012 では、ASP.NET 4.5 機能が Windows のこれらのリリースにインストールされている場合には有効にならないためです。</span><span class="sxs-lookup"><span data-stu-id="106dc-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="106dc-209">ASP.NET 4.5 を有効にするには、「 [Windows の機能の有効化または無効化](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)」で説明されている手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="106dc-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows の機能を有効または無効にする](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="106dc-211">または、コマンドラインを使用して ASP.NET 4.5 を有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="106dc-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="106dc-212">管理者モードでコマンドプロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="106dc-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="106dc-213">次のコマンドを実行して、ASP.NET 4.5 を有効にします。</span><span class="sxs-lookup"><span data-stu-id="106dc-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
