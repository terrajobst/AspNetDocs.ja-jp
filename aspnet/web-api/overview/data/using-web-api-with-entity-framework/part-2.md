---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: モデルとコントローラーの追加 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449188"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="25a03-102">モデルとコントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="25a03-102">Add Models and Controllers</span></span>

<span data-ttu-id="25a03-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="25a03-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="25a03-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="25a03-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="25a03-105">このセクションでは、データベースエンティティを定義するモデルクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="25a03-106">次に、それらのエンティティに対して CRUD 操作を実行する Web API コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="25a03-107">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="25a03-107">Add Model Classes</span></span>

<span data-ttu-id="25a03-108">このチュートリアルでは、Entity Framework (EF) への "Code First" アプローチを使用してデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="25a03-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="25a03-109">Code First では、データベースC#テーブルに対応するクラスを記述し、EF によってデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="25a03-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="25a03-110">(詳細については、「 [Entity Framework の開発方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="25a03-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="25a03-111">まず、ドメインオブジェクトを POCOs (plain old CLR object) として定義します。</span><span class="sxs-lookup"><span data-stu-id="25a03-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="25a03-112">次の POCOs が作成されます。</span><span class="sxs-lookup"><span data-stu-id="25a03-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="25a03-113">Author</span><span class="sxs-lookup"><span data-stu-id="25a03-113">Author</span></span>
- <span data-ttu-id="25a03-114">Book</span><span class="sxs-lookup"><span data-stu-id="25a03-114">Book</span></span>

<span data-ttu-id="25a03-115">ソリューションエクスプローラーで、[モデル] フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="25a03-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="25a03-116">**[追加]** を選択し、 **[クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="25a03-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="25a03-117">クラスに `Author` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="25a03-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="25a03-118">Author.cs のすべての定型コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="25a03-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="25a03-119">次のコードを使用して、`Book`という名前の別のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="25a03-120">Entity Framework は、これらのモデルを使用してデータベーステーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="25a03-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="25a03-121">モデルごとに、`Id` プロパティがデータベーステーブルの主キー列になります。</span><span class="sxs-lookup"><span data-stu-id="25a03-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="25a03-122">Book クラスでは、`AuthorId` によって `Author` テーブルに外部キーが定義されます。</span><span class="sxs-lookup"><span data-stu-id="25a03-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="25a03-123">(わかりやすくするために、各書籍には1人の著者がいることを前提としています)。Book クラスには、関連する `Author`へのナビゲーションプロパティも含まれています。</span><span class="sxs-lookup"><span data-stu-id="25a03-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="25a03-124">ナビゲーションプロパティを使用して、コード内の関連する `Author` にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="25a03-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="25a03-125">第4部では、エンティティの関係を[処理](part-4.md)するナビゲーションプロパティについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="25a03-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="25a03-126">Web API コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="25a03-126">Add Web API Controllers</span></span>

<span data-ttu-id="25a03-127">このセクションでは、CRUD 操作 (作成、読み取り、更新、および削除) をサポートする Web API コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="25a03-128">コントローラーは Entity Framework を使用してデータベース層と通信します。</span><span class="sxs-lookup"><span data-stu-id="25a03-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="25a03-129">最初に、ファイルコントローラー/ファイルコントローラーの .cs を削除します。</span><span class="sxs-lookup"><span data-stu-id="25a03-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="25a03-130">このファイルには Web API コントローラーの例が含まれていますが、このチュートリアルでは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="25a03-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="25a03-131">次に、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="25a03-131">Next, build the project.</span></span> <span data-ttu-id="25a03-132">Web API のスキャフォールディングは、リフレクションを使用してモデルクラスを検索するため、コンパイルされたアセンブリが必要です。</span><span class="sxs-lookup"><span data-stu-id="25a03-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="25a03-133">ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="25a03-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="25a03-134">**[追加]** を選択し、 **[コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="25a03-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="25a03-135">**スキャフォールディングの追加** ダイアログで、Entity Framework アクションを含む Web API 2 コントローラー を選択します。</span><span class="sxs-lookup"><span data-stu-id="25a03-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="25a03-136">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="25a03-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="25a03-137">**[コントローラーの追加]** ダイアログで、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="25a03-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="25a03-138">**[モデルクラス]** ドロップダウンで、`Author` クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="25a03-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="25a03-139">(ドロップダウンリストに表示されない場合は、プロジェクトをビルドしたことを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="25a03-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="25a03-140">[Async controller アクションを使用する] をオンにします。</span><span class="sxs-lookup"><span data-stu-id="25a03-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="25a03-141">コントローラー名は &quot;AuthorsController&quot;のままにします。</span><span class="sxs-lookup"><span data-stu-id="25a03-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="25a03-142">**[データコンテキストクラス]** の横にある正符号 (+) ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="25a03-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="25a03-143">**[新しいデータコンテキスト]** ダイアログボックスで、既定の名前をそのまま使用し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="25a03-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="25a03-144">**[追加]** をクリックして、 **[コントローラーの追加]** ダイアログを完了します。</span><span class="sxs-lookup"><span data-stu-id="25a03-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="25a03-145">このダイアログでは、2つのクラスがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="25a03-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="25a03-146">`AuthorsController` は、Web API コントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="25a03-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="25a03-147">コントローラーは、クライアントが作成者の一覧に対して CRUD 操作を実行するために使用する REST API を実装します。</span><span class="sxs-lookup"><span data-stu-id="25a03-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="25a03-148">`BookServiceContext` は、実行時にエンティティオブジェクトを管理します。これには、データベースからのデータを使用したオブジェクトの読み込み、変更の追跡、データベースへのデータの保持などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="25a03-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="25a03-149">`DbContext` から継承します。</span><span class="sxs-lookup"><span data-stu-id="25a03-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="25a03-150">この時点で、プロジェクトをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="25a03-150">At this point, build the project again.</span></span> <span data-ttu-id="25a03-151">次に、同じ手順を実行して `Book` エンティティの API コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="25a03-152">今度は、モデルクラスの `Book` を選択し、データコンテキストクラスの既存の `BookServiceContext` クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="25a03-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="25a03-153">(新しいデータコンテキストを作成しないでください)。 **[追加]** をクリックしてコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="25a03-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="25a03-154">[前へ](part-1.md)
> [次へ](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="25a03-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
