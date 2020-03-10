---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2 での依存関係の注入-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、ASP.NET 4.x の ASP.NET Web API controller に依存関係を挿入する方法について説明します。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504946"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="aa7e5-103">ASP.NET Web API 2 での依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="aa7e5-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="aa7e5-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="aa7e5-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="aa7e5-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="aa7e5-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="aa7e5-106">このチュートリアルでは、ASP.NET Web API コントローラーに依存関係を挿入する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="aa7e5-107">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="aa7e5-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="aa7e5-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="aa7e5-108">Web API 2</span></span>
> - [<span data-ttu-id="aa7e5-109">Unity アプリケーションブロック</span><span class="sxs-lookup"><span data-stu-id="aa7e5-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="aa7e5-110">Entity Framework 6 (バージョン5も動作)</span><span class="sxs-lookup"><span data-stu-id="aa7e5-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="aa7e5-111">依存関係の挿入とは</span><span class="sxs-lookup"><span data-stu-id="aa7e5-111">What is Dependency Injection?</span></span>

<span data-ttu-id="aa7e5-112">"*依存関係*" とは、他のオブジェクトが必要とする任意のオブジェクトのことです。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="aa7e5-113">たとえば、データアクセスを処理する[リポジトリ](http://martinfowler.com/eaaCatalog/repository.html)を定義するのは一般的です。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="aa7e5-114">例を使って説明します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-114">Let's illustrate with an example.</span></span> <span data-ttu-id="aa7e5-115">まず、ドメインモデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="aa7e5-116">Entity Framework を使用してデータベースに項目を格納する単純なリポジトリクラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="aa7e5-117">次に、`Product` エンティティの GET 要求をサポートする Web API コントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="aa7e5-118">(簡潔にするために POST やその他の方法を抜けています)。最初の試行は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="aa7e5-119">コントローラークラスが `ProductRepository`に依存しており、コントローラーが `ProductRepository` インスタンスを作成することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="aa7e5-120">ただし、いくつかの理由から、この方法で依存関係をハードコーディングすることは不適切です。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="aa7e5-121">`ProductRepository` を別の実装に置き換える場合は、コントローラークラスも変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="aa7e5-122">`ProductRepository` に依存関係がある場合は、コントローラー内でこれらを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="aa7e5-123">複数のコントローラーを持つ大規模なプロジェクトの場合、構成コードはプロジェクト全体にわたって分散されます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="aa7e5-124">コントローラーはデータベースに対してクエリを実行するようにハードコーディングされているため、単体テストは困難です。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="aa7e5-125">単体テストでは、モックまたはスタブリポジトリを使用する必要があります。これは、現在の設計ではできません。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="aa7e5-126">これらの問題に対処するには、コントローラーにリポジトリを*挿入*します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="aa7e5-127">まず、`ProductRepository` クラスをインターフェイスにリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="aa7e5-128">次に、`IProductRepository` をコンストラクターパラメーターとして指定します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="aa7e5-129">この例では、[コンストラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="aa7e5-130">Setter*インジェクション*を使用することもできます。 setter メソッドまたはプロパティを使用して依存関係を設定します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="aa7e5-131">しかし、アプリケーションではコントローラーが直接作成されないため、問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="aa7e5-132">Web API は要求をルーティングするときにコントローラーを作成し、Web API は `IProductRepository`について何も知らない。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="aa7e5-133">ここで、Web API 依存関係競合回避モジュールが登場します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="aa7e5-134">Web API 依存関係競合回避モジュール</span><span class="sxs-lookup"><span data-stu-id="aa7e5-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="aa7e5-135">Web API は、依存関係を解決するための**Idependencyresolver**インターフェイスを定義します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="aa7e5-136">インターフェイスの定義を次に示します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="aa7e5-137">**IDependencyScope**インターフェイスには、次の2つのメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="aa7e5-138">**GetService**は、型のインスタンスを1つ作成します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="aa7e5-139">**Getservices**は、指定された型のオブジェクトのコレクションを作成します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="aa7e5-140">**Idependencyresolver**メソッドは**IDependencyScope**を継承し、 **beginscope**メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="aa7e5-141">スコープについては、このチュートリアルで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="aa7e5-142">Web API はコントローラーインスタンスを作成するときに、まず**Idependencyresolver. GetService**を呼び出し、コントローラーの種類を渡します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="aa7e5-143">この機能拡張フックを使用してコントローラーを作成し、依存関係を解決することができます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="aa7e5-144">**GetService**が null を返す場合、Web API はコントローラークラスでパラメーターなしのコンストラクターを検索します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="aa7e5-145">Unity コンテナーを使用した依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="aa7e5-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="aa7e5-146">完全な**Idependencyresolver**実装をゼロから作成することもできますが、インターフェイスは Web API と既存の IoC コンテナーの間のブリッジとして機能するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="aa7e5-147">IoC コンテナーは、依存関係の管理を担当するソフトウェアコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="aa7e5-148">型をコンテナーに登録した後、コンテナーを使用してオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="aa7e5-149">コンテナーは、依存関係の関係を自動的に判別します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="aa7e5-150">多くの IoC コンテナーでは、オブジェクトの有効期間やスコープなどを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7e5-151">"IoC" は、フレームワークがアプリケーションコードを呼び出す一般的なパターンである "コントロールの反転" を表します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="aa7e5-152">IoC コンテナーによってオブジェクトが構築され、通常の制御フローが "反転" されます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="aa7e5-153">このチュートリアルでは、Microsoft のパターン &amp; プラクティスから[Unity](https://msdn.microsoft.com/library/ff647202.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="aa7e5-154">(他の一般的なライブラリには、[城主の Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)、および構造体の[マップ](http://structuremap.github.io/documentation/)が含まれています)。NuGet パッケージマネージャーを使用して Unity をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="aa7e5-155">Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="aa7e5-156">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="aa7e5-157">Unity コンテナーをラップする**Idependencyresolver**の実装を次に示します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="aa7e5-158">**GetService**メソッドが型を解決できない場合は、 **null**を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="aa7e5-159">**Getservices**メソッドが型を解決できない場合は、空のコレクションオブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="aa7e5-160">不明な型に対しては例外をスローしません。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="aa7e5-161">依存関係競合回避モジュールの構成</span><span class="sxs-lookup"><span data-stu-id="aa7e5-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="aa7e5-162">グローバル**Httpconfiguration**オブジェクトの**dependencyresolver**プロパティに依存関係競合回避モジュールを設定します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="aa7e5-163">次のコードでは、`IProductRepository` インターフェイスを Unity に登録し、`UnityResolver`を作成します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="aa7e5-164">依存関係のスコープとコントローラーの有効期間</span><span class="sxs-lookup"><span data-stu-id="aa7e5-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="aa7e5-165">コントローラーは要求ごとに作成されます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-165">Controllers are created per request.</span></span> <span data-ttu-id="aa7e5-166">オブジェクトの有効期間を管理するために、 **Idependencyresolver**は*スコープ*の概念を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="aa7e5-167">**Httpconfiguration**オブジェクトにアタッチされている依存関係競合回避モジュールには、グローバルスコープがあります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="aa7e5-168">Web API がコントローラーを作成すると、 **Beginscope**が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="aa7e5-169">このメソッドは、子スコープを表す**IDependencyScope**を返します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="aa7e5-170">Web API は、子スコープで**GetService**を呼び出してコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="aa7e5-171">要求が完了すると、Web API は子スコープで**Dispose**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="aa7e5-172">**Dispose**メソッドを使用して、コントローラーの依存関係を破棄します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="aa7e5-173">**Beginscope**の実装方法は、IoC コンテナーによって異なります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="aa7e5-174">Unity の場合、スコープは子コンテナーに対応します。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="aa7e5-175">ほとんどの IoC コンテナーには同様の同等のものがあります。</span><span class="sxs-lookup"><span data-stu-id="aa7e5-175">Most IoC containers have similar equivalents.</span></span>
