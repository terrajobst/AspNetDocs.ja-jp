---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: モデルの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0221539f5e468faacf3e38374452c0cc2a7d31d3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59398749"
---
# <a name="adding-a-model"></a><span data-ttu-id="d856a-102">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="d856a-102">Adding a Model</span></span>

<span data-ttu-id="d856a-103">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="d856a-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="d856a-104">このセクションでは、データベースのムービーを管理するためのいくつかのクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="d856a-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="d856a-105">これらのクラスがありますが、&quot;モデル&quot;ASP.NET MVC アプリの一部です。</span><span class="sxs-lookup"><span data-stu-id="d856a-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="d856a-106">呼ばれる .NET Framework データ アクセス テクノロジを使用します、 [Entity Framework](https://docs.microsoft.com/ef/)を定義し、これらのモデル クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="d856a-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="d856a-107">開発パラダイムと呼ばれる、(EF とも呼ばれます)、Entity Framework がサポート*Code First*します。</span><span class="sxs-lookup"><span data-stu-id="d856a-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="d856a-108">まず、コードを使用すると、単純なクラスを記述することで、モデル オブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d856a-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="d856a-109">(これらとも呼ばれる、POCO クラスから&quot;plain-old CLR object&quot;)。データベースが非常にクリーンで迅速な開発ワークフローを有効にするクラスからその場で作成することができます。</span><span class="sxs-lookup"><span data-stu-id="d856a-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="d856a-110">まずデータベースを作成するために必要な場合は、MVC と EF のアプリ開発の詳細については、このチュートリアルを引き続きに従ってできます。</span><span class="sxs-lookup"><span data-stu-id="d856a-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="d856a-111">その後 Tom Fizmakens [ASP.NET スキャフォールディング](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)チュートリアルでは、データベースの最初のアプローチを対象とします。</span><span class="sxs-lookup"><span data-stu-id="d856a-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="d856a-112">モデル クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="d856a-112">Adding Model Classes</span></span>

<span data-ttu-id="d856a-113">**ソリューション エクスプ ローラー**を右クリックして、*モデル*フォルダーで、**追加**、し、**クラス**します。</span><span class="sxs-lookup"><span data-stu-id="d856a-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="d856a-114">入力、*クラス*名前&quot;ムービー&quot;します。</span><span class="sxs-lookup"><span data-stu-id="d856a-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="d856a-115">次の 5 つのプロパティを追加、`Movie`クラス。</span><span class="sxs-lookup"><span data-stu-id="d856a-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="d856a-116">使用して、`Movie`をデータベースのムービーを表すクラス。</span><span class="sxs-lookup"><span data-stu-id="d856a-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="d856a-117">各インスタンスを`Movie`オブジェクトは、データベース テーブルとの各プロパティ内の行に対応している、`Movie`クラスは、テーブル内の列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="d856a-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="d856a-118">メモ:System.Data.Entity、および関連するクラスを使用するのには、インストールする必要があります、 [Entity Framework NuGet パッケージ](https://www.nuget.org/packages/EntityFramework/)します。</span><span class="sxs-lookup"><span data-stu-id="d856a-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="d856a-119">詳細については、リンクに従います。</span><span class="sxs-lookup"><span data-stu-id="d856a-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="d856a-120">同じファイルで次の追加`MovieDBContext`クラス。</span><span class="sxs-lookup"><span data-stu-id="d856a-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="d856a-121">`MovieDBContext`クラスは、フェッチ、格納、および更新を処理する Entity Framework ムービー データベース コンテキストを表します。`Movie`クラス、データベース内のインスタンス。</span><span class="sxs-lookup"><span data-stu-id="d856a-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="d856a-122">`MovieDBContext`から派生した、`DbContext`基本クラスを Entity Framework によって提供されます。</span><span class="sxs-lookup"><span data-stu-id="d856a-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="d856a-123">参照できるようにするためには`DbContext`と`DbSet`、以下を追加する必要がある`using`ファイルの上部にあるステートメント。</span><span class="sxs-lookup"><span data-stu-id="d856a-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="d856a-124">使用して、手動で追加することでこれを行うステートメント、またはすることができます合わせると赤色の波線をクリックします`Show potential fixes` をクリック</span><span class="sxs-lookup"><span data-stu-id="d856a-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click</span></span> `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

<span data-ttu-id="d856a-125">メモ:いくつか使用されていない`using`ステートメントが削除されました。</span><span class="sxs-lookup"><span data-stu-id="d856a-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="d856a-126">Visual Studio は、未使用の依存関係を灰色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="d856a-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="d856a-127">ポインターを合わせると灰色の依存関係で使用されていない依存関係を削除するか、をクリックして`Show potential fixes`クリック**未使用の Using の削除します。**</span><span class="sxs-lookup"><span data-stu-id="d856a-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="d856a-128">最後にモデル (MVC で M) が追加されました。</span><span class="sxs-lookup"><span data-stu-id="d856a-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="d856a-129">次のセクションでは、データベース接続文字列を使用します。</span><span class="sxs-lookup"><span data-stu-id="d856a-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d856a-130">[前へ](adding-a-view.md)
> [次へ](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="d856a-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
