---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 'パート 10: ナビゲーションとサイト設計の最終更新、結論 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート10では、ナビゲーションと...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433612"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="daea5-104">パート 10: ナビゲーションとサイト設計の最終更新、結論</span><span class="sxs-lookup"><span data-stu-id="daea5-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="daea5-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="daea5-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="daea5-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="daea5-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="daea5-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="daea5-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="daea5-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="daea5-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="daea5-109">パート10では、ナビゲーションとサイト設計の最終的な更新について説明します。</span><span class="sxs-lookup"><span data-stu-id="daea5-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="daea5-110">サイトの主要な機能はすべて完了しましたが、サイトのナビゲーション、ホームページ、ストアの参照ページに追加できる機能がまだいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="daea5-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="daea5-111">ショッピングカートの概要部分ビューの作成</span><span class="sxs-lookup"><span data-stu-id="daea5-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="daea5-112">サイト全体のユーザーのショッピングカートに含まれる項目の数を公開したいと考えています。</span><span class="sxs-lookup"><span data-stu-id="daea5-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="daea5-113">これを簡単に実装するには、部分ビューを作成します。これは、サイトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="daea5-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="daea5-114">前に示したように、ShoppingCart コントローラーには、部分ビューを返す CartSummary action メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="daea5-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="daea5-115">CartSummary 部分ビューを作成するには、Views/ShoppingCart フォルダーを右クリックし、[ビューの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="daea5-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="daea5-116">ビューに CartSummary という名前を付け、次に示すように [部分ビューを作成する] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="daea5-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="daea5-117">CartSummary 部分ビューは非常に単純です。これは、カート内の項目の数を表示する ShoppingCart Index ビューへのリンクです。</span><span class="sxs-lookup"><span data-stu-id="daea5-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="daea5-118">CartSummary の完全なコードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="daea5-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="daea5-119">サイトマスターを含む、サイト内の任意のページに部分ビューを含めることができます。これには、Html の RenderAction メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="daea5-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="daea5-120">RenderAction を実行するには、次のようにアクション名 ("CartSummary") とコントローラー名 ("ShoppingCart") を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="daea5-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="daea5-121">これをサイトレイアウトに追加する前に、ジャンルメニューも作成します。これにより、すべてのサイトが一度に更新されます。</span><span class="sxs-lookup"><span data-stu-id="daea5-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="daea5-122">ジャンルメニュー部分ビューの作成</span><span class="sxs-lookup"><span data-stu-id="daea5-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="daea5-123">ストア内で利用可能なすべてのジャンルを一覧表示する Genre メニューを追加することで、ユーザーがストア内をより簡単に移動できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="daea5-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="daea5-124">同じ手順を実行して、[GenreMenu] 部分ビューも作成します。次に、両方をサイトマスターに追加します。</span><span class="sxs-lookup"><span data-stu-id="daea5-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="daea5-125">まず、次の GenreMenu コントローラーアクションを StoreController に追加します。</span><span class="sxs-lookup"><span data-stu-id="daea5-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="daea5-126">この操作により、部分ビューに表示されるジャンルの一覧が返されます。これは次に作成します。</span><span class="sxs-lookup"><span data-stu-id="daea5-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="daea5-127">*メモ: このコントローラーアクションに [ChildActionOnly] 属性を追加しました。これは、このアクションを部分ビューからのみ使用することを示します。この属性を設定すると、コントローラーの操作を実行できなくなります。これは部分ビューには必要ありませんが、コントローラーのアクションが意図したとおりに使用されていることを確認する必要があるため、お勧めします。また、ビューではなく PartialView も返されます。これにより、ビューエンジンは、他のビューに含まれているため、このビューのレイアウトを使用しないことを確認できます。*</span><span class="sxs-lookup"><span data-stu-id="daea5-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="daea5-128">GenreMenu controller アクションを右クリックし、次に示すように Genre view データクラスを使用して厳密に型指定された GenreMenu という名前の部分ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="daea5-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="daea5-129">次のように、順序付けられていないリストを使用して項目を表示するように、GenreMenu 部分ビューのビューコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="daea5-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="daea5-130">部分ビューを表示するようにサイトレイアウトを更新しています</span><span class="sxs-lookup"><span data-stu-id="daea5-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="daea5-131">Html の RenderAction () を呼び出すことによって、部分ビューをサイトレイアウト (/ビュー/Shared/\_Layout) に追加できます。</span><span class="sxs-lookup"><span data-stu-id="daea5-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="daea5-132">次に示すように、との両方に追加のマークアップを追加して表示します。</span><span class="sxs-lookup"><span data-stu-id="daea5-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="daea5-133">アプリケーションを実行すると、左側のナビゲーション領域にジャンルが表示され、[カートの概要] が上部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="daea5-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="daea5-134">ストアの参照ページに更新する</span><span class="sxs-lookup"><span data-stu-id="daea5-134">Update to the Store Browse page</span></span>

<span data-ttu-id="daea5-135">ストアの参照ページは機能していますが、正しくありません。</span><span class="sxs-lookup"><span data-stu-id="daea5-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="daea5-136">ページを更新して、次のようにビューコード (/Views/Store/Browse.cshtml にあります) を更新することにより、アルバムがより適切なレイアウトで表示されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="daea5-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="daea5-137">ここでは、Html.actionlink ではなく、Url を使用します。これにより、アルバムのアートワークを含めるための特別な書式設定をリンクに適用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="daea5-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="daea5-138">*注: これらのアルバムの一般的なアルバムカバーを表示しています。この情報はデータベースに保存され、ストアマネージャーを使用して編集できます。独自のアートワークを追加できるようになります。*</span><span class="sxs-lookup"><span data-stu-id="daea5-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="daea5-139">ジャンルを参照すると、アルバムのアートワークがグリッドに表示されます。</span><span class="sxs-lookup"><span data-stu-id="daea5-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="daea5-140">ホームページを更新して、売上の多いアルバムを表示する</span><span class="sxs-lookup"><span data-stu-id="daea5-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="daea5-141">売上を増やすために、ホームページで上位の販売アルバムを機能させたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="daea5-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="daea5-142">これを処理するために、HomeController にいくつかの更新を行い、追加のグラフィックスも追加します。</span><span class="sxs-lookup"><span data-stu-id="daea5-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="daea5-143">まず、アルバムクラスにナビゲーションプロパティを追加します。これにより、EntityFramework が関連付けられていることを認識します。</span><span class="sxs-lookup"><span data-stu-id="daea5-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="daea5-144">**アルバム**クラスの最後の数行は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="daea5-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="daea5-145">*注: これには、using ステートメントを追加して、system.string 名前空間を取り込む必要があります。*</span><span class="sxs-lookup"><span data-stu-id="daea5-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="daea5-146">まず、他のコントローラーと同様に、ステートメントを使用して storeDB フィールドと MvcMusicStore を追加します。</span><span class="sxs-lookup"><span data-stu-id="daea5-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="daea5-147">次に、HomeController に次のメソッドを追加します。このメソッドは、OrderDetails に従って上位の販売アルバムを検索するために、データベースにクエリを行います。</span><span class="sxs-lookup"><span data-stu-id="daea5-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="daea5-148">これは、コントローラーアクションとして使用できないようにするためのプライベートメソッドです。</span><span class="sxs-lookup"><span data-stu-id="daea5-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="daea5-149">わかりやすくするために HomeController に追加していますが、ビジネスロジックは、必要に応じて別のサービスクラスに移動することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="daea5-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="daea5-150">その後、インデックスコントローラーアクションを更新して、上位5つの販売アルバムに対してクエリを実行し、ビューに返すことができます。</span><span class="sxs-lookup"><span data-stu-id="daea5-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="daea5-151">更新された HomeController の完全なコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="daea5-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="daea5-152">最後に、モデルの種類を更新してアルバムリストを下部に追加することで、アルバムの一覧を表示できるように、ホームインデックスビューを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="daea5-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="daea5-153">この機会に、見出しとプロモーションセクションもページに追加します。</span><span class="sxs-lookup"><span data-stu-id="daea5-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="daea5-154">アプリケーションを実行すると、更新されたホームページが表示され、売上が多いアルバムとプロモーションメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="daea5-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="daea5-155">まとめ</span><span class="sxs-lookup"><span data-stu-id="daea5-155">Conclusion</span></span>

<span data-ttu-id="daea5-156">ASP.NET MVC を使用すると、データベースアクセス、メンバーシップ、AJAX などを使用して、洗練された web サイトを簡単に作成できることがわかりました。</span><span class="sxs-lookup"><span data-stu-id="daea5-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="daea5-157">非常に迅速です。</span><span class="sxs-lookup"><span data-stu-id="daea5-157">pretty quickly.</span></span> <span data-ttu-id="daea5-158">このチュートリアルでは、独自の ASP.NET MVC アプリケーションの構築を開始するために必要なツールが用意されています。</span><span class="sxs-lookup"><span data-stu-id="daea5-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="daea5-159">[[戻る]](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="daea5-159">[Previous](mvc-music-store-part-9.md)</span></span>
