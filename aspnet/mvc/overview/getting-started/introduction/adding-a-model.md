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
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499084"
---
# <a name="adding-a-model"></a><span data-ttu-id="4f575-102">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="4f575-102">Adding a Model</span></span>

<span data-ttu-id="4f575-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4f575-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="4f575-104">このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="4f575-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="4f575-105">これらのクラスは、ASP.NET MVC アプリの一部&quot; &quot;モデルになります。</span><span class="sxs-lookup"><span data-stu-id="4f575-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="4f575-106">[Entity Framework](https://docs.microsoft.com/ef/)と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。</span><span class="sxs-lookup"><span data-stu-id="4f575-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="4f575-107">Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="4f575-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="4f575-108">Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4f575-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="4f575-109">(これらは、&quot;の古い CLR オブジェクトからの POCO クラスとも呼ばれます。&quot;)その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="4f575-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="4f575-110">データベースを最初に作成する必要がある場合でも、このチュートリアルに従って MVC と EF アプリの開発について学習することができます。</span><span class="sxs-lookup"><span data-stu-id="4f575-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="4f575-111">その後、Tom Fizmakens [ASP.NET スキャフォールディング](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)チュートリアルに従うことができます。このチュートリアルでは、データベースの最初のアプローチについて説明します。</span><span class="sxs-lookup"><span data-stu-id="4f575-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="4f575-112">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="4f575-112">Adding Model Classes</span></span>

<span data-ttu-id="4f575-113">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="4f575-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="4f575-114">&quot;Movie&quot;*クラス*名を入力します。</span><span class="sxs-lookup"><span data-stu-id="4f575-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="4f575-115">次の5つのプロパティを `Movie` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="4f575-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="4f575-116">`Movie` クラスを使用して、データベース内の映画を表します。</span><span class="sxs-lookup"><span data-stu-id="4f575-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="4f575-117">`Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="4f575-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="4f575-118">注: system.object と関連クラスを使用するには、 [Entity Framework NuGet パッケージ](https://www.nuget.org/packages/EntityFramework/)をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f575-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="4f575-119">詳細な手順については、リンク先を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4f575-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="4f575-120">同じファイルで、次の `MovieDBContext` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4f575-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="4f575-121">`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。</span><span class="sxs-lookup"><span data-stu-id="4f575-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="4f575-122">`MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="4f575-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="4f575-123">`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `using` ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f575-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="4f575-124">これを行うには、using ステートメントを手動で追加するか、赤色の波線の上にマウスポインターを移動し、`Show potential fixes` をクリックして `using System.Data.Entity;` をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4f575-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="4f575-125">注: いくつかの未使用の `using` ステートメントが削除されました。</span><span class="sxs-lookup"><span data-stu-id="4f575-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="4f575-126">Visual Studio では、未使用の依存関係が灰色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="4f575-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="4f575-127">灰色の依存関係をポイントし、[`Show potential fixes`] をクリックし、 **[未使用の using の削除]** をクリックすることで、未使用の依存関係を削除できます。</span><span class="sxs-lookup"><span data-stu-id="4f575-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="4f575-128">最後にモデル (MVC では M) を追加しました。</span><span class="sxs-lookup"><span data-stu-id="4f575-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="4f575-129">次のセクションでは、データベース接続文字列を操作します。</span><span class="sxs-lookup"><span data-stu-id="4f575-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4f575-130">[前へ](adding-a-view.md)
> [次へ](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="4f575-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
