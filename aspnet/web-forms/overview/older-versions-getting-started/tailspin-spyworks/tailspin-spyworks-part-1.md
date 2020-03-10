---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 'パート 1: ファイル > 新しいプロジェクト |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル/新しいプロジェクトについて説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516538"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="53b72-104">パート 1: ファイル > 新しいプロジェクト</span><span class="sxs-lookup"><span data-stu-id="53b72-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="53b72-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="53b72-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="53b72-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="53b72-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="53b72-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="53b72-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="53b72-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="53b72-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="53b72-109">パート1では、概要とファイル/新しいプロジェクトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="53b72-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="53b72-110">概要</span><span class="sxs-lookup"><span data-stu-id="53b72-110">Overview</span></span>

<span data-ttu-id="53b72-111">このチュートリアルでは、ASP.NET WebForms の概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="53b72-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="53b72-112">開始に時間がかかります。初心者レベルの web 開発エクスペリエンスは問題ありません。</span><span class="sxs-lookup"><span data-stu-id="53b72-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="53b72-113">構築するアプリケーションは、単純なオンラインストアです。</span><span class="sxs-lookup"><span data-stu-id="53b72-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="53b72-114">訪問者はカテゴリで製品を参照できます。</span><span class="sxs-lookup"><span data-stu-id="53b72-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="53b72-115">1つの製品を表示し、カートに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="53b72-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="53b72-116">カートをレビューして、不要になったアイテムを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="53b72-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="53b72-117">チェックアウトに進むと、</span><span class="sxs-lookup"><span data-stu-id="53b72-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="53b72-118">順序を付けると、簡単な確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="53b72-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="53b72-119">まず、Visual Studio 2010 で新しい ASP.NET WebForms プロジェクトを作成します。次に、機能を段階的に追加して、完全に機能するアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="53b72-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="53b72-120">その過程で、データベースアクセス、リストとグリッドビュー、データ更新ページ、データの検証、ページレイアウトの一貫性のためのマスターページの使用、AJAX、検証、ユーザーメンバーシップなどについて説明します。</span><span class="sxs-lookup"><span data-stu-id="53b72-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="53b72-121">ステップバイステップで進めることができます。または、完成したアプリケーションをからダウンロードすることもでき[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="53b72-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="53b72-122">[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)から visual Studio 2010 または無料の Visual Web Developer 2010 を使用できます。</span><span class="sxs-lookup"><span data-stu-id="53b72-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="53b72-123">アプリケーションをビルドするには、SQL Server または無料の SQL Server Express を使用してデータベースをホストできます。</span><span class="sxs-lookup"><span data-stu-id="53b72-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="53b72-124">ファイル/新しいプロジェクト</span><span class="sxs-lookup"><span data-stu-id="53b72-124">File / New Project</span></span>

<span data-ttu-id="53b72-125">まず、Visual Studio の [ファイル] メニューから新しいプロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="53b72-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="53b72-126">[新しいプロジェクト] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="53b72-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="53b72-127">左側の [ビジュアルC# /Web テンプレート] グループを選択し、中央の列で [ASP.NET Web Application] テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="53b72-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="53b72-128">プロジェクトに TailspinSpyworks という名前を指定し、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="53b72-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="53b72-129">これにより、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="53b72-129">This will create our project.</span></span> <span data-ttu-id="53b72-130">アプリケーションに含まれているフォルダーを右側のソリューションエクスプローラーに見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="53b72-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="53b72-131">空のソリューションは完全に空ではないため、基本的なフォルダー構造が追加されます。</span><span class="sxs-lookup"><span data-stu-id="53b72-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="53b72-132">ASP.NET 4 の既定のプロジェクトテンプレートによって実装される規則に注意してください。</span><span class="sxs-lookup"><span data-stu-id="53b72-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="53b72-133">"Account" フォルダーには、ASP 用の基本的なユーザーインターフェイスが実装されています。NET のメンバーシップサブシステム。</span><span class="sxs-lookup"><span data-stu-id="53b72-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="53b72-134">"Scripts" フォルダーは、クライアント側の JavaScript ファイルのリポジトリとして機能し、主要な jQuery .js ファイルは既定で使用可能になります。</span><span class="sxs-lookup"><span data-stu-id="53b72-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="53b72-135">"Styles" フォルダーは、web サイトのビジュアルを整理するために使用されます (CSS スタイルシート)</span><span class="sxs-lookup"><span data-stu-id="53b72-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="53b72-136">F5 キーを押してアプリケーションを実行し、default.aspx ページを表示すると、次のような画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="53b72-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="53b72-137">最初のアプリケーション拡張機能では、既定の WebForms テンプレートの .css ファイルを、CSS クラスと、Tailspin Spyworks アプリケーションに必要な visual asthetics をレンダリングする関連イメージファイルに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="53b72-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="53b72-138">その後、default.aspx ページは次のようにレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="53b72-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="53b72-139">ページの右上の画像リンクと、マスターページに追加されたメニュー項目に注目してください。</span><span class="sxs-lookup"><span data-stu-id="53b72-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="53b72-140">"サインイン" リンクと "アカウント" リンクのみが、(既定のテンプレートによって生成される) 存在するページと、アプリケーションをビルドするときに実装する残りのページをポイントします。</span><span class="sxs-lookup"><span data-stu-id="53b72-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="53b72-141">また、マスターページを Styles ディレクトリに再配置します。</span><span class="sxs-lookup"><span data-stu-id="53b72-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="53b72-142">これは単なる優先事項ですが、将来アプリケーションを "skinable" にする場合は、少し簡単にすることができます。</span><span class="sxs-lookup"><span data-stu-id="53b72-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="53b72-143">この操作を行った後、既定の ASP.NET WebForms ページによって生成されるすべての .aspx ファイルのマスターページ参照を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53b72-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="53b72-144">Next</span><span class="sxs-lookup"><span data-stu-id="53b72-144">Next</span></span>](tailspin-spyworks-part-2.md)
