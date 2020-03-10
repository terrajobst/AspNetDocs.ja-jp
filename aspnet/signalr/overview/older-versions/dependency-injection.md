---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1.x での依存関係の注入 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431542"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="b94b7-102">SignalR 1.x の依存関係挿入</span><span class="sxs-lookup"><span data-stu-id="b94b7-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="b94b7-103">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b94b7-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b94b7-104">依存関係の挿入は、オブジェクト間のハードコーディングされた依存関係を削除する方法であり、テスト (モックオブジェクトを使用) または実行時の動作の変更のために、オブジェクトの依存関係を簡単に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="b94b7-105">このチュートリアルでは、SignalR hub で依存関係の挿入を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="b94b7-106">また、SignalR で IoC コンテナーを使用する方法も示します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="b94b7-107">IoC コンテナーは、依存関係の挿入のための一般的なフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="b94b7-108">依存関係の挿入とは</span><span class="sxs-lookup"><span data-stu-id="b94b7-108">What is Dependency Injection?</span></span>

<span data-ttu-id="b94b7-109">依存関係の挿入について既によく理解している場合は、このセクションをスキップしてください。</span><span class="sxs-lookup"><span data-stu-id="b94b7-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="b94b7-110">*依存関係の挿入*(DI) は、オブジェクトが独自の依存関係を作成することを担当しないパターンです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="b94b7-111">DI を動機付けする簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="b94b7-112">メッセージをログに記録する必要があるオブジェクトがあるとします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="b94b7-113">ログインターフェイスを定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="b94b7-114">オブジェクトでは、メッセージをログに記録するための `ILogger` を作成できます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="b94b7-115">これは機能しますが、最適な設計ではありません。</span><span class="sxs-lookup"><span data-stu-id="b94b7-115">This works, but it's not the best design.</span></span> <span data-ttu-id="b94b7-116">`FileLogger` を別の `ILogger` 実装に置き換える場合は、`SomeComponent`を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="b94b7-117">他のオブジェクトの中には `FileLogger`を使用するものがあるため、すべてを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="b94b7-118">または、シングルトン `FileLogger` する場合は、アプリケーション全体で変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="b94b7-119">より適切な方法は、コンストラクター引数を使用して、オブジェクトに `ILogger` を "挿入" することです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="b94b7-120">これで、オブジェクトは、使用する `ILogger` を選択する責任を負いません。</span><span class="sxs-lookup"><span data-stu-id="b94b7-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="b94b7-121">`ILogger` の実装は、依存するオブジェクトを変更せずに切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="b94b7-122">このパターンは、[コンストラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="b94b7-123">もう1つのパターンは setter インジェクションで、setter メソッドまたはプロパティを使用して依存関係を設定します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="b94b7-124">SignalR での単純な依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="b94b7-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="b94b7-125">[SignalR を使用](../getting-started/tutorial-getting-started-with-signalr.md)したチュートリアルはじめにのチャットアプリケーションについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="b94b7-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="b94b7-126">そのアプリケーションのハブクラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="b94b7-127">送信前にチャットメッセージをサーバーに保存するとします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="b94b7-128">この機能を抽象化するインターフェイスを定義し、DI を使用して `ChatHub` クラスにインターフェイスを挿入することもできます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="b94b7-129">唯一の問題は、SignalR アプリケーションが直接ハブを作成しないことです。SignalR によって作成されます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="b94b7-130">既定では、SignalR はハブクラスにパラメーターなしのコンストラクターがあることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="b94b7-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="b94b7-131">ただし、ハブインスタンスを作成する関数を簡単に登録し、この関数を使用して DI を実行できます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="b94b7-132">**Globalhost. DependencyResolver. register**を呼び出して、関数を登録します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="b94b7-133">これで、SignalR インスタンス `ChatHub` を作成する必要があるときに、はこの匿名関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="b94b7-134">IoC コンテナー</span><span class="sxs-lookup"><span data-stu-id="b94b7-134">IoC Containers</span></span>

<span data-ttu-id="b94b7-135">前のコードは、単純なケースでは問題ありません。</span><span class="sxs-lookup"><span data-stu-id="b94b7-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="b94b7-136">しかし、次のように記述する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="b94b7-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="b94b7-137">多くの依存関係がある複雑なアプリケーションでは、この "配線" コードの多くを記述しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="b94b7-138">特に依存関係が入れ子になっている場合は、このコードを維持することは困難です。</span><span class="sxs-lookup"><span data-stu-id="b94b7-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="b94b7-139">単体テストも困難です。</span><span class="sxs-lookup"><span data-stu-id="b94b7-139">It is also hard to unit test.</span></span>

<span data-ttu-id="b94b7-140">1つの解決策は、IoC コンテナーを使用することです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="b94b7-141">IoC コンテナーは、依存関係の管理を担当するソフトウェアコンポーネントです。型をコンテナーに登録した後、コンテナーを使用してオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="b94b7-142">コンテナーは、依存関係の関係を自動的に判別します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="b94b7-143">多くの IoC コンテナーでは、オブジェクトの有効期間やスコープなどを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="b94b7-144">"IoC" は、フレームワークがアプリケーションコードを呼び出す一般的なパターンである "コントロールの反転" を表します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="b94b7-145">IoC コンテナーによってオブジェクトが構築され、通常の制御フローが "反転" されます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="b94b7-146">SignalR での IoC コンテナーの使用</span><span class="sxs-lookup"><span data-stu-id="b94b7-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="b94b7-147">多くの場合、このチャットアプリケーションは、IoC コンテナーを活用するのには簡単ではありません。</span><span class="sxs-lookup"><span data-stu-id="b94b7-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="b94b7-148">では、 [Stockticker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)サンプルを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="b94b7-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="b94b7-149">StockTicker サンプルでは、次の2つの主要なクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="b94b7-150">`StockTickerHub`: クライアント接続を管理するハブクラス。</span><span class="sxs-lookup"><span data-stu-id="b94b7-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="b94b7-151">`StockTicker`: 株価を保持し、定期的に更新するシングルトン。</span><span class="sxs-lookup"><span data-stu-id="b94b7-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="b94b7-152">`StockTickerHub` は `StockTicker` シングルトンへの参照を保持し、`StockTicker` は `StockTickerHub`の**IHubConnectionContext**への参照を保持します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="b94b7-153">このインターフェイスを使用して、`StockTickerHub` インスタンスと通信します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="b94b7-154">(詳細については、「 [ASP.NET SignalR でのサーバーブロードキャスト](index.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b94b7-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="b94b7-155">IoC コンテナーを使用して、これらの依存関係をビットに untangle ことができます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="b94b7-156">まず、`StockTickerHub` クラスと `StockTicker` クラスを簡略化しましょう。</span><span class="sxs-lookup"><span data-stu-id="b94b7-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="b94b7-157">次のコードでは、必要のない部分をコメント化しています。</span><span class="sxs-lookup"><span data-stu-id="b94b7-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="b94b7-158">パラメーターなしのコンストラクターを `StockTicker`から削除します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="b94b7-159">代わりに、常に DI を使用してハブを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="b94b7-160">StockTicker の場合は、シングルトンインスタンスを削除します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="b94b7-161">後で、IoC コンテナーを使用して StockTicker の有効期間を制御します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="b94b7-162">また、コンストラクターをパブリックにします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="b94b7-163">次に、`StockTicker`のインターフェイスを作成してコードをリファクターできます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="b94b7-164">このインターフェイスを使用して、`StockTicker` クラスの `StockTickerHub` を分離します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="b94b7-165">この種のリファクタリングは、Visual Studio によって簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="b94b7-166">StockTicker.cs ファイルを開き、`StockTicker` クラスの宣言を右クリックして、[**リファクター** ...] を選択します。**インターフェイスを抽出**します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="b94b7-167">**[インターフェイスの抽出]** ダイアログで、 **[すべて選択]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="b94b7-168">他の既定値はそのままにします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-168">Leave the other defaults.</span></span> <span data-ttu-id="b94b7-169">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="b94b7-170">Visual Studio によって `IStockTicker`という名前の新しいインターフェイスが作成され、`IStockTicker`から派生する `StockTicker` も変更されます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="b94b7-171">IStockTicker.cs ファイルを開き、インターフェイスを**public**に変更します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="b94b7-172">`StockTickerHub` クラスで、`StockTicker` の2つのインスタンスを `IStockTicker`に変更します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="b94b7-173">`IStockTicker` インターフェイスの作成は、厳密には必要ありませんが、アプリケーション内のコンポーネント間の結合を減らすために DI がどのように役立つかを説明したいと考えました。</span><span class="sxs-lookup"><span data-stu-id="b94b7-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="b94b7-174">Ninject ライブラリを追加する</span><span class="sxs-lookup"><span data-stu-id="b94b7-174">Add the Ninject Library</span></span>

<span data-ttu-id="b94b7-175">.NET 用に多数のオープンソースの IoC コンテナーがあります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="b94b7-176">このチュートリアルでは、 [Ninject](http://www.ninject.org/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="b94b7-177">(他の一般的なライブラリには、[城主の Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)、および構造体の[マップ](http://docs.structuremap.net)が含まれています)。</span><span class="sxs-lookup"><span data-stu-id="b94b7-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="b94b7-178">NuGet パッケージマネージャーを使用して、 [Ninject ライブラリ](https://nuget.org/packages/Ninject/3.0.1.10)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="b94b7-179">Visual Studio で、 **[ツール]** メニューの [ **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b94b7-180">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="b94b7-181">SignalR Dependency Resolver を置き換える</span><span class="sxs-lookup"><span data-stu-id="b94b7-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="b94b7-182">SignalR 内で Ninject を使用するには、 **Defaultdependencyresolver**から派生するクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="b94b7-183">このクラスは、 **Defaultdependencyresolver**の**GetService**メソッドと**getservices**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="b94b7-184">SignalR は、これらのメソッドを呼び出して、ハブインスタンスを含む、実行時にさまざまなオブジェクトを作成します。また、SignalR によって内部的に使用されるさまざまなサービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="b94b7-185">**GetService**メソッドは、型の1つのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="b94b7-186">Ninject カーネルの**Tryget**メソッドを呼び出すには、このメソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="b94b7-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="b94b7-187">このメソッドが null を返す場合は、既定の競合回避モジュールに戻ります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="b94b7-188">**Getservices**メソッドは、指定された型のオブジェクトのコレクションを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="b94b7-189">このメソッドをオーバーライドして、Ninject の結果と既定の競合回避モジュールの結果を連結します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="b94b7-190">Ninject バインドを構成する</span><span class="sxs-lookup"><span data-stu-id="b94b7-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="b94b7-191">ここで、Ninject を使用して型バインドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="b94b7-192">RegisterHubs.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="b94b7-193">`RegisterHubs.Start` メソッドで、ninject コンテナーを作成します。 Ninject は*カーネル*を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="b94b7-194">カスタム依存関係競合回避モジュールのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="b94b7-195">次のように `IStockTicker` のバインドを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="b94b7-196">このコードは2つのことを言います。</span><span class="sxs-lookup"><span data-stu-id="b94b7-196">This code is saying two things.</span></span> <span data-ttu-id="b94b7-197">まず、アプリケーションに `IStockTicker`が必要な場合は常に、カーネルが `StockTicker`のインスタンスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="b94b7-198">次に、`StockTicker` クラスをシングルトンオブジェクトとして作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b94b7-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="b94b7-199">Ninject は、オブジェクトのインスタンスを1つ作成し、要求ごとに同じインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="b94b7-200">次のように、 **IHubConnectionContext**のバインドを作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="b94b7-201">このコードは、 **IHubConnection**を返す匿名関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="b94b7-202">**WhenInjectedInto**メソッドは、`IStockTicker` のインスタンスを作成するときにのみ、この関数を使用するように ninject を指示します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="b94b7-203">その理由は、SignalR が**IHubConnectionContext**インスタンスを内部で作成し、SignalR がそれらを作成する方法をオーバーライドしないためです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="b94b7-204">この関数は、`StockTicker` クラスにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="b94b7-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="b94b7-205">**Maphubs**メソッドに依存関係競合回避モジュールを渡します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="b94b7-206">SignalR では、既定の競合回避モジュールではなく、 **Maphubs**に指定されている競合回避モジュールが使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b94b7-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="b94b7-207">`RegisterHubs.Start`の完全なコードリストを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="b94b7-208">Visual Studio で StockTicker アプリケーションを実行するには、F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="b94b7-209">ブラウザーウィンドウで、`http://localhost:*port*/SignalR.Sample/StockTicker.html`に移動します。</span><span class="sxs-lookup"><span data-stu-id="b94b7-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="b94b7-210">アプリケーションの機能は以前とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="b94b7-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="b94b7-211">(説明については、「 [ASP.NET SignalR でのサーバーブロードキャスト](index.md)」を参照してください)。動作は変更されていません。コードを簡単にテスト、保守、および進化させることができました。</span><span class="sxs-lookup"><span data-stu-id="b94b7-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
