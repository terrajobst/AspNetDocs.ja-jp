---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: コントローラーの追加 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485446"
---
# <a name="adding-a-controller"></a><span data-ttu-id="5144b-104">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="5144b-104">Adding a Controller</span></span>

<span data-ttu-id="5144b-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5144b-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="5144b-106">このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。</span><span class="sxs-lookup"><span data-stu-id="5144b-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="5144b-107">より安全で、より簡単にフォローし、より多くの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="5144b-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="5144b-108">MVC は、*モデルビューコントローラー*を表します。</span><span class="sxs-lookup"><span data-stu-id="5144b-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="5144b-109">MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。</span><span class="sxs-lookup"><span data-stu-id="5144b-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="5144b-110">MVC ベースのアプリケーションには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5144b-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="5144b-111">**M** odels: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。</span><span class="sxs-lookup"><span data-stu-id="5144b-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="5144b-112">**V** iews: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。</span><span class="sxs-lookup"><span data-stu-id="5144b-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="5144b-113">**C** ontrollers: 入力方向のブラウザー要求を処理し、モデルデータを取得し、ブラウザーに応答を返すビューテンプレートを指定するクラス。</span><span class="sxs-lookup"><span data-stu-id="5144b-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="5144b-114">このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5144b-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="5144b-115">まず、コントローラークラスを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5144b-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="5144b-116">**ソリューションエクスプローラー**で、[*コントローラー* ] フォルダーを右クリックし、 **[コントローラーの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5144b-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="5144b-117">新しいコントローラーに HelloWorldController&quot;&quot;名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5144b-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="5144b-118">既定のテンプレートは**空の MVC コントローラー**のままにして、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5144b-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![コントローラーの追加](adding-a-controller/_static/image2.png)

<span data-ttu-id="5144b-120">**ソリューションエクスプローラー**に、 *HelloWorldController.cs*という名前の新しいファイルが作成されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5144b-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="5144b-121">ファイルは IDE で開かれています。</span><span class="sxs-lookup"><span data-stu-id="5144b-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="5144b-122">このファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5144b-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="5144b-123">コントローラーメソッドは HTML の文字列を例として返します。</span><span class="sxs-lookup"><span data-stu-id="5144b-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="5144b-124">コントローラーには `HelloWorldController` という名前が付けられ、上記の最初のメソッドには `Index`という名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="5144b-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="5144b-125">ブラウザーから呼び出してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5144b-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="5144b-126">アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="5144b-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="5144b-127">ブラウザーで、&quot;HelloWorld&quot; をアドレスバーのパスに追加します。</span><span class="sxs-lookup"><span data-stu-id="5144b-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="5144b-128">(たとえば、次の図では `http://localhost:1234/HelloWorld.`)ブラウザーのページは次のスクリーンショットのようになります。</span><span class="sxs-lookup"><span data-stu-id="5144b-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="5144b-129">上記のメソッドでは、コードによって文字列が直接返されました。</span><span class="sxs-lookup"><span data-stu-id="5144b-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="5144b-130">HTML を返すだけでシステムに指示しました。</span><span class="sxs-lookup"><span data-stu-id="5144b-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="5144b-131">ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5144b-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="5144b-132">ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。</span><span class="sxs-lookup"><span data-stu-id="5144b-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="5144b-133">URL の最初の部分では、実行するコントローラークラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="5144b-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="5144b-134">そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。</span><span class="sxs-lookup"><span data-stu-id="5144b-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="5144b-135">URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。</span><span class="sxs-lookup"><span data-stu-id="5144b-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="5144b-136">したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5144b-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="5144b-137">また、 *HelloWorld*を参照するだけで、`Index` メソッドが既定で使用されていたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5144b-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="5144b-138">これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="5144b-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="5144b-139">[https://www.microsoft.com](`http://localhost:xxxx/HelloWorld/Welcome`) を参照します。</span><span class="sxs-lookup"><span data-stu-id="5144b-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="5144b-140">`Welcome` メソッドが実行され、文字列 &quot;返されます。これは、ウェルカムアクションメソッド...&quot;です。</span><span class="sxs-lookup"><span data-stu-id="5144b-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="5144b-141">既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="5144b-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="5144b-142">この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。</span><span class="sxs-lookup"><span data-stu-id="5144b-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="5144b-143">URL の `[Parameters]` の部分はまだ使っていません。</span><span class="sxs-lookup"><span data-stu-id="5144b-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="5144b-144">例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="5144b-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="5144b-145">次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="5144b-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="5144b-146">このコードでは、 C#省略可能なパラメーターの機能を使用して、パラメーターに値が渡されない場合に、`numTimes` パラメーターが既定値の1に設定されることを示していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5144b-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="5144b-147">アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`を参照します。</span><span class="sxs-lookup"><span data-stu-id="5144b-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="5144b-148">URL の `name` と `numtimes` に違う値を指定してみてください。</span><span class="sxs-lookup"><span data-stu-id="5144b-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="5144b-149">[ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。</span><span class="sxs-lookup"><span data-stu-id="5144b-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="5144b-150">これらの例では、コントローラーが MVC の &quot;VC&quot; の部分 (ビューとコントローラーが動作) を実行しています。</span><span class="sxs-lookup"><span data-stu-id="5144b-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="5144b-151">コントローラーは HTML を直接返しています。</span><span class="sxs-lookup"><span data-stu-id="5144b-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="5144b-152">通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。</span><span class="sxs-lookup"><span data-stu-id="5144b-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="5144b-153">代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="5144b-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="5144b-154">次に、その方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="5144b-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5144b-155">[前へ](intro-to-aspnet-mvc-4.md)
> [次へ](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="5144b-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
