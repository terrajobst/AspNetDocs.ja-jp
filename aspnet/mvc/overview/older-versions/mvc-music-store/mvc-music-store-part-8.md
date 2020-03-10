---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 'パート 8: Ajax 更新プログラムを使用したショッピングカート |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート8では、Ajax の更新プログラムを使用したショッピングカートについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433516"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="4664b-104">パート 8: Ajax 更新プログラムを使用したショッピングカート</span><span class="sxs-lookup"><span data-stu-id="4664b-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="4664b-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="4664b-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="4664b-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="4664b-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="4664b-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="4664b-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="4664b-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="4664b-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="4664b-109">パート8では、Ajax の更新プログラムを使用したショッピングカートについて説明します。</span><span class="sxs-lookup"><span data-stu-id="4664b-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="4664b-110">ユーザーは登録せずにカートにアルバムを配置することができますが、チェックアウトを完了するにはゲストとして登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4664b-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="4664b-111">ショッピングとチェックアウトのプロセスは2つのコントローラーに分けられます。 ShoppingCart コントローラーは、項目をカートに匿名で追加できるようにし、チェックアウトプロセスを処理するチェックアウトコントローラーです。</span><span class="sxs-lookup"><span data-stu-id="4664b-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="4664b-112">このセクションのショッピングカートから始めて、次のセクションでチェックアウトプロセスを作成します。</span><span class="sxs-lookup"><span data-stu-id="4664b-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="4664b-113">カート、注文、および OrderDetail モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="4664b-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="4664b-114">ショッピングカートとチェックアウトプロセスでは、いくつかの新しいクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4664b-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="4664b-115">[モデル] フォルダーを右クリックし、次のコードを使用してカートクラス (Cart.cs) を追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="4664b-116">このクラスは、これまでに使用した他のクラスと非常によく似ています。ただし、RecordId プロパティの [Key] 属性は例外です。</span><span class="sxs-lookup"><span data-stu-id="4664b-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="4664b-117">カートの項目には、匿名ショッピングを許可する CartID という名前の文字列識別子がありますが、テーブルには RecordId という整数の主キーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4664b-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="4664b-118">慣例として、Entity Framework コードでは、買い物かごという名前のテーブルの主キーが CartId または ID のいずれかであることを前提としていますが、必要に応じて、注釈やコードを使用して簡単にオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="4664b-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="4664b-119">この例では、Entity Framework コードで単純な規則を使用する方法について説明していますが、これらの規則に違反している場合は、これらの規則によって制限されません。</span><span class="sxs-lookup"><span data-stu-id="4664b-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="4664b-120">次に、次のコードを使用して Order クラス (Order.cs) を追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="4664b-121">このクラスは、注文の概要および配信情報を追跡します。</span><span class="sxs-lookup"><span data-stu-id="4664b-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="4664b-122">まだ作成されていないクラスに依存する OrderDetails ナビゲーションプロパティがあるため、**まだコンパイルされません**。</span><span class="sxs-lookup"><span data-stu-id="4664b-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="4664b-123">ここで、OrderDetail.cs という名前のクラスを追加して、次のコードを追加して修正してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4664b-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="4664b-124">これらの新しいモデルクラスを公開する DbSets を追加するために、MusicStoreEntities クラスに対して1つの最後の更新を行います。これには、Dbsets&lt;アーティスト&gt;も含まれます。</span><span class="sxs-lookup"><span data-stu-id="4664b-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="4664b-125">更新された MusicStoreEntities クラスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4664b-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="4664b-126">ショッピングカートのビジネスロジックを管理する</span><span class="sxs-lookup"><span data-stu-id="4664b-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="4664b-127">次に、[モデル] フォルダーに ShoppingCart クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="4664b-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="4664b-128">ShoppingCart モデルは、カートテーブルへのデータアクセスを処理します。</span><span class="sxs-lookup"><span data-stu-id="4664b-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="4664b-129">さらに、ショッピングカートのアイテムを追加および削除するために、ビジネスロジックを処理します。</span><span class="sxs-lookup"><span data-stu-id="4664b-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="4664b-130">ショッピングカートに商品を追加するだけで、アカウントにサインアップするようにユーザーに要求しないので、ユーザーがショッピングカートにアクセスするときに、ユーザーに対して一時的な一意識別子 (GUID を使用) またはグローバル一意識別子を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="4664b-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="4664b-131">この ID は、ASP.NET Session クラスを使用して格納します。</span><span class="sxs-lookup"><span data-stu-id="4664b-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="4664b-132">*注: ASP.NET セッションは、ユーザー固有の情報を格納するのに便利な場所であり、サイトから離れた後に期限切れになります。より大きなサイトでは、セッション状態の誤用によってパフォーマンスが低下する可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="4664b-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="4664b-133">ShoppingCart クラスは、次のメソッドを公開します。</span><span class="sxs-lookup"><span data-stu-id="4664b-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="4664b-134">**Addtocart**は、アルバムをパラメーターとして受け取り、それをユーザーのカートに追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="4664b-135">カートテーブルでは、各アルバムの数量が追跡されるため、必要に応じて新しい行を作成するロジックや、ユーザーが既にアルバムのコピーを注文している場合は数量を増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="4664b-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="4664b-136">**Removefromcart**は、アルバム ID を取得し、ユーザーのカートから削除します。</span><span class="sxs-lookup"><span data-stu-id="4664b-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="4664b-137">カートにアルバムのコピーが1つしかない場合、その行は削除されます。</span><span class="sxs-lookup"><span data-stu-id="4664b-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="4664b-138">**Emptycart**は、ユーザーのショッピングカートからすべての項目を削除します。</span><span class="sxs-lookup"><span data-stu-id="4664b-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="4664b-139">**GetCartItems**は、表示または処理のために CartItems の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="4664b-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="4664b-140">**GetCount**は、ユーザーがショッピングカートに持っているアルバムの合計数を取得します。</span><span class="sxs-lookup"><span data-stu-id="4664b-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="4664b-141">**Gettotal**は、カート内のすべての品目の総コストを計算します。</span><span class="sxs-lookup"><span data-stu-id="4664b-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="4664b-142">**Createorder**は、チェックアウトフェーズ中にショッピングカートを注文に変換します。</span><span class="sxs-lookup"><span data-stu-id="4664b-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="4664b-143">**Getcart**は、コントローラーがカートオブジェクトを取得できるようにする静的メソッドです。</span><span class="sxs-lookup"><span data-stu-id="4664b-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="4664b-144">**Getcartid**メソッドを使用して、ユーザーのセッションからの cartid の読み取りを処理します。</span><span class="sxs-lookup"><span data-stu-id="4664b-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="4664b-145">GetCartId メソッドでは HttpContextBase が必要であるため、ユーザーのセッションからユーザーの CartId を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="4664b-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="4664b-146">完全な**ShoppingCart クラス**を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4664b-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="4664b-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="4664b-147">ViewModels</span></span>

<span data-ttu-id="4664b-148">ショッピングカートコントローラーは、モデルオブジェクトに完全にマップされない複雑な情報をビューに伝達する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4664b-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="4664b-149">ビューに合わせてモデルを変更する必要はありません。モデルクラスは、ユーザーインターフェイスではなく、ドメインを表す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4664b-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="4664b-150">1つの解決策は、ストアマネージャーのドロップダウン情報の場合と同様に、ViewBag クラスを使用して情報をビューに渡すことですが、ViewBag を介して大量の情報を渡すと管理が困難になります。</span><span class="sxs-lookup"><span data-stu-id="4664b-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="4664b-151">これを解決するには、*ビューモデル*パターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="4664b-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="4664b-152">このパターンを使用すると、特定のビューシナリオ用に最適化された、厳密に型指定されたクラスを作成し、ビューテンプレートに必要な動的な値/コンテンツのプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="4664b-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="4664b-153">次に、コントローラークラスを設定して、ビューに最適化されたこれらのクラスをビューテンプレートに渡して使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="4664b-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="4664b-154">これにより、ビューテンプレート内でタイプセーフ、コンパイル時チェック、およびエディター IntelliSense が有効になります。</span><span class="sxs-lookup"><span data-stu-id="4664b-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="4664b-155">ショッピングカートコントローラーで使用する2つのビューモデルを作成します。 ShoppingCartViewModel はユーザーのショッピングカートの内容を保持し、ユーザーが何かを削除したときに、ShoppingCartRemoveViewModel を使用して確認情報を表示します。カートから</span><span class="sxs-lookup"><span data-stu-id="4664b-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="4664b-156">プロジェクトのルートに新しい Viewmodel フォルダーを作成して、整理しておきましょう。</span><span class="sxs-lookup"><span data-stu-id="4664b-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="4664b-157">プロジェクトを右クリックし、[追加]、[新しいフォルダー] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="4664b-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="4664b-158">フォルダーに Viewmodel という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="4664b-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="4664b-159">次に、Viewmodel フォルダーに ShoppingCartViewModel クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="4664b-160">2つのプロパティがあります。カート項目のリストと、カート内のすべての品目の合計価格を保持する10進値です。</span><span class="sxs-lookup"><span data-stu-id="4664b-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="4664b-161">次の4つのプロパティを使用して、ShoppingCartRemoveViewModel を Viewmodel フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="4664b-162">ショッピングカートコントローラー</span><span class="sxs-lookup"><span data-stu-id="4664b-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="4664b-163">ショッピングカートコントローラーには主に3つの目的があります。カートへのアイテムの追加、カートからのアイテムの削除、およびカート内のアイテムの表示です。</span><span class="sxs-lookup"><span data-stu-id="4664b-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="4664b-164">ここで作成した3つのクラス (ShoppingCartViewModel、ShoppingCartRemoveViewModel、および ShoppingCart) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4664b-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="4664b-165">StoreController と StoreManagerController のように、MusicStoreEntities のインスタンスを保持するフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="4664b-166">空のコントローラーテンプレートを使用して、新しいショッピングカートコントローラーをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="4664b-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="4664b-167">完全な ShoppingCart コントローラーを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4664b-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="4664b-168">インデックスとコントローラーの追加アクションは非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="4664b-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="4664b-169">Remove と CartSummary controller アクションは2つの特殊なケースを処理します。これについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="4664b-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="4664b-170">JQuery を使用した Ajax の更新</span><span class="sxs-lookup"><span data-stu-id="4664b-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="4664b-171">次に、ShoppingCartViewModel に厳密に型指定されたショッピングカートのインデックスページを作成し、前と同じ方法を使用してリストビューテンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="4664b-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="4664b-172">ただし、Html.actionlink を使用してカートから項目を削除するのではなく、jQuery を使用して、このビュー内のすべてのリンク (HTML クラス RemoveLink を含む) に対して click イベントを "接続" します。</span><span class="sxs-lookup"><span data-stu-id="4664b-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="4664b-173">フォームを送信するのではなく、この click イベントハンドラーは、RemoveFromCart コントローラーアクションへの AJAX コールバックを行います。</span><span class="sxs-lookup"><span data-stu-id="4664b-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="4664b-174">RemoveFromCart は、JSON でシリアル化された結果を返します。この結果、jQuery コールバックは次に jQuery を使用して、このページに対して4つのクイック更新を解析して実行します。</span><span class="sxs-lookup"><span data-stu-id="4664b-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="4664b-175">削除されたアルバムを一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="4664b-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="4664b-176">ヘッダーのカート数を更新します</span><span class="sxs-lookup"><span data-stu-id="4664b-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="4664b-177">ユーザーに更新メッセージを表示します</span><span class="sxs-lookup"><span data-stu-id="4664b-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="4664b-178">カートの合計価格を更新します。</span><span class="sxs-lookup"><span data-stu-id="4664b-178">Updates the cart total price</span></span>

<span data-ttu-id="4664b-179">削除シナリオは、インデックスビュー内の Ajax コールバックによって処理されるため、RemoveFromCart アクションの追加のビューは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="4664b-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="4664b-180">/ShoppingCart/Index ビューの完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4664b-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="4664b-181">これをテストするには、ショッピングカートに商品を追加できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4664b-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="4664b-182">**店舗の詳細** ビューを更新して、カートに追加 ボタンを含めます。</span><span class="sxs-lookup"><span data-stu-id="4664b-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="4664b-183">ここでは、このビューを最後に更新した後に追加したアルバムの追加情報 (ジャンル、アーティスト、価格、アルバムアート) を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4664b-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="4664b-184">次に示すように、更新されたストアの詳細ビューのコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4664b-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="4664b-185">これで、ストアをクリックして、ショッピングカートに対するアルバムの追加と削除をテストできます。</span><span class="sxs-lookup"><span data-stu-id="4664b-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="4664b-186">アプリケーションを実行し、ストアインデックスを参照します。</span><span class="sxs-lookup"><span data-stu-id="4664b-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="4664b-187">次に、ジャンルをクリックして、アルバムの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="4664b-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="4664b-188">アルバムのタイトルをクリックすると、[カートに追加] ボタンを含む、更新されたアルバムの詳細ビューが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="4664b-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="4664b-189">[カートに追加] ボタンをクリックすると、ショッピングカートのインデックスビューがショッピングカートの概要リストと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4664b-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="4664b-190">ショッピングカートを読み込んだ後、[カートから削除] リンクをクリックすると、お客様のショッピングカートの Ajax 更新を確認できます。</span><span class="sxs-lookup"><span data-stu-id="4664b-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="4664b-191">登録されていないユーザーがカートに項目を追加できるようにする、実用的なショッピングカートを構築しました。</span><span class="sxs-lookup"><span data-stu-id="4664b-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="4664b-192">次のセクションでは、チェックアウトプロセスの登録と完了を許可します。</span><span class="sxs-lookup"><span data-stu-id="4664b-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4664b-193">[前へ](mvc-music-store-part-7.md)
> [次へ](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="4664b-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
