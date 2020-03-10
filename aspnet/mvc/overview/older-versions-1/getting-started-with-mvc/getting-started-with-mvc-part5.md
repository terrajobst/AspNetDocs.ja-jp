---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437368"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="5063d-104">コントローラーからモデルのデータにアクセスする</span><span class="sxs-lookup"><span data-stu-id="5063d-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="5063d-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="5063d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="5063d-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="5063d-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="5063d-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="5063d-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="5063d-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5063d-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="5063d-109">このセクションでは、新しい Moviescontroller.cs クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="5063d-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="5063d-110">Controllers フォルダーを右クリックし、新しい Moviescontroller.cs を作成します。</span><span class="sxs-lookup"><span data-stu-id="5063d-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="5063d-111">[コントローラーの追加 ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5063d-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="5063d-112">これにより、プロジェクト内の \ Controllers フォルダーの下に新しい "MoviesController.cs" ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5063d-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="5063d-113">MovieController を更新して、新しく設定されたデータベースから映画の一覧を取得してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5063d-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="5063d-114">1984年の夏の後にリリースされた映画のみを取得するように LINQ クエリを実行しています。</span><span class="sxs-lookup"><span data-stu-id="5063d-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="5063d-115">このムービーの一覧を表示するにはビューテンプレートが必要です。そのため、メソッドを右クリックし、[ビューの追加] を選択して作成します。</span><span class="sxs-lookup"><span data-stu-id="5063d-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="5063d-116">[ビューの追加] ダイアログボックスで、ビューテンプレートに&lt;映画&gt; リストを渡していることを示します。</span><span class="sxs-lookup"><span data-stu-id="5063d-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="5063d-117">以前に [ビューの追加] ダイアログを使用し、"空の" テンプレートを作成することを選択したのとは異なり、今回は、Visual Studio が既定のコンテンツを含むビューテンプレートを自動的に "スキャフォールディング" するように指定します。</span><span class="sxs-lookup"><span data-stu-id="5063d-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="5063d-118">これを行うには、[コンテンツの表示] ドロップダウンメニュー内の [リスト] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="5063d-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="5063d-119">新しいクラスを作成した場合は、[ビューの追加] ダイアログボックスに表示されるように、アプリケーションをコンパイルする必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5063d-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![ビューの追加](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="5063d-121">[追加] をクリックすると、ムービーの一覧を表示するビューのコードが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="5063d-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="5063d-122">&lt;h2&gt; の見出しを、前に Hello World ビューで行ったような "マイムービーリスト" のように変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5063d-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="5063d-123">[![映画-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5063d-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="5063d-124">アプリケーションを実行し、アドレスバーで [/ムービー] にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="5063d-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="5063d-125">これで、コントローラー内の基本的なクエリを使用してデータベースからデータを取得し、ムービーを認識するビューにデータを返しました。</span><span class="sxs-lookup"><span data-stu-id="5063d-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="5063d-126">その後、そのビューはムービーの一覧をスピンし、データのテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="5063d-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="5063d-127">[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="5063d-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="5063d-128">このアプリケーションでは編集、詳細、削除機能を実装しません。そのため、スキャフォールディングテンプレートによって作成された既定のリンクは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5063d-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="5063d-129">/Movies/Index.aspx ファイルを開き、削除します。</span><span class="sxs-lookup"><span data-stu-id="5063d-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="5063d-130">更新されたビューテンプレートのソースコードを次に示します。これらの変更を行った後は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5063d-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="5063d-131">必要のないリンクが作成されているので、この例ではリンクを削除します。</span><span class="sxs-lookup"><span data-stu-id="5063d-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="5063d-132">次に示すように、新しいリンクを作成しておきます。</span><span class="sxs-lookup"><span data-stu-id="5063d-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="5063d-133">この列を削除すると、アプリは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5063d-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="5063d-134">[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="5063d-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="5063d-135">これで、ムービーデータを簡単に一覧表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5063d-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="5063d-136">ただし、[新規作成] リンクをクリックすると、フックされていないためエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="5063d-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="5063d-137">Create Action メソッドを実装し、ユーザーがデータベースに新しい映画を入力できるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="5063d-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5063d-138">[前へ](getting-started-with-mvc-part4.md)
> [次へ](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="5063d-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
