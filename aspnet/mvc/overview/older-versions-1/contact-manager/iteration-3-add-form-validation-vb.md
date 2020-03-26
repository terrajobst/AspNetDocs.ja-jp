---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 'イテレーション #3 –フォーム検証を追加する (VB) |Microsoft Docs'
author: microsoft
description: 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437968"
---
# <a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="9d326-105">イテレーション #3 –フォーム検証の追加 (VB)</span><span class="sxs-lookup"><span data-stu-id="9d326-105">Iteration #3 – Add form validation (VB)</span></span>

<span data-ttu-id="9d326-106">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9d326-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9d326-107">コードのダウンロード</span><span class="sxs-lookup"><span data-stu-id="9d326-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="9d326-108">3番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="9d326-109">必要なフォームフィールドを完了しないで、フォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="9d326-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="9d326-110">また、電子メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="9d326-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="9d326-111">Contact Management ASP.NET MVC アプリケーションの構築 (VB)</span><span class="sxs-lookup"><span data-stu-id="9d326-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="9d326-112">この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。</span><span class="sxs-lookup"><span data-stu-id="9d326-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="9d326-113">連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレスなど) をユーザーの一覧に格納できます。</span><span class="sxs-lookup"><span data-stu-id="9d326-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="9d326-114">複数のイテレーションに対してアプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="9d326-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="9d326-115">各イテレーションで、アプリケーションを段階的に改善します。</span><span class="sxs-lookup"><span data-stu-id="9d326-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="9d326-116">この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="9d326-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="9d326-117">イテレーション #1-アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="9d326-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="9d326-118">最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。</span><span class="sxs-lookup"><span data-stu-id="9d326-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="9d326-119">基本的なデータベース操作のサポートを追加します。作成、読み取り、更新、および削除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="9d326-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="9d326-120">イテレーション #2-アプリケーションの外観を良くします。</span><span class="sxs-lookup"><span data-stu-id="9d326-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="9d326-121">このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。</span><span class="sxs-lookup"><span data-stu-id="9d326-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="9d326-122">イテレーション #3-フォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="9d326-123">3番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="9d326-124">必要なフォームフィールドを完了しないで、フォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="9d326-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="9d326-125">また、電子メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="9d326-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="9d326-126">イテレーション #4-アプリケーションの疎結合を実現します。</span><span class="sxs-lookup"><span data-stu-id="9d326-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="9d326-127">この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9d326-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="9d326-128">たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="9d326-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="9d326-129">イテレーション #5-単体テストを作成します。</span><span class="sxs-lookup"><span data-stu-id="9d326-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="9d326-130">5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。</span><span class="sxs-lookup"><span data-stu-id="9d326-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="9d326-131">データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。</span><span class="sxs-lookup"><span data-stu-id="9d326-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="9d326-132">イテレーション #6-テスト駆動型開発を使用します。</span><span class="sxs-lookup"><span data-stu-id="9d326-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="9d326-133">この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="9d326-134">このイテレーションでは、連絡先グループを追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="9d326-135">イテレーション #7-Ajax 機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="9d326-136">7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。</span><span class="sxs-lookup"><span data-stu-id="9d326-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="9d326-137">このイテレーション</span><span class="sxs-lookup"><span data-stu-id="9d326-137">This Iteration</span></span>

<span data-ttu-id="9d326-138">Contact Manager アプリケーションのこの2回目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="9d326-139">必須フォームフィールドの値を入力することなく、連絡先を送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="9d326-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="9d326-140">また、電話番号と電子メールアドレスも検証します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="9d326-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="9d326-141">[[新しいプロジェクト] ダイアログボックスの ![](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9d326-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="9d326-142">**図 01**:検証付きのフォーム ([クリックすると、フルサイズの画像が表示](iteration-3-add-form-validation-vb/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="9d326-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="9d326-143">このイテレーションでは、コントローラーアクションに検証ロジックを直接追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="9d326-144">一般に、ASP.NET MVC アプリケーションに検証を追加する方法として推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="9d326-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="9d326-145">より優れたアプローチは、アプリケーションの検証ロジックを別の[サービス層](http://martinfowler.com/eaaCatalog/serviceLayer.html)に配置することです。</span><span class="sxs-lookup"><span data-stu-id="9d326-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="9d326-146">次のイテレーションでは、アプリケーションの保守が容易になるように Contact Manager アプリケーションをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="9d326-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="9d326-147">このイテレーションでは、簡単にするために、すべての検証コードを手動で記述します。</span><span class="sxs-lookup"><span data-stu-id="9d326-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="9d326-148">検証コードを自分で記述する代わりに、検証フレームワークを利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="9d326-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="9d326-149">たとえば、Microsoft エンタープライズライブラリ検証アプリケーションブロック (VAB) を使用して、ASP.NET MVC アプリケーションの検証ロジックを実装できます。</span><span class="sxs-lookup"><span data-stu-id="9d326-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="9d326-150">検証アプリケーションブロックの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9d326-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="9d326-151">Create ビューへの検証の追加</span><span class="sxs-lookup"><span data-stu-id="9d326-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="9d326-152">まず、検証ロジックを Create ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="9d326-153">幸い、Visual Studio で作成ビューを生成したため、検証メッセージを表示するために必要なすべてのユーザーインターフェイスロジックが既に作成ビューに含まれています。</span><span class="sxs-lookup"><span data-stu-id="9d326-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="9d326-154">[作成] ビューは、リスト1に含まれています。</span><span class="sxs-lookup"><span data-stu-id="9d326-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="9d326-155">**Listing 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="9d326-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="9d326-156">フィールド検証-エラークラスは、Html. ValidationMessage () ヘルパーによって表示される出力のスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="9d326-157">入力検証-エラークラスは、Html の TextBox () ヘルパーによって表示されるテキストボックスのスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="9d326-158">"検証-概要-エラー" クラスは、Html. ValidationSummary () ヘルパーによって表示される順序付けられていないリストのスタイルを適用するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9d326-159">このセクションで説明するスタイルシートクラスを変更して、検証エラーメッセージの外観をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="9d326-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="9d326-160">作成アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="9d326-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="9d326-161">現時点では、メッセージを生成するロジックが記述されていないため、Create view は検証エラーメッセージを表示しません。</span><span class="sxs-lookup"><span data-stu-id="9d326-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="9d326-162">検証エラーメッセージを表示するには、エラーメッセージを ModelState に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9d326-163">UpdateModel () メソッドは、フォームフィールドの値をプロパティに割り当てるときにエラーが発生した場合に、エラーメッセージを ModelState に自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="9d326-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="9d326-164">たとえば、文字列 "apple" を DateTime 値を受け取る "誕生日" プロパティに割り当てようとすると、UpdateModel () メソッドによって ModelState にエラーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="9d326-165">リスト2の Create () メソッドを変更すると、新しい連絡先がデータベースに挿入される前に Contact クラスのプロパティを検証する新しいセクションが追加されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="9d326-166">**リスト 2-コントローラーの一覧表示 (検証を使用した作成)**</span><span class="sxs-lookup"><span data-stu-id="9d326-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="9d326-167">Validate セクションでは、4つの異なる検証規則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="9d326-168">FirstName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)</span><span class="sxs-lookup"><span data-stu-id="9d326-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="9d326-169">LastName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)</span><span class="sxs-lookup"><span data-stu-id="9d326-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="9d326-170">Phone プロパティの値が (長さが0より大きい) 場合、Phone プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="9d326-171">Email プロパティの値が (長さが0より大きい) 場合、Email プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="9d326-172">検証規則違反が発生すると、AddModelError () メソッドを使用してエラーメッセージが ModelState に追加されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="9d326-173">ModelState にメッセージを追加する場合は、プロパティの名前と検証エラーメッセージのテキストを指定します。</span><span class="sxs-lookup"><span data-stu-id="9d326-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="9d326-174">このエラーメッセージは、Html. ValidationSummary () および Html の Validationsummary () ヘルパーメソッドによってビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="9d326-175">検証規則が実行されると、ModelState の IsValid プロパティがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="9d326-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="9d326-176">IsValid プロパティは、ModelState に検証エラーメッセージが追加されたときに false を返します。</span><span class="sxs-lookup"><span data-stu-id="9d326-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="9d326-177">検証が失敗すると、エラーメッセージと共に作成フォームが再生成されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9d326-178">の正規表現リポジトリから電話番号と電子メールアドレスを検証する正規表現があります。 [ *http://regexlib.com* ](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="9d326-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="9d326-179">編集アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="9d326-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="9d326-180">Edit () アクションを実行すると、連絡先が更新されます。</span><span class="sxs-lookup"><span data-stu-id="9d326-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="9d326-181">Edit () アクションでは、Create () アクションとまったく同じ検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="9d326-182">同じ検証コードを複製するのではなく、Create () と Edit () の両方のアクションが同じ検証メソッドを呼び出すように Contact controller をリファクターする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="9d326-183">変更した Contact controller クラスは、リスト3に含まれています。</span><span class="sxs-lookup"><span data-stu-id="9d326-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="9d326-184">このクラスには、Create () アクションと Edit () アクションの両方で呼び出される新しい ValidateContact () メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="9d326-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="9d326-185">**Listing 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="9d326-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="9d326-186">まとめ</span><span class="sxs-lookup"><span data-stu-id="9d326-186">Summary</span></span>

<span data-ttu-id="9d326-187">このイテレーションでは、Contact Manager アプリケーションに基本的なフォーム検証を追加しました。</span><span class="sxs-lookup"><span data-stu-id="9d326-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="9d326-188">この検証ロジックにより、ユーザーは FirstName プロパティと LastName プロパティの値を指定せずに、新しい連絡先を送信したり、既存の連絡先を編集したりすることができなくなります。</span><span class="sxs-lookup"><span data-stu-id="9d326-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="9d326-189">さらに、ユーザーは有効な電話番号と電子メールアドレスを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d326-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="9d326-190">このイテレーションでは、最も簡単な方法で Contact Manager アプリケーションに検証ロジックを追加しました。</span><span class="sxs-lookup"><span data-stu-id="9d326-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="9d326-191">ただし、検証ロジックをコントローラーロジックに混在させると、長期的に問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="9d326-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="9d326-192">時間の経過と共に、アプリケーションの保守と変更が困難になります。</span><span class="sxs-lookup"><span data-stu-id="9d326-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="9d326-193">次のイテレーションでは、検証ロジックとデータベースアクセスロジックをコントローラーからリファクターします。</span><span class="sxs-lookup"><span data-stu-id="9d326-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="9d326-194">複数のソフトウェア設計原則を利用して、より疎結合で保守性の高いアプリケーションを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9d326-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d326-195">[前へ](iteration-2-make-the-application-look-nice-vb.md)
> [次へ](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9d326-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
