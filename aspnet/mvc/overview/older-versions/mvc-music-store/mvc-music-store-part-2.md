---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 'パート 2: コントローラー |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート2では、コントローラーについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451192"
---
# <a name="part-2-controllers"></a><span data-ttu-id="ae5d1-104">パート 2: コントローラー</span><span class="sxs-lookup"><span data-stu-id="ae5d1-104">Part 2: Controllers</span></span>

<span data-ttu-id="ae5d1-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="ae5d1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ae5d1-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ae5d1-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="ae5d1-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ae5d1-109">パート2では、コントローラーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="ae5d1-110">従来の web フレームワークでは、着信 Url は通常、ディスク上のファイルにマップされます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="ae5d1-111">たとえば、"/-.Aspx" や "/" などの URL の要求は、"Products" ファイルまたは "Products. php" ファイルによって処理される場合があります。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="ae5d1-112">Web ベースの MVC フレームワークでは、Url が少し異なる方法でサーバーコードにマップされます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="ae5d1-113">受信 Url をファイルにマッピングする代わりに、代わりに、Url をクラスのメソッドにマップします。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="ae5d1-114">これらのクラスは "コントローラー" と呼ばれ、受信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返信するための応答の決定 (HTML の表示、ファイルのダウンロード、別のファイルへのリダイレクトなど) を担当します。URL など)。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="ae5d1-115">HomeController の追加</span><span class="sxs-lookup"><span data-stu-id="ae5d1-115">Adding a HomeController</span></span>

<span data-ttu-id="ae5d1-116">サイトのホームページへの Url を処理するコントローラークラスを追加して、MVC ミュージックストアアプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="ae5d1-117">ASP.NET MVC の既定の名前付け規則に従って、HomeController を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="ae5d1-118">ソリューションエクスプローラー内の "Controllers" フォルダーを右クリックし、[追加] をクリックして、[コントローラー...]メニュー</span><span class="sxs-lookup"><span data-stu-id="ae5d1-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="ae5d1-119">これにより、[コントローラーの追加] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="ae5d1-120">コントローラーに "HomeController" という名前を指定し、[追加] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="ae5d1-121">これにより、次のコードを使用して新しいファイル HomeController.cs が作成されます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="ae5d1-122">できるだけ簡単に開始するために、Index メソッドを単に文字列を返す単純なメソッドに置き換えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="ae5d1-123">次の2つの変更を行います。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-123">We'll make two changes:</span></span>

- <span data-ttu-id="ae5d1-124">ActionResult ではなく文字列を返すようにメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="ae5d1-125">Return ステートメントを変更して "Hello from Home" を返します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="ae5d1-126">メソッドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="ae5d1-127">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="ae5d1-127">Running the Application</span></span>

<span data-ttu-id="ae5d1-128">では、サイトを実行してみましょう。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-128">Now let's run the site.</span></span> <span data-ttu-id="ae5d1-129">Web サーバーを起動して、次のいずれかを使用してサイトを試すことができます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="ae5d1-130">[Debug ⇨ Start デバッグ] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="ae5d1-131">ツールバーの緑色の矢印ボタンをクリックし ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="ae5d1-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="ae5d1-132">キーボードショートカットの F5 キーを使用します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="ae5d1-133">上記のいずれかの手順を使用すると、プロジェクトがコンパイルされ、Visual Web Developer に組み込まれている ASP.NET 開発サーバーが開始されます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="ae5d1-134">ASP.NET 開発サーバーが起動したことを示す通知が画面の下部に表示され、実行されているポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="ae5d1-135">Visual Web Developer によって、Web サーバーを指す URL を持つブラウザーウィンドウが自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="ae5d1-136">これにより、web アプリケーションを簡単に試すことができます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="ae5d1-137">これは非常に簡単でした。新しい web サイトを作成し、3行の機能を追加し、ブラウザーにテキストを追加しました。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="ae5d1-138">ロケット科学はありませんが、これは始まりです。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="ae5d1-139">*注: Visual Web Developer には ASP.NET 開発サーバーが含まれています。これにより、web サイトがランダムな "ポート" 番号で実行されます。上のスクリーンショットでは、サイトは `http://localhost:26641/`で実行されているので、ポート26641を使用しています。ポート番号は異なります。このチュートリアルでは、/Store/Browse のような URL について説明します。これは、ポート番号の後に移動します。ポート番号26641を指定した場合は、`http://localhost:26641/Store/Browse`を参照していることを意味します。*</span><span class="sxs-lookup"><span data-stu-id="ae5d1-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="ae5d1-140">StoreController の追加</span><span class="sxs-lookup"><span data-stu-id="ae5d1-140">Adding a StoreController</span></span>

<span data-ttu-id="ae5d1-141">サイトのホームページを実装する単純な HomeController を追加しました。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="ae5d1-142">ここで、音楽ストアの閲覧機能を実装するために使用する別のコントローラーを追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="ae5d1-143">ストアコントローラーでは、次の3つのシナリオがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="ae5d1-144">音楽ストアの音楽ジャンルのリストページ</span><span class="sxs-lookup"><span data-stu-id="ae5d1-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="ae5d1-145">特定のジャンルにあるすべての音楽アルバムを一覧表示する参照ページ</span><span class="sxs-lookup"><span data-stu-id="ae5d1-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="ae5d1-146">特定のミュージックアルバムに関する情報を示す詳細ページ</span><span class="sxs-lookup"><span data-stu-id="ae5d1-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="ae5d1-147">まず、新しい StoreController クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="ae5d1-148">まだ開いていない場合は、ブラウザーを閉じるか、[デバッグ] [デバッグ] [⇨の停止] メニュー項目の順に選択して、アプリケーションの実行を停止します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="ae5d1-149">次に、新しい StoreController を追加します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-149">Now add a new StoreController.</span></span> <span data-ttu-id="ae5d1-150">HomeController の場合と同様に、この操作を行うには、ソリューションエクスプローラー内の "Controllers" フォルダーを右クリックし、[&gt;コントローラー] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="ae5d1-151">新しい StoreController には既に "Index" メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="ae5d1-152">この "Index" メソッドを使用して、音楽ストア内のすべてのジャンルを一覧表示するリストページを実装します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="ae5d1-153">また、StoreController で処理する他の2つのシナリオ (参照と詳細) を実装する2つのメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="ae5d1-154">コントローラー内のこれらのメソッド (インデックス、参照、および詳細) は "コントローラーアクション" と呼ばれ、HomeController () アクションメソッドで既に説明したように、ジョブは URL 要求に応答し、(一般的には) コンテンツを決定します。は、URL を呼び出したブラウザーまたはユーザーに返信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="ae5d1-155">StoreController 実装を開始するには、theIndex () メソッドを変更して "Hello from Store. Index ()" という文字列を返します。次に、Browse () と Details () に同様のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="ae5d1-156">プロジェクトを再度実行し、次の Url を参照します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="ae5d1-157">/Store</span><span class="sxs-lookup"><span data-stu-id="ae5d1-157">/Store</span></span>
- <span data-ttu-id="ae5d1-158">/ストア/参照</span><span class="sxs-lookup"><span data-stu-id="ae5d1-158">/Store/Browse</span></span>
- <span data-ttu-id="ae5d1-159">ストア/詳細</span><span class="sxs-lookup"><span data-stu-id="ae5d1-159">/Store/Details</span></span>

<span data-ttu-id="ae5d1-160">これらの Url にアクセスすると、コントローラー内のアクションメソッドが呼び出され、文字列応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="ae5d1-161">これはすばらしいことですが、これらは定数文字列にすぎません。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="ae5d1-162">動的なものにして、URL から情報を取得し、ページ出力に表示してみましょう。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="ae5d1-163">まず、参照アクションメソッドを変更して、URL から querystring 値を取得します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="ae5d1-164">これを行うには、アクションメソッドに "genre" パラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="ae5d1-165">この操作を実行すると、ASP.NET MVC は、呼び出されたときに、"genre" という名前のクエリ文字列またはフォームポストパラメーターを自動的にアクションメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="ae5d1-166">*メモ: HtmlEncode ユーティリティメソッドを使用して、ユーザー入力をサニタイズしています。これにより、ユーザーがビューに Javascript を挿入できなくなります。Genre =&lt;スクリプト&gt;ウィンドウ. location = 'http://hackersite.com'&lt;/script&gt;。*</span><span class="sxs-lookup"><span data-stu-id="ae5d1-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="ae5d1-167">次に、参照して参照してみましょう。Genre = Disco</span><span class="sxs-lookup"><span data-stu-id="ae5d1-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="ae5d1-168">次に、[詳細] アクションを [ID] という名前の入力パラメーターを読み取って表示するように変更します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="ae5d1-169">前のメソッドとは異なり、ID 値を querystring パラメーターとして埋め込むことはできません。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="ae5d1-170">代わりに、URL 自体に直接埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="ae5d1-171">例:/Store/詳細/5。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="ae5d1-172">ASP.NET MVC を使用すると、何も構成しなくても簡単にこの操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="ae5d1-173">ASP.NET MVC の既定のルーティング規則では、アクションメソッド名の後の URL のセグメントを "ID" という名前のパラメーターとして扱います。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="ae5d1-174">アクションメソッドに ID という名前のパラメーターがある場合、ASP.NET MVC は自動的に URL セグメントをパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="ae5d1-175">アプリケーションを実行し、次のように参照します。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="ae5d1-176">これまでに実行したことをまとめてみましょう。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="ae5d1-177">Visual Web Developer で新しい ASP.NET MVC プロジェクトを作成しました</span><span class="sxs-lookup"><span data-stu-id="ae5d1-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="ae5d1-178">ASP.NET MVC アプリケーションの基本的なフォルダー構造について説明しました。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="ae5d1-179">ASP.NET 開発サーバーを使用して web サイトを実行する方法を学習しました</span><span class="sxs-lookup"><span data-stu-id="ae5d1-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="ae5d1-180">HomeController と StoreController という2つのコントローラークラスを作成しました。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="ae5d1-181">URL 要求に応答してテキストをブラウザーに返す、コントローラーにアクションメソッドを追加しました。</span><span class="sxs-lookup"><span data-stu-id="ae5d1-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ae5d1-182">[前へ](mvc-music-store-part-1.md)
> [次へ](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="ae5d1-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
