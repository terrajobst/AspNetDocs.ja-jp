---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 効率的なデータページングを実装する |Microsoft Docs
author: microsoft
description: 手順 8. 数千のディナーを一度に表示するのではなく、/Dinners の URL にページングサポートを追加する方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486484"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="a00f7-103">効率的なデータ ページングを実装する</span><span class="sxs-lookup"><span data-stu-id="a00f7-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="a00f7-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a00f7-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="a00f7-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="a00f7-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="a00f7-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順8です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a00f7-107">手順 8. では、/Dinners URL にページングサポートを追加して、ディナーの数千を一度に表示するのではなく、一度に10個のディナーが表示されるようにして、エンドユーザーがリスト全体を反復可能な方法でページバックして前方に移動できるようにする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="a00f7-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a00f7-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="a00f7-109">ステップ 8: ページングのサポート</span><span class="sxs-lookup"><span data-stu-id="a00f7-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="a00f7-110">サイトが正常に実行されると、何千ものディナーがあります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="a00f7-111">これらのすべてのディナーを処理し、ユーザーが参照できるように UI をスケーリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="a00f7-112">これを有効にするには、 */Dinners* URL にページングサポートを追加します。これにより、数千 of ディナーを一度に表示するのではなく、一度に10個のディナーが表示されるようになり、エンドユーザーが SEO のわかりやすい方法でリスト全体をページバックおよび転送できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="a00f7-113">Index () アクションメソッドの要約</span><span class="sxs-lookup"><span data-stu-id="a00f7-113">Index() Action Method Recap</span></span>

<span data-ttu-id="a00f7-114">次のように、Dinのコントローラークラス内の Index () アクションメソッドは、現在は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="a00f7-115">*/Dinners* URL に対して要求が行われると、今後のすべてのディナーの一覧を取得し、すべての一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="a00f7-116">IQueryable&lt;T&gt; について</span><span class="sxs-lookup"><span data-stu-id="a00f7-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="a00f7-117">*IQueryable&lt;t&gt;* は、.net 3.5 の一部として LINQ で導入されたインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="a00f7-118">これにより、ページングサポートを実装するために利用できる強力な "遅延実行" シナリオが可能になります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="a00f7-119">このリポジトリでは、FindUpcomingDinners () メソッドから IQueryable&lt;ディナー&gt; シーケンスを返しています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="a00f7-120">FindUpcomingDinners () メソッドによって返される IQueryable&lt;ディナー&gt; オブジェクトは、LINQ to SQL を使用してデータベースからディナーオブジェクトを取得するクエリをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="a00f7-121">重要なのは、クエリ内のデータに対してアクセスまたは反復処理を試みるか、そのデータに対して ToList () メソッドを呼び出すまで、データベースに対してクエリを実行しないことです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="a00f7-122">FindUpcomingDinners () メソッドを呼び出すコードでは、必要に応じて、クエリを実行する前に、IQueryable&lt;ディナー&gt; オブジェクトに "チェーン" 操作/フィルターを追加することを選択できます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="a00f7-123">その後、データが要求されたときにデータベースに対して結合クエリを実行するのに十分な LINQ to SQL です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="a00f7-124">ページングロジックを実装するには、Din() を呼び出す前に、返された IQueryable&lt;ディナー&gt; シーケンスに追加の "Skip" 演算子と "Take" 演算子を適用するように、dinの Scontroller の Index () アクションメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="a00f7-125">上記のコードは、データベース内の最初の10個のディナーをスキップし、戻り値の20ディナーを返します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="a00f7-126">LINQ to SQL は、web サーバーではなく、SQL database でこのスキップロジックを実行する最適化された SQL クエリを作成するのに十分なスマートです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="a00f7-127">これは、データベースに数百万のディナーがある場合でも、必要な10のみをこの要求の一部として取得することを意味します (効率と拡張性を実現します)。</span><span class="sxs-lookup"><span data-stu-id="a00f7-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="a00f7-128">URL への "ページ" 値の追加</span><span class="sxs-lookup"><span data-stu-id="a00f7-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="a00f7-129">特定のページ範囲をハードコーディングするのではなく、ユーザーが要求しているディナー範囲を示す "page" パラメーターを Url に含めるようにします。</span><span class="sxs-lookup"><span data-stu-id="a00f7-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="a00f7-130">Querystring 値の使用</span><span class="sxs-lookup"><span data-stu-id="a00f7-130">Using a Querystring value</span></span>

<span data-ttu-id="a00f7-131">次のコードは、クエリ文字列パラメーターをサポートする Index () アクションメソッドを更新し、 */Dinners? page = 2*のような url を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="a00f7-132">上記の Index () アクションメソッドには、"page" という名前のパラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="a00f7-133">パラメーターが null 許容の整数として宣言されています (int? はを示します)。</span><span class="sxs-lookup"><span data-stu-id="a00f7-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="a00f7-134">これは、 */Dinners? page = 2* URL によって値 "2" がパラメーター値として渡されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="a00f7-135">*/Dinners* URL (querystring 値なし) を指定すると、null 値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="a00f7-136">ページの値をページサイズ (この場合は10行) で乗算して、スキップするディナーの数を決定します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="a00f7-137">Null 許容型を処理するときに役立つ、 [ C# null の "合体" 演算子 (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)を使用しています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="a00f7-138">ページパラメーターが null の場合、上記のコードによって値0が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="a00f7-139">埋め込み URL 値の使用</span><span class="sxs-lookup"><span data-stu-id="a00f7-139">Using Embedded URL values</span></span>

<span data-ttu-id="a00f7-140">Querystring 値を使用する代わりに、実際の URL 自体にページパラメーターを埋め込むこともできます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="a00f7-141">たとえば、次のよう*になります*(例:// *page/page/* /)。</span><span class="sxs-lookup"><span data-stu-id="a00f7-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="a00f7-142">ASP.NET MVC には、このようなシナリオを簡単にサポートできる強力な URL ルーティングエンジンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="a00f7-143">任意の受信 URL または URL 形式を任意のコントローラークラスまたはアクションメソッドにマップするカスタムルーティング規則を登録できます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="a00f7-144">必要なのは、プロジェクト内で global.asax ファイルを開くことだけです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="a00f7-145">次に、ルートの最初の呼び出しのような MapRoute () ヘルパーメソッドを使用して、新しいマッピング規則を登録します。MapRoute () 以下:</span><span class="sxs-lookup"><span data-stu-id="a00f7-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="a00f7-146">上の例では、"UpcomingDinners" という名前の新しいルーティング規則を登録しています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="a00f7-147">URL 形式が "ディナー/Page/{Page}" であることを示しています。 {Page} は、URL 内に埋め込まれているパラメーター値です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="a00f7-148">MapRoute () メソッドの3番目のパラメーターは、この形式に一致する Url を、Dinの Scontroller クラスの Index () アクションメソッドにマップする必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="a00f7-149">以前に使用したものとまったく同じインデックス () コードをクエリ文字列シナリオで使用できます。ただし、"page" パラメーターは、querystring ではなく URL から取得されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="a00f7-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="a00f7-150">ここで、アプリケーションを実行し、 */Dinners*に「」と入力すると、次のディナーの最初の10が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="a00f7-151">*/Dinners/Page/1*に入力すると、ディナーの次のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="a00f7-152">ページナビゲーション UI の追加</span><span class="sxs-lookup"><span data-stu-id="a00f7-152">Adding page navigation UI</span></span>

<span data-ttu-id="a00f7-153">ページングシナリオを完了するための最後の手順は、ビューテンプレート内に "next" および "previous" ナビゲーション UI を実装して、ユーザーがディナーデータを簡単にスキップできるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="a00f7-154">これを正しく実装するには、データベースのディナーの合計数と、このが変換されるデータのページ数を把握しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="a00f7-155">次に、現在要求されている "ページ" 値がデータの先頭または末尾にあるかどうかを計算し、それに従って "previous" と "next" UI を表示または非表示にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="a00f7-156">このロジックは、Index () アクションメソッド内に実装できます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="a00f7-157">または、このロジックを再利用可能な方法でカプセル化するヘルパークラスをプロジェクトに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="a00f7-158">次に示すのは、.NET Framework に組み込まれている&lt;T&gt; コレクションクラスのリストから派生する単純な "PaginatedList" ヘルパークラスです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="a00f7-159">再利用可能なコレクションクラスを実装しています。このクラスを使用すると、IQueryable データの任意のシーケンスに改ページすることができます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="a00f7-160">この例では、IQueryable&lt;ディナー&gt; の結果を処理していますが、その他のアプリケーションシナリオでは、IQueryable&lt;製品&gt; または IQueryable&lt;の結果に簡単に使用できます。&gt;</span><span class="sxs-lookup"><span data-stu-id="a00f7-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="a00f7-161">"PageIndex"、"PageSize"、"TotalCount"、"TotalPages" などのプロパティがどのように計算され、公開されるかに注目してください。</span><span class="sxs-lookup"><span data-stu-id="a00f7-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="a00f7-162">さらに、コレクション内のデータのページが元のシーケンスの先頭または末尾にあるかどうかを示す、2つのヘルパープロパティ "HasPreviousPage" と "HasNextPage" を公開します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="a00f7-163">上記のコードでは、2つの SQL クエリが実行されます。1つ目は、1つは整数を返す "SELECT COUNT" ステートメントを実行し、もう1つはオブジェクトを返さず、次の行だけを取得するためです。データの現在のページについて、データベースから必要なデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="a00f7-164">次に、DinPaginatedList () ヘルパーメソッドを更新して、FindUpcomingDinners () 結果から&lt;ディナー&gt; を作成し、ビューテンプレートに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="a00f7-165">次に、\Views\Dinners\Index.aspx view テンプレートを更新して&lt;ViewPage&lt;IEnumerable&lt;ディナー&gt;&gt;ではなく PaginatedList&lt;ディナー&gt;&gt; を継承し、次のコードをビューテンプレートの下部に追加して、次のナビゲーション UI と前のナビゲーション UI を表示または非表示にすることができます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="a00f7-166">この記事では、Html の Teltelink () ヘルパーメソッドを使用してハイパーリンクを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="a00f7-167">このメソッドは、以前に使用した Html.actionlink () ヘルパーメソッドに似ています。</span><span class="sxs-lookup"><span data-stu-id="a00f7-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="a00f7-168">違いは、global.asax ファイル内で設定する "UpcomingDinners" ルーティング規則を使用して URL を生成していることです。</span><span class="sxs-lookup"><span data-stu-id="a00f7-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="a00f7-169">これにより *、次の*形式の Index () アクションメソッドへの url が生成されます。 {Page} の値は、現在の PageIndex に基づいて前に指定した変数です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="a00f7-170">アプリケーションをもう一度実行すると、ブラウザーに10のディナーが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="a00f7-171">また、ページの下部にある &lt;&lt; と &gt;の &gt;&gt; ナビゲーション UI も &lt;します。これにより、検索エンジンのアクセス可能な Url を使用してデータの転送と逆方向のスキップを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a00f7-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="a00f7-172">**サイドトピック: IQueryable&lt;T&gt; の影響について**</span><span class="sxs-lookup"><span data-stu-id="a00f7-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="a00f7-173">IQueryable&lt;T&gt; は、さまざまな興味深い実行シナリオ (ページングやコンポジションベースのクエリなど) を可能にする非常に強力な機能です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="a00f7-174">すべての強力な機能と同様に、使用方法について慎重に検討し、悪用されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="a00f7-175">リポジトリから IQueryable&lt;T&gt; 結果を返すことにより、呼び出し元のコードがチェーン演算子メソッドに追加され、最終的なクエリの実行に参加することを認識することが重要です。</span><span class="sxs-lookup"><span data-stu-id="a00f7-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="a00f7-176">この機能の呼び出しコードを指定しない場合は、既に実行されているクエリの結果を含む IList&lt;T&gt; または IEnumerable&lt;T&gt; 結果を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="a00f7-177">改ページのシナリオでは、実際のデータ改ページロジックを、呼び出されるリポジトリメソッドにプッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a00f7-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="a00f7-178">このシナリオでは、FindUpcomingDinners () finder メソッドを更新して、PaginatedList を返したシグネチャを取得することがあります。 PaginatedList&lt; ディナー&gt; FindUpcomingDinners (int pageIndex, int pageSize) {} を返すか、IList&lt;ディナー&gt;を返し、"totalCount" out パラメーターを使用してディナー: IList&lt;ディナー&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) {} の合計数を返します。</span><span class="sxs-lookup"><span data-stu-id="a00f7-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="a00f7-179">次の手順</span><span class="sxs-lookup"><span data-stu-id="a00f7-179">Next Step</span></span>

<span data-ttu-id="a00f7-180">次に、認証と承認のサポートをアプリケーションに追加する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="a00f7-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a00f7-181">[前へ](re-use-ui-using-master-pages-and-partials.md)
> [次へ](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="a00f7-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
