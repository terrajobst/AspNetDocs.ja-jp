---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: キャッシュされたページに動的コンテンツを追加する (VB) |Microsoft Docs
author: microsoft
description: 動的コンテンツとキャッシュされたコンテンツを同じページに混在させる方法について説明します。 キャッシュ後の置換では、バナー広告などの動的なコンテンツを表示できます...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f2f4372498e5a38bbfcb96d6e9f6338b0ef4df1f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486964"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a><span data-ttu-id="2d77b-104">キャッシュされたページに動的コンテンツを追加する (VB)</span><span class="sxs-lookup"><span data-stu-id="2d77b-104">Adding Dynamic Content to a Cached Page (VB)</span></span>

<span data-ttu-id="2d77b-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2d77b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2d77b-106">動的コンテンツとキャッシュされたコンテンツを同じページに混在させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="2d77b-107">キャッシュ後の置換を使用すると、出力がキャッシュされているページ内に、バナー広告やニュース項目などの動的コンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="2d77b-108">出力キャッシュを利用することで、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="2d77b-109">ページを毎回再生成するのではなく、ページが要求されるたびに、ページを生成し、複数のユーザーのメモリにキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="2d77b-110">しかし、問題があります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-110">But there is a problem.</span></span> <span data-ttu-id="2d77b-111">動的なコンテンツをページに表示する必要がある場合はどうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="2d77b-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="2d77b-112">たとえば、ページにバナー広告を表示する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="2d77b-113">すべてのユーザーに同じ提供情報が表示されるように、バナー広告がキャッシュされないようにします。</span><span class="sxs-lookup"><span data-stu-id="2d77b-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="2d77b-114">そのようなことはできません。</span><span class="sxs-lookup"><span data-stu-id="2d77b-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="2d77b-115">幸いにも、簡単な解決策があります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="2d77b-116">*キャッシュ後の置換*と呼ばれる ASP.NET フレームワークの機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="2d77b-117">キャッシュ後の置換を使用すると、メモリにキャッシュされているページの動的コンテンツを置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="2d77b-118">通常、&lt;OutputCache&gt; 属性を使用してページのキャッシュを出力すると、サーバーとクライアント (web ブラウザー) の両方にページがキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-118">Normally, when you output cache a page by using the &lt;OutputCache&gt; attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="2d77b-119">キャッシュ後の置換を使用する場合、ページはサーバーにのみキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="2d77b-120">キャッシュ後の置換の使用</span><span class="sxs-lookup"><span data-stu-id="2d77b-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="2d77b-121">キャッシュ後の置換を使用するには、2つの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="2d77b-122">まず、キャッシュされたページに表示する動的コンテンツを表す文字列を返すメソッドを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="2d77b-123">次に、Httpresponse.cache () メソッドを呼び出して、動的なコンテンツをページに挿入します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="2d77b-124">たとえば、キャッシュされたページで異なるニュースアイテムをランダムに表示する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="2d77b-125">リスト1のクラスは、RenderNews () という1つのメソッドを公開します。このメソッドは、3つのニュース項目のリストから1つのニュース項目をランダムに返します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="2d77b-126">**リスト1– Models\News.vb**</span><span class="sxs-lookup"><span data-stu-id="2d77b-126">**Listing 1 – Models\News.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

<span data-ttu-id="2d77b-127">キャッシュ後の置換を利用するには、WriteSubstitution () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="2d77b-128">WriteSubstitution () メソッドは、キャッシュされたページの領域を動的なコンテンツに置き換えるようにコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="2d77b-129">WriteSubstitution () メソッドを使用して、リスト2のビューにランダムなニュース項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="2d77b-130">**リスト2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="2d77b-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

<span data-ttu-id="2d77b-131">RenderNews メソッドは、WriteSubstitution () メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="2d77b-132">RenderNews メソッドは呼び出されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2d77b-132">Notice that the RenderNews method is not called.</span></span> <span data-ttu-id="2d77b-133">代わりに、メソッドへの参照は、AddressOf 演算子を使用して WriteSubstitution () に渡されます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-133">Instead a reference to the method is passed to WriteSubstitution() with the help of the AddressOf operator.</span></span>

<span data-ttu-id="2d77b-134">インデックスビューがキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-134">The Index view is cached.</span></span> <span data-ttu-id="2d77b-135">ビューは、リスト3のコントローラーによって返されます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="2d77b-136">Index () アクションが &lt;OutputCache&gt; 属性で修飾され、インデックスビューが60秒間キャッシュされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2d77b-136">Notice that the Index() action is decorated with an &lt;OutputCache&gt; attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="2d77b-137">**リスト3– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="2d77b-137">**Listing 3 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

<span data-ttu-id="2d77b-138">インデックスビューがキャッシュされている場合でも、インデックスページを要求すると、異なるランダムニュース項目が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="2d77b-139">インデックスページを要求すると、ページに表示される時間は60秒間は変わりません (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="2d77b-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="2d77b-140">時間が変更されないという事実は、ページがキャッシュされていることを証明します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="2d77b-141">ただし、WriteSubstitution () メソッドによって挿入されたコンテンツ (ランダムニュース項目) は、要求ごとに変化します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="2d77b-142">**図 1: キャッシュされたページに動的なニュース項目を挿入する**</span><span class="sxs-lookup"><span data-stu-id="2d77b-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="2d77b-144">ヘルパーメソッドでのキャッシュ後の置換の使用</span><span class="sxs-lookup"><span data-stu-id="2d77b-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="2d77b-145">キャッシュ後の置換を利用する簡単な方法は、カスタムヘルパーメソッド内で WriteSubstitution () メソッドの呼び出しをカプセル化することです。</span><span class="sxs-lookup"><span data-stu-id="2d77b-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="2d77b-146">この方法は、リスト4のヘルパーメソッドによって示されています。</span><span class="sxs-lookup"><span data-stu-id="2d77b-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="2d77b-147">**リスト4– & # 3.**</span><span class="sxs-lookup"><span data-stu-id="2d77b-147">**Listing 4 – Helpers\AdHelper.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

<span data-ttu-id="2d77b-148">リスト4には、RenderBanner () と RenderBannerInternal () という2つのメソッドを公開する Visual Basic モジュールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2d77b-148">Listing 4 contains a Visual Basic module that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="2d77b-149">RenderBanner () メソッドは、実際のヘルパーメソッドを表します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="2d77b-150">このメソッドは、標準の ASP.NET MVC HtmlHelper クラスを拡張します。これにより、他のヘルパーメソッドと同様に、ビューで Html の RenderBanner () を呼び出すことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="2d77b-151">RenderBanner () メソッドは、RenderBannerInternal () メソッドを WriteSubstitution () メソッドに渡して、WriteSubstitution () メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="2d77b-152">RenderBannerInternal () メソッドはプライベートメソッドです。</span><span class="sxs-lookup"><span data-stu-id="2d77b-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="2d77b-153">このメソッドは、ヘルパーメソッドとして公開されません。</span><span class="sxs-lookup"><span data-stu-id="2d77b-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="2d77b-154">RenderBannerInternal () メソッドは、3つのバナー広告画像のリストから、1つのバナー広告画像をランダムに返します。</span><span class="sxs-lookup"><span data-stu-id="2d77b-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="2d77b-155">リスト5の変更されたインデックスビューは、RenderBanner () ヘルパーメソッドを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2d77b-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="2d77b-156">MvcApplication1 名前空間をインポートするために、ビューの先頭に追加の &lt;% @ Import%&gt; ディレクティブが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2d77b-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="2d77b-157">この名前空間のインポートを怠ると、RenderBanner () メソッドが Html プロパティのメソッドとして表示されません。</span><span class="sxs-lookup"><span data-stu-id="2d77b-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="2d77b-158">**リスト5– Views\Home\Index.aspx (RenderBanner () メソッドを使用)**</span><span class="sxs-lookup"><span data-stu-id="2d77b-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

<span data-ttu-id="2d77b-159">リスト5のビューによって表示されるページを要求すると、要求ごとに異なるバナー広告が表示されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="2d77b-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="2d77b-160">ページはキャッシュされますが、バナー広告は RenderBanner () ヘルパーメソッドによって動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="2d77b-161">**図2–ランダムなバナー広告を表示するインデックスビュー**</span><span class="sxs-lookup"><span data-stu-id="2d77b-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="2d77b-163">まとめ</span><span class="sxs-lookup"><span data-stu-id="2d77b-163">Summary</span></span>

<span data-ttu-id="2d77b-164">このチュートリアルでは、キャッシュされたページのコンテンツを動的に更新する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="2d77b-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="2d77b-165">Httpresponse.cache () メソッドを使用して、キャッシュされたページに動的コンテンツを挿入できるようにする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="2d77b-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="2d77b-166">また、HTML ヘルパーメソッド内で WriteSubstitution () メソッドの呼び出しをカプセル化する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="2d77b-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="2d77b-167">可能な限りキャッシュを利用する– web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2d77b-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="2d77b-168">このチュートリアルで説明するように、動的なコンテンツをページに表示する必要がある場合でも、キャッシュを利用できます。</span><span class="sxs-lookup"><span data-stu-id="2d77b-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2d77b-169">[前へ](improving-performance-with-output-caching-vb.md)
> [次へ](creating-a-controller-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2d77b-169">[Previous](improving-performance-with-output-caching-vb.md)
[Next](creating-a-controller-vb.md)</span></span>
