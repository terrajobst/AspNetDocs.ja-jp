---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Create メソッドと Create View | を追加するMicrosoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437290"
---
# <a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="d2324-104">Create メソッドと Create ビューの追加</span><span class="sxs-lookup"><span data-stu-id="d2324-104">Adding a Create Method and Create View</span></span>

<span data-ttu-id="d2324-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="d2324-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="d2324-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="d2324-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="d2324-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="d2324-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="d2324-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2324-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="d2324-109">このセクションでは、ユーザーがデータベースに新しい映画を作成できるようにするために必要なサポートを実装します。</span><span class="sxs-lookup"><span data-stu-id="d2324-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="d2324-110">これを行うには、/Movies/Create URL アクションを実装します。</span><span class="sxs-lookup"><span data-stu-id="d2324-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="d2324-111">/Movies/Create URL の実装は、2つの手順で行います。</span><span class="sxs-lookup"><span data-stu-id="d2324-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="d2324-112">ユーザーが最初に/Movies/Create URL にアクセスしたときに、新しいムービーを入力するために入力できる HTML フォームを表示したいと考えています。</span><span class="sxs-lookup"><span data-stu-id="d2324-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="d2324-113">次に、ユーザーがフォームを送信し、データをサーバーにポストバックするときに、ポストされた内容を取得してデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="d2324-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="d2324-114">これらの2つの手順は、Moviescontroller.cs クラス内の2つの Create () メソッド内に実装します。</span><span class="sxs-lookup"><span data-stu-id="d2324-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="d2324-115">1つの方法では、ユーザーが新しいムービーを作成するために入力する必要のある &lt;フォーム&gt; を示します。</span><span class="sxs-lookup"><span data-stu-id="d2324-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="d2324-116">2番目の方法では、ユーザーが &lt;フォーム&gt; をサーバーに送り返し、データベース内に新しいムービーを保存するときに、ポストされたデータの処理を処理します。</span><span class="sxs-lookup"><span data-stu-id="d2324-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="d2324-117">Moviescontroller.cs クラスに追加して、これを実装するコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="d2324-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="d2324-118">上のコードには、コントローラー内で必要なすべてのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d2324-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="d2324-119">ここで、フォームをユーザーに表示するために使用する Create View テンプレートを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="d2324-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="d2324-120">最初の Create メソッドを右クリックし、[ビューの追加] を選択して、ムービーフォームのビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="d2324-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="d2324-121">ビューテンプレートに "Movie" を表示データクラスとして渡し、"スキャフォールディング" というテンプレートを "作成" することを指定します。</span><span class="sxs-lookup"><span data-stu-id="d2324-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="d2324-122">[ビューの追加 ![](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d2324-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="d2324-123">[追加] ボタンをクリックすると、\Movies\Create.aspx View テンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d2324-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="d2324-124">[View content] \ (コンテンツの表示 \) ドロップダウンから [作成] を選択したので、[ビューの追加] ダイアログボックスには既定のコンテンツが自動的に "スキャフォールディング" されます。</span><span class="sxs-lookup"><span data-stu-id="d2324-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="d2324-125">スキャフォールディングによって、HTML &lt;フォーム&gt;が作成され、検証エラーメッセージが表示されます。スキャフォールディングによってムービーが認識されるため、クラスの各プロパティのラベルとフィールドが作成されました。</span><span class="sxs-lookup"><span data-stu-id="d2324-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="d2324-126">このデータベースでは、ムービーに ID が自動的に付与されるため、モデルを参照するフィールドを削除してみましょう。[作成] ビューの Id。</span><span class="sxs-lookup"><span data-stu-id="d2324-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="d2324-127">凡例の&gt;フィールド&gt;&lt;[凡例] の &lt;7 行を削除します。これには、不要な ID フィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d2324-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="d2324-128">ここで、新しいムービーを作成し、データベースに追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="d2324-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="d2324-129">この操作を行うには、アプリケーションをもう一度実行し、"/映画" の URL にアクセスし、[作成] リンクをクリックして新しいムービーを追加します。</span><span class="sxs-lookup"><span data-stu-id="d2324-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="d2324-130">[![作成-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d2324-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="d2324-131">[作成] ボタンをクリックすると、このフォームのデータが、先ほど作成した/Movies/Create メソッドにポストバックされます (HTTP POST 経由)。</span><span class="sxs-lookup"><span data-stu-id="d2324-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="d2324-132">システムが URL から "numTimes" パラメーターと "name" パラメーターを自動的に取得して、以前のメソッドのパラメーターにマップした場合と同様に、システムは自動的に POST からフォームフィールドを取得し、オブジェクトにマップします。</span><span class="sxs-lookup"><span data-stu-id="d2324-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="d2324-133">この場合、"ReleaseDate" や "Title" などの HTML のフィールドの値は、ムービーの新しいインスタンスの正しいプロパティに自動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="d2324-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="d2324-134">もう一度 Moviescontroller.cs から2つ目の Create メソッドを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="d2324-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="d2324-135">引数として "Movie" オブジェクトを取得する方法に注目してください。</span><span class="sxs-lookup"><span data-stu-id="d2324-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="d2324-136">その後、このムービーオブジェクトは、Create action メソッドの [HttpPost] バージョンに渡され、データベースに保存された後、ムービーリストに保存された結果を示す Index () アクションメソッドにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="d2324-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="d2324-137">[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d2324-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="d2324-138">ただし、ムービーが正しいかどうかは確認しません。また、データベースでタイトルのないムービーを保存することはできません。</span><span class="sxs-lookup"><span data-stu-id="d2324-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="d2324-139">データベースがエラーをスローする前に、ユーザーに通知することもできます。</span><span class="sxs-lookup"><span data-stu-id="d2324-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="d2324-140">これを行うには、アプリケーションに検証サポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="d2324-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2324-141">[前へ](getting-started-with-mvc-part5.md)
> [次へ](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="d2324-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
