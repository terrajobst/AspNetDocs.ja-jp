---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: データアクセス層を作成する |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575751"
---
# <a name="create-the-data-access-layer"></a><span data-ttu-id="2cb4d-103">データ アクセス層の作成</span><span class="sxs-lookup"><span data-stu-id="2cb4d-103">Create the Data Access Layer</span></span>

<span data-ttu-id="2cb4d-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="2cb4d-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="2cb4d-105">[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="2cb4d-106">このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="2cb4d-107">このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="2cb4d-108">このチュートリアルでは、ASP.NET Web フォームと Entity Framework Code First を使用して、データベースのデータを作成、アクセス、および確認する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="2cb4d-109">このチュートリアルは、前の「プロジェクトを作成する」チュートリアルに基づいており、Wingtip 玩具 Store チュートリアルシリーズの一部です。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="2cb4d-110">このチュートリアルを完了すると、プロジェクトの [*モデル*] フォルダーにあるデータアクセスクラスのグループが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2cb4d-111">学習内容:</span><span class="sxs-lookup"><span data-stu-id="2cb4d-111">What you'll learn:</span></span>

- <span data-ttu-id="2cb4d-112">データモデルを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-112">How to create the data models.</span></span>
- <span data-ttu-id="2cb4d-113">データベースを初期化してシードする方法。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="2cb4d-114">データベースをサポートするようにアプリケーションを更新および構成する方法。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="2cb4d-115">このチュートリアルで導入された機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="2cb4d-116">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="2cb4d-116">Entity Framework Code First</span></span>
- <span data-ttu-id="2cb4d-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="2cb4d-117">LocalDB</span></span>
- <span data-ttu-id="2cb4d-118">データの注釈</span><span class="sxs-lookup"><span data-stu-id="2cb4d-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="2cb4d-119">データモデルの作成</span><span class="sxs-lookup"><span data-stu-id="2cb4d-119">Creating the Data Models</span></span>

<span data-ttu-id="2cb4d-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723)は、オブジェクトリレーショナルマッピング (ORM) フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="2cb4d-121">これにより、リレーショナルデータをオブジェクトとして扱うことができるため、通常は書き込む必要があるほとんどのデータアクセスコードが排除されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="2cb4d-122">Entity Framework を使用すると、 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx)を使用してクエリを発行し、厳密に型指定されたオブジェクトとしてデータを取得および操作できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="2cb4d-123">LINQ には、データのクエリと更新のためのパターンが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="2cb4d-124">Entity Framework を使用すると、データアクセスの基礎を重視するのではなく、アプリケーションの残りの部分を作成することに集中できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="2cb4d-125">このチュートリアルシリーズの後半では、データを使用してナビゲーションと製品のクエリを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="2cb4d-126">Entity Framework は、 *Code First*と呼ばれる開発パラダイムをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="2cb4d-127">Code First を使用すると、クラスを使用してデータモデルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="2cb4d-128">クラスは、他の型、メソッド、およびイベントの変数をまとめてグループ化することによって、独自のカスタム型を作成できるようにするコンストラクトです。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="2cb4d-129">クラスは、既存のデータベースにマップすることも、データベースを生成するために使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="2cb4d-130">このチュートリアルでは、データモデルクラスを記述してデータモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="2cb4d-131">次に、これらの新しいクラスを使用して、すぐにデータベースを作成 Entity Framework ます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="2cb4d-132">最初に、Web フォームアプリケーションのデータモデルを定義するエンティティクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="2cb4d-133">次に、エンティティクラスを管理し、データベースへのデータアクセスを提供するコンテキストクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="2cb4d-134">また、データベースを設定するために使用する初期化子クラスも作成します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="2cb4d-135">Entity Framework と参照</span><span class="sxs-lookup"><span data-stu-id="2cb4d-135">Entity Framework and References</span></span>

<span data-ttu-id="2cb4d-136">既定では、 **Web フォーム**テンプレートを使用して新しい**ASP.NET web アプリケーション**を作成するときに Entity Framework が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="2cb4d-137">Entity Framework は、NuGet パッケージとしてインストール、アンインストール、および更新できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="2cb4d-138">この NuGet パッケージには、次の**ランタイム**アセンブリがプロジェクト内に含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="2cb4d-139">EntityFramework .dll – Entity Framework によって使用されるすべての共通ランタイムコード</span><span class="sxs-lookup"><span data-stu-id="2cb4d-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="2cb4d-140">EntityFramework. SqlServer .dll – Entity Framework の Microsoft SQL Server プロバイダー</span><span class="sxs-lookup"><span data-stu-id="2cb4d-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="2cb4d-141">エンティティクラス</span><span class="sxs-lookup"><span data-stu-id="2cb4d-141">Entity Classes</span></span>

<span data-ttu-id="2cb4d-142">データのスキーマを定義するために作成したクラスは、エンティティクラスと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="2cb4d-143">データベースの設計に慣れていない場合は、エンティティクラスをデータベースのテーブル定義と見なしてください。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="2cb4d-144">クラスの各プロパティは、データベースのテーブルの列を指定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="2cb4d-145">これらのクラスは、オブジェクト指向コードとデータベースのリレーショナルテーブル構造との間に、軽量のオブジェクトリレーショナルインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="2cb4d-146">このチュートリアルでは、製品とカテゴリのスキーマを表す単純なエンティティクラスを追加することから始めます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="2cb4d-147">Products クラスには、各製品の定義が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="2cb4d-148">Product クラスの各メンバーの名前は、`ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`、および `Category`になります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="2cb4d-149">Category クラスには、車両、ボート、平面など、製品が属することができる各カテゴリの定義が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="2cb4d-150">Category クラスの各メンバーの名前は、`CategoryID`、`CategoryName`、`Description`、および `Products`になります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="2cb4d-151">各製品は、いずれかのカテゴリに属します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="2cb4d-152">これらのエンティティクラスは、プロジェクトの [既存の*モデル*] フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="2cb4d-153">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、[ -&gt;**新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![データアクセス層を作成する-[新しい項目] メニュー](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="2cb4d-155">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="2cb4d-156">左側の **[インストール済み]** ウィンドウの **[ビジュアルC# ]** で、 **[コード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![データアクセス層を作成する-[新しい項目] メニュー](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="2cb4d-158">中央のペインから **[クラス]** を選択し、この新しいクラスに*Product.cs*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="2cb4d-159">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-159">Click **Add**.</span></span>  
   <span data-ttu-id="2cb4d-160">新しいクラスファイルがエディターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="2cb4d-161">既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="2cb4d-162">手順 1. ~ 4. を繰り返して別のクラスを作成し、新しいクラスに*Category.cs*という名前を付けて、既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="2cb4d-163">前述のように、`Category` クラスは、アプリケーションが販売するように設計されている製品の<a id="a"></a>種類 (&quot;自動車&quot;、&quot;ボート&quot;、&quot;Rockets&quot;など) を表します。また、`Product` クラスは、データベース内の個々の製品 (toys) を表します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="2cb4d-164">`Product` オブジェクトの各インスタンスは、リレーショナルデータベーステーブル内の行に対応します。 Product クラスの各プロパティは、リレーショナルデータベーステーブルの列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="2cb4d-165">このチュートリアルの後の方で、データベースに含まれている製品データを確認します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="2cb4d-166">データの注釈</span><span class="sxs-lookup"><span data-stu-id="2cb4d-166">Data Annotations</span></span>

<span data-ttu-id="2cb4d-167">クラスの一部のメンバーには、`[ScaffoldColumn(false)]`など、メンバーに関する詳細を指定する属性があることに気付きました。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="2cb4d-168">これらは*データ注釈*です。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-168">These are *data annotations*.</span></span> <span data-ttu-id="2cb4d-169">データ注釈属性では、そのメンバーのユーザー入力を検証する方法、そのメンバーの書式を指定する方法、およびデータベースの作成時にモデル化する方法を指定できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="2cb4d-170">Context クラス</span><span class="sxs-lookup"><span data-stu-id="2cb4d-170">Context Class</span></span>

<span data-ttu-id="2cb4d-171">クラスを使用してデータアクセスを開始するには、コンテキストクラスを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="2cb4d-172">前述のように、コンテキストクラスは、エンティティクラス (`Product` クラスや `Category` クラスなど) を管理し、データベースへのデータアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="2cb4d-173">この手順では、 C#新しいコンテキストクラスを [*モデル*] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="2cb4d-174">[*モデル*] フォルダーを右クリックし、[**新しい項目**の -&gt;**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="2cb4d-175">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="2cb4d-176">中央のペインで **[クラス]** を選択し、「 *ProductContext.cs* 」という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="2cb4d-177">クラスに含まれる既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="2cb4d-178">このコードは、厳密に型指定されたオブジェクトを使用してデータのクエリ、挿入、更新、および削除を行う機能を含む、Entity Framework のすべてのコア機能にアクセスできるように、`System.Data.Entity` 名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="2cb4d-179">`ProductContext` クラスは Entity Framework 製品データベースコンテキストを表します。これは、データベース内の `Product` クラスインスタンスのフェッチ、格納、および更新を処理します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="2cb4d-180">`ProductContext` クラスは Entity Framework によって提供される `DbContext` 基底クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="2cb4d-181">初期化子クラス</span><span class="sxs-lookup"><span data-stu-id="2cb4d-181">Initializer Class</span></span>

<span data-ttu-id="2cb4d-182">コンテキストが初めて使用されたときにデータベースを初期化するには、いくつかのカスタムロジックを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="2cb4d-183">これにより、シードデータをデータベースに追加して、製品とカテゴリをすぐに表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="2cb4d-184">この手順では、 C#新しい初期化子クラスを [*モデル*] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="2cb4d-185">[*モデル*] フォルダーに別の `Class` を作成し、「 *ProductDatabaseInitializer.cs*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="2cb4d-186">クラスに含まれる既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="2cb4d-187">上記のコードからわかるように、データベースを作成および初期化すると、`Seed` プロパティがオーバーライドされ、設定されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="2cb4d-188">`Seed` プロパティが設定されている場合は、カテゴリと製品の値を使用してデータベースを設定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="2cb4d-189">データベースの作成後に上記のコードを変更してシードデータを更新しようとすると、Web アプリケーションを実行しても更新は表示されません。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="2cb4d-190">その理由は、上記のコードでは、`DropCreateDatabaseIfModelChanges` クラスの実装を使用して、シードデータをリセットする前にモデル (スキーマ) が変更されたかどうかを認識するためです。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="2cb4d-191">`Category` エンティティクラスと `Product` エンティティクラスが変更されていない場合、データベースはシードデータを使用して再初期化されません。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2cb4d-192">アプリケーションを実行するたびにデータベースを再作成する場合は、`DropCreateDatabaseIfModelChanges` クラスではなく、`DropCreateDatabaseAlways` クラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="2cb4d-193">ただし、このチュートリアルシリーズでは、`DropCreateDatabaseIfModelChanges` クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>

<span data-ttu-id="2cb4d-194">このチュートリアルのこの時点では、4つの新しいクラスと1つの既定のクラスを持つ*モデル*フォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![データアクセスレイヤー-モデルフォルダーを作成する](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="2cb4d-196">データモデルを使用するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="2cb4d-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="2cb4d-197">データを表すクラスを作成したので、クラスを使用するようにアプリケーションを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="2cb4d-198">*Global.asax*ファイルで、モデルを初期化するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="2cb4d-199">*Web.config ファイルで*、新しいデータクラスによって表されるデータを格納するために使用するデータベースをアプリケーションに通知する情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="2cb4d-200">*Global.asax*ファイルは、アプリケーションイベントまたはメソッドを処理するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="2cb4d-201">Web.config*ファイルを*使用すると、ASP.NET web アプリケーションの構成を制御できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="2cb4d-202">Global.asax ファイルを更新しています</span><span class="sxs-lookup"><span data-stu-id="2cb4d-202">Updating the Global.asax file</span></span>

<span data-ttu-id="2cb4d-203">アプリケーションの起動時にデータモデルを初期化するには、 *Global.asax.cs*ファイルの `Application_Start` ハンドラーを更新します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2cb4d-204">ソリューションエクスプローラーでは、 *global.asax*ファイルまたは*Global.asax.cs*ファイルのいずれかを選択して、 *Global.asax.cs*ファイルを編集できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>

1. <span data-ttu-id="2cb4d-205">*Global.asax.cs*ファイルの `Application_Start` メソッドに、黄色で強調表示されている次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="2cb4d-206">ブラウザーでこのチュートリアルシリーズを表示するときに、ブラウザーで HTML5 をサポートして、黄色で強調表示されているコードを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>

<span data-ttu-id="2cb4d-207">上のコードに示すように、アプリケーションの起動時に、アプリケーションは、データに初めてアクセスしたときに実行される初期化子を指定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="2cb4d-208">`Database` オブジェクトおよび `ProductDatabaseInitializer` オブジェクトにアクセスするには、2つの追加の名前空間が必要です。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="2cb4d-209">Web.config ファイルの変更</span><span class="sxs-lookup"><span data-stu-id="2cb4d-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="2cb4d-210">データベースにシードデータが設定されると、Entity Framework Code First によって既定の場所にデータベースが生成されますが、独自の接続情報をアプリケーションに追加することで、データベースの場所を制御できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="2cb4d-211">このデータベース接続は、プロジェクトのルートにあるアプリケーションの*web.config*ファイル内の接続文字列を使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="2cb4d-212">新しい接続文字列を追加することによって、データベース (*ウィング*) の場所を、既定の場所ではなく、アプリケーションのデータディレクトリ (*アプリ\_データ*) に組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="2cb4d-213">この変更を行うと、このチュートリアルの後半でデータベースファイルを検索して調べることができます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="2cb4d-214">\**ソリューションエクスプローラー\*\*\*で、web.config ファイルを*見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="2cb4d-215">次のように、黄色で強調表示されている接続文字列を*web.config ファイルの*`<connectionStrings>` セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="2cb4d-216">アプリケーションを初めて実行すると、接続文字列によって指定された場所にデータベースが構築されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="2cb4d-217">しかし、アプリケーションを実行する前に、最初にビルドしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="2cb4d-218">アプリケーションのビルド</span><span class="sxs-lookup"><span data-stu-id="2cb4d-218">Building the Application</span></span>

<span data-ttu-id="2cb4d-219">Web アプリケーションに対するすべてのクラスと変更が確実に動作するようにするには、アプリケーションをビルドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="2cb4d-220">**[デバッグ]** メニューの **[ウィングヒント toys のビルド]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="2cb4d-221">**[出力]** ウィンドウが表示され、すべて*正常に完了*すると、成功メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![データアクセス層の出力ウィンドウを作成する](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="2cb4d-223">エラーが発生した場合は、上記の手順を再確認してください。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="2cb4d-224">**[出力]** ウィンドウの情報には、問題が発生しているファイルと、ファイル内の変更が必要な場所が示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="2cb4d-225">この情報を使用すると、プロジェクトで上記の手順のどの部分を確認し、修正する必要があるかを判断できます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="2cb4d-226">要約</span><span class="sxs-lookup"><span data-stu-id="2cb4d-226">Summary</span></span>

<span data-ttu-id="2cb4d-227">このシリーズのこのチュートリアルでは、と同様に、データモデルを作成し、データベースの初期化とシードに使用するコードを追加しました。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="2cb4d-228">また、アプリケーションの実行時にデータモデルを使用するようにアプリケーションを構成しました。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="2cb4d-229">次のチュートリアルでは、UI を更新し、ナビゲーションを追加して、データベースからデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="2cb4d-230">これにより、このチュートリアルで作成したエンティティクラスに基づいて、データベースが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cb4d-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2cb4d-231">その他の資料</span><span class="sxs-lookup"><span data-stu-id="2cb4d-231">Additional Resources</span></span>

<span data-ttu-id="2cb4d-232">[Entity Framework の概要](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="2cb4d-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="2cb4d-233">[ADO.NET Entity Framework  の初心](https://msdn.microsoft.com/data/ee712907)者向けガイド</span><span class="sxs-lookup"><span data-stu-id="2cb4d-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="2cb4d-234">[Entity Framework を使用した Code First 開発](http://www.msteched.com/2010/Europe/DEV212)(ビデオ)</span><span class="sxs-lookup"><span data-stu-id="2cb4d-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="2cb4d-235">[Code First リレーションシップの FLUENT API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="2cb4d-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="2cb4d-236">データ注釈の Code First</span><span class="sxs-lookup"><span data-stu-id="2cb4d-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="2cb4d-237">Entity Framework の生産性の向上</span><span class="sxs-lookup"><span data-stu-id="2cb4d-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="2cb4d-238">[前へ](create-the-project.md)
> [次へ](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="2cb4d-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
