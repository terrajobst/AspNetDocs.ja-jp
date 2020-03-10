---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 'パート 9: 登録とチェックアウト |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート9では、登録とチェックアウトについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450898"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="cb017-104">パート 9: 登録とチェックアウト</span><span class="sxs-lookup"><span data-stu-id="cb017-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="cb017-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="cb017-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="cb017-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="cb017-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="cb017-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="cb017-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="cb017-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="cb017-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="cb017-109">パート9では、登録とチェックアウトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="cb017-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="cb017-110">このセクションでは、顧客の住所と支払い情報を収集する CheckoutController を作成します。</span><span class="sxs-lookup"><span data-stu-id="cb017-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="cb017-111">ユーザーは、チェックアウトの前にサイトに登録する必要があるため、このコントローラーには承認が必要です。</span><span class="sxs-lookup"><span data-stu-id="cb017-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="cb017-112">ユーザーは、[チェックアウト] ボタンをクリックして、ショッピングカートからチェックアウトプロセスに移動します。</span><span class="sxs-lookup"><span data-stu-id="cb017-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="cb017-113">ユーザーがログインしていない場合は、メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="cb017-114">ログインが成功すると、ユーザーにはアドレスと支払いのビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="cb017-115">フォームに入力して注文を送信すると、注文確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="cb017-116">存在しない順序を表示しようとしたか、または属していない順序を表示しようとすると、エラービューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="cb017-117">ショッピングカートの移行</span><span class="sxs-lookup"><span data-stu-id="cb017-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="cb017-118">ショッピングプロセスは匿名ですが、ユーザーが [チェックアウト] ボタンをクリックすると、登録とログインが必要になります。</span><span class="sxs-lookup"><span data-stu-id="cb017-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="cb017-119">ユーザーは、訪問の間にショッピングカートの情報を保持することを期待しています。そのため、登録またはログインが完了したら、ショッピングカートの情報をユーザーに関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb017-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="cb017-120">ShoppingCart クラスには、現在のカート内のすべての項目をユーザー名と関連付けるメソッドが既に用意されているため、これは実際には非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="cb017-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="cb017-121">ユーザーが登録またはログインを完了したときに、このメソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb017-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="cb017-122">メンバーシップと承認を設定したときに追加した**Accountcontroller**クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="cb017-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="cb017-123">MvcMusicStore を参照する using ステートメントを追加し、次の MigrateShoppingCart メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="cb017-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="cb017-124">次に、次に示すように、ユーザーが検証された後に MigrateShoppingCart を呼び出すように、ログオン post アクションを変更します。</span><span class="sxs-lookup"><span data-stu-id="cb017-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="cb017-125">ユーザーアカウントが正常に作成された直後に、Register post アクションに対して同じ変更を行います。</span><span class="sxs-lookup"><span data-stu-id="cb017-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="cb017-126">これで完了です。登録またはログインが成功すると、匿名ショッピングカートが自動的にユーザーアカウントに転送されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cb017-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="cb017-127">CheckoutController の作成</span><span class="sxs-lookup"><span data-stu-id="cb017-127">Creating the CheckoutController</span></span>

<span data-ttu-id="cb017-128">Controllers フォルダーを右クリックし、空のコントローラーテンプレートを使用して、CheckoutController という名前のプロジェクトに新しいコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="cb017-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="cb017-129">まず、ユーザーにチェックアウトの前に登録するように要求するために、コントローラークラス宣言の上に承認属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="cb017-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="cb017-130">*注: これは、StoreManagerController に対して以前に行った変更に似ていますが、その場合、承認属性では、ユーザーが管理者ロールに存在する必要がありました。チェックアウトコントローラーでは、ユーザーはログインする必要がありますが、管理者である必要はありません。*</span><span class="sxs-lookup"><span data-stu-id="cb017-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="cb017-131">わかりやすくするために、このチュートリアルでは支払い情報については扱いません。</span><span class="sxs-lookup"><span data-stu-id="cb017-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="cb017-132">代わりに、ユーザーがプロモーションコードを使用してチェックアウトできるようにしています。</span><span class="sxs-lookup"><span data-stu-id="cb017-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="cb017-133">このキャンペーンコードは、プロモーションコードという名前の定数を使用して保存されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="cb017-134">StoreController のように、storeDB という名前の MusicStoreEntities クラスのインスタンスを保持するフィールドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="cb017-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="cb017-135">MusicStoreEntities クラスを使用するには、MvcMusicStore 名前空間の using ステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb017-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="cb017-136">Checkout コントローラーの上部が下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="cb017-137">CheckoutController には、次のコントローラーアクションがあります。</span><span class="sxs-lookup"><span data-stu-id="cb017-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="cb017-138">**AddressAndPayment (GET メソッド)** は、ユーザーが情報を入力するためのフォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="cb017-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="cb017-139">**AddressAndPayment (POST メソッド)** は入力を検証し、注文を処理します。</span><span class="sxs-lookup"><span data-stu-id="cb017-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="cb017-140">ユーザーがチェックアウトプロセスを正常に完了すると、**完了**したことが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cb017-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="cb017-141">このビューには、確認としてユーザーの注文番号が含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb017-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="cb017-142">まず、(コントローラーを作成したときに生成された) インデックスコントローラーアクションの名前を AddressAndPayment に変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="cb017-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="cb017-143">このコントローラーアクションでは、チェックアウトフォームのみが表示されるため、モデル情報は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="cb017-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="cb017-144">AddressAndPayment POST メソッドは、StoreManagerController で使用したのと同じパターンに従います。フォームの送信を受け入れて注文を完了しようとし、失敗した場合はフォームを再表示します。</span><span class="sxs-lookup"><span data-stu-id="cb017-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="cb017-145">フォーム入力が注文の検証要件を満たしていることを検証した後、プロモーションコード form 値を直接確認します。</span><span class="sxs-lookup"><span data-stu-id="cb017-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="cb017-146">すべてが正しいことを前提として、更新された情報を注文と共に保存し、注文プロセスを完了するように ShoppingCart オブジェクトに指示して、完全なアクションにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="cb017-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="cb017-147">チェックアウトプロセスが正常に完了すると、ユーザーはコントローラーの完了アクションにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="cb017-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="cb017-148">このアクションでは、注文番号を確認のために表示する前に、その注文が実際にログインしているユーザーに属していることを検証するための簡単なチェックを実行します。</span><span class="sxs-lookup"><span data-stu-id="cb017-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="cb017-149">*注: プロジェクトを開始したときに、エラービューが/ビュー/共有フォルダーに自動的に作成されました。*</span><span class="sxs-lookup"><span data-stu-id="cb017-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="cb017-150">完全な CheckoutController コードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cb017-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="cb017-151">AddressAndPayment ビューの追加</span><span class="sxs-lookup"><span data-stu-id="cb017-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="cb017-152">ここで、AddressAndPayment ビューを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="cb017-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="cb017-153">AddressAndPayment controller アクションの1つを右クリックし、次に示すように、注文として厳密に型指定された AddressAndPayment という名前のビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="cb017-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="cb017-154">このビューでは、StoreManagerEdit ビューの構築時に見た2つの手法を使用します。</span><span class="sxs-lookup"><span data-stu-id="cb017-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="cb017-155">Html EditorForModel () を使用して、注文モデルのフォームフィールドを表示します。</span><span class="sxs-lookup"><span data-stu-id="cb017-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="cb017-156">検証属性を持つ Order クラスを使用して検証規則を活用します。</span><span class="sxs-lookup"><span data-stu-id="cb017-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="cb017-157">まず、Html EditorForModel () を使用するようにフォームコードを更新し、次にプロモーションコード用に追加のテキストボックスを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb017-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="cb017-158">AddressAndPayment ビューの完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="cb017-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="cb017-159">注文の検証規則の定義</span><span class="sxs-lookup"><span data-stu-id="cb017-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="cb017-160">ビューが設定されたので、前にアルバムモデルに対して行ったように、注文モデルの検証規則を設定します。</span><span class="sxs-lookup"><span data-stu-id="cb017-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="cb017-161">[モデル] フォルダーを右クリックし、Order という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="cb017-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="cb017-162">以前にアルバムで使用していた検証属性に加えて、正規表現を使用してユーザーの電子メールアドレスを検証します。</span><span class="sxs-lookup"><span data-stu-id="cb017-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="cb017-163">不明または無効な情報が含まれているフォームを送信しようとすると、クライアント側の検証を使用したエラーメッセージが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cb017-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="cb017-164">それでは、チェックアウトプロセスでは、ほとんどの作業が完了しました。いくつかのことが終わり、終了します。</span><span class="sxs-lookup"><span data-stu-id="cb017-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="cb017-165">2つの単純なビューを追加する必要があり、ログインプロセス中にカート情報のハンドオフを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb017-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="cb017-166">チェックアウトの完了ビューの追加</span><span class="sxs-lookup"><span data-stu-id="cb017-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="cb017-167">[チェックアウトの完了] ビューは、注文 ID を表示するだけで済むため、非常に単純です。</span><span class="sxs-lookup"><span data-stu-id="cb017-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="cb017-168">Complete controller アクションを右クリックし、「Complete」という名前のビューを追加します。これは int として厳密に型指定されています。</span><span class="sxs-lookup"><span data-stu-id="cb017-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="cb017-169">次に示すように、ビューコードを更新して注文 ID を表示します。</span><span class="sxs-lookup"><span data-stu-id="cb017-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="cb017-170">エラービューの更新</span><span class="sxs-lookup"><span data-stu-id="cb017-170">Updating The Error view</span></span>

<span data-ttu-id="cb017-171">既定のテンプレートには、サイト内の他の場所で再利用できるように、[共有ビュー] フォルダーに [エラー] ビューが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cb017-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="cb017-172">このエラー表示には非常に単純なエラーが含まれており、サイトレイアウトは使用しないため、更新します。</span><span class="sxs-lookup"><span data-stu-id="cb017-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="cb017-173">これは一般的なエラーページであるため、コンテンツは非常に単純です。</span><span class="sxs-lookup"><span data-stu-id="cb017-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="cb017-174">ユーザーが操作をやり直す必要がある場合は、履歴内の前のページに移動するためのメッセージとリンクを含めます。</span><span class="sxs-lookup"><span data-stu-id="cb017-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="cb017-175">[前へ](mvc-music-store-part-8.md)
> [次へ](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="cb017-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
