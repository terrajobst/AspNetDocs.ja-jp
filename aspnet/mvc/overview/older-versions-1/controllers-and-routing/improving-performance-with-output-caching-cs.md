---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 出力キャッシュを使用したC#パフォーマンスの向上 () |Microsoft Docs
author: microsoft
description: このチュートリアルでは、出力キャッシュを利用して、ASP.NET MVC web アプリケーションのパフォーマンスを大幅に向上させる方法について説明します。 あなたが。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: 548c5bea2e9cf26e0574e72d2c0ea204dbd90f9c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486670"
---
# <a name="improving-performance-with-output-caching-c"></a><span data-ttu-id="b7943-104">出力キャッシュでパフォーマンスを改善する (C#)</span><span class="sxs-lookup"><span data-stu-id="b7943-104">Improving Performance with Output Caching (C#)</span></span>

<span data-ttu-id="b7943-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b7943-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b7943-106">このチュートリアルでは、出力キャッシュを利用して、ASP.NET MVC web アプリケーションのパフォーマンスを大幅に向上させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b7943-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="b7943-107">新しいユーザーがアクションを呼び出すたびに同じコンテンツを作成する必要がないように、コントローラーアクションから返された結果をキャッシュする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b7943-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="b7943-108">このチュートリアルの目的は、出力キャッシュを利用して、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させる方法について説明することです。</span><span class="sxs-lookup"><span data-stu-id="b7943-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="b7943-109">出力キャッシュを使用すると、コントローラーアクションによって返されるコンテンツをキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="b7943-110">これにより、同じコントローラーアクションが呼び出されるたびに、同じコンテンツを生成する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="b7943-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="b7943-111">たとえば、ASP.NET MVC アプリケーションで、インデックスという名前のビューにデータベースレコードの一覧が表示されているとします。</span><span class="sxs-lookup"><span data-stu-id="b7943-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="b7943-112">通常は、ユーザーがインデックスビューを返すコントローラーアクションを呼び出すたびに、データベースクエリを実行してデータベースからデータベースレコードのセットを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7943-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="b7943-113">一方、出力キャッシュを利用する場合は、ユーザーが同じコントローラーアクションを呼び出すたびに、データベースクエリを実行しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b7943-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="b7943-114">ビューは、コントローラーアクションから再生成されるのではなく、キャッシュから取得できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="b7943-115">キャッシュを使用すると、サーバー上で冗長な作業を実行することを回避できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-115">Caching enables you to avoid performing redundant work on the server.</span></span>

## <a name="enabling-output-caching"></a><span data-ttu-id="b7943-116">出力キャッシュの有効化</span><span class="sxs-lookup"><span data-stu-id="b7943-116">Enabling Output Caching</span></span>

<span data-ttu-id="b7943-117">出力キャッシュを有効にするには、[OutputCache] 属性を個々のコントローラーアクションまたはコントローラークラス全体に追加します。</span><span class="sxs-lookup"><span data-stu-id="b7943-117">You enable output caching by adding an [OutputCache] attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="b7943-118">たとえば、リスト1のコントローラーは、Index () という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="b7943-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="b7943-119">Index () アクションの出力は10秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="b7943-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="b7943-120">**リスト1– Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="b7943-120">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

<span data-ttu-id="b7943-121">ASP.NET MVC のベータ版では、出力キャッシュは[http://www.MySite.com/](http://www.mysite.com/)のような URL に対しては機能しません。</span><span class="sxs-lookup"><span data-stu-id="b7943-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="b7943-122">代わりに、 [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)のような URL を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7943-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span> 

<span data-ttu-id="b7943-123">リスト1では、Index () アクションの出力が10秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="b7943-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="b7943-124">必要に応じて、キャッシュ期間をかなり長く指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="b7943-125">たとえば、1日のコントローラーアクションの出力をキャッシュする場合は、キャッシュ期間として86400秒 (60 秒 \* 60 分 \* 24 時間) を指定できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="b7943-126">指定した時間だけコンテンツがキャッシュされる保証はありません。</span><span class="sxs-lookup"><span data-stu-id="b7943-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="b7943-127">メモリリソースが不足すると、キャッシュによってコンテンツが自動的に再起動されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="b7943-128">リスト1のホームコントローラーは、一覧2のインデックスビューを返します。</span><span class="sxs-lookup"><span data-stu-id="b7943-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="b7943-129">このビューには特別なことはありません。</span><span class="sxs-lookup"><span data-stu-id="b7943-129">There is nothing special about this view.</span></span> <span data-ttu-id="b7943-130">インデックスビューには、現在の時刻が表示されます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="b7943-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="b7943-131">**リスト2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="b7943-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

<span data-ttu-id="b7943-132">**図 1: キャッシュされたインデックスビュー**</span><span class="sxs-lookup"><span data-stu-id="b7943-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

<span data-ttu-id="b7943-134">ブラウザーのアドレスバーに URL/Home/Index を入力し、ブラウザーの [更新]/[再読み込み] ボタンを繰り返し押すことによって Index () アクションを複数回呼び出すと、インデックスビューで表示される時間が10秒間変更されません。</span><span class="sxs-lookup"><span data-stu-id="b7943-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="b7943-135">ビューがキャッシュされているため、同じ時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="b7943-136">アプリケーションにアクセスするすべてのユーザーに対して同じビューがキャッシュされていることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="b7943-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="b7943-137">Index () アクションを呼び出すすべてのユーザーは、同じキャッシュされたバージョンのインデックスビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="b7943-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="b7943-138">これは、インデックスビューを提供するために web サーバーが実行する必要がある作業量が大幅に減少することを意味します。</span><span class="sxs-lookup"><span data-stu-id="b7943-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="b7943-139">リスト2のビューは、非常に単純な処理を実行しています。</span><span class="sxs-lookup"><span data-stu-id="b7943-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="b7943-140">ビューには、現在の時刻だけが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-140">The view just displays the current time.</span></span> <span data-ttu-id="b7943-141">ただし、データベースレコードのセットを表示するビューを簡単にキャッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="b7943-142">その場合は、データベースレコードのセットをデータベースから取得する必要はありません。また、ビューを返すコントローラーアクションが呼び出されるたびにデータベースレコードを取得する必要もありません。</span><span class="sxs-lookup"><span data-stu-id="b7943-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="b7943-143">キャッシュを使用すると、web サーバーとデータベースサーバーの両方で実行する必要がある作業量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="b7943-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="b7943-144">MVC ビューでは、ページ &lt;% @ OutputCache%&gt; ディレクティブは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="b7943-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="b7943-145">このディレクティブは Web フォームからは漏れるため、ASP.NET MVC アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="b7943-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span>

## <a name="where-content-is-cached"></a><span data-ttu-id="b7943-146">コンテンツがキャッシュされる場所</span><span class="sxs-lookup"><span data-stu-id="b7943-146">Where Content is Cached</span></span>

<span data-ttu-id="b7943-147">既定では、[OutputCache] 属性を使用すると、コンテンツは web サーバー、プロキシサーバー、および web ブラウザーの3つの場所にキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="b7943-147">By default, when you use the [OutputCache] attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="b7943-148">[OutputCache] 属性の Location プロパティを変更することで、コンテンツがキャッシュされる場所を正確に制御できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-148">You can control exactly where content is cached by modifying the Location property of the [OutputCache] attribute.</span></span>

<span data-ttu-id="b7943-149">Location プロパティは、次のいずれかの値に設定できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="b7943-150">·いつ</span><span class="sxs-lookup"><span data-stu-id="b7943-150">· Any</span></span>
> 
> <span data-ttu-id="b7943-151">·Client</span><span class="sxs-lookup"><span data-stu-id="b7943-151">· Client</span></span>
> 
> <span data-ttu-id="b7943-152">·ダウンストリーム</span><span class="sxs-lookup"><span data-stu-id="b7943-152">· Downstream</span></span>
> 
> <span data-ttu-id="b7943-153">·Server</span><span class="sxs-lookup"><span data-stu-id="b7943-153">· Server</span></span>
> 
> <span data-ttu-id="b7943-154">·存在</span><span class="sxs-lookup"><span data-stu-id="b7943-154">· None</span></span>
> 
> <span data-ttu-id="b7943-155">·ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="b7943-155">· ServerAndClient</span></span>

<span data-ttu-id="b7943-156">既定では、Location プロパティの値は Any です。</span><span class="sxs-lookup"><span data-stu-id="b7943-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="b7943-157">ただし、ブラウザーだけでキャッシュすることも、サーバー上でのみキャッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="b7943-158">たとえば、ユーザーごとにカスタマイズされた情報をキャッシュする場合は、サーバー上の情報をキャッシュしないようにします。</span><span class="sxs-lookup"><span data-stu-id="b7943-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="b7943-159">ユーザーごとに異なる情報を表示する場合は、クライアントにのみ情報をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7943-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="b7943-160">たとえば、リスト3のコントローラーは、現在のユーザー名を返す、GetName () という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="b7943-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="b7943-161">Jack が web サイトにログインし、GetName () アクションを呼び出す場合、アクションは文字列 "Hi Jack" を返します。</span><span class="sxs-lookup"><span data-stu-id="b7943-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="b7943-162">その後、Jill が web サイトにログインし、GetName () アクションを呼び出すと、文字列 "Hi Jack" も取得されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="b7943-163">文字列は、すべてのユーザーに対して web サーバーにキャッシュされます。これにより、ジャックは最初にコントローラーアクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b7943-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="b7943-164">**リスト3–コントローラー (& c)**</span><span class="sxs-lookup"><span data-stu-id="b7943-164">**Listing 3 – Controllers\BadUserController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

<span data-ttu-id="b7943-165">場合によっては、リスト3のコントローラーが希望どおりに機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="b7943-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="b7943-166">Jill に "Hi Jack" というメッセージは表示しません。</span><span class="sxs-lookup"><span data-stu-id="b7943-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="b7943-167">パーソナライズされたコンテンツをサーバーキャッシュにキャッシュしないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="b7943-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="b7943-168">ただし、パフォーマンスを向上させるために、パーソナライズされたコンテンツをブラウザーキャッシュにキャッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="b7943-169">ブラウザーにコンテンツをキャッシュし、ユーザーが同じコントローラー操作を複数回呼び出す場合は、サーバーではなくブラウザーキャッシュからコンテンツを取得できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="b7943-170">リスト4の変更されたコントローラーは、GetName () アクションの出力をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="b7943-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="b7943-171">ただし、コンテンツは、サーバー上ではなく、ブラウザーにのみキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="b7943-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="b7943-172">このようにして、複数のユーザーが GetName () メソッドを呼び出すと、各ユーザーは別のユーザー名ではなく、自分のユーザー名を取得します。</span><span class="sxs-lookup"><span data-stu-id="b7943-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="b7943-173">**リスト4–コントローラー (& c)**</span><span class="sxs-lookup"><span data-stu-id="b7943-173">**Listing 4 – Controllers\UserController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

<span data-ttu-id="b7943-174">リスト4の [OutputCache] 属性には、"OutputCacheLocation. Client" という値に設定された Location プロパティが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b7943-174">Notice that the [OutputCache] attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="b7943-175">[OutputCache] 属性には、NoStore プロパティも含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7943-175">The [OutputCache] attribute also includes a NoStore property.</span></span> <span data-ttu-id="b7943-176">NoStore プロパティは、キャッシュされたコンテンツの永続的なコピーを格納しないようにプロキシサーバーとブラウザーに通知するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-176">The NoStore property is used to inform proxy servers and browser that they should not store a permanent copy of the cached content.</span></span>

## <a name="varying-the-output-cache"></a><span data-ttu-id="b7943-177">出力キャッシュの変更</span><span class="sxs-lookup"><span data-stu-id="b7943-177">Varying the Output Cache</span></span>

<span data-ttu-id="b7943-178">場合によっては、同じコンテンツの異なるキャッシュバージョンが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="b7943-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="b7943-179">たとえば、マスター/詳細ページを作成しているとします。</span><span class="sxs-lookup"><span data-stu-id="b7943-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="b7943-180">マスターページには、ムービータイトルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="b7943-181">タイトルをクリックすると、選択したムービーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="b7943-182">詳細ページをキャッシュすると、クリックした映画に関係なく、同じムービーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="b7943-183">最初のユーザーが選択した最初のムービーは、今後のすべてのユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="b7943-184">この問題を解決するには、[OutputCache] 属性の VaryByParam プロパティを利用します。</span><span class="sxs-lookup"><span data-stu-id="b7943-184">You can fix this problem by taking advantage of the VaryByParam property of the [OutputCache] attribute.</span></span> <span data-ttu-id="b7943-185">このプロパティを使用すると、フォームパラメーターまたはクエリ文字列パラメーターが異なる場合に、同じコンテンツの異なるキャッシュバージョンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="b7943-186">たとえば、リスト5のコントローラーは、Master () と Details () という名前の2つのアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="b7943-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="b7943-187">マスター () アクションは、映画のタイトルの一覧を返し、Details () アクションは、選択されたムービーの詳細を返します。</span><span class="sxs-lookup"><span data-stu-id="b7943-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="b7943-188">**リスト5– Controllers\MoviesController.cs**</span><span class="sxs-lookup"><span data-stu-id="b7943-188">**Listing 5 – Controllers\MoviesController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

<span data-ttu-id="b7943-189">Master () アクションには、"none" という値を持つ VaryByParam プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7943-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="b7943-190">Master () アクションが呼び出されると、同じキャッシュされたバージョンのマスタービューが返されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="b7943-191">任意のフォームパラメーターまたはクエリ文字列パラメーターは無視されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="b7943-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="b7943-192">**図2–/Movies/Master ビュー**</span><span class="sxs-lookup"><span data-stu-id="b7943-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

<span data-ttu-id="b7943-194">**図3–/Movies/Details ビュー**</span><span class="sxs-lookup"><span data-stu-id="b7943-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

<span data-ttu-id="b7943-196">Details () アクションには、値 "Id" を持つ VaryByParam プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7943-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="b7943-197">Id パラメーターの異なる値がコントローラーアクションに渡されると、詳細ビューの異なるキャッシュバージョンが生成されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="b7943-198">VaryByParam プロパティを使用すると、より多くのキャッシュが得られることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="b7943-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="b7943-199">Id パラメーターの異なるバージョンごとに、異なるキャッシュバージョンの詳細ビューが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="b7943-200">VaryByParam プロパティを次の値に設定できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="b7943-201">\* = フォームまたはクエリ文字列パラメーターが変化するたびに、別のキャッシュされたバージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="b7943-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="b7943-202">none = 異なるキャッシュバージョンを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="b7943-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="b7943-203">パラメーターのセミコロンの一覧 = リスト内のいずれかの形式またはクエリ文字列パラメーターが異なる場合は、キャッシュされた複数のバージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="b7943-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

## <a name="creating-a-cache-profile"></a><span data-ttu-id="b7943-204">キャッシュプロファイルの作成</span><span class="sxs-lookup"><span data-stu-id="b7943-204">Creating a Cache Profile</span></span>

<span data-ttu-id="b7943-205">[OutputCache] 属性のプロパティを変更して出力キャッシュプロパティを構成する代わりに、web 構成 (web.config) ファイルでキャッシュプロファイルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b7943-205">As an alternative to configuring output cache properties by modifying properties of the [OutputCache] attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="b7943-206">Web 構成ファイルでキャッシュプロファイルを作成することには、いくつかの重要な利点があります。</span><span class="sxs-lookup"><span data-stu-id="b7943-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="b7943-207">まず、web 構成ファイルで出力キャッシュを構成することにより、コントローラーアクションがコンテンツを1か所にキャッシュする方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="b7943-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="b7943-208">キャッシュプロファイルを1つ作成し、そのプロファイルを複数のコントローラーまたはコントローラーアクションに適用することができます。</span><span class="sxs-lookup"><span data-stu-id="b7943-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="b7943-209">2つ目は、アプリケーションを再コンパイルせずに、web 構成ファイルを変更する方法です。</span><span class="sxs-lookup"><span data-stu-id="b7943-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="b7943-210">実稼働環境に既に配置されているアプリケーションのキャッシュを無効にする必要がある場合は、web 構成ファイルで定義されているキャッシュプロファイルを変更するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="b7943-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="b7943-211">Web 構成ファイルへの変更は自動的に検出され、適用されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="b7943-212">たとえば、リスト6の &lt;キャッシュ&gt; web 構成セクションには、Cache1Hour という名前のキャッシュプロファイルが定義されています。</span><span class="sxs-lookup"><span data-stu-id="b7943-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="b7943-213">&lt;キャッシュ&gt; セクションは、web 構成ファイルの &lt;system.web&gt; セクション内になければなりません。</span><span class="sxs-lookup"><span data-stu-id="b7943-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="b7943-214">**リスト6– web.config のキャッシュセクション**</span><span class="sxs-lookup"><span data-stu-id="b7943-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

<span data-ttu-id="b7943-215">リスト7のコントローラーは、[OutputCache] 属性を使用してコントローラーアクションに Cache1Hour プロファイルを適用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b7943-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the [OutputCache] attribute.</span></span>

<span data-ttu-id="b7943-216">**リスト7– Controllers\ProfileController.cs**</span><span class="sxs-lookup"><span data-stu-id="b7943-216">**Listing 7 – Controllers\ProfileController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

<span data-ttu-id="b7943-217">リスト7でコントローラーによって公開されている Index () アクションを呼び出すと、1時間は同じ時刻が返されます。</span><span class="sxs-lookup"><span data-stu-id="b7943-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

## <a name="summary"></a><span data-ttu-id="b7943-218">まとめ</span><span class="sxs-lookup"><span data-stu-id="b7943-218">Summary</span></span>

<span data-ttu-id="b7943-219">出力キャッシュは、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させる非常に簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="b7943-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="b7943-220">このチュートリアルでは、[OutputCache] 属性を使用してコントローラーアクションの出力をキャッシュする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b7943-220">In this tutorial, you learned how to use the [OutputCache] attribute to cache the output of controller actions.</span></span> <span data-ttu-id="b7943-221">また、Duration プロパティや VaryByParam プロパティなどの [OutputCache] 属性のプロパティを変更して、コンテンツのキャッシュ方法を変更する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="b7943-221">You also learned how to modify properties of the [OutputCache] attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="b7943-222">最後に、web 構成ファイルでキャッシュプロファイルを定義する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b7943-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b7943-223">[前へ](understanding-action-filters-cs.md)
> [次へ](adding-dynamic-content-to-a-cached-page-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b7943-223">[Previous](understanding-action-filters-cs.md)
[Next](adding-dynamic-content-to-a-cached-page-cs.md)</span></span>
