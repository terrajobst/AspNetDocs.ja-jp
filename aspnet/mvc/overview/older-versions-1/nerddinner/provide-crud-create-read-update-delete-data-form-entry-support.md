---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供します。Microsoft Docs
author: microsoft
description: 手順 5. では、ディナーでの編集、作成、および削除のサポートを有効にすることで、さらに Dinのコントローラークラスをさらに活用する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468916"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="6c93d-103">CRUD (作成、読み取り、更新、削除) データ フォーム エントリ サポートを提供する</span><span class="sxs-lookup"><span data-stu-id="6c93d-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="6c93d-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6c93d-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="6c93d-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="6c93d-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="6c93d-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションチュートリアル](introducing-the-nerddinner-tutorial.md)の手順5です。</span><span class="sxs-lookup"><span data-stu-id="6c93d-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="6c93d-107">手順 5. では、ディナーでの編集、作成、および削除のサポートを有効にすることで、さらに Dinのコントローラークラスをさらに活用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="6c93d-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="6c93d-109">ステップ 5: フォームの作成、更新、削除のシナリオ</span><span class="sxs-lookup"><span data-stu-id="6c93d-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="6c93d-110">ここでは、コントローラーとビューについて説明しました。また、これらの機能を使用して、サイトでディナーのリスト/詳細エクスペリエンスを実装する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="6c93d-111">次の手順として、Dinのコントローラークラスをさらに追加し、ディナーでの編集、作成、および削除のサポートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="6c93d-112">Din. Controller によって処理される Url</span><span class="sxs-lookup"><span data-stu-id="6c93d-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="6c93d-113">以前*は、2*つの url のサポートを実装した*Din/Dinners* scontroller にアクションメソッドを追加しました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="6c93d-114">**[URL]**</span><span class="sxs-lookup"><span data-stu-id="6c93d-114">**URL**</span></span> | <span data-ttu-id="6c93d-115">**助動詞**</span><span class="sxs-lookup"><span data-stu-id="6c93d-115">**VERB**</span></span> | <span data-ttu-id="6c93d-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="6c93d-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c93d-117">*ディナー*</span><span class="sxs-lookup"><span data-stu-id="6c93d-117">*/Dinners/*</span></span> | <span data-ttu-id="6c93d-118">GET</span><span class="sxs-lookup"><span data-stu-id="6c93d-118">GET</span></span> | <span data-ttu-id="6c93d-119">今後のディナーの HTML リストを表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="6c93d-120">*///[Id]*</span><span class="sxs-lookup"><span data-stu-id="6c93d-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="6c93d-121">GET</span><span class="sxs-lookup"><span data-stu-id="6c93d-121">GET</span></span> | <span data-ttu-id="6c93d-122">特定のディナーに関する詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="6c93d-123">ここでは、*次の 3*つの追加 url を実装するアクションメソッドを追加します。/ *Din/edit/[id]* 、 */Dinners/Delete/[id]* 。</span><span class="sxs-lookup"><span data-stu-id="6c93d-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="6c93d-124">これらの Url を使用して、既存のディナーの編集、新しいディナーの作成、ディナーの削除をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="6c93d-125">これらの新しい Url では、HTTP GET と HTTP POST の両方の動詞をサポートします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="6c93d-126">これらの Url への HTTP GET 要求によって、データの初期 HTML ビュー ("edit" の場合はディナーデータが入力されたフォーム)、"create" の場合は空のフォーム、"削除" の場合は削除の確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="6c93d-127">これらの Url への HTTP POST 要求により、Dinのリポジトリ (およびデータベースから) のディナーデータが保存/更新/削除されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="6c93d-128">**[URL]**</span><span class="sxs-lookup"><span data-stu-id="6c93d-128">**URL**</span></span> | <span data-ttu-id="6c93d-129">**助動詞**</span><span class="sxs-lookup"><span data-stu-id="6c93d-129">**VERB**</span></span> | <span data-ttu-id="6c93d-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="6c93d-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c93d-131">*//編集/[id]*</span><span class="sxs-lookup"><span data-stu-id="6c93d-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="6c93d-132">GET</span><span class="sxs-lookup"><span data-stu-id="6c93d-132">GET</span></span> | <span data-ttu-id="6c93d-133">ディナーデータを設定した編集可能な HTML フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="6c93d-134">POST</span><span class="sxs-lookup"><span data-stu-id="6c93d-134">POST</span></span> | <span data-ttu-id="6c93d-135">特定のディナーのフォームの変更をデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="6c93d-136">*/Din*</span><span class="sxs-lookup"><span data-stu-id="6c93d-136">*/Dinners/Create*</span></span> | <span data-ttu-id="6c93d-137">GET</span><span class="sxs-lookup"><span data-stu-id="6c93d-137">GET</span></span> | <span data-ttu-id="6c93d-138">ユーザーが新しいディナーを定義できる空の HTML フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="6c93d-139">POST</span><span class="sxs-lookup"><span data-stu-id="6c93d-139">POST</span></span> | <span data-ttu-id="6c93d-140">新しいディナーを作成し、データベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="6c93d-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="6c93d-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="6c93d-142">GET</span><span class="sxs-lookup"><span data-stu-id="6c93d-142">GET</span></span> | <span data-ttu-id="6c93d-143">削除の確認画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="6c93d-144">POST</span><span class="sxs-lookup"><span data-stu-id="6c93d-144">POST</span></span> | <span data-ttu-id="6c93d-145">指定されたディナーをデータベースから削除します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="6c93d-146">サポートの編集</span><span class="sxs-lookup"><span data-stu-id="6c93d-146">Edit Support</span></span>

<span data-ttu-id="6c93d-147">まず、"編集" シナリオを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="6c93d-148">HTTP GET Edit アクションメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="6c93d-149">まず、edit アクションメソッドの HTTP "GET" 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="6c93d-150">このメソッドは、/ *Dins/Edit/[id]* URL が要求されたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="6c93d-151">実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="6c93d-152">上記のコードでは、Dinのリポジトリを使用してディナーオブジェクトを取得しています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="6c93d-153">次に、ディナーオブジェクトを使用して、ビューテンプレートをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="6c93d-154">テンプレート名は明示的に*view ()* ヘルパーメソッドに渡されていないので、規則ベースの既定のパスを使用してビューテンプレートを解決します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="6c93d-155">ここで、このビューテンプレートを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-155">Let's now create this view template.</span></span> <span data-ttu-id="6c93d-156">これを行うには、Edit メソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="6c93d-157">[ビューの追加] ダイアログボックスで、そのモデルとしてディナーオブジェクトをビューテンプレートに渡し、"Edit" テンプレートの自動スキャフォールディングを選択することを示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="6c93d-158">[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Edit .aspx" ビューテンプレートファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="6c93d-159">また、コードエディター内で新しい "Edit .aspx" ビューテンプレートが開き、次のような初期の "Edit" スキャフォールディングの実装が設定されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="6c93d-160">既定の "edit" スキャフォールディングに対していくつかの変更を行い、次のコンテンツを含むように編集ビューテンプレートを更新します (公開したくないプロパティがいくつか削除されます)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="6c93d-161">アプリケーションを実行して *"/Dinners/Edit/1"* URL を要求すると、次のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="6c93d-162">ビューによって生成される HTML マークアップは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="6c93d-163">これは標準の HTML です。 &lt;フォーム&gt; 要素を使用して、"Save" &lt;input type = "submit"/&gt; ボタンがプッシュされたときに */Dinners/Edit/1* URL への HTTP POST を実行します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="6c93d-164">編集可能な各プロパティに対して、HTML &lt;input type = "text"/&gt; 要素が出力されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="6c93d-165">Html. BeginForm () および Html テキストボックス () Html ヘルパーメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="6c93d-166">"Edit .aspx" ビューテンプレートでは、html、ValidationSummary ()、Html. BeginForm ()、.Html ()、および Html の Validationsummary () の複数の "Html ヘルパー" メソッドが使用されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="6c93d-167">これらのヘルパーメソッドは、HTML マークアップを生成するだけでなく、組み込みのエラー処理と検証のサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="6c93d-168">Html. BeginForm () ヘルパーメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="6c93d-169">Html. BeginForm () ヘルパーメソッドは、マークアップの HTML &lt;フォーム&gt; 要素を出力します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="6c93d-170">編集 .aspx ビューテンプレートでは、このメソッドを使用するときに " C# using" ステートメントを適用していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="6c93d-171">左中かっこは、コンテンツ&gt; &lt;フォームの先頭を示します。右中かっこは、&lt;///&gt; 要素の末尾を示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="6c93d-172">または、このようなシナリオに対して "using" ステートメントの不自然な方法が見つかった場合は、次のように Html の BeginForm () と Html の EndForm () の組み合わせを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="6c93d-173">パラメーターを指定せずに Html. BeginForm () を呼び出すと、現在の要求の URL に HTTP POST を実行する form 要素が出力されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="6c93d-174">このため、Edit ビューでは *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 要素が生成されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="6c93d-175">別の URL に投稿する場合は、別の方法で、明示的なパラメーターを Html に渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="6c93d-176">Html. TextBox () ヘルパーメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="6c93d-177">編集 .aspx ビューでは、Html の TextBox () ヘルパーメソッドを使用して &lt;input type = "text"/&gt; 要素を出力します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="6c93d-178">上記の .Html () メソッドは、1つのパラメーターを受け取ります。これは、出力する &lt;入力型 = "text"/&gt; 要素の id/name 属性と、テキストボックスの値を設定するモデルプロパティの両方を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="6c93d-179">たとえば、編集ビューに渡されたディナーオブジェクトの "Title" プロパティ値が ".NET フューチャ" になっているため、Html テキストボックス ("Title") メソッドの呼び出し出力: *&lt;入力 id = "title" name = "title" type = "text" value = ". NET フューチャ"/&gt;* です。</span><span class="sxs-lookup"><span data-stu-id="6c93d-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="6c93d-180">または、最初の .Html () パラメーターを使用して要素の id と名前を指定し、次に2番目のパラメーターとして使用する値を明示的に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="6c93d-181">多くの場合、出力される値に対してカスタム書式設定を実行します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="6c93d-182">.NET に組み込まれている String. Format () 静的メソッドは、これらのシナリオに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="6c93d-183">編集 .aspx ビューテンプレートでは、このメソッドを使用して EventDate 値 (DateTime 型) を書式設定し、その時間に秒が表示されないようにしています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="6c93d-184">Html. TextBox () の3番目のパラメーターは、追加の HTML 属性を出力するために必要に応じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="6c93d-185">次のコードスニペットは、追加の size = "30" 属性と、class = "mycssclass" 属性を &lt;input type = "text"/&gt; 要素に表示する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="6c93d-186">ここでは、"@" character because "クラス" を使用してクラス属性の名前をエスケープする方法にC#ついて説明します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="6c93d-187">HTTP ポスト編集アクションメソッドの実装</span><span class="sxs-lookup"><span data-stu-id="6c93d-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="6c93d-188">これで、編集アクションメソッドの HTTP GET バージョンが実装されました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="6c93d-189">ユーザーが */Dinners/Edit/1* URL を要求すると、次のような HTML ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="6c93d-190">[Save] \ (保存 \) ボタンを押すと、 */Dinners/Edit/1* URL へのフォームポストが行われ、HTTP post 動詞を使用して HTML &lt;入力&gt; フォーム値が送信されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="6c93d-191">ここで、編集アクションメソッドの HTTP POST 動作を実装します。これにより、ディナーの保存が処理されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="6c93d-192">まず、オーバーロードされた "Edit" アクションメソッドを Dinのコントローラーに追加します。このメソッドには、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="6c93d-193">オーバーロードされたアクションメソッドに [AcceptVerbs] 属性が適用されると、ASP.NET MVC は、受信 HTTP 動詞に応じて、適切なアクションメソッドへのディスパッチ要求を自動的に処理します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="6c93d-194">HTTP POST 要求が */Dins/edit/[id]* の*url にアクセス*すると、上記の編集メソッドが使用されますが、その他のすべての http 動詞要求 (& n) は、実装した (`[AcceptVerbs]` 属性を持たない) 最初の編集メソッドに送られます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="6c93d-195">**サイドトピック: HTTP 動詞を使用して区別する理由**</span><span class="sxs-lookup"><span data-stu-id="6c93d-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="6c93d-196">1つの URL を使用し、HTTP 動詞でその動作を区別するのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="6c93d-197">編集変更の読み込みと保存を処理するために2つの異なる Url を用意する必要があるのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="6c93d-198">たとえば、フォームを保存するためのフォームの post を処理する場合、最初のフォームと/Din/[id] を表示するには、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="6c93d-199">2つの異なる Url を公開する場合の欠点は、1/3 に投稿した後、入力エラーのために HTML フォームを再表示する必要がある場合、エンドユーザーはブラウザーのアドレスバーに (フォームがポストされた URL であるため)、その URL が使用されるようになることです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="6c93d-200">エンドユーザーがこの再表示されたページをブラウザーのお気に入りの一覧にブックマークしたり、URL をコピーして友人に送信したりすると、後では機能しない URL が保存されます (その URL は post 値に依存しているため)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="6c93d-201">1 つの URL を公開することで (のような:/Dinners/Edit/[id]) および HTTP 動詞でその処理を区別するの編集ページをブックマークや他のユーザーに、URL を送信するエンドユーザーのも安全です。</span><span class="sxs-lookup"><span data-stu-id="6c93d-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="6c93d-202">フォームポスト値の取得</span><span class="sxs-lookup"><span data-stu-id="6c93d-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="6c93d-203">HTTP POST の "Edit" メソッドでは、ポストされたフォームパラメーターにさまざまな方法でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="6c93d-204">単純な方法の1つとして、Controller 基本クラスの Request プロパティを使用してフォームコレクションにアクセスし、ポストされた値を直接取得するだけです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="6c93d-205">ただし、上記の方法は、特にエラー処理ロジックを追加した後は少し詳細になります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="6c93d-206">このシナリオでは、コントローラーの基本クラスで組み込みの*UpdateModel ()* ヘルパーメソッドを利用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="6c93d-207">オブジェクトのプロパティの更新は、受信フォームパラメーターを使用して渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="6c93d-208">このメソッドは、リフレクションを使用してオブジェクトのプロパティ名を決定し、クライアントによって送信された入力値に基づいて、値を自動的に変換して値を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="6c93d-209">UpdateModel () メソッドを使用して、次のコードを使用して HTTP POST 編集アクションを簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="6c93d-210">これで、 */Dinners/Edit/1* URL にアクセスし、ディナーのタイトルを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="6c93d-211">[保存] ボタンをクリックすると、編集アクションへのフォームの投稿が実行され、更新された値はデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="6c93d-212">次に、ディナーの詳細 URL にリダイレクトされます (新たに保存された値が表示されます)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="6c93d-213">編集エラーの処理</span><span class="sxs-lookup"><span data-stu-id="6c93d-213">Handling Edit Errors</span></span>

<span data-ttu-id="6c93d-214">現在の HTTP ポストの実装は、エラーがある場合を除き、正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="6c93d-215">ユーザーがフォームを編集するときに、フォームが再表示され、問題を修正するための情報を示すエラーメッセージが表示されていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="6c93d-216">これには、エンドユーザーが間違った入力 (たとえば、形式が正しくない日付文字列) を投稿する場合や、入力形式が有効であってもビジネスルール違反がある場合などがあります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="6c93d-217">エラーが発生すると、フォームはユーザーが最初に入力した入力データを保持する必要があるため、手動で変更を補充する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="6c93d-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="6c93d-218">このプロセスは、フォームが正常に完了するまで、必要な回数だけ繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="6c93d-219">ASP.NET MVC には、エラー処理とフォーム再表示を容易にする便利な組み込み機能がいくつか用意されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="6c93d-220">これらの機能を実際に確認するには、編集アクションメソッドを次のコードで更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="6c93d-221">上記のコードは、前の実装に似ています。ただし、ここでは、作業の前後に try/catch エラー処理ブロックをラップしている点が異なります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="6c93d-222">UpdateModel () の呼び出し中に例外が発生した場合、または Dinを保存しようとしたときに (保存しようとしているディナーオブジェクトがモデル内のルール違反のために無効である場合に例外が発生する)、キャッチエラー処理ブロックは、おい.</span><span class="sxs-lookup"><span data-stu-id="6c93d-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="6c93d-223">その中で、ディナーオブジェクトに存在する規則違反をループし、ModelState オブジェクトに追加します (これについては後で説明します)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="6c93d-224">次に、ビューを再表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-224">We then redisplay the view.</span></span>

<span data-ttu-id="6c93d-225">この作業を確認するには、アプリケーションを再実行し、ディナーを編集して、空のタイトル、EventDate が "BOGUS" になるように変更して、国の値が USA である英国の電話番号を使用します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="6c93d-226">[保存] ボタンを押すと、HTTP POST Edit メソッドは、(エラーがあるために) ディナーを保存できなくなり、フォームが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="6c93d-227">アプリケーションのエラーエクスペリエンスが向上しています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-227">Our application has a decent error experience.</span></span> <span data-ttu-id="6c93d-228">無効な入力を持つテキスト要素が赤色で強調表示され、エンドユーザーに対して検証エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="6c93d-229">このフォームには、ユーザーが最初に入力した入力データも保持されるため、何も入力する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="6c93d-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="6c93d-230">どうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="6c93d-231">[タイトル]、[EventDate]、および [ContactPhone] の各テキストボックス自体が赤で強調表示され、最初に入力したユーザー値が出力されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="6c93d-232">エラーメッセージが上部の一覧に表示されるのはどのようなものですか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="6c93d-233">これはマジックではありませんでした。これは、入力の検証とエラー処理のシナリオを簡単に行う組み込みの ASP.NET MVC 機能の一部を使用したためです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="6c93d-234">ModelState と検証 HTML ヘルパーメソッドについて</span><span class="sxs-lookup"><span data-stu-id="6c93d-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="6c93d-235">コントローラークラスには、ビューに渡されるモデルオブジェクトのエラーが存在することを示すための "ModelState" プロパティコレクションがあります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="6c93d-236">ModelState コレクション内のエラーエントリは、問題のあるモデルプロパティの名前 ("Title"、"EventDate"、"ContactPhone" など) を識別し、わかりやすいエラーメッセージを指定できるようにします (例: "タイトルが必要")。</span><span class="sxs-lookup"><span data-stu-id="6c93d-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="6c93d-237">*UpdateModel ()* ヘルパーメソッドは、モデルオブジェクトのプロパティにフォーム値を割り当てようとしているときに、エラーが発生したときに modelstate コレクションを自動的に設定します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="6c93d-238">たとえば、ディナーオブジェクトの EventDate プロパティは DateTime 型です。</span><span class="sxs-lookup"><span data-stu-id="6c93d-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="6c93d-239">上記のシナリオで、UpdateModel () メソッドが文字列値 "BOGUS" をこのメソッドに割り当てることができなかった場合、UpdateModel () メソッドは、そのプロパティで割り当てエラーが発生したことを示すエントリを ModelState コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="6c93d-240">開発者は、"catch" エラー処理ブロック内で次に示すように、エラーエントリを ModelState コレクションに明示的に追加するコードを記述することもできます。これは、ディナーオブジェクト:</span><span class="sxs-lookup"><span data-stu-id="6c93d-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="6c93d-241">Html ヘルパーと ModelState の統合</span><span class="sxs-lookup"><span data-stu-id="6c93d-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="6c93d-242">Html ヘルパーメソッド (Html. TextBox () など)-出力をレンダリングするときに ModelState コレクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="6c93d-243">項目のエラーが存在する場合は、ユーザーが入力した値と CSS エラークラスを表示します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="6c93d-244">たとえば、"Edit" ビューでは、Html. TextBox () ヘルパーメソッドを使用して、ディナーオブジェクトの EventDate をレンダリングしています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="6c93d-245">エラーシナリオでビューがレンダリングされると、.Html () メソッドは ModelState コレクションを確認して、ディナーオブジェクトの "EventDate" プロパティに関連付けられたエラーがあるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="6c93d-246">エラーが発生したと判断した場合、送信されたユーザー入力 ("偽") を値としてレンダリングし、css error クラスを &lt;input type = "textbox"/&gt; 生成したマークアップに追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="6c93d-247">必要に応じて、css error クラスの外観をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="6c93d-248">既定の CSS エラークラス– "入力-検証-エラー" –は、次のように、 *\ content\ sitestylesheet*スタイルシートで定義されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="6c93d-249">この CSS 規則は、次のように、無効な入力要素が強調表示される原因となっています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="6c93d-250">Html. ValidationMessage () ヘルパーメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="6c93d-251">Html の ValidationMessage () ヘルパーメソッドを使用すると、特定のモデルプロパティに関連付けられている ModelState エラーメッセージを出力できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="6c93d-252">上記のコードでは、 *&lt;span class = "/span"&gt; になります。値 ' BOGUS ' は無効&lt;&gt;*</span><span class="sxs-lookup"><span data-stu-id="6c93d-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="6c93d-253">Html の ValidationMessage () ヘルパーメソッドでは、表示されているエラーテキストメッセージを開発者がオーバーライドできる2番目のパラメーターもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="6c93d-254">上記のコードでは、EventDate プロパティにエラーが存在する場合に、既定のエラーテキストではなく、 *span class = "/span"&gt;\*&lt;&gt;* を出力しています&lt;。</span><span class="sxs-lookup"><span data-stu-id="6c93d-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="6c93d-255">Html. ValidationSummary () ヘルパーメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="6c93d-256">Html. ValidationSummary () ヘルパーメソッドを使用すると、集計エラーメッセージを表示できます。これには、&lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState コレクション内のすべての詳細エラーメッセージの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="6c93d-257">Html の ValidationSummary () ヘルパーメソッドは、省略可能な文字列パラメーターを受け取ります。これは、詳細なエラーの一覧の上に表示する概要エラーメッセージを定義します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="6c93d-258">必要に応じて CSS を使用して、エラー一覧の外観をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="6c93d-259">AddRuleViolations ヘルパーメソッドの使用</span><span class="sxs-lookup"><span data-stu-id="6c93d-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="6c93d-260">最初の HTTP POST 編集の実装では、catch ブロック内で foreach ステートメントを使用して、ディナーオブジェクトの規則違反をループし、コントローラーの ModelState コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="6c93d-261">このコードは、"コントローラーヘルパー" クラスを "コントローラー" プロジェクトに追加し、ASP.NET MVC ModelStateDictionary クラスにヘルパーメソッドを追加する "AddRuleViolations" 拡張メソッドを実装することによって、少しすっきりしたものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="6c93d-262">この拡張メソッドは、ModelStateDictionary に RuleViolation エラーの一覧を設定するために必要なロジックをカプセル化できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="6c93d-263">次に、HTTP POST 編集アクションメソッドを更新して、この拡張メソッドを使用して、ディナールール違反を ModelState コレクションに設定できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="6c93d-264">アクションメソッドの実装の完了</span><span class="sxs-lookup"><span data-stu-id="6c93d-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="6c93d-265">以下のコードは、編集シナリオに必要なすべてのコントローラーロジックを実装しています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="6c93d-266">編集実装に関するすばらしい点は、コントローラークラスもビューテンプレートも、ディナーモデルによって適用されている特定の検証またはビジネスルールに関する情報を知る必要がないということです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="6c93d-267">将来、モデルに追加のルールを追加することができます。また、サポートされるように、コントローラーやビューにコード変更を加える必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6c93d-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="6c93d-268">これにより、コードの変更を最小限に抑えて、将来的にアプリケーションの要件を簡単に拡張できる柔軟性が提供されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="6c93d-269">サポートを作成する</span><span class="sxs-lookup"><span data-stu-id="6c93d-269">Create Support</span></span>

<span data-ttu-id="6c93d-270">Dinのコントローラークラスの "編集" 動作の実装が完了しました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="6c93d-271">ここで、ユーザーが新しいディナーを追加できるようにするための "Create" サポートを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="6c93d-272">HTTP-GET Create Action メソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="6c93d-273">まず、create action メソッドの HTTP "GET" 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="6c93d-274">このメソッドは、他のユーザーが */Dins/create* URL にアクセスしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="6c93d-275">実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="6c93d-276">上記のコードでは、新しいディナーオブジェクトを作成し、その EventDate プロパティを1週間後に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="6c93d-277">次に、新しいディナーオブジェクトに基づくビューをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="6c93d-278">明示的に名前を*view ()* ヘルパーメソッドに渡していないので、規則ベースの既定のパスを使用してビューテンプレートを解決します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="6c93d-279">ここで、このビューテンプレートを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-279">Let's now create this view template.</span></span> <span data-ttu-id="6c93d-280">これを行うには、Create action メソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="6c93d-281">[ビューの追加] ダイアログボックスで、ディナーオブジェクトをビューテンプレートに渡し、"Create" テンプレートの自動スキャフォールディングを選択することを指定します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="6c93d-282">[追加] ボタンをクリックすると、Visual Studio によって新しいスキャフォールディングベースの "\Views\Dinners" ビューが "" ディレクトリに保存され、IDE 内で開かれます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="6c93d-283">既定の "create" スキャフォールディングファイルに対して生成された変更をいくつか行い、次のように変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="6c93d-284">ここで、アプリケーションを実行し、ブラウザー内で *"/dinの S/create"* URL にアクセスすると、次のような UI が作成アクションの実装から表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="6c93d-285">HTTP ポスト作成アクションメソッドの実装</span><span class="sxs-lookup"><span data-stu-id="6c93d-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="6c93d-286">Create action メソッドの HTTP GET バージョンが実装されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="6c93d-287">ユーザーが [保存] ボタンをクリックする*と、その URL へ*のフォームポストが実行され、HTTP post 動詞を使用して HTML &lt;入力&gt; フォーム値が送信されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="6c93d-288">ここで、create action メソッドの HTTP POST 動作を実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="6c93d-289">まず、オーバーロードされた "Create" アクションメソッドを、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ Din: コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="6c93d-290">HTTP ポストが有効な "Create" メソッドでは、ポストされたフォームパラメーターにさまざまな方法でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="6c93d-291">1つの方法として、新しいディナーオブジェクトを作成し、 *UpdateModel ()* ヘルパーメソッド (Edit アクションの場合と同様) を使用して、ポストされたフォーム値を設定する方法があります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="6c93d-292">次に、これを Dinレポジトリに追加し、データベースに保存します。次のコードを使用して、新しく作成したディナーを表示するように、ユーザーを [詳細] アクションにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="6c93d-293">または、Create () アクションメソッドが、メソッドパラメーターとしてディナーオブジェクトを受け取る方法を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="6c93d-294">ASP.NET MVC は、自動的に新しいディナーオブジェクトをインスタンス化し、フォーム入力を使用してプロパティを設定し、それをアクションメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="6c93d-295">上記のアクションメソッドは、"ModelState. IsValid" プロパティをチェックして、ディナーオブジェクトにフォームポスト値が正常に設定されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="6c93d-296">これは、入力変換の問題 (たとえば、EventDate プロパティに "偽" の文字列) がある場合に false を返します。問題がある場合は、アクションメソッドによってフォームが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="6c93d-297">入力値が有効な場合、アクションメソッドは、新しいディナーを Dinare リポジトリに追加して保存しようとします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="6c93d-298">この作業は try/catch ブロック内にラップされ、ビジネスルール違反がある場合はフォームを再実行します (これにより、例外が発生する可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="6c93d-299">このエラー処理の動作を確認するには、 */Dins/create* URL を要求し、新しいディナーに関する詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="6c93d-300">入力または値が正しくないと、次のように強調表示されたエラーと共に作成フォームが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="6c93d-301">Create フォームには、編集フォームとまったく同じ検証とビジネスルールが適用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6c93d-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="6c93d-302">これは、検証とビジネスルールがモデルで定義されており、アプリケーションの UI またはコントローラー内に埋め込まれていないためです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="6c93d-303">つまり、後で検証やビジネスルールを1か所で変更/進化させ、アプリケーション全体に適用することができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="6c93d-304">Edit または Create アクションメソッド内のコードを変更しなくても、新しいルールや既存のルールに対する変更を自動的に受け入れることができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="6c93d-305">入力値を修正して [保存] ボタンをもう一度クリックすると、Dinのリポジトリへの追加が成功し、新しいディナーがデータベースに追加されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="6c93d-306">その後、次の URL にリダイレクトされます。ここに*は、新しく*作成したディナーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="6c93d-307">サポートの削除</span><span class="sxs-lookup"><span data-stu-id="6c93d-307">Delete Support</span></span>

<span data-ttu-id="6c93d-308">次に、"削除" のサポートを Dincontroller に追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="6c93d-309">HTTP-GET Delete アクションメソッド</span><span class="sxs-lookup"><span data-stu-id="6c93d-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="6c93d-310">まず、delete アクションメソッドの HTTP GET 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="6c93d-311">このメソッドは、他のユーザーが */Dinners/Delete/[id]* URL にアクセスしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="6c93d-312">実装は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="6c93d-313">アクションメソッドは、削除するディナーを取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="6c93d-314">ディナーが存在する場合は、ディナーオブジェクトに基づいてビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="6c93d-315">オブジェクトが存在しない (または既に削除されている) 場合は、"Details" アクションメソッド用に以前に作成した "NotFound" ビューテンプレートを表示するビューを返します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="6c93d-316">"削除" ビューテンプレートを作成するには、Delete アクションメソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="6c93d-317">[ビューの追加] ダイアログボックスで、そのモデルとしてディナーオブジェクトをビューテンプレートに渡し、空のテンプレートを作成することを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="6c93d-318">[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Delete .aspx" ビューテンプレートファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="6c93d-319">次のように、テンプレートに HTML とコードを追加して、削除の確認画面を実装します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="6c93d-320">上のコードは、削除するディナーのタイトルを表示し、エンドユーザーがその中の [Delete] ボタンをクリックした場合に/Dinners/Delete/[id] URL への投稿を行う &lt;フォーム&gt; 要素を出力します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="6c93d-321">アプリケーションを実行し、有効なディナーオブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のような UI が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="6c93d-322">**サイドトピック: 投稿を実行する理由**</span><span class="sxs-lookup"><span data-stu-id="6c93d-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="6c93d-323">[削除の確認] 画面で&gt; &lt;フォームを作成する必要があるのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="6c93d-324">標準ハイパーリンクを使用して、実際の削除操作を実行するアクションメソッドにリンクしているのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="6c93d-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="6c93d-325">これは、web クローラーと検索エンジンに対して Url を検出し、誤ってリンクをたどるとデータが削除されることを防ぐために注意する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="6c93d-326">HTTP-GET ベースの Url は、アクセス/クロールのために "安全" と見なされ、HTTP ポストに従わないことが想定されています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="6c93d-327">適切なルールとして、常に破棄またはデータの変更操作を HTTP ポスト要求の背後に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="6c93d-328">HTTP ポスト削除アクションメソッドの実装</span><span class="sxs-lookup"><span data-stu-id="6c93d-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="6c93d-329">これで、削除の確認画面を表示する、HTTP GET バージョンの Delete アクションメソッドが実装されました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="6c93d-330">エンドユーザーが [削除] ボタンをクリックすると、 *[id]* URL へのフォームの投稿が実行されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="6c93d-331">次のコードを使用して、delete アクションメソッドの HTTP "POST" 動作を実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="6c93d-332">削除アクションメソッドの HTTP POST バージョンは、削除するディナーオブジェクトを取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="6c93d-333">(既に削除されているため) 見つからない場合は、"NotFound" テンプレートをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="6c93d-334">夕食が見つかった場合は、Dinレポジトリから削除されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="6c93d-335">その後、"Deleted" テンプレートがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="6c93d-336">"Deleted" テンプレートを実装するには、アクションメソッドを右クリックし、[ビューの追加] コンテキストメニューを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="6c93d-337">ビューに "Deleted" という名前を付けると、空のテンプレートになります (厳密に型指定されたモデルオブジェクトを使用することはできません)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="6c93d-338">次に、HTML コンテンツをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="6c93d-339">ここで、アプリケーションを実行し、有効なディナーオブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のようなディナー削除確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="6c93d-340">[Delete] \ (削除 \) ボタンをクリックすると、 */Dinners/Delete/[id]* URL への HTTP POST が実行されます。これにより、データベースからディナーが削除され、"Deleted" ビューテンプレートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="6c93d-341">モデルバインディングのセキュリティ</span><span class="sxs-lookup"><span data-stu-id="6c93d-341">Model Binding Security</span></span>

<span data-ttu-id="6c93d-342">ASP.NET MVC の組み込みのモデルバインド機能を使用する2つの異なる方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="6c93d-343">最初の方法では、UpdateModel () メソッドを使用して既存のモデルオブジェクトのプロパティを更新し、2つ目のメソッドでモデルオブジェクトをアクションメソッドパラメーターとして渡すための ASP.NET MVC のサポートを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="6c93d-344">これらの方法はどちらも非常に強力で、非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="6c93d-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="6c93d-345">また、it 部門の責任もあります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="6c93d-346">ユーザー入力を受け入れるときは常にセキュリティについて paranoid することが重要です。これは、オブジェクトを入力にバインドする場合にも当てはまります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="6c93d-347">HTML および JavaScript インジェクション攻撃を防ぐために、ユーザーが入力した値は常に HTML エンコードする必要があります。また、SQL インジェクション攻撃にも注意してください (注: アプリケーションには LINQ to SQL を使用します。これにより、パラメーターが自動的にエンコードされ、これらを防ぐことができます。攻撃の種類。</span><span class="sxs-lookup"><span data-stu-id="6c93d-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="6c93d-348">クライアント側の検証だけでなく、偽の値を送信しようとしているハッカーからの防御を常にサーバー側で検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="6c93d-349">ASP.NET MVC のバインド機能を使用するときに考慮する必要がある追加のセキュリティ項目の1つは、バインドするオブジェクトのスコープであることです。</span><span class="sxs-lookup"><span data-stu-id="6c93d-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="6c93d-350">具体的には、バインドを許可するプロパティのセキュリティへの影響を確実に理解し、エンドユーザーが更新できるようにする必要があるプロパティのみを許可するようにします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="6c93d-351">既定では、UpdateModel () メソッドは、入力された形式のパラメーター値に一致するモデルオブジェクトのすべてのプロパティを更新しようとします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="6c93d-352">同様に、アクションメソッドのパラメーターとして渡されるオブジェクトでも、既定では、すべてのプロパティをフォームパラメーターを使用して設定できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="6c93d-353">使用単位でバインドをロックダウンする</span><span class="sxs-lookup"><span data-stu-id="6c93d-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="6c93d-354">更新可能なプロパティの明示的な "インクルードリスト" を指定することで、使用単位でバインドポリシーをロックダウンできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="6c93d-355">これを行うには、次のように、余分な文字列配列パラメーターを UpdateModel () メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="6c93d-356">アクションメソッドのパラメーターとして渡されるオブジェクトは、次のように、許可されたプロパティの "include list" を有効にする [Bind] 属性もサポートします。</span><span class="sxs-lookup"><span data-stu-id="6c93d-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="6c93d-357">型に基づいてバインディングをロックダウンする</span><span class="sxs-lookup"><span data-stu-id="6c93d-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="6c93d-358">また、型ごとにバインド規則をロックダウンすることもできます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="6c93d-359">これにより、バインド規則を1回指定することができ、すべてのコントローラーとアクションメソッドで、すべてのシナリオ (UpdateModel とアクションメソッドの両方のシナリオを含む) に適用することができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="6c93d-360">型に対して [Bind] 属性を追加するか、アプリケーションの global.asax ファイル内に登録することによって、型ごとのバインド規則をカスタマイズできます (型を所有していない場合に便利です)。</span><span class="sxs-lookup"><span data-stu-id="6c93d-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="6c93d-361">その後、バインド属性の Include プロパティと Exclude プロパティを使用して、特定のクラスまたはインターフェイスに対してバインドできるプロパティを制御できます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="6c93d-362">ここでは、次のように、このアプリケーションのディナークラスにこの手法を使用し、バインド可能なプロパティの一覧を次のように制限する [Bind] 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="6c93d-363">バインドを使用した RSVPs コレクションの操作は許可されていません。また、バインドによって Dinare Id または HostedBy プロパティを設定することもできません。</span><span class="sxs-lookup"><span data-stu-id="6c93d-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="6c93d-364">セキュリティ上の理由から、代わりに、アクションメソッド内の明示的なコードを使用して、これらの特定のプロパティのみを操作します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="6c93d-365">CRUD のラップアップ</span><span class="sxs-lookup"><span data-stu-id="6c93d-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="6c93d-366">ASP.NET MVC には、フォームポストのシナリオを実装するのに役立つさまざまな機能が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="6c93d-367">私たちは、このようなさまざまな機能を使用して、Dinのリポジトリに対して CRUD UI のサポートを提供していました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="6c93d-368">ここでは、モデルに重点を置いたアプローチを使用して、アプリケーションを実装しています。</span><span class="sxs-lookup"><span data-stu-id="6c93d-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="6c93d-369">これは、すべての検証とビジネスルールのロジックが、コントローラーやビュー内ではなく、モデルレイヤー内で定義されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="6c93d-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="6c93d-370">コントローラークラスもビューテンプレートにも、ディナーモデルクラスによって適用される特定のビジネスルールについての情報はありません。</span><span class="sxs-lookup"><span data-stu-id="6c93d-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="6c93d-371">これにより、アプリケーションアーキテクチャのクリーンアップが維持され、テストが容易になります。</span><span class="sxs-lookup"><span data-stu-id="6c93d-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="6c93d-372">将来、モデルレイヤーにビジネスルールを追加することができます。また、サポートされるように、コントローラーやビューに*コード変更を加える必要もありません*。</span><span class="sxs-lookup"><span data-stu-id="6c93d-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="6c93d-373">これにより、将来のアプリケーションの進化と変更に多大な機敏性をもたらすことができます。</span><span class="sxs-lookup"><span data-stu-id="6c93d-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="6c93d-374">Dinは、ディナーリスト/詳細のほか、作成、編集、削除のサポートを有効にするようになりました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="6c93d-375">クラスの完全なコードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c93d-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="6c93d-376">次の手順</span><span class="sxs-lookup"><span data-stu-id="6c93d-376">Next Step</span></span>

<span data-ttu-id="6c93d-377">これで、お客様の Dinのコントローラークラス内で、基本的な CRUD (作成、読み取り、更新、削除) のサポートを実装できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="6c93d-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="6c93d-378">次に、ViewData クラスとビューモデルクラスを使用して、フォームでさらに充実した UI を有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="6c93d-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6c93d-379">[前へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [次へ](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="6c93d-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
