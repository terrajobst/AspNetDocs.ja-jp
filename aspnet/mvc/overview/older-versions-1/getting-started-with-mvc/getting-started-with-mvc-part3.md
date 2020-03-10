---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: ビューを追加する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469774"
---
# <a name="adding-a-view"></a><span data-ttu-id="1ec51-104">ビューの追加</span><span class="sxs-lookup"><span data-stu-id="1ec51-104">Adding a View</span></span>

<span data-ttu-id="1ec51-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="1ec51-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="1ec51-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="1ec51-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="1ec51-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="1ec51-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ec51-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="1ec51-109">このセクションでは、HelloWorldController クラスがビューテンプレートファイルを使用して、HTML 応答の生成をクライアントに対して正常にカプセル化する方法を見ていきます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="1ec51-110">まず、ビューテンプレートとインデックスメソッドを使用してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="1ec51-111">このメソッドは Index と呼ばれ、HelloWorldController にあります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="1ec51-112">現在、Index () メソッドは、コントローラークラス内にハードコードされたメッセージを含む文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="1ec51-113">次のように、インデックスメソッドをに変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="1ec51-114">ここで、Index () メソッドに使用できるビューテンプレートをプロジェクトに追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="1ec51-115">これを行うには、Index メソッドの途中でマウスを右クリックし、[ビューの追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![image](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="1ec51-117">[ビューの追加] ダイアログが表示されます。このダイアログでは、Index メソッドで使用できるビューテンプレートを作成する方法に関するいくつかのオプションを提供しています。</span><span class="sxs-lookup"><span data-stu-id="1ec51-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="1ec51-118">ここでは、何も変更せずに、[追加] ボタンをクリックするだけです。</span><span class="sxs-lookup"><span data-stu-id="1ec51-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="1ec51-119">[![ビューの追加 ダイアログ](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="1ec51-120">[追加] をクリックすると、次に示すように、ソリューションフォルダーに新しいフォルダーと新しいファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="1ec51-121">これで、[ビュー] の下に HelloWorld フォルダーがあり、そのフォルダー内にインデックス .aspx ファイルが作成されました。</span><span class="sxs-lookup"><span data-stu-id="1ec51-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="1ec51-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="1ec51-123">新しいインデックスファイルも既に開いていて、編集する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="1ec51-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="1ec51-124">最初の &lt;h2&gt;Index&lt;/h2&gt; "Hello World" のようなテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="1ec51-125">アプリケーションを実行し、ブラウザーでもう一度[`http://localhost:xx/HelloWorld`](http://localhostxx)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="1ec51-126">この例では、コントローラーの Index メソッドは何の処理も行いませんでしたが、"return View ()" を呼び出しました。これは、ビューテンプレートファイルを使用してクライアントに応答を返すことを示していました。</span><span class="sxs-lookup"><span data-stu-id="1ec51-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="1ec51-127">使用するビューテンプレートファイルの名前を明示的に指定しなかったため、ASP.NET MVC では、\Views\HelloWorld フォルダー内のインデックス .aspx ビューファイルを使用するように既定で設定されています。</span><span class="sxs-lookup"><span data-stu-id="1ec51-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="1ec51-128">これで、ビューにハードコーディングされた文字列が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="1ec51-129">[![インデックス-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="1ec51-130">すばらしいですね。</span><span class="sxs-lookup"><span data-stu-id="1ec51-130">Looks pretty good.</span></span> <span data-ttu-id="1ec51-131">ただし、ブラウザーのタイトルには "Index" と表示され、ページの大きなタイトルは "My MVC Application" と表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1ec51-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="1ec51-132">これらを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="1ec51-133">ビューおよびマスターページの変更</span><span class="sxs-lookup"><span data-stu-id="1ec51-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="1ec51-134">まず、"My MVC Application" というテキストを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="1ec51-135">そのテキストは共有され、すべてのページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="1ec51-136">実際には、アプリ内のすべてのページにある場合でも、コード内の1つの場所にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="1ec51-137">ソリューションエクスプローラーの [/]/[共有] フォルダーにアクセスして、[] を開きます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="1ec51-138">このファイルはマスターページと呼ばれ、他のすべてのページで使用される共有の "シェル" です。</span><span class="sxs-lookup"><span data-stu-id="1ec51-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="1ec51-139">このファイルに "MainContent" というテキストが ContentPlaceholder れていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1ec51-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="1ec51-140">このプレースホルダーには、作成したすべてのページが表示され、マスターページに "ラップ" されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="1ec51-141">タイトルを変更してから、アプリを実行して複数のページにアクセスしてみてください。</span><span class="sxs-lookup"><span data-stu-id="1ec51-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="1ec51-142">1つの変更が複数のページに表示されることがわかります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="1ec51-143">これで、すべてのページに、"マイ MVC ムービーアプリケーション" という主要な見出しが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1ec51-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="1ec51-144">これにより、すべてのページで共有されている白いテキストが上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="1ec51-145">次に示すのは、変更されたタイトルを含む、次のような場合です。</span><span class="sxs-lookup"><span data-stu-id="1ec51-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="1ec51-146">次に、インデックスページのタイトルを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="1ec51-147">/HelloWorld/Index.aspx. を開く</span><span class="sxs-lookup"><span data-stu-id="1ec51-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="1ec51-148">変更する場所は2つあります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-148">There's two places to change.</span></span> <span data-ttu-id="1ec51-149">最初に、ブラウザーのタイトルに表示されるタイトル、2番目のヘッダー (H2) も表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="1ec51-150">アプリケーションのどの部分に変更が加えられたかを確認できるように、それぞれを少し異なるようにします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="1ec51-151">アプリを実行し、/Movies. にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="1ec51-152">ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1ec51-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="1ec51-153">ビューに小さな変更を加えることで、アプリの大きな変更を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="1ec51-154">[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="1ec51-155">"データ" の少しです (この例では "Hello World!")。</span><span class="sxs-lookup"><span data-stu-id="1ec51-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="1ec51-156">メッセージ) がハードコーディングされています。</span><span class="sxs-lookup"><span data-stu-id="1ec51-156">message) was hard coded though.</span></span> <span data-ttu-id="1ec51-157">V (Views) がありますが、C (コントローラー) を持っていますが、M (モデル) はまだありません。</span><span class="sxs-lookup"><span data-stu-id="1ec51-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="1ec51-158">ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="1ec51-159">ビューモデルの引き渡し</span><span class="sxs-lookup"><span data-stu-id="1ec51-159">Passing a ViewModel</span></span>

<span data-ttu-id="1ec51-160">データベースにアクセスしてモデルについて説明する前に、まず "Viewmodel" について説明します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="1ec51-161">これらは、HTML 応答をクライアントに返すためにビューテンプレートが必要とするものを表すオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1ec51-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="1ec51-162">これらは通常、コントローラークラスによって作成され、ビューテンプレートに渡されます。また、ビューテンプレートに必要なデータだけを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="1ec51-163">以前の HelloWorld サンプルでは、Welcome () アクションメソッドは名前と numTimes パラメーターを受け取り、ブラウザーに出力しました。</span><span class="sxs-lookup"><span data-stu-id="1ec51-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="1ec51-164">コントローラーがこの応答を直接レンダリングするのではなく、そのデータを保持する小さいクラスを作成し、それをビューテンプレートに渡して、それを使用して HTML 応答を表示します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="1ec51-165">このようにして、コントローラーは1つの問題とビューテンプレートを考慮しています。これにより、アプリケーション内でクリーンな "問題の分離" を維持できるようになります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="1ec51-166">HelloWorldController.cs ファイルに戻り、新しい "WelcomeViewModel" クラスを追加して、コントローラー内の Welcome メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="1ec51-167">同じファイル内の新しいクラスを含む完全な HelloWorldController.cs を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="1ec51-168">複数の行に存在していても、ようこそメソッドは実際には2つのコードステートメントにすぎません。</span><span class="sxs-lookup"><span data-stu-id="1ec51-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="1ec51-169">最初のステートメントは、2つのパラメーターをモデル化オブジェクトにパッケージ化し、2つ目のパラメーターは結果のオブジェクトをビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="1ec51-170">ここで、ウェルカムビューテンプレートが必要です。</span><span class="sxs-lookup"><span data-stu-id="1ec51-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="1ec51-171">[ようこそ] メソッドを右クリックし、[ビューの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="1ec51-172">今回は、[厳密に型指定されたビューを作成する] チェックボックスをオンにし、ドロップダウンリストから WelcomeViewModel クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="1ec51-173">この新しいビューでは、WelcomeViewModels とその他の種類のオブジェクトは認識されません。</span><span class="sxs-lookup"><span data-stu-id="1ec51-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="1ec51-174">*注: ドロップダウンリストに表示するには、WelcomeViewModel を追加した後に1回コンパイルする必要があります。*</span><span class="sxs-lookup"><span data-stu-id="1ec51-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>

<span data-ttu-id="1ec51-175">[ビューの追加] ダイアログボックスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1ec51-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="1ec51-176">[追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-176">Click the Add button.</span></span> ![丸で囲んだビューの追加](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="1ec51-178">新しい Welcome の &lt;h2&gt; の下に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="1ec51-179">ループを作成し、ユーザーが必要としている回数だけ Hello と言います。</span><span class="sxs-lookup"><span data-stu-id="1ec51-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="1ec51-180">また、次のスクリーンショットに示されているように、モデルオブジェクトを参照するたびに便利な Intellisense が得られるので、このビューを入力している間に、WelcomeViewModel についての情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="1ec51-181">[![NumTime ソースコード](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="1ec51-182">アプリケーションを実行し、`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` にもう一度アクセスします。</span><span class="sxs-lookup"><span data-stu-id="1ec51-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="1ec51-183">これで、URL からデータを取得し、コントローラーに自動的に渡されます。コントローラーはデータをビューモデルにパッケージ化し、そのオブジェクトをビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="1ec51-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="1ec51-184">ビューでは、データが HTML としてユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ec51-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="1ec51-185">[![ようこそ-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1ec51-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="1ec51-186">それは、モデルの "M" ですが、データベースの種類ではありませんでした。</span><span class="sxs-lookup"><span data-stu-id="1ec51-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="1ec51-187">学習した内容を見て、映画のデータベースを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="1ec51-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ec51-188">[前へ](getting-started-with-mvc-part2.md)
> [次へ](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="1ec51-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
