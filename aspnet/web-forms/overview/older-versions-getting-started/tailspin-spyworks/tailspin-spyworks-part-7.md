---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 'パート 7: 機能の追加 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート7では、account 確認などの機能が追加されています。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521566"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="cc2c9-104">パート 7: 機能の追加</span><span class="sxs-lookup"><span data-stu-id="cc2c9-104">Part 7: Adding Features</span></span>

<span data-ttu-id="cc2c9-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="cc2c9-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="cc2c9-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="cc2c9-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="cc2c9-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="cc2c9-109">パート7では、アカウントレビュー、製品レビュー、"人気のあるアイテム"、"購入した" ユーザーコントロールなどの追加機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="cc2c9-110">機能の追加</span><span class="sxs-lookup"><span data-stu-id="cc2c9-110">Adding Features</span></span>

<span data-ttu-id="cc2c9-111">ユーザーはカタログを参照し、ショッピングカートにアイテムを配置し、チェックアウトプロセスを完了することができますが、サイトを改善するためのサポート機能がいくつか用意されています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="cc2c9-112">アカウントレビュー (注文の一覧表示と詳細の表示)</span><span class="sxs-lookup"><span data-stu-id="cc2c9-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="cc2c9-113">コンテキスト固有のコンテンツを前面ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="cc2c9-114">カタログ内の製品をユーザーが確認できるようにする機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="cc2c9-115">人気のある項目を表示し、そのコントロールを前面のページに配置するユーザーコントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="cc2c9-116">"購入済み" のユーザーコントロールを作成し、[製品の詳細] ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="cc2c9-117">連絡先ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="cc2c9-118">[バージョン情報] ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-118">Add an About Page.</span></span>
8. <span data-ttu-id="cc2c9-119">グローバルエラー</span><span class="sxs-lookup"><span data-stu-id="cc2c9-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="cc2c9-120">アカウントのレビュー</span><span class="sxs-lookup"><span data-stu-id="cc2c9-120">Account Review</span></span>

<span data-ttu-id="cc2c9-121">"Account" フォルダーで、OrderList という名前の2つの .aspx ページを作成し、OrderDetails という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="cc2c9-122">OrderList .aspx では、以前と同じように GridView と EntityDataSource のコントロールが活用されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="cc2c9-123">EntityDataSource は、ユーザーのログイン時にセッション変数に設定されている、ユーザー名でフィルター処理された Orders テーブルからレコードを選択します (where-object パラメーターを参照)。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="cc2c9-124">GridView の [ハイパーリンク] フィールドにも、次のパラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="cc2c9-125">これらは、各製品の注文詳細ビューへのリンクを指定します。これは、OrderDetails ページの QueryString パラメーターとして OrderID フィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="cc2c9-126">OrderDetails</span><span class="sxs-lookup"><span data-stu-id="cc2c9-126">OrderDetails.aspx</span></span>

<span data-ttu-id="cc2c9-127">注文データを表示するために EntityDataSource コントロールを使用し、他の EntityDataSource を GridView と共に使用して注文のすべての行項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="cc2c9-128">分離コードファイル (OrderDetails.aspx.cs) には、2つの簡単なハウスキーピングがあります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="cc2c9-129">まず、OrderDetails が常に OrderId を取得するようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="cc2c9-130">また、行アイテムから注文合計を計算して表示する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="cc2c9-131">ホームページ</span><span class="sxs-lookup"><span data-stu-id="cc2c9-131">The Home Page</span></span>

<span data-ttu-id="cc2c9-132">Default.aspx ページに静的コンテンツをいくつか追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="cc2c9-133">まず、"Content" フォルダーを作成し、Images フォルダー内に作成します (ホームページで使用するイメージを含めます)。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="cc2c9-134">Default.aspx ページの下のプレースホルダーに、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="cc2c9-135">製品レビュー</span><span class="sxs-lookup"><span data-stu-id="cc2c9-135">Product Reviews</span></span>

<span data-ttu-id="cc2c9-136">まず、製品レビューを開始するために使用できるフォームへのリンクを含むボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="cc2c9-137">クエリ文字列で ProductID を渡していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="cc2c9-138">次に、ReviewAdd という名前のページを追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="cc2c9-139">このページでは、ASP.NET AJAX Control Toolkit を使用します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="cc2c9-140">まだ実行していない場合は、 [Devexpress](http://devexpress.com/act)からダウンロードできます。このツールキットを Visual Studio で使用するための設定については、 [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="cc2c9-141">デザインモードで、[ツールボックス] からコントロールとバリデーターをドラッグし、次のようなフォームを作成します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="cc2c9-142">マークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="cc2c9-143">レビューを入力できるようになったので、これらのレビューを製品ページで表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="cc2c9-144">このマークアップを ProductDetails .aspx ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="cc2c9-145">ここでアプリケーションを実行し、製品に移動すると、顧客のレビューなどの製品情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="cc2c9-146">一般的な項目コントロール (ユーザーコントロールの作成)</span><span class="sxs-lookup"><span data-stu-id="cc2c9-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="cc2c9-147">Web サイトの売上を向上させるために、人気のある製品や関連製品を "推奨販売" する機能をいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="cc2c9-148">これらの機能の1つは、製品カタログの人気のある製品の一覧です。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="cc2c9-149">"ユーザーコントロール" を作成して、アプリケーションのホームページで上位の販売項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="cc2c9-150">これはコントロールであるため、Visual Studio のデザイナーでコントロールを任意のページにドラッグアンドドロップするだけで、任意のページで使用できます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="cc2c9-151">Visual Studio のソリューションエクスプローラーで、ソリューション名を右クリックし、"Controls" という名前の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="cc2c9-152">これを行う必要はありませんが、"Controls" ディレクトリにすべてのユーザーコントロールを作成して、プロジェクトを整理したままにしておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="cc2c9-153">[コントロール] フォルダーを右クリックし、[新しい項目] を選択します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="cc2c9-154">"PopularItems" のコントロールの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="cc2c9-155">ユーザーコントロールのファイル拡張子は .ascx ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="cc2c9-156">人気のある項目のユーザーコントロールは、次のように定義されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="cc2c9-157">ここでは、このアプリケーションでまだ使用していないメソッドを使用しています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="cc2c9-158">Repeater コントロールを使用しています。データソースコントロールを使用する代わりに、Repeater コントロールを LINQ to Entities クエリの結果にバインドしています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="cc2c9-159">コントロールの分離コードでは、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="cc2c9-160">また、この重要な行は、コントロールのマークアップの上部にあります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="cc2c9-161">最も人気のある項目は分単位で変更されないため、aching ディレクティブを追加してアプリケーションのパフォーマンスを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="cc2c9-162">このディレクティブを使用すると、コントロールのキャッシュされた出力の有効期限が切れたときにのみ、コントロールコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="cc2c9-163">それ以外の場合は、コントロールの出力のキャッシュされたバージョンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="cc2c9-164">次に、default.aspx ページに新しいコントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="cc2c9-165">ドラッグアンドドロップを使用して、既定のフォームの [開く] 列にコントロールのインスタンスを配置します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="cc2c9-166">アプリケーションを実行すると、最も人気のある項目がホームページに表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="cc2c9-167">"購入済み" コントロール (パラメーターを使用したユーザーコントロール)</span><span class="sxs-lookup"><span data-stu-id="cc2c9-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="cc2c9-168">2番目に作成するユーザーコントロールは、コンテキストの特異性を追加することによって、次のレベルに推奨することになります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="cc2c9-169">上位の "購入した" 項目を計算するロジックは、重要ではありません。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="cc2c9-170">"購入済み" コントロールは、現在選択されている ProductID の OrderDetails レコード (以前に購入したもの) を選択し、見つかった一意の注文ごとに OrderIDs を取得します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="cc2c9-171">次に、これらすべての注文から製品を選択し、購入した数量を合計します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="cc2c9-172">製品をその数量の合計で並べ替え、上位5つの項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="cc2c9-173">このロジックが複雑になると、このアルゴリズムはストアドプロシージャとして実装されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="cc2c9-174">ストアドプロシージャの T-sql は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="cc2c9-175">このストアドプロシージャ (SelectPurchasedWithProducts) は、アプリケーションに含まれていたデータベース内に存在していたので Entity Data Model、必要なテーブルとビューに加えて、必要なテーブルとビューに加えて、Entity Data Model を生成した場合は、次のように指定されていることに注意してください。には、このストアドプロシージャを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="cc2c9-176">Entity Data Model からストアドプロシージャにアクセスするには、関数をインポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="cc2c9-177">ソリューションエクスプローラーで Entity Data Model をダブルクリックしてデザイナーで開き、モデルブラウザーを開き、デザイナーで右クリックして、[関数インポートの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="cc2c9-178">そうすると、このダイアログが開きます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="cc2c9-179">上記のフィールドに入力し、"SelectPurchasedWithProducts" を選択して、インポートした関数の名前としてプロシージャ名を使用します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="cc2c9-180">[Ok] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-180">Click "Ok".</span></span>

<span data-ttu-id="cc2c9-181">これを行うには、モデル内の他の項目と同じように、ストアドプロシージャに対してプログラミングするだけです。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="cc2c9-182">そのため、"コントロール" フォルダーで、AlsoPurchased という名前の新しいユーザーコントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="cc2c9-183">このコントロールのマークアップは、PopularItems コントロールに非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="cc2c9-184">注目すべき違いは、表示される項目の内容が製品によって異なるため、出力がキャッシュされないことです。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="cc2c9-185">ProductId は、コントロールの "プロパティ" になります。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="cc2c9-186">コントロールの PreRender イベントハンドラーで、3つの処理を eed します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="cc2c9-187">ProductID が設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="cc2c9-188">現在の製品が購入されている製品があるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="cc2c9-189">#2 で決定されたとおりに項目を出力します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="cc2c9-190">モデルを通じてストアドプロシージャを呼び出すことがいかに簡単であるかに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="cc2c9-191">「購入済み」があることを確認した後は、クエリによって返された結果にリピータをバインドするだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="cc2c9-192">"購入済み" の項目がない場合は、カタログから他の人気のある項目を表示するだけです。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="cc2c9-193">"購入済み" の項目を表示するには、ProductDetails .aspx ページを開き、ソリューションエクスプローラーから AlsoPurchased コントロールをドラッグして、マークアップ内のこの位置に表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="cc2c9-194">これにより、ProductDetails ページの上部にコントロールへの参照が作成されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="cc2c9-195">AlsoPurchased ユーザーコントロールには ProductId 番号が必要であるため、ページの現在のデータモデルアイテムに対して Eval ステートメントを使用して、コントロールの ProductID プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="cc2c9-196">今すぐビルドして実行し、製品を参照すると、"購入済み" の項目も表示されます。</span><span class="sxs-lookup"><span data-stu-id="cc2c9-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="cc2c9-197">[前へ](tailspin-spyworks-part-6.md)
> [次へ](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="cc2c9-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
