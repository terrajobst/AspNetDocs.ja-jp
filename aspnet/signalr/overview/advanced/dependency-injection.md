---
uid: signalr/overview/advanced/dependency-injection
title: SignalR | での依存関係の挿入Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431866"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="cb8bf-103">SignalR の依存関係挿入</span><span class="sxs-lookup"><span data-stu-id="cb8bf-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="cb8bf-104">[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="cb8bf-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="cb8bf-105">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="cb8bf-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="cb8bf-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cb8bf-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="cb8bf-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="cb8bf-107">.NET 4.5</span></span>
> - <span data-ttu-id="cb8bf-108">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="cb8bf-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="cb8bf-109">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="cb8bf-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="cb8bf-110">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="cb8bf-111">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="cb8bf-111">Questions and comments</span></span>
>
> <span data-ttu-id="cb8bf-112">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cb8bf-113">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="cb8bf-114">依存関係の挿入は、オブジェクト間のハードコーディングされた依存関係を削除する方法であり、テスト (モックオブジェクトを使用) または実行時の動作の変更のために、オブジェクトの依存関係を簡単に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="cb8bf-115">このチュートリアルでは、SignalR hub で依存関係の挿入を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="cb8bf-116">また、SignalR で IoC コンテナーを使用する方法も示します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="cb8bf-117">IoC コンテナーは、依存関係の挿入のための一般的なフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="cb8bf-118">依存関係の挿入とは</span><span class="sxs-lookup"><span data-stu-id="cb8bf-118">What is Dependency Injection?</span></span>

<span data-ttu-id="cb8bf-119">依存関係の挿入について既によく理解している場合は、このセクションをスキップしてください。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="cb8bf-120">*依存関係の挿入*(DI) は、オブジェクトが独自の依存関係を作成することを担当しないパターンです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="cb8bf-121">DI を動機付けする簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="cb8bf-122">メッセージをログに記録する必要があるオブジェクトがあるとします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="cb8bf-123">ログインターフェイスを定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="cb8bf-124">オブジェクトでは、メッセージをログに記録するための `ILogger` を作成できます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="cb8bf-125">これは機能しますが、最適な設計ではありません。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-125">This works, but it's not the best design.</span></span> <span data-ttu-id="cb8bf-126">`FileLogger` を別の `ILogger` 実装に置き換える場合は、`SomeComponent`を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="cb8bf-127">他のオブジェクトの中には `FileLogger`を使用するものがあるため、すべてを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="cb8bf-128">または、シングルトン `FileLogger` する場合は、アプリケーション全体で変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="cb8bf-129">より適切な方法は、コンストラクター引数を使用して、オブジェクトに `ILogger` を "挿入" することです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="cb8bf-130">これで、オブジェクトは、使用する `ILogger` を選択する責任を負いません。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="cb8bf-131">`ILogger` の実装は、依存するオブジェクトを変更せずに切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="cb8bf-132">このパターンは、[コンストラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="cb8bf-133">もう1つのパターンは setter インジェクションで、setter メソッドまたはプロパティを使用して依存関係を設定します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="cb8bf-134">SignalR での単純な依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="cb8bf-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="cb8bf-135">[SignalR を使用](../getting-started/tutorial-getting-started-with-signalr.md)したチュートリアルはじめにのチャットアプリケーションについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="cb8bf-136">そのアプリケーションのハブクラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="cb8bf-137">送信前にチャットメッセージをサーバーに保存するとします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="cb8bf-138">この機能を抽象化するインターフェイスを定義し、DI を使用して `ChatHub` クラスにインターフェイスを挿入することもできます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="cb8bf-139">唯一の問題は、SignalR アプリケーションが直接ハブを作成しないことです。SignalR によって作成されます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="cb8bf-140">既定では、SignalR はハブクラスにパラメーターなしのコンストラクターがあることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="cb8bf-141">ただし、ハブインスタンスを作成する関数を簡単に登録し、この関数を使用して DI を実行できます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="cb8bf-142">**Globalhost. DependencyResolver. register**を呼び出して、関数を登録します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="cb8bf-143">これで、SignalR インスタンス `ChatHub` を作成する必要があるときに、はこの匿名関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="cb8bf-144">IoC コンテナー</span><span class="sxs-lookup"><span data-stu-id="cb8bf-144">IoC Containers</span></span>

<span data-ttu-id="cb8bf-145">前のコードは、単純なケースでは問題ありません。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="cb8bf-146">しかし、次のように記述する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="cb8bf-147">多くの依存関係がある複雑なアプリケーションでは、この "配線" コードの多くを記述しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="cb8bf-148">特に依存関係が入れ子になっている場合は、このコードを維持することは困難です。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="cb8bf-149">単体テストも困難です。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-149">It is also hard to unit test.</span></span>

<span data-ttu-id="cb8bf-150">1つの解決策は、IoC コンテナーを使用することです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="cb8bf-151">IoC コンテナーは、依存関係の管理を担当するソフトウェアコンポーネントです。型をコンテナーに登録した後、コンテナーを使用してオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="cb8bf-152">コンテナーは、依存関係の関係を自動的に判別します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="cb8bf-153">多くの IoC コンテナーでは、オブジェクトの有効期間やスコープなどを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="cb8bf-154">"IoC" は、フレームワークがアプリケーションコードを呼び出す一般的なパターンである "コントロールの反転" を表します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="cb8bf-155">IoC コンテナーによってオブジェクトが構築され、通常の制御フローが "反転" されます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="cb8bf-156">SignalR での IoC コンテナーの使用</span><span class="sxs-lookup"><span data-stu-id="cb8bf-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="cb8bf-157">多くの場合、このチャットアプリケーションは、IoC コンテナーを活用するのには簡単ではありません。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="cb8bf-158">では、 [Stockticker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)サンプルを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="cb8bf-159">StockTicker サンプルでは、次の2つの主要なクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="cb8bf-160">`StockTickerHub`: クライアント接続を管理するハブクラス。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="cb8bf-161">`StockTicker`: 株価を保持し、定期的に更新するシングルトン。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="cb8bf-162">`StockTickerHub` は `StockTicker` シングルトンへの参照を保持し、`StockTicker` は `StockTickerHub`の**IHubConnectionContext**への参照を保持します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="cb8bf-163">このインターフェイスを使用して、`StockTickerHub` インスタンスと通信します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="cb8bf-164">(詳細については、「 [ASP.NET SignalR でのサーバーブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="cb8bf-165">IoC コンテナーを使用して、これらの依存関係をビットに untangle ことができます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="cb8bf-166">まず、`StockTickerHub` クラスと `StockTicker` クラスを簡略化しましょう。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="cb8bf-167">次のコードでは、必要のない部分をコメント化しています。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="cb8bf-168">パラメーターなしのコンストラクターを `StockTickerHub`から削除します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="cb8bf-169">代わりに、常に DI を使用してハブを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="cb8bf-170">StockTicker の場合は、シングルトンインスタンスを削除します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="cb8bf-171">後で、IoC コンテナーを使用して StockTicker の有効期間を制御します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="cb8bf-172">また、コンストラクターをパブリックにします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="cb8bf-173">次に、`StockTicker`のインターフェイスを作成してコードをリファクターできます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="cb8bf-174">このインターフェイスを使用して、`StockTicker` クラスの `StockTickerHub` を分離します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="cb8bf-175">この種のリファクタリングは、Visual Studio によって簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="cb8bf-176">StockTicker.cs ファイルを開き、`StockTicker` クラスの宣言を右クリックして、[**リファクター** ...] を選択します。**インターフェイスを抽出**します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="cb8bf-177">**[インターフェイスの抽出]** ダイアログで、 **[すべて選択]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="cb8bf-178">他の既定値はそのままにします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-178">Leave the other defaults.</span></span> <span data-ttu-id="cb8bf-179">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="cb8bf-180">Visual Studio によって `IStockTicker`という名前の新しいインターフェイスが作成され、`IStockTicker`から派生する `StockTicker` も変更されます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="cb8bf-181">IStockTicker.cs ファイルを開き、インターフェイスを**public**に変更します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="cb8bf-182">`StockTickerHub` クラスで、`StockTicker` の2つのインスタンスを `IStockTicker`に変更します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="cb8bf-183">`IStockTicker` インターフェイスの作成は、厳密には必要ありませんが、アプリケーション内のコンポーネント間の結合を減らすために DI がどのように役立つかを説明したいと考えました。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="cb8bf-184">Ninject ライブラリを追加する</span><span class="sxs-lookup"><span data-stu-id="cb8bf-184">Add the Ninject Library</span></span>

<span data-ttu-id="cb8bf-185">.NET 用に多数のオープンソースの IoC コンテナーがあります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="cb8bf-186">このチュートリアルでは、 [Ninject](http://www.ninject.org/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="cb8bf-187">(他の一般的なライブラリには、[城主の Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)、および構造体の[マップ](http://docs.structuremap.net)が含まれています)。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="cb8bf-188">NuGet パッケージマネージャーを使用して、 [Ninject ライブラリ](https://nuget.org/packages/Ninject/3.0.1.10)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="cb8bf-189">Visual Studio で、 **[ツール]** メニューの [ **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="cb8bf-190">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="cb8bf-191">SignalR Dependency Resolver を置き換える</span><span class="sxs-lookup"><span data-stu-id="cb8bf-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="cb8bf-192">SignalR 内で Ninject を使用するには、 **Defaultdependencyresolver**から派生するクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="cb8bf-193">このクラスは、 **Defaultdependencyresolver**の**GetService**メソッドと**getservices**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="cb8bf-194">SignalR は、これらのメソッドを呼び出して、ハブインスタンスを含む、実行時にさまざまなオブジェクトを作成します。また、SignalR によって内部的に使用されるさまざまなサービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="cb8bf-195">**GetService**メソッドは、型の1つのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="cb8bf-196">Ninject カーネルの**Tryget**メソッドを呼び出すには、このメソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="cb8bf-197">このメソッドが null を返す場合は、既定の競合回避モジュールに戻ります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="cb8bf-198">**Getservices**メソッドは、指定された型のオブジェクトのコレクションを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="cb8bf-199">このメソッドをオーバーライドして、Ninject の結果と既定の競合回避モジュールの結果を連結します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="cb8bf-200">Ninject バインドを構成する</span><span class="sxs-lookup"><span data-stu-id="cb8bf-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="cb8bf-201">ここで、Ninject を使用して型バインドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="cb8bf-202">アプリケーションの Startup.cs クラスを開きます (`readme.txt`のパッケージの指示に従って手動で作成したか、プロジェクトに認証を追加することによって作成されたもの)。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="cb8bf-203">`Startup.Configuration` メソッドで、ninject コンテナーを作成します。 Ninject は*カーネル*を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="cb8bf-204">カスタム依存関係競合回避モジュールのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="cb8bf-205">次のように `IStockTicker` のバインドを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="cb8bf-206">このコードは2つのことを言います。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-206">This code is saying two things.</span></span> <span data-ttu-id="cb8bf-207">まず、アプリケーションに `IStockTicker`が必要な場合は常に、カーネルが `StockTicker`のインスタンスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="cb8bf-208">次に、`StockTicker` クラスをシングルトンオブジェクトとして作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="cb8bf-209">Ninject は、オブジェクトのインスタンスを1つ作成し、要求ごとに同じインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="cb8bf-210">次のように、 **IHubConnectionContext**のバインドを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="cb8bf-211">このコードは、 **IHubConnection**を返す匿名関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="cb8bf-212">**WhenInjectedInto**メソッドは、`IStockTicker` のインスタンスを作成するときにのみ、この関数を使用するように ninject を指示します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="cb8bf-213">その理由は、SignalR が**IHubConnectionContext**インスタンスを内部で作成し、SignalR がそれらを作成する方法をオーバーライドしないためです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="cb8bf-214">この関数は、`StockTicker` クラスにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="cb8bf-215">ハブ構成を追加して、依存関係競合回避モジュールを**MapSignalR**メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="cb8bf-216">新しいパラメーターを使用して、サンプルの Startup クラスの ConfigureSignalR メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="cb8bf-217">SignalR では、既定の競合回避モジュールではなく、 **MapSignalR**で指定された競合回避モジュールが使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="cb8bf-218">`Startup.Configuration`の完全なコードリストを次に示します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="cb8bf-219">Visual Studio で StockTicker アプリケーションを実行するには、F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="cb8bf-220">ブラウザーウィンドウで、`http://localhost:*port*/SignalR.Sample/StockTicker.html`に移動します。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="cb8bf-221">アプリケーションの機能は以前とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="cb8bf-222">(説明については、「 [ASP.NET SignalR でのサーバーブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)」を参照してください)。動作は変更されていません。コードを簡単にテスト、保守、および進化させることができました。</span><span class="sxs-lookup"><span data-stu-id="cb8bf-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
