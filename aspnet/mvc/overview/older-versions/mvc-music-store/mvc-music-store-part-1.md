---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 'パート 1: 概要とファイル > 新しいプロジェクト |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル > 新しいプロジェクトについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451282"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="3eef5-104">パート 1: 概要とファイル > 新しいプロジェクト</span><span class="sxs-lookup"><span data-stu-id="3eef5-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="3eef5-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="3eef5-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3eef5-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="3eef5-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="3eef5-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="3eef5-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="3eef5-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="3eef5-109">パート1では、概要とファイル&gt;新しいプロジェクトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="3eef5-110">概要</span><span class="sxs-lookup"><span data-stu-id="3eef5-110">Overview</span></span>

<span data-ttu-id="3eef5-111">MVC Music Store は、ASP.NET MVC と Visual Web Developer を使用して Web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="3eef5-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="3eef5-112">開始に時間がかかります。初心者レベルの web 開発エクスペリエンスは問題ありません。</span><span class="sxs-lookup"><span data-stu-id="3eef5-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="3eef5-113">ビルドするアプリケーションは、単純なミュージックストアです。</span><span class="sxs-lookup"><span data-stu-id="3eef5-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="3eef5-114">アプリケーションには、買い物、チェックアウト、管理という3つの主要な部分があります。</span><span class="sxs-lookup"><span data-stu-id="3eef5-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="3eef5-115">閲覧者はジャンルでアルバムを参照できます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="3eef5-116">1つのアルバムを表示し、カートに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="3eef5-117">カートをレビューして、不要になったアイテムを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="3eef5-118">チェックアウトに進むと、ユーザーアカウントにログインまたは登録するように求められます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="3eef5-119">アカウントを作成した後は、出荷と支払いに関する情報を入力して注文を完了できます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="3eef5-120">簡潔にするために、すばらしいプロモーションを実行しています。プロモーションコードを "無料" で入力すると、すべて無料で利用できます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="3eef5-121">順序を付けると、簡単な確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="3eef5-122">顧客向けのページだけでなく、管理者がアルバムの作成、編集、削除を行うことができるアルバムの一覧を示す管理者セクションも作成します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="3eef5-123">1. ファイル&gt; 新しいプロジェクト</span><span class="sxs-lookup"><span data-stu-id="3eef5-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="3eef5-124">ソフトウェアのインストール</span><span class="sxs-lookup"><span data-stu-id="3eef5-124">Installing the software</span></span>

<span data-ttu-id="3eef5-125">このチュートリアルを開始するには、無料の Visual Web Developer 2010 Express (無料) を使用して新しい ASP.NET MVC 3 プロジェクトを作成し、機能を段階的に追加して、完全に機能するアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="3eef5-126">この過程で、データベースへのアクセス、フォームのポストのシナリオ、データの検証、一貫性のあるページレイアウトのためのマスターページの使用、ページの更新と検証に AJAX を使用する、ユーザーログインなどについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="3eef5-127">ステップバイステップで進めることができます。または、完成したアプリケーションを[MVC-Music-ストア](https://github.com/evilDave/MVC-Music-Store)からダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="3eef5-128">Visual Studio 2010 SP1 または Visual Web Developer 2010 Express SP1 (Visual Studio 2010 の無料版) のいずれかを使用して、アプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="3eef5-129">データベースをホストするために SQL Server Compact (または無料) を使用します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="3eef5-130">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3eef5-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="3eef5-131">[Visual Studio Web Developer Express SP1 の前提条件]</span><span class="sxs-lookup"><span data-stu-id="3eef5-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="3eef5-132">[ASP.NET MVC 3 Tools Update]</span><span class="sxs-lookup"><span data-stu-id="3eef5-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="3eef5-133">[SQL Server Compact 4.0]-ランタイムとツールの両方のサポートを含む</span><span class="sxs-lookup"><span data-stu-id="3eef5-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="3eef5-134">新しい ASP.NET MVC 3 プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3eef5-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="3eef5-135">まず、Visual Web Developer の [ファイル] メニューから [新しいプロジェクト] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="3eef5-136">[新しいプロジェクト] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="3eef5-137">左側の [Visual C#&gt; web テンプレート] グループを選択し、中央の列で "ASP.NET MVC 3 web アプリケーション" テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="3eef5-138">プロジェクトに MvcMusicStore という名前を指定し、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3eef5-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="3eef5-139">これにより、プロジェクトの MVC 固有の設定を行うためのセカンダリダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="3eef5-140">次のように選択します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-140">Select the following:</span></span>

<span data-ttu-id="3eef5-141">プロジェクトテンプレート-[空を選択]</span><span class="sxs-lookup"><span data-stu-id="3eef5-141">Project Template - select Empty</span></span>

<span data-ttu-id="3eef5-142">ビューエンジン-Razor の選択</span><span class="sxs-lookup"><span data-stu-id="3eef5-142">View Engine - select Razor</span></span>

<span data-ttu-id="3eef5-143">HTML5 セマンティックマークアップの使用-チェック済み</span><span class="sxs-lookup"><span data-stu-id="3eef5-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="3eef5-144">設定が次のようになっていることを確認し、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3eef5-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="3eef5-145">これにより、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-145">This will create our project.</span></span> <span data-ttu-id="3eef5-146">ここでは、アプリケーションに追加されたフォルダーを右側のソリューションエクスプローラーに見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="3eef5-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="3eef5-147">空の MVC 3 テンプレートは完全に空ではないため、基本的なフォルダー構造が追加されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="3eef5-148">ASP.NET MVC では、フォルダー名に対していくつかの基本的な名前付け規則を使用します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="3eef5-149">**フォルダー**</span><span class="sxs-lookup"><span data-stu-id="3eef5-149">**Folder**</span></span> | <span data-ttu-id="3eef5-150">**目的**</span><span class="sxs-lookup"><span data-stu-id="3eef5-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="3eef5-151">**/コントローラー**</span><span class="sxs-lookup"><span data-stu-id="3eef5-151">**/Controllers**</span></span> | <span data-ttu-id="3eef5-152">コントローラーは、ブラウザーからの入力に応答し、その処理を決定し、ユーザーに応答を返します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="3eef5-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="3eef5-153">**/Views**</span></span> | <span data-ttu-id="3eef5-154">ビューは UI テンプレートを保持します</span><span class="sxs-lookup"><span data-stu-id="3eef5-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="3eef5-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="3eef5-155">**/Models**</span></span> | <span data-ttu-id="3eef5-156">データの保持と操作を行うモデル</span><span class="sxs-lookup"><span data-stu-id="3eef5-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="3eef5-157">**/コンテンツ**</span><span class="sxs-lookup"><span data-stu-id="3eef5-157">**/Content**</span></span> | <span data-ttu-id="3eef5-158">このフォルダーには、イメージ、CSS、およびその他の静的コンテンツが保持されます。</span><span class="sxs-lookup"><span data-stu-id="3eef5-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="3eef5-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="3eef5-159">**/Scripts**</span></span> | <span data-ttu-id="3eef5-160">このフォルダーには、JavaScript ファイルが保持します</span><span class="sxs-lookup"><span data-stu-id="3eef5-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="3eef5-161">これらのフォルダーは、空の ASP.NET MVC アプリケーションにも含まれています。 ASP.NET MVC フレームワークでは、既定では "構成に基づく規約" アプローチが使用され、フォルダーの名前付け規則に基づいて既定の仮定がいくつか行われているためです。</span><span class="sxs-lookup"><span data-stu-id="3eef5-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="3eef5-162">たとえば、コントローラーは既定で Views フォルダー内のビューを検索しますが、コードで明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3eef5-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="3eef5-163">既定の規則に従うと、記述する必要のあるコードの量が減り、他の開発者がプロジェクトを理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="3eef5-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="3eef5-164">これらの規則については、アプリケーションを作成するときに説明します。</span><span class="sxs-lookup"><span data-stu-id="3eef5-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3eef5-165">Next</span><span class="sxs-lookup"><span data-stu-id="3eef5-165">Next</span></span>](mvc-music-store-part-2.md)
