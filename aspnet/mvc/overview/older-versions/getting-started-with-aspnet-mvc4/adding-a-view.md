---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: ビューを追加する |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457636"
---
# <a name="adding-a-view"></a><span data-ttu-id="7aaf8-104">ビューの追加</span><span class="sxs-lookup"><span data-stu-id="7aaf8-104">Adding a View</span></span>

<span data-ttu-id="7aaf8-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7aaf8-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="7aaf8-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="7aaf8-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="7aaf8-108">このセクションでは、`HelloWorldController` クラスを変更して、ビューテンプレートファイルを使用して、クライアントに HTML 応答を生成するプロセスを完全にカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="7aaf8-109">ASP.NET MVC 3 で導入された[Razor ビューエンジン](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)を使用して、ビューテンプレートファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="7aaf8-110">Razor ベースのビューテンプレートには、ファイル拡張子が*cshtml*と、を使用してC#HTML 出力を作成するための洗練された方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="7aaf8-111">Razor では、ビューテンプレートを記述するときに必要な文字数とキーストロークの数が最小限に抑えられ、滑らかなコーディングワークフローが可能になります。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="7aaf8-112">現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="7aaf8-113">次のコードに示すように、`View` オブジェクトを返すように `Index` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="7aaf8-114">上記の `Index` メソッドでは、ビューテンプレートを使用してブラウザーへの HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="7aaf8-115">上の `Index` メソッドなどのコントローラーメソッド ([アクションメソッド](http://rachelappel.com/asp.net-mvc-actionresults-explained)とも呼ばれます) は、通常、文字列のようなプリミティブ型ではなく、 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (または[actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)から派生したクラス) を返します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="7aaf8-116">プロジェクトで、`Index` メソッドで使用できるビューテンプレートを追加します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="7aaf8-117">これを行うには、`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="7aaf8-118">**[ビューの追加]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="7aaf8-119">既定値のままにして、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="7aaf8-120">*MvcMovie\Views\HelloWorld*フォルダーと*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="7aaf8-121">**ソリューションエクスプローラー**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="7aaf8-122">作成された*インデックスの cshtml*ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="7aaf8-124">`<h2>` タグの下に次の HTML を追加します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="7aaf8-125">完全な*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="7aaf8-126">Visual Studio 2012 を使用している場合は、ソリューションエクスプローラーで、 *Index. cshtml*ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="7aaf8-128">この新しいツールの詳細については、 [Page Inspector チュートリアル](../../views/using-page-inspector-in-aspnet-mvc.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="7aaf8-129">または、アプリケーションを実行し、`HelloWorld` コントローラー (`http://localhost:xxxx/HelloWorld`) を参照します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="7aaf8-130">コントローラーの `Index` メソッドでは、多くの作業が行われませんでした。単にステートメント `return View()`を実行しました。これは、メソッドがビューテンプレートファイルを使用してブラウザーに応答を表示する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="7aaf8-131">使用するビューテンプレートファイルの名前を明示的に指定していないので、ASP.NET MVC では、\Views\HelloWorld フォルダー内のファイルを使用するように既定で設定されてい*ます。*</span><span class="sxs-lookup"><span data-stu-id="7aaf8-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="7aaf8-132">次の画像は、ビューテンプレートから Hello &quot;文字列を示しています。&quot;、ビューにハードコーディングされています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="7aaf8-133">すばらしいですね。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-133">Looks pretty good.</span></span> <span data-ttu-id="7aaf8-134">ただし、ブラウザーのタイトルバーに &quot;Index My ASP.NET A&quot; が表示され、ページの上部にある大きなリンクには、ここでロゴの &quot;が示されています。ロゴ &quot;の下に&quot; ます。&quot; リンクは [登録] リンクと [ログイン] リンクです。 [ホーム]、[About]、[Contact] ページにリンクしています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="7aaf8-135">これらのいくつかを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="7aaf8-136">ビューおよびレイアウトページの変更</span><span class="sxs-lookup"><span data-stu-id="7aaf8-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="7aaf8-137">まず、ロゴ &quot;をここで変更します。ページの上部にあるタイトルを&quot; ます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="7aaf8-138">このテキストは、すべてのページに共通です。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-138">That text is common to every page.</span></span> <span data-ttu-id="7aaf8-139">実際には、アプリケーション内のすべてのページに表示される場合でも、プロジェクト内の1つの場所にのみ実装されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="7aaf8-140">**ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、 *\_Layout*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="7aaf8-141">このファイルは*レイアウトページ*と呼ばれ、他のすべてのページで使用される共有 &quot;シェル&quot; です。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="7aaf8-143">レイアウトテンプレートを使用すると、サイトの HTML コンテナーレイアウトを1か所で指定し、サイト内の複数のページに適用できます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="7aaf8-144">`@RenderBody()` という行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="7aaf8-145">`RenderBody` は、作成したビュー固有のページがすべて表示されるプレースホルダーで、レイアウト ページに&quot;ラップ&quot;されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="7aaf8-146">たとえば、About リンクを選択すると、`RenderBody` メソッド内に*Views\Home\About.cshtml*ビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="7aaf8-147">レイアウト テンプレートの サイトタイトル 見出しは、ここにあるロゴ &quot;から、MVC Movie&quot;&quot;&quot; に変更します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="7aaf8-148">Title 要素の内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="7aaf8-149">アプリケーションを実行し、[MVC Movie &quot;&quot;] と表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="7aaf8-150">**[About]** リンクをクリックすると、そのページに MVC ムービー&quot;の &quot;が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="7aaf8-151">レイアウトテンプレートで変更を1回行って、サイトのすべてのページに新しいタイトルを反映させることができました。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="7aaf8-152">次に、インデックスビューのタイトルを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="7aaf8-153">*MvcMovie\Views\HelloWorld\Index.cshtml*を開きます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="7aaf8-154">2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、2番目のヘッダー (`<h2>` 要素) の順に移動します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="7aaf8-155">これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="7aaf8-156">表示する HTML タイトルを示すために、上記のコードでは `ViewBag` オブジェクトの `Title` プロパティを設定しています (これは、*インデックスの cshtml*ビューテンプレートに含まれています)。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="7aaf8-157">レイアウトテンプレートのソースコードを確認すると、テンプレートは、以前に変更した HTML の `<head>` セクションの一部として、`<title>` 要素内のこの値を使用していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="7aaf8-158">この `ViewBag` アプローチを使用すると、ビューテンプレートとレイアウトファイルの間で、他のパラメーターを簡単に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="7aaf8-159">アプリケーションを実行し、`http://localhost:xx/HelloWorld`を参照します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="7aaf8-160">ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください</span><span class="sxs-lookup"><span data-stu-id="7aaf8-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="7aaf8-161">(ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="7aaf8-162">ブラウザーで Ctrl キーを押しながら F5 キーを押して、サーバーからの応答を強制的に読み込みます。)ブラウザーのタイトルは、 *Index. cshtml* view テンプレートで設定した `ViewBag.Title` で作成され、追加の &quot;ムービーアプリ&quot; レイアウトファイルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="7aaf8-163">また、*インデックスの cshtml*ビューテンプレートの内容が *\_のレイアウト*にマージされ、1つの HTML 応答がブラウザーに送信されたことにも注目してください。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="7aaf8-164">レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="7aaf8-165">ほとんどの &quot;データ&quot; (この場合は、ビューテンプレート!&quot; message から Hello &quot;) がハードコーディングされています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="7aaf8-166">MVC アプリケーションには &quot;V&quot; (ビュー) があり、&quot;C&quot; (コントローラー) がありますが、&quot;M&quot; (モデル) はまだありません。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="7aaf8-167">ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="7aaf8-168">コントローラーからビューへのデータの受け渡し</span><span class="sxs-lookup"><span data-stu-id="7aaf8-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="7aaf8-169">データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="7aaf8-170">コントローラークラスは、受信 URL 要求に応答して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="7aaf8-171">コントローラークラスは、入力方向のブラウザー要求を処理し、データベースからデータを取得し、最終的にブラウザーに返す応答の種類を決定するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="7aaf8-172">これで、ビューテンプレートをコントローラーから使用して、ブラウザーに HTML 応答を生成して書式設定することができます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="7aaf8-173">コントローラーは、ビューテンプレートがブラウザーに応答を表示するために必要なすべてのデータまたはオブジェクトを提供する役割を担います。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="7aaf8-174">ベストプラクティス:**ビューテンプレートでは、ビジネスロジックを実行したり、データベースを直接操作したりしないで**ください。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="7aaf8-175">代わりに、ビューテンプレートは、コントローラーによって提供されるデータでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="7aaf8-176">この &quot;、問題の分離を維持することにより、コードをクリーンで、テストしやすく、保守しやすくなり&quot; ます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="7aaf8-177">現時点では、`HelloWorldController` クラスの `Welcome` アクションメソッドは `name` と `numTimes` パラメーターを受け取り、ブラウザーに値を直接出力します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="7aaf8-178">コントローラーがこの応答を文字列として表示するのではなく、ビューテンプレートを使用するようにコントローラーを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="7aaf8-179">このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="7aaf8-180">これを行うには、ビューテンプレートで必要とされる動的データ (パラメーター) をコントローラーに配置し、ビューテンプレートがアクセスできるように `ViewBag` オブジェクト内に表示します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="7aaf8-181">*HelloWorldController.cs*ファイルに戻り、`Welcome` メソッドを変更して、`ViewBag` オブジェクトに `Message` と `NumTimes` の値を追加します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="7aaf8-182">`ViewBag` は動的なオブジェクトであるため、任意のものを自由に配置できます。`ViewBag` オブジェクトには、その中に何かを配置するまで、定義されたプロパティはありません。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="7aaf8-183">[ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)は、アドレスバーのクエリ文字列からメソッドのパラメーターに、名前付きパラメーター (`name` と `numTimes`) を自動的にマップします。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="7aaf8-184">完全な *HelloWorldController.cs* ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="7aaf8-185">現在、`ViewBag` オブジェクトには、ビューに自動的に渡されるデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="7aaf8-186">次に、ウェルカムビューテンプレートが必要です。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="7aaf8-187">**[ビルド]** メニューの **[Mvcmovie のビルド]** を選択して、プロジェクトがコンパイルされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="7aaf8-188">次に、`Welcome` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="7aaf8-189">**[ビューの追加]** ダイアログボックスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="7aaf8-190">**[追加]** をクリックし、新しい*Welcome. cshtml*ファイルの `<h2>` 要素の下に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="7aaf8-191">ユーザーが指定した回数だけ &quot;Hello&quot; というループを作成します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="7aaf8-192">次に、完全な*Welcome*ファイルを示します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="7aaf8-193">アプリケーションを実行し、次の URL を参照します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="7aaf8-194">これで、データは URL から取得され、[モデルバインダー](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)を使用してコントローラーに渡されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="7aaf8-195">コントローラーは、データを `ViewBag` オブジェクトにパッケージ化し、そのオブジェクトをビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="7aaf8-196">ビューには、データが HTML としてユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="7aaf8-197">上記のサンプルでは、`ViewBag` オブジェクトを使用して、コントローラーからビューにデータを渡しています。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="7aaf8-198">チュートリアルの後半では、ビューモデルを使用して、コントローラーからビューにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="7aaf8-199">データを渡すビューモデルのアプローチは、一般にビューバッグアプローチよりもはるかに優先されます。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="7aaf8-200">詳細については、「 [Dynamic V 厳密に型指定](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)されたビュー」のブログエントリを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="7aaf8-201">これは、モデルの &quot;M&quot; ですが、データベースの種類ではありませんでした。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="7aaf8-202">学習したことを確認し、ムービーのデータベースを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="7aaf8-202">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7aaf8-203">[前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="7aaf8-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
