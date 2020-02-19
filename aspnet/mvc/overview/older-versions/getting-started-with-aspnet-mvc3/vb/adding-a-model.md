---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: モデルの追加 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457246"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="a8a7c-103">モデルの追加 (VB)</span><span class="sxs-lookup"><span data-stu-id="a8a7c-103">Adding a Model (VB)</span></span>

<span data-ttu-id="a8a7c-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a8a7c-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="a8a7c-105">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="a8a7c-106">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="a8a7c-107">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="a8a7c-108">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="a8a7c-109">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="a8a7c-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="a8a7c-110">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="a8a7c-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="a8a7c-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="a8a7c-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="a8a7c-112">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="a8a7c-113">このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="a8a7c-114">[VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="a8a7c-115">必要に応じC#て[ C# ](../cs/adding-a-model.md) 、このチュートリアルのバージョンに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="a8a7c-116">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="a8a7c-116">Adding a Model</span></span>

<span data-ttu-id="a8a7c-117">このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="a8a7c-118">これらのクラスは、ASP.NET MVC アプリケーションの "モデル" 部分になります。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="a8a7c-119">Entity Framework と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="a8a7c-120">Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="a8a7c-121">Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="a8a7c-122">(これらは、"plain old CLR objects" の POCO クラスとも呼ばれます)。その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="a8a7c-123">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="a8a7c-123">Adding Model Classes</span></span>

<span data-ttu-id="a8a7c-124">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="a8a7c-125">クラスに "Movie" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-125">Name the class "Movie".</span></span>

<span data-ttu-id="a8a7c-126">次の5つのプロパティを `Movie` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="a8a7c-127">`Movie` クラスを使用して、データベース内の映画を表します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="a8a7c-128">`Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="a8a7c-129">同じファイルで、次の `MovieDBContext` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="a8a7c-130">`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="a8a7c-131">`MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="a8a7c-132">`DbContext` と `DbSet`の詳細については、「 [Entity Framework の生産性の向上](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="a8a7c-133">`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `imports` ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="a8a7c-134">完成した*ムービー .vb*ファイルを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="a8a7c-135">接続文字列の作成と SQL Server Compact の操作</span><span class="sxs-lookup"><span data-stu-id="a8a7c-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="a8a7c-136">作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="a8a7c-137">ただし、接続先のデータベースを指定する方法について質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="a8a7c-138">これを行うに*は、アプリケーションの web.config ファイルに*接続情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="a8a7c-139">アプリケーション*ルートの web.config ファイル*を開きます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="a8a7c-140">( *Views*フォルダー*内の web.config ファイルで*はありません)。次の図は、両方の web.config ファイルを示して*い*ます。赤で囲まれた web.config ファイルを*開きます。*</span><span class="sxs-lookup"><span data-stu-id="a8a7c-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="a8a7c-141">次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*</span><span class="sxs-lookup"><span data-stu-id="a8a7c-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="a8a7c-142">次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="a8a7c-143">この少量のコードと XML は、ムービーデータを表現してデータベースに格納するために記述する必要があるすべてのものです。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="a8a7c-144">次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a8a7c-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8a7c-145">[前へ](adding-a-view.md)
> [次へ](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="a8a7c-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
