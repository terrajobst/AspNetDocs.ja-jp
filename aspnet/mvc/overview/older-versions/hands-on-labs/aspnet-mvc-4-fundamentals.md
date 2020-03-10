---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 の基礎 |Microsoft Docs
author: rick-anderson
description: このハンズオンラボは、MVC (モデルビューコントローラー) の音楽ストアに基づいています。これは、ASP.NET MV の使用方法を説明するチュートリアルアプリケーションです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484570"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="0f0cc-103">ASP.NET MVC 4 の基礎</span><span class="sxs-lookup"><span data-stu-id="0f0cc-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="0f0cc-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="0f0cc-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="0f0cc-105">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="0f0cc-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="0f0cc-106">このハンズオンラボは、MVC (モデルビューコントローラー) の音楽ストアに基づいています。このアプリケーションは、ASP.NET MVC と Visual Studio を使用する手順について説明するチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="0f0cc-107">ラボ全体で、シンプルさを学習しながら、これらのテクノロジを組み合わせて使用することができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="0f0cc-108">まず、単純なアプリケーションから始めて、完全に機能する ASP.NET MVC 4 Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="0f0cc-109">このラボは、ASP.NET MVC 4 で動作します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="0f0cc-110">チュートリアルアプリケーションの ASP.NET MVC 3 バージョンについては、「 [mvc-音楽-ストア](https://github.com/evilDave/MVC-Music-Store)」で確認できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="0f0cc-111">このハンズオンラボでは、開発者が HTML や JavaScript などの Web 開発テクノロジを経験していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="0f0cc-112">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="0f0cc-113">このラボに固有のプロジェクトについては、「 [ASP.NET MVC 4 の基礎](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="0f0cc-114">ミュージックストアアプリケーション</span><span class="sxs-lookup"><span data-stu-id="0f0cc-114">The Music Store application</span></span>

<span data-ttu-id="0f0cc-115">このラボ全体で構築されるミュージックストア web アプリケーションは、ショッピング、チェックアウト、管理という3つの主要な部分で構成されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="0f0cc-116">閲覧者は、ジャンルでアルバムを参照したり、カートにアルバムを追加したり、選択内容を確認したり、最後に [ログイン] に進み、注文を完了することができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="0f0cc-117">さらに、ストア管理者は、使用可能なアルバムとメインプロパティを管理することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="0f0cc-118">![音楽ストアの画面](aspnet-mvc-4-fundamentals/_static/image1.png "音楽ストアの画面")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="0f0cc-119">*音楽ストアの画面*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="0f0cc-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="0f0cc-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="0f0cc-121">ミュージックストアアプリケーションは、**モデルビューコントローラー (MVC)** を使用して構築されます。これは、アプリケーションを3つの主要なコンポーネントに分離するアーキテクチャパターンです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="0f0cc-122">**モデル: モデル**オブジェクトは、ドメインロジックを実装するアプリケーションの一部です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="0f0cc-123">モデルオブジェクトは、多くの場合、モデルの状態を取得してデータベースに格納します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="0f0cc-124">**ビュー:** ビューは、アプリケーションのユーザーインターフェイス (UI) を表示するコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="0f0cc-125">通常、この UI はモデル データから作成されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="0f0cc-126">例としては、アルバムオブジェクトの現在の状態に基づいて、テキストボックスとドロップダウンリストを表示するアルバムの編集ビューがあります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="0f0cc-127">**コントローラー:** コントローラーは、ユーザーの操作を処理し、モデルを操作し、最終的に UI を表示するビューを選択するコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="0f0cc-128">MVC アプリケーションでは、ビューは情報を表示するだけです。ユーザー入力やユーザーとの対話を処理し、それらに応答するのは、コントローラーです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="0f0cc-129">MVC パターンを使用すると、アプリケーションのさまざまな側面 (入力ロジック、ビジネスロジック、および UI ロジック) を分離するアプリケーションを作成できます。一方、これらの要素間に疎結合が提供されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="0f0cc-130">この分離により、アプリケーションを構築する際の複雑さを管理できます。これにより、実装の1つの側面に焦点を当てることができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="0f0cc-131">さらに、MVC パターンを使用すると、アプリケーションのテストが簡単になり、アプリケーションを作成するためのテスト駆動開発 (TDD) の使用も促進されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="0f0cc-132">**ASP.NET mvc**フレームワークには、ASP.NET mvc ベースの web アプリケーションを作成するための ASP.NET web フォームパターンの代替手段が用意されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="0f0cc-133">**ASP.NET MVC**フレームワークは、(Web フォームベースのアプリケーションの場合と同様に) 既存の ASP.NET 機能と統合された軽量で高度なテストが可能なプレゼンテーションフレームワークであり、コア .net framework のすべての機能を利用できるように、マスターページやメンバーシップベースの認証などの既存の機能と統合されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="0f0cc-134">これは、既に使用しているすべてのライブラリが ASP.NET MVC 4 でも使用できるため、既に ASP.NET Web フォームを使い慣れている場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="0f0cc-135">さらに、MVC アプリケーションの3つの主要なコンポーネント間の疎結合により、並列開発も促進されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="0f0cc-136">たとえば、1人の開発者がビューを操作し、2つ目の開発者がコントローラーロジックを操作し、3番目の開発者がモデルのビジネスロジックに集中できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="0f0cc-137">目標</span><span class="sxs-lookup"><span data-stu-id="0f0cc-137">Objectives</span></span>

<span data-ttu-id="0f0cc-138">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="0f0cc-139">ミュージックストアアプリケーションのチュートリアルに基づいて ASP.NET MVC アプリケーションを最初から作成する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="0f0cc-140">サイトのホームページへの Url を処理し、その主な機能を参照するためのコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="0f0cc-141">ビューを追加して、表示されるコンテンツとそのスタイルをカスタマイズします</span><span class="sxs-lookup"><span data-stu-id="0f0cc-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="0f0cc-142">データとドメインロジックを格納および管理するためのモデルクラスを追加する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="0f0cc-143">ビューモデルパターンを使用してコントローラーアクションからビューテンプレートに情報を渡す</span><span class="sxs-lookup"><span data-stu-id="0f0cc-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="0f0cc-144">インターネットアプリケーション用の ASP.NET MVC 4 の新しいテンプレートについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="0f0cc-145">前提条件</span><span class="sxs-lookup"><span data-stu-id="0f0cc-145">Prerequisites</span></span>

<span data-ttu-id="0f0cc-146">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="0f0cc-147">[Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (インストール方法について[は、付録 A](#AppendixA)を参照してください)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="0f0cc-148">セットアップ</span><span class="sxs-lookup"><span data-stu-id="0f0cc-148">Setup</span></span>

<span data-ttu-id="0f0cc-149">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="0f0cc-150">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="0f0cc-151">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="0f0cc-152">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="0f0cc-153">手順</span><span class="sxs-lookup"><span data-stu-id="0f0cc-153">Exercises</span></span>

<span data-ttu-id="0f0cc-154">このハンズオンラボは、次の演習によって構成されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="0f0cc-155">演習 1: MusicStore ASP.NET MVC Web アプリケーションプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="0f0cc-156">演習 2: コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="0f0cc-157">演習 3: コントローラーへのパラメーターの引き渡し</span><span class="sxs-lookup"><span data-stu-id="0f0cc-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="0f0cc-158">演習 4: ビューの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="0f0cc-159">演習 5: ビューモデルの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="0f0cc-160">演習 6: ビューでのパラメーターの使用</span><span class="sxs-lookup"><span data-stu-id="0f0cc-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="0f0cc-161">演習 7: ASP.NET MVC 4 の新しいテンプレートをラップする</span><span class="sxs-lookup"><span data-stu-id="0f0cc-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="0f0cc-162">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="0f0cc-163">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="0f0cc-164">このラボの推定所要時間: **60 分**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="0f0cc-165">演習 1: MusicStore ASP.NET MVC Web アプリケーションプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="0f0cc-166">この演習では、Visual Studio 2012 Express for Web とメインフォルダーの組織で ASP.NET MVC アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="0f0cc-167">また、新しいコントローラーを追加して、アプリケーションのホームページに単純な文字列を表示させる方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="0f0cc-168">タスク 1-ASP.NET MVC Web アプリケーションプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="0f0cc-169">このタスクでは、MVC Visual Studio テンプレートを使用して、空の ASP.NET MVC アプリケーションプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="0f0cc-170">**VS Express for Web**を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="0f0cc-171">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="0f0cc-172">**[新しいプロジェクト]** ダイアログボックスで、[**ビジュアルC#] の** **[web]** テンプレート の一覧にある**ASP.NET MVC 4 Web アプリケーション**プロジェクトの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="0f0cc-173">**名前**を*MvcMusicStore*に変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="0f0cc-174">この演習のソースフォルダーの新しい**Begin**フォルダー内にソリューションの場所を設定します。たとえば、 **[\Source\Ex01-CreatingMusicStoreProject\Begin]** のように指定します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="0f0cc-175">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-175">Click **OK**.</span></span>

    <span data-ttu-id="0f0cc-176">![[新しいプロジェクトの作成] ダイアログボックス](aspnet-mvc-4-fundamentals/_static/image2.png "[新しいプロジェクトの作成] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="0f0cc-177">*[新しいプロジェクトの作成] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="0f0cc-178">**[新しい ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、**基本**テンプレートを選択し、選択した**ビューエンジン**が**Razor**になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="0f0cc-179">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-179">Click **OK**.</span></span>

    <span data-ttu-id="0f0cc-180">![[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス](aspnet-mvc-4-fundamentals/_static/image3.png "[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="0f0cc-181">*[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="0f0cc-182">タスク 2-ソリューション構造の調査</span><span class="sxs-lookup"><span data-stu-id="0f0cc-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="0f0cc-183">ASP.NET MVC フレームワークには、MVC パターンをサポートする Web アプリケーションを作成するのに役立つ Visual Studio プロジェクトテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="0f0cc-184">このテンプレートは、必要なフォルダー、項目テンプレート、および構成ファイルエントリを含む新しい ASP.NET MVC Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="0f0cc-185">ここでは、ソリューションの構造を調べて、関連する要素とその関係について理解します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="0f0cc-186">次のフォルダーはすべての ASP.NET MVC アプリケーションに含まれています。 ASP.NET MVC フレームワークでは、既定では、構成&quot; アプローチに対して &quot;規約が使用され、フォルダーの名前付け規則に基づいて既定の仮定がいくつか行われるためです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="0f0cc-187">プロジェクトが作成されたら、右側のソリューションエクスプローラーに作成されたフォルダー構造を確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="0f0cc-188">![ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET](aspnet-mvc-4-fundamentals/_static/image4.png "ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="0f0cc-189">*ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="0f0cc-190">**コントローラー**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-190">**Controllers**.</span></span> <span data-ttu-id="0f0cc-191">このフォルダーには、コントローラークラスが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="0f0cc-192">MVC ベースのアプリケーションでは、コントローラーはエンドユーザーの操作を処理し、モデルを操作し、最終的に UI を表示するビューを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="0f0cc-193">MVC フレームワークでは、すべてのコントローラーの名前を &quot;Controller&quot;(HomeController、LoginController、ProductController など) で終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="0f0cc-194">**モデル**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-194">**Models**.</span></span> <span data-ttu-id="0f0cc-195">このフォルダーは、MVC Web アプリケーションのアプリケーションモデルを表すクラス用に用意されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="0f0cc-196">これには通常、オブジェクトおよびデータストアと対話するためのロジックを定義するコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="0f0cc-197">実際のモデル オブジェクトは別のクラス ライブラリに格納するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="0f0cc-198">ただし、新しいアプリケーションを作成する場合は、クラスを追加し、開発サイクルの後の段階でクラスを個別のクラスライブラリに移動することができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="0f0cc-199">**ビュー**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-199">**Views**.</span></span> <span data-ttu-id="0f0cc-200">このフォルダーは、アプリケーションのユーザーインターフェイスを表示するコンポーネントであるビューの推奨される場所です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="0f0cc-201">ビューでは、表示ビューに関連するその他のファイルに加えて、.aspx、.ascx、cshtml、および .master ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="0f0cc-202">Views フォルダーには、各コントローラーのフォルダーが含まれています。フォルダーには、コントローラー名のプレフィックスが付いた名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="0f0cc-203">たとえば、 **HomeController**という名前のコントローラーがある場合、Views フォルダーには Home という名前のフォルダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="0f0cc-204">既定では、ASP.NET MVC フレームワークによってビューが読み込まれるときに、Views\controllerName フォルダー (**views [controllerName] [action] .aspx**) または (**views [ControllerName] [action]. cshtml**) のビュー名を持つ .Aspx ファイルが Razor ビューで検索されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-205">前に示したフォルダーに加えて、MVC Web アプリケーションは**グローバルな global.asax**ファイルを使用してグローバルな URL ルーティングの既定値を設定し、web.config ファイルを使用してアプリケーションを構成**します。**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="0f0cc-206">タスク 3-HomeController の追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="0f0cc-207">MVC フレームワークを使用しない ASP.NET アプリケーションでは、ユーザーの操作はページ、およびそれらのページからのイベントの発生と処理を中心に編成されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="0f0cc-208">これに対し、ASP.NET MVC アプリケーションとのユーザー操作は、コントローラーとそのアクションメソッドを中心に編成されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="0f0cc-209">一方、ASP.NET MVC フレームワークは、Url をコントローラーと呼ばれるクラスにマップします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="0f0cc-210">コントローラーは、着信要求を処理し、ユーザーの入力と操作を処理し、適切なアプリケーションロジックを実行して、クライアントに送り返す応答を決定します (HTML の表示、ファイルのダウンロード、別の URL へのリダイレクトなど)。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="0f0cc-211">HTML を表示する場合、通常、コントローラークラスは個別のビューコンポーネントを呼び出して、要求の HTML マークアップを生成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="0f0cc-212">MVC アプリケーションでは、ビューは情報を表示するだけです。ユーザー入力やユーザーとの対話を処理し、それらに応答するのは、コントローラーです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="0f0cc-213">このタスクでは、ミュージックストアサイトのホームページへの Url を処理するコントローラークラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="0f0cc-214">ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** コマンド の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="0f0cc-215">![コントローラーコマンドを追加する](aspnet-mvc-4-fundamentals/_static/image5.png "コントローラーコマンドを追加する")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="0f0cc-216">*コントローラーコマンドの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="0f0cc-217">**[コントローラーの追加]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="0f0cc-218">コントローラーに*HomeController*という名前を指定し、 **[追加]** を押します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="0f0cc-219">![[コントローラーの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image6.png "[コントローラーの追加] ダイアログ")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="0f0cc-220">*[コントローラーの追加] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="0f0cc-221">**HomeController.cs**ファイルが**Controllers**フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="0f0cc-222">**HomeController**がインデックスアクションに対して文字列を返すようにするには、 **index**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-223">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex1 HomeController Index*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="0f0cc-224">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="0f0cc-225">このタスクでは、web ブラウザーでアプリケーションを試します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="0f0cc-226">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="0f0cc-227">プロジェクトがコンパイルされ、ローカル IIS Web サーバーが起動します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="0f0cc-228">ローカルの IIS Web サーバーは、web サーバーの URL を指す web ブラウザーを自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="0f0cc-229">![Web ブラウザーで実行されているアプリケーション](aspnet-mvc-4-fundamentals/_static/image7.png "Web ブラウザーで実行されているアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="0f0cc-230">*Web ブラウザーで実行されているアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-231">ローカルの IIS Web サーバーは、web サイトをランダムなフリーポート番号で実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="0f0cc-232">上の図では、サイトは `http://localhost:50103/`で実行されているので、ポート50103を使用しています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="0f0cc-233">ポート番号は異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-233">Your port number may vary.</span></span>
2. <span data-ttu-id="0f0cc-234">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="0f0cc-235">演習 2: コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="0f0cc-236">この演習では、音楽ストアアプリケーションの簡単な機能を実装するようにコントローラーを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="0f0cc-237">このコントローラーは、次の特定の要求を処理するアクションメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="0f0cc-238">音楽ストアの音楽ジャンルの一覧ページ</span><span class="sxs-lookup"><span data-stu-id="0f0cc-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="0f0cc-239">特定のジャンルのすべての音楽アルバムを一覧表示する参照ページ</span><span class="sxs-lookup"><span data-stu-id="0f0cc-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="0f0cc-240">特定のミュージックアルバムに関する情報を示す詳細ページ</span><span class="sxs-lookup"><span data-stu-id="0f0cc-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="0f0cc-241">この演習の範囲において、これらのアクションは単にここで文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="0f0cc-242">タスク 1-新しい StoreController クラスを追加する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="0f0cc-243">このタスクでは、新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="0f0cc-244">まだ開いていない場合は**VS Express for Web 2012**を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="0f0cc-245">**[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="0f0cc-246">[プロジェクトを開く] ダイアログボックスで、 **Source\Ex02-CreatingAController\Begin**に移動し、 **[開始]** を選択して **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="0f0cc-247">または、前の演習を完了した後に取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="0f0cc-248">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0f0cc-249">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0f0cc-250">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0f0cc-251">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-252">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0f0cc-253">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0f0cc-254">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="0f0cc-255">新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-255">Add the new controller.</span></span> <span data-ttu-id="0f0cc-256">これを行うには、ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** を選択して、 **[コントローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="0f0cc-257">**コントローラー名**を*StoreController*に変更し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="0f0cc-258">![[コントローラーの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image8.png "[コントローラーの追加] ダイアログ")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="0f0cc-259">*[コントローラーの追加] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="0f0cc-260">タスク 2-StoreController のアクションを変更する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="0f0cc-261">このタスクでは、**アクション**と呼ばれるコントローラーメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="0f0cc-262">アクションは、URL 要求を処理し、URL を呼び出したブラウザーまたはユーザーに返信するコンテンツを決定します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="0f0cc-263">**StoreController**クラスには既に**Index**メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="0f0cc-264">このラボでは、このラボを使用して、音楽ストアのすべてのジャンルを一覧表示するページを実装します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="0f0cc-265">ここでは、 **index**メソッドを次のコードに置き換えます。このコードでは、&quot;Hello from Store. index ()&quot;の文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="0f0cc-266">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex2 StoreController Index*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="0f0cc-267">**参照**と**詳細**のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="0f0cc-268">これを行うには、 **StoreController**に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="0f0cc-269">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="0f0cc-270">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="0f0cc-271">このタスクでは、web ブラウザーでアプリケーションを試します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="0f0cc-272">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-273">プロジェクトは**ホーム**ページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="0f0cc-274">各アクションの実装を確認するには、URL を変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="0f0cc-275">**/ストア**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-275">**/Store**.</span></span> <span data-ttu-id="0f0cc-276">**&quot;Hello From Store. Index ()&quot;** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="0f0cc-277">**/ストア/参照**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-277">**/Store/Browse**.</span></span> <span data-ttu-id="0f0cc-278">**&quot;Hello From Store. 参照 ()&quot;** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="0f0cc-279">**ストア/詳細**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-279">**/Store/Details**.</span></span> <span data-ttu-id="0f0cc-280">**&quot;Hello From Store. Details ()&quot;** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="0f0cc-281">![StoreBrowse の参照](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse の参照")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="0f0cc-282">*参照/参照*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="0f0cc-283">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="0f0cc-284">演習 3: コントローラーへのパラメーターの引き渡し</span><span class="sxs-lookup"><span data-stu-id="0f0cc-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="0f0cc-285">これまでは、コントローラーから定数文字列が返されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="0f0cc-286">この演習では、URL と querystring を使用してコントローラーにパラメーターを渡す方法を学習し、メソッドのアクションがテキストでブラウザーに応答するようにします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="0f0cc-287">タスク 1-Genre パラメーターを StoreController に追加する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="0f0cc-288">このタスクでは、 **querystring**を使用して、 **StoreController**の**参照**アクションメソッドにパラメーターを送信します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="0f0cc-289">まだ開いていない場合は、 **VS Express for Web**を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="0f0cc-290">**[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="0f0cc-291">[プロジェクトを開く] ダイアログボックスで、 **Source\Ex03-PassingParametersToAController\Begin**に移動し、 **[開始]** を選択して **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="0f0cc-292">または、前の演習を完了した後に取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="0f0cc-293">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0f0cc-294">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0f0cc-295">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0f0cc-296">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-297">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0f0cc-298">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0f0cc-299">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="0f0cc-300">**StoreController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-300">Open **StoreController** class.</span></span> <span data-ttu-id="0f0cc-301">これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="0f0cc-302">**参照**メソッドを変更し、特定のジャンルに対する要求に文字列パラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="0f0cc-303">ASP.NET MVC は、呼び出されたときに、 **genre**という名前のクエリ文字列またはフォームポストパラメーターをこのアクションメソッドに自動的に渡します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="0f0cc-304">これを行うには、 **Browse**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-305">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="0f0cc-306">HtmlEncode ユーティリティメソッドを使用して、 **HttpUtility**などのリンクを使用して、ユーザーが Javascript をビューに挿入できないようにします**か?Genre =&lt;スクリプト&gt;ウィンドウ. location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="0f0cc-307">詳細については、こちらの[msdn 記事](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="0f0cc-308">タスク 2-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="0f0cc-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="0f0cc-309">このタスクでは、web ブラウザーでアプリケーションを試し、 **genre**パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="0f0cc-310">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-311">プロジェクトは**ホーム**ページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="0f0cc-312">URL を「 */Store/Browse」に変更します。Genre = Disco* : アクションが genre パラメーターを受け取ることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="0f0cc-313">![StoreBrowseGenre の参照 = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre の参照 = Disco")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="0f0cc-314">*参照/参照Genre = Disco*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="0f0cc-315">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="0f0cc-316">タスク 3-URL に埋め込まれた Id パラメーターの追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="0f0cc-317">このタスクでは、 **URL**を使用して、 **StoreController**の**Details** action メソッドに**Id**パラメーターを渡します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="0f0cc-318">ASP.NET MVC の既定のルーティング規則では、アクションメソッド名の後の URL のセグメントを、 **Id**という名前のパラメーターとして扱います。アクションメソッドに Id という名前のパラメーターがある場合、ASP.NET MVC は自動的に URL セグメントをパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="0f0cc-319">URL **Store/Details/5**では、 **Id**は**5**と解釈されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="0f0cc-320">**StoreController**の**Details**メソッドを変更し、 **id**という名前の**int**パラメーターを追加します。これを行うには、 **Details**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-321">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex3 StoreController のメソッド*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="0f0cc-322">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="0f0cc-323">このタスクでは、web ブラウザーでアプリケーションを試し、 **Id**パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="0f0cc-324">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-325">プロジェクトは**ホーム**ページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="0f0cc-326">URL を */Store//5*に変更して、アクションが id パラメーターを受け取ることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="0f0cc-327">![StoreDetails5 の参照](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 の参照")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="0f0cc-328">*参照/表示 (/dns)/5*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="0f0cc-329">演習 4: ビューの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="0f0cc-330">ここまでは、コントローラーアクションから文字列を返していました。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="0f0cc-331">これは、コントローラーがどのように動作するかを理解するのに便利な方法ですが、実際の Web アプリケーションの構築方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="0f0cc-332">ビューは、テンプレートファイルを使用してブラウザーに HTML を返すためのより優れた方法を提供するコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="0f0cc-333">この演習では、共通の HTML コンテンツ用のテンプレートを設定するためのレイアウトマスターページを追加する方法、サイトのルックアンドフィールを向上させるためのスタイルシート、最後にビューテンプレートを追加して、HomeController が HTML を返すようにする方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="0f0cc-334">タスク 1-ファイル \_layout を変更する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="0f0cc-335">**\_** ファイルを使用すると、web サイト全体で共通 HTML を使用するためのテンプレートを設定できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="0f0cc-336">このタスクでは、共通のヘッダーと、ホームページと店舗区分へのリンクを含むレイアウトマスターページを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="0f0cc-337">まだ開いていない場合は、 **VS Express for Web**を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="0f0cc-338">**[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="0f0cc-339">プロジェクトを開く ダイアログで、**ソース** を参照して 開始 を選択し、**開始** をクリックして、**開く** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="0f0cc-340">または、前の演習を完了した後に取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="0f0cc-341">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0f0cc-342">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0f0cc-343">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0f0cc-344">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-345">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0f0cc-346">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0f0cc-347">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="0f0cc-348">ファイル<strong>\_の layout</strong>には、サイト上のすべてのページの HTML コンテナーレイアウトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="0f0cc-349">これには、HTML 応答の<strong>&lt;html&gt;</strong>要素だけでなく、 <strong>&lt;ヘッド&gt;</strong>および<strong>&lt;本体&gt;</strong>要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="0f0cc-350">HTML 本文内の<strong>@RenderBody()</strong>は、ビューテンプレートで動的なコンテンツを格納できる領域を識別します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="0f0cc-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="0f0cc-352">サイト内のすべてのページに、ホームページと店舗領域へのリンクを含む共通ヘッダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="0f0cc-353">そのためには、&lt;body&gt; ステートメントの下に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="0f0cc-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="0f0cc-355">各ページの本文セクションを表示するための div を含めます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="0f0cc-356"><strong>@RenderBody()</strong>を、次の強調表示されC#たコードに置き換えます。 ()</span><span class="sxs-lookup"><span data-stu-id="0f0cc-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="0f0cc-357">ご存知でしたか?</span><span class="sxs-lookup"><span data-stu-id="0f0cc-357">Did you know?</span></span> <span data-ttu-id="0f0cc-358">Visual Studio 2012 には、一般的に使用されるコードを HTML やコードファイルなどに簡単に追加できるようにするスニペットが用意されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="0f0cc-359">**&lt;div&gt;** を入力し、 **tab**キーを2回押して、完全な**div**タグを挿入してみてください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="0f0cc-360">タスク 2-CSS スタイルシートの追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="0f0cc-361">空のプロジェクトテンプレートには、非常に効率的な CSS ファイルが含まれています。これには、基本的なフォームおよび検証メッセージの表示に使用されるスタイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="0f0cc-362">サイトのルックアンドフィールを強化するために、追加の CSS とイメージ (デザイナーによって提供される可能性があります) を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="0f0cc-363">このタスクでは、CSS スタイルシートを追加して、サイトのスタイルを定義します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="0f0cc-364">CSS ファイルとイメージは、このラボの**Source\Assets\Content**フォルダーに含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="0f0cc-365">アプリケーションに追加するには、次に示すように、 **Windows エクスプローラー**ウィンドウから Web 用 Visual Studio Express の**ソリューションエクスプローラー**にコンテンツをドラッグします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="0f0cc-366">![ドラッグ (スタイルの内容を)](aspnet-mvc-4-fundamentals/_static/image12.png "ドラッグ (スタイルの内容を)")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="0f0cc-367">*ドラッグ (スタイルの内容を)*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="0f0cc-368">[警告] ダイアログが表示され、**サイトの .css**ファイルと既存のイメージの置換を確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="0f0cc-369">**[すべての項目に適用]** チェックボックスをオンにし、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="0f0cc-370">タスク 3-ビューテンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="0f0cc-371">このタスクでは、ビューテンプレートを追加して、この演習で追加したレイアウトマスターページと CSS を使用する HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="0f0cc-372">サイトのホームページを参照するときにビューテンプレートを使用するには、最初に、文字列を返す代わりに、 **HomeController Index**メソッドが**ビュー**を返すことを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="0f0cc-373">**HomeController**クラスを開き、 **actionresult**を返すように**Index**メソッドを変更し、 **View ()** を返すようにします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="0f0cc-374">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex4 HomeController Index*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="0f0cc-375">次に、適切なビューテンプレートを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="0f0cc-376">これを行うには、 **Index**アクションメソッド内を**右クリック**し、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="0f0cc-377">**[ビューの追加]** ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="0f0cc-378">![Index メソッド内からビューを追加する](aspnet-mvc-4-fundamentals/_static/image13.png "Index メソッド内からビューを追加する")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="0f0cc-379">*Index メソッド内からビューを追加する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="0f0cc-380">**[ビューの追加]** ダイアログボックスが表示され、ビューテンプレートファイルが生成されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="0f0cc-381">既定では、このダイアログボックスには、ビューテンプレートを使用するアクションメソッドと一致するように、ビューテンプレートの名前が事前に設定されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="0f0cc-382">HomeController 内の**index**アクションメソッド内で **[ビューの追加]** コンテキストメニューを使用したので、 **[ビューの追加]** ダイアログには既定のビュー名としてインデックスがあります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="0f0cc-383">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-383">Click **Add**.</span></span>

    <span data-ttu-id="0f0cc-384">![[ビューの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image14.png "[ビューの追加] ダイアログ")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="0f0cc-385">*[ビューの追加] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="0f0cc-386">**Views\Home**フォルダー内に**Index. cshtml** view テンプレートが生成され、それが開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="0f0cc-387">![ホームインデックスビューが作成されました](aspnet-mvc-4-fundamentals/_static/image15.png "ホームインデックスビューが作成されました")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="0f0cc-388">*ホームインデックスビューが作成されました*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-389">**Index. cshtml**ファイルの名前と場所は、既定の ASP.NET MVC 名前付け規則に従っています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="0f0cc-390">フォルダー \ Views\**home*\* は、コントローラー名 (**home**コントローラー) と一致します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="0f0cc-391">ビューテンプレート名 (**Index**) は、ビューを表示するコントローラーアクションメソッドに一致します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="0f0cc-392">このように、ASP.NET MVC では、この名前付け規則を使用してビューを返すときに、ビューテンプレートの名前または場所を明示的に指定する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="0f0cc-393">生成されたビューテンプレートは、前に定義した **\_の layout**テンプレートに基づいています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="0f0cc-394">次のコードに示すように、ViewBag プロパティを**home**に更新し、メインコンテンツを**次のホームページ**に変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="0f0cc-395">ソリューションエクスプローラーで [ **MvcMusicStore**プロジェクト] を選択し、 **F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="0f0cc-396">タスク 4: 検証</span><span class="sxs-lookup"><span data-stu-id="0f0cc-396">Task 4: Verification</span></span>

<span data-ttu-id="0f0cc-397">前の演習のすべての手順を正しく実行したことを確認するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="0f0cc-398">ブラウザーでアプリケーションを開いたときに、次の点に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="0f0cc-399">ビューテンプレートが標準の名前付け規則に従っているため、HomeController のインデックスアクションメソッドが見つかり、 **\Views\Home\Index.cshtml** view テンプレートが表示されます。これは、**リターンビュー ()** を呼び出したコードです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="0f0cc-400">ホームページには、 **\Views\Home\Index.cshtml** view テンプレート内で定義されているウェルカムメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="0f0cc-401">ホームページでは **\_layout**テンプレートが使用されているため、ウェルカムメッセージは標準のサイト HTML レイアウト内に含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="0f0cc-402">![定義済みの LayoutPage と style を使用したホームインデックスビュー](aspnet-mvc-4-fundamentals/_static/image16.png "定義済みの LayoutPage と style を使用したホームインデックスビュー")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="0f0cc-403">*定義済みの LayoutPage と style を使用したホームインデックスビュー*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="0f0cc-404">演習 5: ビューモデルの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="0f0cc-405">これまでは、ビューにハードコードされた HTML が表示されていましたが、動的な web アプリケーションを作成するために、ビューテンプレートはコントローラーから情報を受信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="0f0cc-406">この目的に使用される一般的な手法の1つは、**モデル**化パターンです。これにより、コントローラーは、適切な HTML 応答を生成するために必要なすべての情報をパッケージ化できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="0f0cc-407">この演習では、ビューモデルクラスを作成し、必要なプロパティを追加する方法を学習します。これには、ストア内のジャンルの数と、それらのジャンルの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="0f0cc-408">また、作成されたビューモデルを使用するように StoreController を更新します。最後に、ページに記載されているプロパティを表示する新しいビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="0f0cc-409">タスク 1-ビューモデルクラスの作成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="0f0cc-410">このタスクでは、ストアのジャンル一覧表示シナリオを実装するビューモデルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="0f0cc-411">まだ開いていない場合は、 **VS Express for Web**を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="0f0cc-412">**[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="0f0cc-413">[プロジェクトを開く] ダイアログで、 **Source05-を**参照し、 **[開始]** を選択して、 **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="0f0cc-414">または、前の演習を完了した後に取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="0f0cc-415">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0f0cc-416">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0f0cc-417">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0f0cc-418">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-419">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0f0cc-420">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0f0cc-421">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="0f0cc-422">ビューモデルを保持する**viewmodel**フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="0f0cc-423">これを行うには、最上位レベルの**MvcMusicStore**プロジェクトを右クリックし、 **[追加]** 、 **[新しいフォルダー]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="0f0cc-424">![新しいフォルダーの追加](aspnet-mvc-4-fundamentals/_static/image17.png "新しいフォルダーの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="0f0cc-425">*新しいフォルダーの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="0f0cc-426">フォルダーに*viewmodel*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="0f0cc-427">![ソリューションエクスプローラーの Viewmodel フォルダー](aspnet-mvc-4-fundamentals/_static/image18.png "ソリューションエクスプローラーの Viewmodel フォルダー")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="0f0cc-428">*ソリューションエクスプローラーの Viewmodel フォルダー*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="0f0cc-429">**ビューモデル**クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="0f0cc-430">これを行うには、最近作成された **[viewmodel]** フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="0f0cc-431">**[コード]** で **[クラス]** 項目を選択し、ファイルに*StoreIndexViewModel.cs*という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="0f0cc-432">![新しいクラスの追加](aspnet-mvc-4-fundamentals/_static/image19.png "新しいクラスの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="0f0cc-433">*新しいクラスの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-433">*Adding a new Class*</span></span>

    <span data-ttu-id="0f0cc-434">![StoreIndexViewModel クラスを作成しています](aspnet-mvc-4-fundamentals/_static/image20.png "StoreIndexViewModel クラスを作成しています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="0f0cc-435">*StoreIndexViewModel クラスを作成しています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="0f0cc-436">タスク 2-ビューモデルクラスにプロパティを追加する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="0f0cc-437">予想される HTML 応答を生成するために、StoreController からビューテンプレートに渡されるパラメーターは2つあります。ストア内のジャンルの数とそれらのジャンルの一覧です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="0f0cc-438">このタスクでは、これら2つのプロパティを**Storeindexviewmodel**クラスに追加します。 **numberofgenres** (整数) と**ジャンル**(文字列のリスト) です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="0f0cc-439">**Numberofgenres**と**ジャンル**のプロパティを**storeindexviewmodel**クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="0f0cc-440">これを行うには、クラス定義に次の2行を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="0f0cc-441">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="0f0cc-442">**{Get; set;}** 表記では、 C#の自動実装プロパティ機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="0f0cc-443">これにより、バッキングフィールドを宣言しなくても、プロパティの利点が得られます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="0f0cc-444">タスク 3-StoreIndexViewModel を使用するための StoreController の更新</span><span class="sxs-lookup"><span data-stu-id="0f0cc-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="0f0cc-445">**Storeindexviewmodel**クラスは、応答を生成するために、 **StoreController**の**インデックス**メソッドからビューテンプレートに渡すために必要な情報をカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="0f0cc-446">このタスクでは、 **Storeindexviewmodel**を使用するように**StoreController**を更新します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="0f0cc-447">**StoreController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="0f0cc-448">![StoreController クラスを開く](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController クラスを開く")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="0f0cc-449">*StoreController クラスを開く*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="0f0cc-450">**StoreController**から**storeindexviewmodel**クラスを使用するには、 **StoreController**コードの先頭に次の名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="0f0cc-451">(コードスニペット- *ASP.NET MVC 4 の基礎-viewmodel を使用した Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="0f0cc-452">StoreController の**インデックス**アクションメソッドを変更して、 **storeindexviewmodel**オブジェクトを作成および設定し、それをビューテンプレートに渡して HTML 応答を生成するようにします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-453">ラボ &quot;ASP.NET MVC モデルとデータアクセス&quot; では、データベースからストアのジャンルの一覧を取得するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="0f0cc-454">次のコードでは、 **Storeindexviewmodel**を設定するダミーデータのジャンルの**一覧**を作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="0f0cc-455">**Storeindexviewmodel**オブジェクトを作成して設定すると、そのオブジェクトは引数として**View**メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="0f0cc-456">これは、ビューテンプレートがそのオブジェクトを使用して HTML 応答を生成することを示します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="0f0cc-457">**Index**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-458">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex5 StoreController Index メソッド*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="0f0cc-459">にC#慣れていない場合は、 **var**を使用すると、**ビューモデル**変数が遅延バインディングされることを想定できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="0f0cc-460">これは適切ではありC#ません。コンパイラは、変数に代入した内容に基づいて、型の推定を使用して、**ビューモデル**が**storeindexviewmodel**型であると判断します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="0f0cc-461">また、ローカルの**ビューモデル**変数を**storeindexviewmodel**形式としてコンパイルすると、コンパイル時チェックと Visual Studio コードエディターのサポートが得られます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="0f0cc-462">タスク 4-StoreIndexViewModel を使用するビューテンプレートを作成する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="0f0cc-463">このタスクでは、コントローラーから渡された StoreIndexViewModel オブジェクトを使用してジャンルの一覧を表示するビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="0f0cc-464">新しいビューテンプレートを作成する前に、[**ビューの追加] ダイアログ**で**storeindexviewmodel**クラスについて理解できるように、プロジェクトをビルドしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="0f0cc-465">**[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="0f0cc-466">![プロジェクトのビルド](aspnet-mvc-4-fundamentals/_static/image22.png "プロジェクトのビルド")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="0f0cc-467">*プロジェクトのビルド*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-467">*Building the project*</span></span>
2. <span data-ttu-id="0f0cc-468">新しいビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-468">Create a new View template.</span></span> <span data-ttu-id="0f0cc-469">これを行うには、 **Index**メソッド内を右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="0f0cc-470">![ビューの追加](aspnet-mvc-4-fundamentals/_static/image23.png "ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="0f0cc-471">*ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-471">*Adding a View*</span></span>
3. <span data-ttu-id="0f0cc-472">[**ビューの追加] ダイアログ**は**StoreController**から呼び出されたため、既定では **\Views\Store\Index.cshtml**ファイルにビューテンプレートが追加されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="0f0cc-473">**[厳密に型指定されたビューを作成する]** チェックボックスをオンにし、**モデルクラス**として **[storeindexviewmodel]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="0f0cc-474">また、選択したビューエンジンが**Razor**であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="0f0cc-475">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-475">Click **Add**.</span></span>

    <span data-ttu-id="0f0cc-476">![[ビューの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image24.png "[ビューの追加] ダイアログ")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="0f0cc-477">*[ビューの追加] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-477">*Add View Dialog*</span></span>

    <span data-ttu-id="0f0cc-478">**\Views\Store\Index.cshtml** View テンプレートファイルが作成されて開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="0f0cc-479">ビューテンプレートでは、最後の手順の **[ビューの追加]** ダイアログに表示される情報に基づいて、 **storeindexviewmodel**インスタンスが HTML 応答の生成に使用するデータとして想定されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="0f0cc-480">テンプレートがのC#`ViewPage<musicstore.viewmodels.storeindexviewmodel>` を継承していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="0f0cc-481">タスク 5-ビューテンプレートを更新する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="0f0cc-482">このタスクでは、最後のタスクで作成されたビューテンプレートを更新して、ページ内のジャンルの数とその名前を取得します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="0f0cc-483">ビューテンプレート内でコードを実行するには、@ 構文 (多くの場合 &quot;code ナゲット&quot;) を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="0f0cc-484">**Index. cshtml**ファイルの**Store**フォルダー内で、コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="0f0cc-485">**Storeindexviewmodel**のジャンルリストをループし、 **foreach**ループを使用して HTML **&lt;ul&gt;** リストを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="0f0cc-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="0f0cc-487">**F5**キーを押してアプリケーションを実行し、[参照] **/[ストア**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="0f0cc-488">**Storeindexviewmodel**からビューテンプレートに渡されたジャンルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="0f0cc-489">![ジャンルの一覧を表示するビュー](aspnet-mvc-4-fundamentals/_static/image26.png "ジャンルの一覧を表示するビュー")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="0f0cc-490">*ジャンルの一覧を表示するビュー*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="0f0cc-491">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="0f0cc-492">演習 6: ビューでのパラメーターの使用</span><span class="sxs-lookup"><span data-stu-id="0f0cc-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="0f0cc-493">演習3では、コントローラーにパラメーターを渡す方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="0f0cc-494">この演習では、ビューテンプレートでこれらのパラメーターを使用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="0f0cc-495">この目的のために、まず、データとドメインロジックを管理するのに役立つモデルクラスを紹介します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="0f0cc-496">また、URL パスのエンコードなどを気にせずに、ASP.NET MVC アプリケーション内のページへのリンクを作成する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="0f0cc-497">タスク 1-モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="0f0cc-498">コントローラーからビューに情報を渡すためだけに作成される Viewmodel とは異なり、モデルクラスはデータとドメインロジックを格納および管理するために構築されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="0f0cc-499">このタスクでは、これらの概念を表す2つのモデルクラス (**ジャンル**と**アルバム**) を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="0f0cc-500">まだ開いていない場合は、開始**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="0f0cc-501">**[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="0f0cc-502">プロジェクトを開く ダイアログで、**ソース**、開始 の順に選択し、**開始** を選択して **開く** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="0f0cc-503">または、前の演習を完了した後に取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="0f0cc-504">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0f0cc-505">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0f0cc-506">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0f0cc-507">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0f0cc-508">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0f0cc-509">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0f0cc-510">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="0f0cc-511">**ジャンル**モデルクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="0f0cc-512">これを行うには、**ソリューションエクスプローラー**で **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="0f0cc-513">**[コード]** で **[クラス]** 項目を選択し、ファイルに*Genre.cs*という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="0f0cc-514">![クラスの追加](aspnet-mvc-4-fundamentals/_static/image27.png "クラスの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="0f0cc-515">*新しい項目の追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-515">*Adding a new item*</span></span>

    <span data-ttu-id="0f0cc-516">![ジャンルモデルクラスの追加](aspnet-mvc-4-fundamentals/_static/image28.png "ジャンルモデルクラスの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="0f0cc-517">*ジャンルモデルクラスの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="0f0cc-518">**名前**プロパティを Genre クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="0f0cc-519">これを行うには、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-519">To do this, add the following code:</span></span>

    <span data-ttu-id="0f0cc-520">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 Genre*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="0f0cc-521">前と同じ手順に従って、**アルバム**クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="0f0cc-522">これを行うには、**ソリューションエクスプローラー**で **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="0f0cc-523">**[コード]** で **[クラス]** 項目を選択し、ファイルに*Album.cs*という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="0f0cc-524">アルバムクラスに**ジャンル**と**タイトル**の2つのプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="0f0cc-525">これを行うには、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-525">To do this, add the following code:</span></span>

    <span data-ttu-id="0f0cc-526">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 アルバム*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="0f0cc-527">タスク 2-StoreBrowseViewModel の追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="0f0cc-528">このタスクでは、選択したジャンルに一致するアルバムを表示するために**StoreBrowseViewModel**が使用されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="0f0cc-529">このタスクでは、このクラスを作成し、**ジャンル**とその**アルバム**の一覧を処理する2つのプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="0f0cc-530">**StoreBrowseViewModel**クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="0f0cc-531">これを行うには、**ソリューションエクスプローラー**で **[viewmodel]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="0f0cc-532">**[コード]** で **[クラス]** 項目を選択し、ファイルに*StoreBrowseViewModel.cs*という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="0f0cc-533">**StoreBrowseViewModel**クラスのモデルへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="0f0cc-534">これを行うには、次の using 名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="0f0cc-535">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 を通じてモデルを*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="0f0cc-536">**StoreBrowseViewModel**クラスに**ジャンル**と**アルバム**の2つのプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="0f0cc-537">これを行うには、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-537">To do this, add the following code:</span></span>

    <span data-ttu-id="0f0cc-538">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="0f0cc-539">**&lt;アルバム&gt;の一覧**とは?: この定義では、**リスト&lt;t&gt;** 型を使用しています。ここで、 **t**は、この**リスト**の要素に属する型 (この場合は**アルバム**(またはその子孫)) を制限します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="0f0cc-540">この機能は、クラスやメソッドが宣言され、クライアントコードによってインスタンス化されるまで、1つ以上の型の仕様を遅延さC#せるクラスとメソッドを設計するための機能です。これは、**ジェネリック**と呼ばれる言語の機能です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="0f0cc-541">**リスト&lt;t&gt;** は**ArrayList**型に相当する汎用であり、 **system.string 名前空間**で使用できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="0f0cc-542">**ジェネリック**を使用する利点の1つは、型が指定されているため、 **ArrayList**の場合と同様に、要素を**アルバム**にキャストするなどの型チェック操作を処理する必要がないことです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="0f0cc-543">タスク 3-StoreController で新しいビューモデルを使用する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="0f0cc-544">このタスクでは、新しい**StoreBrowseViewModel**を使用するように**StoreController**の**Browse**および**Details**アクションメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="0f0cc-545">**StoreController**クラスの [モデル] フォルダーへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="0f0cc-546">これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="0f0cc-547">その後、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-547">Then add the following code:</span></span>

    <span data-ttu-id="0f0cc-548">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 のプラグイン*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="0f0cc-549">**参照**アクションメソッドを置き換えて、 **Storeviewstoretローラ**クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="0f0cc-550">次のハンズオンラボでは、ジャンルと、ダミーデータを含む2つの新しいアルバムオブジェクトを作成します (次のハンズオンラボでは、データベースから実際のデータを使用します)。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="0f0cc-551">これを行うには、 **Browse**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-552">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="0f0cc-553">**詳細**アクションメソッドを置き換えて、 **Storeviewstoretローラ**クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="0f0cc-554">**ビュー**に返される新しい**アルバム**オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="0f0cc-555">これを行うには、 **Details**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="0f0cc-556">(コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 のメソッド*)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="0f0cc-557">タスク 4-参照ビューテンプレートを追加する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="0f0cc-558">このタスクでは、特定のジャンルのアルバムが表示されるように、**参照**ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="0f0cc-559">新しいビューテンプレートを作成する前に、プロジェクトをビルドして、 **[ビューの追加]** ダイアログが使用するビュー**モデル**クラスを認識できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="0f0cc-560">**[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="0f0cc-561">**参照**ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-561">Add a **Browse** View.</span></span> <span data-ttu-id="0f0cc-562">これを行うには、 **StoreController**の **[参照]** アクションメソッドを右クリックし、 **[ビューの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="0f0cc-563">**[ビューの追加]** ダイアログボックスで、ビュー名が **[参照]** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="0f0cc-564">厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[モデルクラス]** ドロップダウンから **[StoreBrowseViewModel]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="0f0cc-565">他のフィールドは既定値のままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="0f0cc-566">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-566">Then click **Add**.</span></span>

    <span data-ttu-id="0f0cc-567">![参照ビューの追加](aspnet-mvc-4-fundamentals/_static/image29.png "参照ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="0f0cc-568">*参照ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="0f0cc-569">ビューテンプレートに渡される**StoreBrowseViewModel**オブジェクトにアクセスして、Genre の情報を表示するように、Browse を変更し**ます**。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="0f0cc-570">これを行うには、内容を次のようにC#置き換えます。 ()</span><span class="sxs-lookup"><span data-stu-id="0f0cc-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="0f0cc-571">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="0f0cc-572">このタスクでは **、browse メソッドが** **browse**メソッドアクションからアルバムを取得することをテストします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="0f0cc-573">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-574">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-574">The project starts in the Home page.</span></span> <span data-ttu-id="0f0cc-575">URL を「 **/Store/Browse」に変更します。Genre = Disco**は、アクションが2つのアルバムを返すことを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="0f0cc-576">![ストアの Disco アルバムの参照](aspnet-mvc-4-fundamentals/_static/image30.png "ストアの Disco アルバムの参照")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="0f0cc-577">*ストアの Disco アルバムの参照*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="0f0cc-578">タスク 6-特定のアルバムに関する情報を表示する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="0f0cc-579">このタスクでは、 **[ストア/詳細]** ビューを実装して、特定のアルバムに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="0f0cc-580">このハンズオンラボでは、アルバムに関して表示されるすべてのものが、既に**ビュー**テンプレートに含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="0f0cc-581">そのため、 **StoreStoreBrowseViewModel ビューモデル**クラスを作成するのではなく、現在のテンプレートを使用してアルバムに渡します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="0f0cc-582">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="0f0cc-583">**StoreController**の**details**アクションメソッドの新しい**詳細**ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="0f0cc-584">これを行うには、 **StoreController**クラスの**詳細**メソッドを右クリックし、 **[ビューの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="0f0cc-585">**[ビューの追加]** ダイアログで、**ビュー名**が **[詳細]** であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="0f0cc-586">厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[モデルクラス]** ドロップダウンから **[アルバム]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="0f0cc-587">他のフィールドは既定値のままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="0f0cc-588">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-588">Then click **Add**.</span></span> <span data-ttu-id="0f0cc-589">これにより、 **\Views\Store\Details.cshtml**ファイルが作成されて開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="0f0cc-590">![詳細ビューの追加](aspnet-mvc-4-fundamentals/_static/image31.png "詳細ビューの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="0f0cc-591">*詳細ビューの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="0f0cc-592">詳細の**cshtml**ファイルを変更して、アルバムの情報を表示し、ビューテンプレートに渡される**アルバム**オブジェクトにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="0f0cc-593">これを行うには、内容を次のようにC#置き換えます。 ()</span><span class="sxs-lookup"><span data-stu-id="0f0cc-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="0f0cc-594">タスク 7-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="0f0cc-595">このタスクで**は、詳細ビューが** **詳細アクション**メソッドからアルバムの情報を取得することをテストします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="0f0cc-596">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-597">プロジェクトは**ホーム**ページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="0f0cc-598">アルバムの情報を確認するには、URL を **/ストア/詳細/5**に変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="0f0cc-599">![アルバムの閲覧の詳細](aspnet-mvc-4-fundamentals/_static/image32.png "アルバムの閲覧の詳細")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="0f0cc-600">*アルバムの詳細を閲覧する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="0f0cc-601">タスク 8-ページ間のリンクの追加</span><span class="sxs-lookup"><span data-stu-id="0f0cc-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="0f0cc-602">このタスクでは、ストアビューにリンクを追加して、各ジャンル名のリンクを適切な **/storeurl**にリンクします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="0f0cc-603">このようにして、ジャンルをクリックすると、 **[ディスコ]** 、[**参照]** 、[ジャンル]、[ディスコ URL] の順に移動します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="0f0cc-604">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="0f0cc-605">**[インデックス]** ページを更新して、 **[参照]** ページへのリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="0f0cc-606">この操作を行うには、**ソリューションエクスプローラー** **Views**  フォルダーを展開し、**Store** フォルダーをクリックして、**Index. cshtml** ページをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="0f0cc-607">選択したジャンルを示すリンクを参照ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="0f0cc-608">これを行うには、 **&lt;li&gt;** タグ内の強調表示されたC#次のコードを置き換えます。 ()</span><span class="sxs-lookup"><span data-stu-id="0f0cc-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="0f0cc-609">別の方法として、次のようなコードを使用して、ページに直接リンクすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="0f0cc-610">href =&quot;/Store/Browse? genre =@genreName&quot;&gt;@genreName&lt;/a &lt;&gt;</span><span class="sxs-lookup"><span data-stu-id="0f0cc-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="0f0cc-611">この方法は機能しますが、ハードコーディングされた文字列に依存します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="0f0cc-612">後でコントローラーの名前を変更する場合は、この手順を手動で変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="0f0cc-613">代わりに、 **HTML ヘルパー**メソッドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="0f0cc-614">ASP.NET MVC には、このようなタスクで使用できる HTML ヘルパーメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="0f0cc-615">**Html.actionlink ()** ヘルパーメソッドを使用すると、 **&gt;リンク&lt;** html を簡単に作成できるため、url パスが適切に url エンコードされます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="0f0cc-616">Html.actionlink にはいくつかのオーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="0f0cc-617">この演習では、次の3つのパラメーターを受け取るものを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="0f0cc-618">ジャンル名を表示するリンクテキスト</span><span class="sxs-lookup"><span data-stu-id="0f0cc-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="0f0cc-619">コントローラーアクション名 (**参照**)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="0f0cc-620">ルートパラメーターの値。名前 (**ジャンル**) と値 (**ジャンル名**) の両方を指定します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="0f0cc-621">タスク 9-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="0f0cc-622">このタスクでは、各ジャンルが適切な **/Store/参照**URL へのリンクと共に表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="0f0cc-623">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-624">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-624">The project starts in the Home page.</span></span> <span data-ttu-id="0f0cc-625">URL を **/Store**に変更して、各ジャンルが適切な **/** ストア URL にリンクされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="0f0cc-626">![閲覧ページへのリンクを使用したジャンルの参照](aspnet-mvc-4-fundamentals/_static/image33.png "閲覧ページへのリンクを使用したジャンルの参照")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="0f0cc-627">*閲覧ページへのリンクを使用したジャンルの参照*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="0f0cc-628">タスク 10-動的なビューモデルのコレクションを使用した値の引き渡し</span><span class="sxs-lookup"><span data-stu-id="0f0cc-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="0f0cc-629">このタスクでは、モデルを変更せずに、コントローラーとビューの間で値を渡すシンプルで強力な方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="0f0cc-630">ASP.NET MVC 4 は、コレクション &quot;モデル&quot;を提供します。これを任意の動的な値に割り当てて、コントローラーやビュー内でアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="0f0cc-631">次に、ViewBag 動的コレクションを使用して、コントローラーからビューに &quot;**星付きジャンル**&quot; の一覧を渡します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="0f0cc-632">ストアインデックスビューは、ビュー**モデル**にアクセスして情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="0f0cc-633">必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="0f0cc-634">**StoreController.cs**を開き、 **Index**メソッドを変更して、星付きジャンルのリストをビューモデルコレクションに作成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="0f0cc-635">また、構文**ViewBag [&quot;星付き&quot;]** を使用してプロパティにアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="0f0cc-636">このラボの**Source\Assets\Images**フォルダーには、**星付き&quot;&quot;** star アイコンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="0f0cc-637">アプリケーションに追加するには、次に示すように、 **Windows エクスプローラー**ウィンドウから Visual Web Developer Express の**ソリューションエクスプローラー**にコンテンツをドラッグします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="0f0cc-638">![ソリューションへのスターイメージの追加](aspnet-mvc-4-fundamentals/_static/image34.png "ソリューションへのスターイメージの追加")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="0f0cc-639">*ソリューションへのスターイメージの追加*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="0f0cc-640">ビュー**ストア/インデックス**を開き、内容を変更します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="0f0cc-641">**ViewBag**コレクションで &quot;星付き&quot; プロパティを読み取り、現在のジャンル名が一覧に含まれているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="0f0cc-642">その場合は、ジャンルのリンクに星のアイコンを表示します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="0f0cc-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="0f0cc-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="0f0cc-644">タスク 11-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="0f0cc-645">このタスクでは、星付きのジャンルに星のアイコンが表示されることをテストします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="0f0cc-646">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="0f0cc-647">プロジェクトは**ホーム**ページから開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="0f0cc-648">URL を「 **/Store** 」に変更して、おすすめの各ジャンルに次のラベルが付いていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="0f0cc-649">![星付き要素を使用したジャンルの参照](aspnet-mvc-4-fundamentals/_static/image35.png "星付き要素を使用したジャンルの参照")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="0f0cc-650">*星付き要素を使用したジャンルの参照*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="0f0cc-651">演習 7: ASP.NET MVC 4 の新しいテンプレートをラップする</span><span class="sxs-lookup"><span data-stu-id="0f0cc-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="0f0cc-652">この演習では、ASP.NET MVC 4 プロジェクトテンプレートの機能強化について説明し、新しいテンプレートの最も関連する機能を見ていきます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="0f0cc-653">タスク 1: ASP.NET MVC 4 インターネットアプリケーションテンプレートを探索する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="0f0cc-654">まだ開いていない場合は、開始**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="0f0cc-655">ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="0f0cc-656">**[新しいプロジェクト]** ダイアログで、[ **Visual C#|] を選択します。** 左側のウィンドウツリーで [Web テンプレート] を選択し、 **ASP.NET MVC 4 web アプリケーション**を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="0f0cc-657">プロジェクトに*MusicStore*という**名前**を設定し、**ソリューション名**を*開始*するように更新してから、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="0f0cc-658">![新しい ASP.NET MVC 4 プロジェクトを作成する](aspnet-mvc-4-fundamentals/_static/image36.png "新しい ASP.NET MVC 4 プロジェクトを作成する")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="0f0cc-659">*新しい ASP.NET MVC 4 プロジェクトを作成する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="0f0cc-660">**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="0f0cc-661">ビューエンジンとして Razor または ASPX を選択できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="0f0cc-662">![新しい ASP.NET MVC 4 インターネットアプリケーションを作成する](aspnet-mvc-4-fundamentals/_static/image37.png "新しい ASP.NET MVC 4 インターネットアプリケーションを作成する")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="0f0cc-663">*新しい ASP.NET MVC 4 インターネットアプリケーションを作成する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-664">Razor 構文は、ASP.NET MVC 3 で導入されました。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="0f0cc-665">その目的は、ファイルで必要とされる文字数とキーストローク数を最小限に抑えることです。これにより、高速で滑らかなコーディングワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="0f0cc-666">既存 C#/VB (またはその他) を活用する razor 言語スキルと最高の HTML の構築ワークフローを有効にするテンプレート マークアップ構文を提供します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="0f0cc-667">**F5**キーを押してソリューションを実行し、更新されたテンプレートを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="0f0cc-668">次の機能を確認できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="0f0cc-669">**モダンスタイルのテンプレート**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-669">**Modern-style templates**</span></span>

        <span data-ttu-id="0f0cc-670">テンプレートが更新され、最新のスタイルを提供しています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="0f0cc-671">![ASP.NET MVC 4 の再スタイル化テンプレート](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 の再スタイル化テンプレート")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="0f0cc-672">*ASP.NET MVC 4 の再スタイル化テンプレート*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="0f0cc-673">**アダプティブレンダリング**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="0f0cc-674">ブラウザーウィンドウのサイズを変更し、ページレイアウトが新しいウィンドウサイズに動的に適応することを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="0f0cc-675">これらのテンプレートでは、アダプティブレンダリング技法を使用して、デスクトップとモバイルの両方のプラットフォームで適切にレンダリングできます。カスタマイズは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="0f0cc-676">![さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート](aspnet-mvc-4-fundamentals/_static/image39.png "さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="0f0cc-677">*さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="0f0cc-678">ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="0f0cc-679">これで、ソリューションを調査し、プロジェクトテンプレートで ASP.NET MVC 4 によって導入された新機能の一部を確認できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="0f0cc-680">![ASP.NET MVC4 (プロジェクトテンプレート)](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="0f0cc-681">*ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="0f0cc-682">**HTML5 マークアップ**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-682">**HTML5 markup**</span></span>

       <span data-ttu-id="0f0cc-683">テンプレートビューを参照して新しいテーママークアップを確認します。たとえば、 **[ホーム]** フォルダー内の **[... cshtml]** ビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="0f0cc-684">![新しいテンプレート、Razor および HTML5 マークアップの使用](aspnet-mvc-4-fundamentals/_static/image41.png "新しいテンプレート、Razor および HTML5 マークアップの使用")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="0f0cc-685">*新しいテンプレート、Razor および HTML5 マークアップの使用*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="0f0cc-686">**含まれている JavaScript ライブラリ**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="0f0cc-687">**jquery**: jquery は、HTML ドキュメントの走査、イベント処理、アニメーション化、および Ajax 相互作用を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="0f0cc-688">**JQUERY UI**: このライブラリは、Jquery JavaScript ライブラリ上に構築された低レベルの相互作用とアニメーション、高度な効果、および可能なウィジェットの抽象化を提供します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="0f0cc-689">[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)では、jQuery と jquery UI について学習できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="0f0cc-690">**KnockoutJS**: ASP.NET MVC 4 の既定のテンプレートに**KnockoutJS**が含まれるようになりました。 javascript と HTML を使用して、高度で応答性の高い web アプリケーションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="0f0cc-691">ASP.NET MVC 3 の場合と同様に、jQuery および jQuery UI ライブラリも ASP.NET MVC 4 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="0f0cc-692">KnockOutJS library の詳細については、「 [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="0f0cc-693">**Modernizr**: このライブラリは自動的に実行され、HTML5 および CSS3 テクノロジを使用するときに、サイトと古いブラウザーとの互換性を確保します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="0f0cc-694">Modernizr ライブラリの詳細については、「 [http://www.modernizr.com/](http://www.modernizr.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="0f0cc-695">**ソリューションに含まれる SimpleMembership**</span><span class="sxs-lookup"><span data-stu-id="0f0cc-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="0f0cc-696">SimpleMembership は、前の ASP.NET ロールおよびメンバーシッププロバイダーシステムに代わるものとして設計されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="0f0cc-697">これには、開発者が web ページをより柔軟にセキュリティで保護するための多くの新機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="0f0cc-698">インターネットテンプレートでは、SimpleMembership を統合するためのいくつかの処理が既に完了しています。たとえば、AccountController は OAuthWebSecurity (OAuth アカウントの登録、ログイン、管理など) と Web セキュリティを使用するために準備されています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="0f0cc-699">![ソリューションに含まれる SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "ソリューションに含まれる SimpleMembership")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="0f0cc-700">*ソリューションに含まれる SimpleMembership*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="0f0cc-701">[Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)の詳細については、MSDN を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="0f0cc-702">また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="0f0cc-703">まとめ</span><span class="sxs-lookup"><span data-stu-id="0f0cc-703">Summary</span></span>

<span data-ttu-id="0f0cc-704">このハンズオンラボを完了することで、ASP.NET MVC の基本を学習できました。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="0f0cc-705">MVC アプリケーションのコア要素とその相互作用</span><span class="sxs-lookup"><span data-stu-id="0f0cc-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="0f0cc-706">ASP.NET MVC アプリケーションを作成する方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="0f0cc-707">URL と querystring を通じて渡されるパラメーターを処理するようにコントローラーを追加および構成する方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="0f0cc-708">共通の HTML コンテンツ用のテンプレートを設定するためのレイアウトマスターページの追加方法、外観を強化するためのスタイルシート、および HTML コンテンツを表示するためのビューテンプレート</span><span class="sxs-lookup"><span data-stu-id="0f0cc-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="0f0cc-709">ビューテンプレートにプロパティを渡して動的な情報を表示するために、ビューモデルパターンを使用する方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="0f0cc-710">ビューテンプレートでコントローラーに渡されるパラメーターの使用方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="0f0cc-711">ASP.NET MVC アプリケーション内のページにリンクを追加する方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="0f0cc-712">ビューに動的プロパティを追加して使用する方法</span><span class="sxs-lookup"><span data-stu-id="0f0cc-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="0f0cc-713">ASP.NET MVC 4 プロジェクトテンプレートの機能強化</span><span class="sxs-lookup"><span data-stu-id="0f0cc-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="0f0cc-714">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="0f0cc-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="0f0cc-715">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="0f0cc-716">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="0f0cc-717">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0f0cc-718">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="0f0cc-719">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-719">Click on **Install Now**.</span></span> <span data-ttu-id="0f0cc-720">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0f0cc-721">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0f0cc-722">![Visual Studio Express のインストール](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="0f0cc-723">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="0f0cc-724">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="0f0cc-726">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0f0cc-727">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-727">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="0f0cc-729">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-729">*Installation progress*</span></span>
6. <span data-ttu-id="0f0cc-730">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-730">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="0f0cc-732">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-732">*Installation completed*</span></span>
7. <span data-ttu-id="0f0cc-733">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="0f0cc-734">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="0f0cc-736">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0f0cc-737">付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="0f0cc-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="0f0cc-738">この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="0f0cc-739">タスク 1-Windows Azure ポータルから新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="0f0cc-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="0f0cc-740">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-741">Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="0f0cc-742">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="0f0cc-743">![Windows Azure portal にログオンします。](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="0f0cc-744">*Windows Azure 管理ポータルにログオンします。*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="0f0cc-745">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="0f0cc-746">![新しい Web サイトの作成](aspnet-mvc-4-fundamentals/_static/image49.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="0f0cc-747">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="0f0cc-748">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="0f0cc-749">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="0f0cc-750">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-751">Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="0f0cc-752">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="0f0cc-753">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="0f0cc-754">![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-fundamentals/_static/image50.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="0f0cc-755">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="0f0cc-756">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="0f0cc-757">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="0f0cc-758">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="0f0cc-759">![新しい web サイトを参照しています](aspnet-mvc-4-fundamentals/_static/image51.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="0f0cc-760">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="0f0cc-761">![実行中の Web サイト](aspnet-mvc-4-fundamentals/_static/image52.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="0f0cc-762">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-762">*Web site running*</span></span>
6. <span data-ttu-id="0f0cc-763">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="0f0cc-764">![Web サイトの管理ページを開く](aspnet-mvc-4-fundamentals/_static/image53.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="0f0cc-765">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="0f0cc-766">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-767">*発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="0f0cc-768">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="0f0cc-769">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="0f0cc-770">![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-fundamentals/_static/image54.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="0f0cc-771">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="0f0cc-772">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="0f0cc-773">この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="0f0cc-774">![発行プロファイルファイルを保存しています](aspnet-mvc-4-fundamentals/_static/image55.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="0f0cc-775">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="0f0cc-776">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="0f0cc-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="0f0cc-777">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="0f0cc-778">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="0f0cc-779">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="0f0cc-780">サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="0f0cc-781">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="0f0cc-782">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="0f0cc-783">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="0f0cc-784">![SQL Database サーバーダッシュボード](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="0f0cc-785">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="0f0cc-786">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="0f0cc-787">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-fundamentals/_static/image57.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="0f0cc-789">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="0f0cc-790">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="0f0cc-792">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0f0cc-793">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="0f0cc-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="0f0cc-794">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="0f0cc-795">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="0f0cc-796">![アプリケーションの発行](aspnet-mvc-4-fundamentals/_static/image60.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="0f0cc-797">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="0f0cc-798">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="0f0cc-799">![発行プロファイルをインポートしています](aspnet-mvc-4-fundamentals/_static/image61.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="0f0cc-800">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="0f0cc-801">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-801">Click **Validate Connection**.</span></span> <span data-ttu-id="0f0cc-802">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f0cc-803">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="0f0cc-804">![接続の検証](aspnet-mvc-4-fundamentals/_static/image62.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="0f0cc-805">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-805">*Validating connection*</span></span>
4. <span data-ttu-id="0f0cc-806">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="0f0cc-807">![Web deploy の構成](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="0f0cc-808">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="0f0cc-809">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="0f0cc-810">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="0f0cc-811">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="0f0cc-812">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="0f0cc-813">新しいデータベース名を入力します (例: *MVC4SampleDB*)。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="0f0cc-814">![変換先の接続文字列を構成しています](aspnet-mvc-4-fundamentals/_static/image64.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="0f0cc-815">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="0f0cc-816">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="0f0cc-816">Then click **OK**.</span></span> <span data-ttu-id="0f0cc-817">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="0f0cc-818">![データベースの作成](aspnet-mvc-4-fundamentals/_static/image65.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="0f0cc-819">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-819">*Creating the database*</span></span>
7. <span data-ttu-id="0f0cc-820">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="0f0cc-821">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-821">Then click **Next**.</span></span>

    <span data-ttu-id="0f0cc-822">![SQL Database を指す接続文字列](aspnet-mvc-4-fundamentals/_static/image66.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="0f0cc-823">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="0f0cc-824">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="0f0cc-825">![Web アプリケーションの発行](aspnet-mvc-4-fundamentals/_static/image67.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="0f0cc-826">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="0f0cc-827">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="0f0cc-828">![Windows Azure に発行されたアプリケーション](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure に発行されたアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="0f0cc-829">*Windows Azure に発行されたアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="0f0cc-830">付録 C: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="0f0cc-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="0f0cc-831">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="0f0cc-832">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="0f0cc-833">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="0f0cc-834">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="0f0cc-835">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="0f0cc-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="0f0cc-836">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="0f0cc-837">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="0f0cc-838">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="0f0cc-839">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="0f0cc-840">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="0f0cc-841">![スニペット名の入力を開始します](aspnet-mvc-4-fundamentals/_static/image70.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="0f0cc-842">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="0f0cc-843">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-fundamentals/_static/image71.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="0f0cc-844">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="0f0cc-845">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-fundamentals/_static/image72.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="0f0cc-846">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="0f0cc-847">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="0f0cc-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="0f0cc-848">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="0f0cc-849">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="0f0cc-850">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="0f0cc-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="0f0cc-851">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-fundamentals/_static/image73.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="0f0cc-852">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="0f0cc-853">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-fundamentals/_static/image74.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="0f0cc-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="0f0cc-854">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="0f0cc-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
