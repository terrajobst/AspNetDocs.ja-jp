---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでのリポジトリと作業単位のパターンの実装 (9 件) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434380"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="4a53f-103">ASP.NET MVC アプリケーションでのリポジトリと作業単位のパターンの実装 (9 件)</span><span class="sxs-lookup"><span data-stu-id="4a53f-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>

<span data-ttu-id="4a53f-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4a53f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="4a53f-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="4a53f-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="4a53f-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="4a53f-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="4a53f-108">チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="4a53f-109">解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="4a53f-110">一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="4a53f-111">一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="4a53f-112">前のチュートリアルでは、継承を使用して、`Student` および `Instructor` エンティティクラスの冗長コードを減らしています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-112">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="4a53f-113">このチュートリアルでは、CRUD 操作にリポジトリと作業単位パターンを使用するいくつかの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-113">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="4a53f-114">前のチュートリアルと同様に、このチュートリアルでは、新しいページを作成するのではなく、既に作成したページに対するコードの動作方法を変更します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-114">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="4a53f-115">リポジトリと作業単位のパターン</span><span class="sxs-lookup"><span data-stu-id="4a53f-115">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="4a53f-116">リポジトリと作業単位のパターンは、アプリケーションのデータアクセス層とビジネスロジック層の間に抽象レイヤーを作成することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-116">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="4a53f-117">これらのパターンを実装すると、データ ストアの変更からアプリケーションを隔離でき、自動化された単体テストやテスト駆動開発 (TDD) を円滑化できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-117">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="4a53f-118">このチュートリアルでは、エンティティ型ごとにリポジトリクラスを実装します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-118">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="4a53f-119">`Student` エンティティ型については、リポジトリインターフェイスとリポジトリクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-119">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="4a53f-120">コントローラーでリポジトリをインスタンス化する場合は、コントローラーがリポジトリインターフェイスを実装するオブジェクトへの参照を受け入れるように、インターフェイスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-120">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="4a53f-121">コントローラーは、web サーバーで実行されると、Entity Framework と連携するリポジトリを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-121">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="4a53f-122">単体テストクラスで実行されているコントローラーは、メモリ内コレクションなど、テストのために簡単に操作できる方法で格納されているデータと連携するリポジトリを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-122">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="4a53f-123">このチュートリアルの後半では、複数のリポジトリと、`Course` コントローラーのエンティティ型の `Course` および `Department` の作業単位クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-123">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="4a53f-124">作業単位クラスは、すべてのリポジトリで共有される単一のデータベースコンテキストクラスを作成することによって、複数のリポジトリの作業を調整します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-124">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="4a53f-125">自動単体テストを実行できるようにする場合は、`Student` リポジトリの場合と同じように、これらのクラスのインターフェイスを作成して使用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-125">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="4a53f-126">ただし、このチュートリアルを簡単にするために、インターフェイスを使用せずにこれらのクラスを作成して使用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-126">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="4a53f-127">次の図は、リポジトリまたは作業単位のパターンをまったく使用しない場合と比較して、コントローラーとコンテキストクラス間のリレーションシップを概念化する方法の一例を示しています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-127">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="4a53f-129">このチュートリアルシリーズでは単体テストを作成しません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-129">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="4a53f-130">リポジトリパターンを使用する MVC アプリケーションでの TDD の概要については、「[チュートリアル: ASP.NET MVC での tdd の使用](https://msdn.microsoft.com/library/ff847525.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-130">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="4a53f-131">リポジトリパターンの詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-131">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="4a53f-132">MSDN の[リポジトリパターン](https://msdn.microsoft.com/library/ff649690.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4a53f-132">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="4a53f-133">Entity Framework チームブログの[「Entity Framework 4.0 でリポジトリと作業単位のパターンを使用する](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-133">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="4a53f-134">ジュリー Lerman のブログで、[アジャイル Entity Framework 4 リポジトリ](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)シリーズの投稿</span><span class="sxs-lookup"><span data-stu-id="4a53f-134">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="4a53f-135">Dan Wahlin のブログで、この[アカウントを一目で HTML5/JQuery アプリケーションで作成](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-135">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="4a53f-136">リポジトリと作業単位パターンを実装するには、さまざまな方法があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-136">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="4a53f-137">作業単位クラスの有無にかかわらず、リポジトリクラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-137">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="4a53f-138">すべてのエンティティ型に対して1つのリポジトリを実装することも、型ごとに1つのリポジトリを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-138">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="4a53f-139">型ごとに1つのを実装する場合は、個別のクラス、ジェネリック基底クラスと派生クラス、または抽象基底クラスと派生クラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-139">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="4a53f-140">リポジトリにビジネスロジックを含めることも、データアクセスロジックに限定することもできます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-140">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="4a53f-141">また、エンティティセットの[Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)型ではなく、 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)インターフェイスを使用して、データベースコンテキストクラスに抽象レイヤーを構築することもできます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-141">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="4a53f-142">このチュートリアルで示す抽象化レイヤーを実装する方法は、すべてのシナリオと環境について推奨するものではなく、考慮する必要がある1つのオプションです。</span><span class="sxs-lookup"><span data-stu-id="4a53f-142">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>

## <a name="creating-the-student-repository-class"></a><span data-ttu-id="4a53f-143">Student Repository クラスの作成</span><span class="sxs-lookup"><span data-stu-id="4a53f-143">Creating the Student Repository Class</span></span>

<span data-ttu-id="4a53f-144">*DAL*フォルダーで、 *IStudentRepository.cs*という名前のクラスファイルを作成し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-144">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="4a53f-145">このコードは、2つの read メソッド (すべての `Student` エンティティを返すメソッドと、ID によって1つの `Student` エンティティを検索するメソッド) を含む、一般的な CRUD メソッドのセットを宣言します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-145">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="4a53f-146">*DAL*フォルダーで、 *StudentRepository.cs* file という名前のクラスファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-146">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="4a53f-147">既存のコードを、`IStudentRepository` インターフェイスを実装する次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-147">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="4a53f-148">データベースコンテキストはクラス変数で定義され、コンストラクターは呼び出し元のオブジェクトがコンテキストのインスタンスを渡すことを想定しています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-148">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="4a53f-149">リポジトリで新しいコンテキストをインスタンス化することもできますが、1つのコントローラーで複数のリポジトリを使用した場合は、それぞれが個別のコンテキストで終了します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-149">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="4a53f-150">後で、`Course` コントローラーで複数のリポジトリを使用します。また、作業単位のクラスによって、すべてのリポジトリで同じコンテキストが使用されるかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-150">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="4a53f-151">リポジトリは[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)を実装し、コントローラーで前に見たようにデータベースコンテキストを破棄します。その CRUD メソッドは、前に見たのと同じ方法でデータベースコンテキストを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-151">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="4a53f-152">リポジトリを使用するように学生コントローラーを変更する</span><span class="sxs-lookup"><span data-stu-id="4a53f-152">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="4a53f-153">*StudentController.cs*で、現在クラスにあるコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-153">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="4a53f-154">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-154">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="4a53f-155">コントローラーは、コンテキストクラスではなく、`IStudentRepository` インターフェイスを実装するオブジェクトのクラス変数を宣言するようになりました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-155">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="4a53f-156">既定の (パラメーターなしの) コンストラクターは、新しいコンテキストインスタンスを作成します。また、省略可能なコンストラクターによって、呼び出し元はコンテキストインスタンスを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-156">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="4a53f-157">(*依存関係の挿入*(di) を使用していた場合は、既定のコンストラクターは必要ありません。 di ソフトウェアによって、正しいリポジトリオブジェクトが常に提供されるためです)。</span><span class="sxs-lookup"><span data-stu-id="4a53f-157">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="4a53f-158">CRUD メソッドでは、リポジトリはコンテキストではなく呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-158">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="4a53f-159">`Dispose` メソッドは、コンテキストではなくリポジトリを破棄するようになりました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-159">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="4a53f-160">サイトを実行し、 **[Students]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4a53f-160">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="4a53f-162">このページは、リポジトリを使用するようにコードを変更した場合と同じように動作し、他の学生ページも同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-162">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="4a53f-163">ただし、コントローラーの `Index` メソッドがフィルター処理と順序付けを行う方法には、重要な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-163">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="4a53f-164">このメソッドの元のバージョンには、次のコードが含まれていました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-164">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="4a53f-165">更新された `Index` メソッドには、次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-165">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="4a53f-166">強調表示されたコードのみが変更されています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-166">Only the highlighted code has changed.</span></span>

<span data-ttu-id="4a53f-167">コードの元のバージョンでは、`students` は `IQueryable` オブジェクトとして型指定されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-167">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="4a53f-168">`ToList`などのメソッドを使用してコレクションに変換されるまで、クエリはデータベースに送信されません。これは、インデックスビューが student モデルにアクセスするまで発生しません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-168">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="4a53f-169">上記の元のコードの `Where` メソッドは、データベースに送信される SQL クエリの `WHERE` 句になります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-169">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="4a53f-170">また、選択したエンティティのみがデータベースによって返されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-170">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="4a53f-171">ただし、`context.Students` を `studentRepository.GetStudents()`に変更すると、このステートメントの後にある `students` 変数は、データベース内のすべての学生を含む `IEnumerable` コレクションになります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-171">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="4a53f-172">`Where` メソッドを適用した結果は同じになりますが、作業は、データベースではなく、web サーバー上のメモリで実行されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-172">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="4a53f-173">大量のデータを返すクエリの場合、これは非効率的になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-173">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="4a53f-174">**IQueryable と IEnumerable**</span><span class="sxs-lookup"><span data-stu-id="4a53f-174">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="4a53f-175">次に示すように、リポジトリを実装した後、**検索**ボックスに何かを入力しても、SQL Server に送信されたクエリは、検索条件を含まないため、すべての Student 行を返します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-175">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="4a53f-176">このクエリでは、検索条件を認識せずにクエリが実行されたため、すべての学生データが返されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-176">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="4a53f-177">検索、検索条件の適用、ページング用のデータのサブセットの選択 (このケースでは3つの行のみを表示) の処理は、後で `ToPagedList` メソッドが `IEnumerable` コレクションで呼び出されたときにメモリ内で行われます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-177">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="4a53f-178">以前のバージョンのコードでは (リポジトリを実装する前)、`IQueryable` オブジェクトで `ToPagedList` が呼び出されたときに、検索条件が適用されるまで、クエリはデータベースに送信されません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-178">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="4a53f-179">`IQueryable` オブジェクトで ToPagedList が呼び出されると、SQL Server に送信されるクエリによって検索文字列が指定されます。結果として、検索条件を満たす行だけが返されます。メモリ内でフィルター処理を行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-179">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="4a53f-180">(次のチュートリアルでは、SQL Server に送信されたクエリを確認する方法について説明します)。</span><span class="sxs-lookup"><span data-stu-id="4a53f-180">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>

<span data-ttu-id="4a53f-181">次のセクションでは、データベースでこの作業を実行することを指定できるようにするリポジトリメソッドを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-181">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="4a53f-182">これで、コントローラーと Entity Framework データベースコンテキストの間に抽象レイヤーが作成されました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-182">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="4a53f-183">このアプリケーションで自動単体テストを実行する場合は、`IStudentRepository`を実装する単体テストプロジェクトで代替リポジトリクラスを作成でき*ます。*</span><span class="sxs-lookup"><span data-stu-id="4a53f-183">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="4a53f-184">このモックリポジトリクラスは、コンテキストを呼び出してデータの読み取りと書き込みを行うのではなく、コントローラー関数をテストするためにインメモリコレクションを操作できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-184">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="4a53f-185">汎用リポジトリと作業単位クラスを実装する</span><span class="sxs-lookup"><span data-stu-id="4a53f-185">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="4a53f-186">エンティティ型ごとにリポジトリクラスを作成すると、冗長なコードが大量に生成され、部分的な更新が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-186">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="4a53f-187">たとえば、同じトランザクションの一部として、2つの異なるエンティティ型を更新する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="4a53f-187">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="4a53f-188">それぞれが別のデータベースコンテキストインスタンスを使用している場合は、成功する可能性があり、もう1つは失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-188">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="4a53f-189">冗長なコードを最小限に抑える方法の1つとして、汎用リポジトリを使用し、すべてのリポジトリが同じデータベースコンテキストを使用する (つまり、すべての更新を調整する) ことを保証するには、作業単位クラスを使用する方法があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-189">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="4a53f-190">チュートリアルのこのセクションでは、`GenericRepository` クラスと `UnitOfWork` クラスを作成し、それらを `Course` コントローラーで使用して、`Department` と `Course` の両方のエンティティセットにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="4a53f-190">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="4a53f-191">前に説明したように、チュートリアルのこの部分を単純にするために、これらのクラスのインターフェイスを作成しません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-191">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="4a53f-192">ただし、TDD を容易にするために使用する場合は、通常、`Student` リポジトリと同じようにインターフェイスを使用して実装します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-192">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="4a53f-193">汎用リポジトリを作成する</span><span class="sxs-lookup"><span data-stu-id="4a53f-193">Create a Generic Repository</span></span>

<span data-ttu-id="4a53f-194">*DAL*フォルダーで、 *GenericRepository.cs*を作成し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-194">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="4a53f-195">クラス変数は、データベースコンテキストと、リポジトリがインスタンス化されるエンティティセットに対して宣言されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-195">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="4a53f-196">コンストラクターは、データベースコンテキストインスタンスを受け取り、エンティティセット変数を初期化します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-196">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="4a53f-197">`Get` メソッドは、ラムダ式を使用して、呼び出し元のコードがフィルター条件と結果を並べ替える列を指定できるようにします。また、文字列パラメーターを使用すると、呼び出し元は一括読み込みのためのナビゲーションプロパティのコンマ区切りリストを指定できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-197">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="4a53f-198">コード `Expression<Func<TEntity, bool>> filter` は、呼び出し元が `TEntity` の型に基づいてラムダ式を提供し、この式がブール値を返すことを意味します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-198">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="4a53f-199">たとえば、`Student` エンティティ型に対してリポジトリがインスタンス化されている場合、呼び出し元のメソッドのコードでは、`filter` パラメーターに対して `student => student.LastName == "Smith`&quot; を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-199">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="4a53f-200">また、コード `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` は、呼び出し元がラムダ式を提供することも意味します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-200">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="4a53f-201">ただし、この場合、式への入力は `TEntity` 型の `IQueryable` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="4a53f-201">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="4a53f-202">式は、その `IQueryable` オブジェクトの順序付けされたバージョンを返します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-202">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="4a53f-203">たとえば、`Student` エンティティ型に対してリポジトリがインスタンス化されている場合、呼び出し元のメソッドのコードでは、`orderBy` パラメーターの `q => q.OrderBy(s => s.LastName)` を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-203">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="4a53f-204">`Get` メソッドのコードは、`IQueryable` オブジェクトを作成し、フィルター式がある場合はそれを適用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-204">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="4a53f-205">次に、コンマ区切りのリストを解析した後、一括読み込み式を適用します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-205">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="4a53f-206">最後に、`orderBy` 式がある場合はそれを適用し、結果を返します。それ以外の場合は、順序付けられていないクエリの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-206">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="4a53f-207">`Get` メソッドを呼び出すと、これらの関数のパラメーターを指定する代わりに、メソッドによって返される `IEnumerable` コレクションに対してフィルター処理や並べ替えを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-207">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="4a53f-208">ただし、並べ替えとフィルター処理は、web サーバー上のメモリで実行されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-208">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="4a53f-209">これらのパラメーターを使用して、作業が web サーバーではなくデータベースによって実行されるようにします。</span><span class="sxs-lookup"><span data-stu-id="4a53f-209">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="4a53f-210">別の方法としては、特定のエンティティ型の派生クラスを作成し、`GetStudentsInNameOrder` や `GetStudentsByName`などの特殊な `Get` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-210">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="4a53f-211">ただし、複雑なアプリケーションでは、このような派生クラスや特殊なメソッドが多数発生する可能性があります。これは、保守作業がより多くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-211">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="4a53f-212">`GetByID`、`Insert`、および `Update` メソッドのコードは、非ジェネリックリポジトリで見たものと似ています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-212">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="4a53f-213">(`Find` メソッドを使用して一括読み込みを実行することはできないため、`GetByID` シグネチャに一括読み込みパラメーターを指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="4a53f-213">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="4a53f-214">`Delete` メソッドには、次の2つのオーバーロードが用意されています。</span><span class="sxs-lookup"><span data-stu-id="4a53f-214">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="4a53f-215">これらのいずれかを使用すると、削除するエンティティの ID だけを渡すことができ、1つのエンティティインスタンスを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="4a53f-215">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="4a53f-216">[同時実行の処理](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するチュートリアルで説明したように、同時実行の処理では、追跡プロパティの元の値を含むエンティティインスタンスを受け取る `Delete` メソッドが必要です。</span><span class="sxs-lookup"><span data-stu-id="4a53f-216">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="4a53f-217">この汎用リポジトリは、一般的な CRUD 要件を処理します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-217">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="4a53f-218">特定のエンティティ型に特別な要件 (より複雑なフィルター処理や順序付けなど) がある場合は、その型の追加のメソッドを持つ派生クラスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-218">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="4a53f-219">作業単位クラスの作成</span><span class="sxs-lookup"><span data-stu-id="4a53f-219">Creating the Unit of Work Class</span></span>

<span data-ttu-id="4a53f-220">作業単位クラスは、1つの目的を果たします。複数のリポジトリを使用するときに、1つのデータベースコンテキストを共有します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-220">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="4a53f-221">これにより、作業単位が完了したら、そのコンテキストのインスタンスで `SaveChanges` メソッドを呼び出して、関連するすべての変更が調整されることを保証できます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-221">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="4a53f-222">クラスが必要とするのは、`Save` メソッドと各リポジトリのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="4a53f-222">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="4a53f-223">各リポジトリプロパティは、他のリポジトリインスタンスと同じデータベースコンテキストインスタンスを使用してインスタンス化されたリポジトリインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-223">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="4a53f-224">*DAL*フォルダーで、 *UnitOfWork.cs*という名前のクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-224">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="4a53f-225">このコードは、データベースコンテキストと各リポジトリのクラス変数を作成します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-225">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="4a53f-226">`context` 変数の場合、新しいコンテキストがインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-226">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="4a53f-227">各リポジトリプロパティは、リポジトリが既に存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-227">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="4a53f-228">そうでない場合は、リポジトリがインスタンス化され、コンテキストインスタンスが渡されます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-228">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="4a53f-229">その結果、すべてのリポジトリは同じコンテキストインスタンスを共有します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-229">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="4a53f-230">`Save` メソッドは、データベースコンテキストで `SaveChanges` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-230">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="4a53f-231">クラス変数内のデータベースコンテキストをインスタンス化するクラスと同様に、`UnitOfWork` クラスは `IDisposable` を実装し、コンテキストを破棄します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-231">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="4a53f-232">UnitOfWork クラスとリポジトリを使用するようにコースコントローラーを変更する</span><span class="sxs-lookup"><span data-stu-id="4a53f-232">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="4a53f-233">*CourseController.cs*で現在使用しているコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-233">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="4a53f-234">このコードは、`UnitOfWork` クラスのクラス変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-234">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="4a53f-235">(ここでインターフェイスを使用していた場合は、ここで変数を初期化するのではなく、`Student` リポジトリの場合と同じように、2つのコンストラクターのパターンを実装します)。</span><span class="sxs-lookup"><span data-stu-id="4a53f-235">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="4a53f-236">クラスの残りの部分では、`UnitOfWork` プロパティを使用してリポジトリにアクセスすることにより、データベースコンテキストへのすべての参照が適切なリポジトリへの参照に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="4a53f-236">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="4a53f-237">`Dispose` メソッドは、`UnitOfWork` インスタンスを破棄します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-237">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="4a53f-238">サイトを実行し、 **[コース]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4a53f-238">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="4a53f-240">ページは変更前と同じように見えますが、他のコースページも同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-240">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="4a53f-241">まとめ</span><span class="sxs-lookup"><span data-stu-id="4a53f-241">Summary</span></span>

<span data-ttu-id="4a53f-242">これで、リポジトリと作業単位の両方のパターンが実装されました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-242">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="4a53f-243">汎用リポジトリでは、メソッドパラメーターとしてラムダ式を使用しました。</span><span class="sxs-lookup"><span data-stu-id="4a53f-243">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="4a53f-244">これらの式を `IQueryable` オブジェクトと共に使用する方法の詳細については、MSDN ライブラリの「 [IQueryable (t) インターフェイス (system.string)](https://msdn.microsoft.com/library/bb351562.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-244">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="4a53f-245">次のチュートリアルでは、いくつかの高度なシナリオを処理する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="4a53f-245">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="4a53f-246">その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4a53f-246">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4a53f-247">[前へ](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="4a53f-247">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
