---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: モデルの追加 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434416"
---
# <a name="adding-a-model"></a><span data-ttu-id="55021-104">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="55021-104">Adding a Model</span></span>

<span data-ttu-id="55021-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="55021-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="55021-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="55021-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="55021-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="55021-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="55021-108">このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="55021-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="55021-109">これらのクラスは、ASP.NET MVC アプリケーションの一部&quot; &quot;モデルになります。</span><span class="sxs-lookup"><span data-stu-id="55021-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="55021-110">[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。</span><span class="sxs-lookup"><span data-stu-id="55021-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="55021-111">Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="55021-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="55021-112">Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="55021-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="55021-113">(これらは、&quot;の古い CLR オブジェクトからの POCO クラスとも呼ばれます。&quot;)その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="55021-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="55021-114">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="55021-114">Adding Model Classes</span></span>

<span data-ttu-id="55021-115">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="55021-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="55021-116">&quot;Movie&quot;*クラス*名を入力します。</span><span class="sxs-lookup"><span data-stu-id="55021-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="55021-117">次の5つのプロパティを `Movie` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="55021-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="55021-118">`Movie` クラスを使用して、データベース内の映画を表します。</span><span class="sxs-lookup"><span data-stu-id="55021-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="55021-119">`Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="55021-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="55021-120">同じファイルで、次の `MovieDBContext` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="55021-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="55021-121">`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。</span><span class="sxs-lookup"><span data-stu-id="55021-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="55021-122">`MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="55021-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="55021-123">`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `using` ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="55021-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="55021-124">完全な*Movie.cs*ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="55021-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="55021-125">(不要な using ステートメントがいくつか削除されました)。</span><span class="sxs-lookup"><span data-stu-id="55021-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="55021-126">接続文字列の作成と SQL Server LocalDB の使用</span><span class="sxs-lookup"><span data-stu-id="55021-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="55021-127">作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。</span><span class="sxs-lookup"><span data-stu-id="55021-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="55021-128">ただし、接続先のデータベースを指定する方法について質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="55021-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="55021-129">これを行うに*は、アプリケーションの web.config ファイルに*接続情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="55021-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="55021-130">アプリケーション*ルートの web.config ファイル*を開きます。</span><span class="sxs-lookup"><span data-stu-id="55021-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="55021-131">( *Views*フォルダー*内の web.config ファイルで*はありません)。赤で囲まれた web.config ファイルを*開きます。*</span><span class="sxs-lookup"><span data-stu-id="55021-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="55021-132">次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*</span><span class="sxs-lookup"><span data-stu-id="55021-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="55021-133">次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="55021-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="55021-134">この少量のコードと XML は、ムービーデータを表現してデータベースに格納するために記述する必要があるすべてのものです。</span><span class="sxs-lookup"><span data-stu-id="55021-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="55021-135">次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="55021-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="55021-136">[前へ](adding-a-view.md)
> [次へ](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="55021-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
