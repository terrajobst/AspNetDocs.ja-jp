---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR の依存関係挿入 1.x |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117067"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="31c6d-102">SignalR 1.x の依存関係挿入</span><span class="sxs-lookup"><span data-stu-id="31c6d-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="31c6d-103">によって[Mike Wasson](https://github.com/MikeWasson)、 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="31c6d-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="31c6d-104">依存関係の挿入は、簡単になります (モック オブジェクトを使用して) テストのいずれかのオブジェクトの依存関係を置換するか、実行時の動作を変更するオブジェクト間の依存関係をハードコーディングを削除する方法です。</span><span class="sxs-lookup"><span data-stu-id="31c6d-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="31c6d-105">このチュートリアルでは、SignalR ハブの依存関係の挿入を実行する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="31c6d-106">SignalR で IoC コンテナーを使用する方法も示します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="31c6d-107">IoC コンテナーは、依存関係の挿入の一般的なフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="31c6d-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="31c6d-108">依存関係の挿入とは何ですか。</span><span class="sxs-lookup"><span data-stu-id="31c6d-108">What is Dependency Injection?</span></span>

<span data-ttu-id="31c6d-109">依存関係の挿入を理解している場合は、このセクションをスキップします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="31c6d-110">*依存関係の注入*(DI) は、パターン オブジェクトが独自の依存関係の作成を担当します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="31c6d-111">DI を顧客が簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="31c6d-112">メッセージを記録する必要があるオブジェクトがあるとします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="31c6d-113">ログ記録のインターフェイスを定義する場合があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="31c6d-114">オブジェクトを作成できます、`ILogger`メッセージを記録します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="31c6d-115">これは、動作しますが、最適なデザインではありません。</span><span class="sxs-lookup"><span data-stu-id="31c6d-115">This works, but it's not the best design.</span></span> <span data-ttu-id="31c6d-116">置換する場合`FileLogger`別`ILogger`の実装を変更する必要がある`SomeComponent`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="31c6d-117">多くの他のオブジェクトで使用されると`FileLogger`、それらのすべてを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="31c6d-118">作成する場合または`FileLogger`シングルトンもする必要があります、アプリケーション全体での変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="31c6d-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="31c6d-119">「注入」するほうが効果的、`ILogger`オブジェクトに、たとえば、コンス トラクター引数を使用しています。</span><span class="sxs-lookup"><span data-stu-id="31c6d-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="31c6d-120">選択するため、オブジェクトはありませんので`ILogger`を使用します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="31c6d-121">切り替えることができます`ILogger`それに依存するオブジェクトを変更することがなく実装します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="31c6d-122">このパターンと呼ばれます[コンス トラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="31c6d-123">パターンの 1 つは、セッターの挿入、setter メソッドまたはプロパティから依存関係を設定します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="31c6d-124">SignalR で単純な依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="31c6d-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="31c6d-125">チュートリアルのチャット アプリケーションを考えます[SignalR の概要](../getting-started/tutorial-getting-started-with-signalr.md)します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="31c6d-126">そのアプリケーションからハブ クラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="31c6d-127">チャット メッセージを送信する前にサーバーに格納するとします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="31c6d-128">この機能は、抽象化するインターフェイスを定義してにインターフェイスを挿入する DI を使用する場合があります、`ChatHub`クラス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="31c6d-129">唯一の問題は、SignalR アプリケーションがハブ; を直接作成していないことSignalR を作成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="31c6d-130">既定では、SignalR には、パラメーターなしのコンス トラクターを持つハブ クラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="31c6d-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="31c6d-131">ただし、ハブのインスタンスを作成する関数を登録して、この関数を使用して、DI を実行することができます簡単にします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="31c6d-132">関数を呼び出すことによって登録**GlobalHost.DependencyResolver.Register**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="31c6d-133">SignalR は、作成する必要があるたびに、この匿名関数が呼び出すので、`ChatHub`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="31c6d-134">IoC コンテナー</span><span class="sxs-lookup"><span data-stu-id="31c6d-134">IoC Containers</span></span>

<span data-ttu-id="31c6d-135">前のコードは、単純なケースに適してします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="31c6d-136">これを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="31c6d-137">多くの依存関係を持つ複雑なアプリケーションでは、多くの「接続」このコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="31c6d-138">このコードの依存関係が入れ子になった場合に特にハードを維持することはできます。</span><span class="sxs-lookup"><span data-stu-id="31c6d-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="31c6d-139">また、単体テストは困難です。</span><span class="sxs-lookup"><span data-stu-id="31c6d-139">It is also hard to unit test.</span></span>

<span data-ttu-id="31c6d-140">1 つのソリューションでは、IoC コンテナーを使用します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="31c6d-141">IoC コンテナーは、依存関係の管理を担当するソフトウェア コンポーネントです。型、コンテナーを登録し、コンテナーを使用して、オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="31c6d-142">コンテナーは、依存関係を自動的に検出します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="31c6d-143">多くの IoC コンテナーでは、オブジェクトの有効期間とスコープなどを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="31c6d-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="31c6d-144">"IoC"「の制御の反転」の略フレームワークからアプリケーション コードを呼び出す、一般的なパターンは。</span><span class="sxs-lookup"><span data-stu-id="31c6d-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="31c6d-145">IoC コンテナーを構築、オブジェクト、コントロールの通常のフローの「反転」をします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="31c6d-146">SignalR の IoC コンテナーの使用</span><span class="sxs-lookup"><span data-stu-id="31c6d-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="31c6d-147">チャット アプリケーションは、IoC コンテナーのメリットは単純すぎる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="31c6d-148">代わりを見てみましょう、 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)サンプル。</span><span class="sxs-lookup"><span data-stu-id="31c6d-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="31c6d-149">StockTicker サンプルでは、2 つの主要なクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="31c6d-150">`StockTickerHub`:ハブ クラスはクライアント接続を管理します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="31c6d-151">`StockTicker`:株価を保持し、定期的に更新するシングルトン。</span><span class="sxs-lookup"><span data-stu-id="31c6d-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="31c6d-152">`StockTickerHub` 参照を保持、`StockTicker`シングルトン、中に`StockTicker`への参照を保持、 **IHubConnectionContext**の`StockTickerHub`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="31c6d-153">このインターフェイスを使用して通信を`StockTickerHub`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="31c6d-154">(詳細については、次を参照してください[ASP.NET SignalR によるサーバー ブロードキャスト](index.md)。)。</span><span class="sxs-lookup"><span data-stu-id="31c6d-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="31c6d-155">これらの依存関係を少し整理して、IoC コンテナーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="31c6d-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="31c6d-156">まず、少し簡略化し、`StockTickerHub`と`StockTicker`クラス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="31c6d-157">次のコードではコメント部分にしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="31c6d-158">パラメーターなしのコンス トラクターを削除`StockTicker`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="31c6d-159">代わりに、ハブを作成するのに DI を常に使用します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="31c6d-160">StockTicker シングルトン インスタンスを削除します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="31c6d-161">その後、StockTicker 有効期間を制御、IoC コンテナーを使用します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="31c6d-162">パブリック コンス トラクターは、また、ください。</span><span class="sxs-lookup"><span data-stu-id="31c6d-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="31c6d-163">次に、インターフェイスを作成して、コードをリファクタリングできます`StockTicker`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="31c6d-164">このインターフェイスを使用して、分離、`StockTickerHub`から、`StockTicker`クラス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="31c6d-165">Visual Studio でこの種のリファクタリングも簡単。</span><span class="sxs-lookup"><span data-stu-id="31c6d-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="31c6d-166">StockTicker.cs ファイルを開きを右クリックし、`StockTicker`クラス宣言、および選択**リファクタリング**.**インターフェイスの抽出**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="31c6d-167">**インターフェイスの抽出**ダイアログ ボックスで、をクリックして**すべて選択**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="31c6d-168">その他の既定値のままにします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-168">Leave the other defaults.</span></span> <span data-ttu-id="31c6d-169">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="31c6d-170">Visual Studio は、という名前の新しいインターフェイスを作成します。 `IStockTicker`、し、変更も`StockTicker`から派生する`IStockTicker`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="31c6d-171">IStockTicker.cs ファイルを開き、インターフェイスを変更**パブリック**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="31c6d-172">`StockTickerHub`クラス、2 つのインスタンスを変更する`StockTicker`に`IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="31c6d-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="31c6d-173">作成、`IStockTicker`インターフェイスが厳密には必要はありませんが、DI、アプリケーションのコンポーネント間の結合の削減を支援する方法を表示したいです。</span><span class="sxs-lookup"><span data-stu-id="31c6d-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="31c6d-174">Ninject ライブラリを追加します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-174">Add the Ninject Library</span></span>

<span data-ttu-id="31c6d-175">.NET の多くのオープン ソース IoC コンテナーがあります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="31c6d-176">このチュートリアルで使用します[Ninject](http://www.ninject.org/)します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="31c6d-177">(その他の一般的なライブラリを含める[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)、および[StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="31c6d-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="31c6d-178">NuGet パッケージ マネージャーを使用して、インストール、 [Ninject ライブラリ](https://nuget.org/packages/Ninject/3.0.1.10)します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="31c6d-179">Visual Studio から、**ツール**メニューの  **NuGet パッケージ マネージャー** > **パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="31c6d-180">パッケージ マネージャー コンソール ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="31c6d-181">SignalR の依存関係競合回避モジュールを置き換えます</span><span class="sxs-lookup"><span data-stu-id="31c6d-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="31c6d-182">SignalR 内 Ninject を使用するから派生したクラスを作成**DefaultDependencyResolver**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="31c6d-183">このクラスのオーバーライド、 **GetService**と**GetServices**メソッドの**DefaultDependencyResolver**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="31c6d-184">SignalR ハブのインスタンスの SignalR によって内部的に使用されるさまざまなサービスなど、実行時にさまざまなオブジェクトを作成するこれらのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="31c6d-185">**GetService**メソッドは、型の 1 つのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="31c6d-186">このメソッドを呼び出す、Ninject カーネルのオーバーライド**TryGet**メソッド。</span><span class="sxs-lookup"><span data-stu-id="31c6d-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="31c6d-187">そのメソッドが null を返す場合は、既定の競合回避モジュールに戻ります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="31c6d-188">**GetServices**メソッドは、指定した型のオブジェクトのコレクションを作成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="31c6d-189">既定のリゾルバーからの結果には、Ninject からの結果を連結するには、このメソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="31c6d-190">Ninject バインドを構成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="31c6d-191">宣言型バインディングに Ninject を使用します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="31c6d-192">RegisterHubs.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="31c6d-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="31c6d-193">`RegisterHubs.Start`メソッド、Ninject 呼び出す Ninject コンテナーを作成、*カーネル*します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="31c6d-194">このカスタム依存関係競合回避モジュールのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="31c6d-195">バインドを作成`IStockTicker`次のようにします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="31c6d-196">このコードは次の 2 つことを示しています。</span><span class="sxs-lookup"><span data-stu-id="31c6d-196">This code is saying two things.</span></span> <span data-ttu-id="31c6d-197">最初に、アプリケーションに必要なときに、 `IStockTicker`、カーネルがのインスタンスを作成する必要があります`StockTicker`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="31c6d-198">2 番目、`StockTicker`クラスはシングルトン オブジェクトとして作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="31c6d-199">Ninject では、オブジェクトの 1 つのインスタンスを作成し、要求ごとに同じインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="31c6d-200">バインドを作成**IHubConnectionContext**次のようにします。</span><span class="sxs-lookup"><span data-stu-id="31c6d-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="31c6d-201">このコードを返す匿名関数の作成、 **IHubConnection**します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="31c6d-202">**WhenInjectedInto**メソッドに指示を作成するときにのみ、この関数を使用する Ninject`IStockTicker`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="31c6d-203">理由は、SignalR が作成される**IHubConnectionContext**インスタンスを内部的には、SignalR での作成方法をオーバーライドする必要はないです。</span><span class="sxs-lookup"><span data-stu-id="31c6d-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="31c6d-204">この関数にのみ適用されます、`StockTicker`クラス。</span><span class="sxs-lookup"><span data-stu-id="31c6d-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="31c6d-205">依存関係の競合回避モジュールに渡す、 **MapHubs**メソッド。</span><span class="sxs-lookup"><span data-stu-id="31c6d-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="31c6d-206">SignalR がで指定された競合回避モジュールを使用して**MapHubs**既定のリゾルバーではなく。</span><span class="sxs-lookup"><span data-stu-id="31c6d-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="31c6d-207">完全なコードを次に示します`RegisterHubs.Start`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="31c6d-208">Visual Studio で、StockTicker アプリケーションを実行するには、f5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="31c6d-209">ブラウザーのウィンドウでに移動します。`http://localhost:*port*/SignalR.Sample/StockTicker.html`します。</span><span class="sxs-lookup"><span data-stu-id="31c6d-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="31c6d-210">アプリケーションには、正確に前に、のと同じ機能があります。</span><span class="sxs-lookup"><span data-stu-id="31c6d-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="31c6d-211">(詳細については、次を参照してください[ASP.NET SignalR によるサーバー ブロードキャスト](index.md)。)。動作を変更していません。テスト、保守、および進化を簡単にコードを単になりました。</span><span class="sxs-lookup"><span data-stu-id="31c6d-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
