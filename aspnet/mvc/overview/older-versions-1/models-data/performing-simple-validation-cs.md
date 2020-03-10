---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: 単純な検証をC#実行する () |Microsoft Docs
author: StephenWalther
description: ASP.NET MVC アプリケーションで検証を実行する方法について説明します。 このチュートリアルでは、Stephen Walther がモデルの状態と検証 HTML ヘルパーについて説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: e33f522af74efe97b5a245e956bc0b918ea769af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436720"
---
# <a name="performing-simple-validation-c"></a><span data-ttu-id="ea5ff-104">簡易検証を実行する (C#)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-104">Performing Simple Validation (C#)</span></span>

<span data-ttu-id="ea5ff-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="ea5ff-106">ASP.NET MVC アプリケーションで検証を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="ea5ff-107">このチュートリアルでは、Stephen Walther が、モデルの状態と検証 HTML ヘルパーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>

<span data-ttu-id="ea5ff-108">このチュートリアルの目的は、ASP.NET MVC アプリケーション内で検証を実行する方法について説明することです。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="ea5ff-109">たとえば、必要なフィールドの値が含まれていないユーザーがフォームを送信できないようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="ea5ff-110">モデルの状態と検証 HTML ヘルパーを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="ea5ff-111">モデルの状態について</span><span class="sxs-lookup"><span data-stu-id="ea5ff-111">Understanding Model State</span></span>

<span data-ttu-id="ea5ff-112">検証エラーを表すには、モデル状態を使用するか、より正確にモデル状態ディクショナリを使用します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="ea5ff-113">たとえば、リスト1の Create () アクションは、Product クラスをデータベースに追加する前に、Product クラスのプロパティを検証します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>

<span data-ttu-id="ea5ff-114">検証またはデータベースロジックをコントローラーに追加することは推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="ea5ff-115">コントローラーには、アプリケーションフロー制御に関連するロジックのみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="ea5ff-116">単純なものを保持するためのショートカットがあります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-116">We are taking a shortcut to keep things simple.</span></span>

<span data-ttu-id="ea5ff-117">**リスト 1-コントローラー (productコントローラー)**</span><span class="sxs-lookup"><span data-stu-id="ea5ff-117">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

<span data-ttu-id="ea5ff-118">リスト1では、Product クラスの名前、説明、および在庫プロパティが検証されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="ea5ff-119">これらのプロパティのいずれかが検証テストに失敗した場合、モデル状態ディクショナリ (コントローラークラスの ModelState プロパティで表される) にエラーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="ea5ff-120">モデル状態にエラーがある場合、ModelState. IsValid プロパティは false を返します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="ea5ff-121">この場合、新しい製品を作成するための HTML フォームが再生成されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="ea5ff-122">それ以外の場合、検証エラーがない場合は、新しい製品がデータベースに追加されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="ea5ff-123">検証ヘルパーの使用</span><span class="sxs-lookup"><span data-stu-id="ea5ff-123">Using the Validation Helpers</span></span>

<span data-ttu-id="ea5ff-124">ASP.NET MVC フレームワークには、2つの検証ヘルパー (Html. ValidationMessage () ヘルパーと Html. Validationmessage () ヘルパー) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="ea5ff-125">ビューでこれらの2つのヘルパーを使用して、検証エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="ea5ff-126">ASP.NET MVC スキャフォールディングによって自動的に生成される Create ビューと Edit ビューでは、Html の ValidationMessage () ヘルパーと Html. Validationmessage () ヘルパーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="ea5ff-127">作成ビューを生成するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="ea5ff-128">製品コントローラーで [作成] () アクションを右クリックし、[ビューの**追加**] メニューオプションを選択します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="ea5ff-129">**[ビューの追加]** ダイアログで、厳密に型指定され **[たビューを作成する]** チェックボックスをオンにします (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="ea5ff-130">**[データクラスの表示]** ドロップダウンリストから、Product クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="ea5ff-131">**ビューコンテンツ** ボックスの一覧から 作成 を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="ea5ff-132">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-132">Click the **Add** button.</span></span>

<span data-ttu-id="ea5ff-133">ビューを追加する前に、アプリケーションをビルドしていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="ea5ff-134">それ以外の場合は、 **[ビューデータクラス]** ボックスの一覧にクラスの一覧が表示されません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>

<span data-ttu-id="ea5ff-135">[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-135">[![The New Project dialog box](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="ea5ff-136">**図 01**: ビューを追加[する (クリックすると、フルサイズの画像が表示](performing-simple-validation-cs/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-cs/_static/image2.png))</span></span>

<span data-ttu-id="ea5ff-137">[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-137">[![The New Project dialog box](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span></span>

<span data-ttu-id="ea5ff-138">**図 02**: 厳密に型指定されたビューの作成 ([クリックすると、フルサイズの画像が表示](performing-simple-validation-cs/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-cs/_static/image4.png))</span></span>

<span data-ttu-id="ea5ff-139">これらの手順を完了すると、リスト2の [作成] ビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="ea5ff-140">**リスト 2-Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="ea5ff-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

<span data-ttu-id="ea5ff-141">リスト2では、html 形式ではすぐに html 形式の Summary () ヘルパーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="ea5ff-142">このヘルパーは、検証エラーメッセージの一覧を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="ea5ff-143">Html. ValidationSummary () ヘルパーは、箇条書きでエラーを表示します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="ea5ff-144">Html の ValidationMessage () ヘルパーは、各 HTML フォームフィールドの横に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="ea5ff-145">このヘルパーは、フォームフィールドの横にエラーメッセージを表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="ea5ff-146">リスト2の場合、エラーが発生すると、Html. ValidationMessage () ヘルパーにアスタリスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="ea5ff-147">図3のページは、不足しているフィールドと無効な値を使用してフォームを送信したときに検証ヘルパーによって表示されるエラーメッセージを示しています。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>

<span data-ttu-id="ea5ff-148">[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-148">[![The New Project dialog box](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span></span>

<span data-ttu-id="ea5ff-149">**図 03**: 問題が発生して送信される作成ビュー ([クリックすると、フルサイズの画像が表示](performing-simple-validation-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-cs/_static/image6.png))</span></span>

<span data-ttu-id="ea5ff-150">検証エラーが発生すると、HTML 入力フィールドの外観も変更されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="ea5ff-151">.Html () ヘルパーは、Html. TextBox () ヘルパーによってレンダリングされるプロパティに関連付けられている検証エラーがある場合に、 *class = "input-validation-error"* 属性をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="ea5ff-152">検証エラーの表示を制御するために使用されるカスケードスタイルシートクラスには、次の3つがあります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="ea5ff-153">入力-検証-エラー-Html. TextBox () ヘルパーによってレンダリングされる &lt;入力&gt; タグに適用されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="ea5ff-154">フィールド検証-エラー-&lt;スパン&gt; タグに適用されます。これは、Html. ValidationMessage () ヘルパーによって表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="ea5ff-155">検証-概要-エラー-Html. ValidationSummary () ヘルパーによってレンダリングされる &lt;ul&gt; タグに適用されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSummary() helper.</span></span>

<span data-ttu-id="ea5ff-156">これらのカスケードスタイルシートクラスを変更して、コンテンツフォルダーに配置されているサイトの .css ファイルを変更することで、検証エラーの外観を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ea5ff-157">HtmlHelper クラスには、検証に関連する CSS クラスの名前を取得するための読み取り専用の静的プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="ea5ff-158">これらの静的プロパティの名前は、ValidationInputCssClassName、ValidationValidationSummaryCssClassName、およびです。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>

## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="ea5ff-159">事前バインディング検証と Postbinding 検証</span><span class="sxs-lookup"><span data-stu-id="ea5ff-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="ea5ff-160">製品を作成するための HTML フォームを送信したときに、[価格] フィールドに無効な値を入力し、[在庫管理] フィールドに値が入力されていない場合は、図4に検証メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="ea5ff-161">これらの検証エラーメッセージの発信元</span><span class="sxs-lookup"><span data-stu-id="ea5ff-161">Where do these validation error messages come from?</span></span>

<span data-ttu-id="ea5ff-162">[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-162">[![The New Project dialog box](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span></span>

<span data-ttu-id="ea5ff-163">**図 04**: 事前バインディングの検証エラー ([クリックしてフルサイズのイメージを表示](performing-simple-validation-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="ea5ff-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-cs/_static/image8.png))</span></span>

<span data-ttu-id="ea5ff-164">実際には、2種類の検証エラーメッセージ (HTML フォームフィールドがクラスにバインドされる前に生成されたものと、フォームフィールドがクラスにバインドされた後に生成されたもの) があります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="ea5ff-165">つまり、事前バインディング検証エラーと postbinding 検証エラーがあります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="ea5ff-166">リスト1の製品コントローラーによって公開される Create () アクションでは、Product クラスのインスタンスが受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="ea5ff-167">Create メソッドのシグネチャは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-167">The signature of the Create method looks like this:</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

<span data-ttu-id="ea5ff-168">作成フォームの HTML フォームフィールドの値は、モデルバインダーと呼ばれるものによって productToCreate クラスにバインドされます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="ea5ff-169">既定のモデルバインダーは、フォームフィールドをフォームプロパティにバインドできない場合に、エラーメッセージをモデル状態に自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="ea5ff-170">既定のモデルバインダーは、文字列 "apple" を Product クラスの Price プロパティにバインドできません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="ea5ff-171">Decimal プロパティに文字列を割り当てることはできません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="ea5ff-172">そのため、モデルバインダーは、モデルの状態にエラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="ea5ff-173">既定のモデルバインダーでは、null 値を許容しないプロパティに null 値を割り当てることもできません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-173">The default model binder also cannot assign a null value to a property that does not accept nulls.</span></span> <span data-ttu-id="ea5ff-174">特に、モデルバインダーは、在庫プロパティに null 値を割り当てることはできません。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-174">In particular, the model binder cannot assign a null value to the UnitsInStock property.</span></span> <span data-ttu-id="ea5ff-175">この場合も、モデルバインダーによってエラーメッセージがモデルの状態に追加されます。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="ea5ff-176">これらのプリバインドエラーメッセージの外観をカスタマイズする場合は、これらのメッセージのリソース文字列を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="ea5ff-177">まとめ</span><span class="sxs-lookup"><span data-stu-id="ea5ff-177">Summary</span></span>

<span data-ttu-id="ea5ff-178">このチュートリアルの目的は、ASP.NET MVC フレームワークでの検証の基本的なしくみを説明することでした。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="ea5ff-179">モデルの状態と検証 HTML ヘルパーの使用方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="ea5ff-180">また、prebinding と postbinding の検証の違いについても説明しました。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="ea5ff-181">他のチュートリアルでは、検証コードをコントローラーからモデルクラスに移行するためのさまざまな戦略について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea5ff-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ea5ff-182">[前へ](displaying-a-table-of-database-data-cs.md)
> [次へ](validating-with-the-idataerrorinfo-interface-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ea5ff-182">[Previous](displaying-a-table-of-database-data-cs.md)
[Next](validating-with-the-idataerrorinfo-interface-cs.md)</span></span>
