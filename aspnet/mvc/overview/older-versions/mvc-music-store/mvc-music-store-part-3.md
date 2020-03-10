---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 'パート 3: Views と Viewmodel |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート3では、ビューと Viewmodel について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451132"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="5338a-104">パート 3: Views と Viewmodel</span><span class="sxs-lookup"><span data-stu-id="5338a-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="5338a-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="5338a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="5338a-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="5338a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="5338a-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="5338a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="5338a-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="5338a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="5338a-109">パート3では、ビューと Viewmodel について説明します。</span><span class="sxs-lookup"><span data-stu-id="5338a-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="5338a-110">ここまでで、コントローラーアクションから文字列を返していました。</span><span class="sxs-lookup"><span data-stu-id="5338a-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="5338a-111">これは、コントローラーがどのように動作するかを把握するのに便利な方法ですが、実際の web アプリケーションを構築する方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="5338a-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="5338a-112">ここでは、サイトにアクセスするブラウザーに HTML を返す方が優れています。1つはテンプレートファイルを使用して、送信した HTML コンテンツを簡単にカスタマイズできるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="5338a-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="5338a-113">このビューでは、まさにこのビューが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="5338a-114">ビューテンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="5338a-114">Adding a View template</span></span>

<span data-ttu-id="5338a-115">ビューテンプレートを使用するには、ActionResult を返すように HomeController Index メソッドを変更し、次のように View () を返すようにします。</span><span class="sxs-lookup"><span data-stu-id="5338a-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="5338a-116">上記の変更は、文字列を返さずに、代わりに "ビュー" を使用して結果を返すことを示しています。</span><span class="sxs-lookup"><span data-stu-id="5338a-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="5338a-117">次に、適切なビューテンプレートをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="5338a-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="5338a-118">これを行うには、Index アクションメソッド内にテキストカーソルを置き、右クリックして [ビューの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5338a-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="5338a-119">[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="5338a-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5338a-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="5338a-121">[ビューの追加] ダイアログボックスを使用すると、ビューテンプレートファイルをすばやく簡単に生成できます。</span><span class="sxs-lookup"><span data-stu-id="5338a-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="5338a-122">既定では、[ビューの追加] ダイアログボックスに、作成するビューテンプレートの名前があらかじめ設定されているので、それを使用するアクションメソッドと一致します。</span><span class="sxs-lookup"><span data-stu-id="5338a-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="5338a-123">HomeController の Index () アクションメソッド内で [ビューの追加] コンテキストメニューを使用したので、上の [ビューの追加] ダイアログには、既定でビュー名として "Index" が設定されています。</span><span class="sxs-lookup"><span data-stu-id="5338a-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="5338a-124">このダイアログのオプションを変更する必要はありません。 [追加] ボタンをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="5338a-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="5338a-125">[追加] ボタンをクリックすると、Visual Web Developer によって \Views\Home ディレクトリに新しいインデックスの cshtml ビューテンプレートが作成され、まだ存在しない場合はフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="5338a-126">"Index. cshtml" ファイルの名前とフォルダーの場所は重要で、既定の ASP.NET MVC 名前付け規則に従います。</span><span class="sxs-lookup"><span data-stu-id="5338a-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="5338a-127">ディレクトリ名 \Views\Home は、HomeController という名前のコントローラーに一致します。</span><span class="sxs-lookup"><span data-stu-id="5338a-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="5338a-128">ビューテンプレート名 Index は、ビューを表示するコントローラーアクションメソッドに一致します。</span><span class="sxs-lookup"><span data-stu-id="5338a-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="5338a-129">ASP.NET MVC を使用すると、この名前付け規則を使用してビューを返すときに、ビューテンプレートの名前または場所を明示的に指定しなくても済むようになります。</span><span class="sxs-lookup"><span data-stu-id="5338a-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="5338a-130">HomeController 内に次のようなコードを記述すると、既定で \Views\Home\Index.cshtml view テンプレートがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="5338a-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="5338a-131">[ビューの追加] ダイアログボックスで [追加] ボタンをクリックした後、Visual Web Developer によって "Index. cshtml" ビューテンプレートが作成され、開かれました。</span><span class="sxs-lookup"><span data-stu-id="5338a-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="5338a-132">次に、インデックスの内容を示します。</span><span class="sxs-lookup"><span data-stu-id="5338a-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="5338a-133">このビューでは Razor 構文が使用されています。これは、ASP.NET Web フォームと以前のバージョンの ASP.NET MVC で使用される Web フォームビューエンジンよりも簡潔です。</span><span class="sxs-lookup"><span data-stu-id="5338a-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="5338a-134">Web フォームビューエンジンは ASP.NET MVC 3 でも使用できますが、多くの開発者は、Razor ビューエンジンが ASP.NET MVC の開発に適していることを確認しています。</span><span class="sxs-lookup"><span data-stu-id="5338a-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="5338a-135">最初の3行は、ViewBag を使用してページタイトルを設定します。</span><span class="sxs-lookup"><span data-stu-id="5338a-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="5338a-136">この機能の詳細については、後で詳しく説明しますが、まずテキスト見出しのテキストを更新し、ページを表示してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="5338a-137">次に示すように、&lt;h2&gt; タグを更新して、"これはホームページです" と言います。</span><span class="sxs-lookup"><span data-stu-id="5338a-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="5338a-138">アプリケーションを実行すると、新しいテキストがホームページに表示されることがわかります。</span><span class="sxs-lookup"><span data-stu-id="5338a-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="5338a-139">一般的なサイト要素のレイアウトの使用</span><span class="sxs-lookup"><span data-stu-id="5338a-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="5338a-140">ほとんどの web サイトには、ナビゲーション、フッター、ロゴ画像、スタイルシート参照など、多くのページ間で共有されているコンテンツがあります。Razor ビューエンジンでは、/ビュー/共有フォルダー内に自動的に作成された \_Layout. cshtml という名前のページを使用して、管理が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5338a-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="5338a-141">次に示す内容を表示するには、このフォルダーをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="5338a-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="5338a-142">個々のビューのコンテンツは @RenderBody() コマンドによって表示されます。また、の外部に表示されるすべての共通コンテンツは、\_Layout マークアップに追加できます。</span><span class="sxs-lookup"><span data-stu-id="5338a-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="5338a-143">MVC ミュージックストアには、サイト内のすべてのページのホームページと店舗領域へのリンクを含む共通ヘッダーを含めるようにします。そのため、その @RenderBody() ステートメントのすぐ上のテンプレートに追加します。</span><span class="sxs-lookup"><span data-stu-id="5338a-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="5338a-144">スタイルシートの更新</span><span class="sxs-lookup"><span data-stu-id="5338a-144">Updating the StyleSheet</span></span>

<span data-ttu-id="5338a-145">空のプロジェクトテンプレートには、検証メッセージを表示するために使用されるスタイルだけを含む非常に簡素化された CSS ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5338a-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="5338a-146">このデザイナーでは、サイトのルックアンドフィールを定義するために追加の CSS とイメージを用意しているので、ここで追加します。</span><span class="sxs-lookup"><span data-stu-id="5338a-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="5338a-147">更新された CSS ファイルとイメージは、MvcMusicStore-Assets のコンテンツディレクトリに含まれています。このディレクトリは、 [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="5338a-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="5338a-148">次に示すように、Windows エクスプローラーで両方のファイルを選択し、Visual Web Developer のソリューションのコンテンツフォルダーにドロップします。</span><span class="sxs-lookup"><span data-stu-id="5338a-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="5338a-149">既存のサイトの .css ファイルを上書きするかどうかを確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="5338a-150">[はい] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5338a-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="5338a-151">これで、アプリケーションのコンテンツフォルダーが次のように表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="5338a-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="5338a-152">次に、アプリケーションを実行して、ホームページの変更内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="5338a-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="5338a-153">変更内容を確認してみましょう。ビューテンプレートは標準的な名前付け規則に従っているため、HomeController のインデックスアクションメソッドが見つかり、\Views\Home\Index.cshtmlView テンプレートが表示されています。</span><span class="sxs-lookup"><span data-stu-id="5338a-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="5338a-154">ホームページには、\Views\Home\Index.cshtml view テンプレート内で定義されている簡単なウェルカムメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="5338a-155">ホームページでは \_Layout テンプレートが使用されているため、ウェルカムメッセージは標準のサイト HTML レイアウト内に含まれています。</span><span class="sxs-lookup"><span data-stu-id="5338a-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="5338a-156">モデルを使用してビューに情報を渡す</span><span class="sxs-lookup"><span data-stu-id="5338a-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="5338a-157">ハードコードされた HTML だけを表示するビューテンプレートでは、非常に興味深い web サイトを作成しません。</span><span class="sxs-lookup"><span data-stu-id="5338a-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="5338a-158">動的な web サイトを作成するには、代わりにコントローラーアクションからの情報をビューテンプレートに渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="5338a-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="5338a-159">モデルビューコントローラーパターンでは、モデルという用語は、アプリケーション内のデータを表すオブジェクトを指します。</span><span class="sxs-lookup"><span data-stu-id="5338a-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="5338a-160">多くの場合、モデルオブジェクトはデータベース内のテーブルに対応していますが、これは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5338a-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="5338a-161">ActionResult を返すコントローラーアクションメソッドは、モデルオブジェクトをビューに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="5338a-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="5338a-162">これにより、コントローラーは、応答を生成するために必要なすべての情報を完全にパッケージ化してから、この情報をビューテンプレートに渡して、適切な HTML 応答を生成するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="5338a-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="5338a-163">これは動作を確認することで簡単に理解できるので、始めましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="5338a-164">まず、ストア内のジャンルとアルバムを表すモデルクラスをいくつか作成します。</span><span class="sxs-lookup"><span data-stu-id="5338a-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="5338a-165">まず、Genre クラスを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="5338a-166">プロジェクト内の "モデル" フォルダーを右クリックし、[クラスの追加] オプションを選択して、ファイルに "Genre.cs" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5338a-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="5338a-167">次に、作成されたクラスに "パブリック文字列名" プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="5338a-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="5338a-168">*注: ご注意のために、{get; set;} という表記は、 C#の自動実装プロパティ機能を使用しています。これにより、バッキングフィールドを宣言しなくても、プロパティの利点を得ることができます。*</span><span class="sxs-lookup"><span data-stu-id="5338a-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="5338a-169">次に、同じ手順に従って、タイトルと Genre プロパティを持つアルバムクラス (Album.cs という名前の) を作成します。</span><span class="sxs-lookup"><span data-stu-id="5338a-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="5338a-170">ここで、StoreController を変更して、モデルの動的な情報を表示するビューを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5338a-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="5338a-171">-デモンストレーションの目的で、要求 ID に基づいてアルバムという名前を付けた場合は、次のビューのようにその情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="5338a-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="5338a-172">まず、Store Details (ストアの詳細) アクションを変更することで、1つのアルバムの情報が表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="5338a-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="5338a-173">**StoreControllers**クラスの先頭に "using" ステートメントを追加して、MvcMusicStore 名前空間を含めます。そのため、アルバムクラスを使用するたびに MvcMusicStore を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5338a-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="5338a-174">そのクラスの "using" セクションが次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="5338a-175">次に、HomeController の Index メソッドで行ったように、文字列ではなく ActionResult を返すように Details controller アクションを更新します。</span><span class="sxs-lookup"><span data-stu-id="5338a-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="5338a-176">これで、アルバムオブジェクトをビューに返すロジックを変更できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5338a-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="5338a-177">このチュートリアルの後半では、データベースからデータを取得しますが、ここでは "ダミーデータ" を使用して作業を開始します。</span><span class="sxs-lookup"><span data-stu-id="5338a-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="5338a-178">*注: にC#慣れていない場合は、var を使用すると、アルバム変数が遅延バインディングされることを想定できます。これは適切ではありC#ません。コンパイラは、変数に割り当てられている内容に基づいて型の推論を使用して、アルバムの種類がアルバムであることを判別し、アルバムの種類としてローカルのアルバム変数をコンパイルします。そのため、コンパイル時のチェックと Visual Studio コードエディターのサポートが得られます。*</span><span class="sxs-lookup"><span data-stu-id="5338a-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="5338a-179">ここで、アルバムを使用して HTML 応答を生成するビューテンプレートを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="5338a-180">この作業を行う前に、[ビューの追加] ダイアログで新しく作成したアルバムクラスについて理解できるように、プロジェクトをビルドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5338a-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="5338a-181">プロジェクトをビルドするには、[⇨ Build MvcMusicStore のデバッグ] メニュー項目を選択します (追加のクレジットの場合は、Ctrl + Shift + B のショートカットを使用してプロジェクトをビルドします)。</span><span class="sxs-lookup"><span data-stu-id="5338a-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="5338a-182">サポートクラスを設定したので、ビューテンプレートをビルドする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="5338a-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="5338a-183">詳細メソッド内を右クリックし、[ビューの追加...] を選択します。コンテキストメニューから。</span><span class="sxs-lookup"><span data-stu-id="5338a-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="5338a-184">HomeController の前に作成したのと同じように、新しいビューテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="5338a-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="5338a-185">StoreController から作成するため、既定では \Views\Store\Index.cshtml ファイルに生成されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="5338a-186">以前とは異なり、[厳密に型指定されたビューを作成する] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="5338a-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="5338a-187">次に、[データクラスの表示] ドロップダウンリストで "アルバム" クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="5338a-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="5338a-188">これにより、[ビューの追加] ダイアログボックスが表示され、使用するためにアルバムオブジェクトが渡されることを期待するビューテンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="5338a-189">[追加] ボタンをクリックすると、次のコードを含む \Views\Store\Details.cshtml View テンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="5338a-190">最初の行に注目してください。これは、このビューがアルバムクラスに厳密に型指定されていることを示します。</span><span class="sxs-lookup"><span data-stu-id="5338a-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="5338a-191">Razor ビューエンジンは、そのオブジェクトがアルバムオブジェクトに渡されたことを認識します。これにより、モデルプロパティに簡単にアクセスできるようになります。また、Visual Web Developer エディターで IntelliSense を利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="5338a-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="5338a-192">&lt;h2&gt; タグを更新して、次のように、その行を変更することでアルバムの Title プロパティを表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="5338a-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="5338a-193">@Model キーワードの後にピリオドを入力すると、IntelliSense がトリガーされることに注意してください。これは、アルバムクラスでサポートされるプロパティとメソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="5338a-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="5338a-194">ここで、プロジェクトを再実行し、/ストア/ページの URL にアクセスしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="5338a-195">次のようなアルバムの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="5338a-196">次に、ストアの参照アクションメソッドに対して同様の更新を行います。</span><span class="sxs-lookup"><span data-stu-id="5338a-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="5338a-197">メソッドを更新して ActionResult を返し、メソッドのロジックを変更して、新しい Genre オブジェクトを作成し、それをビューに返すようにします。</span><span class="sxs-lookup"><span data-stu-id="5338a-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="5338a-198">Browse メソッドを右クリックし、[ビューの追加...] を選択します。コンテキストメニューから、厳密に型指定されたビューを追加して、Genre クラスに厳密に型指定されたを追加します。</span><span class="sxs-lookup"><span data-stu-id="5338a-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="5338a-199">ビューコード (/Views/Store/Browse.cshtml) の &lt;h2&gt; 要素を更新して、ジャンル情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5338a-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="5338a-200">次に、プロジェクトを再実行して、/ストアに移動してみましょう。Genre = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="5338a-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="5338a-201">次のように、参照ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="5338a-202">最後に、ストア**インデックス**のアクションメソッドとビューを少し複雑に更新して、ストア内のすべてのジャンルの一覧を表示してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5338a-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="5338a-203">これを行うには、1つのジャンルだけではなく、モデルオブジェクトとしてジャンルのリストを使用します。</span><span class="sxs-lookup"><span data-stu-id="5338a-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="5338a-204">ストアインデックスアクションメソッドを右クリックし、[前のビューを追加] を選択して、モデルクラスとして [ジャンル] を選択し、[追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="5338a-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="5338a-205">まず、@model 宣言を変更して、ビューが1つだけではなく複数の Genre オブジェクトを必要とすることを示します。</span><span class="sxs-lookup"><span data-stu-id="5338a-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="5338a-206">/ストアの最初の行を次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="5338a-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="5338a-207">これにより、複数の Genre オブジェクトを保持できるモデルオブジェクトを操作することを Razor ビューエンジンに通知します。</span><span class="sxs-lookup"><span data-stu-id="5338a-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="5338a-208">一般的なものであるため、IEnumerable&lt;Genre&gt;&lt;&gt; を使用しています。これは一般に、IEnumerable インターフェイスをサポートする任意のオブジェクト型に後でモデルの種類を変更できるためです。</span><span class="sxs-lookup"><span data-stu-id="5338a-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="5338a-209">次に、次の「完成したビューコード」に示されているように、モデル内の Genre オブジェクトをループ処理します。</span><span class="sxs-lookup"><span data-stu-id="5338a-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="5338a-210">このコードを入力すると IntelliSense が完全にサポートされるので、「@Model」と入力すると、</span><span class="sxs-lookup"><span data-stu-id="5338a-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="5338a-211">種類が Genre の IEnumerable でサポートされているすべてのメソッドとプロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="5338a-212">"Foreach" ループ内では、Visual Web Developer は各項目の種類が Genre であることを認識しているため、ジャンルの種類ごとに IntelliSense が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="5338a-213">次に、スキャフォールディング機能は Genre オブジェクトを調べ、それぞれに Name プロパティがあることを確認したので、ループ処理して出力します。また、個々の項目に対する編集、詳細、および削除のリンクも生成します。</span><span class="sxs-lookup"><span data-stu-id="5338a-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="5338a-214">この機能については、ストアマネージャーで後ほど説明しますが、ここでは単純なリストを使用します。</span><span class="sxs-lookup"><span data-stu-id="5338a-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="5338a-215">アプリケーションを実行して、[ストア] を参照すると、カウントとジャンルの一覧の両方が表示されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="5338a-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="5338a-216">ページ間のリンクの追加</span><span class="sxs-lookup"><span data-stu-id="5338a-216">Adding Links between pages</span></span>

<span data-ttu-id="5338a-217">現在、ジャンルを一覧表示する/ストア URL では、ジャンル名が単にプレーンテキストとして一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="5338a-218">これを変更して、プレーンテキストではなく、ジャンル名を適切な/Store/browse URL にリンクさせます。これにより、"Disco" のような音楽のジャンルをクリックすると、"Disco" に移動します。</span><span class="sxs-lookup"><span data-stu-id="5338a-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="5338a-219">次のようなコードを使用して、これらのリンクを出力するように \Views\Store\Index.cshtml View テンプレートを更新することもできます **(これを入力しないでください)** 。</span><span class="sxs-lookup"><span data-stu-id="5338a-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="5338a-220">これは機能しますが、ハードコーディングされた文字列に依存しているため、後で問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5338a-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="5338a-221">たとえば、コントローラーの名前を変更する場合は、コードを検索して、更新する必要があるリンクを探す必要があります。</span><span class="sxs-lookup"><span data-stu-id="5338a-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="5338a-222">別の方法として、HTML ヘルパーメソッドを利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="5338a-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="5338a-223">ASP.NET MVC には、このようなさまざまな一般的なタスクを実行するために、ビューテンプレートコードから使用できる HTML ヘルパーメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5338a-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="5338a-224">Html.actionlink () ヘルパーメソッドは特に便利であり、&gt; リンクの HTML &lt;を簡単に作成できます。また、URL パスが適切に URL エンコードされているかどうかなど、面倒な詳細も考慮します。</span><span class="sxs-lookup"><span data-stu-id="5338a-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="5338a-225">Html.actionlink () には、リンクに必要な量の情報を指定できるように、いくつかの異なるオーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="5338a-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="5338a-226">最も単純なケースでは、クライアントでハイパーリンクがクリックされたときに、リンクテキストとアクションメソッドを指定するだけです。</span><span class="sxs-lookup"><span data-stu-id="5338a-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="5338a-227">たとえば、次の呼び出しを使用して、ストアの詳細ページの "/Store/" Index () メソッドにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="5338a-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="5338a-228">*注: この場合、現在のビューを表示しているのと同じコントローラー内の別のアクションにリンクするだけなので、コントローラー名を指定する必要はありませんでした。*</span><span class="sxs-lookup"><span data-stu-id="5338a-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="5338a-229">参照ページへのリンクではパラメーターを渡す必要があるので、次の3つのパラメーターを受け取る Html.actionlink メソッドの別のオーバーロードを使用します。</span><span class="sxs-lookup"><span data-stu-id="5338a-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="5338a-230">ジャンル名を表示するリンクテキスト</span><span class="sxs-lookup"><span data-stu-id="5338a-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="5338a-231">コントローラーアクション名 (参照)</span><span class="sxs-lookup"><span data-stu-id="5338a-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="5338a-232">ルートパラメーターの値。名前 (ジャンル) と値 (ジャンル名) の両方を指定します。</span><span class="sxs-lookup"><span data-stu-id="5338a-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="5338a-233">これらのリンクをまとめて、ストアインデックスビューへのリンクを次のように記述します。</span><span class="sxs-lookup"><span data-stu-id="5338a-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="5338a-234">ここでプロジェクトをもう一度実行し、/Store/URL にアクセスすると、ジャンルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5338a-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="5338a-235">各ジャンルはハイパーリンクです。クリックすると、/Store/Browse? genre = *[genre]* URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="5338a-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="5338a-236">ジャンルリストの HTML は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5338a-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="5338a-237">[前へ](mvc-music-store-part-2.md)
> [次へ](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="5338a-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
