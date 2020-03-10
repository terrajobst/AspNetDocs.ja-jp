---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: コントローラーの追加 |Microsoft Docs
author: shanselman
description: このチュートリアルが使用可能な場合は、Visual Studio 2013 を使用して更新されたバージョンです。 新しいチュートリアルでは、ASP.NET MVC 5 を使用します。これにより、
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437566"
---
# <a name="adding-a-controller"></a><span data-ttu-id="22002-104">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="22002-104">Adding a Controller</span></span>

<span data-ttu-id="22002-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="22002-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="22002-106">このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。</span><span class="sxs-lookup"><span data-stu-id="22002-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="22002-107">このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="22002-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="22002-108">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="22002-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="22002-109">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="22002-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="22002-110">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="22002-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="22002-111">MVC は、モデル、ビュー、コントローラーを表します。</span><span class="sxs-lookup"><span data-stu-id="22002-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="22002-112">MVC は、アプリケーションを開発するためのパターンであり、各部分が別の部分とは異なる責任を担います。</span><span class="sxs-lookup"><span data-stu-id="22002-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="22002-113">モデル: アプリケーションのデータ</span><span class="sxs-lookup"><span data-stu-id="22002-113">Model: The data of your application</span></span>
- <span data-ttu-id="22002-114">Views: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。</span><span class="sxs-lookup"><span data-stu-id="22002-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="22002-115">コントローラー: アプリケーションへの受信 URL 要求を処理し、モデルデータを取得して、クライアントに応答を返すビューテンプレートを指定するクラス</span><span class="sxs-lookup"><span data-stu-id="22002-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="22002-116">このチュートリアルでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="22002-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="22002-117">ソリューションエクスプローラーで controllers フォルダーを右クリックし、[コントローラーの追加] を選択して、新しいコントローラーを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="22002-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="22002-118">[![Addコントローラーの追加](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="22002-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="22002-119">新しいコントローラーに "HelloWorldController" という名前を指定し、[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="22002-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="22002-120">[[コントローラーの追加] ダイアログ ![](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="22002-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="22002-121">右側のソリューションエクスプローラーに、HelloWorldController.cs という名前の新しいファイルが作成され、そのファイルが**IDE**で開かれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="22002-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="22002-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="22002-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="22002-123">新しいパブリッククラス HelloWorldController 内で、次のような2つの新しいメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="22002-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="22002-124">例として、コントローラーから直接 HTML の文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="22002-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="22002-125">コントローラーは HelloWorldController という名前で、新しいメソッドは Index と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="22002-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="22002-126">先ほどと同じように、アプリケーションをもう一度実行します ([再生] ボタンをクリックするか、F5 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="22002-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="22002-127">ブラウザーが起動したら、アドレスバーのパスを `http://localhost:xx/HelloWorld` に変更します。ここで、xx はコンピューターが選択した任意の番号です。</span><span class="sxs-lookup"><span data-stu-id="22002-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="22002-128">これでブラウザーは次のスクリーンショットのようになります。</span><span class="sxs-lookup"><span data-stu-id="22002-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="22002-129">上記のメソッドでは、"Content" という名前のメソッドに渡された文字列を返しました。</span><span class="sxs-lookup"><span data-stu-id="22002-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="22002-130">システムが HTML を返すだけです。</span><span class="sxs-lookup"><span data-stu-id="22002-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="22002-131">ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="22002-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="22002-132">ASP.NET MVC で使用される既定のマッピングロジックでは、次のような形式を使用して、実行されるコードを制御します。</span><span class="sxs-lookup"><span data-stu-id="22002-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="22002-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="22002-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="22002-134">URL の最初の部分では、実行するコントローラークラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="22002-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="22002-135">そのため、HelloWorld は HelloWorldController クラスにマップされます。</span><span class="sxs-lookup"><span data-stu-id="22002-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="22002-136">URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。</span><span class="sxs-lookup"><span data-stu-id="22002-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="22002-137">したがって、/HelloWorld/Index では、HelloWorldController クラスの Index () メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="22002-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldController class to execute.</span></span> <span data-ttu-id="22002-138">上の例にのみアクセスする必要があり、メソッドインデックスが暗黙的に示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="22002-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="22002-139">これは、"Index" という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。</span><span class="sxs-lookup"><span data-stu-id="22002-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="22002-140">[既定のアクション ![](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="22002-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="22002-141">ここで `http://localhost:xx/HelloWorld/Welcome.` にアクセスして、ウェルカムメソッドが実行され、HTML 文字列が返されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="22002-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="22002-142">ここでも、/[Controller]/[ActionName]/[Parameters] のように、コントローラーは HelloWorld で、この場合は Welcome がメソッドです。</span><span class="sxs-lookup"><span data-stu-id="22002-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="22002-143">パラメーターはまだ完了していません。</span><span class="sxs-lookup"><span data-stu-id="22002-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="22002-144">[![開始アクションメソッド](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="22002-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="22002-145">サンプルを少し変更して、URL の一部の情報をコントローラーに渡すことができるようにします。たとえば、/HelloWorld/Welcome? name = Scott&amp;numtimes = 4 のようにします。</span><span class="sxs-lookup"><span data-stu-id="22002-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="22002-146">2つのパラメーターを含むように Welcome メソッドを変更し、次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="22002-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="22002-147">C#省略可能なパラメーター機能を使用して、パラメーター numtimes が渡されなかった場合、既定値は1に設定されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="22002-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="22002-148">アプリケーションを実行し、[名前] と [numtimes] の値を必要に応じて変更 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="22002-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="22002-149">システムによって、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。</span><span class="sxs-lookup"><span data-stu-id="22002-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="22002-150">これらの例では、コントローラーがすべての作業を行っており、HTML を直接返しています。</span><span class="sxs-lookup"><span data-stu-id="22002-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="22002-151">通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に面倒であるためです。</span><span class="sxs-lookup"><span data-stu-id="22002-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="22002-152">代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="22002-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="22002-153">これを実行する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="22002-153">Let's look at how we can do this.</span></span> <span data-ttu-id="22002-154">ブラウザーを閉じて、IDE に戻ります。</span><span class="sxs-lookup"><span data-stu-id="22002-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22002-155">[前へ](getting-started-with-mvc-part1.md)
> [次へ](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="22002-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
