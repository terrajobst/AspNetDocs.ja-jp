---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: モデルの追加 (C#) |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457787"
---
# <a name="adding-a-model-c"></a><span data-ttu-id="b2617-104">モデルの追加 (C#)</span><span class="sxs-lookup"><span data-stu-id="b2617-104">Adding a Model (C#)</span></span>

<span data-ttu-id="b2617-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b2617-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="b2617-106">このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="b2617-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="b2617-107">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="b2617-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="b2617-108">これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b2617-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="b2617-109">または、次のリンクを使用して、前提条件を個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b2617-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="b2617-110">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="b2617-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="b2617-111">ASP.NET MVC 3 ツールの更新</span><span class="sxs-lookup"><span data-stu-id="b2617-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="b2617-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="b2617-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="b2617-113">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="b2617-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="b2617-114">このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="b2617-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="b2617-115">[バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="b2617-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="b2617-116">Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/adding-a-model.md)に切り替えてください。</span><span class="sxs-lookup"><span data-stu-id="b2617-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="b2617-117">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="b2617-117">Adding a Model</span></span>

<span data-ttu-id="b2617-118">このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="b2617-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="b2617-119">これらのクラスは、ASP.NET MVC アプリケーションの "モデル" 部分になります。</span><span class="sxs-lookup"><span data-stu-id="b2617-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="b2617-120">Entity Framework と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。</span><span class="sxs-lookup"><span data-stu-id="b2617-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="b2617-121">Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b2617-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="b2617-122">Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b2617-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="b2617-123">(これらは、"plain old CLR objects" の POCO クラスとも呼ばれます)。その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="b2617-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="b2617-124">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="b2617-124">Adding Model Classes</span></span>

<span data-ttu-id="b2617-125">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="b2617-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="b2617-126">*クラス*に "Movie" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2617-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="b2617-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="b2617-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="b2617-128">次の5つのプロパティを `Movie` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b2617-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="b2617-129">`Movie` クラスを使用して、データベース内の映画を表します。</span><span class="sxs-lookup"><span data-stu-id="b2617-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="b2617-130">`Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="b2617-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="b2617-131">同じファイルで、次の `MovieDBContext` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2617-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="b2617-132">`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。</span><span class="sxs-lookup"><span data-stu-id="b2617-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="b2617-133">`MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="b2617-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="b2617-134">`DbContext` と `DbSet`の詳細については、「 [Entity Framework の生産性の向上](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2617-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="b2617-135">`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `using` ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2617-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="b2617-136">完全な*Movie.cs*ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b2617-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="b2617-137">接続文字列の作成と SQL Server Compact の操作</span><span class="sxs-lookup"><span data-stu-id="b2617-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="b2617-138">作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。</span><span class="sxs-lookup"><span data-stu-id="b2617-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="b2617-139">ただし、接続先のデータベースを指定する方法について質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="b2617-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="b2617-140">これを行うに*は、アプリケーションの web.config ファイルに*接続情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="b2617-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="b2617-141">アプリケーション*ルートの web.config ファイル*を開きます。</span><span class="sxs-lookup"><span data-stu-id="b2617-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="b2617-142">( *Views*フォルダー*内の web.config ファイルで*はありません)。次の図は、両方の web.config ファイルを示して*い*ます。赤で囲まれた web.config ファイルを*開きます。*</span><span class="sxs-lookup"><span data-stu-id="b2617-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

<span data-ttu-id="b2617-143">次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*</span><span class="sxs-lookup"><span data-stu-id="b2617-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="b2617-144">次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="b2617-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="b2617-145">この少量のコードと XML は、ムービーデータを表現してデータベースに格納するために記述する必要があるすべてのものです。</span><span class="sxs-lookup"><span data-stu-id="b2617-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="b2617-146">次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="b2617-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b2617-147">[前へ](adding-a-view.md)
> [次へ](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="b2617-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
