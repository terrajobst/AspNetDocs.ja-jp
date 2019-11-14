---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 の新機能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 は、適切に確立された設計パターンと ASP.NET の力を使用して、拡張性のある標準ベースの web アプリケーションを構築するためのフレームワークです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057029"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="8321c-103">ASP.NET MVC 4 の新機能</span><span class="sxs-lookup"><span data-stu-id="8321c-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="8321c-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="8321c-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="8321c-105">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="8321c-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="8321c-106">ASP.NET MVC 4 は、適切に確立された設計パターンと ASP.NET と .NET framework の機能を使用して、スケーラブルで標準ベースの web アプリケーションを構築するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="8321c-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="8321c-107">この新しい4番目のバージョンのフレームワークは、モバイル web アプリケーションの開発をより簡単にすることに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="8321c-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="8321c-108">まず、新しい ASP.NET MVC 4 プロジェクトを作成するときに、モバイルアプリケーションプロジェクトテンプレートを使用して、モバイルデバイス専用のスタンドアロンアプリを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="8321c-109">さらに、ASP.NET MVC 4 は、jQuery の NuGet パッケージを通じて jQuery Mobile と統合されています。</span><span class="sxs-lookup"><span data-stu-id="8321c-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="8321c-110">jQuery Mobile は、Windows Phone、iPhone、Android など、一般的なすべてのモバイルデバイスプラットフォームと互換性のある web アプリを開発するための HTML5 ベースのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="8321c-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="8321c-111">ただし、特殊化が必要な場合は、ASP.NET MVC 4 を使用すると、デバイスごとに異なるビューを提供し、デバイス固有の最適化を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="8321c-112">このハンズオンラボでは、まず、ASP.NET MVC 4 &quot;Internet Application&quot; プロジェクトテンプレートを使用して、フォトギャラリーアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="8321c-113">JQuery Mobile と ASP.NET MVC 4 の新機能を使用してアプリを段階的に強化し、さまざまなモバイルデバイスとデスクトップ web ブラウザーとの互換性を確保します。</span><span class="sxs-lookup"><span data-stu-id="8321c-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="8321c-114">また、コード生成用の新しいコードレシピと、ASP.NET MVC 4 によって、タスク&lt;ActionResult&gt; 戻り値の型をサポートすることで、非同期アクションメソッドを簡単に記述できるようになる方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="8321c-115">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="8321c-116">このラボに固有のプロジェクトは、 [「ASP.NET 4.5 の Web フォームの新機能](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)」から入手できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="8321c-117">目的</span><span class="sxs-lookup"><span data-stu-id="8321c-117">Objectives</span></span>

<span data-ttu-id="8321c-118">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="8321c-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="8321c-119">ASP.NET MVC プロジェクトテンプレートの機能強化を活用する (新しいモバイルアプリケーションプロジェクトテンプレートを含む)</span><span class="sxs-lookup"><span data-stu-id="8321c-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="8321c-120">HTML5 ビューポート属性と CSS メディアクエリを使用してモバイルデバイスの表示を改善する</span><span class="sxs-lookup"><span data-stu-id="8321c-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="8321c-121">JQuery Mobile を使用してプログレッシブ拡張を行い、タッチに最適化された web UI を作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="8321c-122">モバイル固有のビューを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-122">Create mobile-specific views</span></span>
- <span data-ttu-id="8321c-123">アプリケーションのモバイルビューとデスクトップビューを切り替えるには、ビュースイッチャーコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="8321c-124">タスクサポートを使用して非同期コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="8321c-125">必要条件</span><span class="sxs-lookup"><span data-stu-id="8321c-125">Prerequisites</span></span>

<span data-ttu-id="8321c-126">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="8321c-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="8321c-127">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)します (付録 B をインストールする手順については、 [「付録 B](#AppendixB) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="8321c-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="8321c-128">[ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 インストールに含まれています)</span><span class="sxs-lookup"><span data-stu-id="8321c-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="8321c-129">Windows Phone Emulator ( [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)に含まれています)</span><span class="sxs-lookup"><span data-stu-id="8321c-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="8321c-130">オプション- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) With**電気 Plum iPhone シミュレーター**拡張機能 (iphone シミュレーターで web アプリケーションを参照するために使用する演習3のみ)</span><span class="sxs-lookup"><span data-stu-id="8321c-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="8321c-131">セットアップ</span><span class="sxs-lookup"><span data-stu-id="8321c-131">Setup</span></span>

<span data-ttu-id="8321c-132">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="8321c-133">便宜上、そのコードのほとんどは Visual Studio Code のスニペットとして提供されています。これを Visual Studio 内から使用すると、手動で追加する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="8321c-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="8321c-134">コードスニペットをインストールするには:</span><span class="sxs-lookup"><span data-stu-id="8321c-134">To install the code snippets:</span></span>

1. <span data-ttu-id="8321c-135">Windows エクスプローラーウィンドウを開き、ラボの**Source\Setup**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="8321c-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="8321c-136">このフォルダーにある**setup.exe**ファイルをダブルクリックして、Visual Studio のコードスニペットをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8321c-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="8321c-137">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 a: コードスニペット](#AppendixA)&quot;の使用」 &quot;参照してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="8321c-138">手順</span><span class="sxs-lookup"><span data-stu-id="8321c-138">Exercises</span></span>

<span data-ttu-id="8321c-139">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="8321c-140">新しい ASP.NET MVC 4 プロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="8321c-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="8321c-141">フォトギャラリー Web アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="8321c-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="8321c-142">モバイルデバイスのサポートの追加</span><span class="sxs-lookup"><span data-stu-id="8321c-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="8321c-143">非同期コントローラーの使用</span><span class="sxs-lookup"><span data-stu-id="8321c-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="8321c-144">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="8321c-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="8321c-145">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="8321c-146">このラボの推定所要時間: **60 分**。</span><span class="sxs-lookup"><span data-stu-id="8321c-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="8321c-147">演習 1: 新しい ASP.NET MVC 4 プロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="8321c-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="8321c-148">この演習では、ASP.NET MVC 4 プロジェクトテンプレートの拡張機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="8321c-149">MVC 3 に既に存在するインターネットアプリケーションテンプレートに加えて、このバージョンにはモバイルアプリケーション用の別のテンプレートが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="8321c-150">まず、各テンプレートの関連する機能をいくつか見ていきます。</span><span class="sxs-lookup"><span data-stu-id="8321c-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="8321c-151">次に、適切な方法を使用して、さまざまなプラットフォームでページを正しく表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="8321c-152">タスク 1-インターネットアプリケーションテンプレートを探索する</span><span class="sxs-lookup"><span data-stu-id="8321c-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="8321c-153">**Visual Studio**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="8321c-154">ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。</span><span class="sxs-lookup"><span data-stu-id="8321c-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="8321c-155">**新しいプロジェクト** ダイアログで、 **Visual C# | を選択します。** 左側のウィンドウツリーで web テンプレート を選択し、 **ASP.NET MVC 4 web アプリケーション** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="8321c-156">プロジェクトに**Photogallery**という名前を設定し、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-157">後で、作成中の PhotoGallery ASP.NET MVC 4 ソリューションをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="8321c-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="8321c-158">![新しいプロジェクトの作成](whats-new-in-aspnet-mvc-4/_static/image1.png "新しいプロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="8321c-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="8321c-159">*新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="8321c-159">*Creating a new project*</span></span>
3. <span data-ttu-id="8321c-160">**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="8321c-161">ビューエンジンとして Razor が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="8321c-162">![新しい ASP.NET MVC 4 インターネットアプリケーションを作成する](whats-new-in-aspnet-mvc-4/_static/image2.png "新しい ASP.NET MVC 4 インターネットアプリケーションを作成する")</span><span class="sxs-lookup"><span data-stu-id="8321c-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="8321c-163">*新しい ASP.NET MVC 4 インターネットアプリケーションを作成する*</span><span class="sxs-lookup"><span data-stu-id="8321c-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-164">Razor 構文は、ASP.NET MVC 3 で導入されました。</span><span class="sxs-lookup"><span data-stu-id="8321c-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="8321c-165">その目的は、ファイルで必要とされる文字数とキーストローク数を最小限に抑えることです。これにより、高速で滑らかなコーディングワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="8321c-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="8321c-166">Razor は、 C#既存の/VB (またはその他の) 言語スキルを活用し、優れた HTML 構築ワークフローを可能にするテンプレートマークアップ構文を提供します。</span><span class="sxs-lookup"><span data-stu-id="8321c-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="8321c-167">**F5**キーを押してソリューションを実行し、更新されたテンプレートを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="8321c-168">次の機能を確認できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-168">You can check out the following features:</span></span>

    <span data-ttu-id="8321c-169">**モダンスタイルのテンプレート**</span><span class="sxs-lookup"><span data-stu-id="8321c-169">**Modern-style templates**</span></span>

    <span data-ttu-id="8321c-170">テンプレートが更新され、最新のスタイルを提供しています。</span><span class="sxs-lookup"><span data-stu-id="8321c-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="8321c-171">![ASP.NET MVC 4 の再スタイル化テンプレート](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 の再スタイル化テンプレート")</span><span class="sxs-lookup"><span data-stu-id="8321c-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="8321c-172">*ASP.NET MVC 4 の再スタイル化テンプレート*</span><span class="sxs-lookup"><span data-stu-id="8321c-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="8321c-173">![新しい連絡先ページ](whats-new-in-aspnet-mvc-4/_static/image4.png "新しい連絡先ページ")</span><span class="sxs-lookup"><span data-stu-id="8321c-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="8321c-174">*新しい連絡先ページ*</span><span class="sxs-lookup"><span data-stu-id="8321c-174">*New Contact page*</span></span>

    <span data-ttu-id="8321c-175">**アダプティブレンダリング**</span><span class="sxs-lookup"><span data-stu-id="8321c-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="8321c-176">ブラウザーウィンドウのサイズを変更し、ページレイアウトが新しいウィンドウサイズに動的に適応することを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="8321c-177">これらのテンプレートでは、アダプティブレンダリング技法を使用して、デスクトップとモバイルの両方のプラットフォームで適切にレンダリングできます。カスタマイズは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="8321c-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="8321c-178">![さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート](whats-new-in-aspnet-mvc-4/_static/image5.png "さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート")</span><span class="sxs-lookup"><span data-stu-id="8321c-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="8321c-179">*さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート*</span><span class="sxs-lookup"><span data-stu-id="8321c-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="8321c-180">**JavaScript を使用した豊富な UI**</span><span class="sxs-lookup"><span data-stu-id="8321c-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="8321c-181">既定のプロジェクトテンプレートのもう1つの拡張機能は、JavaScript を使用してより対話的な JavaScript を提供することです。</span><span class="sxs-lookup"><span data-stu-id="8321c-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="8321c-182">テンプレートで使用されるログインリンクとレジスタリンクは、jQuery 検証を使用してクライアント側から入力フィールドを検証する方法を知性します。</span><span class="sxs-lookup"><span data-stu-id="8321c-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 検証](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="8321c-184">*jQuery 検証*</span><span class="sxs-lookup"><span data-stu-id="8321c-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-185">2つのログセクションに注目してください。最初のセクションでは、サイトの登録済みアカウントを使用してログインできます。2番目のセクションでは、別の認証サービス (既定では無効) を使用してログインすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="8321c-186">ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="8321c-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="8321c-187">**アプリ\_** の [開始] フォルダーの下にあるファイル**AuthConfig.cs**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="8321c-188">最後の行のコメントを削除して、Google client for *OAuth* authentication を登録します。</span><span class="sxs-lookup"><span data-stu-id="8321c-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="8321c-189">Facebook、Twitter、Microsoft などの OpenID または OAuth サービスを使用して、認証を簡単に有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="8321c-190">**F5**キーを押してソリューションを実行し、ログインページに移動します。</span><span class="sxs-lookup"><span data-stu-id="8321c-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="8321c-191">[ **Google** service] を選択してログインします。</span><span class="sxs-lookup"><span data-stu-id="8321c-191">Select **Google** service to log in.</span></span>

    ![ログインサービスの選択](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="8321c-193">*ログインサービスの選択*</span><span class="sxs-lookup"><span data-stu-id="8321c-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="8321c-194">Google アカウントを使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="8321c-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="8321c-195">サイト (localhost) が Google アカウントから情報を取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8321c-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="8321c-196">最後に、Google アカウントを関連付けるために、サイトに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![Google アカウントを関連付ける](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="8321c-198">*Google アカウントの関連付け*</span><span class="sxs-lookup"><span data-stu-id="8321c-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="8321c-199">ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="8321c-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="8321c-200">次に、ソリューションを調べて、プロジェクトテンプレートで ASP.NET MVC 4 によって導入された他の新機能を確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="8321c-201">![ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート")</span><span class="sxs-lookup"><span data-stu-id="8321c-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="8321c-202">*ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート*</span><span class="sxs-lookup"><span data-stu-id="8321c-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="8321c-203">**HTML 5 マークアップ**</span><span class="sxs-lookup"><span data-stu-id="8321c-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="8321c-204">テンプレートビューを参照して、新しいテーママークアップを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="8321c-205">![新しいテンプレート (Razor と HTML5 のマークアップを使用した場合)。](whats-new-in-aspnet-mvc-4/_static/image10.png "新しいテンプレート (Razor と HTML5 のマークアップを使用した場合)。")</span><span class="sxs-lookup"><span data-stu-id="8321c-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="8321c-206">*新しいテンプレート。 Razor および HTML5 マークアップを使用します (約 cshtml)。*</span><span class="sxs-lookup"><span data-stu-id="8321c-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="8321c-207">**更新された JavaScript ライブラリ**</span><span class="sxs-lookup"><span data-stu-id="8321c-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="8321c-208">ASP.NET MVC 4 の既定のテンプレートには、javascript と HTML を使用して高度で応答性の高い web アプリケーションを作成するための JavaScript MVVM フレームワークである KnockoutJS が含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="8321c-209">MVC3 の場合と同様に、jQuery および jQuery UI ライブラリも ASP.NET MVC 4 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8321c-210">KnockOutJS library の詳細については、「 [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="8321c-211">また、 [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)の jQuery および jquery UI についても学習できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="8321c-212">タスク 2-モバイルアプリケーションテンプレートを探索する</span><span class="sxs-lookup"><span data-stu-id="8321c-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="8321c-213">ASP.NET MVC 4 は、モバイルおよびタブレットブラウザー用の web サイトの開発を容易にします。</span><span class="sxs-lookup"><span data-stu-id="8321c-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="8321c-214">このテンプレートには、インターネットアプリケーションテンプレートと同じアプリケーション構造があります (コントローラーコードは事実上同じであることに注意してください) が、タッチベースのモバイルデバイスで適切にレンダリングされるようにスタイルが変更されています。</span><span class="sxs-lookup"><span data-stu-id="8321c-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="8321c-215">ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。</span><span class="sxs-lookup"><span data-stu-id="8321c-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="8321c-216">**[新しいプロジェクト]** ダイアログで、[ **Visual C# |] を選択します。** 左側のウィンドウツリーで [Web テンプレート] を選択し、 **ASP.NET MVC 4 web アプリケーション**を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="8321c-217">プロジェクトに「 **Photogallery. Mobile**」という名前を設定し、場所を選択し (または既定値のまま)、[&quot;をソリューションに追加&quot;] を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="8321c-218">**[New ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[モバイルアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="8321c-219">ビューエンジンとして Razor が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="8321c-220">![新しい ASP.NET MVC 4 モバイルアプリケーションの作成](whats-new-in-aspnet-mvc-4/_static/image11.png "新しい ASP.NET MVC 4 モバイルアプリケーションの作成")</span><span class="sxs-lookup"><span data-stu-id="8321c-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="8321c-221">*新しい ASP.NET MVC 4 モバイルアプリケーションの作成*</span><span class="sxs-lookup"><span data-stu-id="8321c-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="8321c-222">これで、ソリューションを探索し、mobile 用の ASP.NET MVC 4 ソリューションテンプレートで導入された新機能の一部を確認できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="8321c-223">**jQuery モバイルライブラリ**</span><span class="sxs-lookup"><span data-stu-id="8321c-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="8321c-224">モバイルアプリケーションプロジェクトテンプレートには、モバイルブラウザー互換性のためのオープンソースライブラリである jQuery Mobile library が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="8321c-225">jQuery Mobile は、CSS と JavaScript をサポートするモバイルブラウザーにプログレッシブ拡張機能を適用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="8321c-226">プログレッシブ拡張機能を使用すると、すべてのブラウザーで web ページの基本コンテンツを表示できるだけではありますが、リッチコンテンツを表示できるのは最も強力なブラウザーのみになります。</span><span class="sxs-lookup"><span data-stu-id="8321c-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="8321c-227">JQuery Mobile スタイルに含まれている JavaScript ファイルと CSS ファイルを使用すると、モバイルブラウザーでページマークアップを変更することなく、コンテンツを画面に収めることができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery: テンプレートに含まれています。](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="8321c-229">*テンプレートに含まれている jQuery mobile ライブラリ*</span><span class="sxs-lookup"><span data-stu-id="8321c-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="8321c-230">**HTML5 ベースのマークアップ**</span><span class="sxs-lookup"><span data-stu-id="8321c-230">**HTML5 based markup**</span></span>

        ![-HTML5-マークアップの使用](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="8321c-232">*HTML5 マークアップを使用したモバイルアプリケーションテンプレート (Login. cshtml および index. cshtml)*</span><span class="sxs-lookup"><span data-stu-id="8321c-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="8321c-233">**F5**キーを押してソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="8321c-234">**Windows Phone 7 エミュレーター**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="8321c-235">電話のスタート画面で、Internet Explorer を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="8321c-236">デスクトップアプリケーションが開始した URL を確認し、電話からその URL を参照します (例: `http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="8321c-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="8321c-237">これで、ログインページを入力したり、[バージョン情報] ページを確認したりできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="8321c-238">Web サイトのスタイルは、mobile 用の新しい Metro アプリに基づいていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="8321c-239">ASP.NET MVC 4 プロジェクトテンプレートがモバイルデバイスに正しく表示され、ページのすべての要素が表示され、有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="8321c-240">ヘッダーのリンクは、クリックまたはタップするのに十分な大きさであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="8321c-241">![モバイルデバイスのプロジェクトテンプレートページ](whats-new-in-aspnet-mvc-4/_static/image14.png "モバイルデバイスのプロジェクトテンプレートページ")</span><span class="sxs-lookup"><span data-stu-id="8321c-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="8321c-242">*モバイルデバイスのプロジェクトテンプレートページ*</span><span class="sxs-lookup"><span data-stu-id="8321c-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="8321c-243">新しいテンプレートでは、**ビューポートメタタグ**も使用されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="8321c-244">ほとんどのモバイルブラウザーでは、仮想ブラウザーウィンドウの幅が定義されているか、または &quot;ビューポートが&quot;。これは、モバイルデバイスの実際の幅を超えています。</span><span class="sxs-lookup"><span data-stu-id="8321c-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="8321c-245">これにより、モバイルブラウザーで web ページ全体を仮想ディスプレイ内に表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="8321c-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="8321c-246">Web 開発者は、**ビューポート meta タグ**を使用して、モバイルデバイスのブラウザー領域の幅、高さ、およびスケールを設定でき**ます。**</span><span class="sxs-lookup"><span data-stu-id="8321c-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="8321c-247">モバイルアプリケーション用の ASP.NET MVC 4 テンプレートでは、レイアウトテンプレート (*Views\Shared\_layout*) で、ビューポートがデバイスの幅に設定され (&quot;width = デバイス幅&quot;)、すべてのページのビューポートがデバイスの画面幅に設定されるようにします。</span><span class="sxs-lookup"><span data-stu-id="8321c-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="8321c-248">ビューポートメタタグは、既定のブラウザービューを変更しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="8321c-249">Views | にある **\_Layout を開きます。** **共有**フォルダーと、ビューポートメタタグをコメント化します。</span><span class="sxs-lookup"><span data-stu-id="8321c-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="8321c-250">まだ開いていない場合はアプリケーションを実行し、相違点を確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="8321c-251">![ビューポートメタタグをコメント化した後のサイト](whats-new-in-aspnet-mvc-4/_static/image15.png "ビューポートメタタグをコメント化した後のサイト")</span><span class="sxs-lookup"><span data-stu-id="8321c-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="8321c-252">*ビューポートメタタグをコメント化した後のサイト*</span><span class="sxs-lookup"><span data-stu-id="8321c-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="8321c-253">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="8321c-254">ビューポートのメタタグをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="8321c-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="8321c-255">タスク 3-アダプティブレンダリングの使用</span><span class="sxs-lookup"><span data-stu-id="8321c-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="8321c-256">この実習では、カスタマイズを行わずに、モバイルデバイスと Web ブラウザーで Web ページを正しく表示する別の方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="8321c-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="8321c-257">同じ目的でビューポートメタタグを既に使用しています。</span><span class="sxs-lookup"><span data-stu-id="8321c-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="8321c-258">次に、別の強力な方法である*アダプティブレンダリング*を使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="8321c-259">アダプティブレンダリングは、 **CSS3 メディアクエリ**を使用して、ページに適用されるスタイルをカスタマイズする手法です。</span><span class="sxs-lookup"><span data-stu-id="8321c-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="8321c-260">メディアクエリは、スタイルシート内で条件を定義し、特定の条件下で CSS スタイルをグループ化します。</span><span class="sxs-lookup"><span data-stu-id="8321c-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="8321c-261">条件が true の場合にのみ、宣言されたオブジェクトにスタイルが適用されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="8321c-262">アダプティブレンダリング手法によって実現される柔軟性により、さまざまなデバイスでサイトを表示するためのカスタマイズが可能になります。</span><span class="sxs-lookup"><span data-stu-id="8321c-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="8321c-263">スタイルを選択するロジックコードを記述しなくても、1つのスタイルシートに対して必要な数だけスタイルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="8321c-264">そのため、ページスタイルを適合させるための非常に便利な方法です。これにより、重複するコードの量と描画のためのロジックが減少します。</span><span class="sxs-lookup"><span data-stu-id="8321c-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="8321c-265">一方、CSS ファイルのサイズがわずかに増加する可能性があるため、帯域幅の消費が増加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="8321c-266">アダプティブレンダリング技法を使用すると、ブラウザーに関係なく、サイトが**正しく表示されます。**</span><span class="sxs-lookup"><span data-stu-id="8321c-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="8321c-267">ただし、帯域幅の追加負荷が問題になるかどうかを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="8321c-268">メディアクエリの基本的な形式は次のとおりです。 @media \[Scope: all |ハンドヘルド |print |射影 |画面\] ([プロパティ: 値] と...[プロパティ: 値])</span><span class="sxs-lookup"><span data-stu-id="8321c-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="8321c-269">メディアクエリの例: &gt; **@media すべて (最大幅: 1000px) と (最小幅: 700px) {}:** 700px から1000px までのすべての解像度を示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="8321c-270">**@media 画面および (最小幅: 400px) と (最大幅: 700px) {...}:** 画面にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="8321c-271">解像度は 400 ~ 700px の範囲で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="8321c-272">**@media ハンドヘルドと (最小幅: 20em)、画面および (最小幅: 20em) {...}:** ハンドヘルド (モバイルおよびデバイス) と画面の場合。</span><span class="sxs-lookup"><span data-stu-id="8321c-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="8321c-273">最小幅は20em よりも大きくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="8321c-274">詳細については、 [W3C サイト](http://www.w3.org/TR/css3-mediaqueries/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="8321c-275">アダプティブレンダリングがどのように動作するかを調べ、ASP.NET MVC 4 の既定の web サイトテンプレートの読みやすさを向上させます。</span><span class="sxs-lookup"><span data-stu-id="8321c-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="8321c-276">タスク1で作成した**photogallery .sln**ソリューションを開き、 **photogallery**プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="8321c-277">**F5**キーを押してソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="8321c-278">ブラウザーの幅を変更し、ウィンドウを半分または元のサイズの4分の1に設定します。</span><span class="sxs-lookup"><span data-stu-id="8321c-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="8321c-279">ヘッダーの項目がどのように処理されるかに注意してください。一部の要素は、ヘッダーの表示領域に表示されません。</span><span class="sxs-lookup"><span data-stu-id="8321c-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="8321c-280">**コンテンツ**プロジェクトフォルダーにある Visual Studio ソリューションエクスプローラーから、**サイトの .css**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="8321c-281">**CTRL + F**キーを押して Visual Studio 統合検索を開き、`@media` を記述して**CSS メディアクエリ**を見つけます。</span><span class="sxs-lookup"><span data-stu-id="8321c-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="8321c-282">このテンプレートで定義されているメディアクエリ条件は、次のように動作します。ブラウザーのウィンドウサイズが**850 px**を下回る場合、適用される CSS ルールは、このメディアブロック内で定義されているものです。</span><span class="sxs-lookup"><span data-stu-id="8321c-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="8321c-283">![メディアクエリの検索](whats-new-in-aspnet-mvc-4/_static/image16.png "メディアクエリの検索")</span><span class="sxs-lookup"><span data-stu-id="8321c-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="8321c-284">*メディアクエリの検索*</span><span class="sxs-lookup"><span data-stu-id="8321c-284">*Locating the media query*</span></span>
4. <span data-ttu-id="8321c-285">アダプティブレンダリングを無効にするために、850 px で設定された最大幅属性の値を**10px**に置き換え、 **ctrl + S**キーを押して変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="8321c-286">ブラウザーに戻り、CTRL キーを押し**ながら F5**キーを押して、変更内容を反映したページを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="8321c-287">ウィンドウの幅を調整するときに、両方のページの違いに注目してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="8321c-288">![左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。](whats-new-in-aspnet-mvc-4/_static/image17.png "左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。")</span><span class="sxs-lookup"><span data-stu-id="8321c-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="8321c-289">*左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。*</span><span class="sxs-lookup"><span data-stu-id="8321c-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="8321c-290">では、モバイルデバイスの動作を確認してみましょう。</span><span class="sxs-lookup"><span data-stu-id="8321c-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="8321c-291">![左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。](whats-new-in-aspnet-mvc-4/_static/image18.png "左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。")</span><span class="sxs-lookup"><span data-stu-id="8321c-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="8321c-292">*左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。*</span><span class="sxs-lookup"><span data-stu-id="8321c-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="8321c-293">Web ブラウザーでページを表示したときの変更はあまり重要ではありませんが、モバイルデバイスを使用すると、違いがより明確になります。</span><span class="sxs-lookup"><span data-stu-id="8321c-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="8321c-294">画像の左側には、カスタムスタイルの読みやすさが向上していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="8321c-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="8321c-295">アダプティブレンダリングは、他の多くのシナリオで使用できます。これにより、Web サイトに条件付きスタイルを適用したり、一般的なスタイルの問題を適切な方法で解決したりすることが容易になります。</span><span class="sxs-lookup"><span data-stu-id="8321c-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="8321c-296">ビューポートのメタタグと CSS メディアクエリは ASP.NET MVC 4 に固有のものではないため、これらの機能はどの web アプリケーションでも利用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="8321c-297">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="8321c-298">演習 2: フォトギャラリー Web アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="8321c-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="8321c-299">この演習では、フォトギャラリーアプリケーションを使用して写真を表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="8321c-300">まず、ASP.NET MVC 4 プロジェクトテンプレートを使用します。次に、サービスから写真を取得してホームページに表示する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="8321c-301">次の演習では、モバイルデバイスでの表示方法を向上させるために、このソリューションを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="8321c-302">タスク 1-モック写真サービスの作成</span><span class="sxs-lookup"><span data-stu-id="8321c-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="8321c-303">このタスクでは、ギャラリーに表示されるコンテンツを取得するために、フォトサービスのモックを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="8321c-304">これを行うには、各写真のデータと共に JSON ファイルを返すだけの新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="8321c-305">まだ開いていない場合は、 **Visual Studio**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="8321c-306">ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。</span><span class="sxs-lookup"><span data-stu-id="8321c-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="8321c-307">**新しいプロジェクト** ダイアログで、 **Visual C# | を選択します。** 左側のウィンドウツリーで web テンプレート を選択し、 **ASP.NET MVC 4 web アプリケーション** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="8321c-308">プロジェクトに**Photogallery**という名前を設定し、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="8321c-309">または、**演習 1**の既存の ASP.NET MVC 4**インターネットアプリケーション**ソリューションから作業を続行し、次の手順をスキップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="8321c-310">**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="8321c-311">ビューエンジンとして Razor が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="8321c-312">**ソリューションエクスプローラー**で、プロジェクトの [ **App\_Data** ] フォルダーを右クリックし、[追加] を選択します。 **既存のアイテム**。</span><span class="sxs-lookup"><span data-stu-id="8321c-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="8321c-313">このラボの**Source\Assets\App\_Data**フォルダーに移動し、 **Photos**ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="8321c-314">**Photocontroller**という名前の新しいコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="8321c-315">これを行うには、 **Controllers**フォルダーを右クリックし、**追加** にアクセスして、コントローラー を選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="8321c-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="8321c-316">コントローラー名を入力し、**空の MVC コントローラー**テンプレートをそのまま使用して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="8321c-317">![PhotoController の追加](whats-new-in-aspnet-mvc-4/_static/image19.png "PhotoController の追加")</span><span class="sxs-lookup"><span data-stu-id="8321c-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="8321c-318">*PhotoController の追加*</span><span class="sxs-lookup"><span data-stu-id="8321c-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="8321c-319">**Index**メソッドを次の**ギャラリー**アクションに置き換え、最近プロジェクトに追加した JSON ファイルからコンテンツを返します。</span><span class="sxs-lookup"><span data-stu-id="8321c-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="8321c-320">(コードスニペット- *ASP.NET MVC 4 Lab-Ex02 アクション*)</span><span class="sxs-lookup"><span data-stu-id="8321c-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="8321c-321">**F5**キーを押してソリューションを実行し、モック写真サービスをテストするために次の URL を参照します。 `http://localhost:[port]/photo/gallery` ([port] 値は、アプリケーションが起動された現在のポートによって異なります)。</span><span class="sxs-lookup"><span data-stu-id="8321c-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="8321c-322">この URL への要求では、 **Photos**ファイルのコンテンツを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="8321c-323">![モック写真サービスのテスト](whats-new-in-aspnet-mvc-4/_static/image20.png "モック写真サービスのテスト")</span><span class="sxs-lookup"><span data-stu-id="8321c-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="8321c-324">*モック写真サービスのテスト*</span><span class="sxs-lookup"><span data-stu-id="8321c-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="8321c-325">実際の実装では、 [ASP.NET Web API](../../../../web-api/index.md)を使用してフォトギャラリーサービスを実装できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="8321c-326">ASP.NET Web API は、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを簡単に構築できるフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="8321c-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="8321c-327">ASP.NET Web API は、.NET Framework に基づいて RESTful アプリケーションを構築するのに最適なプラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="8321c-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="8321c-328">タスク 2-フォトギャラリーを表示する</span><span class="sxs-lookup"><span data-stu-id="8321c-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="8321c-329">このタスクでは、この演習の最初の作業で作成したモックサービスを使用して、ホームページを更新し、フォトギャラリーを表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="8321c-330">モデルファイルを追加し、ギャラリービューを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="8321c-331">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="8321c-332">**[モデル]** フォルダーに**Photo**クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="8321c-333">これを行うには、 **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="8321c-334">次に、名前を**Photo.cs**に設定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="8321c-335">次のメンバーを**Photo**クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="8321c-336">(コードスニペット- *ASP.NET MVC 4 Lab-Ex02-Photo モデル*)</span><span class="sxs-lookup"><span data-stu-id="8321c-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="8321c-337">**Controllers** フォルダーから **HomeController.cs** ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="8321c-338">次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-338">Add the following using statements.</span></span>

    <span data-ttu-id="8321c-339">(コードスニペット- *ASP.NET MVC 4 Lab-Ex02-HomeController using*)</span><span class="sxs-lookup"><span data-stu-id="8321c-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="8321c-340">**Httpclient**を使用してギャラリーデータを取得するように**Index**アクションを更新し、 **JavaScriptSerializer**を使用してビューモデルに逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="8321c-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="8321c-341">(コードスニペット- *ASP.NET MVC 4 Lab-Ex02 アクション*)</span><span class="sxs-lookup"><span data-stu-id="8321c-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="8321c-342">**Views\Home**フォルダーの下にある**インデックスの cshtml**ファイルを開き、すべての内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8321c-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="8321c-343">このコードは、サービスから取得したすべての写真をループ処理し、順序なしの一覧に表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="8321c-344">(コードスニペット- *ASP.NET MVC 4 Lab-Ex02-Photo List*)</span><span class="sxs-lookup"><span data-stu-id="8321c-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="8321c-345">**ソリューションエクスプローラー**で、プロジェクトの**コンテンツ**フォルダーを右クリックし、[追加] を選択します。 **既存のアイテム**。</span><span class="sxs-lookup"><span data-stu-id="8321c-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="8321c-346">このラボの**Source\Assets\Content**フォルダーを参照し、サイトの **.css**ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="8321c-347">置換を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="8321c-348">**サイトの .css**ファイルを開いている場合は、ファイルを再度読み込むことも確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="8321c-349">ファイルエクスプローラーを開き、このラボの **[Source\ Assets]** フォルダーの下にある **[Photos]** フォルダー全体を、ソリューションエクスプローラーのプロジェクトのルートフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="8321c-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="8321c-350">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-350">Run the application.</span></span> <span data-ttu-id="8321c-351">これで、ギャラリーに写真を表示するホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="8321c-352">![フォトギャラリー](whats-new-in-aspnet-mvc-4/_static/image21.png "フォトギャラリー")</span><span class="sxs-lookup"><span data-stu-id="8321c-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="8321c-353">*フォトギャラリー*</span><span class="sxs-lookup"><span data-stu-id="8321c-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="8321c-354">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="8321c-355">演習 3: モバイルデバイスのサポートを追加する</span><span class="sxs-lookup"><span data-stu-id="8321c-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="8321c-356">ASP.NET MVC 4 の主要な更新プログラムの1つに、モバイル開発のサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="8321c-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="8321c-357">この演習では、前の演習で作成した PhotoGallery ソリューションを拡張することで、モバイルアプリケーションの ASP.NET MVC 4 の新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="8321c-358">タスク 1-ASP.NET MVC 4 アプリケーションで jQuery Mobile をインストールする</span><span class="sxs-lookup"><span data-stu-id="8321c-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="8321c-359">**Source/Ex3-MobileSupport/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="8321c-360">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8321c-361">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8321c-362">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8321c-363">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="8321c-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8321c-364">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="8321c-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8321c-365">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="8321c-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8321c-366">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8321c-367">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="8321c-368">[ > **ツール**] **[NuGet パッケージマネージャー]** [ > **パッケージマネージャーコンソール**] オプションの順にクリックして、**パッケージマネージャーコンソール**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="8321c-369">![NuGet パッケージマネージャーコンソールを開く](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet パッケージマネージャーコンソールを開く")</span><span class="sxs-lookup"><span data-stu-id="8321c-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="8321c-370">*NuGet パッケージマネージャーコンソールを開く*</span><span class="sxs-lookup"><span data-stu-id="8321c-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="8321c-371">パッケージマネージャーコンソールで、次のコマンドを実行して、 **jQuery**パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8321c-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="8321c-372">jQuery Mobile は、タッチに最適化された web UI を構築するためのオープンソースライブラリです。</span><span class="sxs-lookup"><span data-stu-id="8321c-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="8321c-373">JQuery の NuGet パッケージには、ASP.NET MVC 4 アプリケーションで jQuery Mobile を使用するヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-374">次のコマンドを実行すると、Nuget から jQuery. Mobile. MVC ライブラリがダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="8321c-375">PM</span><span class="sxs-lookup"><span data-stu-id="8321c-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="8321c-376">このコマンドにより、jQuery Mobile と、次のようなヘルパーファイルがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="8321c-377">**Views/Shared/\_layout: mobile. cshtml**: 小さい画面用に最適化された jQuery モバイルベースのレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="8321c-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="8321c-378">Web サイトがモバイルブラウザーから要求を受信すると、元のレイアウト (\_Layout) がこの web サイトに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8321c-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="8321c-379">ビュースイッチャーコンポーネント: **Views/Shared/\_ViewSwitcher (cshtml** partial) ビューと**ViewSwitcherController.cs**コントローラーで構成されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="8321c-380">このコンポーネントは、ユーザーがページのデスクトップバージョンに切り替えることができるように、モバイルブラウザーにリンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="8321c-381">![Mobile support を使用したフォトギャラリープロジェクト](whats-new-in-aspnet-mvc-4/_static/image23.png "Phmobile サポート付き oto Gallery プロジェクト)</span><span class="sxs-lookup"><span data-stu-id="8321c-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="8321c-382">*Mobile support を使用したフォトギャラリープロジェクト*</span><span class="sxs-lookup"><span data-stu-id="8321c-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="8321c-383">モバイルバンドルを登録します。</span><span class="sxs-lookup"><span data-stu-id="8321c-383">Register the Mobile bundles.</span></span> <span data-ttu-id="8321c-384">これを行うには、 **Global.asax.cs**ファイルを開き、次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="8321c-385">(コードスニペット- *ASP.NET MVC 4 Lab-Ex03-Mobile バンドルの登録*)</span><span class="sxs-lookup"><span data-stu-id="8321c-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="8321c-386">デスクトップ web ブラウザーを使用してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="8321c-387">[スタート] メニューにある [ **Windows Phone 7] エミュレーターを**開きます。 **すべてのプログラム |Windows Phone SDK 7.1 |Windows Phone エミュレーター。**</span><span class="sxs-lookup"><span data-stu-id="8321c-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="8321c-388">電話のスタート画面で、Internet Explorer を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="8321c-389">アプリケーションが開始された URL を確認し、電話ブラウザーでその URL を参照します (例: `http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="8321c-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="8321c-390">Windows Phone エミュレーターでは、アプリケーションの外観が異なることがわかります。これは、モバイルデバイス用に最適化されたビューを表示する新しいアセットがプロジェクトに作成されたためです。</span><span class="sxs-lookup"><span data-stu-id="8321c-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="8321c-391">電話の上部に、デスクトップビューに切り替えるリンクが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="8321c-392">また、インストールしたパッケージによって作成された **\_のレイアウト**は、アプリケーションに別のレイアウトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-393">ここまでは、モバイルビューに戻るためのリンクはありません。</span><span class="sxs-lookup"><span data-stu-id="8321c-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="8321c-394">これは、それ以降のバージョンに含まれる予定です。</span><span class="sxs-lookup"><span data-stu-id="8321c-394">It will be included in later versions.</span></span>

    <span data-ttu-id="8321c-395">![フォトギャラリーホームページのモバイルビュー](whats-new-in-aspnet-mvc-4/_static/image24.png "フォトギャラリーホームページのモバイルビュー")</span><span class="sxs-lookup"><span data-stu-id="8321c-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="8321c-396">*フォトギャラリーホームページのモバイルビュー*</span><span class="sxs-lookup"><span data-stu-id="8321c-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="8321c-397">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="8321c-398">タスク 2-モバイルビューの作成</span><span class="sxs-lookup"><span data-stu-id="8321c-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="8321c-399">このタスクでは、モバイルデバイスでの外観を改善するためにコンテンツを適合させた状態で、インデックスビューのモバイルバージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="8321c-400">**Views\Home\Index.cshtml**ビューをコピーして貼り付け、コピーを作成します。新しいファイルの名前を「 **Index. Mobile. cshtml**」に変更します。</span><span class="sxs-lookup"><span data-stu-id="8321c-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="8321c-401">新しく作成した**Index. Mobile. cshtml**ビューを開き、既存の &lt;ul&gt; タグをこのコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8321c-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="8321c-402">これにより、jquery のモバイルテーマを使用するように、jQuery モバイルデータ注釈を使用して &lt;ul&gt; タグを更新することになります。</span><span class="sxs-lookup"><span data-stu-id="8321c-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="8321c-403">以下の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="8321c-404">**Listview**に設定されている**データロール**属性は、listview スタイルを使用してリストを表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="8321c-405">**データ埋め込み**属性が true に設定されている場合は、境界線と余白が丸められたリストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="8321c-406">**データフィルター**属性を**true**に設定すると、検索ボックスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="8321c-407">JQuery Mobile の規則の詳細については、次のプロジェクトドキュメントを参照してください: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="8321c-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="8321c-408">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="8321c-409">**Windows Phone エミュレーター**に切り替えて、サイトを最新の状態に更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="8321c-410">ギャラリーの一覧の新しい外観と、上部にある新しい検索ボックスに注目してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="8321c-411">次に、検索ボックスに単語 (例、 **Tulips**) を入力して、フォトギャラリーで検索を開始します。</span><span class="sxs-lookup"><span data-stu-id="8321c-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="8321c-412">![フィルターを使用して listview スタイルを使用するギャラリー](whats-new-in-aspnet-mvc-4/_static/image25.png "フィルターを使用して listview スタイルを使用するギャラリー")</span><span class="sxs-lookup"><span data-stu-id="8321c-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="8321c-413">*フィルターを使用して listview スタイルを使用するギャラリー*</span><span class="sxs-lookup"><span data-stu-id="8321c-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="8321c-414">まとめると、「Mobilizer 表示」レシピを使用して、&quot;mobile&quot; サフィックスを持つインデックスビューのコピーを作成しました。</span><span class="sxs-lookup"><span data-stu-id="8321c-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="8321c-415">このサフィックスは、モバイルデバイスから生成されたすべての要求がこのインデックスのコピーを使用することを ASP.NET MVC 4 に示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="8321c-416">さらに、モバイルデバイスのサイトの外観を拡張するために jQuery Mobile を使用するように、インデックスビューのモバイルバージョンを更新しました。</span><span class="sxs-lookup"><span data-stu-id="8321c-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="8321c-417">Visual Studio に戻り、 **Content**フォルダーの下にある **[.css]** を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="8321c-418">画像の右側に表示されるように、写真のタイトルの位置を修正します。</span><span class="sxs-lookup"><span data-stu-id="8321c-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="8321c-419">これを行うには、次のコードを追加し**ます。**</span><span class="sxs-lookup"><span data-stu-id="8321c-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="8321c-420">CSS</span><span class="sxs-lookup"><span data-stu-id="8321c-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="8321c-421">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="8321c-422">**Windows Phone エミュレーター**に戻り、サイトを最新の状態に更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="8321c-423">写真のタイトルが正しく配置されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="8321c-424">![イメージの右側に配置されたタイトル](whats-new-in-aspnet-mvc-4/_static/image26.png "イメージの右側に配置されたタイトル")</span><span class="sxs-lookup"><span data-stu-id="8321c-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="8321c-425">*イメージの右側に配置されたタイトル*</span><span class="sxs-lookup"><span data-stu-id="8321c-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="8321c-426">タスク 3-jQuery Mobile のテーマ</span><span class="sxs-lookup"><span data-stu-id="8321c-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="8321c-427">JQuery Mobile のすべてのレイアウトとウィジェットは、新しいオブジェクト指向の CSS フレームワークを中心に設計されています。これにより、完全な統合されたビジュアルデザインテーマをサイトとアプリケーションに適用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="8321c-428">jQuery Mobile の既定のテーマには、クイックリファレンス用に文字 (a、b、c、d、e) が指定された5つの見本が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="8321c-429">このタスクでは、既定とは異なるテーマを使用するようにモバイルレイアウトを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="8321c-430">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="8321c-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="8321c-431">**Views\Shared**にある **\_Layout**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="8321c-432">データロールが &quot;ページ&quot; に設定されている div 要素を見つけ、**データテーマ**を &quot;**e**&quot;に更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="8321c-433">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="8321c-434">**Windows Phone エミュレーター**でサイトを更新すると、新しい配色が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="8321c-435">![別の配色でのモバイルレイアウト](whats-new-in-aspnet-mvc-4/_static/image27.png "別の配色でのモバイルレイアウト")</span><span class="sxs-lookup"><span data-stu-id="8321c-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="8321c-436">*別の配色でのモバイルレイアウト*</span><span class="sxs-lookup"><span data-stu-id="8321c-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="8321c-437">タスク 4-ビュースイッチャーコンポーネントとブラウザーを使用して機能をオーバーライドする</span><span class="sxs-lookup"><span data-stu-id="8321c-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="8321c-438">モバイルで最適化された web ページの規則としては、ユーザーがデスクトップバージョンのページに切り替えることができるように、デスクトップビューや完全サイトモードなどのテキストを持つリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="8321c-439">JQuery パッケージには、この目的のためのサンプルの**ビュースイッチャー**コンポーネントが含まれています。これは **\_Layout**ビューで使用されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="8321c-440">![デスクトップビューに切り替えるためのリンク](whats-new-in-aspnet-mvc-4/_static/image28.png "デスクトップビューに切り替えるためのリンク")</span><span class="sxs-lookup"><span data-stu-id="8321c-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="8321c-441">*デスクトップビューに切り替えるためのリンク*</span><span class="sxs-lookup"><span data-stu-id="8321c-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="8321c-442">ビュースイッチャーは、**ブラウザーのオーバーライド**と呼ばれる新しい機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="8321c-443">この機能により、アプリケーションは、実際に使用されているものとは異なるブラウザー (ユーザーエージェント) からの要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="8321c-444">このタスクでは、ASP.NET によって追加されたビュースイッチャーの実装のサンプルと、新しいブラウザーで、MVC 4 の新機能をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="8321c-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="8321c-445">Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="8321c-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="8321c-446">**Views\Shared**フォルダーの下にある **\_Layout**を開き、ビュースイッチャーコンポーネントが部分ビューとして参照されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="8321c-447">![ビュースイッチャーコンポーネントを使用したモバイルレイアウト](whats-new-in-aspnet-mvc-4/_static/image29.png "ビュースイッチャーコンポーネントを使用したモバイルレイアウト")</span><span class="sxs-lookup"><span data-stu-id="8321c-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="8321c-448">*ビュースイッチャーコンポーネントを使用したモバイルレイアウト*</span><span class="sxs-lookup"><span data-stu-id="8321c-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="8321c-449">**\_ViewSwitcher**の部分ビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="8321c-450">部分ビューでは、新しいメソッド**GetOverriddenBrowser ()** を使用して、web 要求の送信元を特定し、対応するリンクを表示してデスクトップまたはモバイルビューに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="8321c-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="8321c-451">**GetOverriddenBrowser**メソッドは、要求に対して現在設定されているユーザーエージェント (実際またはオーバーライド) に対応する**HttpBrowserCapabilitiesBase**インスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="8321c-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="8321c-452">この値を使用して、 **IsMobileDevice**などのプロパティを取得できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="8321c-453">![ViewSwitcher 部分ビュー](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 部分ビュー")</span><span class="sxs-lookup"><span data-stu-id="8321c-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="8321c-454">*ViewSwitcher 部分ビュー*</span><span class="sxs-lookup"><span data-stu-id="8321c-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="8321c-455">**Controllers**フォルダーにある**ViewSwitcherController.cs**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="8321c-456">この SwitchView アクションが ViewSwitcher コンポーネントのリンクによって呼び出され、新しい HttpContext メソッドがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="8321c-457">**ClearOverriddenBrowser ()** メソッドは、現在の要求に対してオーバーライドされたユーザーエージェントを削除します。</span><span class="sxs-lookup"><span data-stu-id="8321c-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="8321c-458">**SetOverriddenBrowser ()** メソッドは、指定されたユーザーエージェントを使用して、要求の実際のユーザーエージェント値をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="8321c-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="8321c-459">![ViewSwitcher コントローラー](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher コントローラー ")</span><span class="sxs-lookup"><span data-stu-id="8321c-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="8321c-460">*ViewSwitcher コントローラー*</span><span class="sxs-lookup"><span data-stu-id="8321c-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="8321c-461">ブラウザーのオーバーライドは ASP.NET MVC 4 の中核機能であり、jQuery パッケージをインストールしない場合でも利用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="8321c-462">ただし、この機能は、ビュー、レイアウト、および部分ビューのみに影響し、要求の Browser オブジェクトに依存する機能には影響しません。</span><span class="sxs-lookup"><span data-stu-id="8321c-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="8321c-463">タスク 5-デスクトップビューでのビュースイッチャーの追加</span><span class="sxs-lookup"><span data-stu-id="8321c-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="8321c-464">このタスクでは、ビュースイッチャーを含むようにデスクトップレイアウトを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="8321c-465">これにより、モバイルユーザーは、デスクトップビューを参照するときにモバイルビューに戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="8321c-466">**Windows Phone エミュレーター**でサイトを最新の状態に更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="8321c-467">ギャラリーの上部にある **[デスクトップビュー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="8321c-468">デスクトップビューには、モバイルビューに戻ることができるビュースイッチャーがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="8321c-469">Visual Studio に戻り、 **\_Layout**ビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="8321c-470">Login セクションを検索し、呼び出しを挿入して、 **\_LogOnPartial**部分ビューの下に **\_viewswitcher**部分ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="8321c-471">次に、 **CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="8321c-472">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="8321c-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="8321c-473">Windows Phone エミュレーターでページを更新し、画面をダブルクリックして拡大します。</span><span class="sxs-lookup"><span data-stu-id="8321c-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="8321c-474">ホームページの [モバイル**ビュー** ] リンクが表示され、モバイルからデスクトップへの表示に切り替わります。</span><span class="sxs-lookup"><span data-stu-id="8321c-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="8321c-475">![デスクトップビューで表示されたビュースイッチャー](whats-new-in-aspnet-mvc-4/_static/image32.png "デスクトップビューで表示されたビュースイッチャー")</span><span class="sxs-lookup"><span data-stu-id="8321c-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="8321c-476">*デスクトップビューで表示されたビュースイッチャー*</span><span class="sxs-lookup"><span data-stu-id="8321c-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="8321c-477">もう一度モバイルビューに切り替えて、 **[バージョン情報]** ページ (http://localhost [ポート]/Home/About) に移動します。</span><span class="sxs-lookup"><span data-stu-id="8321c-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="8321c-478">About. Mobile. cshtml ビューを作成していない場合でも、モバイルレイアウト (\_Layout) を使用して [バージョン情報] ページが表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="8321c-479">![[バージョン情報] ページ](whats-new-in-aspnet-mvc-4/_static/image33.png "About ページ")</span><span class="sxs-lookup"><span data-stu-id="8321c-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="8321c-480">*[バージョン情報] ページ*</span><span class="sxs-lookup"><span data-stu-id="8321c-480">*About page*</span></span>
8. <span data-ttu-id="8321c-481">最後に、デスクトップ Web ブラウザーでサイトを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="8321c-482">以前の更新プログラムがデスクトップビューに影響を与えていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="8321c-483">![PhotoGallery デスクトップビュー](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery デスクトップビュー")</span><span class="sxs-lookup"><span data-stu-id="8321c-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="8321c-484">*PhotoGallery デスクトップビュー*</span><span class="sxs-lookup"><span data-stu-id="8321c-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="8321c-485">タスク 6-新しい表示モードを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="8321c-486">新しい表示モード機能を使用すると、アプリケーションは要求を生成しているブラウザーに応じてビューを選択できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="8321c-487">たとえば、デスクトップブラウザーがホームページを要求した場合、アプリケーションは**Views\Home\Index.cshtml**テンプレートを返します。</span><span class="sxs-lookup"><span data-stu-id="8321c-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="8321c-488">その後、モバイルブラウザーがホームページを要求すると、アプリケーションは**Views\Home\Index.mobile.cshtml**テンプレートを返します。</span><span class="sxs-lookup"><span data-stu-id="8321c-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="8321c-489">このタスクでは、iPhone デバイス用にカスタマイズされたレイアウトを作成し、iPhone デバイスからの要求をシミュレートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="8321c-490">これを行うには、iPhone エミュレーター/シミュレーター ([電気モバイルシミュレーター](http://www.electricplum.com/)など) を使用するか、ユーザーエージェントを変更するアドオンを含むブラウザーを使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="8321c-491">Safari ブラウザーでユーザーエージェント文字列を設定して iPhone をエミュレートする方法については、David Alison のブログで Safari を使用して[いることを safari に任せる方法](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="8321c-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="8321c-492">**このタスクは省略可能であることに注意してください。ラボを実行しなくても続行できます。**</span><span class="sxs-lookup"><span data-stu-id="8321c-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="8321c-493">Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="8321c-494">**Global.asax.cs**を開き、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="8321c-495">次の強調表示されたコードをアプリケーション\_の開始メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="8321c-496">(コードスニペット- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="8321c-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="8321c-497">静的な**Displaymodeprovider. Instance. mode** **&quot;&quot;という名前の新しい defaultdisplaymode**を登録しました。これは、各受信要求に対して照合されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="8321c-498">受信要求に iPhone&quot;の文字列 &quot;が含まれている場合、ASP.NET MVC では、名前に &quot;iPhone&quot; サフィックスが含まれるビューが検索されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="8321c-499">0パラメーターは、どのように新しいモードを指定するかを示します。たとえば、このビューは、モバイルデバイスからの要求に一致する一般的な &quot;mobile&quot; ルールよりも具体的です。</span><span class="sxs-lookup"><span data-stu-id="8321c-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="8321c-500">このコードが実行されると、iPhone ブラウザーが要求を生成するときに、アプリケーションでは、次の手順で作成する**Views\Shared\\_Layout**を使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="8321c-501">IPhone の要求をテストするこの方法はデモを目的として簡略化されており、すべての iPhone ユーザーエージェント文字列で想定どおりに機能しない可能性があります (たとえば、テストでは大文字と小文字が区別されます)。</span><span class="sxs-lookup"><span data-stu-id="8321c-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="8321c-502">**Views\Shared**フォルダーに **\_Layout**ファイルのコピーを作成し、コピーの名前を &quot; **\_layout**&quot;に変更します。</span><span class="sxs-lookup"><span data-stu-id="8321c-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="8321c-503">前の手順で作成した **\_のレイアウト**を開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="8321c-504">データロール属性が**ページ**に設定されている div 要素を見つけ、**データテーマ**属性**を&quot;&quot;に変更**します。</span><span class="sxs-lookup"><span data-stu-id="8321c-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="8321c-505">これで、ASP.NET MVC 4 アプリケーションに3つのレイアウトが作成されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="8321c-506">**\_layout**: デスクトップブラウザーで使用される既定のレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="8321c-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="8321c-507">**\_** は、モバイルデバイスで使用される既定のレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="8321c-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="8321c-508">**\_** のレイアウトです。 iphone デバイスの特定のレイアウトでは、別の配色を使用して \_のレイアウトを区別します。</span><span class="sxs-lookup"><span data-stu-id="8321c-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="8321c-509">**F5**キーを押してアプリケーションを実行し、 **Windows Phone エミュレーター**でサイトを参照します。</span><span class="sxs-lookup"><span data-stu-id="8321c-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="8321c-510">**Iphone**シミュレーターを開き (iphone シミュレーターのインストールと構成の手順については、[付録 C](#AppendixC)を参照してください)、サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="8321c-511">各電話で特定のテンプレートが使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-511">Notice that each phone is using the specific template.</span></span>

    ![-デバイス2を使用して-異なるビューを使用する](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="8321c-513">*モバイルデバイスごとに異なるビューを使用する*</span><span class="sxs-lookup"><span data-stu-id="8321c-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="8321c-514">演習 4: 非同期コントローラーの使用</span><span class="sxs-lookup"><span data-stu-id="8321c-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="8321c-515">Microsoft .NET Framework 4.5 でC#は、と Visual Basic の新しい言語機能が導入されており、.net プログラミングにおける非同期性の新しい基盤を提供しています。</span><span class="sxs-lookup"><span data-stu-id="8321c-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="8321c-516">この新しい基盤により、非同期プログラミングは、と同様に、同期型のプログラミングと同様に簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="8321c-517">**Asynccontroller**クラスを使用して、ASP.NET MVC 4 で非同期アクションメソッドを記述できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="8321c-518">非同期アクションメソッドは、実行時間の長い CPU にバインドされていない要求に使用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="8321c-519">これにより、要求の処理中に Web サーバーが作業を実行できなくなります。</span><span class="sxs-lookup"><span data-stu-id="8321c-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="8321c-520">AsyncController クラスは、通常、実行時間の長い Web サービス呼び出しに使用されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="8321c-521">この演習では、ASP.NET MVC 4 での非同期操作の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="8321c-522">詳細については、次の記事を確認してください: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="8321c-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="8321c-523">タスク 1-非同期コントローラーを実装する</span><span class="sxs-lookup"><span data-stu-id="8321c-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="8321c-524">**Source/Ex4/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="8321c-525">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="8321c-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8321c-526">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8321c-527">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8321c-528">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="8321c-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8321c-529">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="8321c-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8321c-530">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="8321c-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8321c-531">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8321c-532">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="8321c-533">**Controllers**フォルダーから**HomeController.cs**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="8321c-534">次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="8321c-535">**Asynccontroller**から継承するように**HomeController**クラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="8321c-536">AsyncController から派生したコントローラーは、ASP.NET が非同期要求を処理できるようにします。また、同期アクションメソッドを処理することもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="8321c-537">**Async**キーワードを**Index**メソッドに追加し、Type**タスク&lt;actionresult&gt;** を返します。</span><span class="sxs-lookup"><span data-stu-id="8321c-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="8321c-538">**Async**キーワードは、.NET Framework 4.5 が提供する新しいキーワードの1つです。このメソッドは、このメソッドが非同期コードを含むことをコンパイラに伝えます。</span><span class="sxs-lookup"><span data-stu-id="8321c-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="8321c-539">**Task**オブジェクトは、将来のある時点で完了する可能性のある非同期操作を表します。</span><span class="sxs-lookup"><span data-stu-id="8321c-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="8321c-540">クライアントを置き換え**ます。GetAsync ()** は、次に示すように、await キーワードを使用する完全な非同期バージョンでを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8321c-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="8321c-541">(コードスニペット- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="8321c-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="8321c-542">以前のバージョンでは、**タスク**オブジェクトから**result**プロパティを使用して、結果が返されるまでスレッドをブロックしていました (同期バージョン)。</span><span class="sxs-lookup"><span data-stu-id="8321c-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="8321c-543">**Await**キーワードを追加すると、メソッド呼び出しから返されたタスクを非同期に待機するようにコンパイラに指示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="8321c-544">これは、待機中のメソッドが完了した後にのみ、コードの残りの部分がコールバックとして実行されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="8321c-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="8321c-545">もう1つの注意点は、この作業を行うために try-catch ブロックを変更する必要がないことです。つまり、バックグラウンドまたはフォアグラウンドで発生する例外は、フレームワークによって提供されるハンドラーを使用して追加の作業を行わずにキャッチされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="8321c-546">次に示すように、行を新しいコードに置き換えて、非同期実装で続行するようにコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="8321c-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="8321c-547">(コードスニペット- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="8321c-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="8321c-548">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-548">Run the application.</span></span> <span data-ttu-id="8321c-549">大きな変更はありませんが、スレッドプールからのスレッドをブロックすることはできません。これにより、サーバーリソースの使用率が向上し、パフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="8321c-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-550">このラボの新しい非同期プログラミング機能の詳細については、Visual Studio トレーニングキットに含まれている **C#と Visual Basic&quot; の .net 4.5 での &quot;非同期プログラミング」** を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8321c-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="8321c-551">タスク 2-キャンセルトークンを使用したタイムアウト処理</span><span class="sxs-lookup"><span data-stu-id="8321c-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="8321c-552">タスクインスタンスを返す非同期アクションメソッドは、タイムアウトをサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="8321c-553">このタスクでは、キャンセルトークンを使用してタイムアウトシナリオを処理するように、インデックスメソッドコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="8321c-554">Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="8321c-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="8321c-555">次の using ステートメントを**HomeController.cs**ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="8321c-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="8321c-556">**CancellationToken**引数を受け取るように Index アクションを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="8321c-557">**GetAsync**呼び出しを更新して、キャンセルトークンを渡します。</span><span class="sxs-lookup"><span data-stu-id="8321c-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="8321c-558">(コードスニペット- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*)</span><span class="sxs-lookup"><span data-stu-id="8321c-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="8321c-559">**Asynctimeout**属性を500ミリ秒に設定し、 **TimedOut**ビューにリダイレクトして**TaskCanceledException**を処理するように構成された**HandleError**属性を使用して、 *Index*メソッドを修飾します。</span><span class="sxs-lookup"><span data-stu-id="8321c-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="8321c-560">(コードスニペット- *ASP.NET MVC 4 Ex04-Attributes*)</span><span class="sxs-lookup"><span data-stu-id="8321c-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="8321c-561">**Photocontroller**クラスを開き、実行時間の長いタスクをシミュレートするために、1000ミリ秒 (1 秒) の実行を遅延するように**ギャラリー**メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="8321c-562">**Web.config ファイルを**開き、次の要素を追加してカスタムエラーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="8321c-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="8321c-563">**TimedOut**という名前の新しいビューを**Views\Shared**に作成し、既定のレイアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="8321c-564">ソリューションエクスプローラーで、 **Views\Shared**フォルダーを右クリックし、[追加] を選択します。 **ビュー**。</span><span class="sxs-lookup"><span data-stu-id="8321c-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="8321c-565">![モバイルデバイスごとに異なるビューを使用する](whats-new-in-aspnet-mvc-4/_static/image36.png "モバイルデバイスごとに異なるビューを使用する")</span><span class="sxs-lookup"><span data-stu-id="8321c-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="8321c-566">*モバイルデバイスごとに異なるビューを使用する*</span><span class="sxs-lookup"><span data-stu-id="8321c-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="8321c-567">次に示すように、 **TimedOut** view コンテンツを更新します。</span><span class="sxs-lookup"><span data-stu-id="8321c-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="8321c-568">アプリケーションを実行し、ルート URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="8321c-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="8321c-569">スレッドを追加したときに、1000ミリ秒の**スリープ状態**でタイムアウトエラーが発生し、 **asynctimeout**属性によって生成され、 **HandleError**属性でキャッチされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="8321c-570">![タイムアウト例外の処理](whats-new-in-aspnet-mvc-4/_static/image37.png "タイムアウト例外の処理")</span><span class="sxs-lookup"><span data-stu-id="8321c-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="8321c-571">*タイムアウト例外の処理*</span><span class="sxs-lookup"><span data-stu-id="8321c-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="8321c-572">また、このアプリケーションは、 [「付録 D: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixD)」に従って、Windows Azure の Web サイトにデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="8321c-573">まとめ</span><span class="sxs-lookup"><span data-stu-id="8321c-573">Summary</span></span>

<span data-ttu-id="8321c-574">このハンズオンラボでは、ASP.NET MVC 4 に存在する新機能の一部を確認しました。</span><span class="sxs-lookup"><span data-stu-id="8321c-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="8321c-575">次の概念について説明しました。</span><span class="sxs-lookup"><span data-stu-id="8321c-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="8321c-576">ASP.NET MVC プロジェクトテンプレートの機能強化を活用する (新しいモバイルアプリケーションプロジェクトテンプレートを含む)</span><span class="sxs-lookup"><span data-stu-id="8321c-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="8321c-577">HTML5 ビューポート属性と CSS メディアクエリを使用してモバイルデバイスの表示を改善する</span><span class="sxs-lookup"><span data-stu-id="8321c-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="8321c-578">JQuery Mobile を使用してプログレッシブ拡張を行い、タッチに最適化された web UI を作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="8321c-579">モバイル固有のビューを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-579">Create mobile-specific views</span></span>
- <span data-ttu-id="8321c-580">アプリケーションのモバイルビューとデスクトップビューを切り替えるには、ビュースイッチャーコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="8321c-581">タスクサポートを使用して非同期コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="8321c-582">付録 A: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="8321c-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="8321c-583">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="8321c-584">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="8321c-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="8321c-585">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="8321c-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="8321c-586">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="8321c-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="8321c-587">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="8321c-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="8321c-588">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="8321c-589">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="8321c-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="8321c-590">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="8321c-591">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="8321c-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="8321c-592">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="8321c-593">![スニペット名の入力を開始します](whats-new-in-aspnet-mvc-4/_static/image39.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="8321c-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="8321c-594">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="8321c-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="8321c-595">![Tab キーを押して、強調表示されているスニペットを選択します](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="8321c-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="8321c-596">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="8321c-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="8321c-597">![もう一度 Tab キーを押すと、スニペットが展開されます。](whats-new-in-aspnet-mvc-4/_static/image41.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="8321c-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="8321c-598">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="8321c-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="8321c-599">***マウス (C#、VISUAL BASIC および XML) を使用してコードスニペットを追加するには***</span><span class="sxs-lookup"><span data-stu-id="8321c-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="8321c-600">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="8321c-601">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="8321c-602">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="8321c-603">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](whats-new-in-aspnet-mvc-4/_static/image42.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="8321c-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="8321c-604">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="8321c-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="8321c-605">![一覧から関連するスニペットをクリックして選択します。](whats-new-in-aspnet-mvc-4/_static/image43.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="8321c-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="8321c-606">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="8321c-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="8321c-607">付録 B: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="8321c-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="8321c-608">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="8321c-609">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="8321c-610">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="8321c-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="8321c-611">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;*Visual Studio Express 2012 For web With Windows AZURE SDK*&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="8321c-612">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-612">Click on **Install Now**.</span></span> <span data-ttu-id="8321c-613">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="8321c-614">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="8321c-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="8321c-615">![Visual Studio Express のインストール](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="8321c-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="8321c-616">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="8321c-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="8321c-617">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="8321c-619">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="8321c-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="8321c-620">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="8321c-620">Wait until the downloading and installation process completes.</span></span>

    ![インストールの進行状況](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="8321c-622">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="8321c-622">*Installation progress*</span></span>
6. <span data-ttu-id="8321c-623">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-623">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="8321c-625">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="8321c-625">*Installation completed*</span></span>
7. <span data-ttu-id="8321c-626">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="8321c-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="8321c-627">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="8321c-629">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="8321c-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="8321c-630">付録 C: WebMatrix 2 と iPhone シミュレーターのインストール</span><span class="sxs-lookup"><span data-stu-id="8321c-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="8321c-631">シミュレートされた iPhone デバイスでサイトを実行するには、iPhone の拡張機能 &quot;iPhone の&quot;に使用できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="8321c-632">また、Visual Studio 2012 からシミュレーターを実行するための同じ拡張機能を構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="8321c-633">タスク 1-WebMatrix 2 をインストールする</span><span class="sxs-lookup"><span data-stu-id="8321c-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="8321c-634">[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="8321c-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="8321c-635">または、Web Platform Installer が既にインストールされている場合は、それを開いて、 *WebMatrix 2*&quot;の製品 &quot;検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="8321c-636">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-636">Click on **Install Now**.</span></span> <span data-ttu-id="8321c-637">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="8321c-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="8321c-638">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="8321c-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="8321c-639">![WebMatrix 2 をインストールする](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 2 をインストールする")</span><span class="sxs-lookup"><span data-stu-id="8321c-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="8321c-640">*WebMatrix 2 をインストールする*</span><span class="sxs-lookup"><span data-stu-id="8321c-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="8321c-641">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="8321c-642">![ライセンス条項に同意する](whats-new-in-aspnet-mvc-4/_static/image50.png "ライセンス条項に同意する")</span><span class="sxs-lookup"><span data-stu-id="8321c-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="8321c-643">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="8321c-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="8321c-644">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="8321c-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="8321c-645">![インストールの進行状況](whats-new-in-aspnet-mvc-4/_static/image51.png "インストールの進行状況")</span><span class="sxs-lookup"><span data-stu-id="8321c-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="8321c-646">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="8321c-646">*Installation progress*</span></span>
6. <span data-ttu-id="8321c-647">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="8321c-648">![インストールの完了](whats-new-in-aspnet-mvc-4/_static/image52.png "インストールの完了")</span><span class="sxs-lookup"><span data-stu-id="8321c-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="8321c-649">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="8321c-649">*Installation completed*</span></span>
7. <span data-ttu-id="8321c-650">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="8321c-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="8321c-651">タスク 2-iPhone シミュレーター拡張機能のインストール</span><span class="sxs-lookup"><span data-stu-id="8321c-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="8321c-652">**WebMatrix**を実行し、既存の Web サイトを開くか、新しい Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="8321c-653">**[ホーム]** リボンの **[実行]** ボタンをクリックし、 **[新規追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="8321c-654">![新しい WebMatrix 拡張機能を追加しています](whats-new-in-aspnet-mvc-4/_static/image53.png "新しい WebMatrix 拡張機能を追加しています")</span><span class="sxs-lookup"><span data-stu-id="8321c-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="8321c-655">*新しい WebMatrix 拡張機能を追加しています*</span><span class="sxs-lookup"><span data-stu-id="8321c-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="8321c-656">**[IPhone シミュレーター]** を選択し、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="8321c-657">![WebMatrix 拡張機能の参照](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 拡張機能の参照")</span><span class="sxs-lookup"><span data-stu-id="8321c-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="8321c-658">*WebMatrix 拡張機能の参照*</span><span class="sxs-lookup"><span data-stu-id="8321c-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="8321c-659">パッケージの詳細 で、**インストール** をクリックして拡張機能のインストールを続行します。</span><span class="sxs-lookup"><span data-stu-id="8321c-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="8321c-660">![iPhone シミュレーター拡張機能](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone シミュレーター拡張機能")</span><span class="sxs-lookup"><span data-stu-id="8321c-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="8321c-661">*iPhone シミュレーター拡張機能*</span><span class="sxs-lookup"><span data-stu-id="8321c-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="8321c-662">拡張機能の EULA を読んで同意します。</span><span class="sxs-lookup"><span data-stu-id="8321c-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="8321c-663">![WebMatrix 拡張機能の EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 拡張機能の EULA")</span><span class="sxs-lookup"><span data-stu-id="8321c-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="8321c-664">*WebMatrix 拡張機能の EULA*</span><span class="sxs-lookup"><span data-stu-id="8321c-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="8321c-665">これで、iPhone シミュレーターオプションを使用して WebMatrix から Web サイトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="8321c-666">![IPhone を使用して実行する](whats-new-in-aspnet-mvc-4/_static/image57.png "IPhone を使用して実行する")</span><span class="sxs-lookup"><span data-stu-id="8321c-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="8321c-667">*IPhone を使用して実行する*</span><span class="sxs-lookup"><span data-stu-id="8321c-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="8321c-668">タスク 3-iPhone シミュレーターを実行するように Visual Studio 2012 を構成する</span><span class="sxs-lookup"><span data-stu-id="8321c-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="8321c-669">**Visual Studio 2012**を開き、任意の Web サイトを開くか、新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="8321c-670">実行 ボタンの下矢印をクリックし、**参照** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="8321c-671">![参照](whats-new-in-aspnet-mvc-4/_static/image58.png "参照")</span><span class="sxs-lookup"><span data-stu-id="8321c-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="8321c-672">*参照*</span><span class="sxs-lookup"><span data-stu-id="8321c-672">*Browse with*</span></span>
3. <span data-ttu-id="8321c-673">[&quot; の &quot;を参照] ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="8321c-674">[&quot;プログラム&quot; の追加] ダイアログで、次の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="8321c-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="8321c-675">**Program**: C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(それに応じてパスを更新します)*</span><span class="sxs-lookup"><span data-stu-id="8321c-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="8321c-676">**引数**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="8321c-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="8321c-677">**フレンドリ名**: iPhone シミュレーター</span><span class="sxs-lookup"><span data-stu-id="8321c-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="8321c-678">![プログラムの追加](whats-new-in-aspnet-mvc-4/_static/image59.png "プログラムの追加")</span><span class="sxs-lookup"><span data-stu-id="8321c-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="8321c-679">*参照するプログラムを追加する*</span><span class="sxs-lookup"><span data-stu-id="8321c-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="8321c-680">[ **OK]** をクリックして、ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="8321c-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="8321c-681">これで、iPhone シミュレーターで Visual Studio 2012 から Web アプリケーションを実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8321c-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="8321c-682">![IPhone シミュレーターを使用して参照する](whats-new-in-aspnet-mvc-4/_static/image60.png "IPhone シミュレーターを使用して参照する")</span><span class="sxs-lookup"><span data-stu-id="8321c-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="8321c-683">*IPhone シミュレーターを使用して参照する*</span><span class="sxs-lookup"><span data-stu-id="8321c-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="8321c-684">付録 D: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="8321c-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="8321c-685">この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="8321c-686">タスク 1-Windows Azure ポータルから新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="8321c-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="8321c-687">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="8321c-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-688">Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="8321c-689">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="8321c-690">![Windows Azure portal にログオンします。](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="8321c-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="8321c-691">*Windows Azure 管理ポータルにログオンします。*</span><span class="sxs-lookup"><span data-stu-id="8321c-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="8321c-692">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="8321c-693">![新しい Web サイトの作成](whats-new-in-aspnet-mvc-4/_static/image62.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="8321c-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="8321c-694">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="8321c-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="8321c-695">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="8321c-696">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="8321c-697">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-698">Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="8321c-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="8321c-699">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="8321c-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="8321c-700">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="8321c-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="8321c-701">![簡易作成を使用した新しい Web サイトの作成](whats-new-in-aspnet-mvc-4/_static/image63.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="8321c-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="8321c-702">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="8321c-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="8321c-703">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="8321c-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="8321c-704">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="8321c-705">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="8321c-706">![新しい web サイトを参照しています](whats-new-in-aspnet-mvc-4/_static/image64.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="8321c-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="8321c-707">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="8321c-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="8321c-708">![実行中の Web サイト](whats-new-in-aspnet-mvc-4/_static/image65.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="8321c-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="8321c-709">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="8321c-709">*Web site running*</span></span>
6. <span data-ttu-id="8321c-710">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="8321c-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="8321c-711">![Web サイトの管理ページを開く](whats-new-in-aspnet-mvc-4/_static/image66.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="8321c-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="8321c-712">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="8321c-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="8321c-713">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-714">*発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="8321c-715">発行プロファイルには、パブリケーションメソッドが有効になっている各エンドポイントに接続して認証するために必要な Url、ユーザー資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8321c-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="8321c-716">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8321c-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="8321c-717">![Web サイト発行プロファイルをダウンロードしています](whats-new-in-aspnet-mvc-4/_static/image67.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="8321c-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="8321c-718">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="8321c-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="8321c-719">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="8321c-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="8321c-720">この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8321c-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="8321c-721">![発行プロファイルファイルを保存しています](whats-new-in-aspnet-mvc-4/_static/image68.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="8321c-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="8321c-722">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="8321c-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="8321c-723">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="8321c-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="8321c-724">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="8321c-725">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="8321c-726">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="8321c-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="8321c-727">サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="8321c-728">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="8321c-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="8321c-729">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="8321c-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="8321c-730">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="8321c-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="8321c-731">![SQL Database サーバーダッシュボード](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="8321c-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="8321c-732">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="8321c-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="8321c-733">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="8321c-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="8321c-734">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](whats-new-in-aspnet-mvc-4/_static/image70.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="8321c-736">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="8321c-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="8321c-737">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="8321c-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="8321c-739">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="8321c-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="8321c-740">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="8321c-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="8321c-741">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="8321c-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="8321c-742">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8321c-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="8321c-743">![アプリケーションの発行](whats-new-in-aspnet-mvc-4/_static/image73.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="8321c-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="8321c-744">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="8321c-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="8321c-745">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="8321c-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="8321c-746">![発行プロファイルをインポートしています](whats-new-in-aspnet-mvc-4/_static/image74.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="8321c-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="8321c-747">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="8321c-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="8321c-748">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-748">Click **Validate Connection**.</span></span> <span data-ttu-id="8321c-749">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8321c-750">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="8321c-751">![接続の検証](whats-new-in-aspnet-mvc-4/_static/image75.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="8321c-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="8321c-752">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="8321c-752">*Validating connection*</span></span>
4. <span data-ttu-id="8321c-753">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="8321c-754">![Web deploy の構成](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="8321c-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="8321c-755">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="8321c-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="8321c-756">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="8321c-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="8321c-757">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="8321c-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="8321c-758">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="8321c-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="8321c-759">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="8321c-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="8321c-760">新しいデータベース名を入力します (例: *MVC4SampleDB*)。</span><span class="sxs-lookup"><span data-stu-id="8321c-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="8321c-761">![変換先の接続文字列を構成しています](whats-new-in-aspnet-mvc-4/_static/image77.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="8321c-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="8321c-762">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="8321c-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="8321c-763">次に、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-763">Then click **OK**.</span></span> <span data-ttu-id="8321c-764">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="8321c-765">![データベースの作成](whats-new-in-aspnet-mvc-4/_static/image78.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="8321c-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="8321c-766">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="8321c-766">*Creating the database*</span></span>
7. <span data-ttu-id="8321c-767">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="8321c-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="8321c-768">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-768">Then click **Next**.</span></span>

    <span data-ttu-id="8321c-769">![SQL Database を指す接続文字列](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="8321c-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="8321c-770">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="8321c-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="8321c-771">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8321c-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="8321c-772">![Web アプリケーションの発行](whats-new-in-aspnet-mvc-4/_static/image80.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="8321c-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="8321c-773">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="8321c-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="8321c-774">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="8321c-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="8321c-775">![Windows Azure に発行されたアプリケーション](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure に発行されたアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="8321c-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="8321c-776">*Windows Azure に発行されたアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="8321c-776">*Application published to Windows Azure*</span></span>
