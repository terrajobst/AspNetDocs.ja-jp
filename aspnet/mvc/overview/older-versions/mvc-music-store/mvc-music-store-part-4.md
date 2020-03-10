---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 'パート 4: モデルとデータアクセス |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート4では、モデルとデータアクセスについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451018"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="f6e61-104">パート 4: モデルとデータアクセス</span><span class="sxs-lookup"><span data-stu-id="f6e61-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="f6e61-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="f6e61-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f6e61-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="f6e61-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="f6e61-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="f6e61-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="f6e61-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="f6e61-109">パート4では、モデルとデータアクセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="f6e61-110">ここまでは、コントローラーからビューテンプレートに "ダミーデータ" を渡しています。</span><span class="sxs-lookup"><span data-stu-id="f6e61-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="f6e61-111">これで、実際のデータベースをフックする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="f6e61-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="f6e61-112">このチュートリアルでは、データベースエンジンとして SQL Server Compact エディション (多くの場合、SQL CE) を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="f6e61-113">SQL CE は、インストールや構成を必要としない、組み込まれた、ファイルベースの無料のデータベースです。これにより、ローカルでの開発に非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="f6e61-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="f6e61-114">Entity Framework コードを使用したデータベースアクセス</span><span class="sxs-lookup"><span data-stu-id="f6e61-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="f6e61-115">ASP.NET MVC 3 プロジェクトに含まれている Entity Framework (EF) のサポートを使用して、データベースのクエリと更新を行います。</span><span class="sxs-lookup"><span data-stu-id="f6e61-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="f6e61-116">EF は、オブジェクト指向の方法でデータベースに格納されているデータのクエリと更新を開発者が行うことができる柔軟なオブジェクトリレーショナルマッピング (ORM) データ API です。</span><span class="sxs-lookup"><span data-stu-id="f6e61-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="f6e61-117">Entity Framework version 4 では、code first と呼ばれる開発パラダイムがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f6e61-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="f6e61-118">Code first では、単純なクラス ("plain old" CLR オブジェクトからの POCO とも呼ばれます) を記述することによってモデルオブジェクトを作成できます。また、クラスからすぐにデータベースを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="f6e61-119">モデルクラスの変更点</span><span class="sxs-lookup"><span data-stu-id="f6e61-119">Changes to our Model Classes</span></span>

<span data-ttu-id="f6e61-120">このチュートリアルでは Entity Framework のデータベース作成機能を利用します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="f6e61-121">これを行う前に、モデルクラスにいくつかの軽微な変更を加えて、後で使用するいくつかの点を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f6e61-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="f6e61-122">アーティストモデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="f6e61-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="f6e61-123">アルバムはアーティストに関連付けられるので、アーティストを説明する単純なモデルクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="f6e61-124">次に示すコードを使用して、Artist.cs という名前のモデルフォルダーに新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="f6e61-125">モデルクラスを更新しています</span><span class="sxs-lookup"><span data-stu-id="f6e61-125">Updating our Model Classes</span></span>

<span data-ttu-id="f6e61-126">次に示すようにアルバムクラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="f6e61-127">次に、Genre クラスに対して次の更新を行います。</span><span class="sxs-lookup"><span data-stu-id="f6e61-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="f6e61-128">アプリ\_データフォルダーの追加</span><span class="sxs-lookup"><span data-stu-id="f6e61-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="f6e61-129">ここでは、SQL Server Express データベースファイルを保持するために、アプリ\_データディレクトリをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="f6e61-130">アプリ\_データは、データベースアクセスに対する適切なセキュリティアクセス許可を既に持っている ASP.NET の特別なディレクトリです。</span><span class="sxs-lookup"><span data-stu-id="f6e61-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="f6e61-131">[プロジェクト] メニューの [ASP.NET フォルダーの追加]、[アプリ\_データ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="f6e61-132">Web.config ファイルでの接続文字列の作成</span><span class="sxs-lookup"><span data-stu-id="f6e61-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="f6e61-133">Web サイトの構成ファイルに数行を追加して、Entity Framework がデータベースへの接続方法を認識できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f6e61-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="f6e61-134">プロジェクトのルートにある web.config ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6e61-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="f6e61-135">このファイルの一番下までスクロールし、次に示すように、最後の行のすぐ上に &lt;connectionStrings&gt; セクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="f6e61-136">コンテキストクラスの追加</span><span class="sxs-lookup"><span data-stu-id="f6e61-136">Adding a Context Class</span></span>

<span data-ttu-id="f6e61-137">[モデル] フォルダーを右クリックし、MusicStoreEntities.cs という名前の新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="f6e61-138">このクラスは Entity Framework データベースコンテキストを表し、作成、読み取り、更新、削除の各操作を処理します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="f6e61-139">このクラスのコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="f6e61-140">これで、他の構成や特別なインターフェイスなどはありません。DbContext 基本クラスを拡張することで、MusicStoreEntities クラスはデータベース操作を処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f6e61-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="f6e61-141">これで、データベース内の追加情報の一部を利用するために、いくつかのプロパティをモデルクラスに追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f6e61-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="f6e61-142">ストアカタログデータを追加しています</span><span class="sxs-lookup"><span data-stu-id="f6e61-142">Adding our store catalog data</span></span>

<span data-ttu-id="f6e61-143">新しく作成されたデータベースに "シード" データを追加する Entity Framework の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="f6e61-144">これにより、ストアカタログにジャンル、アーティスト、アルバムの一覧が事前設定されます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="f6e61-145">このチュートリアルの前半で使用したサイト設計ファイルが含まれている MvcMusicStore-Assets download には、このシードデータを含むクラスファイルがあります。このファイルは、コードという名前のフォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="f6e61-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="f6e61-146">次に示すように、[コード/モデル] フォルダー内の SampleData.cs ファイルを見つけて、プロジェクトの [モデル] フォルダーにドロップします。</span><span class="sxs-lookup"><span data-stu-id="f6e61-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="f6e61-147">次に、SampleData クラスについて Entity Framework を示す1行のコードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e61-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="f6e61-148">プロジェクトのルートにある global.asax ファイルをダブルクリックして開き、次の行をアプリケーション\_の開始メソッドの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="f6e61-149">この時点で、プロジェクトの Entity Framework を構成するために必要な作業が完了しました。</span><span class="sxs-lookup"><span data-stu-id="f6e61-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="f6e61-150">データベースに対するクエリの実行</span><span class="sxs-lookup"><span data-stu-id="f6e61-150">Querying the Database</span></span>

<span data-ttu-id="f6e61-151">次に、"ダミーデータ" を使用する代わりに、データベースを呼び出してすべての情報を照会するように、StoreController を更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f6e61-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="f6e61-152">まず、 **StoreController**のフィールドを宣言して、storedb という名前の MusicStoreEntities クラスのインスタンスを保持します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="f6e61-153">データベースに対してクエリを実行するためのストアインデックスの更新</span><span class="sxs-lookup"><span data-stu-id="f6e61-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="f6e61-154">MusicStoreEntities クラスは Entity Framework によって管理され、データベース内の各テーブルのコレクションプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="f6e61-155">StoreController のインデックスアクションを更新して、データベース内のすべてのジャンルを取得してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f6e61-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="f6e61-156">以前は、文字列データをハードコーディングしていました。</span><span class="sxs-lookup"><span data-stu-id="f6e61-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="f6e61-157">次に、Entity Framework コンテキストのコレクションを使用するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="f6e61-158">ビューテンプレートを変更する必要はありません。以前に返された同じ StoreIndexViewModel を返しています。ここでは、データベースからライブデータを返すだけです。</span><span class="sxs-lookup"><span data-stu-id="f6e61-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="f6e61-159">プロジェクトを再度実行して "/Store" URL にアクセスすると、データベース内のすべてのジャンルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="f6e61-160">ライブデータを使用するためのストアの参照と詳細の更新</span><span class="sxs-lookup"><span data-stu-id="f6e61-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="f6e61-161">/Store/Browse? genre = *[some genre]* アクションメソッドを使用して、名前でジャンルを検索しています。</span><span class="sxs-lookup"><span data-stu-id="f6e61-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="f6e61-162">同じジャンル名に対して2つのエントリを持つことはできないため、1つの結果のみが期待されます。これにより、を使用できるようになります。次のように適切な Genre オブジェクトを照会するための LINQ の単一 () 拡張機能 (これはまだ入力しないでください):</span><span class="sxs-lookup"><span data-stu-id="f6e61-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="f6e61-163">1つのメソッドは、ラムダ式をパラメーターとして受け取ります。これは、定義した値と名前が一致するように、1つの Genre オブジェクトを必要とすることを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="f6e61-164">上記の例では、Disco という名前の値を持つ1つの Genre オブジェクトを読み込んでいます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="f6e61-165">ここでは、Genre オブジェクトを取得するときに、読み込まれる他の関連エンティティを示すことができる Entity Framework 機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="f6e61-166">この機能はクエリ結果の整形と呼ばれており、必要なすべての情報を取得するために、データベースにアクセスする必要がある回数を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="f6e61-167">取得したジャンルのアルバムを事前にフェッチして、ジャンルに含まれるようにクエリを更新します。関連するアルバムが必要であることを示すには、"アルバム" を含めます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="f6e61-168">これは、1つのデータベース要求でジャンルとアルバムの両方のデータを取得するため、より効率的です。</span><span class="sxs-lookup"><span data-stu-id="f6e61-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="f6e61-169">説明については、更新された Browse controller アクションは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f6e61-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="f6e61-170">ストアの参照ビューを更新して、各ジャンルで利用できるアルバムを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f6e61-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="f6e61-171">ビューテンプレート (/Views/Store/Browse.cshtml にあります) を開き、次のように、アルバムの箇条書きリストを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e61-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="f6e61-172">アプリケーションを実行し、/ストア/参照を参照します。 genre = ジャズは、結果がデータベースからプルされ、選択したジャンルのすべてのアルバムが表示されるようになったことを示しています。</span><span class="sxs-lookup"><span data-stu-id="f6e61-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="f6e61-173">ここでは、/Store/[id] URL に対して同じ変更を行い、ダミーデータを、パラメーター値に一致する ID を持つアルバムを読み込むデータベースクエリに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="f6e61-174">アプリケーションを実行して/Store/Details/1 を参照すると、結果がデータベースからプルされていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="f6e61-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="f6e61-175">これで、ストアの詳細 ページがアルバム ID でアルバムを表示するように設定されたので、**参照** ビューを更新して詳細ビューにリンクします。</span><span class="sxs-lookup"><span data-stu-id="f6e61-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="f6e61-176">ここでは、Html.actionlink を使用します。これは、ストアインデックスから、前のセクションの最後のストア参照にリンクするのと同じです。</span><span class="sxs-lookup"><span data-stu-id="f6e61-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="f6e61-177">参照ビューの完全なソースが下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="f6e61-178">これで、ストアのページから、利用可能なアルバムを一覧表示するジャンルページを参照できるようになりました。アルバムをクリックすると、そのアルバムの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="f6e61-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="f6e61-179">[前へ](mvc-music-store-part-3.md)
> [次へ](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="f6e61-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
