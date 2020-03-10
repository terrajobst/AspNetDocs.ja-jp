---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: Details メソッドと Delete メソッドの検証 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 37787a26f37473b9d36792a9f7715982cb274074
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485314"
---
# <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="662bf-104">Details メソッドと Delete メソッドの確認</span><span class="sxs-lookup"><span data-stu-id="662bf-104">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="662bf-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="662bf-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="662bf-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="662bf-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="662bf-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="662bf-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="662bf-108">チュートリアルのこの部分では、自動的に生成された `Details` と `Delete` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="662bf-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="662bf-109">Details メソッドと Delete メソッドの確認</span><span class="sxs-lookup"><span data-stu-id="662bf-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="662bf-110">`Movie` コントローラーを開き、`Details` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="662bf-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="662bf-111">このアクションメソッドを作成した MVC スキャフォールディングエンジンは、メソッドを呼び出す HTTP 要求を示すコメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="662bf-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="662bf-112">この例では、3つの URL セグメント、`Movies` コントローラー、`Details` メソッド、および `ID` 値を含む `GET` 要求です。</span><span class="sxs-lookup"><span data-stu-id="662bf-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="662bf-113">Code First により、`Find` メソッドを使用してデータを簡単に検索できます。</span><span class="sxs-lookup"><span data-stu-id="662bf-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="662bf-114">メソッドに組み込まれている重要なセキュリティ機能として、コードがコードで何かを実行しようとする前に、`Find` メソッドがムービーを検出したことを検証することが挙げられます。</span><span class="sxs-lookup"><span data-stu-id="662bf-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="662bf-115">たとえば、ハッカーは、リンクによって作成された URL を `http://localhost:xxxx/Movies/Details/1` から `http://localhost:xxxx/Movies/Details/12345` (または実際のムービーを表さない他の値) に変更することによって、サイトにエラーを持ち込む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="662bf-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="662bf-116">Null ムービーを確認しなかった場合、null ムービーはデータベースエラーになります。</span><span class="sxs-lookup"><span data-stu-id="662bf-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="662bf-117">`Delete` メソッドと `DeleteConfirmed` メソッドを調べます。</span><span class="sxs-lookup"><span data-stu-id="662bf-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="662bf-118">`HTTP Get``Delete` メソッドは、指定されたムービーを削除せず、削除を送信 (`HttpPost`) できるムービーのビューを返します。</span><span class="sxs-lookup"><span data-stu-id="662bf-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="662bf-119">GET 要求の応答で削除操作を実行すると (さらに言えば、編集操作、作成操作、データを変更するその他のあらゆる操作を実行すると)、セキュリティに穴が空きます。</span><span class="sxs-lookup"><span data-stu-id="662bf-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="662bf-120">詳細については、「Stephen Walther's blog entry ASP.NET MVC Tip #46」を参照してください。[削除リンクは、セキュリティホールを作成するため、使用しないで](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)ください。</span><span class="sxs-lookup"><span data-stu-id="662bf-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="662bf-121">データを削除する `HttpPost` メソッドの名前は「`DeleteConfirmed`」になり、HTTP POST メソッドに一意のシグネチャまたは名前が与えられます。</span><span class="sxs-lookup"><span data-stu-id="662bf-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="662bf-122">2 つのメソッド シグネチャは下の画像のようになります。</span><span class="sxs-lookup"><span data-stu-id="662bf-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="662bf-123">共通言語ランタイム (CLR) は、オーバーロードのメソッドに一意のパラメーター シグネチャを持つことを要求します (メソッド名は同じであるが、パラメーターの一覧が異なる)。</span><span class="sxs-lookup"><span data-stu-id="662bf-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="662bf-124">ただし、ここでは2つの Delete メソッドが必要です。1つは GET、もう1つは同じパラメーターシグネチャを持ちます。</span><span class="sxs-lookup"><span data-stu-id="662bf-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="662bf-125">(いずれも、1 つの整数をパラメーターとして受け取る必要があります。)</span><span class="sxs-lookup"><span data-stu-id="662bf-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="662bf-126">これを並べ替えるために、いくつかのことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="662bf-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="662bf-127">1つは、メソッドに異なる名前を付けることです。</span><span class="sxs-lookup"><span data-stu-id="662bf-127">One is to give the methods different names.</span></span> <span data-ttu-id="662bf-128">先の例では、スキャフォールディング メカニズムがこれを行いました。</span><span class="sxs-lookup"><span data-stu-id="662bf-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="662bf-129">ただし、これは小さな問題を引き起こします。ASP.NET が URL のセグメントをアクション メソッドに名前でマッピングします。メソッドの名前を変更すると、通常、ルーティングでそのメソッドが見つからなくなります。</span><span class="sxs-lookup"><span data-stu-id="662bf-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="662bf-130">この解決策はこの例で確認できます。`ActionName("Delete")` 属性を `DeleteConfirmed` メソッドに追加しています。</span><span class="sxs-lookup"><span data-stu-id="662bf-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="662bf-131">これにより、ルーティングシステムのマッピングが効果的に実行されるため、POST 要求の<em>/Delete/</em>が含まれている URL が `DeleteConfirmed` メソッドを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="662bf-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="662bf-132">同じ名前とシグネチャを持つメソッドの問題を回避するもう1つの一般的な方法は、POST メソッドのシグネチャを意図的に変更して、未使用のパラメーターを含めることです。</span><span class="sxs-lookup"><span data-stu-id="662bf-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="662bf-133">たとえば、一部の開発者は、POST メソッドに渡される `FormCollection` パラメーター型を追加し、パラメーターを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="662bf-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="662bf-134">まとめ</span><span class="sxs-lookup"><span data-stu-id="662bf-134">Summary</span></span>

<span data-ttu-id="662bf-135">これで、ローカル DB データベースにデータを格納する完全な ASP.NET MVC アプリケーションが完成しました。</span><span class="sxs-lookup"><span data-stu-id="662bf-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="662bf-136">ムービーの作成、読み取り、更新、削除、検索を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="662bf-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="662bf-137">次の手順</span><span class="sxs-lookup"><span data-stu-id="662bf-137">Next Steps</span></span>

<span data-ttu-id="662bf-138">Web アプリケーションをビルドしてテストしたら、次の手順として、インターネット経由で他のユーザーが使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="662bf-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="662bf-139">これを行うには、それを web ホスティングプロバイダーに展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="662bf-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="662bf-140">Microsoft では、無料の[Windows Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で最大10個の web サイトを無料で提供しています。</span><span class="sxs-lookup"><span data-stu-id="662bf-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="662bf-141">次に、 [「メンバーシップ、OAuth、および SQL Database を使用する Secure ASP.NET MVC アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する」をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="662bf-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="662bf-142">優れたチュートリアルとして、Tom Dykstra の中間レベルで、 [ASP.NET MVC アプリケーションの Entity Framework データモデルを作成して](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)います。</span><span class="sxs-lookup"><span data-stu-id="662bf-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="662bf-143">[Stackoverflow](http://stackoverflow.com/help)と[ASP.NET MVC フォーラム](https://forums.asp.net/1146.aspx)は、質問をする絶好の場所です。</span><span class="sxs-lookup"><span data-stu-id="662bf-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="662bf-144">最新[のチュートリアル](https://twitter.com/RickAndMSFT)で更新プログラムを入手できるように、twitter でフォローします。</span><span class="sxs-lookup"><span data-stu-id="662bf-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="662bf-145">フィードバックは歓迎します。</span><span class="sxs-lookup"><span data-stu-id="662bf-145">Feedback is welcome.</span></span>

<span data-ttu-id="662bf-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="662bf-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="662bf-147">— [Scott マン Selman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="662bf-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="662bf-148">[[戻る]](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="662bf-148">[Previous](adding-validation-to-the-model.md)</span></span>
