---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依存関係の注入 |Microsoft Docs
author: rick-anderson
description: '注: このハンズオンラボでは、ASP.NET MVC と ASP.NET MVC 4 のフィルターに関する基本的な知識があることを前提としています。 前に ASP.NET MVC 4 フィルターを使用していない場合は、...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451822"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="4ddda-104">ASP.NET MVC 4 依存関係挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="4ddda-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="4ddda-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4ddda-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="4ddda-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4ddda-107">このハンズオンラボでは、 **ASP.NET mvc**と**ASP.NET mvc 4 フィルター**に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="4ddda-108">前に**ASP.NET mvc 4 フィルター**を使用していない場合は、 **ASP.NET Mvc カスタムアクションフィルター**のハンズオンラボに進むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-109">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4ddda-110">このラボに固有のプロジェクトは、 [ASP.NET MVC 4 依存関係の挿入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="4ddda-111">**オブジェクト指向プログラミング**パラダイムでは、オブジェクトは共同作成者とコンシューマーが存在するコラボレーションモデルで連携します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="4ddda-112">当然ながら、この通信モデルでは、オブジェクトとコンポーネント間の依存関係が生成されるため、複雑さが増加しても管理が困難になります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="4ddda-113">![クラスの依存関係とモデルの複雑さ](aspnet-mvc-4-dependency-injection/_static/image1.png "クラスの依存関係とモデルの複雑さ")</span><span class="sxs-lookup"><span data-stu-id="4ddda-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="4ddda-114">*クラスの依存関係とモデルの複雑さ*</span><span class="sxs-lookup"><span data-stu-id="4ddda-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="4ddda-115">多くの場合、**ファクトリパターン**と、サービスを使用したインターフェイスと実装の分離について耳にします。クライアントオブジェクトは、サービスの場所を担当します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="4ddda-116">依存関係の注入パターンは、制御の反転の特定の実装です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="4ddda-117">**制御の反転 (IoC)** は、オブジェクトがその他のオブジェクトを作成せずに作業に依存することを意味します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="4ddda-118">代わりに、外部ソース (xml 構成ファイルなど) から必要なオブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="4ddda-119">**依存関係の挿入 (DI)** は、オブジェクトの介入なしに実行されることを意味します。通常は、コンストラクターのパラメーターを渡し、プロパティを設定するフレームワークコンポーネントによって行われます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="4ddda-120">依存関係の挿入 (DI) デザインパターン</span><span class="sxs-lookup"><span data-stu-id="4ddda-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="4ddda-121">大まかに言えば、依存関係の注入の目的は、クライアントクラス (*ゴルファー*など) がインターフェイスを満たすもの ( *iclub*など) を必要とすることです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="4ddda-122">具象型 (例: *WoodClub、IronClub、WedgeClub* 、または*putterclub*) は考慮されません。他のユーザーがそれを処理するようにします (たとえば、適切な*caddy*)。</span><span class="sxs-lookup"><span data-stu-id="4ddda-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="4ddda-123">ASP.NET MVC の依存関係競合回避モジュールを使用すると、他の場所 (コンテナーや*クラブのバッグ*など) に依存関係ロジックを登録できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="4ddda-124">![依存関係の挿入の図](aspnet-mvc-4-dependency-injection/_static/image2.png "依存関係の挿入の図")</span><span class="sxs-lookup"><span data-stu-id="4ddda-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="4ddda-125">*依存関係の挿入-ゴルフの例え*</span><span class="sxs-lookup"><span data-stu-id="4ddda-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="4ddda-126">依存関係の挿入パターンと制御の反転を使用する利点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="4ddda-127">クラスの結合を減らす</span><span class="sxs-lookup"><span data-stu-id="4ddda-127">Reduces class coupling</span></span>
- <span data-ttu-id="4ddda-128">コードの再利用を増やす</span><span class="sxs-lookup"><span data-stu-id="4ddda-128">Increases code reusing</span></span>
- <span data-ttu-id="4ddda-129">コードの保守性を向上させる</span><span class="sxs-lookup"><span data-stu-id="4ddda-129">Improves code maintainability</span></span>
- <span data-ttu-id="4ddda-130">アプリケーションテストの向上</span><span class="sxs-lookup"><span data-stu-id="4ddda-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-131">依存関係の挿入は、抽象ファクトリデザインパターンと比較されることがありますが、両方の方法にわずかな違いがあります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="4ddda-132">DI には、ファクトリと登録済みサービスを呼び出すことによって依存関係を解決するためのフレームワークが用意されています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="4ddda-133">依存関係の挿入パターンについて理解したところで、このラボ全体を通じて ASP.NET MVC 4 で適用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="4ddda-134">**コントローラー**で依存関係の挿入を使用して、データベースアクセスサービスを含めることを開始します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="4ddda-135">次に、サービスを使用して情報を表示するために、依存関係の挿入を**ビュー**に適用します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="4ddda-136">最後に、DI を ASP.NET MVC 4 フィルターに拡張し、ソリューションにカスタムアクションフィルターを挿入します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="4ddda-137">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="4ddda-138">NuGet パッケージを使用して依存関係の挿入を行うために ASP.NET MVC 4 と Unity を統合する</span><span class="sxs-lookup"><span data-stu-id="4ddda-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="4ddda-139">ASP.NET MVC コントローラー内での依存関係の挿入の使用</span><span class="sxs-lookup"><span data-stu-id="4ddda-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="4ddda-140">ASP.NET MVC ビュー内での依存関係の挿入の使用</span><span class="sxs-lookup"><span data-stu-id="4ddda-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="4ddda-141">ASP.NET MVC アクションフィルター内での依存関係の挿入の使用</span><span class="sxs-lookup"><span data-stu-id="4ddda-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-142">このラボでは、依存関係の解決に Mvc3 NuGet パッケージを使用していますが、ASP.NET MVC 4 で動作するように依存関係挿入フレームワークを調整することもできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4ddda-143">前提条件</span><span class="sxs-lookup"><span data-stu-id="4ddda-143">Prerequisites</span></span>

<span data-ttu-id="4ddda-144">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4ddda-145">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="4ddda-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4ddda-146">セットアップ</span><span class="sxs-lookup"><span data-stu-id="4ddda-146">Setup</span></span>

<span data-ttu-id="4ddda-147">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="4ddda-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="4ddda-148">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4ddda-149">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4ddda-150">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 B: コードスニペット](#AppendixB)&quot;の使用」 &quot;参照してください。</span><span class="sxs-lookup"><span data-stu-id="4ddda-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4ddda-151">手順</span><span class="sxs-lookup"><span data-stu-id="4ddda-151">Exercises</span></span>

<span data-ttu-id="4ddda-152">このハンズオンラボは、次の演習によって構成されています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="4ddda-153">演習 1: コントローラーの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="4ddda-154">演習 2: ビューの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="4ddda-155">演習 3: フィルターの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="4ddda-156">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4ddda-157">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="4ddda-158">このラボの推定所要時間: **30 分**。</span><span class="sxs-lookup"><span data-stu-id="4ddda-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="4ddda-159">演習 1: コントローラーの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="4ddda-160">この演習では、NuGet パッケージを使用して Unity を統合することによって、ASP.NET MVC コントローラーで依存関係の挿入を使用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="4ddda-161">そのため、データアクセスからロジックを分離するために、MvcMusicStore コントローラーにサービスを含めます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="4ddda-162">サービスは、コントローラーコンストラクターに新しい依存関係を作成します。これは、 **Unity**のヘルプを使用して依存関係の挿入を使用して解決されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="4ddda-163">このアプローチでは、より柔軟性が高く、保守とテストが容易な、結合の少ないアプリケーションを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="4ddda-164">また、ASP.NET MVC と Unity を統合する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="4ddda-165">StoreManager サービスについて</span><span class="sxs-lookup"><span data-stu-id="4ddda-165">About StoreManager Service</span></span>

<span data-ttu-id="4ddda-166">Begin ソリューションで提供される MVC ミュージックストアには、 **Storeservice**という名前のストアコントローラーデータを管理するサービスが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="4ddda-167">以下では、ストアサービスの実装について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="4ddda-168">すべてのメソッドがモデルエンティティを返すことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4ddda-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="4ddda-169">Begin ソリューションの**StoreController**が**storeservice**を使用するようになりました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="4ddda-170">すべてのデータ参照が**StoreController**から削除され、 **storeservice**を使用するメソッドを変更せずに現在のデータアクセスプロバイダーを変更できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="4ddda-171">**StoreController**実装には、クラスコンストラクター内で**storeservice**との依存関係があることがわかります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-172">この演習で導入された依存関係は、**制御の反転**(IoC) に関連しています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="4ddda-173">**StoreController**クラスコンストラクターは、 **istoreservice**型パラメーターを受け取ります。これは、クラス内からのサービス呼び出しを実行するために不可欠です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="4ddda-174">ただし、 **StoreController**は、コントローラーが ASP.NET MVC を操作するために必要な既定のコンストラクター (パラメーターなし) を実装していません。</span><span class="sxs-lookup"><span data-stu-id="4ddda-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="4ddda-175">依存関係を解決するには、抽象ファクトリ (指定された型のオブジェクトを返すクラス) によってコントローラーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="4ddda-176">宣言されたパラメーターなしのコンストラクターがないため、クラスがサービスオブジェクトを送信せずに StoreController を作成しようとすると、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="4ddda-177">タスク 1-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="4ddda-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="4ddda-178">このタスクでは、Begin アプリケーションを実行します。このアプリケーションでは、アプリケーションロジックからデータアクセスを分離するストアコントローラーにサービスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="4ddda-179">アプリケーションを実行すると、既定ではコントローラーサービスがパラメーターとして渡されないため、例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="4ddda-180">**ソース \ Ex01-の挿入 Controller\Begin**にある**Begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="4ddda-181">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4ddda-182">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4ddda-183">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4ddda-184">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4ddda-185">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4ddda-186">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4ddda-187">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4ddda-188">Ctrl キーを押し**ながら F5**キーを押して、デバッグを行わずにアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="4ddda-189">**このオブジェクト&quot;にパラメーターなしのコンストラクターが定義されていない**&quot;エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="4ddda-190">![ASP.NET MVC Begin Application の実行中にエラーが発生しました](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC Begin Application の実行中にエラーが発生しました")</span><span class="sxs-lookup"><span data-stu-id="4ddda-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="4ddda-191">*ASP.NET MVC Begin Application の実行中にエラーが発生しました*</span><span class="sxs-lookup"><span data-stu-id="4ddda-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="4ddda-192">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-192">Close the browser.</span></span>

<span data-ttu-id="4ddda-193">次の手順では、このコントローラーが必要とする依存関係を挿入するミュージックストアソリューションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="4ddda-194">タスク 2-Unity を MvcMusicStore ソリューションに含める</span><span class="sxs-lookup"><span data-stu-id="4ddda-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="4ddda-195">このタスクでは、 **Mvc3** NuGet パッケージをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-196">Mvc3 パッケージは ASP.NET MVC 3 向けに設計されていますが、ASP.NET MVC 4 と完全に互換性があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="4ddda-197">Unity は、拡張可能な軽量の依存関係挿入コンテナーであり、オプションでインスタンスと型のインターセプトをサポートします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="4ddda-198">これは、あらゆる種類の .NET アプリケーションで使用するための汎用コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="4ddda-199">オブジェクトの作成、実行時の依存関係の指定による要件の抽象化、コンポーネントの構成をコンテナーに延期することによって、依存関係の注入メカニズムに含まれる共通の機能をすべて提供します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="4ddda-200">**MvcMusicStore**プロジェクトに**Mvc3** NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="4ddda-201">これを行うには、[**他のウィンドウ** | **表示**] から**パッケージマネージャーコンソール**を開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="4ddda-202">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-202">Run the following command.</span></span>

    <span data-ttu-id="4ddda-203">PMC</span><span class="sxs-lookup"><span data-stu-id="4ddda-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="4ddda-204">![Mvc3 NuGet パッケージをインストールしています](aspnet-mvc-4-dependency-injection/_static/image4.png "Mvc3 NuGet パッケージをインストールしています")</span><span class="sxs-lookup"><span data-stu-id="4ddda-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="4ddda-205">*Mvc3 NuGet パッケージをインストールしています*</span><span class="sxs-lookup"><span data-stu-id="4ddda-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="4ddda-206">Unity の構成を簡略化するために、 **Mvc3**パッケージがインストールされたら、自動的に追加されるファイルとフォルダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="4ddda-207">![インストールされている Mvc3 パッケージ](aspnet-mvc-4-dependency-injection/_static/image5.png "インストールされている Mvc3 パッケージ")</span><span class="sxs-lookup"><span data-stu-id="4ddda-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="4ddda-208">*インストールされている Mvc3 パッケージ*</span><span class="sxs-lookup"><span data-stu-id="4ddda-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="4ddda-209">タスク 3-Global.asax.cs アプリケーションへの Unity の登録\_開始</span><span class="sxs-lookup"><span data-stu-id="4ddda-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="4ddda-210">このタスクでは、 **Global.asax.cs**にある**アプリケーション\_開始**メソッドを更新して Unity ブートストラップ初期化子を呼び出し、依存関係の挿入に使用するサービスとコントローラーを登録するブートストラップファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="4ddda-211">次に、Unity コンテナーと依存関係競合回避モジュールを初期化するファイルであるブートストラップをフックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="4ddda-212">これを行うには、 **Global.asax.cs**を開き、次の強調表示されたコードを**Application\_Start**メソッド内に追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="4ddda-213">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-Initialize Unity*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="4ddda-214">**Bootstrapper.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="4ddda-215">**MvcMusicStore**と**MusicStore**の各名前空間を含めます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="4ddda-216">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-ブートストラップ名前空間の追加*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="4ddda-217">**Buildunitycontainer**メソッドの内容を、ストアコントローラーとストアサービスを登録する次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="4ddda-218">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-Register Store Controller And Service*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4ddda-219">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="4ddda-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="4ddda-220">このタスクでは、アプリケーションを実行して、Unity をインクルードした後でアプリケーションを読み込むことができることを確認します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="4ddda-221">**F5**キーを押してアプリケーションを実行すると、エラーメッセージを表示せずにアプリケーションが読み込まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="4ddda-222">![依存関係の挿入を使用したアプリケーションの実行](aspnet-mvc-4-dependency-injection/_static/image6.png "依存関係の挿入を使用したアプリケーションの実行")</span><span class="sxs-lookup"><span data-stu-id="4ddda-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="4ddda-223">*依存関係の挿入を使用したアプリケーションの実行*</span><span class="sxs-lookup"><span data-stu-id="4ddda-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="4ddda-224">**/ストア**に移動します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-224">Browse to **/Store**.</span></span> <span data-ttu-id="4ddda-225">これにより、 **Unity**を使用して作成された**StoreController**が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="4ddda-226">![MVC ミュージックストア](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC ミュージックストア")</span><span class="sxs-lookup"><span data-stu-id="4ddda-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="4ddda-227">*MVC ミュージックストア*</span><span class="sxs-lookup"><span data-stu-id="4ddda-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="4ddda-228">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-228">Close the browser.</span></span>

<span data-ttu-id="4ddda-229">次の演習では、ASP.NET MVC ビューおよびアクションフィルター内で使用するように依存関係挿入スコープを拡張する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="4ddda-230">演習 2: ビューの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="4ddda-231">この演習では、ASP.NET MVC 4 for Unity 統合の新機能を使用して、ビューで依存関係の挿入を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="4ddda-232">そのためには、ストアの参照ビュー内でカスタムサービスを呼び出します。これにより、次のメッセージと画像が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="4ddda-233">次に、プロジェクトを Unity と統合し、カスタム依存関係競合回避モジュールを作成して依存関係を挿入します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="4ddda-234">タスク 1-サービスを使用するビューの作成</span><span class="sxs-lookup"><span data-stu-id="4ddda-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="4ddda-235">このタスクでは、サービス呼び出しを実行して新しい依存関係を生成するビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="4ddda-236">このサービスは、このソリューションに含まれる単純なメッセージングサービスで構成されています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="4ddda-237">**Sourceex02-挿入 View\ begin**フォルダーにある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="4ddda-238">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4ddda-239">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4ddda-240">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4ddda-241">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4ddda-242">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4ddda-243">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4ddda-244">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4ddda-245">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4ddda-246">詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4ddda-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4ddda-247">**ソース \ Assets**フォルダーにある**MessageService.cs**クラスと**IMessageService.cs**クラスを **/Services**に含めます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="4ddda-248">これを行うには、 **[サービス]** フォルダーを右クリックし、 **[既存項目の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="4ddda-249">ファイルの場所を参照して指定します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="4ddda-250">![メッセージサービスとサービスインターフェイスの追加](aspnet-mvc-4-dependency-injection/_static/image8.png "メッセージサービスとサービスインターフェイスの追加")</span><span class="sxs-lookup"><span data-stu-id="4ddda-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="4ddda-251">*メッセージサービスとサービスインターフェイスの追加*</span><span class="sxs-lookup"><span data-stu-id="4ddda-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ddda-252">**IMessageService**インターフェイスは、 **messageservice**クラスによって実装される2つのプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="4ddda-253">これらのプロパティ-**メッセージ**と**ImageUrl**-メッセージと、表示されるイメージの URL を格納します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="4ddda-254">プロジェクトのルートフォルダーにフォルダー **/ページ**を作成し、 **MyBasePage.cs**の既存のクラスを追加し**ます。**</span><span class="sxs-lookup"><span data-stu-id="4ddda-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="4ddda-255">継承元の基本ページの構造は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="4ddda-256">![ページフォルダー](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages フォルダー")</span><span class="sxs-lookup"><span data-stu-id="4ddda-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="4ddda-257">/ビュー/**ストア**フォルダーから**Browse**ビューを開き、 **MyBasePage.cs**から継承されるようにします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="4ddda-258">**参照**ビューで、 **messageservice**の呼び出しを追加して、イメージとサービスによって取得されたメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="4ddda-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="4ddda-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="4ddda-260">タスク 2-カスタム依存関係競合回避モジュールとカスタムビューページアクティベーターを含む</span><span class="sxs-lookup"><span data-stu-id="4ddda-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="4ddda-261">前のタスクでは、ビュー内に新しい依存関係を挿入し、その中でサービス呼び出しを実行していました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="4ddda-262">次に、ASP.NET MVC 依存関係挿入インターフェイス**Iviewpageactivator**と**idependencyresolver**を実装することで、その依存関係を解決します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="4ddda-263">Unity を使用したサービスの取得を処理する**Idependencyresolver**の実装は、ソリューションに含めます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="4ddda-264">次に、ビューの作成を解決する**Iviewpageactivator**インターフェイスの別のカスタム実装を追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="4ddda-265">ASP.NET MVC 3 以降、依存関係の挿入の実装により、サービスを登録するためのインターフェイスが簡略化されました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="4ddda-266">**Idependencyresolver**と**Iviewpageactivator**は、依存関係の挿入のための ASP.NET MVC 3 機能の一部です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="4ddda-267">**-Idependencyresolver**インターフェイスは、前の IMvcServiceLocator を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="4ddda-268">IDependencyResolver の実装は、サービスまたはサービスコレクションのインスタンスを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="4ddda-269">**-Iviewpageactivator**インターフェイスを使用すると、依存関係の挿入によってビューページをインスタンス化する方法をより細かく制御できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="4ddda-270">**Iviewpageactivator**インターフェイスを実装するクラスは、コンテキスト情報を使用してビューインスタンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="4ddda-271">プロジェクトのルートフォルダーに/**factory**フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="4ddda-272">**/Sources/Assets/** to **factory**フォルダーからソリューションに**CustomViewPageActivator.cs**を追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="4ddda-273">これを行うには、 **/工場** フォルダーを右クリックし、追加 を選択します。 **既存の項目** をクリックし、**CustomViewPageActivator.cs** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="4ddda-274">このクラスは、Unity コンテナーを保持する**Iviewpageactivator**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ddda-275">**Customviewpageactivator**は、Unity コンテナーを使用してビューの作成を管理する役割を担います。</span><span class="sxs-lookup"><span data-stu-id="4ddda-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="4ddda-276">**UnityDependencyResolver.cs** **ファイルをインクルードフォルダーに追加** **します**。</span><span class="sxs-lookup"><span data-stu-id="4ddda-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="4ddda-277">これを行うには、 **/工場** フォルダーを右クリックし、追加 を選択します。 **既存の項目** をクリックし、**UnityDependencyResolver.cs** file を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ddda-278">**Unitydependencyresolver**クラスは、Unity のカスタム dependencyresolver です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="4ddda-279">Unity コンテナー内にサービスが見つからない場合、基本競合回避モジュールは invocated です。</span><span class="sxs-lookup"><span data-stu-id="4ddda-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="4ddda-280">次のタスクでは、両方の実装が登録され、モデルでサービスとビューの場所を把握できるようになります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="4ddda-281">タスク 3-Unity コンテナー内での依存関係の挿入の登録</span><span class="sxs-lookup"><span data-stu-id="4ddda-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="4ddda-282">このタスクでは、依存関係の挿入を行うために、前のすべての項目をまとめます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="4ddda-283">現在、ソリューションには次の要素があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="4ddda-284">**MyBaseClass**から継承し、 **messageservice**を使用する**参照**ビュー。</span><span class="sxs-lookup"><span data-stu-id="4ddda-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="4ddda-285">サービスインターフェイスに対して依存関係の挿入が宣言されている中間クラス**MyBaseClass**。</span><span class="sxs-lookup"><span data-stu-id="4ddda-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="4ddda-286">サービス**Messageservice**とそのインターフェイス**IMessageService**。</span><span class="sxs-lookup"><span data-stu-id="4ddda-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="4ddda-287">サービスの取得を処理する Unity- **Unitydependencyresolver**のカスタム依存関係競合回避モジュール。</span><span class="sxs-lookup"><span data-stu-id="4ddda-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="4ddda-288">ページを作成するビューページアクティベーター- **Customviewpageactivator** 。</span><span class="sxs-lookup"><span data-stu-id="4ddda-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="4ddda-289">**参照**ビューを挿入するには、Unity コンテナーにカスタム依存関係競合回避モジュールを登録します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="4ddda-290">**Bootstrapper.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="4ddda-291">サービスを初期化するために、 **Messageservice**のインスタンスを Unity コンテナーに登録します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="4ddda-292">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Register Message Service*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="4ddda-293">**MvcMusicStore**名前空間への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="4ddda-294">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02 名前空間*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="4ddda-295">**Customviewpageactivator**をビューページアクティベーターとして Unity コンテナーに登録します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="4ddda-296">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Register CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="4ddda-297">ASP.NET MVC 4 の既定の依存関係競合回避モジュールを**Unitydependencyresolver**のインスタンスに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="4ddda-298">これを行うには、 **Initialize**メソッドの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="4ddda-299">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Update Dependency Resolver*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ddda-300">ASP.NET MVC には、既定の依存関係リゾルバークラスが用意されています。</span><span class="sxs-lookup"><span data-stu-id="4ddda-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="4ddda-301">Unity 用に作成したものとしてカスタム依存関係競合回避モジュールを使用するには、このリゾルバーを置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4ddda-302">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="4ddda-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="4ddda-303">このタスクでは、アプリケーションを実行して、ストアブラウザーがサービスを使用し、取得したイメージとメッセージが表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="4ddda-304">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4ddda-305">ジャンル メニュー内の **ロック** をクリックし、 **messageservice**がビューに挿入され、ウェルカムメッセージと画像が読み込まれたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="4ddda-306">この例では、を入力して、**ロック**&quot;を &quot;します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="4ddda-307">![MVC ミュージックストア-ビューの挿入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC ミュージックストア-ビューの挿入")</span><span class="sxs-lookup"><span data-stu-id="4ddda-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="4ddda-308">*MVC ミュージックストア-ビューの挿入*</span><span class="sxs-lookup"><span data-stu-id="4ddda-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="4ddda-309">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="4ddda-310">演習 3: アクションフィルターの挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="4ddda-311">前のハンズオンラボの**カスタムアクションフィルター**では、フィルターのカスタマイズと挿入が使用されていました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="4ddda-312">この演習では、Unity コンテナーを使用して依存関係の挿入を含むフィルターを挿入する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="4ddda-313">これを行うには、サイトのアクティビティをトレースするカスタムアクションフィルターをミュージックストアソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="4ddda-314">タスク 1-ソリューション内の追跡フィルターを含む</span><span class="sxs-lookup"><span data-stu-id="4ddda-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="4ddda-315">このタスクでは、[ミュージックストアにカスタムアクションフィルターを追加してイベントをトレースする] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="4ddda-316">カスタムアクションフィルターの概念は、前のラボで既に処理されています。カスタムアクションフィルター&quot;&quot;、このラボの Assets フォルダーからフィルタークラスを追加し、Unity のフィルタープロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="4ddda-317">**ソース \ ex03-挿入アクション filter¥ begin**フォルダーにある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="4ddda-318">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4ddda-319">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4ddda-320">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4ddda-321">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4ddda-322">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4ddda-323">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="4ddda-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4ddda-324">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4ddda-325">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4ddda-326">詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4ddda-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4ddda-327">**TraceActionFilter.cs** **ファイルをインクルードフォルダーに追加** **します**。</span><span class="sxs-lookup"><span data-stu-id="4ddda-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ddda-328">このカスタムアクションフィルターは、ASP.NET のトレースを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="4ddda-329">詳細については、&quot;ASP.NET MVC 4 のローカルアクションフィルターと動的アクションフィルター&quot; ラボを確認してください。</span><span class="sxs-lookup"><span data-stu-id="4ddda-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="4ddda-330">空のクラス**FilterProvider.cs** **をフォルダー内**のプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="4ddda-331">FilterProvider.cs 名前**空間と、** **その名前**空間をに追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="4ddda-332">(コードスニペット- *ASP.NET 依存関係挿入ラボ-Ex03 プロバイダーの名前空間の追加*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="4ddda-333">クラスが**Ifilterprovider**インターフェイスから継承されるようにします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="4ddda-334">**Filterprovider**クラスに**Iunitycontainer**プロパティを追加し、コンテナーを割り当てるクラスコンストラクターを作成します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="4ddda-335">(コードスニペット- *ASP.NET Dependency インジェクション Ex03-Filter Provider コンストラクター*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ddda-336">フィルタープロバイダークラスコンストラクターが、内に**新しい**オブジェクトを作成していません。</span><span class="sxs-lookup"><span data-stu-id="4ddda-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="4ddda-337">コンテナーはパラメーターとして渡され、その依存関係は Unity によって解決されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="4ddda-338">**Filterprovider**クラスで、 **ifilterprovider**インターフェイスから**getfilters**メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="4ddda-339">(コードスニペット- *ASP.NET Dependency インジェクション Ex03-Filter Provider GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="4ddda-340">タスク 2-フィルターの登録と有効化</span><span class="sxs-lookup"><span data-stu-id="4ddda-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="4ddda-341">このタスクでは、サイトの追跡を有効にします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="4ddda-342">これを行うには、 **Bootstrapper.cs BuildUnityContainer**メソッドにフィルターを登録して、トレースを開始します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="4ddda-343">プロジェクトルートに**ある web.config を開き、** system.web グループでトレース追跡を有効にします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="4ddda-344">プロジェクトルートで**Bootstrapper.cs**を開きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="4ddda-345">**MvcMusicStore**名前空間への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="4ddda-346">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex03-ブートストラップ名前空間の追加*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="4ddda-347">**Buildunitycontainer**メソッドを選択し、Unity コンテナーにフィルターを登録します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="4ddda-348">フィルタープロバイダーとアクションフィルターを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="4ddda-349">(コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex03-Register FilterProvider And ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="4ddda-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4ddda-350">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="4ddda-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="4ddda-351">このタスクでは、アプリケーションを実行し、カスタムアクションフィルターがアクティビティをトレースしていることをテストします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="4ddda-352">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4ddda-353">ジャンル メニュー内の **ロック** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="4ddda-354">必要に応じて、より多くのジャンルを参照できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="4ddda-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span><span class="sxs-lookup"><span data-stu-id="4ddda-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="4ddda-356">*Music Store*</span><span class="sxs-lookup"><span data-stu-id="4ddda-356">*Music Store*</span></span>
3. <span data-ttu-id="4ddda-357">[アプリケーショントレース] ページを参照して選択し、[**詳細の表示** **] をクリック**します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="4ddda-358">![アプリケーショントレースログ](aspnet-mvc-4-dependency-injection/_static/image12.png "アプリケーショントレースログ")</span><span class="sxs-lookup"><span data-stu-id="4ddda-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="4ddda-359">*アプリケーショントレースログ*</span><span class="sxs-lookup"><span data-stu-id="4ddda-359">*Application Trace Log*</span></span>

    <span data-ttu-id="4ddda-360">![アプリケーショントレース-要求の詳細](aspnet-mvc-4-dependency-injection/_static/image13.png "アプリケーショントレース-要求の詳細")</span><span class="sxs-lookup"><span data-stu-id="4ddda-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="4ddda-361">*アプリケーショントレース-要求の詳細*</span><span class="sxs-lookup"><span data-stu-id="4ddda-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="4ddda-362">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4ddda-363">まとめ</span><span class="sxs-lookup"><span data-stu-id="4ddda-363">Summary</span></span>

<span data-ttu-id="4ddda-364">このハンズオンラボを完了すると、NuGet パッケージを使用して Unity を統合することで、ASP.NET MVC 4 で依存関係の挿入を使用する方法を学習できました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="4ddda-365">これを実現するには、コントローラー、ビュー、およびアクションフィルター内で依存関係の挿入を使用しました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="4ddda-366">次の概念について説明しました。</span><span class="sxs-lookup"><span data-stu-id="4ddda-366">The following concepts were covered:</span></span>

- <span data-ttu-id="4ddda-367">ASP.NET MVC 4 依存関係挿入機能</span><span class="sxs-lookup"><span data-stu-id="4ddda-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="4ddda-368">Unity の Mvc3 NuGet パッケージを使用した統合</span><span class="sxs-lookup"><span data-stu-id="4ddda-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="4ddda-369">コントローラーでの依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="4ddda-370">ビューでの依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="4ddda-371">アクションフィルターの依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="4ddda-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4ddda-372">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="4ddda-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4ddda-373">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4ddda-374">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4ddda-375">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4ddda-376">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4ddda-377">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-377">Click on **Install Now**.</span></span> <span data-ttu-id="4ddda-378">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4ddda-379">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4ddda-380">![Visual Studio Express のインストール](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="4ddda-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4ddda-381">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="4ddda-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4ddda-382">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="4ddda-384">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="4ddda-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4ddda-385">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-385">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="4ddda-387">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="4ddda-387">*Installation progress*</span></span>
6. <span data-ttu-id="4ddda-388">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-388">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="4ddda-390">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="4ddda-390">*Installation completed*</span></span>
7. <span data-ttu-id="4ddda-391">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4ddda-392">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="4ddda-394">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="4ddda-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="4ddda-395">付録 B: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="4ddda-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="4ddda-396">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4ddda-397">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="4ddda-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4ddda-398">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="4ddda-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4ddda-399">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="4ddda-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4ddda-400">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="4ddda-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4ddda-401">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4ddda-402">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4ddda-403">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4ddda-404">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="4ddda-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4ddda-405">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="4ddda-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4ddda-406">![スニペット名の入力を開始します](aspnet-mvc-4-dependency-injection/_static/image20.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="4ddda-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4ddda-407">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="4ddda-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="4ddda-408">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="4ddda-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4ddda-409">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="4ddda-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4ddda-410">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-dependency-injection/_static/image22.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="4ddda-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4ddda-411">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="4ddda-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4ddda-412">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="4ddda-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4ddda-413">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="4ddda-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4ddda-414">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4ddda-415">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="4ddda-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4ddda-416">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-dependency-injection/_static/image23.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="4ddda-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4ddda-417">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="4ddda-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4ddda-418">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-dependency-injection/_static/image24.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="4ddda-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4ddda-419">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="4ddda-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
