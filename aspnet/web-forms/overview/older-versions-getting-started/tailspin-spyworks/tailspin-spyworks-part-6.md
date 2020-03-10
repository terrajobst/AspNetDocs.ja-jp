---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 'パート 6: ASP.NET Membership |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート6では、ASP.NET メンバーシップを追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454882"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="c57cd-104">パート 6: ASP.NET メンバーシップ</span><span class="sxs-lookup"><span data-stu-id="c57cd-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="c57cd-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c57cd-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c57cd-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c57cd-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c57cd-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c57cd-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c57cd-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c57cd-109">パート6では、ASP.NET メンバーシップを追加します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="c57cd-110">ASP.NET メンバーシップの使用</span><span class="sxs-lookup"><span data-stu-id="c57cd-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="c57cd-111">[セキュリティ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c57cd-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="c57cd-112">フォーム認証を使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="c57cd-113">[Create User] \ (ユーザーの作成 \) リンクを使用して、いくつかのユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="c57cd-114">完了したら、[ソリューションエクスプローラー] ウィンドウを参照して、ビューを更新します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="c57cd-115">ASPNETDB.MDF であることに注意してください。MDF が正常に作成されました。</span><span class="sxs-lookup"><span data-stu-id="c57cd-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="c57cd-116">このファイルには、メンバーシップのようなコア ASP.NET サービスをサポートするテーブルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c57cd-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="c57cd-117">これで、チェックアウトプロセスの実装を開始できます。</span><span class="sxs-lookup"><span data-stu-id="c57cd-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="c57cd-118">まず、CheckOut ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="c57cd-119">チェックアウトページは、ログインしているユーザーのみが使用できるようにする必要があります。ログインしているユーザーへのアクセスを制限し、ログインページにログインしていないユーザーをリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="c57cd-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="c57cd-120">これを行うには、web.config ファイルの構成セクションに次の内容を追加します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="c57cd-121">ASP.NET Web フォームアプリケーション用のテンプレートによって、認証セクションが web.config ファイルに自動的に追加され、既定のログインページが確立されました。</span><span class="sxs-lookup"><span data-stu-id="c57cd-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="c57cd-122">ユーザーがログインするときに、匿名ショッピングカートを移行するには、login.aspx コードビハインドファイルを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57cd-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="c57cd-123">次のように、ページ\_読み込みイベントを変更します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="c57cd-124">次に、このような "LoggedIn" イベントハンドラーを追加して、新しくログインしたユーザーにセッション名を設定し、MyShoppingCart クラスの MigrateCart メソッドを呼び出して、ショッピングカート内の一時的なセッション id をユーザーの一時的なセッション id に変更します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="c57cd-125">(.Cs ファイルに実装されています)</span><span class="sxs-lookup"><span data-stu-id="c57cd-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="c57cd-126">このような MigrateCart () メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="c57cd-127">Checkout では、ショッピングカートページで行ったように、チェックアウトページで EntityDataSource と GridView を使用します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="c57cd-128">GridView コントロールで、\_MyList という名前の "ondatabound バインド" イベントハンドラーが指定されていることに注意してください。そのため、このようなイベントハンドラーを実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="c57cd-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="c57cd-129">このメソッドは、各行がバインドされ、GridView の下部の行を更新するときに、ショッピングカートの累計を保持します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="c57cd-130">この段階では、配置する順序の "レビュー" プレゼンテーションを実装しました。</span><span class="sxs-lookup"><span data-stu-id="c57cd-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="c57cd-131">次のように、ページ\_の読み込みイベントに数行のコードを追加して、空のカートシナリオを処理してみましょう。</span><span class="sxs-lookup"><span data-stu-id="c57cd-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="c57cd-132">ユーザーが [送信] ボタンをクリックすると、[送信] ボタンの [イベントハンドラー] で次のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="c57cd-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="c57cd-133">注文送信プロセスの "肉" は、MyShoppingCart クラスの SubmitOrder () メソッドに実装されます。</span><span class="sxs-lookup"><span data-stu-id="c57cd-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="c57cd-134">SubmitOrder は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="c57cd-134">SubmitOrder will:</span></span>

- <span data-ttu-id="c57cd-135">ショッピングカート内のすべての品目を取得し、それらを使用して新しい注文レコードと関連付けられた OrderDetails レコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="c57cd-136">出荷日を計算します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="c57cd-137">ショッピングカートをクリアします。</span><span class="sxs-lookup"><span data-stu-id="c57cd-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="c57cd-138">このサンプルアプリケーションでは、現在の日付に2日を加算するだけで出荷日を計算します。</span><span class="sxs-lookup"><span data-stu-id="c57cd-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="c57cd-139">今すぐアプリケーションを実行すると、ショッピングプロセスを開始から終了までテストできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c57cd-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c57cd-140">[前へ](tailspin-spyworks-part-5.md)
> [次へ](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="c57cd-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
