---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: PayPal を使用したチェックアウトと支払い |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615148"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="026fb-103">精算と PayPal による支払い</span><span class="sxs-lookup"><span data-stu-id="026fb-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="026fb-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="026fb-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="026fb-105">[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。</span><span class="sxs-lookup"><span data-stu-id="026fb-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="026fb-106">このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。</span><span class="sxs-lookup"><span data-stu-id="026fb-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="026fb-107">このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="026fb-108">このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、PayPal を使用したユーザーの承認、登録、支払いを含むようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="026fb-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="026fb-109">ログインしているユーザーのみが製品の購入を許可されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="026fb-110">ASP.NET 4.5 Web フォームプロジェクトテンプレートには、必要なものの多くが既に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="026fb-111">PayPal Express のチェックアウト機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="026fb-112">このチュートリアルでは、PayPal 開発者テスト環境を使用しているため、実際の資金は譲渡されません。</span><span class="sxs-lookup"><span data-stu-id="026fb-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="026fb-113">このチュートリアルの最後では、ショッピングカートに追加する製品を選択し、[チェックアウト] ボタンをクリックして、PayPal テスト web サイトにデータを転送することで、アプリケーションをテストします。</span><span class="sxs-lookup"><span data-stu-id="026fb-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="026fb-114">PayPal テスト web サイトでは、出荷と支払いに関する情報を確認し、ローカル Wingtip Toys サンプルアプリケーションに戻って、購入を確認して完了します。</span><span class="sxs-lookup"><span data-stu-id="026fb-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="026fb-115">拡張性とセキュリティに対処するオンラインショッピングに特化した、経験豊富なサードパーティの支払いプロセッサがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="026fb-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="026fb-116">ASP.NET 開発者は、ショッピングおよび購入ソリューションを実装する前に、サードパーティの支払いソリューションを利用する利点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="026fb-117">Wingtip Toys サンプルアプリケーションは、ASP.NET web 開発者が使用できる特定の ASP.NET の概念と機能を示すように設計されています。</span><span class="sxs-lookup"><span data-stu-id="026fb-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="026fb-118">このサンプルアプリケーションは、スケーラビリティとセキュリティに関して考えられるすべての状況に合わせて最適化されていませんでした。</span><span class="sxs-lookup"><span data-stu-id="026fb-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="026fb-119">学習内容:</span><span class="sxs-lookup"><span data-stu-id="026fb-119">What you'll learn:</span></span>

- <span data-ttu-id="026fb-120">フォルダー内の特定のページへのアクセスを制限する方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="026fb-121">匿名ショッピングカートから既知のショッピングカートを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="026fb-122">プロジェクトに対して SSL を有効にする方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="026fb-123">OAuth プロバイダーをプロジェクトに追加する方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="026fb-124">Paypal を使用して、PayPal テスト環境を使用して製品を購入する方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="026fb-125">**DetailsView**コントロールで PayPal の詳細を表示する方法。</span><span class="sxs-lookup"><span data-stu-id="026fb-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="026fb-126">Wingtip Toys アプリケーションのデータベースを、PayPal から取得した詳細情報で更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="026fb-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="026fb-127">注文追跡の追加</span><span class="sxs-lookup"><span data-stu-id="026fb-127">Adding Order Tracking</span></span>

<span data-ttu-id="026fb-128">このチュートリアルでは、ユーザーが作成した注文からデータを追跡する2つの新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="026fb-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="026fb-129">これらのクラスは、出荷情報、購入合計、および支払いの確認に関するデータを追跡します。</span><span class="sxs-lookup"><span data-stu-id="026fb-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="026fb-130">Order および OrderDetail モデルクラスを追加する</span><span class="sxs-lookup"><span data-stu-id="026fb-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="026fb-131">このチュートリアルシリーズの前半では、[*モデル*] フォルダーに `Category`、`Product`、および `CartItem` クラスを作成することによって、カテゴリ、製品、およびショッピングカート項目のスキーマを定義しています。</span><span class="sxs-lookup"><span data-stu-id="026fb-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="026fb-132">ここでは、2つの新しいクラスを追加して、製品の注文のスキーマと注文の詳細を定義します。</span><span class="sxs-lookup"><span data-stu-id="026fb-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="026fb-133">**[モデル]** フォルダーに、 *Order.cs*という名前の新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="026fb-134">新しいクラスファイルがエディターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="026fb-135">既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="026fb-136">*OrderDetail.cs*クラスを [*モデル*] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="026fb-137">既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="026fb-138">`Order` クラスと `OrderDetail` クラスには、購入および発送に使用する注文情報を定義するためのスキーマが含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="026fb-139">さらに、エンティティクラスを管理し、データベースへのデータアクセスを提供するデータベースコンテキストクラスを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="026fb-140">これを行うには、新しく作成された Order クラスと `OrderDetail` モデルクラスを `ProductContext` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="026fb-141">**ソリューションエクスプローラー**で、 *ProductContext.cs*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="026fb-142">次に示すように、強調表示されているコードを*ProductContext.cs*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="026fb-143">このチュートリアルシリーズで前述したように、 *ProductContext.cs*ファイルのコードは、Entity Framework のすべてのコア機能にアクセスできるように、`System.Data.Entity` 名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="026fb-144">この機能には、厳密に型指定されたオブジェクトを操作することによって、データのクエリ、挿入、更新、および削除を行う機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="026fb-145">`ProductContext` クラスの上記のコードは、新しく追加された `Order` および `OrderDetail` クラスへの Entity Framework アクセスを追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="026fb-146">チェックアウトアクセスの追加</span><span class="sxs-lookup"><span data-stu-id="026fb-146">Adding Checkout Access</span></span>

<span data-ttu-id="026fb-147">Wingtip Toys サンプルアプリケーションを使用すると、匿名ユーザーは、ショッピングカートに製品を確認して追加することができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="026fb-148">ただし、匿名ユーザーがショッピングカートに追加した製品を購入する場合は、サイトにログオンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="026fb-149">ログオンすると、チェックアウトおよび購入プロセスを処理する Web アプリケーションの制限付きページにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="026fb-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="026fb-150">これらの制限付きページは、アプリケーションの*Checkout*フォルダーに含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="026fb-151">チェックアウトフォルダーとページを追加する</span><span class="sxs-lookup"><span data-stu-id="026fb-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="026fb-152">ここ*で、チェックアウトフォルダーと*、チェックアウトプロセス中に顧客に表示されるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="026fb-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="026fb-153">これらのページは、このチュートリアルの後半で更新します。</span><span class="sxs-lookup"><span data-stu-id="026fb-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="026fb-154">**ソリューションエクスプローラー**でプロジェクト名 (**Wingtip Toys**) を右クリックし、 **[新しいフォルダーの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-新しいフォルダー](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="026fb-156">新しいフォルダーに「*チェックアウト*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="026fb-157">[*チェックアウト*] フォルダーを右クリックし、[**新しい項目**の-&gt;**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-新しい項目](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="026fb-159">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="026fb-160">左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="026fb-161">次に、中央のウィンドウで、 **[マスターページを含む Web フォーム]** を選択し、 *CheckoutStart*という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="026fb-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![[新しい項目の追加] ダイアログボックスでの [チェックと支払い]](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="026fb-163">前と同様に、マスターページとして [] を選択し*ます。*</span><span class="sxs-lookup"><span data-stu-id="026fb-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="026fb-164">上記と同じ手順を使用して、次の追加ページを*Checkout*フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="026fb-165">CheckoutReview</span><span class="sxs-lookup"><span data-stu-id="026fb-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="026fb-166">CheckoutComplete</span><span class="sxs-lookup"><span data-stu-id="026fb-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="026fb-167">CheckoutCancel</span><span class="sxs-lookup"><span data-stu-id="026fb-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="026fb-168">CheckoutError</span><span class="sxs-lookup"><span data-stu-id="026fb-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="026fb-169">Web.config ファイルを追加する</span><span class="sxs-lookup"><span data-stu-id="026fb-169">Add a Web.config File</span></span>

<span data-ttu-id="026fb-170">新しい web.config ファイルを*Checkout*フォルダーに追加することで、フォルダーに含まれるすべてのページへのアクセスを制限できるように*なります。*</span><span class="sxs-lookup"><span data-stu-id="026fb-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="026fb-171">[*チェックアウト*] フォルダーを右クリックし、[**新しい項目**の**追加** -&gt;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="026fb-172">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="026fb-173">左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="026fb-174">次に、中央のペインで **[Web 構成ファイル]** を選択し、web.config*の既定*の名前をそのまま使用して、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="026fb-175">*Web.config ファイル内*の既存の XML コンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="026fb-176">*Web.config ファイルを*保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="026fb-177">Web.config*ファイルは*、web アプリケーションのすべての不明なユーザーが、 *Checkout*フォルダーに格納されているページへのアクセスを拒否する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="026fb-178">ただし、ユーザーがアカウントを登録し、ログオンしている場合は、既知のユーザーになり、 *Checkout*フォルダー内のページにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="026fb-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="026fb-179">ASP.NET の構成は階層に従っていることに注意してください。各 web.config ファイルでは、構成設定が含まれているフォルダーとその下のすべての子ディレクトリに適用さ*れます。*</span><span class="sxs-lookup"><span data-stu-id="026fb-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="026fb-180">プロジェクトの SSL を有効にする</span><span class="sxs-lookup"><span data-stu-id="026fb-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="026fb-181">Secure Sockets Layer (SSL) は、Web サーバーと Web クライアントが暗号化を使用してより安全に通信できるように定義されたプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="026fb-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="026fb-182">SSL が使用されていない場合、クライアントとサーバーの間で送信されるデータは、ネットワークへの物理的なアクセスを持つすべてのユーザーによってパケットスニッフィングで開かれます。</span><span class="sxs-lookup"><span data-stu-id="026fb-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="026fb-183">また、いくつかの一般的な認証方式は、プレーンな HTTP を介してセキュリティで保護されていません。</span><span class="sxs-lookup"><span data-stu-id="026fb-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="026fb-184">特に、基本認証とフォーム認証では、暗号化されていない資格情報が送信されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="026fb-185">セキュリティを確保するために、これらの認証方式では SSL を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="026fb-186">**ソリューションエクスプローラー**で、**ウィングヒントの toys**プロジェクトをクリックし、 **F4**キーを押して **[プロパティ]** ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="026fb-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="026fb-187">**SSL Enabled**を `true`に変更します。</span><span class="sxs-lookup"><span data-stu-id="026fb-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="026fb-188">**SSL URL**をコピーして、後で使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="026fb-189">Ssl Web サイトを以前に作成した場合を除き、SSL URL は `https://localhost:44300/` になります (以下の図を参照)。</span><span class="sxs-lookup"><span data-stu-id="026fb-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="026fb-190">![プロジェクト プロパティ](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="026fb-191">**ソリューションエクスプローラー**で、**ウィングヒントの toys**プロジェクトを右クリックし、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="026fb-192">左側のタブで、 **[Web]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="026fb-193">以前に保存した**SSL url**を使用するように**プロジェクト url**を変更します。</span><span class="sxs-lookup"><span data-stu-id="026fb-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="026fb-194">![Project の Web プロパティ](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="026fb-195">**CTRL + S**キーを押して、ページを保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="026fb-196">**Ctrl キーを押しながら F5 キーを押して**アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="026fb-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="026fb-197">Visual Studio には、SSL 警告を回避するためのオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="026fb-198">**[はい]** をクリックして IIS Express SSL 証明書を信頼し、続行します。</span><span class="sxs-lookup"><span data-stu-id="026fb-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="026fb-199">SSL 証明書の詳細を ![IIS Express](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="026fb-200">セキュリティ警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="026fb-201">**[はい]** をクリックして、localhost に証明書をインストールします。</span><span class="sxs-lookup"><span data-stu-id="026fb-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="026fb-202">[セキュリティ警告の ![] ダイアログボックス](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="026fb-203">ブラウザーウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-203">The browser window will be displayed.</span></span>

<span data-ttu-id="026fb-204">SSL を使用して、Web アプリケーションをローカルで簡単にテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="026fb-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="026fb-205">OAuth 2.0 プロバイダーを追加する</span><span class="sxs-lookup"><span data-stu-id="026fb-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="026fb-206">ASP.NET Web フォームは、メンバーシップと認証のための拡張オプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="026fb-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="026fb-207">これらの機能強化には、OAuth が含まれます。</span><span class="sxs-lookup"><span data-stu-id="026fb-207">These enhancements include OAuth.</span></span> <span data-ttu-id="026fb-208">OAuth は、web、モバイル、およびデスクトップのアプリケーションからシンプルで標準的な方法で、セキュリティで保護された承認を可能にするオープンプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="026fb-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="026fb-209">ASP.NET Web フォームテンプレートでは、OAuth を使用して、Facebook、Twitter、Google、Microsoft を認証プロバイダーとして公開しています。</span><span class="sxs-lookup"><span data-stu-id="026fb-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="026fb-210">このチュートリアルでは、認証プロバイダーとして Google のみを使用しますが、任意のプロバイダーを使用するようにコードを簡単に変更できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="026fb-211">他のプロバイダーを実装する手順は、このチュートリアルで説明されている手順とよく似ています。</span><span class="sxs-lookup"><span data-stu-id="026fb-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="026fb-212">このチュートリアルでは、認証に加えて、ロールを使用して承認を実装します。</span><span class="sxs-lookup"><span data-stu-id="026fb-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="026fb-213">`canEdit` のロールに追加したユーザーのみが、データの変更 (連絡先の作成、編集、削除) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="026fb-214">Windows Live アプリケーションは、実用的な web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル web サイトの URL を使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="026fb-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="026fb-215">次の手順では、Google authentication プロバイダーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="026fb-216">*アプリ\_Start\Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="026fb-217">メソッドが次のように表示されるように、`app.UseGoogleAuthentication()` メソッドからコメント文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="026fb-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="026fb-218">[Google 開発者コンソール](https://console.developers.google.com/)に移動します。</span><span class="sxs-lookup"><span data-stu-id="026fb-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="026fb-219">また、Google 開発者の電子メールアカウント (gmail.com) を使用してサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="026fb-220">Google アカウントを持っていない場合は、 **[アカウントの作成]** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="026fb-221">次に、 **Google 開発者コンソール**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="026fb-222">![Google 開発者コンソール](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="026fb-223">**[プロジェクトの作成]** ボタンをクリックし、プロジェクトの名前と ID を入力します (既定値を使用できます)。</span><span class="sxs-lookup"><span data-stu-id="026fb-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="026fb-224">次に、[**アグリーメント] チェックボックス**と **[作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![Google-新しいプロジェクト](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="026fb-226">数秒すると、新しいプロジェクトが作成され、ブラウザーに [新しいプロジェクト] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="026fb-227">左側のタブで、[ **api &amp; auth**] をクリックし、 **[資格情報]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="026fb-228">**[OAuth]** の **[新しいクライアント ID の作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="026fb-229">**[クライアント ID の作成]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="026fb-230">![Google-クライアント ID の作成](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="026fb-231">**[クライアント ID の作成]** ダイアログボックスで、アプリケーションの種類の既定の**Web アプリケーション**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="026fb-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="026fb-232">承認された**JavaScript オリジン**を、このチュートリアルの前半で使用した ssl URL (他の ssl プロジェクトを作成していない場合は`https://localhost:44300/`) に設定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="026fb-233">この URL は、アプリケーションのオリジンです。</span><span class="sxs-lookup"><span data-stu-id="026fb-233">This URL is the origin for your application.</span></span> <span data-ttu-id="026fb-234">このサンプルでは、localhost テスト URL だけを入力します。</span><span class="sxs-lookup"><span data-stu-id="026fb-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="026fb-235">ただし、複数の Url を入力して、localhost と運用環境を考慮することができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="026fb-236">承認された**リダイレクト URI**を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="026fb-237">この値は、ASP.NET OAuth ユーザーが google OAuth サーバーと通信するために使用する URI です。</span><span class="sxs-lookup"><span data-stu-id="026fb-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="026fb-238">上記で使用した SSL URL を記憶します (他の SSL プロジェクトを作成していない場合は `https://localhost:44300/`)。</span><span class="sxs-lookup"><span data-stu-id="026fb-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="026fb-239">**[クライアント ID の作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="026fb-240">Google 開発者コンソールの左側のメニューで、 **[同意画面]** メニュー項目をクリックし、電子メールアドレスと製品名を設定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="026fb-241">フォームが完了したら、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="026fb-242">**[Api]** メニュー項目をクリックして下にスクロールし、 **[Google + API]** の横にある **[オフ]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="026fb-243">このオプションを受け入れると、Google + API が有効になります。</span><span class="sxs-lookup"><span data-stu-id="026fb-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="026fb-244">また、 **Owin** NuGet パッケージをバージョン3.0.0 に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="026fb-245">**[ツール]** メニューの **[nuget パッケージマネージャー]** を選択し、 **[ソリューションの nuget パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="026fb-246">**[NuGet パッケージの管理]** ウィンドウで、 **Owin**パッケージを検索し、バージョン3.0.0 に更新します。</span><span class="sxs-lookup"><span data-stu-id="026fb-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="026fb-247">Visual Studio で、**クライアント ID**と**クライアントシークレット**をコピーしてメソッドに貼り付けることにより、 *Startup.Auth.cs*ページの `UseGoogleAuthentication` メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="026fb-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="026fb-248">次に示す**クライアント ID**と**クライアントシークレット**の値はサンプルであり、機能しません。</span><span class="sxs-lookup"><span data-stu-id="026fb-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="026fb-249">CTRL キーを押し**ながら F5**キーを押して、アプリケーションをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="026fb-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="026fb-250">**[ログイン]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="026fb-251">**[別のサービスを使用してログインする]** で、 **[Google]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="026fb-252">![のログイン](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="026fb-253">資格情報を入力する必要がある場合は、資格情報を入力する google サイトにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google-サインイン](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="026fb-255">資格情報を入力すると、作成した web アプリケーションにアクセス許可を付与するように求められます。</span><span class="sxs-lookup"><span data-stu-id="026fb-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![プロジェクトの既定のサービスアカウント](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="026fb-257">[**同意**する] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-257">Click **Accept**.</span></span> <span data-ttu-id="026fb-258">これで、**ウィングヒント toys**アプリケーションの**登録**ページにリダイレクトされ、Google アカウントを登録できるようになります。</span><span class="sxs-lookup"><span data-stu-id="026fb-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="026fb-259">Google アカウントに登録 ![](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="026fb-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="026fb-260">Gmail アカウントに使用するローカルの電子メール登録名を変更することもできますが、通常は既定の電子メールエイリアス (認証に使用したもの) をそのままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="026fb-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="026fb-261">上に示すよう**に、[ログイン**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="026fb-262">ログイン機能の変更</span><span class="sxs-lookup"><span data-stu-id="026fb-262">Modifying Login Functionality</span></span>

<span data-ttu-id="026fb-263">このチュートリアルシリーズで既に説明したように、既定では、ユーザー登録機能の多くが ASP.NET Web Forms テンプレートに含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="026fb-264">次に、既定の*login.aspx*ページを変更し、`MigrateCart` メソッドを呼び出すように .aspx ページを*登録*します。</span><span class="sxs-lookup"><span data-stu-id="026fb-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="026fb-265">`MigrateCart` メソッドを使用すると、新しくログインしたユーザーを匿名のショッピングカートに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="026fb-266">ユーザーとショッピングカートを関連付けることにより、Wingtip Toys サンプルアプリケーションは、ユーザーのショッピングカートを訪問後に管理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="026fb-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="026fb-267">**ソリューションエクスプローラー**で、*アカウント*フォルダーを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="026fb-268">次のように表示されるように、 *Login.aspx.cs*という名前の分離コードページを変更して、黄色で強調表示されているコードを含めます。</span><span class="sxs-lookup"><span data-stu-id="026fb-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="026fb-269">*Login.aspx.cs*ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="026fb-270">ここでは、`MigrateCart` メソッドの定義がないという警告は無視してかまいません。</span><span class="sxs-lookup"><span data-stu-id="026fb-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="026fb-271">このチュートリアルでは、少し後で追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="026fb-272">*Login.aspx.cs*分離コードファイルは、ログインメソッドをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="026fb-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="026fb-273">Login.aspx ページを調べると、このページに [ログイン] ボタンが含まれていることがわかります。このボタンをクリックすると、コードビハインドで `LogIn` ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="026fb-274">*Login.aspx.cs*の `Login` メソッドが呼び出されると、`usersShoppingCart` という名前のショッピングカートの新しいインスタンスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="026fb-275">ショッピングカートの ID (GUID) が取得され、`cartId` 変数に設定されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="026fb-276">次に、`MigrateCart` メソッドが呼び出され、ログインユーザーの `cartId` と名前の両方がこのメソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="026fb-277">ショッピングカートを移行すると、匿名ショッピングカートの識別に使用される GUID がユーザー名に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="026fb-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="026fb-278">ユーザーがログインするときにショッピングカートを移行するために*Login.aspx.cs*分離コードファイルを変更するだけでなく、ユーザーが新しいアカウントを作成してログインするときに、ショッピングカートを移行するように*Register.aspx.cs 分離コードファイル*を変更する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="026fb-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="026fb-279">*Account*フォルダーで、 *Register.aspx.cs*という名前の分離コードファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="026fb-280">次のように、コードを黄色で含めてコードビハインドファイルを変更します。</span><span class="sxs-lookup"><span data-stu-id="026fb-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="026fb-281">*Register.aspx.cs*ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="026fb-282">ここでも、`MigrateCart` メソッドに関する警告は無視してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="026fb-283">`CreateUser_Click` イベントハンドラーで使用したコードは、`LogIn` メソッドで使用したコードと非常によく似ていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="026fb-284">ユーザーがサイトに登録またはログインすると、`MigrateCart` メソッドの呼び出しが行われます。</span><span class="sxs-lookup"><span data-stu-id="026fb-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="026fb-285">ショッピングカートの移行</span><span class="sxs-lookup"><span data-stu-id="026fb-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="026fb-286">これで、ログインと登録のプロセスが更新されたので、`MigrateCart` 方法を使用して、ショッピングカートを移行するコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="026fb-287">**ソリューションエクスプローラー**で、 *Logic*フォルダーを見つけて、 *ShoppingCartActions.cs*クラスファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="026fb-288">次のように、 *ShoppingCartActions.cs*ファイルのコードが次のように表示されるように、黄色で強調表示されているコードを*ShoppingCartActions.cs*ファイルの既存のコードに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="026fb-289">`MigrateCart` メソッドは、既存の cartId を使用して、ユーザーのショッピングカートを検索します。</span><span class="sxs-lookup"><span data-stu-id="026fb-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="026fb-290">次に、すべてのショッピングカート項目をループし、`CartItem` スキーマによって指定された `CartId` プロパティをログインユーザー名に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="026fb-291">データベース接続を更新しています</span><span class="sxs-lookup"><span data-stu-id="026fb-291">Updating the Database Connection</span></span>

<span data-ttu-id="026fb-292">構築済みの Wingtip Toys サンプルアプリケーションを使用してこの**チュートリアルに従う**場合は、既定のメンバーシップデータベースを再作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="026fb-293">既定の接続文字列を変更することで、次回アプリケーションを実行したときにメンバーシップデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="026fb-294">プロジェクトのルートにある*web.config ファイルを開きます。*</span><span class="sxs-lookup"><span data-stu-id="026fb-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="026fb-295">既定の接続文字列を更新して、次のように表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="026fb-296">PayPal の統合</span><span class="sxs-lookup"><span data-stu-id="026fb-296">Integrating PayPal</span></span>

<span data-ttu-id="026fb-297">PayPal は、オンラインの商人による支払いを受け入れる web ベースの課金プラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="026fb-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="026fb-298">このチュートリアルでは、PayPal の高速チェックアウト機能をアプリケーションに統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="026fb-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="026fb-299">Express Checkout では、顧客が PayPal を使用して、ショッピングカートに追加した商品の支払いを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="026fb-300">PayPal テストアカウントの作成</span><span class="sxs-lookup"><span data-stu-id="026fb-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="026fb-301">PayPal テスト環境を使用するには、開発者テストアカウントを作成して確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="026fb-302">開発者テストアカウントを使用して、購入者テストアカウントと販売者テストアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="026fb-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="026fb-303">開発者テストアカウントの資格情報では、Wingtip Toys サンプルアプリケーションが PayPal テスト環境にアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="026fb-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="026fb-304">ブラウザーで、PayPal 開発者テストサイトに移動します。</span><span class="sxs-lookup"><span data-stu-id="026fb-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="026fb-305">PayPal 開発者アカウントを持っていない場合は、 **[サインアップ]** をクリックし、サインアップ手順に従って新しいアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="026fb-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="026fb-306">既存の PayPal 開発者アカウントを持っている場合は、 **[ログイン]** をクリックしてサインインします。</span><span class="sxs-lookup"><span data-stu-id="026fb-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="026fb-307">Wingtip Toys サンプルアプリケーションをテストするには、このチュートリアルの後半で PayPal 開発者アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="026fb-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="026fb-308">PayPal 開発者アカウントにサインアップしたばかりの場合は、paypal で PayPal 開発者アカウントを確認することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="026fb-309">アカウントは、PayPal が電子メールアカウントに送信した手順に従って確認できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="026fb-310">PayPal 開発者アカウントを確認したら、PayPal 開発者テストサイトに戻ります。</span><span class="sxs-lookup"><span data-stu-id="026fb-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="026fb-311">Paypal 開発者アカウントを使用して PayPal developer サイトにログインした後は、PayPal 購入者テストアカウントを作成する必要があります (まだお持ちでない場合)。</span><span class="sxs-lookup"><span data-stu-id="026fb-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="026fb-312">購入者テストアカウントを作成するには、PayPal サイトで **[アプリケーション]** タブをクリックし、 **[サンドボックスアカウント]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="026fb-313">**[サンドボックステストアカウント]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="026fb-314">PayPal 開発者サイトには、既にマーチャントテストアカウントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="026fb-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![PayPal を使用したチェックアウトと支払い-サンドボックステストアカウント](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="026fb-316">サンドボックステストアカウント ページで、**アカウントの作成** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="026fb-317">**[テストアカウントの作成]** ページで、購入者テストアカウントの電子メールとパスワードを選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="026fb-318">このチュートリアルの最後に Wingtip Toys サンプルアプリケーションをテストするには、購入者の電子メールアドレスとパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="026fb-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![PayPal を使用したチェックアウトと支払い-サンドボックステストアカウント](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="026fb-320">**[アカウントの作成]** ボタンをクリックして購入者テストアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="026fb-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="026fb-321">**[サンドボックステストアカウント]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![PayPal-PayPal アカウントを使用したチェックアウトと支払い](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="026fb-323">**[サンドボックステストアカウント]** ページで、**進行**中の電子メールアカウントをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="026fb-324">**プロファイル**と**通知**のオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="026fb-325">**[プロファイル]** オプションを選択し、 **[api 資格情報]** をクリックして、マーチャントテストアカウントの api 資格情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="026fb-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="026fb-326">テスト API 資格情報をメモ帳にコピーします。</span><span class="sxs-lookup"><span data-stu-id="026fb-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="026fb-327">Wingtip Toys サンプルアプリケーションから PayPal テスト環境への API 呼び出しを行うには、表示されているクラシックテスト API 資格情報 (ユーザー名、パスワード、署名) が必要です。</span><span class="sxs-lookup"><span data-stu-id="026fb-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="026fb-328">次の手順で資格情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="026fb-329">PayPal クラスと API 資格情報の追加</span><span class="sxs-lookup"><span data-stu-id="026fb-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="026fb-330">ほとんどの PayPal コードを1つのクラスに配置します。</span><span class="sxs-lookup"><span data-stu-id="026fb-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="026fb-331">このクラスには、PayPal との通信に使用されるメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="026fb-332">また、PayPal の資格情報をこのクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="026fb-333">Visual Studio 内の Wingtip Toys サンプルアプリケーションで、 **Logic**フォルダーを右クリックし、[ **Add** -&gt;**新しい項目**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="026fb-334">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="026fb-335">左側の **[インストール済み]** ウィンドウの **[ビジュアルC# ]** で、 **[コード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="026fb-336">中央のウィンドウで、 **[クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="026fb-337">この新しいクラスに**PayPalFunctions.cs**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="026fb-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="026fb-338">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-338">Click **Add**.</span></span>  
   <span data-ttu-id="026fb-339">新しいクラスファイルがエディターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="026fb-340">既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="026fb-341">このチュートリアルで前に表示したマーチャント API 資格情報 (ユーザー名、パスワード、署名) を追加して、PayPal テスト環境への関数呼び出しを行うことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="026fb-342">このサンプルアプリケーションでは、単に資格情報をC#ファイル (.cs) に追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="026fb-343">ただし、実装されたソリューションでは、構成ファイルで資格情報を暗号化することを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="026fb-344">NVPAPICaller クラスには、PayPal 機能の大部分が含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="026fb-345">クラスのコードは、PayPal テスト環境からのテスト購入を行うために必要なメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="026fb-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="026fb-346">購入するには、次の3つの PayPal 関数を使用します。</span><span class="sxs-lookup"><span data-stu-id="026fb-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="026fb-347">`SetExpressCheckout` 関数</span><span class="sxs-lookup"><span data-stu-id="026fb-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="026fb-348">`GetExpressCheckoutDetails` 関数</span><span class="sxs-lookup"><span data-stu-id="026fb-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="026fb-349">`DoExpressCheckoutPayment` 関数</span><span class="sxs-lookup"><span data-stu-id="026fb-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="026fb-350">`ShortcutExpressCheckout` メソッドは、ショッピングカートからテスト購入情報と製品の詳細を収集し、`SetExpressCheckout` PayPal 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="026fb-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="026fb-351">`GetCheckoutDetails` メソッドは、購入の詳細を確認し、テストを購入する前に `GetExpressCheckoutDetails` PayPal 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="026fb-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="026fb-352">`DoCheckoutPayment` メソッドは、`DoExpressCheckoutPayment` PayPal 関数を呼び出して、テスト環境からのテストの購入を完了します。</span><span class="sxs-lookup"><span data-stu-id="026fb-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="026fb-353">残りのコードでは、文字列のエンコード、文字列のデコード、配列の処理、資格情報の確認など、PayPal のメソッドとプロセスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="026fb-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="026fb-354">PayPal では、 [paypal の API 仕様](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)に基づいて、オプションの購入の詳細を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="026fb-355">Wingtip Toys サンプルアプリケーションのコードを拡張することで、ローカライズの詳細、製品の説明、税金、顧客のサービス番号、およびその他のオプションのフィールドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="026fb-356">**ShortcutExpressCheckout**メソッドに指定されている return および Cancel の url では、ポート番号が使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="026fb-357">Visual Web Developer で SSL を使用して web プロジェクトを実行する場合は、通常、web サーバーに対してポート44300が使用されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="026fb-358">上記のように、ポート番号は44300です。</span><span class="sxs-lookup"><span data-stu-id="026fb-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="026fb-359">アプリケーションを実行すると、別のポート番号が表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="026fb-360">このチュートリアルの最後に Wingtip Toys サンプルアプリケーションを正常に実行できるように、コードでポート番号を正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="026fb-361">このチュートリアルの次のセクションでは、ローカルホストのポート番号を取得し、PayPal クラスを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="026fb-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="026fb-362">PayPal クラスの LocalHost ポート番号を更新する</span><span class="sxs-lookup"><span data-stu-id="026fb-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="026fb-363">Wingtip Toys サンプルアプリケーションは、PayPal テストサイトに移動し、Wingtip Toys サンプルアプリケーションのローカルインスタンスに戻ることによって、製品を購入します。</span><span class="sxs-lookup"><span data-stu-id="026fb-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="026fb-364">PayPal が正しい URL に戻るようにするには、上で説明した PayPal コードでローカルに実行されるサンプルアプリケーションのポート番号を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="026fb-365">**ソリューションエクスプローラー**でプロジェクト名 (ウィングの**おもちゃ**) を右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="026fb-366">左側の列で、 **[Web]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="026fb-367">**[プロジェクト Url]** ボックスからポート番号を取得します。</span><span class="sxs-lookup"><span data-stu-id="026fb-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="026fb-368">必要に応じて、 *PayPalFunctions.cs*ファイルの PayPal クラス (`NVPAPICaller`) の `returnURL` と `cancelURL` を更新して、web アプリケーションのポート番号を使用します。</span><span class="sxs-lookup"><span data-stu-id="026fb-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="026fb-369">これで、追加したコードが、ローカル Web アプリケーションで想定されているポートと一致するようになります。</span><span class="sxs-lookup"><span data-stu-id="026fb-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="026fb-370">PayPal は、ローカルコンピューターの正しい URL に戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="026fb-371">PayPal の [チェックアウト] ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="026fb-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="026fb-372">これで、主な PayPal 関数がサンプルアプリケーションに追加されたので、これらの関数を呼び出すために必要なマークアップとコードの追加を開始できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="026fb-373">最初に、ユーザーに表示される [チェックアウト] ボタンを [ショッピングカート] ページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="026fb-374">*ShoppingCart*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="026fb-375">ファイルの一番下までスクロールし、`<!--Checkout Placeholder -->` のコメントを見つけます。</span><span class="sxs-lookup"><span data-stu-id="026fb-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="026fb-376">コメントを `ImageButton` コントロールに置き換えて、マークアップが次のように置き換えられるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="026fb-377">*ShoppingCart.aspx.cs*ファイルで、ファイルの末尾付近にある `UpdateBtn_Click` イベントハンドラーの後に、`CheckOutBtn_Click` イベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="026fb-378">また、 *ShoppingCart.aspx.cs*ファイルで `CheckoutBtn`への参照を追加して、[新しいイメージ] ボタンが次のように参照されるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="026fb-379">変更内容を*ShoppingCart*ファイルと*ShoppingCart.aspx.cs*ファイルの両方に保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="026fb-380">メニューから、[**デバッグ**-] を選択して、**ウィングヒント toys を構築**&gt;ます。</span><span class="sxs-lookup"><span data-stu-id="026fb-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="026fb-381">プロジェクトは、新しく追加された**ImageButton**コントロールを使用してリビルドされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="026fb-382">購入の詳細を PayPal に送信する</span><span class="sxs-lookup"><span data-stu-id="026fb-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="026fb-383">ユーザーがショッピングカートページ (*ShoppingCart*) の **[チェックアウト]** ボタンをクリックすると、購入プロセスが開始されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="026fb-384">次のコードは、製品を購入するために必要な最初の PayPal 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="026fb-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="026fb-385">*Checkout*フォルダーから、 *CheckoutStart.aspx.cs*という名前の分離コードファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="026fb-386">分離コードファイルを必ず開いてください。</span><span class="sxs-lookup"><span data-stu-id="026fb-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="026fb-387">既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="026fb-388">アプリケーションのユーザーがショッピングカートページの **[チェックアウト]** ボタンをクリックすると、ブラウザーは*CheckoutStart*ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="026fb-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="026fb-389">*CheckoutStart*ページが読み込まれると、`ShortcutExpressCheckout` メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="026fb-390">この時点で、ユーザーは PayPal テスト web サイトに転送されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="026fb-391">PayPal サイトでは、ユーザーが PayPal 資格情報を入力し、購入の詳細を確認し、PayPal アグリーメントを受け入れ、`ShortcutExpressCheckout` メソッドが完了した Wingtip Toys サンプルアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="026fb-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="026fb-392">`ShortcutExpressCheckout` メソッドが完了すると、`ShortcutExpressCheckout` メソッドに指定された*CheckoutReview*ページにユーザーがリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="026fb-393">これにより、ユーザーは Wingtip Toys サンプルアプリケーション内から注文の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="026fb-394">注文の詳細の確認</span><span class="sxs-lookup"><span data-stu-id="026fb-394">Review Order Details</span></span>

<span data-ttu-id="026fb-395">PayPal から戻った後、Wingtip Toys サンプルアプリケーションの*CheckoutReview*ページに注文の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="026fb-396">このページでは、ユーザーは製品を購入する前に注文の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="026fb-397">*CheckoutReview*ページは次のように作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="026fb-398">*Checkout*フォルダーで、 *CheckoutReview*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="026fb-399">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="026fb-400">*CheckoutReview.aspx.cs*という名前の分離コードページを開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="026fb-401">**DetailsView**コントロールは、PayPal から返された注文の詳細を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="026fb-402">また、上記のコードでは、注文の詳細を `OrderDetail` オブジェクトとして Wingtip Toys データベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="026fb-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="026fb-403">ユーザーが **[注文の完了]** ボタンをクリックすると、 *CheckoutComplete*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="026fb-404">**形**</span><span class="sxs-lookup"><span data-stu-id="026fb-404">**Tip**</span></span>
> 
> <span data-ttu-id="026fb-405">*CheckoutReview*ページのマークアップで、ページの下部付近にある**DetailsView**コントロール内の項目のスタイルを変更するために `<ItemStyle>` タグが使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="026fb-406">**デザインビュー**でページを表示するには (Visual Studio の左下隅にある **[デザイン]** を選択)、 **detailsview**コントロールを選択し、**スマートタグ**(コントロールの右上にある矢印アイコン) を選択します。これにより、 **detailsview タスク**を表示できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![PayPal を使用したチェックアウトと支払い-フィールドの編集](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="026fb-408">**[フィールドの編集]** を選択すると、 **[フィールド]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="026fb-409">このダイアログボックスでは、 **DetailsView**コントロールの**itemstyle**などのビジュアルプロパティを簡単に制御できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![[PayPal-フィールド] ダイアログボックスでのチェックアウトと支払い](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="026fb-411">購入を完了する</span><span class="sxs-lookup"><span data-stu-id="026fb-411">Complete Purchase</span></span>

<span data-ttu-id="026fb-412">*CheckoutComplete*ページでは、PayPal から購入を行います。</span><span class="sxs-lookup"><span data-stu-id="026fb-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="026fb-413">前述のように、ユーザーは、アプリケーションが*CheckoutComplete*ページに移動する前に、 **[Complete Order]** ボタンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="026fb-414">*Checkout*フォルダーで、 *CheckoutComplete*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="026fb-415">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="026fb-416">*CheckoutComplete.aspx.cs*という名前の分離コードページを開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="026fb-417">*CheckoutComplete*ページが読み込まれると、`DoCheckoutPayment` メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="026fb-418">前述のように、`DoCheckoutPayment` 方法では、PayPal テスト環境からの購入を完了します。</span><span class="sxs-lookup"><span data-stu-id="026fb-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="026fb-419">PayPal が注文の購入を完了すると、 *CheckoutComplete*ページに、購入者に `ID` 支払いトランザクションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="026fb-420">購入取り消しの処理</span><span class="sxs-lookup"><span data-stu-id="026fb-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="026fb-421">ユーザーが購入を取り消すことにした場合は、 *CheckoutCancel*ページにリダイレクトされ、注文が取り消されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="026fb-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="026fb-422">*Checkout*フォルダーの*CheckoutCancel*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="026fb-423">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="026fb-424">購入エラーの処理</span><span class="sxs-lookup"><span data-stu-id="026fb-424">Handle Purchase Errors</span></span>

<span data-ttu-id="026fb-425">購入処理中のエラーは、 *CheckoutError*ページによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="026fb-426">*CheckoutStart*ページ、 *CheckoutReview*ページ、および*CheckoutComplete*ページの分離コードは、エラーが発生した場合に、それぞれが*CheckoutError*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="026fb-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="026fb-427">*Checkout*フォルダーの*CheckoutError*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="026fb-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="026fb-428">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="026fb-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="026fb-429">チェックアウト処理中にエラーが発生すると、 *CheckoutError*ページにエラーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="026fb-430">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="026fb-430">Running the Application</span></span>

<span data-ttu-id="026fb-431">アプリケーションを実行して、製品を購入する方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="026fb-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="026fb-432">PayPal テスト環境で実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="026fb-433">実際の金額は交換されていません。</span><span class="sxs-lookup"><span data-stu-id="026fb-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="026fb-434">すべてのファイルが Visual Studio に保存されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="026fb-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="026fb-435">Web ブラウザーを開き、 [https://developer.paypal.com](https://developer.paypal.com/)に移動します。</span><span class="sxs-lookup"><span data-stu-id="026fb-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="026fb-436">このチュートリアルの前の手順で作成した PayPal 開発者アカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="026fb-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="026fb-437">PayPal の開発者サンドボックスの場合は、 [https://developer.paypal.com](https://developer.paypal.com/)でログインして、高速チェックアウトをテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="026fb-438">これは、paypal のライブ環境ではなく、PayPal のサンドボックステストにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="026fb-439">Visual Studio で、 **F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="026fb-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="026fb-440">データベースを再構築すると、ブラウザーが開き、 *default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="026fb-441">商品カテゴリ ("車" など) を選択し、各製品の横にある **[カートに追加]** をクリックして、3つの異なる製品をショッピングカートに追加します。</span><span class="sxs-lookup"><span data-stu-id="026fb-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="026fb-442">ショッピングカートには、選択した製品が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="026fb-443">**[PayPal]** ボタンをクリックしてチェックアウトします。</span><span class="sxs-lookup"><span data-stu-id="026fb-443">Click the **PayPal** button to checkout.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-カート](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="026fb-445">確認するには、Wingtip Toys サンプルアプリケーションのユーザーアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="026fb-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="026fb-446">ページの右側にある**Google**リンクをクリックして、既存の gmail.com 電子メールアカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="026fb-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="026fb-447">Gmail.com アカウントを持っていない場合は、 [www.gmail.com](https://www.gmail.com/)でテスト目的で作成できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="026fb-448">[登録] をクリックして、標準のローカルアカウントを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="026fb-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![PayPal を使用したチェックアウトと支払い-ログイン](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="026fb-450">Gmail アカウントとパスワードを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="026fb-450">Sign in with your gmail account and password.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-Gmail サインイン](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="026fb-452">**[ログイン]** ボタンをクリックして、gmail アカウントを Wingtip Toys サンプルアプリケーションのユーザー名に登録します。</span><span class="sxs-lookup"><span data-stu-id="026fb-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![PayPal を使用した精算と支払い-アカウントの登録](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="026fb-454">PayPal テストサイトで、このチュートリアルの前の手順で作成した**購入**者の電子メールアドレスとパスワードを追加し、 **[ログイン]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-PayPal サインイン](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="026fb-456">PayPal ポリシーに同意し、 **[同意して続行]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="026fb-457">このページは、この PayPal アカウントを初めて使用するときにのみ表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="026fb-458">ここでも、これはテストアカウントであり、実際の金額は交換されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![PayPal を使用した精算と支払い-PayPal ポリシー](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="026fb-460">PayPal テスト環境の確認 ページで注文情報を確認し、**続行** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![PayPal を使用した精算と支払い-レビュー情報](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="026fb-462">*CheckoutReview*ページで注文金額を確認し、生成された出荷先住所を表示します。</span><span class="sxs-lookup"><span data-stu-id="026fb-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="026fb-463">次に、 **[注文の完了]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-463">Then, click the **Complete Order** button.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-注文レビュー](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="026fb-465">**CheckoutComplete**ページには、支払いトランザクション ID が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![PayPal を使用したチェックアウトと支払い-チェックアウト完了](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="026fb-467">データベースの確認</span><span class="sxs-lookup"><span data-stu-id="026fb-467">Reviewing the Database</span></span>

<span data-ttu-id="026fb-468">アプリケーションの実行後に Wingtip Toys サンプルアプリケーションデータベースの更新されたデータを確認することで、アプリケーションが製品の購入を正常に記録したことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="026fb-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="026fb-469">このチュートリアルシリーズで既に説明したように、 **[データベースエクスプローラー]** ウィンドウ (Visual Studio の**サーバーエクスプローラー**ウィンドウ) を使用して、*ウィングの toys. .mdf*データベースファイルに格納されているデータを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="026fb-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="026fb-470">ブラウザーウィンドウが開いたままの場合は閉じます。</span><span class="sxs-lookup"><span data-stu-id="026fb-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="026fb-471">Visual Studio で、**ソリューションエクスプローラー**の上部にある **[すべてのファイルを表示]** アイコンを選択して、**アプリ\_データ**フォルダーを展開できるようにします。</span><span class="sxs-lookup"><span data-stu-id="026fb-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="026fb-472">[**アプリ\_データ**] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="026fb-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="026fb-473">場合によっては、フォルダーの **[すべてのファイルを表示]** アイコンを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="026fb-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="026fb-474">*ウィングヒントの toys*データベースファイルを右クリックし、 **[開く]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="026fb-475">**サーバーエクスプローラー**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="026fb-476">**[テーブル]** フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="026fb-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="026fb-477">**Orders**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="026fb-478">**Orders**テーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="026fb-479">**PaymentTransactionID**列を確認して、成功したトランザクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="026fb-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![PayPal を使用した精算と支払い-データベースの確認](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="026fb-481">**Orders**テーブルウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="026fb-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="026fb-482">サーバーエクスプローラーで、 **OrderDetails**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="026fb-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="026fb-483">**OrderDetails**テーブルの `OrderId` と `Username` の値を確認します。</span><span class="sxs-lookup"><span data-stu-id="026fb-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="026fb-484">これらの値は、 **Orders**テーブルに含まれる `OrderId` および `Username` の値と一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="026fb-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="026fb-485">**OrderDetails**テーブルウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="026fb-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="026fb-486">Wingtip Toys データベースファイル (*ウィングのおもちゃ*) を右クリックし、[接続を**閉じる**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="026fb-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="026fb-487">**[ソリューションエクスプローラー]** ウィンドウが表示されない場合は、**サーバーエクスプローラー**ウィンドウの下部にある **[ソリューションエクスプローラー]** をクリックして、もう一度**ソリューションエクスプローラー**を表示します。</span><span class="sxs-lookup"><span data-stu-id="026fb-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="026fb-488">要約</span><span class="sxs-lookup"><span data-stu-id="026fb-488">Summary</span></span>

<span data-ttu-id="026fb-489">このチュートリアルでは、注文と注文の詳細スキーマを追加して、製品の購入を追跡しました。</span><span class="sxs-lookup"><span data-stu-id="026fb-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="026fb-490">また、PayPal の機能を Wingtip Toys サンプルアプリケーションに統合しています。</span><span class="sxs-lookup"><span data-stu-id="026fb-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="026fb-491">その他の資料</span><span class="sxs-lookup"><span data-stu-id="026fb-491">Additional Resources</span></span>

<span data-ttu-id="026fb-492">[ASP.NET 構成の概要](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="026fb-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="026fb-493">メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure App Service にデプロイする</span><span class="sxs-lookup"><span data-stu-id="026fb-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="026fb-494">Microsoft Azure-無料試用版</span><span class="sxs-lookup"><span data-stu-id="026fb-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="026fb-495">免責情報</span><span class="sxs-lookup"><span data-stu-id="026fb-495">Disclaimer</span></span>

<span data-ttu-id="026fb-496">このチュートリアルには、サンプルコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="026fb-496">This tutorial contains sample code.</span></span> <span data-ttu-id="026fb-497">このようなサンプルコードは、いかなる種類の保証も伴わず、「現状有姿」で提供されます。</span><span class="sxs-lookup"><span data-stu-id="026fb-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="026fb-498">そのため、Microsoft では、サンプルコードの精度、整合性、品質を保証していません。</span><span class="sxs-lookup"><span data-stu-id="026fb-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="026fb-499">独自のリスクでサンプルコードを使用することに同意します。</span><span class="sxs-lookup"><span data-stu-id="026fb-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="026fb-500">どのような場合でも、どのようなサンプルコードやコンテンツについても、どのような方法でもお客様に対して一切の責任を負いません。ただし、すべてのサンプルコード、コンテンツ、またはサンプルコードを使用した結果として発生するあらゆる種類の損失や損害については一切ありません。</span><span class="sxs-lookup"><span data-stu-id="026fb-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="026fb-501">お客様は、お客様が通知を受け取り、補償に同意することになります。マイクロソフトは、いかなる損失、損失の損害、けが、または損害についても、いかなる場合でも、または投稿したマテリアルによって occasioned されたかどうかにかかわらず、いかなるものでもありません。送信、使用、またはその中に表示されているビューへの制限はありません。</span><span class="sxs-lookup"><span data-stu-id="026fb-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="026fb-502">[前へ](shopping-cart.md)
> [次へ](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="026fb-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
