---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData を使用して、ビューモデルクラスを実装する |Microsoft Docs
author: microsoft
description: 手順6では、豊富なフォーム編集シナリオのサポートを有効にする方法と、コントローラーからビューにデータを渡すために使用できる2つの方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435532"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="f86a9-103">ViewData を使用し、ViewModel クラスを実装する</span><span class="sxs-lookup"><span data-stu-id="f86a9-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="f86a9-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f86a9-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="f86a9-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="f86a9-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="f86a9-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順6です。</span><span class="sxs-lookup"><span data-stu-id="f86a9-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f86a9-107">手順6は、豊富なフォーム編集シナリオのサポートを有効にする方法と、コントローラーからビューにデータを渡すために使用できる2つの方法である ViewData とビューについても説明します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="f86a9-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f86a9-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="f86a9-109">ステップ 6: ViewData とビューモデルの操作</span><span class="sxs-lookup"><span data-stu-id="f86a9-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="f86a9-110">ここでは、いくつかのフォームポストシナリオについて説明し、作成、更新、削除 (CRUD) のサポートを実装する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="f86a9-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="f86a9-111">ここでは、さらに詳しく説明します。これにより、より豊富なフォーム編集シナリオがサポートされるようになります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="f86a9-112">ここでは、コントローラーからビューにデータを渡すために使用できる2つの方法 (ViewData とビューモデル) について説明します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="f86a9-113">コントローラーからビューテンプレートにデータを渡す</span><span class="sxs-lookup"><span data-stu-id="f86a9-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="f86a9-114">MVC パターンの定義特性の1つは、アプリケーションのさまざまなコンポーネントの間で適用される、厳密な "懸念事項の分離" です。</span><span class="sxs-lookup"><span data-stu-id="f86a9-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="f86a9-115">モデル、コントローラー、およびビューには、ロールと責任が明確に定義されており、それぞれが明確に定義された方法で相互に通信します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="f86a9-116">これにより、テストの容易性とコードの再利用が促進されます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="f86a9-117">コントローラークラスは、クライアントに HTML 応答を返すことを決定するときに、応答を表示するために必要なすべてのデータをビューテンプレートに明示的に渡す役割を担います。</span><span class="sxs-lookup"><span data-stu-id="f86a9-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="f86a9-118">ビューテンプレートは、データの取得またはアプリケーションロジックを実行しないようにする必要があります。代わりに、コントローラーによって渡されたモデル/データから駆動されるレンダリングコードだけを表示するように制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="f86a9-119">ここで、DinnersController クラスによってビューテンプレートに渡されるモデルデータは単純で、簡単です。 Index () の場合はディナーオブジェクトのリスト、Details ()、Edit ()、Create ()、Delete () の場合は1つのディナーオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="f86a9-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="f86a9-120">アプリケーションに UI 機能を追加すると、多くの場合、ビューテンプレート内に HTML 応答を表示するために、このデータだけではなく、さらに多くのデータを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="f86a9-121">たとえば、Edit および Create ビュー内の "Country" フィールドを、HTML テキストボックスから dropdownlist に変更することができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="f86a9-122">ビューテンプレートで国名のドロップダウンリストをハードコーディングするのではなく、動的に設定する、サポートされている国の一覧から生成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f86a9-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="f86a9-123">ディナーオブジェクト*と*、サポートされている国の一覧をコントローラーからビューテンプレートに渡す方法が必要になります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="f86a9-124">これを実現する2つの方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f86a9-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="f86a9-125">ViewData Dictionary の使用</span><span class="sxs-lookup"><span data-stu-id="f86a9-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="f86a9-126">コントローラーの基本クラスは、コントローラーからビューに追加のデータ項目を渡すために使用できる "ViewData" ディクショナリプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="f86a9-127">たとえば、編集ビュー内の "Country" テキストボックスを HTML テキストボックスから dropdownlist に変更するというシナリオをサポートするために、Edit () アクションメソッドを更新して、m として使用できる SelectList オブジェクトを (ディナーオブジェクトに加えて) 渡すことができます。国の odel の dropdownlist。</span><span class="sxs-lookup"><span data-stu-id="f86a9-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="f86a9-128">上記の SelectList のコンストラクターは、現在選択されている値だけでなく、ドロップダウンリストに入力する郡の一覧を受け入れています。</span><span class="sxs-lookup"><span data-stu-id="f86a9-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="f86a9-129">次に、前に使用した .Html () ヘルパーメソッドではなく、.Html () ヘルパーメソッドを使用するように、編集 .aspx ビューテンプレートを更新できます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="f86a9-130">上記の .Html () ヘルパーメソッドは、2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="f86a9-131">1つ目は、出力する HTML フォーム要素の名前です。</span><span class="sxs-lookup"><span data-stu-id="f86a9-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="f86a9-132">2つ目は、ViewData 辞書を介して渡された "SelectList" モデルです。</span><span class="sxs-lookup"><span data-stu-id="f86a9-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="f86a9-133">C# "As" キーワードを使用して、ディクショナリ内の型を selectlist としてキャストしています。</span><span class="sxs-lookup"><span data-stu-id="f86a9-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="f86a9-134">ここで、アプリケーションを実行し、ブラウザー内で */Dinners/Edit/1* URL にアクセスすると、エディット UI が更新され、テキストボックスではなく country of country が表示されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="f86a9-135">また、編集ビューテンプレートは、HTTP ポスト編集メソッド (エラーが発生した場合) からもレンダリングされるので、エラーシナリオでビューテンプレートがレンダリングされたときに、このメソッドを更新して、SelectList を ViewData に追加するようにします。</span><span class="sxs-lookup"><span data-stu-id="f86a9-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="f86a9-136">これで、Dinがコントローラーを編集するシナリオで DropDownList がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f86a9-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="f86a9-137">ビューモデルパターンの使用</span><span class="sxs-lookup"><span data-stu-id="f86a9-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="f86a9-138">ViewData dictionary のアプローチには、非常に高速で実装が簡単であるという利点があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="f86a9-139">ただし、文字列ベースの辞書を使用しない開発者もいます。これは、入力ミスによってコンパイル時に検出されないエラーが発生する可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="f86a9-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="f86a9-140">また、型指定されていない ViewData 辞書では、ビューテンプレートでのようC#に、厳密に型指定された言語を使用する場合に、"as" 演算子またはキャストを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="f86a9-141">使用できる別の方法として、しばしば "モデル化" パターンと呼ばれるものがあります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="f86a9-142">このパターンを使用すると、特定のビューシナリオ用に最適化された、厳密に型指定されたクラスを作成し、ビューテンプレートに必要な動的な値/コンテンツのプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="f86a9-143">次に、コントローラークラスを設定して、ビューに最適化されたこれらのクラスをビューテンプレートに渡して使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f86a9-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="f86a9-144">これにより、ビューテンプレート内でタイプセーフ、コンパイル時チェック、およびエディター intellisense が有効になります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="f86a9-145">たとえば、ディナーフォーム編集シナリオを有効にするには、次のように、2つの厳密に型指定されたプロパティを公開する "DinnerFormViewModel" クラスを作成します。ディナーオブジェクトと、country に設定するために必要な SelectList モデルです。</span><span class="sxs-lookup"><span data-stu-id="f86a9-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="f86a9-146">次に、Edit () アクションメソッドを更新して、リポジトリから取得したディナーオブジェクトを使用して Dinを作成し、ビューテンプレートに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="f86a9-147">次に、ビューテンプレートを更新して、次のように .aspx ページの上部にある "inherits" 属性を変更することによって、"ディナー" オブジェクトではなく "Din" を必要とするようにします。</span><span class="sxs-lookup"><span data-stu-id="f86a9-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="f86a9-148">この操作を実行すると、ビューテンプレート内の "Model" プロパティの intellisense が更新され、それに渡される Dinare Formmodel 型のオブジェクトモデルが反映されます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="f86a9-149">その後で、ビューコードを更新して、作業を開始することができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="f86a9-150">ここでは、作成している入力要素の名前を変更していないことに注意してください (form 要素には "Title"、"Country" という名前が付けられます)。ただし、HTML ヘルパーメソッドを更新して、Dinare Formformクラスを使用して値を取得します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="f86a9-151">また、レンダリングエラーが発生したときに Dinを使用するように、Edit post メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="f86a9-152">また、Create () アクションメソッドを更新して、まったく同じ*Dinのフォームビューモデル*クラスを再利用し、その中でも Country の DropDownList を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="f86a9-153">HTTP GET 実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="f86a9-154">次に、HTTP ポストの Create メソッドの実装を示します。</span><span class="sxs-lookup"><span data-stu-id="f86a9-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="f86a9-155">これで、編集画面と作成画面の両方で、国を選択するためのドロップダウンリストがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f86a9-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="f86a9-156">カスタムの型のビューモデルクラス</span><span class="sxs-lookup"><span data-stu-id="f86a9-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="f86a9-157">上記のシナリオでは、Dinの Formformmodel クラスが、サポートされている SelectList モデルプロパティと共に、ディナーモデルオブジェクトをプロパティとして直接公開しています。</span><span class="sxs-lookup"><span data-stu-id="f86a9-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="f86a9-158">この方法は、ビューテンプレート内で作成する HTML UI がドメインモデルオブジェクトに対して比較的厳密に対応するシナリオに適しています。</span><span class="sxs-lookup"><span data-stu-id="f86a9-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="f86a9-159">そうではないシナリオでは、使用できるオプションの1つとして、オブジェクトモデルがビューによって消費されるように最適化され、基になるドメインモデルオブジェクトと完全に異なる場合がある、カスタムの形式のビューモデルクラスを作成する方法があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="f86a9-160">たとえば、複数のモデルオブジェクトから収集されたさまざまなプロパティ名や集計プロパティを公開する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="f86a9-161">カスタム整形型のビューモデルクラスを使用すると、コントローラーからビューにデータを渡したり、コントローラーのアクションメソッドにポストバックされるフォームデータを処理したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="f86a9-162">この後のシナリオでは、アクションメソッドを使用して、フォームポストされたデータを含むビューモデルオブジェクトを更新してから、ビューモデルインスタンスを使用して実際のドメインモデルオブジェクトをマップまたは取得することができます。</span><span class="sxs-lookup"><span data-stu-id="f86a9-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="f86a9-163">カスタムの型のビューモデルクラスでは、柔軟性を高めることができます。また、ビューテンプレート内のレンダリングコードや、アクションメソッド内のフォームポストコードを見つけるたびに調査して、複雑になることがあります。</span><span class="sxs-lookup"><span data-stu-id="f86a9-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="f86a9-164">これは多くの場合、ドメインモデルが生成する UI に明確に対応していないこと、および中間のカスタムのビューモデルクラスが役立つことを示しています。</span><span class="sxs-lookup"><span data-stu-id="f86a9-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="f86a9-165">次の手順</span><span class="sxs-lookup"><span data-stu-id="f86a9-165">Next Step</span></span>

<span data-ttu-id="f86a9-166">次に、パーシャルとマスターページを使用して、アプリケーション全体で UI を再利用し、共有する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f86a9-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f86a9-167">[前へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [次へ](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="f86a9-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
