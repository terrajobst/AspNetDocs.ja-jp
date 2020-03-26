---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'イテレーション #3 –フォーム検証の追加C#() |Microsoft Docs'
author: microsoft
description: 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: af2e86e820f60f0a3d8e3db8f78eba67ef63579a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437986"
---
# <a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="01079-105">イテレーション #3 –フォーム検証の追加C#()</span><span class="sxs-lookup"><span data-stu-id="01079-105">Iteration #3 – Add form validation (C#)</span></span>

<span data-ttu-id="01079-106">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="01079-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="01079-107">コードのダウンロード</span><span class="sxs-lookup"><span data-stu-id="01079-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="01079-108">3番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="01079-109">必要なフォームフィールドを完了しないで、フォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="01079-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="01079-110">また、電子メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="01079-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="01079-111">Contact Management ASP.NET MVC アプリケーションの構築 (C#)</span><span class="sxs-lookup"><span data-stu-id="01079-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="01079-112">この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。</span><span class="sxs-lookup"><span data-stu-id="01079-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="01079-113">連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレスなど) をユーザーの一覧に格納できます。</span><span class="sxs-lookup"><span data-stu-id="01079-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="01079-114">複数のイテレーションに対してアプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="01079-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="01079-115">各イテレーションで、アプリケーションを段階的に改善します。</span><span class="sxs-lookup"><span data-stu-id="01079-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="01079-116">この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="01079-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="01079-117">イテレーション #1-アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="01079-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="01079-118">最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。</span><span class="sxs-lookup"><span data-stu-id="01079-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="01079-119">基本的なデータベース操作のサポートを追加します。作成、読み取り、更新、および削除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="01079-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="01079-120">イテレーション #2-アプリケーションの外観を良くします。</span><span class="sxs-lookup"><span data-stu-id="01079-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="01079-121">このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。</span><span class="sxs-lookup"><span data-stu-id="01079-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="01079-122">イテレーション #3-フォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="01079-123">3番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="01079-124">必要なフォームフィールドを完了しないで、フォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="01079-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="01079-125">また、電子メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="01079-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="01079-126">イテレーション #4-アプリケーションの疎結合を実現します。</span><span class="sxs-lookup"><span data-stu-id="01079-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="01079-127">この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="01079-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="01079-128">たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="01079-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="01079-129">イテレーション #5-単体テストを作成します。</span><span class="sxs-lookup"><span data-stu-id="01079-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="01079-130">5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。</span><span class="sxs-lookup"><span data-stu-id="01079-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="01079-131">データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。</span><span class="sxs-lookup"><span data-stu-id="01079-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="01079-132">イテレーション #6-テスト駆動型開発を使用します。</span><span class="sxs-lookup"><span data-stu-id="01079-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="01079-133">この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="01079-134">このイテレーションでは、連絡先グループを追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="01079-135">イテレーション #7-Ajax 機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="01079-136">7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。</span><span class="sxs-lookup"><span data-stu-id="01079-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="01079-137">このイテレーション</span><span class="sxs-lookup"><span data-stu-id="01079-137">This Iteration</span></span>

<span data-ttu-id="01079-138">Contact Manager アプリケーションのこの2回目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="01079-139">必須フォームフィールドの値を入力することなく、連絡先を送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="01079-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="01079-140">また、電話番号と電子メールアドレスも検証します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="01079-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="01079-141">[[新しいプロジェクト] ダイアログボックスの ![](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="01079-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="01079-142">**図 01**:検証付きのフォーム ([クリックすると、フルサイズの画像が表示](iteration-3-add-form-validation-cs/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="01079-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>

<span data-ttu-id="01079-143">このイテレーションでは、コントローラーアクションに検証ロジックを直接追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="01079-144">一般に、ASP.NET MVC アプリケーションに検証を追加する方法として推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="01079-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="01079-145">より優れたアプローチは、アプリケーションの検証ロジックを別の[サービス層](http://martinfowler.com/eaaCatalog/serviceLayer.html)に配置することです。</span><span class="sxs-lookup"><span data-stu-id="01079-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="01079-146">次のイテレーションでは、アプリケーションの保守が容易になるように Contact Manager アプリケーションをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="01079-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="01079-147">このイテレーションでは、簡単にするために、すべての検証コードを手動で記述します。</span><span class="sxs-lookup"><span data-stu-id="01079-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="01079-148">検証コードを自分で記述する代わりに、検証フレームワークを利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="01079-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="01079-149">たとえば、Microsoft エンタープライズライブラリ検証アプリケーションブロック (VAB) を使用して、ASP.NET MVC アプリケーションの検証ロジックを実装できます。</span><span class="sxs-lookup"><span data-stu-id="01079-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="01079-150">検証アプリケーションブロックの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="01079-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="01079-151">Create ビューへの検証の追加</span><span class="sxs-lookup"><span data-stu-id="01079-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="01079-152">まず、検証ロジックを Create ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="01079-153">幸い、Visual Studio で作成ビューを生成したため、検証メッセージを表示するために必要なすべてのユーザーインターフェイスロジックが既に作成ビューに含まれています。</span><span class="sxs-lookup"><span data-stu-id="01079-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="01079-154">[作成] ビューは、リスト1に含まれています。</span><span class="sxs-lookup"><span data-stu-id="01079-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="01079-155">**Listing 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="01079-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="01079-156">Html フォームのすぐ上に表示される、Html. ValidationSummary () ヘルパーメソッドへの呼び出しに注意してください。</span><span class="sxs-lookup"><span data-stu-id="01079-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="01079-157">検証エラーメッセージがある場合、このメソッドは、箇条書きリストに検証メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="01079-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="01079-158">さらに、各フォームフィールドの横に表示される Html の ValidationMessage () の呼び出しに注目してください。</span><span class="sxs-lookup"><span data-stu-id="01079-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="01079-159">ValidationMessage () ヘルパーは、個々の検証エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="01079-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="01079-160">リスト1の場合は、検証エラーが発生したときにアスタリスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="01079-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="01079-161">最後に、ヘルパーによって表示されるプロパティに関連付けられている検証エラーが発生すると、Html の TextBox () ヘルパーはカスケードスタイルシートクラスを自動的にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="01079-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="01079-162">.Html () ヘルパーは、**入力検証-エラー**という名前のクラスをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="01079-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="01079-163">新しい ASP.NET MVC アプリケーションを作成すると、[Content] フォルダーに "" という名前のスタイルシートが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="01079-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="01079-164">このスタイルシートには、検証エラーメッセージの外観に関連する CSS クラスの次の定義が含まれています。</span><span class="sxs-lookup"><span data-stu-id="01079-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="01079-165">フィールド検証-エラークラスは、Html. ValidationMessage () ヘルパーによって表示される出力のスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="01079-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="01079-166">入力検証-エラークラスは、Html の TextBox () ヘルパーによって表示されるテキストボックスのスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="01079-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="01079-167">"検証-概要-エラー" クラスは、Html. ValidationSummary () ヘルパーによって表示される順序付けられていないリストのスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="01079-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="01079-168">このセクションで説明するスタイルシートクラスを変更して、検証エラーメッセージの外観をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="01079-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="01079-169">作成アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="01079-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="01079-170">現時点では、メッセージを生成するロジックが記述されていないため、Create view は検証エラーメッセージを表示しません。</span><span class="sxs-lookup"><span data-stu-id="01079-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="01079-171">検証エラーメッセージを表示するには、エラーメッセージを ModelState に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="01079-172">UpdateModel () メソッドは、フォームフィールドの値をプロパティに割り当てるときにエラーが発生した場合に、エラーメッセージを ModelState に自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="01079-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="01079-173">たとえば、文字列 "apple" を DateTime 値を受け取る "誕生日" プロパティに割り当てようとすると、UpdateModel () メソッドによって ModelState にエラーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="01079-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="01079-174">リスト2の Create () メソッドを変更すると、新しい連絡先がデータベースに挿入される前に Contact クラスのプロパティを検証する新しいセクションが追加されます。</span><span class="sxs-lookup"><span data-stu-id="01079-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="01079-175">**リスト 2-コントローラー (検証を使用した作成)**</span><span class="sxs-lookup"><span data-stu-id="01079-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="01079-176">Validate セクションでは、4つの異なる検証規則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="01079-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="01079-177">FirstName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)</span><span class="sxs-lookup"><span data-stu-id="01079-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="01079-178">LastName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)</span><span class="sxs-lookup"><span data-stu-id="01079-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="01079-179">Phone プロパティの値が (長さが0より大きい) 場合、Phone プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="01079-180">Email プロパティの値が (長さが0より大きい) 場合、Email プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="01079-181">検証規則違反が発生すると、AddModelError () メソッドを使用してエラーメッセージが ModelState に追加されます。</span><span class="sxs-lookup"><span data-stu-id="01079-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="01079-182">ModelState にメッセージを追加する場合は、プロパティの名前と検証エラーメッセージのテキストを指定します。</span><span class="sxs-lookup"><span data-stu-id="01079-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="01079-183">このエラーメッセージは、Html. ValidationSummary () および Html の Validationsummary () ヘルパーメソッドによってビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="01079-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="01079-184">検証規則が実行されると、ModelState の IsValid プロパティがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="01079-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="01079-185">IsValid プロパティは、ModelState に検証エラーメッセージが追加されたときに false を返します。</span><span class="sxs-lookup"><span data-stu-id="01079-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="01079-186">検証が失敗すると、エラーメッセージと共に作成フォームが再生成されます。</span><span class="sxs-lookup"><span data-stu-id="01079-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="01079-187">の正規表現リポジトリから電話番号と電子メールアドレスを検証する正規表現があります。 [ *http://regexlib.com* ](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="01079-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="01079-188">編集アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="01079-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="01079-189">Edit () アクションを実行すると、連絡先が更新されます。</span><span class="sxs-lookup"><span data-stu-id="01079-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="01079-190">Edit () アクションでは、Create () アクションとまったく同じ検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="01079-191">同じ検証コードを複製するのではなく、Create () と Edit () の両方のアクションが同じ検証メソッドを呼び出すように Contact controller をリファクターする必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="01079-192">変更した Contact controller クラスは、リスト3に含まれています。</span><span class="sxs-lookup"><span data-stu-id="01079-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="01079-193">このクラスには、Create () アクションと Edit () アクションの両方で呼び出される新しい ValidateContact () メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="01079-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="01079-194">**Listing 3 - Controllers\ContactController.cs**</span><span class="sxs-lookup"><span data-stu-id="01079-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="01079-195">まとめ</span><span class="sxs-lookup"><span data-stu-id="01079-195">Summary</span></span>

<span data-ttu-id="01079-196">このイテレーションでは、Contact Manager アプリケーションに基本的なフォーム検証を追加しました。</span><span class="sxs-lookup"><span data-stu-id="01079-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="01079-197">この検証ロジックにより、ユーザーは FirstName プロパティと LastName プロパティの値を指定せずに、新しい連絡先を送信したり、既存の連絡先を編集したりすることができなくなります。</span><span class="sxs-lookup"><span data-stu-id="01079-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="01079-198">さらに、ユーザーは有効な電話番号と電子メールアドレスを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01079-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="01079-199">このイテレーションでは、最も簡単な方法で Contact Manager アプリケーションに検証ロジックを追加しました。</span><span class="sxs-lookup"><span data-stu-id="01079-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="01079-200">ただし、検証ロジックをコントローラーロジックに混在させると、長期的に問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="01079-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="01079-201">時間の経過と共に、アプリケーションの保守と変更が困難になります。</span><span class="sxs-lookup"><span data-stu-id="01079-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="01079-202">次のイテレーションでは、検証ロジックとデータベースアクセスロジックをコントローラーからリファクターします。</span><span class="sxs-lookup"><span data-stu-id="01079-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="01079-203">複数のソフトウェア設計原則を利用して、より疎結合で保守性の高いアプリケーションを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="01079-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="01079-204">[前へ](iteration-2-make-the-application-look-nice-cs.md)
> [次へ](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="01079-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>
