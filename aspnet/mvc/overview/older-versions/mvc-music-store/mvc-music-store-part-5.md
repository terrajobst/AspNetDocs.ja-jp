---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 'パート 5: フォームとテンプレートの編集 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート5では、フォームとテンプレートの編集について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450910"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="221f1-104">パート 5: フォームとテンプレートの編集</span><span class="sxs-lookup"><span data-stu-id="221f1-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="221f1-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="221f1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="221f1-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="221f1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="221f1-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="221f1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="221f1-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="221f1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="221f1-109">パート5では、フォームとテンプレートの編集について説明します。</span><span class="sxs-lookup"><span data-stu-id="221f1-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="221f1-110">これまでの章では、データベースからデータを読み込んで表示していました。</span><span class="sxs-lookup"><span data-stu-id="221f1-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="221f1-111">この章では、データの編集も有効にします。</span><span class="sxs-lookup"><span data-stu-id="221f1-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="221f1-112">StoreManagerController の作成</span><span class="sxs-lookup"><span data-stu-id="221f1-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="221f1-113">まず、 **StoreManagerController**という名前の新しいコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="221f1-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="221f1-114">このコントローラーでは、ASP.NET MVC 3 Tools Update で提供されているスキャフォールディング機能を利用します。</span><span class="sxs-lookup"><span data-stu-id="221f1-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="221f1-115">次に示すように、[コントローラーの追加] ダイアログのオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="221f1-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="221f1-116">[追加] ボタンをクリックすると、ASP.NET MVC 3 のスキャフォールディングメカニズムによって適切な作業が行われます。</span><span class="sxs-lookup"><span data-stu-id="221f1-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="221f1-117">ローカル Entity Framework 変数を使用して新しい StoreManagerController を作成します。</span><span class="sxs-lookup"><span data-stu-id="221f1-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="221f1-118">これにより、StoreManager フォルダーがプロジェクトの Views フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="221f1-119">これにより、作成した cshtml、Delete. cshtml、Details、Edit. cshtml、および Index. cshtml ビューが追加され、アルバムクラスに厳密に型指定されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="221f1-120">新しい StoreManager コントローラークラスには、CRUD (作成、読み取り、更新、削除) コントローラーアクションが含まれています。これは、アルバムモデルクラスを使用してデータベースアクセスに Entity Framework のコンテキストを使用する方法を知っています。</span><span class="sxs-lookup"><span data-stu-id="221f1-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="221f1-121">スキャフォールディングビューの変更</span><span class="sxs-lookup"><span data-stu-id="221f1-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="221f1-122">このコードが生成されましたが、このチュートリアル全体を通して記述したのと同じように、標準の ASP.NET MVC コードであることを覚えておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="221f1-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="221f1-123">これは、定型的なコントローラーコードを記述し、厳密に型指定されたビューを手動で作成するために費やされる時間を節約することを目的としていますが、これは、ディレクトリの警告で、コード.</span><span class="sxs-lookup"><span data-stu-id="221f1-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="221f1-124">これはコードであり、変更することが期待されています。</span><span class="sxs-lookup"><span data-stu-id="221f1-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="221f1-125">では、StoreManager インデックスビューのクイック編集 (/Views/StoreManager/Index.cshtml) から始めましょう。</span><span class="sxs-lookup"><span data-stu-id="221f1-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="221f1-126">このビューには、[編集]、[詳細]、[削除] リンクを含むストア内のアルバムの一覧が表示され、アルバムのパブリックプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="221f1-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="221f1-127">この表示ではあまり役に立たないので、AlbumArtUrl フィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="221f1-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="221f1-128">下の強調表示されている行で示されているように、ビューコードの &lt;テーブル&gt; セクションで、次のように、AlbumArtUrl 参照を囲む &lt;th&gt; と &lt;td&gt; 要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="221f1-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="221f1-129">変更されたビューコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="221f1-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="221f1-130">ストアマネージャーの最初の確認</span><span class="sxs-lookup"><span data-stu-id="221f1-130">A first look at the Store Manager</span></span>

<span data-ttu-id="221f1-131">ここで、アプリケーションを実行し、/StoreManager/. に移動します。</span><span class="sxs-lookup"><span data-stu-id="221f1-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="221f1-132">これにより、変更したばかりのストアマネージャーのインデックスが表示され、ストア内のアルバムの一覧と、編集、詳細、削除のリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="221f1-133">[編集] リンクをクリックすると、ジャンルとアーティストのドロップダウンを含む、アルバムのフィールドを含む編集フォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="221f1-134">下部にある [一覧に戻る] リンクをクリックし、アルバムの [Details] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="221f1-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="221f1-135">これにより、個々のアルバムの詳細情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="221f1-136">ここでも、[一覧に戻る] リンクをクリックし、[削除] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="221f1-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="221f1-137">これにより、アルバムの詳細が表示され、削除するかどうかを確認する確認ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="221f1-138">下部にある [削除] ボタンをクリックすると、アルバムが削除され、[インデックス] ページに戻ります。このページには、削除されたアルバムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="221f1-139">ストアマネージャーでは実行されませんが、CRUD 操作を開始するためのコントローラーとビューコードが用意されています。</span><span class="sxs-lookup"><span data-stu-id="221f1-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="221f1-140">ストアマネージャーコントローラーコードを見る</span><span class="sxs-lookup"><span data-stu-id="221f1-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="221f1-141">ストアマネージャーコントローラーには、十分な量のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="221f1-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="221f1-142">これを上から下に見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="221f1-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="221f1-143">コントローラーには、MVC コントローラーの標準名前空間と、モデルの名前空間への参照が含まれています。</span><span class="sxs-lookup"><span data-stu-id="221f1-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="221f1-144">コントローラーには、データアクセスの各コントローラーアクションによって使用される MusicStoreEntities のプライベートインスタンスがあります。</span><span class="sxs-lookup"><span data-stu-id="221f1-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="221f1-145">ストアマネージャーのインデックスと詳細アクション</span><span class="sxs-lookup"><span data-stu-id="221f1-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="221f1-146">インデックスビューでは、各アルバムの参照されているジャンルとアーティスト情報を含むアルバムの一覧が取得されます。これについては、ストアの参照方法に関する説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="221f1-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="221f1-147">インデックスビューは、リンクオブジェクトへの参照に従っているので、各アルバムのジャンル名とアーティスト名を表示できるようにします。これにより、コントローラーは効率的になり、元の要求でこの情報を照会できます。</span><span class="sxs-lookup"><span data-stu-id="221f1-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="221f1-148">StoreManager コントローラーの詳細コントローラーアクションは、先ほど作成したストアコントローラーの詳細アクションとまったく同じように動作します。これは、Find () メソッドを使用して ID でアルバムを照会し、それをビューに返します。</span><span class="sxs-lookup"><span data-stu-id="221f1-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="221f1-149">Create Action メソッド</span><span class="sxs-lookup"><span data-stu-id="221f1-149">The Create Action Methods</span></span>

<span data-ttu-id="221f1-150">作成アクションメソッドは、フォーム入力を処理するため、これまでに見たものとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="221f1-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="221f1-151">ユーザーが初めて/StoreManager/Create/にアクセスすると、空のフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="221f1-152">この HTML ページには、&lt;フォーム&gt; 要素が含まれています。これには、ドロップダウンおよびテキストボックスの入力要素が含まれており、そこでアルバムの詳細を入力できます。</span><span class="sxs-lookup"><span data-stu-id="221f1-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="221f1-153">ユーザーがアルバムフォームの値を入力したら、[保存] ボタンをクリックして、これらの変更をアプリケーションに送信し、データベース内に保存することができます。</span><span class="sxs-lookup"><span data-stu-id="221f1-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="221f1-154">ユーザーが [save] \ (保存 \) ボタンを押すと、&lt;フォーム&gt; によって/StoreManager/Create/URL への HTTP ポストバックが実行され、HTTP POST の一部として &lt;フォーム&gt; 値が送信されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="221f1-155">ASP.NET MVC を使用すると、これら2つの URL 呼び出しシナリオのロジックを簡単に分割できます。 StoreManagerController クラス内に2つの個別の "Create" アクションメソッドを実装し、1つは/StoreManager/Create/URL への最初の HTTP 取得を処理し、もう1つは、送信された変更の HTTP POST を処理します。</span><span class="sxs-lookup"><span data-stu-id="221f1-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="221f1-156">ViewBag を使用して情報をビューに渡す</span><span class="sxs-lookup"><span data-stu-id="221f1-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="221f1-157">このチュートリアルの前半で ViewBag を使用しましたが、これについてはあまり説明していません。</span><span class="sxs-lookup"><span data-stu-id="221f1-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="221f1-158">ViewBag を使用すると、厳密に型指定されたモデルオブジェクトを使用せずに、ビューに情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="221f1-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="221f1-159">この場合、[HTTP-GET controller の編集] アクションでは、ドロップダウンを設定するために、ジャンルとアーティストの一覧の両方をフォームに渡す必要があります。これを行う最も簡単な方法は、ViewBag 項目として返すことです。</span><span class="sxs-lookup"><span data-stu-id="221f1-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="221f1-160">ViewBag は動的なオブジェクトです。つまり、ViewBag または ViewBag と入力すると、これらのプロパティを定義するコードを記述しなくてもかまいません。</span><span class="sxs-lookup"><span data-stu-id="221f1-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="221f1-161">この場合、コントローラーコードは ViewBag と ViewBag を使用して、フォームと共に送信されるドロップダウンの値が GenreId および ArtistId になります。これは、設定されるアルバムプロパティです。</span><span class="sxs-lookup"><span data-stu-id="221f1-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="221f1-162">これらのドロップダウン値は、その目的のためだけに構築された SelectList オブジェクトを使用してフォームに返されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="221f1-163">これは、次のようなコードを使用して行います。</span><span class="sxs-lookup"><span data-stu-id="221f1-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="221f1-164">アクションメソッドコードからわかるように、このオブジェクトを作成するために3つのパラメーターが使用されています。</span><span class="sxs-lookup"><span data-stu-id="221f1-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="221f1-165">ドロップダウンに表示される項目の一覧。</span><span class="sxs-lookup"><span data-stu-id="221f1-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="221f1-166">これは文字列ではないことに注意してください。ジャンルの一覧を渡しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="221f1-167">SelectList に渡される次のパラメーターは、選択された値です。</span><span class="sxs-lookup"><span data-stu-id="221f1-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="221f1-168">ここでは、リスト内の項目を事前に選択する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="221f1-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="221f1-169">これは、編集フォームを見たときに理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="221f1-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="221f1-170">最後のパラメーターは、表示されるプロパティです。</span><span class="sxs-lookup"><span data-stu-id="221f1-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="221f1-171">この場合、Genre.Name プロパティがユーザーに表示されることを示しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="221f1-172">この点を念頭に置いて、HTTP GET Create アクションは非常に単純であり、2つの SelectLists が ViewBag に追加され、モデルオブジェクトは (まだ作成されていないため) フォームに渡されません。</span><span class="sxs-lookup"><span data-stu-id="221f1-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="221f1-173">作成ビューでドロップダウンを表示する HTML ヘルパー</span><span class="sxs-lookup"><span data-stu-id="221f1-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="221f1-174">ここではドロップダウン値がビューにどのように渡されるかを説明したので、ビューを見て、それらの値がどのように表示されるかを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="221f1-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="221f1-175">[コードの表示] (/Views/StoreManager/Create.cshtml) では、ジャンルドロップダウンを表示するために次の呼び出しが行われていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="221f1-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="221f1-176">これを HTML ヘルパーと呼びます。これは、一般的なビュータスクを実行するユーティリティメソッドです。</span><span class="sxs-lookup"><span data-stu-id="221f1-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="221f1-177">HTML ヘルパーは、ビューコードを簡潔かつ読みやすくするために非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="221f1-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="221f1-178">ASP.NET MVC は Html の DropDownList ヘルパーを提供しますが、後で説明するように、アプリケーションで再利用するコードを表示するための独自のヘルパーを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="221f1-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="221f1-179">Html の DropDownList 呼び出しには、表示するリストを取得する場所と、事前に選択する必要がある値 (存在する場合) を2つ指定するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="221f1-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="221f1-180">最初のパラメーター GenreId は、モデルまたは ViewBag のいずれかで GenreId という値を検索するように DropDownList に指示します。</span><span class="sxs-lookup"><span data-stu-id="221f1-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="221f1-181">2番目のパラメーターは、ドロップダウンリストで最初に選択された値を示すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="221f1-182">このフォームは作成フォームなので、事前に選択された値はありません。空の文字列が渡されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="221f1-183">ポストされたフォーム値の処理</span><span class="sxs-lookup"><span data-stu-id="221f1-183">Handling the Posted Form values</span></span>

<span data-ttu-id="221f1-184">前に説明したように、各フォームには2つのアクションメソッドが関連付けられています。</span><span class="sxs-lookup"><span data-stu-id="221f1-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="221f1-185">最初のは、HTTP GET 要求を処理し、フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="221f1-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="221f1-186">2つ目は、送信されたフォーム値を含む HTTP POST 要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="221f1-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="221f1-187">コントローラーアクションには [HttpPost] 属性があり、ASP.NET MVC は HTTP POST 要求にのみ応答する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="221f1-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="221f1-188">このアクションには、次の4つの役割があります。</span><span class="sxs-lookup"><span data-stu-id="221f1-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="221f1-189">フォームの値を読み取る</span><span class="sxs-lookup"><span data-stu-id="221f1-189">Read the form values</span></span>
- 2. <span data-ttu-id="221f1-190">フォーム値が検証規則に合格するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="221f1-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="221f1-191">フォームの送信が有効な場合は、データを保存して更新された一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="221f1-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="221f1-192">フォームの送信が有効でない場合は、検証エラーが表示されたフォームを再表示します。</span><span class="sxs-lookup"><span data-stu-id="221f1-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="221f1-193">モデルバインドを使用したフォーム値の読み取り</span><span class="sxs-lookup"><span data-stu-id="221f1-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="221f1-194">コントローラーアクションは、GenreId と ArtistId (ドロップダウンリスト) の値、および Title、Price、および AlbumArtUrl のテキストボックス値を含むフォーム送信を処理しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="221f1-195">フォーム値に直接アクセスすることもできますが、ASP.NET MVC に組み込まれているモデルバインド機能を使用する方法が適しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="221f1-196">コントローラーアクションがモデル型をパラメーターとして受け取ると、ASP.NET MVC は、フォーム入力 (および route および querystring 値) を使用して、その型のオブジェクトを設定しようとします。</span><span class="sxs-lookup"><span data-stu-id="221f1-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="221f1-197">これを行うには、モデルオブジェクトのプロパティと一致する名前を持つ値を探します。たとえば、新しいアルバムオブジェクトの GenreId 値を設定すると、GenreId という名前の入力が検索されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="221f1-198">ASP.NET MVC の標準メソッドを使用してビューを作成する場合、フォームは常に入力フィールド名としてプロパティ名を使用して表示されるため、このフィールド名は一致するだけです。</span><span class="sxs-lookup"><span data-stu-id="221f1-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="221f1-199">モデルの検証</span><span class="sxs-lookup"><span data-stu-id="221f1-199">Validating the Model</span></span>

<span data-ttu-id="221f1-200">モデルは、ModelState. IsValid の単純な呼び出しで検証されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="221f1-201">まだアルバムクラスに検証ルールを追加していません。これは少しの間、このチェックはあまり実行されません。</span><span class="sxs-lookup"><span data-stu-id="221f1-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="221f1-202">重要なのは、この ModelStat. IsValid check は、モデルに配置した検証規則に適合するため、今後、検証規則を変更しても、コントローラーのアクションコードを更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="221f1-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="221f1-203">送信された値を保存しています</span><span class="sxs-lookup"><span data-stu-id="221f1-203">Saving the submitted values</span></span>

<span data-ttu-id="221f1-204">フォーム送信が検証に合格した場合は、その値をデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="221f1-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="221f1-205">Entity Framework では、モデルをアルバムコレクションに追加し、SaveChanges を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="221f1-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="221f1-206">Entity Framework は、値を永続化するための適切な SQL コマンドを生成します。</span><span class="sxs-lookup"><span data-stu-id="221f1-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="221f1-207">データを保存すると、アルバムの一覧にリダイレクトされ、更新プログラムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="221f1-208">これを行うには、表示するコントローラーアクションの名前を使用して RedirectToAction を返します。</span><span class="sxs-lookup"><span data-stu-id="221f1-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="221f1-209">この例では、これが Index メソッドです。</span><span class="sxs-lookup"><span data-stu-id="221f1-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="221f1-210">検証エラーのある無効なフォーム送信の表示</span><span class="sxs-lookup"><span data-stu-id="221f1-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="221f1-211">無効なフォーム入力の場合は、ドロップダウンの値が (HTTP GET の場合と同様に) ViewBag に追加され、バインドされたモデル値がビューに戻されて表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="221f1-212">検証エラーは、@Html.ValidationMessageFor HTML ヘルパーを使用して自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="221f1-213">作成フォームのテスト</span><span class="sxs-lookup"><span data-stu-id="221f1-213">Testing the Create Form</span></span>

<span data-ttu-id="221f1-214">これをテストするには、アプリケーションを実行し、/StoreManager/Create/に移動します。これにより、StoreController Create HTTP-GET メソッドによって返された空白のフォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="221f1-215">いくつかの値を入力し、[作成] ボタンをクリックしてフォームを送信します。</span><span class="sxs-lookup"><span data-stu-id="221f1-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="221f1-216">編集の処理</span><span class="sxs-lookup"><span data-stu-id="221f1-216">Handling Edits</span></span>

<span data-ttu-id="221f1-217">編集アクションのペア (HTTP-GET と HTTP POST) は、先ほど見た Create アクションメソッドによく似ています。</span><span class="sxs-lookup"><span data-stu-id="221f1-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="221f1-218">編集シナリオでは既存のアルバムを操作するため、Edit HTTP-GET メソッドは、ルートを介して渡される "id" パラメーターに基づいてアルバムを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="221f1-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="221f1-219">AlbumId によってアルバムを取得するためのこのコードは、前に「コントローラーの詳細」アクションで確認したものと同じです。</span><span class="sxs-lookup"><span data-stu-id="221f1-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="221f1-220">Create/HTTP-GET メソッドと同様に、ドロップダウンの値は ViewBag を使用して返されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="221f1-221">これにより、ViewBag を介して追加のデータ (ジャンルの一覧など) を渡すとともに、モデルオブジェクトとしてアルバムを (アルバムクラスに厳密に型指定された) ビューに返すことができます。</span><span class="sxs-lookup"><span data-stu-id="221f1-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="221f1-222">Edit HTTP-POST アクションは、Create HTTP-POST アクションと非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="221f1-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="221f1-223">唯一の違いは、新しいアルバムを db に追加するのではなく、アルバムコレクション。 db を使用してアルバムの現在のインスタンスを検索しています。エントリ (アルバム) を入力し、その状態を "変更済み" に設定します。</span><span class="sxs-lookup"><span data-stu-id="221f1-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="221f1-224">これは、新しいアルバムを作成するのではなく、既存のアルバムを変更することを Entity Framework します。</span><span class="sxs-lookup"><span data-stu-id="221f1-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="221f1-225">これをテストするには、アプリケーションを実行し、/Storemanger/に移動して、アルバムの [編集] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="221f1-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="221f1-226">これにより、Edit HTTP-GET メソッドによって表示される編集フォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="221f1-227">いくつかの値を入力し、[保存] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="221f1-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="221f1-228">これにより、フォームが投稿され、値が保存されて、値が更新されたことを示すアルバムリストに戻ります。</span><span class="sxs-lookup"><span data-stu-id="221f1-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="221f1-229">削除の処理</span><span class="sxs-lookup"><span data-stu-id="221f1-229">Handling Deletion</span></span>

<span data-ttu-id="221f1-230">削除は、編集と作成と同じパターンに従い、1つのコントローラーアクションを使用して確認フォームを表示し、もう1つのコントローラーアクションを使用してフォームの送信を処理します。</span><span class="sxs-lookup"><span data-stu-id="221f1-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="221f1-231">HTTP-Delete controller アクションは、以前のストアマネージャー詳細コントローラーアクションとまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="221f1-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="221f1-232">[ビューコンテンツの削除] テンプレートを使用して、アルバムの種類に厳密に型指定されたフォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="221f1-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="221f1-233">[削除] テンプレートには、モデルのすべてのフィールドが表示されますが、簡単に簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="221f1-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="221f1-234">/Views/StoreManager/Delete.cshtml のビューコードを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="221f1-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="221f1-235">これにより、簡略化された削除の確認が表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="221f1-236">[削除] ボタンをクリックすると、フォームがサーバーにポストバックされます。これにより、DeleteConfirmed アクションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="221f1-237">HTTP ポスト削除コントローラーアクションは、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="221f1-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="221f1-238">ID でアルバムを読み込みます</span><span class="sxs-lookup"><span data-stu-id="221f1-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="221f1-239">アルバムを削除し、変更を保存します</span><span class="sxs-lookup"><span data-stu-id="221f1-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="221f1-240">リストからアルバムが削除されたことを示すインデックスにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="221f1-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="221f1-241">これをテストするには、アプリケーションを実行し、/StoreManager. に移動します。</span><span class="sxs-lookup"><span data-stu-id="221f1-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="221f1-242">一覧からアルバムを選択し、[削除] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="221f1-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="221f1-243">削除の確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="221f1-244">[削除] ボタンをクリックすると、アルバムが削除され、[ストアマネージャーインデックス] ページに戻ります。これは、アルバムが削除されたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="221f1-245">カスタム HTML ヘルパーを使用したテキストの切り捨て</span><span class="sxs-lookup"><span data-stu-id="221f1-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="221f1-246">ストアマネージャーのインデックスページでは、潜在的な問題が1つあります。</span><span class="sxs-lookup"><span data-stu-id="221f1-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="221f1-247">アルバムのタイトルとアーティスト名のプロパティは、どちらも、テーブルの書式設定を破棄するのに十分な長さにすることができます。</span><span class="sxs-lookup"><span data-stu-id="221f1-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="221f1-248">ここでは、これらのプロパティとその他のプロパティをビューで簡単に切り捨てることができるように、カスタム HTML ヘルパーを作成します。</span><span class="sxs-lookup"><span data-stu-id="221f1-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="221f1-249">Razor の @helper 構文では、ビューで使用する独自のヘルパー関数を簡単に作成できました。</span><span class="sxs-lookup"><span data-stu-id="221f1-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="221f1-250">/Views/StoreManager/Index.cshtml ビューを開き、@model 行の直後に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="221f1-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="221f1-251">このヘルパーメソッドは、文字列と最大長を使用して許可します。</span><span class="sxs-lookup"><span data-stu-id="221f1-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="221f1-252">指定したテキストが指定された長さより短い場合、ヘルパーはそれをそのように出力します。</span><span class="sxs-lookup"><span data-stu-id="221f1-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="221f1-253">長い場合は、テキストを切り捨て、"..." をレンダリングします。それ以外の場合はです。</span><span class="sxs-lookup"><span data-stu-id="221f1-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="221f1-254">ここで、Truncate helper を使用して、アルバムのタイトルとアーティスト名の両方のプロパティが25文字未満であることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="221f1-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="221f1-255">新しい Truncate ヘルパーを使用する完全なビューコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="221f1-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="221f1-256">ここで、/StoreManager/URL を参照したときに、アルバムとタイトルは最大長の下に保持されます。</span><span class="sxs-lookup"><span data-stu-id="221f1-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="221f1-257">注: これは、ヘルパーを作成して1つのビューで使用する単純なケースを示しています。</span><span class="sxs-lookup"><span data-stu-id="221f1-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="221f1-258">サイト全体で使用できるヘルパーの作成の詳細については、ブログの投稿: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="221f1-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="221f1-259">[前へ](mvc-music-store-part-4.md)
> [次へ](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="221f1-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
