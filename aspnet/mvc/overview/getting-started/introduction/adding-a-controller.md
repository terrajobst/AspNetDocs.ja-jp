---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: コントローラーの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 194a8a7398e163f0c37164a8724f98b16444984b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499132"
---
# <a name="adding-a-controller"></a><span data-ttu-id="4c080-102">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="4c080-102">Adding a Controller</span></span>

<span data-ttu-id="4c080-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4c080-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="4c080-104">MVC は、*モデルビューコントローラー*を表します。</span><span class="sxs-lookup"><span data-stu-id="4c080-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="4c080-105">MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。</span><span class="sxs-lookup"><span data-stu-id="4c080-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="4c080-106">MVC ベースのアプリケーションには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="4c080-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="4c080-107">**M** odels: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。</span><span class="sxs-lookup"><span data-stu-id="4c080-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="4c080-108">**V** iews: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。</span><span class="sxs-lookup"><span data-stu-id="4c080-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="4c080-109">**C** ontrollers: 入力方向のブラウザー要求を処理し、モデルデータを取得し、ブラウザーに応答を返すビューテンプレートを指定するクラス。</span><span class="sxs-lookup"><span data-stu-id="4c080-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="4c080-110">このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4c080-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="4c080-111">まず、コントローラークラスを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4c080-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="4c080-112">**ソリューションエクスプローラー**で、 *Controllers*フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="4c080-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="4c080-113">**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 コントローラー-空]** をクリックし、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4c080-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="4c080-114">新しいコントローラーに "HelloWorldController" という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4c080-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![コントローラーの追加](adding-a-controller/_static/image3.png)

<span data-ttu-id="4c080-116">*HelloWorldController.cs*という名前の新しいファイルと新しいフォルダー *Views\HelloWorld*が作成されたことを**ソリューションエクスプローラー**に注意してください。</span><span class="sxs-lookup"><span data-stu-id="4c080-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="4c080-117">コントローラーは IDE で開かれています。</span><span class="sxs-lookup"><span data-stu-id="4c080-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="4c080-118">このファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4c080-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="4c080-119">コントローラーメソッドは HTML の文字列を例として返します。</span><span class="sxs-lookup"><span data-stu-id="4c080-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="4c080-120">コントローラーには `HelloWorldController` という名前が付けられ、最初のメソッドには `Index`という名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="4c080-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="4c080-121">ブラウザーから呼び出してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4c080-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="4c080-122">アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="4c080-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="4c080-123">ブラウザーで、&quot;HelloWorld&quot; をアドレスバーのパスに追加します。</span><span class="sxs-lookup"><span data-stu-id="4c080-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="4c080-124">(たとえば、次の図では `http://localhost:1234/HelloWorld.`)ブラウザーのページは次のスクリーンショットのようになります。</span><span class="sxs-lookup"><span data-stu-id="4c080-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="4c080-125">上記のメソッドでは、コードによって文字列が直接返されました。</span><span class="sxs-lookup"><span data-stu-id="4c080-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="4c080-126">HTML を返すだけでシステムに指示しました。</span><span class="sxs-lookup"><span data-stu-id="4c080-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="4c080-127">ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4c080-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="4c080-128">ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。</span><span class="sxs-lookup"><span data-stu-id="4c080-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="4c080-129">アプリでルーティングの形式を設定するには *\_Start/RouteConfig*ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="4c080-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="4c080-130">アプリケーションを実行するときに、URL セグメントを指定しない場合、既定では、上記のコードの [既定] セクションで指定されている "Home" コントローラーと "Index" アクションメソッドが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="4c080-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="4c080-131">URL の最初の部分では、実行するコントローラークラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="4c080-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="4c080-132">そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。</span><span class="sxs-lookup"><span data-stu-id="4c080-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="4c080-133">URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。</span><span class="sxs-lookup"><span data-stu-id="4c080-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="4c080-134">したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="4c080-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="4c080-135">また、 *HelloWorld*を参照するだけで、`Index` メソッドが既定で使用されていたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4c080-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="4c080-136">これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="4c080-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="4c080-137">URL セグメントの 3 番目の部分 (`Parameters`) はルート データ用です。</span><span class="sxs-lookup"><span data-stu-id="4c080-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="4c080-138">ルートデータについては、このチュートリアルで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="4c080-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="4c080-139">[https://www.microsoft.com](`http://localhost:xxxx/HelloWorld/Welcome`) を参照します。</span><span class="sxs-lookup"><span data-stu-id="4c080-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="4c080-140">`Welcome` メソッドが実行され、文字列 &quot;返されます。これは、ウェルカムアクションメソッド...&quot;です。</span><span class="sxs-lookup"><span data-stu-id="4c080-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="4c080-141">既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="4c080-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="4c080-142">この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。</span><span class="sxs-lookup"><span data-stu-id="4c080-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="4c080-143">URL の `[Parameters]` の部分はまだ使っていません。</span><span class="sxs-lookup"><span data-stu-id="4c080-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="4c080-144">例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="4c080-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="4c080-145">次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="4c080-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="4c080-146">このコードでは、 C#省略可能なパラメーターの機能を使用して、パラメーターに値が渡されない場合に、`numTimes` パラメーターが既定値の1に設定されることを示していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4c080-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="4c080-147">セキュリティに関する注意: 上記のコードでは、 [HttpUtility](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)を使用して、悪意のある入力 (つまり JavaScript) からアプリケーションを保護します。</span><span class="sxs-lookup"><span data-stu-id="4c080-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="4c080-148">詳細については[、「方法: HTML エンコーディングを文字列に適用](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4c080-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="4c080-149">アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) を参照します。</span><span class="sxs-lookup"><span data-stu-id="4c080-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="4c080-150">URL の `name` と `numtimes` に違う値を指定してみてください。</span><span class="sxs-lookup"><span data-stu-id="4c080-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="4c080-151">[ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。</span><span class="sxs-lookup"><span data-stu-id="4c080-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="4c080-152">上記のサンプルでは、URL セグメント (`Parameters`) は使用されず、`name` パラメーターと `numTimes` パラメーターは[クエリ文字列](http://en.wikipedia.org/wiki/Query_string)として渡されます。</span><span class="sxs-lookup"><span data-stu-id="4c080-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="4c080-153">?</span><span class="sxs-lookup"><span data-stu-id="4c080-153">The ?</span></span> <span data-ttu-id="4c080-154">上記の URL の (疑問符) は区切り記号であり、クエリ文字列は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4c080-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="4c080-155">&amp; 文字は、クエリ文字列を区切ります。</span><span class="sxs-lookup"><span data-stu-id="4c080-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="4c080-156">Welcome メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4c080-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="4c080-157">アプリケーションを実行し、次の URL を入力します。 `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="4c080-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="4c080-158">この時点で、3番目の URL セグメントがルートパラメーターと一致し `ID.` `Welcome` アクションメソッドには、`RegisterRoutes` メソッドの URL 指定に一致したパラメーター (`ID`) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4c080-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="4c080-159">ASP.NET MVC アプリケーションでは、パラメーターをクエリ文字列として渡すよりも、ルートデータとしてパラメーターを渡す方が一般的です (上記の ID を使用した場合など)。</span><span class="sxs-lookup"><span data-stu-id="4c080-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="4c080-160">ルートを追加して、URL のルートデータとしてパラメーターに `name` と `numtimes` を渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="4c080-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="4c080-161">*アプリ\_Start\RouteConfig.cs*ファイルに、"Hello" ルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="4c080-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="4c080-162">アプリケーションを実行し、`/localhost:XXX/HelloWorld/Welcome/Scott/3`を参照します。</span><span class="sxs-lookup"><span data-stu-id="4c080-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="4c080-163">多くの MVC アプリケーションでは、既定のルートは正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="4c080-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="4c080-164">このチュートリアルの後半では、モデルバインダーを使用してデータを渡す方法について学習します。そのための既定のルートを変更する必要もありません。</span><span class="sxs-lookup"><span data-stu-id="4c080-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="4c080-165">これらの例では、コントローラーが MVC の &quot;VC&quot; の部分を実行しています。つまり、ビューとコントローラーが動作します。</span><span class="sxs-lookup"><span data-stu-id="4c080-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="4c080-166">コントローラーは HTML を直接返しています。</span><span class="sxs-lookup"><span data-stu-id="4c080-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="4c080-167">通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。</span><span class="sxs-lookup"><span data-stu-id="4c080-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="4c080-168">代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="4c080-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="4c080-169">次に、その方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="4c080-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4c080-170">[前へ](getting-started.md)
> [次へ](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="4c080-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
