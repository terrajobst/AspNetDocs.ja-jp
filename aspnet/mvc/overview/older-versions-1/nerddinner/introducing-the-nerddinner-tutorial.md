---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: このチュートリアルの概要 |Microsoft Docs
author: shanselman
description: 新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。 このチュートリアルでは、ASP.NE を使用して小規模で、完成したアプリケーションを作成する方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468934"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="9193a-104">NerdDinner チュートリアルの紹介</span><span class="sxs-lookup"><span data-stu-id="9193a-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="9193a-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="9193a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

<span data-ttu-id="9193a-106">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="9193a-106">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="9193a-107">新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。</span><span class="sxs-lookup"><span data-stu-id="9193a-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="9193a-108">このチュートリアルでは、ASP.NET MVC 1 を使用して小規模で、完成したアプリケーションを作成する方法について説明し、その背後にある主要な概念をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="9193a-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="9193a-109">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9193a-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="9193a-110">のチュートリアル</span><span class="sxs-lookup"><span data-stu-id="9193a-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="9193a-111">新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。</span><span class="sxs-lookup"><span data-stu-id="9193a-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="9193a-112">このチュートリアルでは、ASP.NET MVC を使用して小規模で、完成したアプリケーションを構築する方法について説明し、その背後にある主要な概念をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="9193a-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="9193a-113">ビルドしようとしているアプリケーションは、"実行中" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="9193a-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="9193a-114">ディナー online を簡単に検索して整理するには、次のような簡単な方法があります。</span><span class="sxs-lookup"><span data-stu-id="9193a-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="9193a-115">ユーザーは、ディナーを作成、編集、削除することができます。</span><span class="sxs-lookup"><span data-stu-id="9193a-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="9193a-116">アプリケーション全体で一貫性のある検証とビジネスルールのセットを適用します。</span><span class="sxs-lookup"><span data-stu-id="9193a-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="9193a-117">訪問者は、AJAX ベースのマップを使用して、近い将来に保持されているディナーを検索できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="9193a-118">ディナーをクリックすると、詳細ページが表示され、詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="9193a-119">夕食に参加したい場合は、次のようにして、サイトにログインまたは登録できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="9193a-120">次に、AJAX ベースの RSVP リンクをクリックして、イベントに参加できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="9193a-121">ディナー Dディナーの実装</span><span class="sxs-lookup"><span data-stu-id="9193a-121">Implementing NerdDinner</span></span>

<span data-ttu-id="9193a-122">ここでは、Visual Studio 内でファイル&gt;[新しいプロジェクト] コマンドを使用して新しい ASP.NET MVC プロジェクトを作成することにより、このアプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="9193a-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="9193a-123">次に、機能と機能を段階的に追加します。</span><span class="sxs-lookup"><span data-stu-id="9193a-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="9193a-124">ここでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9193a-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="9193a-125">新しい ASP.NET MVC プロジェクトを作成する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="9193a-126">データベースを作成する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="9193a-127">ビジネスルール検証を使用してモデルを構築する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="9193a-128">リスト/詳細 UI を実装するためにコントローラーとビューを使用する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="9193a-129">CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="9193a-130">ViewData を使用して、ビューモデルクラスを実装する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="9193a-131">マスターページとパーシャルを使用して UI を再利用する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="9193a-132">効率的なデータページングを実装する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="9193a-133">認証と承認を使用してアプリケーションをセキュリティで保護する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="9193a-134">AJAX を使用して動的更新を配信する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="9193a-135">AJAX を使用してマッピングシナリオを実装する方法</span><span class="sxs-lookup"><span data-stu-id="9193a-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="9193a-136">自動単体テストを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="9193a-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="9193a-137">この章のチュートリアルの各手順を実行することで、最初から自分で作成した自分のコピーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="9193a-138">または、ソースコードの完全なバージョンを、 [GitHub の「で](https://github.com/AspNetMVPSamples/NerdDinner)は、こちらからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="9193a-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="9193a-139">このチュートリアルをオフラインで読む場合は、必要に応じて、[このチュートリアルの無料 PDF バージョンをダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)することもできます。</span><span class="sxs-lookup"><span data-stu-id="9193a-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="9193a-140">Visual Studio 2008 または無料の Visual Web Developer 2008 Express を使用して、アプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="9193a-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="9193a-141">SQL Server またはデータベースの空き SQL Server Express を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9193a-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="9193a-142">の V2 を使用して、ASP.NET MVC、Visual Web Developer 2008 Express、SQL Server Express (すべて無料) をインストールでき[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="9193a-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="9193a-143">では、始めましょう。</span><span class="sxs-lookup"><span data-stu-id="9193a-143">Now let's get started....</span></span>

<span data-ttu-id="9193a-144">これで、次は、引き締めをロールアップしてコードを記述しました。</span><span class="sxs-lookup"><span data-stu-id="9193a-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="9193a-145">まず、Visual Studio 内でファイル&gt;新しいプロジェクトを使用して、このアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="9193a-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9193a-146">Next</span><span class="sxs-lookup"><span data-stu-id="9193a-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
