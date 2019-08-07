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
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810767"
---
# <a name="adding-a-controller"></a><span data-ttu-id="e7760-102">コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="e7760-102">Adding a Controller</span></span>

<span data-ttu-id="e7760-103">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="e7760-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="e7760-104">MVC は、*モデルビューコントローラー*を表します。</span><span class="sxs-lookup"><span data-stu-id="e7760-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="e7760-105">MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。</span><span class="sxs-lookup"><span data-stu-id="e7760-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="e7760-106">MVC ベースのアプリケーションには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e7760-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="e7760-107">**M** odels:アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。</span><span class="sxs-lookup"><span data-stu-id="e7760-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="e7760-108">**V** iews:アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。</span><span class="sxs-lookup"><span data-stu-id="e7760-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="e7760-109">**C** ontrollers:入力方向のブラウザー要求を処理し、モデルデータを取得して、ブラウザーに応答を返すビューテンプレートを指定するクラス。</span><span class="sxs-lookup"><span data-stu-id="e7760-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="e7760-110">このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e7760-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="e7760-111">まず、コントローラークラスを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="e7760-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="e7760-112">**ソリューションエクスプローラー**で、 *Controllers*フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7760-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="e7760-113">**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 コントローラー-空]** をクリックし、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7760-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="e7760-114">新しいコントローラーに "HelloWorldController" という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e7760-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![コントローラーの追加](adding-a-controller/_static/image3.png)

<span data-ttu-id="e7760-116">*HelloWorldController.cs*という名前の新しいファイルと新しいフォルダー *Views\HelloWorld*が作成されたことを**ソリューションエクスプローラー**に注意してください。</span><span class="sxs-lookup"><span data-stu-id="e7760-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="e7760-117">コントローラーは IDE で開かれています。</span><span class="sxs-lookup"><span data-stu-id="e7760-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="e7760-118">ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7760-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="e7760-119">コントローラーメソッドは HTML の文字列を例として返します。</span><span class="sxs-lookup"><span data-stu-id="e7760-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="e7760-120">コントローラーにはと`HelloWorldController`いう名前が付けられ`Index`、最初のメソッドにはという名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="e7760-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="e7760-121">ブラウザーから呼び出してみましょう。</span><span class="sxs-lookup"><span data-stu-id="e7760-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="e7760-122">アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="e7760-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="e7760-123">ブラウザーで、HelloWorld &quot;&quot;をアドレスバーのパスに追加します。</span><span class="sxs-lookup"><span data-stu-id="e7760-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="e7760-124">(たとえば、次`http://localhost:1234/HelloWorld.`の図では、ブラウザーのページは次のスクリーンショットのようになります)。</span><span class="sxs-lookup"><span data-stu-id="e7760-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="e7760-125">上記のメソッドでは、コードによって文字列が直接返されました。</span><span class="sxs-lookup"><span data-stu-id="e7760-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="e7760-126">HTML を返すだけでシステムに指示しました。</span><span class="sxs-lookup"><span data-stu-id="e7760-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="e7760-127">ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e7760-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="e7760-128">ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。</span><span class="sxs-lookup"><span data-stu-id="e7760-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="e7760-129">ルーティングの形式は、*アプリ\_の Start/RouteConfig*ファイルで設定します。</span><span class="sxs-lookup"><span data-stu-id="e7760-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="e7760-130">アプリケーションを実行するときに、URL セグメントを指定しない場合、既定では、上記のコードの [既定] セクションで指定されている "Home" コントローラーと "Index" アクションメソッドが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="e7760-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="e7760-131">URL の最初の部分では、実行するコントローラークラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="e7760-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="e7760-132">そのため、 *HelloWorld*は`HelloWorldController`クラスにマップします。</span><span class="sxs-lookup"><span data-stu-id="e7760-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="e7760-133">URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。</span><span class="sxs-lookup"><span data-stu-id="e7760-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="e7760-134">したがって、 */HelloWorld/Index* `Index`では、 `HelloWorldController`クラスのメソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="e7760-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="e7760-135">また、 *HelloWorld*を参照しなければならないことに`Index`注意してください。既定では、メソッドが使用されていました。</span><span class="sxs-lookup"><span data-stu-id="e7760-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="e7760-136">これは、という名前`Index`のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="e7760-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="e7760-137">URL セグメントの 3 番目の部分 (`Parameters`) はルート データ用です。</span><span class="sxs-lookup"><span data-stu-id="e7760-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="e7760-138">ルートデータについては、このチュートリアルで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="e7760-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="e7760-139">`http://localhost:xxxx/HelloWorld/Welcome` を参照します。</span><span class="sxs-lookup"><span data-stu-id="e7760-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="e7760-140">メソッドが実行され、文字列&quot;が返されます。これは歓迎のアクションメソッドです... `Welcome`&quot;.</span><span class="sxs-lookup"><span data-stu-id="e7760-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="e7760-141">既定の MVC マッピングは`/[Controller]/[ActionName]/[Parameters]`です。</span><span class="sxs-lookup"><span data-stu-id="e7760-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="e7760-142">この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。</span><span class="sxs-lookup"><span data-stu-id="e7760-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="e7760-143">URL の `[Parameters]` の部分はまだ使っていません。</span><span class="sxs-lookup"><span data-stu-id="e7760-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="e7760-144">例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name =&amp;Scott numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="e7760-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="e7760-145">次に`Welcome`示すように、2つのパラメーターを含めるようにメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="e7760-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="e7760-146">このコードでは、 C#省略可能な-parameter 機能を使用し`numTimes`て、パラメーターに値が渡されない場合に既定で1に設定する必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="e7760-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="e7760-147">セキュリティに関するメモ :上記のコードでは、HttpUtility を使用して、悪意のある入力 (つまり JavaScript) からアプリケーションを保護してい[ます](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7760-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="e7760-148">詳細については、「[方法: HTML エンコーディングを文字列](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)に適用することで、Web アプリケーションのスクリプト攻略を防止します。</span><span class="sxs-lookup"><span data-stu-id="e7760-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="e7760-149">アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) に移動します。</span><span class="sxs-lookup"><span data-stu-id="e7760-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="e7760-150">URL の `name` と `numtimes` に違う値を指定してみてください。</span><span class="sxs-lookup"><span data-stu-id="e7760-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="e7760-151">[ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。</span><span class="sxs-lookup"><span data-stu-id="e7760-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="e7760-152">上のサンプルでは、URL セグメント ( `Parameters`) は使用されず`name` 、 `numTimes`パラメーターとパラメーターは[クエリ文字列](http://en.wikipedia.org/wiki/Query_string)として渡されます。</span><span class="sxs-lookup"><span data-stu-id="e7760-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="e7760-153">?</span><span class="sxs-lookup"><span data-stu-id="e7760-153">The ?</span></span> <span data-ttu-id="e7760-154">上記の URL の (疑問符) は区切り記号であり、クエリ文字列は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e7760-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="e7760-155">&amp; 文字は、クエリ文字列を区切ります。</span><span class="sxs-lookup"><span data-stu-id="e7760-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="e7760-156">Welcome メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e7760-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="e7760-157">アプリケーションを実行し、次の URL を入力します。`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="e7760-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="e7760-158">この時点で、3番目の url セグメント`ID.`が`Welcome`ルートパラメーターと一致した`ID`場合、アクションメソッドには、 `RegisterRoutes`メソッド内の url 指定に一致するパラメーター () が含まれます。</span><span class="sxs-lookup"><span data-stu-id="e7760-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="e7760-159">ASP.NET MVC アプリケーションでは、パラメーターをクエリ文字列として渡すよりも、ルートデータとしてパラメーターを渡す方が一般的です (上記の ID を使用した場合など)。</span><span class="sxs-lookup"><span data-stu-id="e7760-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="e7760-160">ルートを追加して、と`name` `numtimes`の両方のパラメーターを URL のルートデータとして渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="e7760-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="e7760-161">*App\_Start\RouteConfig.cs*ファイルで、"Hello" ルートを追加します。</span><span class="sxs-lookup"><span data-stu-id="e7760-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="e7760-162">アプリケーションを実行し、に`/localhost:XXX/HelloWorld/Welcome/Scott/3`移動します。</span><span class="sxs-lookup"><span data-stu-id="e7760-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="e7760-163">多くの MVC アプリケーションでは、既定のルートは正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="e7760-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="e7760-164">このチュートリアルの後半では、モデルバインダーを使用してデータを渡す方法について学習します。そのための既定のルートを変更する必要もありません。</span><span class="sxs-lookup"><span data-stu-id="e7760-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="e7760-165">これらの例では、コントローラーが MVC &quot;の&quot; VC 部分 (ビューとコントローラーが動作) を実行しています。</span><span class="sxs-lookup"><span data-stu-id="e7760-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="e7760-166">コントローラーは HTML を直接返しています。</span><span class="sxs-lookup"><span data-stu-id="e7760-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="e7760-167">通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。</span><span class="sxs-lookup"><span data-stu-id="e7760-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="e7760-168">代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="e7760-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="e7760-169">次に、その方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="e7760-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e7760-170">[前へ](getting-started.md)
> [次へ](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="e7760-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
