---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 'パート 4: 製品の一覧表示 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート4では、GridView で製品を一覧表示する方法について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457282"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="d1a7b-104">パート 4: 製品の一覧表示</span><span class="sxs-lookup"><span data-stu-id="d1a7b-104">Part 4: Listing Products</span></span>

<span data-ttu-id="d1a7b-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d1a7b-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="d1a7b-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="d1a7b-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="d1a7b-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="d1a7b-109">パート4では、GridView コントロールで製品を一覧表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="d1a7b-110">GridView コントロールを使用した製品の一覧表示</span><span class="sxs-lookup"><span data-stu-id="d1a7b-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="d1a7b-111">ソリューションを右クリックし、[追加]、[新しい項目] の順に選択して、製品リストの .aspx ページの実装を開始しましょう。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="d1a7b-112">[マスターページを使用した Web フォーム] を選択し、製品のリスト .aspx のページ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="d1a7b-113">[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="d1a7b-114">次に、[スタイル] フォルダーを選択します。このフォルダーは、[フォルダーの内容] ウィンドウから選択します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="d1a7b-115">[Ok] をクリックしてページを作成します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="d1a7b-116">次に示すように、データベースに製品データが入力されます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="d1a7b-117">ページが作成された後、もう一度エンティティデータソースを使用してその製品データにアクセスしますが、この場合は、Product エンティティを選択する必要があります。また、返される項目を、選択したカテゴリの項目のみに制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="d1a7b-118">これを実現するには、WHERE 句を自動生成するように EntityDataSource に指示し、where-object パラメーターを指定します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="d1a7b-119">「製品カテゴリメニュー」でメニュー項目を作成したときに、各リンクの QueryString に CategoryID を追加して、リンクを動的に構築したことを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="d1a7b-120">このクエリ文字列パラメーターから WHERE パラメーターを派生させるように、エンティティデータソースに指示します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="d1a7b-121">次に、製品の一覧を表示するように ListView コントロールを構成します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="d1a7b-122">最適なショッピング体験を作成するには、ListVew に表示される個々の製品ごとに簡潔な機能をいくつか圧縮します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="d1a7b-123">製品名は、製品の詳細ビューへのリンクになります。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="d1a7b-124">製品の価格が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="d1a7b-125">製品のイメージが表示され、アプリケーションのカタログイメージディレクトリからイメージが動的に選択されます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="d1a7b-126">特定の製品をすぐにショッピングカートに追加するためのリンクを含めます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="d1a7b-127">ListView コントロールインスタンスのマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="d1a7b-128">表示されている製品ごとに複数のリンクを動的に構築しています。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="d1a7b-129">また、独自の新しいページをテストする前に、次のように製品カタログイメージのディレクトリ構造を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="d1a7b-130">製品イメージにアクセスできるようになったら、製品リストページをテストできます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="d1a7b-131">サイトのホームページから、カテゴリ一覧のリンクの1つをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="d1a7b-132">次に、ProductDetails .aspx ページと AddToCart 機能を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="d1a7b-133">先ほどと同じように、[ファイル&gt;新規] を使用して、サイトマスターページを使用してページ名 ProductDetails .aspx を作成します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="d1a7b-134">次に、EntityDataSource コントロールを使用してデータベース内の特定の製品レコードにアクセスします。 ASP.NET FormView コントロールを使用して、次のように製品データを表示します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="d1a7b-135">書式設定が少し楽しいものであるかどうかは気にしないでください。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="d1a7b-136">上のマークアップは、後で実装するいくつかの機能について、表示レイアウトの中にスペースを残します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="d1a7b-137">ショッピングカートは、アプリケーション内でより複雑なロジックを表します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="d1a7b-138">作業を開始するには、MyShoppingCart という名前のページを作成するために、ファイル&gt;New を使用します。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="d1a7b-139">ShoppingCart という名前は選択していないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="d1a7b-140">このデータベースには、"ShoppingCart" という名前のテーブルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="d1a7b-141">Entity Data Model 生成されると、データベース内の各テーブルに対してクラスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="d1a7b-142">したがって、Entity Data Model によって、"ShoppingCart" という名前のエンティティクラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="d1a7b-143">このモデルを編集して、ショッピングカートの実装にその名前を使用できるようにすることも、ニーズに合わせて拡張することもできますが、競合を回避する名前を選択するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="d1a7b-144">また、簡単なショッピングカートを作成し、ショッピングカートの表示でショッピングカートのロジックを埋め込むことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="d1a7b-145">また、まったく別のビジネス層にショッピングカートを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="d1a7b-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1a7b-146">[前へ](tailspin-spyworks-part-3.md)
> [次へ](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="d1a7b-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
