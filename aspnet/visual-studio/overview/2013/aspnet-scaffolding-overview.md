---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 のスキャフォールディングを ASP.NET |Microsoft Docs
author: Rick-Anderson
description: ASP.NET スキャフォールディングは Visual Studio 2013 に含まれる新機能です。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449566"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="5d70f-103">Visual Studio 2013 の ASP.NET スキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="5d70f-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="5d70f-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5d70f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5d70f-105">ASP.NET スキャフォールディングは Visual Studio 2013 に含まれる新機能です。</span><span class="sxs-lookup"><span data-stu-id="5d70f-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="5d70f-106">概要</span><span class="sxs-lookup"><span data-stu-id="5d70f-106">Overview</span></span>

<span data-ttu-id="5d70f-107">ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="5d70f-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="5d70f-108">Visual Studio 2013 には、MVC および Web API プロジェクト用のプレインストールされたコードジェネレーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5d70f-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="5d70f-109">データモデルと対話するコードをすばやく追加する場合は、スキャフォールディングをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="5d70f-110">スキャフォールディングを使用すると、プロジェクトで標準データ操作を開発するための時間を短縮できます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="5d70f-111">既定では、Visual Studio 2013 は Web フォームプロジェクトのコードの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加するか、拡張機能をインストールすることにより、Web フォームでスキャフォールディングを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="5d70f-112">両方の方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-112">Both approaches are shown below.</span></span>

<span data-ttu-id="5d70f-113">Visual Studio 2013 Update 2 (現在 RC) では、シナリオの要件を満たすように ASP.NET スキャフォールディングを拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="5d70f-114">この機能を使用すると、カスタマイズされたスキャフォールディングテンプレートを作成し、[新しいスキャフォールディングの追加] ダイアログに追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="5d70f-115">カスタマイズしたテンプレート内で、スキャフォールディング項目を追加するときに生成されるコードを指定します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="5d70f-116">詳細については、「 [Visual Studio のカスタム Scaffolder の作成](https://go.microsoft.com/fwlink/p/?LinkId=395029)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d70f-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="5d70f-117">Prerequisites</span></span>

<span data-ttu-id="5d70f-118">ASP.NET スキャフォールディングを使用するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="5d70f-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="5d70f-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5d70f-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="5d70f-120">Web 開発者ツール (既定 Visual Studio 2013 インストールの一部)</span><span class="sxs-lookup"><span data-stu-id="5d70f-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="5d70f-121">ASP.NET Web フレームワークとツール 2013 (既定の Visual Studio 2013 インストールの一部)</span><span class="sxs-lookup"><span data-stu-id="5d70f-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="5d70f-122">MVC または Web API にスキャフォールディング項目を追加する</span><span class="sxs-lookup"><span data-stu-id="5d70f-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="5d70f-123">スキャフォールディングを追加するには、次の図に示すように、プロジェクトまたはプロジェクト内のフォルダーを右クリックし、[**追加**-**新規スキャフォールディング項目**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![スキャフォールディング項目の追加](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="5d70f-125">**[Add スキャフォールディング]** ウィンドウで、追加するスキャフォールディングの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![スキャフォールディングの種類を選択します](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="5d70f-127">**[コントローラーの追加]** ウィンドウでは、Entity Framework 6 の新しい非同期機能を使用するかどうかなど、コントローラーを生成するためのオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![コントローラーの追加](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="5d70f-129">シナリオに応じて、関連するクラスとページが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="5d70f-130">たとえば、次の図は、ムービーという名前のモデルクラスのスキャフォールディングによって作成された MVC コントローラーとビューを示しています。</span><span class="sxs-lookup"><span data-stu-id="5d70f-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![作成されたファイル](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="5d70f-132">スキャフォールディング項目を Web フォームに追加する</span><span class="sxs-lookup"><span data-stu-id="5d70f-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="5d70f-133">Web フォームコードを生成するスキャフォールディングを追加するには、Visual Studio に拡張機能をインストールするか、MVC 依存関係を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d70f-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="5d70f-134">両方の方法を次に示しますが、これらの方法のいずれかを実行するだけでよいでしょう。</span><span class="sxs-lookup"><span data-stu-id="5d70f-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="5d70f-135">Web フォームのスキャフォールディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="5d70f-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="5d70f-136">Web フォームプロジェクトでスキャフォールディングを使用できるようにする Visual Studio 拡張機能をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="5d70f-137">Visual Studio で、 **[ツール]** 、 **[拡張機能と更新プログラム]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="5d70f-138">このダイアログでは、Visual Studio ギャラリーで**Web フォームのスキャフォールディング**を検索します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![web フォームのスキャフォールディングをインストールする](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="5d70f-140">詳細については、「 [Web フォームのスキャフォールディング](https://go.microsoft.com/fwlink/p/?LinkId=396478)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="5d70f-141">MVC の依存関係</span><span class="sxs-lookup"><span data-stu-id="5d70f-141">MVC Dependencies</span></span>

<span data-ttu-id="5d70f-142">MVC の依存関係を追加するには、[ **add** - **New スキャフォールディング Item**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="5d70f-143">次に示すように、スキャフォールディングの追加 ウィンドウで、 **MVC の依存関係** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![MVC の依存関係の追加](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="5d70f-145">MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。</span><span class="sxs-lookup"><span data-stu-id="5d70f-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="5d70f-146">[最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="5d70f-147">[完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="5d70f-148">スキャフォールディングを簡単に使用するには、[完全な依存関係] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-148">To easily use scaffolding, select Full dependencies.</span></span>

![完全な依存関係の選択](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="5d70f-150">依存関係を追加すると、 **readme.txt**ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="5d70f-151">このファイルの指示に従って、プロジェクトが正しく動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="5d70f-152">Readme.txt ファイルの手順を完了したら、前の「MVC と Web API について」セクションで示したように、新しいスキャフォールディング項目を追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d70f-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="5d70f-153">自動的に生成されたビューとコントローラーは、プロジェクト内で正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="5d70f-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="5d70f-154">チュートリアル</span><span class="sxs-lookup"><span data-stu-id="5d70f-154">Tutorials</span></span>

<span data-ttu-id="5d70f-155">カスタマイズした scaffolder を作成するには、「 [Visual Studio のカスタム scaffolder の作成](https://go.microsoft.com/fwlink/p/?LinkId=395029)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="5d70f-156">生成されたファイルをカスタマイズする方法については、「 [New スキャフォールディング Item」ダイアログで生成されたファイルをカスタマイズする方法](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)に関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="5d70f-157">**Database First 開発**でスキャフォールディングを使用する例については、「 [EF DATABASE FIRST with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="5d70f-158">**Mvc**プロジェクトでスキャフォールディングを使用する例については、「[はじめに with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="5d70f-159">**WEB api**プロジェクトでスキャフォールディングを使用する例については、「 [web Api 2 で属性ルーティングを使用して REST API を作成する](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d70f-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
