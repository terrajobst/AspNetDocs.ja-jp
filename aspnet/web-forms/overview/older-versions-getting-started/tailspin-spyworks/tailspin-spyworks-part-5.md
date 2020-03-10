---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 'パート 5: ビジネスロジック |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート5では、ビジネスロジックを追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511546"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="65e10-104">パート 5: ビジネスロジック</span><span class="sxs-lookup"><span data-stu-id="65e10-104">Part 5: Business Logic</span></span>

<span data-ttu-id="65e10-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="65e10-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="65e10-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="65e10-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="65e10-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="65e10-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="65e10-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="65e10-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="65e10-109">パート5では、ビジネスロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="65e10-110">ビジネスロジックの追加</span><span class="sxs-lookup"><span data-stu-id="65e10-110">Adding Some Business Logic</span></span>

<span data-ttu-id="65e10-111">だれかが web サイトにアクセスするたびに、ショッピング体験を利用できるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="65e10-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="65e10-112">訪問者は、登録されていない、またはログインしていない場合でも、商品を閲覧してショッピングカートに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="65e10-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="65e10-113">チェックアウトの準備ができたら、認証するオプションが付与され、まだメンバーでない場合はアカウントを作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="65e10-114">これは、ショッピングカートを匿名状態から "登録済みユーザー" 状態に変換するロジックを実装する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="65e10-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="65e10-115">"Classes" という名前のディレクトリを作成し、フォルダーを右クリックして、MyShoppingCart.cs という名前の新しい "Class" ファイルを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="65e10-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="65e10-116">前述のように、MyShoppingCart ページを実装するクラスを拡張します。これはを使用して行います。NET の強力な "部分クラス" コンストラクト。</span><span class="sxs-lookup"><span data-stu-id="65e10-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="65e10-117">MyShoppingCart.aspx.cf ファイルに対して生成された呼び出しは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="65e10-118">"Partial" キーワードが使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="65e10-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="65e10-119">生成したクラスファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="65e10-120">このファイルに partial キーワードを追加して、実装をマージします。</span><span class="sxs-lookup"><span data-stu-id="65e10-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="65e10-121">新しいクラスファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="65e10-122">クラスに追加する最初のメソッドは、"AddItem" メソッドです。</span><span class="sxs-lookup"><span data-stu-id="65e10-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="65e10-123">これは、ユーザーが製品リストおよび製品の詳細ページの [追加] リンクをクリックしたときに最終的に呼び出されるメソッドです。</span><span class="sxs-lookup"><span data-stu-id="65e10-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="65e10-124">ページの先頭にある using ステートメントに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="65e10-125">次に、このメソッドを MyShoppingCart クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="65e10-126">LINQ to Entities を使用して、項目が既にカートに存在するかどうかを確認しています。</span><span class="sxs-lookup"><span data-stu-id="65e10-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="65e10-127">その場合は、アイテムの注文数量を更新します。それ以外の場合は、選択したアイテムの新しいエントリを作成します。</span><span class="sxs-lookup"><span data-stu-id="65e10-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="65e10-128">このメソッドを呼び出すには、このメソッドをクラスにするだけでなく、項目が追加された後に現在のショッピング a = カートを表示する AddToCart .aspx ページを実装します。</span><span class="sxs-lookup"><span data-stu-id="65e10-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="65e10-129">ソリューションエクスプローラーでソリューション名を右クリックし、前に行ったように、AddToCart という名前の新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="65e10-130">このページを使用して、低在庫の問題などの中間結果を表示できますが、この実装では、実際にはページがレンダリングされず、代わりに "Add" ロジックとリダイレクトが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="65e10-131">これを実現するには、次のコードをページ\_Load イベントに追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="65e10-132">ここでは、クエリ文字列パラメーターからショッピングカートに追加し、クラスの AddItem メソッドを呼び出すために製品を取得していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="65e10-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="65e10-133">エラーが検出されなかった場合は、次に完全に実装する SHoppingCart ページに制御が渡されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="65e10-134">エラーが発生した場合は、例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="65e10-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="65e10-135">現在、グローバルエラーハンドラーが実装されていないため、この例外はアプリケーションによって処理されませんが、この問題はすぐに解決されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="65e10-136">また、ステートメント Debug. Fail () を使用することもできます (`using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="65e10-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="65e10-137">アプリケーションがデバッガー内で実行されている場合、このメソッドは、指定したエラーメッセージと共に、アプリケーションの状態に関する詳細なダイアログを表示します。</span><span class="sxs-lookup"><span data-stu-id="65e10-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="65e10-138">運用環境で実行する場合、Debug. Fail () ステートメントは無視されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="65e10-139">上記のコードでは、ショッピングカートのクラス名 "GetShoppingCartId" 内のメソッドの呼び出しを確認します。</span><span class="sxs-lookup"><span data-stu-id="65e10-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="65e10-140">次のように、メソッドを実装するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="65e10-141">また、[更新] ボタンと [チェックアウト] ボタン、および "合計" というカートを表示できるラベルも追加されています。</span><span class="sxs-lookup"><span data-stu-id="65e10-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="65e10-142">ショッピングカートに商品を追加できるようになりましたが、製品が追加された後にカートを表示するためのロジックが実装されていません。</span><span class="sxs-lookup"><span data-stu-id="65e10-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="65e10-143">そのため、MyShoppingCart ページで、次のように EntityDataSource コントロールと Grid e コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="65e10-144">[Update カート] ボタンをダブルクリックして、マークアップ内の宣言で指定されている click イベントハンドラーを生成できるように、デザイナーでフォームを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="65e10-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="65e10-145">後で詳細を実装しますが、これを行うと、エラーなしでアプリケーションをビルドして実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="65e10-146">アプリケーションを実行してショッピングカートに項目を追加すると、これが表示されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="65e10-147">ここでは、3つのカスタム列を実装して、"既定" のグリッド表示から逸脱しています。</span><span class="sxs-lookup"><span data-stu-id="65e10-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="65e10-148">1つ目は、数量の編集可能な "バインド" フィールドです。</span><span class="sxs-lookup"><span data-stu-id="65e10-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="65e10-149">次に示すのは、行アイテムの合計を表示する "計算された" 列 (注文する品目のコスト) です。</span><span class="sxs-lookup"><span data-stu-id="65e10-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="65e10-150">最後に、ユーザーがショッピンググラフから項目を削除することを示す CheckBox コントロールを含むカスタム列が用意されています。</span><span class="sxs-lookup"><span data-stu-id="65e10-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="65e10-151">ご覧のように、注文の合計行は空であるため、注文合計を計算するロジックを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="65e10-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="65e10-152">まず、MyShoppingCart クラスに "GetTotal" メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="65e10-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="65e10-153">MyShoppingCart.cs ファイルで、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="65e10-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="65e10-154">次に、ページ\_Load イベントハンドラーで GetTotal メソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="65e10-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="65e10-155">同時に、ショッピングカートが空かどうかを確認するテストを追加し、必要に応じて表示を調整します。</span><span class="sxs-lookup"><span data-stu-id="65e10-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="65e10-156">ショッピングカートが空の場合、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="65e10-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="65e10-157">そうでない場合は、合計が表示されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="65e10-158">ただし、このページはまだ完了していません。</span><span class="sxs-lookup"><span data-stu-id="65e10-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="65e10-159">購入カートを再計算するには、追加のロジックが必要になります。削除のマークが付けられた項目を削除し、ユーザーがグリッド内で変更された可能性のある新しい数量の値を確認します。</span><span class="sxs-lookup"><span data-stu-id="65e10-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="65e10-160">MyShoppingCart.cs のショッピングカートクラスに "RemoveItem" メソッドを追加して、ユーザーが項目を削除対象としてマークした場合に対処できるようにします。</span><span class="sxs-lookup"><span data-stu-id="65e10-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="65e10-161">ここで、ユーザーが GridView での品質を変更するだけの状況を処理するメソッドを ad に渡します。</span><span class="sxs-lookup"><span data-stu-id="65e10-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="65e10-162">基本的な削除機能と更新機能を使用すると、データベース内のショッピングカートを実際に更新するロジックを実装できます。</span><span class="sxs-lookup"><span data-stu-id="65e10-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="65e10-163">(MyShoppingCart.cs 内)</span><span class="sxs-lookup"><span data-stu-id="65e10-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="65e10-164">このメソッドには2つのパラメーターが必要であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="65e10-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="65e10-165">1つはショッピングカート Id で、もう1つはユーザー定義型のオブジェクトの配列です。</span><span class="sxs-lookup"><span data-stu-id="65e10-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="65e10-166">そのため、ユーザーインターフェイスの詳細に対するロジックの依存関係を最小限に抑えるために、GridView コントロールに直接アクセスする必要のないメソッドを使用せずに、ショッピングカートの項目をコードに渡すために使用できるデータ構造を定義しました。</span><span class="sxs-lookup"><span data-stu-id="65e10-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="65e10-167">MyShoppingCart.aspx.cs ファイルでは、次のように、[更新] ボタンの [イベントハンドラー] でこの構造を使用できます。</span><span class="sxs-lookup"><span data-stu-id="65e10-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="65e10-168">カートの更新に加えて、カートの合計も更新されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="65e10-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="65e10-169">特に次のコード行に注目してください。</span><span class="sxs-lookup"><span data-stu-id="65e10-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="65e10-170">GetValues () は、次のように MyShoppingCart.aspx.cs に実装する特別なヘルパー関数です。</span><span class="sxs-lookup"><span data-stu-id="65e10-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="65e10-171">これにより、GridView コントロールのバインドされた要素の値にアクセスするためのクリーンな方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="65e10-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="65e10-172">[項目の削除] チェックボックスコントロールはバインドされていないため、FindControl () メソッドを使用してアクセスします。</span><span class="sxs-lookup"><span data-stu-id="65e10-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="65e10-173">プロジェクトの開発のこの段階では、チェックアウトプロセスを実装する準備が整います。</span><span class="sxs-lookup"><span data-stu-id="65e10-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="65e10-174">これを行う前に、Visual Studio を使用してメンバーシップデータベースを生成し、メンバーシップリポジトリにユーザーを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="65e10-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65e10-175">[前へ](tailspin-spyworks-part-4.md)
> [次へ](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="65e10-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
