---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、Visual Studio 2010 用の ASP.NET MVC 4 Beta のリリースについて説明します。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419842"
---
# <a name="aspnet-mvc-4"></a><span data-ttu-id="ab01d-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ab01d-103">ASP.NET MVC 4</span></span>

> <span data-ttu-id="ab01d-104">このドキュメントでは、Visual Studio 2010 用の ASP.NET MVC 4 Beta のリリースについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="ab01d-105">これは、最新のリリースではありません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-105">This is not the most current release.</span></span> <span data-ttu-id="ab01d-106">ASP.NET MVC 4 RC のリリースノートについては、[こちら](mvc4-release-notes.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>

- [<span data-ttu-id="ab01d-107">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="ab01d-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="ab01d-108">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="ab01d-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="ab01d-109">サポート</span><span class="sxs-lookup"><span data-stu-id="ab01d-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="ab01d-110">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="ab01d-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="ab01d-111">ASP.NET MVC 3 プロジェクトを ASP.NET MVC 4 にアップグレードする</span><span class="sxs-lookup"><span data-stu-id="ab01d-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="ab01d-112">ASP.NET MVC 4 Beta の新機能</span><span class="sxs-lookup"><span data-stu-id="ab01d-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="ab01d-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ab01d-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="ab01d-114">ASP.NET シングルページアプリケーション</span><span class="sxs-lookup"><span data-stu-id="ab01d-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="ab01d-115">既定のプロジェクトテンプレートの機能強化</span><span class="sxs-lookup"><span data-stu-id="ab01d-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="ab01d-116">モバイルプロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="ab01d-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="ab01d-117">表示モード</span><span class="sxs-lookup"><span data-stu-id="ab01d-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="ab01d-118">jQuery Mobile、ビュースイッチャー、およびブラウザーのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="ab01d-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="ab01d-119">Visual Studio でのコード生成のためのレシピ</span><span class="sxs-lookup"><span data-stu-id="ab01d-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="ab01d-120">非同期コントローラーのタスクサポート</span><span class="sxs-lookup"><span data-stu-id="ab01d-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="ab01d-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="ab01d-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="ab01d-122">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="ab01d-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="ab01d-123">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="ab01d-123">Installation Notes</span></span>

<span data-ttu-id="ab01d-124">ASP.NET MVC 4 Beta for Visual Studio 2010 は、Web Platform Installer を使用して[ASP.NET mvc 4 ホームページ](../mvc/mvc4.md)からインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="ab01d-125">ASP.NET MVC 4 Beta をインストールする前に、以前にインストールされた ASP.NET MVC 4 のプレビューをアンインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="ab01d-126">このリリースは、.NET Framework 4.5 Developer Preview と互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="ab01d-127">ASP.NET MVC 4 Beta をインストールする前に、.NET 4.5 Developer Preview をアンインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="ab01d-128">ASP.NET MVC 4 はインストールでき、ASP.NET MVC 3 とサイドバイサイドで実行できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="ab01d-129">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="ab01d-129">Documentation</span></span>

<span data-ttu-id="ab01d-130">ASP.NET MVC のドキュメントについては、次の URL で MSDN Web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="ab01d-131">ASP.NET MVC に関するチュートリアルやその他の情報については、ASP.NET web サイト ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)) の mvc 4 ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="ab01d-132">サポート</span><span class="sxs-lookup"><span data-stu-id="ab01d-132">Support</span></span>

<span data-ttu-id="ab01d-133">これはプレビューリリースであり、公式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="ab01d-134">このリリースの使用についてご質問がある場合は、ASP.NET MVC フォーラム ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) に投稿してください。 ASP.NET コミュニティのメンバーは、多くの場合、非公式のサポートを提供できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="ab01d-135">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="ab01d-135">Software Requirements</span></span>

<span data-ttu-id="ab01d-136">Visual Studio の ASP.NET MVC 4 コンポーネントには、PowerShell 2.0、Visual Studio 2010 Service Pack 1、または Visual Web Developer Express 2010 Service Pack 1 が必要です。</span><span class="sxs-lookup"><span data-stu-id="ab01d-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="ab01d-137">ASP.NET  4、ASP.NET MVC 3 プロジェクトをアップグレードします。</span><span class="sxs-lookup"><span data-stu-id="ab01d-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="ab01d-138">ASP.NET MVC 4 は、ASP.NET MVC 3 とサイドバイサイドで同じコンピューターにインストールできます。これにより、ASP.NET MVC 3 アプリケーションを ASP.NET MVC 4 にアップグレードするタイミングを柔軟に選択できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="ab01d-139">アップグレードする最も簡単な方法は、新しい ASP.NET MVC 4 プロジェクトを作成し、既存の MVC 3 プロジェクトのすべてのビュー、コントローラー、コード、コンテンツファイルを新しいプロジェクトにコピーしてから、新しいプロジェクトのアセンブリ参照を古いプロジェクトに一致するように更新することです。</span><span class="sxs-lookup"><span data-stu-id="ab01d-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="ab01d-140">MVC 3 プロジェクトの web.config ファイルに変更を加えた場合は、それらの変更を MVC 4 プロジェクトの web.config ファイルにマージする必要もあります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="ab01d-141">既存の ASP.NET MVC 3 アプリケーションをバージョン4に手動でアップグレードするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="ab01d-142">プロジェクトのすべての web.config ファイル (プロジェクトのルートに1つ、[Views] フォルダーに1つ、プロジェクト内の各領域の [Views] フォルダーに1つ) で、次のテキストのすべてのインスタンスを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="ab01d-143">には、次の対応するテキストがあります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="ab01d-144">ルートの Web.config ファイルで、Web*ページ: Version*要素を "2.0.0.0" に更新し、値 "true" を持つ新しい*PreserveLoginUrl*キーを追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="ab01d-145">ソリューションエクスプローラーで、(バージョン3の DLL を指す) *system.web. Mvc*への参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="ab01d-146">次に、4.0.0.0 (v) に*参照を追加*します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="ab01d-147">特に、アセンブリ参照を更新するには、次の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="ab01d-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="ab01d-148">これらについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-148">Here are the details:</span></span>

    1. <span data-ttu-id="ab01d-149">ソリューションエクスプローラーで、次のアセンブリへの参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="ab01d-150">*System.web. Mvc*(v 3.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-151">*System.web. Web ページ*(1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-152">*System.web. Razor*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-153">*System.web. Web ページ*(1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-154">*System.web. Web ページ*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="ab01d-155">次のアセンブリへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="ab01d-156">*System.web. Mvc*(v 4.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-157">*System.web. Web ページ*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-158">*System.web. Razor*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-159">*System.web. Web ページ. 配置*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ab01d-160">*System.web. Web ページ*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="ab01d-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="ab01d-161">ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="ab01d-162">次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="ab01d-163">*Projecttypeguids*要素を見つけ、{E53F8FEA-EAE0-44A6-8774-FFD645390401} を {E3E379DF-F4C6-4180-9B81-6769533ABE47} に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="ab01d-164">変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じて、プロジェクトを右クリックし、[プロジェクトの再読み込み] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="ab01d-165">以前のバージョンの ASP.NET MVC を使用してコンパイルされたサードパーティ製のライブラリをプロジェクトが参照する場合は、ルートの Web.config ファイルを開き、*構成*セクションの下に次の3つの*bindingRedirect*要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="ab01d-166">ASP.NET MVC 4 Beta の新機能</span><span class="sxs-lookup"><span data-stu-id="ab01d-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="ab01d-167">このセクションでは、ASP.NET MVC 4 ベータリリースで導入された機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="ab01d-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ab01d-168">ASP.NET Web API</span></span>

<span data-ttu-id="ab01d-169">ASP.NET MVC 4 には、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを作成するための新しいフレームワークである ASP.NET Web API が含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="ab01d-170">ASP.NET Web API は、RESTful サービスを構築するための最適なプラットフォームでもあります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="ab01d-171">ASP.NET Web API には、次の機能のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="ab01d-172">**最新の HTTP プログラミングモデル:** 新しい厳密に型指定された HTTP オブジェクトモデルを使用して、Web Api の HTTP 要求と応答に直接アクセスして操作します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="ab01d-173">新しい HttpClient 型を使用して、クライアントで同じプログラミングモデルと HTTP パイプラインを対称的に使用できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="ab01d-174">**ルートの完全なサポート**: web api では、ルートパラメーターや制約など、常に web スタックの一部であるルート機能の完全なセットがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="ab01d-175">また、アクションへのマッピングでは規約が完全にサポートされているため、[HttpPost] などの属性をクラスやメソッドに適用する必要がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="ab01d-176">**コンテンツネゴシエーション**: クライアントとサーバーは連携して、API から返されるデータの適切な形式を判断できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="ab01d-177">XML、JSON、およびフォームの URL エンコード形式の既定のサポートが用意されています。独自のフォーマッタを追加することによって、このサポートを拡張することも、既定のコンテンツネゴシエーション戦略を置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="ab01d-178">**モデルのバインドと検証:** モデルバインダーを使用すると、HTTP 要求のさまざまな部分からデータを抽出し、それらのメッセージ部分を .NET オブジェクトに変換して、Web API アクションで使用できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="ab01d-179">**フィルター:** Web Api では、[承認] 属性などの既知のフィルターを含むフィルターがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="ab01d-180">アクション、承認、および例外処理のために、独自のフィルターを作成してプラグインすることができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="ab01d-181">**クエリの構成:** IQueryable&lt;T&gt;を返すだけで、Web API は OData URL 規則を使用したクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ab01d-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="ab01d-182">**HTTP 詳細のテストの容易性の向上:** 静的コンテキストオブジェクトで HTTP の詳細を設定するのではなく、Web API アクションを HttpRequestMessage および HttpResponseMessage のインスタンスと共に使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="ab01d-183">これらのオブジェクトのジェネリックバージョンは、HTTP 型に加えてカスタム型を操作できるようにするためにも存在します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="ab01d-184">**DependencyResolver を使用したコントロールの反転 (IoC) の向上:** Web API では、MVC の依存関係競合回避モジュールによって実装されたサービスロケーターパターンを使用して、さまざまな機能のインスタンスを取得するようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="ab01d-185">**コードベースの構成:** Web API の構成はコードを使用してのみ実行され、構成ファイルはクリーンなままになります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="ab01d-186">**自己ホスト:** Web api は、IIS だけでなく、独自のプロセスでホストすることもできます。また、Web API のルートやその他の機能を最大限に活用できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="ab01d-187">の詳細については ASP.NET Web API [https://www.asp.net/web-api](../web-api/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="ab01d-188">ASP.NET シングルページアプリケーション</span><span class="sxs-lookup"><span data-stu-id="ab01d-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="ab01d-189">ASP.NET MVC 4 には、JavaScript と Web Api を使用して、クライアント側の重要な対話機能を備えたシングルページアプリケーションを構築するための初期プレビューが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="ab01d-190">このサポートには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-190">This support includes:</span></span>

- <span data-ttu-id="ab01d-191">キャッシュされたデータとのより高度なローカル操作のための JavaScript ライブラリのセット</span><span class="sxs-lookup"><span data-stu-id="ab01d-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="ab01d-192">作業単位と DAL のサポートのための追加の Web API コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ab01d-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="ab01d-193">すぐに作業を開始するためのスキャフォールディングを含む MVC プロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="ab01d-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="ab01d-194">ASP.NET MVC 4 のシングルページアプリケーションサポートの詳細については、 [https://www.asp.net/single-page-application](../single-page-application/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="ab01d-195">既定のプロジェクトテンプレートの機能強化</span><span class="sxs-lookup"><span data-stu-id="ab01d-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="ab01d-196">新しい ASP.NET MVC 4 プロジェクトを作成するために使用されるテンプレートは、最新の web サイトを作成するように更新されました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="ab01d-197">表面的な機能強化に加えて、新しいテンプレートの機能が強化されています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="ab01d-198">このテンプレートは、デスクトップブラウザーとモバイルブラウザーの両方で適切に表示されるように、アダプティブレンダリングと呼ばれる手法を採用しています。カスタマイズは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="ab01d-199">アダプティブレンダリングが動作していることを確認するには、モバイルエミュレーターを使用するか、デスクトップブラウザーウィンドウのサイズを小さくしてみてください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="ab01d-200">ブラウザーウィンドウのサイズが十分に小さくなると、ページのレイアウトが変わります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="ab01d-201">既定のプロジェクトテンプレートのもう1つの拡張機能は、JavaScript を使用して豊富な UI を提供することです。</span><span class="sxs-lookup"><span data-stu-id="ab01d-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="ab01d-202">テンプレートで使用されるログインリンクとレジスタリンクは、jQuery UI ダイアログを使用してリッチログイン画面を表示する方法の例です。</span><span class="sxs-lookup"><span data-stu-id="ab01d-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="ab01d-203">モバイルプロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="ab01d-203">Mobile Project Template</span></span>

<span data-ttu-id="ab01d-204">新しいプロジェクトを開始していて、モバイルおよびタブレットのブラウザー専用のサイトを作成する場合は、[新しいモバイルアプリケーション] プロジェクトテンプレートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="ab01d-205">これは、タッチに最適化された UI を構築するためのオープンソースライブラリである jQuery Mobile に基づいています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="ab01d-206">このテンプレートには、インターネットアプリケーションテンプレートと同じアプリケーション構造が含まれています (コントローラーコードは実質的に同じです) が、jQuery Mobile を使用してスタイルを適用し、タッチベースのモバイルデバイスで適切に動作します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="ab01d-207">モバイル UI を構造化およびスタイルする方法の詳細については、 [JQuery mobile プロジェクトの web サイト](http://jquerymobile.com/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="ab01d-208">モバイル最適化されたビューを追加するデスクトップ指向サイトが既にある場合、またはデスクトップとモバイルのブラウザーに異なるスタイルのビューを提供する1つのサイトを作成する場合は、新しい表示モード機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="ab01d-209">(次のセクションを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="ab01d-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="ab01d-210">表示モード</span><span class="sxs-lookup"><span data-stu-id="ab01d-210">Display Modes</span></span>

<span data-ttu-id="ab01d-211">新しい表示モード機能を使用すると、アプリケーションは、要求を行っているブラウザーに応じて、ビューを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="ab01d-212">たとえば、デスクトップブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.cshtml テンプレートを使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="ab01d-213">モバイルブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.mobile.cshtml テンプレートを返すことがあります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="ab01d-214">また、レイアウトとパーシャルは、特定のブラウザーの種類に対してオーバーライドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="ab01d-215">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-215">For example:</span></span>

- <span data-ttu-id="ab01d-216">Views\Shared フォルダーに \_Layout と \_Layout の両方のテンプレートが含まれている場合、既定では、アプリケーションは、モバイルブラウザーからの要求中に \_を使用し、他の要求時には \_を使用します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="ab01d-217">フォルダーに \_MyPartial. cshtml と \_MyPartial.\_の両方が含まれている場合、命令 @Html.Partial("MyPartial") は、モバイルブラウザーからの要求時に MyPartial を表示し、他の要求では MyPartial. cshtml を \_します。\_</span><span class="sxs-lookup"><span data-stu-id="ab01d-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="ab01d-218">他のデバイスの特定のビュー、レイアウト、または部分ビューを作成する場合は、新しい*Defaultdisplaymode*インスタンスを登録して、要求が特定の条件を満たすときに検索する名前を指定できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="ab01d-219">たとえば、次のコードを*アプリケーション\_* の global.asax ファイルに追加して、Apple iPhone ブラウザーが要求を行うときに適用される表示モードとして文字列 "iPhone" を登録することができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="ab01d-220">このコードを実行すると、Apple iPhone ブラウザーが要求を行うときに、アプリケーションで Views\Shared\\_Layout (存在する場合) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="ab01d-221">jQuery Mobile、ビュースイッチャー、およびブラウザーのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="ab01d-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="ab01d-222">jQuery Mobile は、タッチに最適化された web UI を構築するためのオープンソースライブラリです。</span><span class="sxs-lookup"><span data-stu-id="ab01d-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="ab01d-223">ASP.NET MVC 4 アプリケーションで jQuery Mobile を使用する場合は、作業の開始に役立つ NuGet パッケージをダウンロードしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="ab01d-224">Visual Studio パッケージマネージャーコンソールからインストールするには、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="ab01d-225">これにより、jQuery Mobile と、次のようなヘルパーファイルがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="ab01d-226">Views/Shared/\_Layout。これは jQuery モバイルベースのレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="ab01d-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="ab01d-227">Views/Shared/\_ViewSwitcher. cshtml partial ビューと ViewSwitcherController.cs controller で構成されるビュースイッチャーコンポーネント。</span><span class="sxs-lookup"><span data-stu-id="ab01d-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="ab01d-228">パッケージをインストールした後、モバイルブラウザーを使用してアプリケーションを実行します (または、Firefox[ユーザーエージェントスイッチャー](http://chrispederick.com/work/user-agent-switcher/)アドオンなどの同等のものを使用します)。</span><span class="sxs-lookup"><span data-stu-id="ab01d-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="ab01d-229">JQuery Mobile はレイアウトとスタイル設定を処理するため、ページの外観が大きく異なることがわかります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="ab01d-230">この機能を利用するには、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="ab01d-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="ab01d-231">前の「[表示モード](#_Toc303253810)」で説明されているように、モバイル固有のビューの上書きを作成します (たとえば、モバイルブラウザーの Views\Home\Index.cshtml を上書きするように Views\Home\Index.mobile.cshtml を作成します)。</span><span class="sxs-lookup"><span data-stu-id="ab01d-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="ab01d-232">タッチに最適化された UI 要素をモバイルビューに追加する方法の詳細については、 [JQuery Mobile のドキュメント](http://jquerymobile.com/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab01d-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="ab01d-233">モバイルで最適化された web ページの規則としては、ユーザーがデスクトップバージョンのページに切り替えることができるように、デスクトップビューや完全サイトモードなどのテキストを持つリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="ab01d-234">JQuery パッケージには、この目的のためのサンプルのビュースイッチャーコンポーネントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="ab01d-235">これは、既定の Views\Shared\\_Layout で使用されます。これは、ページが表示されたときの次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="ab01d-236">ビジターがリンクをクリックすると、同じページのデスクトップバージョンに切り替わります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="ab01d-237">既定では、デスクトップレイアウトにはビュースイッチャーが含まれないため、訪問者はモバイルモードに戻ることができません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="ab01d-238">これを有効にするには、 *\_ViewSwitcher*への次の参照を、 *&lt;body&gt;* 要素の内側にあるデスクトップレイアウトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="ab01d-239">ビュースイッチャーは、ブラウザーのオーバーライドと呼ばれる新しい機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="ab01d-240">この機能を使用すると、アプリケーションは、実際のものとは異なるブラウザー (ユーザーエージェント) からの要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="ab01d-241">次の表に、ブラウザーがオーバーライドするメソッドを示します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="ab01d-242">指定されたユーザー エージェントを使用して、要求の実際のユーザー エージェント値をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="ab01d-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="ab01d-243">要求のユーザーエージェントのオーバーライド値、またはオーバーライドが指定されていない場合は実際のユーザーエージェント文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="ab01d-244">要求に対して現在設定されているユーザーエージェントに対応する*HttpBrowserCapabilitiesBase*インスタンスを返します (実際またはオーバーライドされます)。</span><span class="sxs-lookup"><span data-stu-id="ab01d-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="ab01d-245">この値を使用して、 *IsMobileDevice*などのプロパティを取得できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="ab01d-246">現在の要求でオーバーライドされたユーザー エージェントがあれば削除します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="ab01d-247">ブラウザーのオーバーライドは ASP.NET MVC 4 の中核機能であり、jQuery パッケージをインストールしない場合でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="ab01d-248">ただし、ビュー、レイアウト、および部分ビューの選択にのみ影響します *。 Browser*オブジェクトに依存する他の ASP.NET 機能には影響しません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="ab01d-249">既定では、ユーザーエージェントのオーバーライドは cookie を使用して格納されます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="ab01d-250">(たとえば、データベースで) 上書きを別の場所に保存する場合は、既定のプロバイダー (*Browseroverridestores. Current*) を置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="ab01d-251">このプロバイダーのドキュメントは、ASP.NET MVC の今後のリリースに付属しています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="ab01d-252">Visual Studio でのコード生成のためのレシピ</span><span class="sxs-lookup"><span data-stu-id="ab01d-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="ab01d-253">新しいレシピ機能により、Visual Studio は、NuGet を使用してインストールできるパッケージに基づいて、ソリューション固有のコードを生成できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="ab01d-254">レシピフレームワークを使用すると、開発者はコード生成プラグインを簡単に記述できるようになります。このプラグインを使用すると、追加領域、コントローラーの追加、ビューの追加用の組み込みのコードジェネレーターを置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="ab01d-255">レシピは NuGet パッケージとして配置されるため、簡単にソース管理にチェックインし、プロジェクトのすべての開発者と共有することができます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="ab01d-256">また、ソリューションごとに使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="ab01d-257">非同期コントローラーのタスクサポート</span><span class="sxs-lookup"><span data-stu-id="ab01d-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="ab01d-258">*ActionResult&gt;&lt;* *型の*オブジェクトを返す単一のメソッドとして、非同期アクションメソッドを記述できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="ab01d-259">たとえば、Visual C# 5 (または[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)を使用) を使用している場合は、次のような非同期アクションメソッドを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="ab01d-260">前のアクションメソッドでは、 *NewsService async*と*sportsService*の呼び出しは非同期に呼び出され、スレッドプールからのスレッドはブロックされません。</span><span class="sxs-lookup"><span data-stu-id="ab01d-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="ab01d-261">*タスク*インスタンスを返す非同期アクションメソッドは、タイムアウトをサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="ab01d-262">アクションメソッドをキャンセル可能なにするには、アクションメソッドシグネチャに*CancellationToken*型のパラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="ab01d-263">次の例は、タイムアウトが2500ミリ秒で、タイムアウトが発生した場合に*TimedOut*ビューをクライアントに表示する非同期アクションメソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="ab01d-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="ab01d-264">Azure SDK</span></span>

<span data-ttu-id="ab01d-265">ASP.NET MVC 4 Beta では、Windows Azure SDK の9月 2011 1.5 リリースがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="ab01d-266">既知の問題と重大な変更</span><span class="sxs-lookup"><span data-stu-id="ab01d-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="ab01d-267">**ASP.NET MVC 4 Beta をインストールすると、Visual Studio 2010 Service Pack 1 の cshtml/vbhtml エディターの cshtml/VBHTML エディターが、cshtml または VBHTML ファイル内にスニペットまたは JavaScript を入力した後、長い時間一時停止する場合があります。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="ab01d-268">これは、作成されたばかりでまだコンパイルされていない ASP.NET MVC 4 アプリケーションでのみ発生します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="ab01d-269">この回避策は、プロジェクトをコンパイルして bin フォルダー内のアセンブリを取得することです。</span><span class="sxs-lookup"><span data-stu-id="ab01d-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="ab01d-270">Bin フォルダーからアセンブリを削除するプロジェクトをクリーニングすると、エディターの問題が返されます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="ab01d-271">これは、次のリリースで修正される予定です。</span><span class="sxs-lookup"><span data-stu-id="ab01d-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="ab01d-272">**C#Visual Studio 11 Beta のプロジェクトテンプレートに、Global.asax.cs に正しくない接続文字列が含まれています。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="ab01d-273">Visual Studio 11 Beta で作成されたプロジェクトの Application\_Start メソッドに指定された既定の接続には、エスケープされていない円記号 (\) 文字を含む LocalDB 接続文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ab01d-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="ab01d-274">この結果、SqlException を生成する DbContext Entity Framework にアクセスしようとすると接続エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="ab01d-275">この問題を解決するには、次のように読み取られるように、App\_Start メソッドで円記号をエスケープします。</span><span class="sxs-lookup"><span data-stu-id="ab01d-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="ab01d-276">**.Net 4.5 を対象とする ASP.NET MVC 4 アプリケーションは、.NET 4.0 で実行されるときに FileLoadException アセンブリにアクセスしようとすると、をスローします。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="ab01d-277">.NET 4.5 で作成された ASP.NET MVC 4 アプリケーションには、バインドリダイレクトが含まれています。これにより、"ファイルまたはアセンブリ ' FileLoadException ' またはその依存関係の1つを読み込めませんでした。" という状態になります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="ab01d-278">.NET 4.0 がインストールされているシステムでアプリケーションを実行する場合。</span><span class="sxs-lookup"><span data-stu-id="ab01d-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="ab01d-279">この問題を解決するには、web.config から次のバインドリダイレクトを削除します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="ab01d-280">変更した web.config のアセンブリバインド要素は、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="ab01d-281"><strong>Visual Basic プロジェクトの "コントローラーの追加" 項目テンプレートは、領域内から呼び出されたときに正しくない名前空間を生成し</strong><strong>ます。</strong></span><span class="sxs-lookup"><span data-stu-id="ab01d-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="ab01d-282">Visual Basic を使用する ASP.NET MVC プロジェクトの領域にコントローラーを追加すると、項目テンプレートによって、コントローラーに間違った名前空間が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="ab01d-283">コントローラーのアクションに移動すると、"ファイルが見つかりません" というエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="ab01d-284">生成された名前空間は、ルート名前空間の後にあるすべてのものを省略します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="ab01d-285">たとえば、生成される名前空間は*RootNamespace*ですが、 *RootNamespace*である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="ab01d-286">**Razor ビューエンジンでの重大な変更。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="ab01d-287">Razor パーサーの書き換えの一環として、次の型が*system.web*から削除されました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="ab01d-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="ab01d-288">*ModelSpan*</span></span>
    - <span data-ttu-id="ab01d-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="ab01d-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="ab01d-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="ab01d-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="ab01d-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="ab01d-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="ab01d-292">次のメソッドも削除されました。</span><span class="sxs-lookup"><span data-stu-id="ab01d-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="ab01d-293">*MvcCSharpRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="ab01d-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="ab01d-294">*MvcWebPageRazorHost (RazorCodeGenerator) のようになります。*</span><span class="sxs-lookup"><span data-stu-id="ab01d-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="ab01d-295">*MvcVBRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="ab01d-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="ab01d-296">**ASP.NET MVC 4 アプリの/bin ディレクトリに WebData が含まれている場合、フォーム認証の URL が引き継がれます。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="ab01d-297">WebData アセンブリをアプリケーションに追加する ([配置可能な依存関係の追加] ダイアログボックスを使用して [Razor 構文を使用する] を ASP.NET Web ページ選択するなど) と、既定の ASP.NET MVC アカウントコントローラーによって想定されているように、/account/ログインではなく、認証ログインリダイレクトがオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="ab01d-298">この動作を回避し、web.config の認証セクションに既に指定されている URL を使用するには、PreserveLoginUrl という名前の appSetting を追加し、それを true に設定します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="ab01d-299">**Visual Studio 2010 と Visual Web Developer 2010 をサイドバイサイドでインストールするために ASP.NET MVC 4 をインストールしようとすると、NuGet パッケージマネージャーのインストールが失敗します。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="ab01d-300">Visual Studio 2010 と Visual Web Developer 2010 を ASP.NET MVC 4 とサイドバイサイドで実行するには、Visual Studio の両方のバージョンが既にインストールされていると、ASP.NET MVC 4 をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="ab01d-301">**前提条件が既にアンインストールされている場合、ASP.NET MVC 4 のアンインストールは失敗します。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="ab01d-302">ASP.NET MVC 4you 正常にアンインストールするには、Visual Studio をアンインストールする前に ASP.NET MVC 4 をアンインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="ab01d-303">**既定の Web API プロジェクトを実行すると、存在しない RegisterApis メソッドを使用してルートを追加するようにユーザーに誤って指示する命令が示されます。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="ab01d-304">ルートは、ASP.NET route テーブルを使用して RegisterRoutes メソッドに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="ab01d-305">**ASP.NET MVC 4 Beta ASP.NET をインストールすると、MVC 3 RTM アプリケーションが中断します。**</span><span class="sxs-lookup"><span data-stu-id="ab01d-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="ab01d-306">RTM リリース (ASP.NET MVC 3 Tools Update リリースではない) で作成された ASP.NET MVC 3 アプリケーションでは、ASP.NET MVC 4 Beta とサイドバイサイドで動作するために次の変更が必要です。</span><span class="sxs-lookup"><span data-stu-id="ab01d-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="ab01d-307">これらの更新を行わずにプロジェクトをビルドすると、コンパイルエラーになります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="ab01d-308">**必要な更新プログラム**</span><span class="sxs-lookup"><span data-stu-id="ab01d-308">**Required updates**</span></span>

  1. <span data-ttu-id="ab01d-309">ルートの Web.config ファイルで、新しい *&lt;appSettings&gt;* エントリを追加します。このキー*ページ*には、バージョンと値*1.0.0.0*があります。</span><span class="sxs-lookup"><span data-stu-id="ab01d-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="ab01d-310">ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="ab01d-311">次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="ab01d-312">次のアセンブリ参照を見つけます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="ab01d-313">次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ab01d-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="ab01d-314">変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じてから、プロジェクトを右クリックして [再読み込み] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab01d-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
