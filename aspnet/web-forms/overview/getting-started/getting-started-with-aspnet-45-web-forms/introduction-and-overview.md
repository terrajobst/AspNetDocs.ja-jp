---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web フォームと Visual Studio 2017 でのはじめにMicrosoft Docs
author: Erikre
description: このステップバイステップチュートリアルシリーズでは、ASP.NET 4.7 Microsoft Visual Studio とを使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458344"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="cf871-103">ASP.NET 4.5 Web フォームと Visual Studio 2017 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="cf871-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="cf871-104">[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。</span><span class="sxs-lookup"><span data-stu-id="cf871-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="cf871-105">このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="cf871-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="cf871-106">はじめに</span><span class="sxs-lookup"><span data-stu-id="cf871-106">Introduction</span></span>

<span data-ttu-id="cf871-107">このチュートリアルシリーズでは、Visual Studio 2017 と ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを作成する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="cf871-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="cf871-108">**Wingtip Toys**という名前のアプリケーションを作成します。これは、簡素化されたストア web サイトで、オンラインでアイテムを販売します。</span><span class="sxs-lookup"><span data-stu-id="cf871-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="cf871-109">シリーズの中で、新しい ASP.NET 4.5 の機能が強調表示されています。</span><span class="sxs-lookup"><span data-stu-id="cf871-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="cf871-110">対象読者</span><span class="sxs-lookup"><span data-stu-id="cf871-110">Target audience</span></span>

<span data-ttu-id="cf871-111">ASP.NET Web フォームを初めて使用する開発者は、このチュートリアルシリーズの対象ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="cf871-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="cf871-112">次の領域には、いくつかの知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="cf871-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="cf871-113">オブジェクト指向プログラミング (OOP) と言語</span><span class="sxs-lookup"><span data-stu-id="cf871-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="cf871-114">Web 開発 (HTML、CSS、JavaScript)</span><span class="sxs-lookup"><span data-stu-id="cf871-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="cf871-115">リレーショナル データベース</span><span class="sxs-lookup"><span data-stu-id="cf871-115">Relational databases</span></span>
- <span data-ttu-id="cf871-116">n 層アーキテクチャ</span><span class="sxs-lookup"><span data-stu-id="cf871-116">N-tier architecture</span></span>

<span data-ttu-id="cf871-117">これらの領域を確認するには、次の内容を確認することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="cf871-118">Visual C# 入門</span><span class="sxs-lookup"><span data-stu-id="cf871-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="cf871-119">[Web 開発](https://msdn.microsoft.com/beginner/bb308760.aspx)、 [HTML、CSS、JavaScript、SQL、PHP、JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="cf871-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="cf871-120">リレーショナル データベース</span><span class="sxs-lookup"><span data-stu-id="cf871-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="cf871-121">多層アーキテクチャ</span><span class="sxs-lookup"><span data-stu-id="cf871-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="cf871-122">アプリケーションの機能</span><span class="sxs-lookup"><span data-stu-id="cf871-122">Application features</span></span>

<span data-ttu-id="cf871-123">このシリーズでは、次のような ASP.NET Web フォーム機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="cf871-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="cf871-124">Web アプリケーションプロジェクト (Web サイトプロジェクトではない)</span><span class="sxs-lookup"><span data-stu-id="cf871-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="cf871-125">Web フォーム</span><span class="sxs-lookup"><span data-stu-id="cf871-125">Web Forms</span></span>
- <span data-ttu-id="cf871-126">マスターページ、構成</span><span class="sxs-lookup"><span data-stu-id="cf871-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="cf871-127">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="cf871-127">Bootstrap</span></span>
- <span data-ttu-id="cf871-128">Entity Framework Code First、LocalDB</span><span class="sxs-lookup"><span data-stu-id="cf871-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="cf871-129">要求の検証</span><span class="sxs-lookup"><span data-stu-id="cf871-129">Request Validation</span></span>
- <span data-ttu-id="cf871-130">厳密に型指定されたデータコントロール</span><span class="sxs-lookup"><span data-stu-id="cf871-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="cf871-131">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="cf871-131">Model Binding</span></span>
- <span data-ttu-id="cf871-132">データの注釈</span><span class="sxs-lookup"><span data-stu-id="cf871-132">Data Annotations</span></span>
- <span data-ttu-id="cf871-133">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="cf871-133">Value Providers</span></span>
- <span data-ttu-id="cf871-134">SSL と OAuth</span><span class="sxs-lookup"><span data-stu-id="cf871-134">SSL and OAuth</span></span>
- <span data-ttu-id="cf871-135">ASP.NET Identity、構成、および承認</span><span class="sxs-lookup"><span data-stu-id="cf871-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="cf871-136">控えめに検証</span><span class="sxs-lookup"><span data-stu-id="cf871-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="cf871-137">ルーティング</span><span class="sxs-lookup"><span data-stu-id="cf871-137">Routing</span></span>
- <span data-ttu-id="cf871-138">ASP.NET エラー処理</span><span class="sxs-lookup"><span data-stu-id="cf871-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="cf871-139">アプリケーションのシナリオとタスク</span><span class="sxs-lookup"><span data-stu-id="cf871-139">Application scenarios and tasks</span></span>

<span data-ttu-id="cf871-140">チュートリアルシリーズのタスクは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cf871-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="cf871-141">新しいプロジェクトの作成、確認、および実行</span><span class="sxs-lookup"><span data-stu-id="cf871-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="cf871-142">データベース構造の作成</span><span class="sxs-lookup"><span data-stu-id="cf871-142">Creating a database structure</span></span>
- <span data-ttu-id="cf871-143">データベースの初期化とシード処理</span><span class="sxs-lookup"><span data-stu-id="cf871-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="cf871-144">スタイル、グラフィックス、およびマスターページを使用した UI のカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="cf871-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="cf871-145">ページおよびナビゲーションの追加</span><span class="sxs-lookup"><span data-stu-id="cf871-145">Adding pages and navigation</span></span>
- <span data-ttu-id="cf871-146">メニューの詳細と製品データを表示する</span><span class="sxs-lookup"><span data-stu-id="cf871-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="cf871-147">ショッピングカートの作成</span><span class="sxs-lookup"><span data-stu-id="cf871-147">Creating a shopping cart</span></span>
- <span data-ttu-id="cf871-148">SSL および OAuth サポートの追加</span><span class="sxs-lookup"><span data-stu-id="cf871-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="cf871-149">支払い方法の追加</span><span class="sxs-lookup"><span data-stu-id="cf871-149">Adding a payment method</span></span>
- <span data-ttu-id="cf871-150">管理者ロールとユーザーをアプリケーションに含める</span><span class="sxs-lookup"><span data-stu-id="cf871-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="cf871-151">特定のページおよびフォルダーへのアクセスを制限する</span><span class="sxs-lookup"><span data-stu-id="cf871-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="cf871-152">Web アプリケーションへのファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="cf871-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="cf871-153">入力検証の実装</span><span class="sxs-lookup"><span data-stu-id="cf871-153">Implementing input validation</span></span>
- <span data-ttu-id="cf871-154">Web アプリケーションのルートを登録しています</span><span class="sxs-lookup"><span data-stu-id="cf871-154">Registering routes for the web application</span></span>
- <span data-ttu-id="cf871-155">エラー処理とエラーログの実装</span><span class="sxs-lookup"><span data-stu-id="cf871-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="cf871-156">概要</span><span class="sxs-lookup"><span data-stu-id="cf871-156">Overview</span></span>

<span data-ttu-id="cf871-157">このチュートリアルシリーズは、プログラミングの概念に習熟している方を対象としていますが、ASP.NET Web フォームが新しく追加されました。</span><span class="sxs-lookup"><span data-stu-id="cf871-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="cf871-158">ASP.NET の Web フォームを既に使い慣れている場合でも、このシリーズでは、ASP.NET 4.5 の新機能について学習できます。</span><span class="sxs-lookup"><span data-stu-id="cf871-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="cf871-159">プログラミングの概念と ASP.NET の Web フォームに慣れていない読者には、ASP.NET Web サイトの[はじめに](../../../index.md)セクションに記載されている追加の web フォームチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="cf871-160">このチュートリアルシリーズで提供されている ASP.NET 4.5 には、次の機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="cf871-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="cf871-161">[多くの ASP.NET フレームワーク](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)(web フォーム、MVC、web API) をサポートするプロジェクトを作成するための簡単な UI です。</span><span class="sxs-lookup"><span data-stu-id="cf871-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="cf871-162">[ブートストラップ](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)、レイアウト、テーマ、および応答性のデザインフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="cf871-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="cf871-163">[ASP.NET Identity](../../../../identity/index.md)、すべての ASP.NET フレームワークで同じように動作し、IIS 以外の web ホスティングソフトウェアで動作する新しい ASP.NET メンバーシップシステムです。</span><span class="sxs-lookup"><span data-stu-id="cf871-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="cf871-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="cf871-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="cf871-165">Entity Framework の更新により、次のことが可能になります。</span><span class="sxs-lookup"><span data-stu-id="cf871-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="cf871-166">厳密に型指定されたオブジェクトとしてデータを取得および操作する</span><span class="sxs-lookup"><span data-stu-id="cf871-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="cf871-167">データへの非同期アクセス</span><span class="sxs-lookup"><span data-stu-id="cf871-167">Access data asynchronously</span></span>
  - <span data-ttu-id="cf871-168">一時的な接続エラーの処理</span><span class="sxs-lookup"><span data-stu-id="cf871-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="cf871-169">ログ SQL ステートメント</span><span class="sxs-lookup"><span data-stu-id="cf871-169">Log SQL statements</span></span>

<span data-ttu-id="cf871-170">ASP.NET 4.5 の完全な機能一覧については、 [Visual Studio 2013 リリースノートの ASP.NET and Web Tools](../../../../visual-studio/overview/2013/release-notes.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="cf871-171">Wingtip Toys サンプルアプリケーション</span><span class="sxs-lookup"><span data-stu-id="cf871-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="cf871-172">次のスクリーンショットは、このチュートリアルシリーズで作成する ASP.NET Web フォームアプリケーションのものです。</span><span class="sxs-lookup"><span data-stu-id="cf871-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="cf871-173">Visual Studio でアプリケーションを実行すると、次の web ホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf871-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys-既定のページ](introduction-and-overview/_static/image1.png)

<span data-ttu-id="cf871-175">新しいユーザーとして登録することも、既存のユーザーとしてサインインすることもできます。</span><span class="sxs-lookup"><span data-stu-id="cf871-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="cf871-176">上部のナビゲーションには、データベースから製品カテゴリと製品へのリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="cf871-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="cf871-177">**[製品]** を選択すると、利用可能なすべての製品が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf871-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip Toys-製品](introduction-and-overview/_static/image2.png)

<span data-ttu-id="cf871-179">特定の製品を選択すると、製品の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf871-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip Toys-製品の詳細](introduction-and-overview/_static/image3.png)

<span data-ttu-id="cf871-181">ユーザーは、Web フォームテンプレートの既定の機能を使用して、登録とサインインを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="cf871-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="cf871-182">このチュートリアルでは、既存の Gmail アカウントを使用してサインインする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="cf871-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="cf871-183">また、管理者としてサインインして、データベースの製品を追加および削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="cf871-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-サインイン](introduction-and-overview/_static/image4.png)

<span data-ttu-id="cf871-185">ユーザーとしてサインインすると、ショッピングカートに製品を追加して、PayPal でチェックアウトできます。</span><span class="sxs-lookup"><span data-stu-id="cf871-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="cf871-186">このサンプルアプリケーションは、PayPal の開発者サンドボックスで動作するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="cf871-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="cf871-187">実際の金額トランザクションは発生しません。</span><span class="sxs-lookup"><span data-stu-id="cf871-187">No actual money transaction takes place.</span></span>

![Wingtip Toys-ショッピングカート](introduction-and-overview/_static/image5.png)

<span data-ttu-id="cf871-189">PayPal は、お客様のアカウント、注文、支払い情報を確認します。</span><span class="sxs-lookup"><span data-stu-id="cf871-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="cf871-191">PayPal から戻った後、注文を確認して完了することができます。</span><span class="sxs-lookup"><span data-stu-id="cf871-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-注文レビュー](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="cf871-193">前提条件</span><span class="sxs-lookup"><span data-stu-id="cf871-193">Prerequisites</span></span>

<span data-ttu-id="cf871-194">開始する前に、次のソフトウェアがコンピューターにインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="cf871-195">[Microsoft Visual Studio 2017 または Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="cf871-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="cf871-196">.NET Framework は自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="cf871-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="cf871-197">このチュートリアルシリーズでは、Microsoft Visual Studio Community 2017 を使用します。</span><span class="sxs-lookup"><span data-stu-id="cf871-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="cf871-198">このチュートリアルシリーズを完了するには、または Microsoft Visual Studio 2017 を使用できます。</span><span class="sxs-lookup"><span data-stu-id="cf871-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="cf871-199">Visual Studio については、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="cf871-200">このチュートリアルシリーズでは、Microsoft Visual Studio 2017 と Microsoft Visual Studio Community 2017 を*Visual Studio*と呼びます。</span><span class="sxs-lookup"><span data-stu-id="cf871-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="cf871-201">Visual Studio 2017 は、既にインストールされている古いバージョンの横にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="cf871-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="cf871-202">以前のバージョンで作成されたサイトは Visual Studio 2017 で開くことができ、以前のバージョンでは引き続き開くことができます。</span><span class="sxs-lookup"><span data-stu-id="cf871-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="cf871-203">Visual Studio を初めて起動したときは、 *Web 開発*設定を選択したと見なされます。</span><span class="sxs-lookup"><span data-stu-id="cf871-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="cf871-204">詳細については、「[方法: Web 開発環境の設定を選択する](https://msdn.microsoft.com/library/ff521558.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="cf871-205">前提条件をインストールしたら、このチュートリアルシリーズで紹介する Web プロジェクトの作成を開始できます。</span><span class="sxs-lookup"><span data-stu-id="cf871-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="cf871-206">サンプル アプリケーションのダウンロード</span><span class="sxs-lookup"><span data-stu-id="cf871-206">Download the sample application</span></span>

 <span data-ttu-id="cf871-207">完成したサンプルアプリケーションは、MSDN サンプルサイトからいつでもダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="cf871-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="cf871-208">C# [ASP.NET 4.5 Web フォームと Visual Studio 2013-Wingtip Toys () を使用したはじめに](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="cf871-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="cf871-209">このダウンロードには次の項目があります。</span><span class="sxs-lookup"><span data-stu-id="cf871-209">This download has the following items:</span></span>

- <span data-ttu-id="cf871-210">*ウィングヒント toys*フォルダー内のサンプルアプリケーション。</span><span class="sxs-lookup"><span data-stu-id="cf871-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="cf871-211">このサンプルアプリケーションを作成するために使用されるリソースは、*ウィング? toys*フォルダー内の*ウィングヒントの toys-Assets*フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="cf871-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="cf871-212">ダウンロードは *.zip*ファイルです。</span><span class="sxs-lookup"><span data-stu-id="cf871-212">The download is a *.zip* file.</span></span> <span data-ttu-id="cf871-213">このチュートリアルシリーズで作成した完成したプロジェクトを表示するに*C#* は、.zip ファイル内のフォルダーを見つけて選択します。</span><span class="sxs-lookup"><span data-stu-id="cf871-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="cf871-214">Visual Studio C#プロジェクトを操作するために使用するフォルダーにフォルダーを保存します。</span><span class="sxs-lookup"><span data-stu-id="cf871-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="cf871-215">既定では、Visual Studio 2017 projects フォルダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cf871-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="cf871-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;ユーザー名&gt;</em></strong></span><span class="sxs-lookup"><span data-stu-id="cf871-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="cf871-217">フォルダーの***C#*** 名前を「***ウィング? toys***」に変更します。</span><span class="sxs-lookup"><span data-stu-id="cf871-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="cf871-218">既にプロジェクトフォルダーにウィング? *toys*という名前のフォルダーがある場合は、フォルダーの*C#* 名前を「ウィング? *toys*」に変更する前に、既存のフォルダーの名前を一時的に変更します。</span><span class="sxs-lookup"><span data-stu-id="cf871-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="cf871-219">完成したプロジェクトを実行するには、*ウィングヒントの toys*フォルダーを開き、*ウィングヒントの toys. .sln*ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="cf871-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="cf871-220">Visual Studio 2017 によってプロジェクトが開きます。</span><span class="sxs-lookup"><span data-stu-id="cf871-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="cf871-221">次に、**ソリューションエクスプローラー**で*default.aspx*ファイルを右クリックし、 **[ブラウザーで表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="cf871-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="cf871-222">ASP.NET の Web フォームクイズでコンテンツを確認する</span><span class="sxs-lookup"><span data-stu-id="cf871-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="cf871-223">チュートリアルシリーズを完了したら、クイズを使用して知識をテストし、主要な概念を補強します。</span><span class="sxs-lookup"><span data-stu-id="cf871-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="cf871-224">各質問には、説明と追加のガイダンスへのリンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="cf871-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="cf871-225">ASP.NET Web フォームのクイズ</span><span class="sxs-lookup"><span data-stu-id="cf871-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="cf871-226">チュートリアルのサポートとコメント</span><span class="sxs-lookup"><span data-stu-id="cf871-226">Tutorial support and comments</span></span>

<span data-ttu-id="cf871-227">質問やコメントについては、 [ASP.NET 4.5 Web フォームおよび Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) サンプルページのはじめにに記載されている Q とセクションを使用します。</span><span class="sxs-lookup"><span data-stu-id="cf871-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="cf871-228">このチュートリアルシリーズのコメントは歓迎されます。</span><span class="sxs-lookup"><span data-stu-id="cf871-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="cf871-229">このチュートリアルシリーズを更新すると、修正や改善の提案についてすべての取り組みが行われます。</span><span class="sxs-lookup"><span data-stu-id="cf871-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="cf871-230">エラーが発生した場合は、対応するエラーメッセージが混乱する可能性があり、修正方法についての適切な説明はありません。</span><span class="sxs-lookup"><span data-stu-id="cf871-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="cf871-231">ヘルプを表示するには、 [ASP.NET フォーラム](https://forums.asp.net/)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="cf871-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="cf871-232">もう1つの優れたソースは、 [ASP.NET 4.5 Web フォームと Visual Studio 2013 Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) サンプルページのはじめにの Q と A セクションです。</span><span class="sxs-lookup"><span data-stu-id="cf871-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="cf871-233">Next</span><span class="sxs-lookup"><span data-stu-id="cf871-233">Next</span></span>](create-the-project.md)
